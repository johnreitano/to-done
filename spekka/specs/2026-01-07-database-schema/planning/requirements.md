# Spec Requirements: Database Schema for To-Done Rails app

## Initial Description
Create the database schema for the To-Done Rails application, a simple todo list app using PostgreSQL and hosted on Heroku.

## Requirements Discussion

### First Round Questions

**Q1:** What fields should the todo table include?
**Answer:** Title field (string, max 255 characters, NOT NULL), completed field (boolean, defaults to false, NOT NULL), standard Rails timestamps, and an additional completed_at timestamp to track when a task was marked complete.

**Q2:** Should there be a user_id field for authentication?
**Answer:** No user_id field - intentional design decision. All todos are public with no authentication.

**Q3:** What indexes are needed for query performance?
**Answer:** Add index on the completed column for filtering queries.

**Q4:** What database naming convention should be used?
**Answer:** Standard Rails convention - to_done_development for development, to_done_test for test, and production auto-configured via Heroku's DATABASE_URL.

**Q5:** Are there any features to explicitly exclude?
**Answer:** No soft deletes, audit logging, or other features - explicitly excluded.

### Existing Code to Reference

No similar existing features identified for reference. This is a brand new Rails app with no existing migrations or code.

### Follow-up Questions

No follow-up questions were needed.

## Visual Assets

### Files Provided:
No visual assets provided.

### Visual Insights:
N/A - No visual assets to analyze.

## Requirements Summary

### Functional Requirements
- Create todos table with title, completed, timestamps, and completed_at fields
- Title field: string type, max 255 characters, NOT NULL constraint at database level
- Completed field: boolean, defaults to false, NOT NULL constraint
- Timestamps: Standard Rails created_at and updated_at
- Completed_at: nullable timestamp to track when task was marked complete
- Index on completed column for efficient filtering queries

### Reusability Opportunities
- None identified - brand new Rails application with no existing code

### Scope Boundaries
**In Scope:**
- Database schema for todos table
- All field definitions with constraints
- Index on completed column
- Database configuration for development, test, and production environments

**Out of Scope:**
- User authentication (no user_id field)
- Soft deletes
- Audit logging
- Any other additional features

### Technical Considerations
- PostgreSQL database
- Hosting on Heroku (production database configured via DATABASE_URL)
- Standard Rails conventions for naming and structure
- Brand new Rails app with no existing migrations
