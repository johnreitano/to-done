## Validation Standards

### Server-Side Validation (Required)
Always validate in API routes and server actions—never trust client data.

```typescript
// Using Zod for schema validation
import { z } from 'zod';

const createTaskSchema = z.object({
  title: z.string().min(1).max(200),
  description: z.string().max(2000).optional(),
  deadline: z.string().datetime().optional(),
  listId: z.string().uuid().optional(),
});

export async function POST(request: Request) {
  const body = await request.json();
  const result = createTaskSchema.safeParse(body);

  if (!result.success) {
    return NextResponse.json(
      { errors: result.error.flatten().fieldErrors },
      { status: 400 }
    );
  }
  // Use result.data (typed and validated)
}
```

### Client-Side Validation (UX Only)
Use for immediate feedback; duplicate all checks server-side.

```typescript
// React Hook Form with Zod
const form = useForm<CreateTaskInput>({
  resolver: zodResolver(createTaskSchema),
});
```

### Supabase Row-Level Security
Enforce access control at database level:

```sql
-- Users can only read their own tasks
CREATE POLICY "Users read own tasks"
ON tasks FOR SELECT
USING (auth.uid() = user_id);
```

### Validation Principles
- **Fail early:** Validate at API boundary before any processing
- **Specific errors:** Return field-level error messages
- **Allowlists:** Define allowed values explicitly (e.g., status enum)
- **Sanitization:** Supabase parameterized queries prevent SQL injection; sanitize HTML for display
