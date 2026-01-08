---
name: Global Commenting
description: Code commenting guidelines. Use this skill when deciding whether and how to add comments to code.
---

# Global Commenting

## When to use this skill:
- When writing complex logic that needs explanation
- When reviewing code for documentation
- When deciding if a comment is necessary

## Instructions

### Self-Documenting Code First
Write code that explains itself through clear naming:

```ruby
# Bad - needs comment to explain
# Check if todo is overdue
if todo.due_date && todo.due_date < Date.current && !todo.completed

# Good - self-documenting
if todo.overdue?

# In model
def overdue?
  due_date.present? && due_date < Date.current && !completed?
end
```

### When to Comment
Add comments for:
- Complex business logic that isn't obvious
- Non-obvious "why" decisions
- Workarounds with context

```ruby
# Calculate priority based on due date proximity and user settings
# See: https://example.com/docs/priority-algorithm
def calculate_priority
  # ...complex logic...
end

# HACK: PostgreSQL doesn't support partial unique indexes on NULL values
# Remove this constraint when we upgrade to PostgreSQL 15+
add_index :todos, :external_id, unique: true, where: "external_id IS NOT NULL"
```

### Don't Comment
- What the code does (let the code speak)
- Obvious logic
- Temporary changes or fixes
- Commented-out code (delete it)

```ruby
# Bad
# Increment counter by 1
counter += 1

# Bad - delete instead of commenting out
# def old_method
#   ...
# end
```

### YARD for Public APIs
Use YARD format for public methods if documentation is needed:

```ruby
# Marks the todo as completed and records completion time.
#
# @return [Boolean] true if save succeeded
def complete!
  update(completed: true, completed_at: Time.current)
end
```
