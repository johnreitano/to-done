# Tech Stack

## Frontend Framework

### Next.js
- **Purpose:** React-based framework providing server-side rendering, API routes, and optimized builds
- **Why:** Enables SEO-friendly task sharing pages via OpenGraph metadata, efficient routing, and integrated API layer
- **Version:** Latest stable (App Router recommended for modern features)

### React
- **Purpose:** UI component library for building interactive user interfaces
- **Why:** Component-based architecture enables reusable task cards, list views, and form elements
- **Version:** 18+ (bundled with Next.js)

## UI & Styling

### Radix UI
- **Purpose:** Unstyled, accessible component primitives
- **Why:** Provides headless components (modals, dropdowns, toggles) ensuring WCAG compliance without imposing design constraints
- **Components Used:** Dialog, Dropdown Menu, Toggle Group (for view switching), Popover, Select

### Tailwind CSS (Recommended)
- **Purpose:** Utility-first CSS framework
- **Why:** Rapid styling of Radix components, responsive design, and consistent design system
- **Note:** While not explicitly mentioned, Radix UI pairs well with Tailwind for production-ready styling

## Backend & Database

### Supabase
- **Purpose:** Backend-as-a-Service providing PostgreSQL database, authentication, real-time subscriptions, and storage
- **Why:**
  - **Database:** Relational data model perfect for tasks, users, lists, and sharing relationships
  - **Auth:** Built-in email/password authentication with JWT tokens
  - **Realtime:** WebSocket subscriptions for live shared list updates (paid tier)
  - **Row Level Security:** Database-level permission enforcement for data access control
  - **Storage:** File uploads for future task attachments
- **Key Features Used:**
  - PostgreSQL database for data persistence
  - Supabase Auth for user management
  - Realtime subscriptions for collaborative features
  - Edge Functions for scheduled reminders and background jobs

## Payment Processing

### Stripe
- **Purpose:** Payment processing and subscription management
- **Why:** Industry-standard for SaaS billing with robust webhook system, subscription lifecycle management, and payment security
- **Integration Points:**
  - Checkout Sessions for upgrade flow
  - Customer Portal for subscription management
  - Webhooks for subscription state changes (activate/cancel/update)
  - Price IDs for free vs paid tier management

## AI & Machine Learning

### OpenAI SDK
- **Purpose:** Integration with OpenAI's language models for AI-powered task assistance
- **Why:** Provides natural language understanding for task breakdown, deadline estimation, and description generation
- **Features Used:**
  - GPT models for task analysis and suggestions
  - Structured outputs for generating subtasks
  - Prompt engineering for context-aware assistance
- **Access Control:** Limited to paid tier users only

## Development Tools

### TypeScript (Recommended)
- **Purpose:** Type-safe JavaScript superset
- **Why:** Catches errors at compile time, improves code maintainability, and provides better IDE support
- **Note:** Essential for large-scale Next.js applications with complex data models

### ESLint & Prettier (Recommended)
- **Purpose:** Code linting and formatting
- **Why:** Maintains consistent code style and catches common errors

## Deployment & Hosting

### Vercel (Recommended)
- **Purpose:** Deployment platform optimized for Next.js
- **Why:** Zero-config deployments, automatic HTTPS, edge functions, and preview deployments
- **Alternative:** Any Node.js-compatible hosting (Netlify, AWS, Railway)

### Supabase Cloud
- **Purpose:** Managed Supabase instance
- **Why:** Production-ready PostgreSQL, automatic backups, and scalability without infrastructure management

## Environment & Configuration

### Environment Variables
Required configuration:
```
# Supabase
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=

# Stripe
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=
STRIPE_PRICE_ID_PAID_TIER=

# OpenAI
OPENAI_API_KEY=

# App
NEXT_PUBLIC_APP_URL= (for OpenGraph links)
```

## Data Architecture

### Database Schema (Supabase PostgreSQL)

**Core Tables:**
- `users` - User accounts (managed by Supabase Auth)
- `profiles` - Extended user data (subscription tier, preferences)
- `tasks` - Individual task items with title, description, deadline, assignee
- `lists` - Shared lists for paid users
- `list_members` - Many-to-many relationship between lists and users
- `share_tokens` - Public share links for individual tasks

**Key Relationships:**
- Users have many tasks (creator)
- Tasks belong to lists (optional for free users, required for shared lists)
- Lists have many members (paid tier only)
- Tasks have share tokens for public access

## Third-Party Services Summary

| Service | Purpose | Tier Availability |
|---------|---------|-------------------|
| Supabase | Database, Auth, Realtime | All tiers |
| Stripe | Payment processing | Paid tier only |
| OpenAI | AI task assistance | Paid tier only |
| Email Service | Reminders (future) | Paid tier only |

## Security Considerations

- **Authentication:** Supabase JWT tokens with HTTP-only cookies
- **Authorization:** Row Level Security policies in Supabase for data access
- **API Security:** Middleware to verify user subscription tier before accessing paid features
- **Payment Security:** Stripe handles all PCI compliance, webhooks verified with signatures
- **Public Sharing:** Share tokens are cryptographically random UUIDs with read-only access
