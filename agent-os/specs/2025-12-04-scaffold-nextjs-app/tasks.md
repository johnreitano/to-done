# Task Breakdown: Scaffold Next.js App

## Overview
Total Tasks: 19

## Task List

### Project Initialization

#### Task Group 1: Next.js Project Setup
**Dependencies:** None

- [ ] 1.0 Complete Next.js project initialization
  - [ ] 1.1 Run create-next-app with App Router and TypeScript
    - Use `npx create-next-app@latest . --typescript --tailwind --eslint --app --src-dir=false --import-alias="@/*"`
    - Confirm App Router is selected (not Pages Router)
    - Ensure project initializes in current directory
  - [ ] 1.2 Verify TypeScript strict mode configuration
    - Check tsconfig.json has `"strict": true`
    - Confirm path aliases are configured (`@/*` mapping)
    - Verify Next.js recommended settings are present
  - [ ] 1.3 Verify Tailwind CSS is properly configured
    - Check tailwind.config.ts exists with correct content paths
    - Verify PostCSS configuration is present
    - Confirm global styles include Tailwind directives
    - Add dark mode support (class-based) to tailwind config
  - [ ] 1.4 Run initial build to verify setup
    - Execute `npm run build` to confirm no errors
    - Verify development server starts with `npm run dev`

**Acceptance Criteria:**
- Next.js App Router project created with TypeScript
- Tailwind CSS configured and working
- Build completes without errors
- Dev server runs successfully

### Development Tooling

#### Task Group 2: ESLint and Prettier Configuration
**Dependencies:** Task Group 1

- [ ] 2.0 Complete linting and formatting setup
  - [ ] 2.1 Install Prettier and related packages
    - Install: `prettier`, `eslint-config-prettier`
    - Add `@typescript-eslint/eslint-plugin` if not present
  - [ ] 2.2 Create Prettier configuration
    - Create `.prettierrc` with consistent formatting rules
    - Create `.prettierignore` for build artifacts and dependencies
  - [ ] 2.3 Update ESLint configuration
    - Extend with `prettier` to disable conflicting rules
    - Ensure Next.js recommended rules are active
    - Add TypeScript-specific rules
  - [ ] 2.4 Add npm scripts for linting and formatting
    - Add `lint` script (if not present)
    - Add `format` script for Prettier
    - Add `format:check` script for CI validation
  - [ ] 2.5 Verify linting and formatting work
    - Run `npm run lint` to confirm no errors
    - Run `npm run format` on codebase

**Acceptance Criteria:**
- Prettier configured with consistent rules
- ESLint works with Prettier without conflicts
- npm scripts available for linting and formatting
- Codebase passes lint and format checks

### Folder Structure

#### Task Group 3: Project Directory Structure
**Dependencies:** Task Group 1

- [ ] 3.0 Complete folder structure setup
  - [ ] 3.1 Create core directories
    - Create `components/` directory with `ui/` subdirectory
    - Create `lib/` directory for utilities and SDK clients
    - Create `types/` directory for TypeScript definitions
    - Create `hooks/` directory for custom React hooks
  - [ ] 3.2 Add placeholder files to prevent empty directories
    - Add `components/.gitkeep` or initial component
    - Add `lib/utils.ts` with cn() helper function
    - Add `types/index.ts` with base type exports
    - Add `hooks/.gitkeep` or initial hook
  - [ ] 3.3 Install utility packages for cn() helper
    - Install `clsx` for conditional class names
    - Install `tailwind-merge` for Tailwind class deduplication
    - Implement cn() function in `lib/utils.ts`

**Acceptance Criteria:**
- All required directories exist
- cn() utility function available for Tailwind class merging
- No empty directories (gitkeep or initial files present)
- Imports work with path aliases

### Environment Configuration

#### Task Group 4: Environment Variables Setup
**Dependencies:** Task Group 1

- [ ] 4.0 Complete environment configuration
  - [ ] 4.1 Create .env.example file
    - Add Supabase placeholders: NEXT_PUBLIC_SUPABASE_URL, NEXT_PUBLIC_SUPABASE_ANON_KEY, SUPABASE_SERVICE_ROLE_KEY
    - Add Stripe placeholders: NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY, STRIPE_SECRET_KEY, STRIPE_WEBHOOK_SECRET, STRIPE_PRICE_ID_PAID_TIER
    - Add OpenAI placeholder: OPENAI_API_KEY
    - Add App placeholder: NEXT_PUBLIC_APP_URL
  - [ ] 4.2 Verify .gitignore includes .env files
    - Confirm `.env.local` is in .gitignore
    - Confirm `.env*.local` pattern is present
    - Add if missing

