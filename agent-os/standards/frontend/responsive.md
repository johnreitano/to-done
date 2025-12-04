## Responsive Design with Tailwind

### Mobile-First Breakpoints
Start with mobile styles, add breakpoint prefixes for larger screens:

```tsx
// Mobile: 1 column, Tablet: 2 columns, Desktop: 3 columns
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  {tasks.map(task => <TaskCard key={task.id} task={task} />)}
</div>
```

### Tailwind Breakpoints
- `sm`: 640px+
- `md`: 768px+ (tablet)
- `lg`: 1024px+ (desktop)
- `xl`: 1280px+

### Touch Targets
Minimum 44x44px for mobile tap targets:

```tsx
<button className="min-h-[44px] min-w-[44px] p-3">
  <TrashIcon className="h-5 w-5" />
</button>
```

### Responsive Typography
```tsx
<h1 className="text-2xl md:text-3xl lg:text-4xl font-bold">
  My Tasks
</h1>
```

### Show/Hide Based on Screen Size
```tsx
// Hide on mobile, show on desktop
<Sidebar className="hidden lg:block" />

// Show on mobile only
<MobileNav className="lg:hidden" />
```

### Container and Max Width
```tsx
<main className="container mx-auto px-4 max-w-4xl">
  {/* Content */}
</main>
```

### Testing
- Use browser DevTools device emulation
- Test actual devices when possible
- Verify touch interactions on mobile
