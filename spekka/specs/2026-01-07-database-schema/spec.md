# Specification: Database Schema for To-Done Rails App

## Goal
Create the PostgreSQL database schema for the To-Done Rails application, including the todos table with all required fields, constraints, and indexes.

## User Stories
- As a developer, I want a properly structured database schema so that I can build CRUD operations for todo items
- As a user, I want my completed tasks to have timestamps so that I can see when I finished them

## Specific Requirements

**Todos Table Creation**
- Create a new Rails migration for the todos table
- Use PostgreSQL as the database adapter
- Follow Rails naming conventions (plural table name, singular model name)

**Title Field**
- String type column named `title`
- Maximum length of 255 characters (Rails string default)
- NOT NULL constraint at database level using `null: false`
- No default value - title must be explicitly provided

**Completed Field**
- Boolean type column named `completed`
- NOT NULL constraint at database level using `null: false`
- Default value of `false` using `default: false`
- Used for filtering active vs completed todos

**Timestamps Fields**
- Standard Rails `timestamps` macro for `created_at` and `updated_at`
- Both fields automatically managed by Rails
- NOT NULL constraints applied by default

**Completed At Field**
- Datetime type column named `completed_at`
- Nullable (no NOT NULL constraint) - only populated when task is completed
- No default value - set programmatically when completed status changes to true

**Database Index**
- Add index on the `completed` column
- Enables efficient filtering queries for active/completed todos
- Use standard Rails `add_index` or inline index option

**Database Configuration**
- Development database: `to_done_development`
- Test database: `to_done_test`
- Production database: configured via Heroku's `DATABASE_URL` environment variable
- PostgreSQL adapter specified in database.yml

## Visual Design
No visual assets provided.

## Existing Code to Leverage
No existing code to leverage - this is a brand new Rails application with no existing migrations or models.

## Out of Scope
- User authentication or user_id foreign key field
- Soft delete functionality (deleted_at column or acts_as_paranoid)
- Audit logging or paper_trail versioning
- Additional tables beyond todos
- Seed data or sample records
- Model validations (schema only, not model layer)
- Position/ordering column for manual sorting
- Priority or due date fields
- Categories or tags associations
- Description or notes text field
