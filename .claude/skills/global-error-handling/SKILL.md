---
name: Global Error Handling
description: Rails error handling patterns. Use this skill when handling exceptions, validation errors, or displaying error messages.
---

# Global Error Handling

## When to use this skill:
- When rescuing exceptions in controllers
- When displaying validation errors to users
- When handling record not found scenarios

## Instructions

### Controller Error Handling
Handle common errors at the controller level:

```ruby
class ApplicationController < ActionController::Base
  rescue_from ActiveRecord::RecordNotFound, with: :not_found

  private

  def not_found
    render file: Rails.public_path.join("404.html"), status: :not_found, layout: false
  end
end
```

### Validation Errors
Display clear, field-specific errors:

```erb
<%= form_with model: @todo do |f| %>
  <% if @todo.errors.any? %>
    <div class="error-summary">
      <h2><%= pluralize(@todo.errors.count, "error") %> prevented saving:</h2>
      <ul>
        <% @todo.errors.full_messages.each do |message| %>
          <li><%= message %></li>
        <% end %>
      </ul>
    </div>
  <% end %>

  <div class="field <%= 'field-error' if @todo.errors[:title].any? %>">
    <%= f.label :title %>
    <%= f.text_field :title %>
  </div>

  <%= f.submit %>
<% end %>
```

### Flash Messages
Use flash for user feedback:

```ruby
def create
  @todo = Todo.new(todo_params)
  if @todo.save
    redirect_to todos_path, notice: "Todo created successfully."
  else
    render :index, status: :unprocessable_entity
  end
end
```

```erb
<% flash.each do |type, message| %>
  <div class="flash flash-<%= type %>"><%= message %></div>
<% end %>
```

### Fail Fast
Validate input early and return clear errors before processing:

```ruby
def update
  @todo = Todo.find(params[:id])
  # Fail fast if record doesn't exist (handled by rescue_from)
  # Fail fast if params invalid (handled by validation)
  @todo.update!(todo_params)
end
```