**Acceptance Criteria:**
- .env.example contains all required placeholders
- Environment files properly gitignored
- Clear documentation of required variables

### SDK Integrations

#### Task Group 5: Supabase SDK Integration
**Dependencies:** Task Groups 3, 4

- [ ] 5.0 Complete Supabase SDK setup
  - [ ] 5.1 Install Supabase packages
    - Install `@supabase/supabase-js`
    - Install `@supabase/ssr` for server-side rendering support
  - [ ] 5.2 Create Supabase client utilities
    - Create `lib/supabase/client.ts` for browser client
    - Create `lib/supabase/server.ts` for server-side client
    - Export typed client creation functions
  - [ ] 5.3 Add Supabase type definitions
    - Create `types/supabase.ts` with placeholder Database type
    - Export types for use across application

**Acceptance Criteria:**
- Supabase SDK installed
- Browser and server clients configured
- Type definitions in place for future schema

#### Task Group 6: Stripe SDK Integration
**Dependencies:** Task Groups 3, 4

- [ ] 6.0 Complete Stripe SDK setup
  - [ ] 6.1 Install Stripe packages
    - Install `stripe` for server-side SDK
    - Install `@stripe/stripe-js` for client-side SDK
  - [ ] 6.2 Create Stripe client utilities
    - Create `lib/stripe/server.ts` with typed Stripe instance
    - Create `lib/stripe/client.ts` with loadStripe helper
  - [ ] 6.3 Add Stripe type definitions
    - Ensure proper TypeScript types for API version
    - Export common types for checkout and subscriptions

**Acceptance Criteria:**
- Stripe server and client SDKs installed
- Typed client instances configured
- Ready for checkout and webhook implementation

#### Task Group 7: OpenAI SDK Integration
**Dependencies:** Task Groups 3, 4

- [ ] 7.0 Complete OpenAI SDK setup
  - [ ] 7.1 Install OpenAI package
    - Install `openai`
  - [ ] 7.2 Create OpenAI client utility
    - Create `lib/openai/client.ts` with typed OpenAI instance
    - Configure for server-side only usage
    - Add helper functions for common operations

**Acceptance Criteria:**
- OpenAI SDK installed
- Typed client configured for server-side use
- Ready for AI feature implementation

### UI Foundation

#### Task Group 8: Radix UI Setup
**Dependencies:** Task Groups 2, 3

- [ ] 8.0 Complete Radix UI foundation
  - [ ] 8.1 Install core Radix UI primitives
    - Install `@radix-ui/react-dialog`
    - Install `@radix-ui/react-dropdown-menu`
    - Install `@radix-ui/react-popover`
    - Install `@radix-ui/react-select`
    - Install `@radix-ui/react-toggle-group`
    - Install `@radix-ui/react-slot`
  - [ ] 8.2 Verify Radix components work with Tailwind
    - Test that cn() utility works with Radix className props
    - Confirm no conflicts with Tailwind configuration

**Acceptance Criteria:**
- All specified Radix UI packages installed
- Components ready for styling with Tailwind
- No configuration conflicts

### Verification

#### Task Group 9: Final Verification
**Dependencies:** Task Groups 1-8

- [ ] 9.0 Complete scaffold verification
  - [ ] 9.1 Run full build
    - Execute `npm run build` to verify no TypeScript errors
    - Confirm all imports resolve correctly
  - [ ] 9.2 Verify development server
    - Run `npm run dev` and confirm app loads
    - Check browser console for errors
  - [ ] 9.3 Verify all SDK clients initialize
    - Confirm Supabase client files have no syntax errors
    - Confirm Stripe client files have no syntax errors
    - Confirm OpenAI client files have no syntax errors

**Acceptance Criteria:**
- Build completes successfully
- Development server runs without errors
- All SDK client files are syntactically correct
- Project ready for feature development

## Execution Order

Recommended implementation sequence:
1. Project Initialization (Task Group 1)
2. Development Tooling (Task Group 2) - can run parallel with Group 3
3. Folder Structure (Task Group 3) - can run parallel with Group 2
4. Environment Configuration (Task Group 4)
5. Supabase SDK Integration (Task Group 5) - can run parallel with Groups 6, 7
6. Stripe SDK Integration (Task Group 6) - can run parallel with Groups 5, 7
7. OpenAI SDK Integration (Task Group 7) - can run parallel with Groups 5, 6
8. Radix UI Setup (Task Group 8)
9. Final Verification (Task Group 9)
