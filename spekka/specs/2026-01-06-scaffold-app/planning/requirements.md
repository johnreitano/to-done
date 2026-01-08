# Spec Requirements: Scaffold App

## Initial Description

Scaffold the Rails app taking into account the tech stack. Provide a plain home page with just the text "Here is your new To-Done app" (XS-sized task from the roadmap).

## Requirements Discussion

### First Round Questions

**Q1:** What Rails version should we use for the scaffold?
**Answer:** Use the latest stable Rails version (Rails 8.x)

**Q2:** Which asset pipeline should we use - Propshaft (modern default) or Sprockets (legacy)?
**Answer:** Use Propshaft (modern Rails default)

**Q3:** What testing framework should we use - Minitest (Rails default) or RSpec?
**Answer:** Use Minitest (Rails default, keeps dependencies minimal)

**Q4:** Should PostgreSQL be configured for all environments (development, test, production) or just production?
**Answer:** Configure PostgreSQL for all environments (development, test, production) for consistency

**Q5:** Should we include Hotwire (Turbo + Stimulus) in the initial scaffold?
**Answer:** Include Turbo and Stimulus in the scaffold

**Q6:** Are there any Rails components we should explicitly exclude to keep the app lightweight?
**Answer:** Exclude Action Mailer, Action Cable, Active Storage, and Action Text to keep the app lightweight

### Existing Code to Reference

No similar existing features identified for reference - this is a fresh scaffold.

### Follow-up Questions

No follow-up questions were needed.

## Visual Assets

### Files Provided:

No visual assets provided.

### Visual Insights:

Not applicable - this is a simple home page displaying static text.

## Requirements Summary

### Functional Requirements

- Generate a new Rails 8.x application scaffold
- Configure PostgreSQL as the database for all environments
- Create a root route pointing to a home page
- Display the text "Here is your new To-Done app" on the home page
- Include Hotwire (Turbo + Stimulus) for future interactive features
- Use Propshaft for asset pipeline
- Use Minitest for testing

### Reusability Opportunities

None applicable - this is the initial application scaffold that will serve as the foundation for all future features.

### Scope Boundaries

**In Scope:**
- Rails 8.x application generation
- PostgreSQL database configuration (development, test, production)
- Propshaft asset pipeline setup
- Hotwire (Turbo + Stimulus) inclusion
- Minitest testing framework
- Root route configuration
- Home page controller and view with "Here is your new To-Done app" text
- Basic application layout

**Out of Scope:**
- Action Mailer (email functionality)
- Action Cable (WebSocket functionality)
- Active Storage (file uploads)
- Action Text (rich text editing)
- Styling beyond basic Rails defaults
- Any database migrations or models
- Authentication or user management
- Deployment configuration (covered in roadmap item #10)

### Technical Considerations

- **Framework:** Ruby on Rails 8.x (latest stable)
- **Database:** PostgreSQL for all environments
- **Asset Pipeline:** Propshaft
- **JavaScript:** Hotwire (Turbo + Stimulus)
- **Testing:** Minitest
- **Templating:** ERB (Rails default)
- **Excluded Components:** Action Mailer, Action Cable, Active Storage, Action Text
- **Hosting Target:** Heroku (per tech stack, but deployment is out of scope for this task)
