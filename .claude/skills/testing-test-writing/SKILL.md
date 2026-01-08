---
name: Testing Test Writing
description: Minitest testing patterns for Rails. Use this skill when writing tests in the test/ directory.
---

# Testing Test Writing

## When to use this skill:
- When writing model, controller, or system tests
- When setting up test fixtures
- When following test-driven development

## Instructions

### Test Only Core User Flows
Focus on critical paths during development. Defer edge cases to dedicated testing phases.

### Test Structure
Use descriptive test names:

```ruby
# test/models/todo_test.rb
require "test_helper"

class TodoTest < ActiveSupport::TestCase
  test "validates presence of title" do
    todo = Todo.new(title: nil)
    assert_not todo.valid?
    assert_includes todo.errors[:title], "can't be blank"
  end

  test "marks todo as completed" do
    todo = todos(:pending)
    todo.complete!
    assert todo.completed?
  end
end
```

### Controller Tests

```ruby
# test/controllers/todos_controller_test.rb
require "test_helper"

class TodosControllerTest < ActionDispatch::IntegrationTest
  test "creates a new todo" do
    assert_difference "Todo.count", 1 do
      post todos_url, params: { todo: { title: "New task" } }
    end
    assert_redirected_to todos_url
  end

  test "shows validation error for blank title" do
    post todos_url, params: { todo: { title: "" } }
    assert_response :unprocessable_entity
  end
end
```

### Fixtures
Use fixtures for test data:

```yaml
# test/fixtures/todos.yml
pending:
  title: Buy groceries
  completed: false

completed:
  title: Walk the dog
  completed: true
```

### Fast Tests
- Mock external services
- Use `setup` and `teardown` for shared setup
- Keep unit tests isolated and fast
