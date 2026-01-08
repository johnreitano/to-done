---
name: Frontend Accessibility
description: Accessibility (a11y) patterns. Use this skill when creating views to ensure they're usable by everyone.
---

# Frontend Accessibility

## When to use this skill:
- When creating any user-facing views
- When adding interactive elements
- When reviewing markup for a11y compliance

## Instructions

### Semantic HTML
Use appropriate elements:

```erb
<!-- Bad -->
<div class="button" onclick="submit()">Submit</div>

<!-- Good -->
<button type="submit">Submit</button>

<!-- Use semantic elements -->
<main>
  <nav>...</nav>
  <article>...</article>
  <aside>...</aside>
</main>
```

### Form Labels
Always associate labels with inputs:

```erb
<%= form_with model: @todo do |f| %>
  <%= f.label :title, "Todo title" %>
  <%= f.text_field :title %>
<% end %>
```

### Keyboard Navigation
Ensure all interactive elements are keyboard accessible:

```css
/* Visible focus indicators */
:focus {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
}

/* Never remove focus outline entirely */
:focus:not(:focus-visible) {
  outline: none;
}

:focus-visible {
  outline: 2px solid var(--color-primary);
}
```

### Color Contrast
Maintain 4.5:1 contrast ratio for normal text:

```css
/* Good contrast */
.text {
  color: #374151;  /* Dark gray on white */
}

/* Don't rely solely on color */
.error {
  color: #dc2626;
  border-left: 3px solid #dc2626;  /* Visual indicator beyond color */
}
```

### Alt Text
Provide meaningful alt text for images:

```erb
<%= image_tag "check.svg", alt: "Completed" %>
<%= image_tag "decorative.png", alt: "" %>  <!-- Empty for decorative -->
```

### ARIA When Needed
Use ARIA only when semantic HTML isn't sufficient:

```erb
<button aria-expanded="false" aria-controls="menu">Menu</button>
<div id="menu" hidden>...</div>
```
