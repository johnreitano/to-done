---
name: Backend Queries
description: ActiveRecord query patterns. Use this skill when writing database queries in controllers, models, or services.
---

# Backend Queries

## When to use this skill:
- When fetching data from the database
- When writing scopes or complex queries
- When optimizing database performance

## Instructions

### Use ActiveRecord Methods
Never interpolate user input—use parameterized queries:

```ruby
# Bad - SQL injection risk
Todo.where("title = '#{params[:title]}'")

# Good
Todo.where(title: params[:title])
Todo.where("title LIKE ?", "%#{params[:q]}%")
```

### Avoid N+1 Queries
Use `includes` for eager loading:

```ruby
# Bad - N+1 queries
todos = Todo.all
todos.each { |t| puts t.user.name }

# Good - single query with JOIN
todos = Todo.includes(:user)
todos.each { |t| puts t.user.name }
```

### Select Only Needed Columns
For performance, select specific columns when you don't need the full record:

```ruby
Todo.select(:id, :title).where(completed: false)
```

### Use Scopes
Define reusable query logic in the model:

```ruby
# In model
scope :recent, -> { order(created_at: :desc) }
scope :completed, -> { where(completed: true) }

# In controller
Todo.recent.completed.limit(10)
```

### Transactions
Wrap related operations in transactions:

```ruby
Todo.transaction do
  todo.update!(completed: true)
  todo.tags.destroy_all
end
```

### Indexes
Ensure columns in `where`, `order`, and `joins` are indexed.
