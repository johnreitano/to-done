## Next.js API Routes (App Router)

### Route Handler Structure
```typescript
// app/api/tasks/route.ts
import { createClient } from '@/lib/supabase/server';
import { NextResponse } from 'next/server';

export async function GET() {
  const supabase = await createClient();
  const { data: { user } } = await supabase.auth.getUser();

  if (!user) {
    return NextResponse.json({ error: 'Unauthorized' }, { status: 401 });
  }

  const { data, error } = await supabase
    .from('tasks')
    .select('*')
    .eq('user_id', user.id);

  if (error) {
    return NextResponse.json({ error: 'Failed to fetch tasks' }, { status: 500 });
  }

  return NextResponse.json({ tasks: data });
}

export async function POST(request: Request) {
  // Validate, create, return 201
}
```

### Dynamic Routes
```typescript
// app/api/tasks/[id]/route.ts
export async function GET(
  request: Request,
  { params }: { params: { id: string } }
) {
  const { id } = params;
  // Fetch single task by id
}
```

### Response Conventions
- `200` - Success (GET, PUT, PATCH)
- `201` - Created (POST)
- `204` - No Content (DELETE)
- `400` - Validation error
- `401` - Unauthorized
- `403` - Forbidden (authenticated but not allowed)
- `404` - Not found
- `500` - Server error

### Authentication Pattern
```typescript
// Reusable auth check
async function requireAuth() {
  const supabase = await createClient();
  const { data: { user } } = await supabase.auth.getUser();
  if (!user) {
    throw new Error('Unauthorized');
  }
  return { supabase, user };
}
```

### Stripe Webhooks
```typescript
// app/api/webhooks/stripe/route.ts
export async function POST(request: Request) {
  const body = await request.text();
  const signature = request.headers.get('stripe-signature')!;

  const event = stripe.webhooks.constructEvent(
    body,
    signature,
    process.env.STRIPE_WEBHOOK_SECRET!
  );

  // Handle event types
  switch (event.type) {
    case 'checkout.session.completed':
      // Upgrade user tier
      break;
  }

  return NextResponse.json({ received: true });
}
```
