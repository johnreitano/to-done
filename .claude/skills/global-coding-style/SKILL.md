---
name: Global Coding Style
description: Ruby and Rails coding conventions. Use this skill when writing any Ruby code, reviewing style consistency, or setting up linting rules.
---

# Global Coding Style

## When to use this skill:
- When writing Ruby classes, modules, or methods
- When naming variables, methods, or files
- When reviewing code for style consistency

## Instructions

### Naming Conventions
- **Classes/Modules:** `PascalCase` (e.g., `TodoItem`, `ApplicationController`)
- **Methods/Variables:** `snake_case` (e.g., `find_by_id`, `created_at`)
- **Constants:** `SCREAMING_SNAKE_CASE` (e.g., `MAX_RETRIES`)
- **Files:** `snake_case.rb` matching class name (e.g., `todo_item.rb`)
- **Predicates:** End with `?` (e.g., `completed?`, `valid?`)
- **Dangerous methods:** End with `!` (e.g., `save!`, `destroy!`)

### Formatting
- **Indentation:** 2 spaces (never tabs)
- **Line length:** Max 120 characters
- **Trailing whitespace:** Remove all trailing whitespace
- **Final newline:** Always end files with a newline

### Best Practices
- Prefer `&&`/`||` over `and`/`or` for boolean logic
- Use `%w[]` for word arrays: `%w[pending active completed]`
- Use `%i[]` for symbol arrays: `%i[create update destroy]`
- Prefer string interpolation over concatenation: `"Hello, #{name}"`
- Use guard clauses to reduce nesting

```ruby
# Bad
def process(item)
  if item.present?
    if item.valid?
      item.save
    end
  end
end

# Good
def process(item)
  return unless item.present?
  return unless item.valid?
  item.save
end
```

### Remove Dead Code
Delete unused code, commented-out blocks, and imports rather than leaving them as clutter.

### DRY Principle
Extract common logic into reusable methods or concerns, but avoid premature abstraction.
