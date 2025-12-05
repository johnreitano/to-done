# Spec Requirements: Scaffold Next.js App

## Initial Description
Scaffold the Next.js app. This is the foundational setup for the To-Done task management application. The user wants to create the initial Next.js application scaffold that will serve as the base for all subsequent features in the roadmap.

## Requirements Discussion

### First Round Questions

**Q1:** Should we use Next.js App Router (recommended for new projects) or Pages Router?
**Answer:** Use Next.js App Router (not Pages Router)

**Q2:** Should TypeScript be enabled for the project?
**Answer:** Scaffold with TypeScript enabled

**Q3:** Should we include Tailwind CSS for styling?
**Answer:** Include Tailwind CSS

**Q4:** What folder structure should be used?
**Answer:** Use standard Next.js App Router folder structure (app/, components/, lib/, types/)

**Q5:** Should ESLint and Prettier configuration be included?
**Answer:** Include ESLint and Prettier configuration

**Q6:** Should placeholder environment variable files be included?
**Answer:** Include placeholder environment variable files (.env.example) for Supabase, Stripe, OpenAI

**Q7:** Should third-party SDKs (Supabase, Stripe, OpenAI) be installed upfront?
**Answer:** Yes, install Supabase, Stripe, and OpenAI SDKs upfront

**Q8:** Are there any features or configurations to exclude from this scaffold?
**Answer:** No exclusions - include everything

### Existing Code to Reference
No similar existing features identified for reference. This is a greenfield scaffold for a new project.

### Follow-up Questions
None required. All requirements are clear and comprehensive.

## Visual Assets

### Files Provided:
No visual assets provided.

### Visual Insights:
N/A - scaffolding spec does not require visual design assets.

## Requirements Summary

### Functional Requirements
- Initialize a new Next.js application using the App Router architecture
- Enable TypeScript for type-safe development
- Configure Tailwind CSS for utility-first styling
- Set up ESLint for code linting
- Set up Prettier for code formatting
- Create placeholder environment variable files for third-party services
- Install and configure Supabase SDK for database and authentication
- Install and configure Stripe SDK for payment processing
- Install and configure OpenAI SDK for AI features

### Folder Structure Requirements
The scaffold should include:
- `app/` - Next.js App Router pages and layouts
- `components/` - Reusable React components
- `lib/` - Utility functions, API clients, and shared logic
- `types/` - TypeScript type definitions

### Environment Variables
Create `.env.example` with placeholders for:
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
NEXT_PUBLIC_APP_URL=
```

### SDK Dependencies to Install
- `@supabase/supabase-js` - Supabase client SDK
- `stripe` - Stripe Node.js SDK
- `@stripe/stripe-js` - Stripe client-side SDK
- `openai` - OpenAI SDK

### Reusability Opportunities
- This is a new scaffold; no existing code to reuse
- Future specs will build upon this foundation

### Scope Boundaries
**In Scope:**
- Next.js App Router initialization with TypeScript
- Tailwind CSS configuration
- ESLint and Prettier setup
- Standard folder structure creation (app/, components/, lib/, types/)
- Environment variable placeholder files
- Installation of Supabase, Stripe, and OpenAI SDKs
- Basic SDK client initialization files in lib/

**Out of Scope:**
- Actual implementation of authentication flows
- Database schema creation
- Payment processing logic
- AI feature implementation
- UI components beyond the default Next.js starter
- Deployment configuration

### Technical Considerations
- Use latest stable versions of all dependencies
- Follow Next.js App Router conventions and best practices
- Ensure TypeScript strict mode is enabled
- Configure ESLint with Next.js recommended rules
- SDK clients should be initialized in lib/ folder with proper typing
- Environment variables should follow Next.js conventions (NEXT_PUBLIC_ prefix for client-side variables)
