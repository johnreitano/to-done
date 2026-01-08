---
name: Frontend CSS
description: Rails CSS and styling patterns. Use this skill when writing stylesheets or working with the asset pipeline.
---

# Frontend CSS

## When to use this skill:
- When creating or modifying stylesheets in `app/assets/stylesheets/`
- When styling views and components
- When organizing CSS architecture

## Instructions

### File Organization
Use Rails asset pipeline structure:

```
app/assets/stylesheets/
├── application.css      # Main manifest
├── components/          # Component-specific styles
│   └── _todo.css
├── layouts/             # Layout styles
│   └── _main.css
└── utilities/           # Helper classes
    └── _spacing.css
```

### Naming Convention
Use BEM-like naming for clarity:

```css
/* Block */
.todo-item { }

/* Element */
.todo-item__title { }
.todo-item__actions { }

/* Modifier */
.todo-item--completed { }
```

### CSS Variables for Consistency
Define design tokens:

```css
:root {
  --color-primary: #3b82f6;
  --color-success: #22c55e;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --border-radius: 4px;
}

.button {
  background: var(--color-primary);
  padding: var(--spacing-sm) var(--spacing-md);
  border-radius: var(--border-radius);
}
```

### Avoid !important
Manage specificity through proper selector structure rather than `!important`.

### Mobile-First
Write base styles for mobile, then add complexity for larger screens:

```css
.container {
  padding: 1rem;
}

@media (min-width: 768px) {
  .container {
    padding: 2rem;
  }
}
```
