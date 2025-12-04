## React Component Standards

### Component Structure
```tsx
// components/TaskCard.tsx
interface TaskCardProps {
  task: Task;
  onComplete?: (id: string) => void;
  className?: string;
}

export function TaskCard({ task, onComplete, className }: TaskCardProps) {
  // Hooks at top
  const [isExpanded, setIsExpanded] = useState(false);

  // Event handlers
  function handleComplete() {
    onComplete?.(task.id);
  }

  // Render
  return (
    <div className={cn('rounded-lg border p-4', className)}>
      {/* ... */}
    </div>
  );
}
```

### Component Principles
- **Single responsibility:** One component, one purpose
- **Props interface:** Always define TypeScript interface for props
- **Optional className prop:** Allow style customization via Tailwind
- **Named exports:** Use named exports for components

### Server vs Client Components
```tsx
// Default: Server Component (no 'use client')
// - Fetch data directly
// - No hooks, no event handlers
// - Better performance

// Client Component: Add 'use client' when needed
'use client';
// - useState, useEffect, event handlers
// - Browser APIs
// - Interactivity required
```

### Composition over Configuration
```tsx
// Good: Composable
<Card>
  <CardHeader>
    <CardTitle>Tasks</CardTitle>
  </CardHeader>
  <CardContent>...</CardContent>
</Card>

// Avoid: Too many props
<Card title="Tasks" subtitle="..." headerIcon={...} />
```

### State Management
- **Local state first:** useState for component-specific state
- **Lift when needed:** Move state up only when siblings need it
- **Server state:** Use React Query or SWR for API data
- **Global state:** Context for auth/theme; avoid for most cases
