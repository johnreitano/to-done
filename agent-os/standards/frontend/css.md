## Tailwind CSS Standards

### Utility-First Approach
Use Tailwind utilities directly in JSX. Avoid custom CSS except for complex animations.

```tsx
// Good: Tailwind utilities
<button className="rounded-lg bg-blue-600 px-4 py-2 text-white hover:bg-blue-700">
  Save Task
</button>

// Avoid: Custom CSS classes
<button className="save-button">Save Task</button>
```

### Class Organization
Order classes consistently: layout → spacing → sizing → typography → colors → effects

```tsx
<div className="flex items-center gap-4 p-4 w-full text-sm text-gray-900 bg-white rounded-lg shadow-sm">
```

### Use cn() for Conditional Classes
```tsx
import { cn } from '@/lib/utils';

<div className={cn(
  'rounded-lg border p-4',
  isCompleted && 'bg-gray-50 opacity-60',
  className
)}>
```

### Design Tokens via Tailwind Config
Define colors, spacing, fonts in `tailwind.config.ts`:

```typescript
// tailwind.config.ts
export default {
  theme: {
    extend: {
      colors: {
        primary: '#3b82f6',
        'primary-hover': '#2563eb',
      },
    },
  },
};
```

### Responsive Design
Mobile-first with breakpoint prefixes:

```tsx
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
```

### Avoid
- `@apply` in CSS files (defeats utility purpose)
- Inline styles except for dynamic values
- Overriding Radix component internals with !important
