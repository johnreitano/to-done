---
name: Backend Migrations
description: Rails database migration patterns. Use this skill when creating, modifying, or running migrations in db/migrate/.
---

# Backend Migrations

## When to use this skill:
- When creating new database tables or columns
- When modifying existing schema
- When adding indexes or constraints
- When working with files in `db/migrate/`

## Instructions

### Always Reversible
Implement `change` method for auto-reversible migrations, or explicit `up`/`down` methods:

```ruby
# Good - auto-reversible
class AddCompletedToTodos < ActiveRecord::Migration[7.1]
  def change
    add_column :todos, :completed, :boolean, default: false, null: false
  end
end

# When reversal isn't obvious
class ChangeStatusColumn < ActiveRecord::Migration[7.1]
  def up
    change_column :todos, :status, :string
  end

  def down
    change_column :todos, :status, :integer
  end
end
```

### Small, Focused Changes
One logical change per migration for easier debugging and rollback.

### Index Best Practices
- Add indexes on foreign keys and frequently queried columns
- Use `algorithm: :concurrently` for large tables in production (requires `disable_ddl_transaction!`)

```ruby
class AddIndexToTodosUserId < ActiveRecord::Migration[7.1]
  disable_ddl_transaction!

  def change
    add_index :todos, :user_id, algorithm: :concurrently
  end
end
```

### Naming Conventions
Use descriptive names: `AddCompletedToTodos`, `CreateTodos`, `RemoveStatusFromTodos`

### Never Modify Deployed Migrations
After pushing to production, create a new migration for changes.
