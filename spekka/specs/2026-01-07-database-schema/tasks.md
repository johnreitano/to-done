# Task Breakdown: Database Schema for To-Done Rails App

## Overview
Total Tasks: 12

This spec focuses exclusively on the database layer - creating the PostgreSQL schema for the todos table with proper fields, constraints, and indexes. No API or UI components are in scope.

## Task List

### Database Configuration

#### Task Group 1: PostgreSQL Database Setup
**Dependencies:** None

- [x] 1.0 Complete database configuration
  - [x] 1.1 Configure database.yml for PostgreSQL
    - Set adapter to `postgresql`
    - Development database: `to_done_development`
    - Test database: `to_done_test`
    - Production: use `DATABASE_URL` environment variable for Heroku
  - [x] 1.2 Verify PostgreSQL gem is in Gemfile
    - Ensure `pg` gem is present
    - Run `bundle install` if needed
  - [x] 1.3 Create development and test databases
    - Run `rails db:create` to create databases
    - Verify databases exist in PostgreSQL

**Acceptance Criteria:**
- database.yml correctly configured for all environments
- `pg` gem installed and available
- Development and test databases created successfully

### Database Migration

#### Task Group 2: Todos Table Migration
**Dependencies:** Task Group 1

- [ ] 2.0 Complete todos table migration
  - [ ] 2.1 Write 4-6 focused tests for database schema
    - Test that todos table exists after migration
    - Test title column has correct type and NOT NULL constraint
    - Test completed column has correct type, default, and NOT NULL constraint
    - Test completed_at column is nullable datetime
    - Test index exists on completed column
    - Test timestamps columns exist
  - [ ] 2.2 Generate todos table migration
    - Run `rails generate migration CreateTodos`
    - Follow Rails naming conventions
  - [ ] 2.3 Implement migration with all fields
    - `title`: string, null: false
    - `completed`: boolean, null: false, default: false
    - `completed_at`: datetime (nullable)
    - `timestamps` for created_at and updated_at
  - [ ] 2.4 Add database index on completed column
    - Add index for efficient filtering of active/completed todos
    - Use inline index option or separate `add_index` call
  - [ ] 2.5 Run and verify migration
    - Execute `rails db:migrate`
    - Verify schema.rb reflects all columns and constraints
  - [ ] 2.6 Ensure database schema tests pass
    - Run ONLY the 4-6 tests written in 2.1
    - Verify all column types, constraints, and indexes are correct
    - Do NOT run the entire test suite at this stage

**Acceptance Criteria:**
- The 4-6 tests written in 2.1 pass
- Migration creates todos table with all specified columns
- Title column: string type, NOT NULL constraint
- Completed column: boolean type, NOT NULL constraint, default false
- Completed_at column: datetime type, nullable
- Timestamps (created_at, updated_at) present with NOT NULL constraints
- Index on completed column exists
- Migration is reversible

### Schema Verification

#### Task Group 3: Schema Validation and Documentation
**Dependencies:** Task Group 2

- [ ] 3.0 Validate final schema
  - [ ] 3.1 Verify schema.rb matches specification
    - Review db/schema.rb for correct table structure
    - Confirm all constraints are properly defined
    - Confirm index is present
  - [ ] 3.2 Test migration rollback
    - Run `rails db:rollback`
    - Verify table is dropped cleanly
    - Run `rails db:migrate` to restore
  - [ ] 3.3 Run all schema tests to confirm implementation
    - Run the 4-6 tests from Task 2.1
    - Verify all tests pass with final schema

**Acceptance Criteria:**
- schema.rb accurately reflects all requirements
- Migration is fully reversible
- All database schema tests pass

## Execution Order

Recommended implementation sequence:
1. Database Configuration (Task Group 1)
2. Todos Table Migration (Task Group 2)
3. Schema Validation (Task Group 3)

## Notes

- This spec is database-layer only - no model validations, API endpoints, or UI components
- Model validations are explicitly out of scope per the spec
- No seed data is included per the spec
- The completed_at field will be managed programmatically by application code (not part of this spec)
