## Supabase Query Standards

### Basic CRUD Operations
```typescript
// lib/supabase/queries/tasks.ts
import { createClient } from '@/lib/supabase/server';

export async function getTasks(userId: string) {
  const supabase = await createClient();
  const { data, error } = await supabase
    .from('tasks')
    .select('id, title, completed, deadline')
    .eq('user_id', userId)
    .order('created_at', { ascending: false });

  if (error) throw new Error('Failed to fetch tasks');
  return data;
}

export async function createTask(task: TaskInsert) {
  const supabase = await createClient();
  const { data, error } = await supabase
    .from('tasks')
    .insert(task)
    .select()
    .single();

  if (error) throw new Error('Failed to create task');
  return data;
}
```

### Select Only What You Need
```typescript
// Good: Select specific columns
.select('id, title, completed')

// Avoid: Select all columns
.select('*')
```

### Joins and Relations
```typescript
// Fetch tasks with list info
const { data } = await supabase
  .from('tasks')
  .select(`
    id,
    title,
    list:lists(id, name)
  `)
  .eq('user_id', userId);
```

### Filtering and Pagination
```typescript
const { data } = await supabase
  .from('tasks')
  .select('*')
  .eq('user_id', userId)
  .eq('completed', false)
  .order('deadline', { ascending: true, nullsFirst: false })
  .range(0, 19); // First 20 items
```

### Transactions
Use Supabase RPC for multi-statement transactions:

```sql
-- Create function in migration
CREATE FUNCTION complete_task_with_subtasks(task_id UUID)
RETURNS void AS $$
BEGIN
  UPDATE tasks SET completed = true WHERE id = task_id;
  UPDATE subtasks SET completed = true WHERE parent_id = task_id;
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;
```

```typescript
await supabase.rpc('complete_task_with_subtasks', { task_id: taskId });
```

### Error Handling
Always check for errors:

```typescript
const { data, error } = await supabase.from('tasks').select('*');
if (error) {
  console.error('Query failed:', error.message);
  throw new Error('Failed to load tasks');
}
```

### Client Types
- **Server:** `createClient()` from `@/lib/supabase/server` (API routes, server components)
- **Client:** `createClient()` from `@/lib/supabase/client` (client components)
