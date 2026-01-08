---
name: Frontend Components
description: Rails view and partial patterns. Use this skill when creating ERB templates, partials, or view helpers.
---

# Frontend Components

## When to use this skill:
- When creating views in `app/views/`
- When extracting reusable partials
- When using view helpers
- When integrating Stimulus controllers

## Instructions

### Partials for Reusability
Extract repeated markup into partials:

```erb
<!-- app/views/todos/_todo.html.erb -->
<div id="<%= dom_id(todo) %>" class="todo-item">
  <span class="<%= 'completed' if todo.completed? %>">
    <%= todo.title %>
  </span>
  <%= button_to "Delete", todo, method: :delete %>
</div>

<!-- app/views/todos/index.html.erb -->
<%= render @todos %>
```

### Naming Conventions
- Partials start with underscore: `_todo.html.erb`
- Use `dom_id(record)` for unique element IDs
- Name partials after the model they represent

### Forms with form_with
Use Rails form helpers:

```erb
<%= form_with model: @todo do |f| %>
  <%= f.text_field :title, placeholder: "Add a todo..." %>
  <%= f.submit "Add" %>
<% end %>
```

### Stimulus Controllers
For JavaScript interactivity:

```erb
<div data-controller="todo">
  <input data-todo-target="input" data-action="keydown.enter->todo#submit">
</div>
```

```javascript
// app/javascript/controllers/todo_controller.js
import { Controller } from "@hotwired/stimulus"

export default class extends Controller {
  static targets = ["input"]

  submit() {
    // Handle submission
  }
}
```

### Keep Views Simple
Move complex logic to helpers or presenters—views should focus on presentation.
