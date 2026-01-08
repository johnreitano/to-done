---
name: Global Validation
description: Rails validation patterns. Use this skill when adding validations to models or handling user input.
---

# Global Validation

## When to use this skill:
- When defining model validations
- When validating form input
- When sanitizing user data

## Instructions

### Model Validations
Use ActiveRecord validations:

```ruby
class Todo < ApplicationRecord
  validates :title, presence: true, length: { maximum: 255 }
  validates :status, inclusion: { in: %w[pending completed] }, allow_nil: true
  validates :priority, numericality: { in: 1..5 }, allow_nil: true
end
```

### Common Validators

```ruby
# Presence
validates :title, presence: true

# Length
validates :title, length: { minimum: 1, maximum: 255 }

# Format
validates :email, format: { with: URI::MailTo::EMAIL_REGEXP }

# Inclusion
validates :status, inclusion: { in: %w[active archived] }

# Uniqueness (use with database constraint)
validates :slug, uniqueness: true

# Custom validation
validate :due_date_not_in_past

def due_date_not_in_past
  return unless due_date.present? && due_date < Date.current
  errors.add(:due_date, "can't be in the past")
end
```

### Database Constraints
Back up model validations with database constraints:

```ruby
# Migration
add_column :todos, :title, :string, null: false
add_index :todos, :slug, unique: true
```

### Strong Parameters
Whitelist permitted attributes in controllers:

```ruby
def todo_params
  params.require(:todo).permit(:title, :completed, :due_date)
end
```

### Sanitization
Rails automatically escapes output. For input sanitization:

```ruby
before_save :sanitize_title

def sanitize_title
  self.title = title.strip.gsub(/\s+/, " ")
end
```
