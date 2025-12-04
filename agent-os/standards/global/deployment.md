## Vercel + Supabase Deployment

### Environments
- `main` branch → Production
- Preview deployments for PRs (automatic)
- Use Vercel environment variables per environment

### CI/CD Flow
1. Push to branch → Vercel preview deployment
2. PR merge to main → Production deployment
3. Database migrations run via Supabase CLI or dashboard

### Supabase Migrations
```bash
# Generate migration from local changes
supabase db diff -f migration_name

# Apply migrations
supabase db push

# Zero-downtime pattern
# 1. Add nullable column
# 2. Deploy code that writes to it
# 3. Backfill existing data
# 4. Make column non-null in new migration
```

### Environment Variables
**Vercel Dashboard (per environment):**
- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`
- `SUPABASE_SERVICE_ROLE_KEY`
- `STRIPE_SECRET_KEY`
- `STRIPE_WEBHOOK_SECRET`
- `OPENAI_API_KEY`

### Monitoring
- Vercel Analytics for performance metrics
- Sentry or similar for error tracking
- Supabase dashboard for database monitoring

### Rollback
```bash
# Vercel: Promote previous deployment
vercel rollback

# Database: Create reversing migration (no automatic rollback)
```
