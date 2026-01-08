# Task Breakdown: Scaffold App

## Overview
Total Tasks: 3 Task Groups with 14 Sub-tasks

This spec covers scaffolding a Rails 8.x application with PostgreSQL, Hotwire, and Propshaft. The application already exists with most components in place. Tasks focus on verification, addressing spec compliance gaps, and adding basic test coverage.

## Task List

### Application Configuration

#### Task Group 1: Verify and Complete Rails Scaffold Configuration
**Dependencies:** None

- [x] 1.0 Complete Rails application configuration verification and fixes
  - [x] 1.1 Verify Rails 8.x version and core dependencies
    - Confirm Rails version is 8.x in Gemfile.lock
    - Confirm PostgreSQL gem (pg) is installed
    - Confirm Propshaft is configured as asset pipeline
    - Confirm Hotwire gems (turbo-rails, stimulus-rails) are present
    - Confirm importmap-rails is present for JavaScript modules
  - [x] 1.2 Verify excluded components per spec requirements
    - Check if Action Mailer is being loaded (should be skipped)
    - Check if Action Cable is being loaded (should be skipped)
    - Check if Active Storage is being loaded (should be skipped)
    - Check if Action Text is being loaded (should be skipped)
    - If components are loaded, update config/application.rb to use selective requires instead of `rails/all`
  - [x] 1.3 Verify database configuration
    - Confirm development database name is `to_done_development`
    - Confirm test database name is `to_done_test`
    - Confirm production database name is `to_done_production`
    - Verify DATABASE_URL support for production deployment
  - [x] 1.4 Run database setup
    - Execute `rails db:create` to create development and test databases
    - Verify databases are created successfully

**Acceptance Criteria:**
- Rails 8.x application boots successfully
- PostgreSQL databases created for development and test environments
- Excluded components (Action Mailer, Action Cable, Active Storage, Action Text) are not loaded
- Propshaft asset pipeline is functioning
- Hotwire (Turbo and Stimulus) are available

### Home Page Implementation

#### Task Group 2: Verify Home Page and Routes
**Dependencies:** Task Group 1

- [x] 2.0 Complete home page verification
  - [x] 2.1 Verify HomeController implementation
    - Confirm HomeController exists at `app/controllers/home_controller.rb`
    - Confirm index action is defined
    - Follows Rails conventions
  - [x] 2.2 Verify home page view
    - Confirm view exists at `app/views/home/index.html.erb`
    - Confirm exact text "Here is your new To-Done app" is displayed in an h1 heading
  - [x] 2.3 Verify routes configuration
    - Confirm root route points to `home#index`
    - Confirm health check route exists at `/up`
  - [x] 2.4 Verify application layout
    - Confirm layout at `app/views/layouts/application.html.erb` has proper meta tags
    - Confirm mobile responsiveness meta tag is present
    - Confirm CSRF protection meta tags are present
    - Confirm Propshaft stylesheet links are included
  - [x] 2.5 Manual verification
    - Start Rails server with `rails server`
    - Visit http://localhost:3000 and confirm "Here is your new To-Done app" displays
    - Visit http://localhost:3000/up and confirm health check returns 200

**Acceptance Criteria:**
- Root URL displays "Here is your new To-Done app" in an h1 heading
- Health check endpoint at /up returns 200 status
- Application layout includes all required meta tags
- Page renders correctly with Propshaft assets

### Testing

#### Task Group 3: Add Basic Test Coverage
**Dependencies:** Task Groups 1-2

- [x] 3.0 Complete basic test coverage for scaffold
  - [x] 3.1 Write 2-4 focused tests for home page functionality
    - Test that root path returns successful response (200)
    - Test that home page contains "Here is your new To-Done app" text
    - Test that health check endpoint returns successful response
    - Test that home page uses correct controller action
  - [x] 3.2 Create controller test file
    - Create `test/controllers/home_controller_test.rb`
    - Use Minitest conventions per Rails defaults
    - Follow existing test patterns in test directory
  - [x] 3.3 Run tests and verify all pass
    - Execute `rails test` to run test suite
    - Verify all tests pass with no failures or errors
    - Confirm no deprecation warnings

**Acceptance Criteria:**
- All tests pass (approximately 2-4 tests total)
- HomeController has test coverage for index action
- Health check endpoint is tested
- Test suite runs without errors or warnings

## Execution Order

Recommended implementation sequence:
1. Application Configuration (Task Group 1) - Verify and fix Rails configuration
2. Home Page Implementation (Task Group 2) - Verify routes and views
3. Testing (Task Group 3) - Add test coverage

## Notes

- This is an XS-sized task from the roadmap - the scaffold already exists
- Primary focus is verification that existing scaffold meets spec requirements
- Configuration changes may be needed if excluded components (Action Mailer, etc.) were not properly skipped during generation
- No custom styling required - using Rails defaults
- No database migrations or models needed for this spec
