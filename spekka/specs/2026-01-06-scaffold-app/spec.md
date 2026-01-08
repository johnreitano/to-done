# Specification: Scaffold App

## Goal
Generate a Rails 8.x application scaffold with PostgreSQL, Hotwire, and Propshaft, featuring a simple home page displaying "Here is your new To-Done app".

## User Stories
- As a developer, I want a properly scaffolded Rails 8.x application so that I have a solid foundation for building the To-Done task management features.
- As a visitor, I want to see a confirmation message on the home page so that I know the application is running correctly.

## Specific Requirements

**Rails 8.x Application Generation**
- Use the latest stable Rails 8.x version
- Generate with PostgreSQL database adapter using the `--database=postgresql` flag
- Use Propshaft as the asset pipeline (Rails 8 default)
- Include Hotwire (Turbo and Stimulus) for frontend interactivity
- Use Minitest as the testing framework (Rails default)
- Use ERB templating (Rails default)

**Excluded Rails Components**
- Skip Action Mailer (`--skip-action-mailer`)
- Skip Action Cable (`--skip-action-cable`)
- Skip Active Storage (`--skip-active-storage`)
- Skip Action Text (`--skip-action-text`)
- These exclusions keep the application lightweight for its initial scope

**PostgreSQL Database Configuration**
- Configure PostgreSQL for development, test, and production environments
- Use `to_done_development` as the development database name
- Use `to_done_test` as the test database name
- Use `to_done_production` as the production database name
- Support DATABASE_URL environment variable for production deployment

**Home Page Implementation**
- Create a HomeController with an index action
- Create corresponding view at `app/views/home/index.html.erb`
- Display the exact text "Here is your new To-Done app" in an h1 heading
- Configure root route to point to `home#index`

**Application Layout**
- Use standard Rails application layout at `app/views/layouts/application.html.erb`
- Include proper meta tags for mobile responsiveness
- Include CSRF protection meta tags
- Link to Propshaft-managed stylesheets
- Include Turbo and Stimulus via importmap-rails

**Health Check Endpoint**
- Maintain Rails default health check at `/up` route
- Returns 200 if app boots correctly, 500 otherwise
- Useful for load balancers and deployment monitoring

## Visual Design
No visual assets provided - this is a simple text-only home page.

## Existing Code to Leverage

**Rails 8.x Default Application Structure**
- The scaffold should follow Rails 8.x conventions for directory structure
- Use default generators for controllers and views
- Follow Rails naming conventions throughout

**Propshaft Asset Pipeline**
- Use Propshaft's default configuration for CSS compilation
- Leverage importmap-rails for JavaScript module management
- Hotwire integration handled automatically by turbo-rails and stimulus-rails gems

## Out of Scope
- Action Mailer (email functionality)
- Action Cable (WebSocket/real-time functionality)
- Active Storage (file upload functionality)
- Action Text (rich text editing functionality)
- Custom CSS styling beyond Rails defaults
- Database migrations or model creation
- User authentication or authorization
- Deployment configuration to Heroku
- PWA manifest configuration
- Custom favicon or branding assets
