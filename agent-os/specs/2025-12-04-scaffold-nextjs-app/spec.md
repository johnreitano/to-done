# Specification: Scaffold Next.js App

## Goal

Create the foundational Next.js application scaffold for the To-Done task management application, establishing the project structure, development tooling, and SDK integrations that all future features will build upon.

## User Stories

- As a developer, I want a properly configured Next.js project so that I can begin implementing task management features
- As a developer, I want pre-configured SDK clients for Supabase, Stripe, and OpenAI so that I can integrate these services without setup overhead

## Specific Requirements

**Next.js App Router Initialization**
- Use `create-next-app` with App Router (not Pages Router)
- Enable TypeScript with strict mode
- Include `src/` directory option disabled (use root-level app/ folder)
- Configure for production-ready defaults

**TypeScript Configuration**
- Enable strict mode for maximum type safety
- Configure path aliases for clean imports (e.g., `@/components`, `@/lib`)
- Include proper tsconfig.json with Next.js recommended settings

**Tailwind CSS Setup**
- Install and configure Tailwind CSS with PostCSS
- Create tailwind.config.ts with content paths for app/, components/
- Include base Tailwind directives in global stylesheet
- Configure for dark mode support (class-based)

**Standard Folder Structure**
- `app/` - Next.js App Router pages, layouts, and API routes
- `components/` - Reusable React components (with ui/ subdirectory for primitives)
- `lib/` - Utility functions, SDK clients, and shared logic
- `types/` - TypeScript type definitions and interfaces
- `hooks/` - Custom React hooks

**ESLint and Prettier Configuration**
- Use Next.js recommended ESLint configuration
- Add Prettier for code formatting with consistent rules
- Configure ESLint to work with Prettier (eslint-config-prettier)
- Include scripts in package.json for linting and formatting

**Environment Variable Configuration**
- Create `.env.example` with all required placeholders
- Include Supabase variables: NEXT_PUBLIC_SUPABASE_URL, NEXT_PUBLIC_SUPABASE_ANON_KEY, SUPABASE_SERVICE_ROLE_KEY
- Include Stripe variables: NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY, STRIPE_SECRET_KEY, STRIPE_WEBHOOK_SECRET, STRIPE_PRICE_ID_PAID_TIER
- Include OpenAI variable: OPENAI_API_KEY
- Include app variable: NEXT_PUBLIC_APP_URL
- Add `.env.local` to .gitignore

**Supabase SDK Integration**
- Install `@supabase/supabase-js`
- Create typed Supabase client in `lib/supabase/client.ts` for browser usage
- Create server-side Supabase client in `lib/supabase/server.ts`
- Export client creation functions with proper typing

**Stripe SDK Integration**
- Install `stripe` (server SDK) and `@stripe/stripe-js` (client SDK)
- Create Stripe server client in `lib/stripe/server.ts`
- Create Stripe client loader in `lib/stripe/client.ts` using loadStripe
- Configure with TypeScript for proper API version typing

**OpenAI SDK Integration**
- Install `openai` package
- Create OpenAI client in `lib/openai/client.ts`
- Configure with proper TypeScript types
- Include helper for server-side only usage

**Radix UI Foundation**
- Install core Radix UI primitives: @radix-ui/react-dialog, @radix-ui/react-dropdown-menu, @radix-ui/react-popover, @radix-ui/react-select, @radix-ui/react-toggle-group
- Install utility: @radix-ui/react-slot for component composition
- Create `lib/utils.ts` with cn() helper for Tailwind class merging (clsx + tailwind-merge)

## Visual Design

No visual assets provided - this is an infrastructure/scaffold specification.

## Existing Code to Leverage

**Tech Stack Document (agent-os/product/tech-stack.md)**
- Reference for all package versions and configurations
- Environment variable naming conventions defined here
- SDK integration patterns and purposes documented
- Use as source of truth for architectural decisions

## Out of Scope

- User authentication implementation (login, signup, logout flows)
- Database schema creation or migrations
- Payment processing logic or Stripe checkout flows
- AI feature implementation or OpenAI API calls
- UI components beyond minimal app shell
- Deployment configuration (Vercel, etc.)
- Testing setup (Jest, React Testing Library)
- Database seeding or sample data
- API route implementations
- Middleware configuration
