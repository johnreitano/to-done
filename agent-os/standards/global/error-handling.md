## Error Handling in Next.js/TypeScript

### API Route Error Handling
```typescript
// app/api/tasks/route.ts
import { NextResponse } from 'next/server';

export async function POST(request: Request) {
  try {
    const body = await request.json();
    // ... validation and logic
    return NextResponse.json({ data }, { status: 201 });
  } catch (error) {
    if (error instanceof ValidationError) {
      return NextResponse.json(
        { error: error.message },
        { status: 400 }
      );
    }
    console.error('Task creation failed:', error);
    return NextResponse.json(
      { error: 'Failed to create task' },
      { status: 500 }
    );
  }
}
```

### Supabase Error Handling
```typescript
const { data, error } = await supabase
  .from('tasks')
  .select('*');

if (error) {
  // Log full error for debugging
  console.error('Supabase query failed:', error);
  // Return user-friendly message
  throw new Error('Failed to load tasks');
}
```

### React Error Boundaries
- Use `error.tsx` files in App Router for route-level boundaries
- Provide user-friendly fallback UI with retry options
- Log errors to monitoring service (Sentry)

### Client-Side Error Handling
```typescript
// In React components
const [error, setError] = useState<string | null>(null);

async function handleSubmit() {
  try {
    setError(null);
    await createTask(data);
  } catch (e) {
    setError('Failed to create task. Please try again.');
  }
}
```

### Best Practices
- Never expose stack traces or internal errors to users
- Log errors with context (user ID, action, input)
- Use typed error classes for different error categories
- Implement retry logic with exponential backoff for external APIs (Stripe, OpenAI)
