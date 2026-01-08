# Product Roadmap

1. [ ] Scaffold App — Scaffold the rails app taking into account the tech stack. Provide a plain home page with just the text "Here is your new To-Done app" `XS`

2. [ ] Database Schema — Create the todos table with fields for title, completed status, and timestamps. Set up PostgreSQL database configuration for development and production environments. `XS`

3. [ ] Todo Model — Implement the Todo model with validations ensuring title presence and completed boolean default. Add any necessary scopes for filtering todos. `XS`

4. [ ] Todo API Endpoints — Build RESTful controller actions for creating, reading, updating, and deleting todos. Include proper response handling and error states. `S`

5. [ ] Todo List View — Create the main page displaying all todos in a clean list format. Show completed status visually and handle empty state when no todos exist. `S`

6. [ ] Add Todo Form — Implement the form for creating new todos with title input. Form should clear after successful submission and display inline on the main page. `XS`

7. [ ] Toggle Todo Completion — Add the ability to mark todos as complete or incomplete with a single click. Update the visual state immediately to reflect the change. `XS`

8. [ ] Edit Todo Inline — Enable editing todo titles directly in the list view. Support save on blur or enter key, and cancel on escape key. `S`

9. [ ] Delete Todo — Add delete functionality with a confirmation step to prevent accidental removal. Remove the todo from the list immediately upon confirmation. `XS`

10. [ ] Production Deployment — Configure Heroku deployment with PostgreSQL addon. Set up environment variables and verify all features work in production. `S`

> Notes
> - Order items by technical dependencies and product architecture
> - Each item should represent an end-to-end (frontend + backend) functional and testable feature
