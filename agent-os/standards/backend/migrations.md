## Supabase Database Migrations

### Creating Migrations
```bash
# Generate migration from schema changes
supabase db diff -f add_deadline_to_tasks

# Creates: supabase/migrations/20241201120000_add_deadline_to_tasks.sql
```

### Migration File Structure
```sql
-- supabase/migrations/20241201120000_add_deadline_to_tasks.sql

-- Add deadline column (nullable first for zero-downtime)
ALTER TABLE tasks ADD COLUMN deadline TIMESTAMPTZ;

-- Add index for deadline queries
CREATE INDEX idx_tasks_deadline ON tasks (deadline) WHERE deadline IS NOT NULL;
```

### Zero-Downtime Pattern
For breaking changes, use multi-step approach:

1. **Migration 1:** Add nullable column
2. **Deploy:** Code writes to new column
3. **Backfill:** Update existing rows
4. **Migration 2:** Add NOT NULL constraint

```sql
-- Step 1: Add nullable
ALTER TABLE tasks ADD COLUMN status TEXT;

-- Step 3: Backfill (run manually or via Edge Function)
UPDATE tasks SET status = 'pending' WHERE status IS NULL;

-- Step 4: Add constraint
ALTER TABLE tasks ALTER COLUMN status SET NOT NULL;
ALTER TABLE tasks ADD CONSTRAINT tasks_status_check
  CHECK (status IN ('pending', 'completed', 'archived'));
```

### Row-Level Security (RLS)
Always add RLS policies for new tables:

```sql
-- Enable RLS
ALTER TABLE tasks ENABLE ROW LEVEL SECURITY;

-- Users can only access their own tasks
CREATE POLICY "Users manage own tasks"
ON tasks FOR ALL
USING (auth.uid() = user_id)
WITH CHECK (auth.uid() = user_id);
```

### Best Practices
- One logical change per migration
- Never modify deployed migrations
- Test migrations on staging first
- Include indexes for foreign keys and filtered queries
- Use `IF NOT EXISTS` for idempotency when appropriate
