## Next.js Project Conventions

### Project Structure
```
app/                    # Next.js App Router pages
  (auth)/              # Route groups for layouts
  api/                 # API routes
components/            # React components
  ui/                  # Radix-based UI primitives
lib/                   # Utilities and helpers
  supabase/           # Supabase client and queries
  stripe/             # Stripe integration
hooks/                 # Custom React hooks
types/                 # TypeScript type definitions
```

### Environment Configuration
- Use `.env.local` for local development (gitignored)
- Prefix client-exposed vars with `NEXT_PUBLIC_`
- Never commit secrets; use Vercel/hosting env vars for production

```bash
# .env.local example
NEXT_PUBLIC_SUPABASE_URL=https://xxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJ...
SUPABASE_SERVICE_ROLE_KEY=eyJ...  # Server-only
```

### Dependency Management
- Use `pnpm` for package management (faster, strict)
- Pin major versions in package.json
- Audit dependencies before adding; prefer established packages

### Feature Development
- Use feature flags via environment variables for incomplete features
- Keep `main` branch deployable at all times
