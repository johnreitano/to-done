## Supabase/PostgreSQL Data Models

### TypeScript Type Generation
Generate types from Supabase schema:

```bash
supabase gen types typescript --local > types/database.ts
```

```typescript
// types/database.ts (generated)
export type Task = Database['public']['Tables']['tasks']['Row'];
export type TaskInsert = Database['public']['Tables']['tasks']['Insert'];
export type TaskUpdate = Database['public']['Tables']['tasks']['Update'];
```

### Table Conventions
```sql
CREATE TABLE tasks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  title TEXT NOT NULL,
  description TEXT,
  completed BOOLEAN NOT NULL DEFAULT false,
  deadline TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Auto-update updated_at
CREATE TRIGGER update_tasks_updated_at
  BEFORE UPDATE ON tasks
  FOR EACH ROW
  EXECUTE FUNCTION update_updated_at_column();
```

### Naming Conventions
- **Tables:** Plural, snake_case (`tasks`, `list_members`)
- **Columns:** snake_case (`user_id`, `created_at`)
- **Primary keys:** `id` (UUID)
- **Foreign keys:** `<table_singular>_id` (`user_id`, `list_id`)
- **Timestamps:** `created_at`, `updated_at`
- **Booleans:** Descriptive names (`completed`, `is_public`)

### Required Columns
Every table should have:
- `id` - UUID primary key
- `created_at` - Creation timestamp
- `updated_at` - Last modification timestamp

### Indexes
```sql
-- Foreign keys
CREATE INDEX idx_tasks_user_id ON tasks (user_id);
CREATE INDEX idx_tasks_list_id ON tasks (list_id);

-- Common query patterns
CREATE INDEX idx_tasks_deadline ON tasks (deadline) WHERE deadline IS NOT NULL;
CREATE INDEX idx_tasks_user_completed ON tasks (user_id, completed);
```

### Constraints
Use database constraints for data integrity:

```sql
ALTER TABLE tasks ADD CONSTRAINT tasks_title_not_empty CHECK (title <> '');
ALTER TABLE profiles ADD CONSTRAINT profiles_tier_check CHECK (tier IN ('free', 'paid'));
```
