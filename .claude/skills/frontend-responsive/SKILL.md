---
name: Frontend Responsive
description: Responsive design patterns. Use this skill when ensuring views work across screen sizes.
---

# Frontend Responsive

## When to use this skill:
- When creating layouts that must work on mobile and desktop
- When testing UI across different screen sizes
- When writing media queries

## Instructions

### Standard Breakpoints

```css
/* Mobile first - base styles */
.container { }

/* Tablet: 768px */
@media (min-width: 768px) { }

/* Desktop: 1024px */
@media (min-width: 1024px) { }

/* Large desktop: 1280px */
@media (min-width: 1280px) { }
```

### Fluid Layouts
Use flexible units:

```css
.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}
```

### Relative Units
Prefer `rem` for scalability:

```css
body {
  font-size: 16px;  /* Base */
}

h1 {
  font-size: 2rem;  /* 32px */
}

.small-text {
  font-size: 0.875rem;  /* 14px */
}
```

### Touch-Friendly Targets
Minimum 44x44px for tap targets:

```css
.button {
  min-height: 44px;
  min-width: 44px;
  padding: 0.75rem 1rem;
}
```

### Content Priority
Show essential content first on mobile, reveal secondary content on larger screens:

```css
.sidebar {
  display: none;
}

@media (min-width: 768px) {
  .sidebar {
    display: block;
  }
}
```
