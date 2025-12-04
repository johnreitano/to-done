---
name: Backend Queries
description: Write Supabase queries with proper select statements, error handling, joins, filtering, and pagination. Use this skill when writing Supabase client queries, when creating files in lib/supabase/queries/, when implementing CRUD operations with the Supabase SDK, when joining related tables with select syntax, when adding filters with .eq() .gt() .order(), when implementing pagination with .range(), when using Supabase RPC functions for transactions, or when handling query errors.
---

## When to use this skill

- When writing queries using the Supabase JavaScript SDK
- When creating or editing files in `lib/supabase/**/*.ts`
- When implementing `.select()`, `.insert()`, `.update()`, `.delete()` operations
- When joining tables using Supabase's nested select syntax
- When filtering with `.eq()`, `.gt()`, `.in()`, `.order()`
- When implementing pagination with `.range()`
- When using `supabase.rpc()` for database functions
- When handling `{ data, error }` response patterns

# Backend Queries

This Skill provides Claude Code with specific guidance on how to adhere to coding standards as they relate to how it should handle backend queries.

## Instructions

For details, refer to the information provided in this file:
[backend queries](../../../agent-os/standards/backend/queries.md)
