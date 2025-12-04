# Product Roadmap

1. [ ] User Authentication & Account Management — Implement Supabase authentication with email/password sign-up and login, user profile storage, and session management to enable secure access to the application. `S`

2. [ ] Core Task CRUD Operations — Build the database schema and API endpoints for creating, reading, updating, and deleting tasks with title (required), description (rich text), deadline, and assignee fields. `M`

3. [ ] Rich Text Editor Integration — Integrate a rich text editor component (using Radix UI primitives or compatible library) for task descriptions, supporting formatting like bold, italics, lists, and links. `S`

4. [ ] List and Card View Modes — Implement toggle between list view (compact, scannable) and card view (detailed, spacious) with user preference persistence and responsive layouts for both modes. `M`

5. [ ] Individual Task Sharing via Links — Generate shareable public links for individual tasks with OpenGraph metadata integration, allowing non-authenticated users to view (but not edit) shared tasks with proper previews. `M`

6. [ ] Stripe Payment Integration & Subscription Management — Implement Stripe checkout flow, subscription creation, webhook handling for payment events, and user role management (free vs paid) with access control middleware. `L`

7. [ ] Shared Lists for Team Collaboration — Enable paid users to create shared lists that multiple authenticated users can access and edit, with real-time synchronization using Supabase realtime features and proper permission management. `L`

8. [ ] Smart Reminders & Notifications — Build notification system for paid users with configurable reminder settings (email, in-app), deadline-based triggers, and overdue task alerts using scheduled jobs or Supabase edge functions. `M`

9. [ ] AI Task Assistant — Integrate OpenAI SDK to provide paid users with AI-powered features: task breakdown into subtasks, deadline suggestions based on task complexity, and automated description drafting with user review. `L`

10. [ ] Dashboard & Analytics — Create user dashboard showing task completion rates, upcoming deadlines, team activity (for paid users), and productivity insights to provide value and encourage engagement. `M`

> Notes
> - Order prioritizes building a functional free-tier MVP (items 1-5) before paid features (items 6-9)
> - Item 6 (Stripe integration) is prerequisite for all paid tier features (7-9)
> - Each item represents an end-to-end (frontend + backend) functional and testable feature
> - Consider soft-launching with free tier only, validating product-market fit, then adding paid features
> - Items 7 and 9 are the most complex (L effort) due to real-time collaboration and AI integration respectively
