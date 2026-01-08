---
name: Global Conventions
description: Rails project conventions. Use this skill when organizing code, files, or following team practices.
---

# Global Conventions

## When to use this skill:
- When creating new files or directories
- When following Rails conventions
- When setting up project structure

## Instructions

### Rails Directory Structure
Follow Rails conventions:

```
app/
├── controllers/     # Handle HTTP requests
├── models/          # Business logic and data
├── views/           # ERB templates
├── helpers/         # View helper methods
├── javascript/      # Stimulus controllers
│   └── controllers/
└── assets/
    └── stylesheets/ # CSS files

config/
├── routes.rb        # URL routing
└── database.yml     # Database config

db/
├── migrate/         # Schema migrations
├── schema.rb        # Current schema
└── seeds.rb         # Seed data

test/
├── models/          # Model tests
├── controllers/     # Controller tests
├── fixtures/        # Test data
└── test_helper.rb   # Test configuration
```

### File Naming
- Models: `app/models/todo.rb` → `class Todo`
- Controllers: `app/controllers/todos_controller.rb` → `class TodosController`
- Views: `app/views/todos/index.html.erb`
- Migrations: `db/migrate/20240101120000_create_todos.rb`

### Environment Variables
Use Rails credentials or environment variables for secrets:

```ruby
# Never commit secrets
# config/credentials.yml.enc (encrypted)

# Access in code
Rails.application.credentials.secret_key
ENV["DATABASE_URL"]
```

### Version Control
- Write clear commit messages
- Never commit `.env`, credentials, or `config/master.key`
- Keep `db/schema.rb` in version control
