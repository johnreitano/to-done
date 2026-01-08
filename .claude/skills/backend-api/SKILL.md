---
name: Backend API
description: Rails controller and routing patterns. Use this skill when creating controllers, defining routes, or handling HTTP requests.
---

# Backend API

## When to use this skill:
- When creating or modifying controllers in `app/controllers/`
- When defining routes in `config/routes.rb`
- When handling form submissions or API requests

## Instructions

### RESTful Routes
Use resourceful routing:

```ruby
# config/routes.rb
Rails.application.routes.draw do
  resources :todos, only: [:index, :create, :update, :destroy]
  root "todos#index"
end
```

### Controller Structure
Keep controllers thin—delegate business logic to models:

```ruby
class TodosController < ApplicationController
  def index
    @todos = Todo.recent
  end

  def create
    @todo = Todo.new(todo_params)
    if @todo.save
      redirect_to todos_path, notice: "Todo created."
    else
      render :index, status: :unprocessable_entity
    end
  end

  def update
    @todo = Todo.find(params[:id])
    if @todo.update(todo_params)
      redirect_to todos_path, notice: "Todo updated."
    else
      render :index, status: :unprocessable_entity
    end
  end

  def destroy
    @todo = Todo.find(params[:id])
    @todo.destroy
    redirect_to todos_path, notice: "Todo deleted."
  end

  private

  def todo_params
    params.require(:todo).permit(:title, :completed)
  end
end
```

### Strong Parameters
Always use `permit` to whitelist allowed attributes.

### HTTP Status Codes
- `200 OK` - successful GET
- `201 Created` - successful POST
- `204 No Content` - successful DELETE
- `422 Unprocessable Entity` - validation errors
- `404 Not Found` - record not found

### Respond to Turbo
For Hotwire/Turbo, return appropriate Turbo Stream responses when needed.
