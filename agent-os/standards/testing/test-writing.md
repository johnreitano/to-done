## Testing Standards (Jest + React Testing Library)

### Testing Philosophy
- **Test core user flows only** during feature development
- **Defer edge cases** until dedicated testing phases
- **Test behavior, not implementation**

### Component Testing
```typescript
// components/TaskCard.test.tsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { TaskCard } from './TaskCard';

describe('TaskCard', () => {
  it('displays task title', () => {
    render(<TaskCard task={{ id: '1', title: 'Buy groceries', completed: false }} />);
    expect(screen.getByText('Buy groceries')).toBeInTheDocument();
  });

  it('calls onComplete when checkbox clicked', async () => {
    const onComplete = jest.fn();
    render(
      <TaskCard
        task={{ id: '1', title: 'Test', completed: false }}
        onComplete={onComplete}
      />
    );

    await userEvent.click(screen.getByRole('checkbox'));
    expect(onComplete).toHaveBeenCalledWith('1');
  });
});
```

### API Route Testing
```typescript
// app/api/tasks/route.test.ts
import { GET, POST } from './route';

// Mock Supabase
jest.mock('@/lib/supabase/server', () => ({
  createClient: () => ({
    auth: { getUser: () => ({ data: { user: { id: 'user-1' } } }) },
    from: () => ({
      select: () => ({ data: [{ id: '1', title: 'Task' }], error: null }),
    }),
  }),
}));

describe('GET /api/tasks', () => {
  it('returns tasks for authenticated user', async () => {
    const response = await GET();
    const data = await response.json();
    expect(data.tasks).toHaveLength(1);
  });
});
```

### Test Naming
Use descriptive names: `it('displays error when title is empty')`

### Mocking
- Mock Supabase client for database operations
- Mock Stripe for payment flows
- Mock OpenAI for AI features
- Use MSW for more complex API mocking

### What to Test
- Critical user paths (create task, complete task, share)
- Form validation feedback
- Loading and error states for important flows

### What NOT to Test (During Development)
- Radix UI component internals
- Tailwind styling
- TypeScript type checking
- Every possible error condition
