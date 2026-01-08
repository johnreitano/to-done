---
name: Backend Models
description: ActiveRecord model patterns. Use this skill when creating or modifying models in app/models/.
---

# Backend Models

## When to use this skill:
- When creating new ActiveRecord models
- When adding validations or associations
- When defining scopes or callbacks
- When working with files in `app/models/`

## Instructions

### Naming
- **Model:** Singular `PascalCase` (e.g., `Todo`, `User`)
- **Table:** Plural `snake_case` (e.g., `todos`, `users`)
- **File:** `app/models/todo.rb`

### Structure Order
Organize model code in this order:

```ruby
class Todo < ApplicationRecord
  # 1. Constants
  STATUSES = %w[pending completed].freeze

  # 2. Associations
  belongs_to :user
  has_many :tags, dependent: :destroy

  # 3. Validations
  validates :title, presence: true, length: { maximum: 255 }
  validates :status, inclusion: { in: STATUSES }

  # 4. Scopes
  scope :completed, -> { where(completed: true) }
  scope :pending, -> { where(completed: false) }

  # 5. Callbacks (use sparingly)
  before_save :normalize_title

  # 6. Class methods
  def self.recent
    order(created_at: :desc)
  end

  # 7. Instance methods
  def complete!
    update!(completed: true)
  end

  private

  def normalize_title
    self.title = title.strip
  end
end
```

### Validations
- Use database constraints AND model validations for critical rules
- Prefer `presence: true` over `validates_presence_of`

### Timestamps
Rails adds `created_at` and `updated_at` by default—keep them.

### Foreign Keys
Always add foreign key constraints in migrations for referential integrity.
