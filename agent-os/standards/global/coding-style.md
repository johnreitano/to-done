## TypeScript/React Coding Style

### Naming Conventions
- **Variables/Functions:** camelCase (`getUserById`, `isLoading`, `handleSubmit`)
- **Components:** PascalCase (`TaskCard`, `UserProfile`)
- **Types/Interfaces:** PascalCase with descriptive names (`TaskWithAssignee`, `CreateTaskInput`)
- **Constants:** SCREAMING_SNAKE_CASE for true constants (`MAX_RETRIES`, `API_BASE_URL`)
- **Files:** kebab-case for utilities (`format-date.ts`), PascalCase for components (`TaskCard.tsx`)
- **Boolean prefixes:** `is`, `has`, `should`, `can` (`isLoading`, `hasPermission`)

### TypeScript Standards
- Enable `strict` mode in tsconfig.json
- Prefer `interface` for object shapes, `type` for unions/intersections
- Avoid `any`; use `unknown` for truly unknown types
- Use explicit return types for exported functions

```typescript
// Good
interface Task {
  id: string;
  title: string;
  completed: boolean;
}

export function getTaskById(id: string): Task | null {
  // ...
}

// Bad
export function getTaskById(id: any) {
  // ...
}
```

### Code Organization
- **2-space indentation** (configured via ESLint/Prettier)
- Keep functions under 30 lines; extract helpers when exceeding
- One component per file
- Co-locate related files: `TaskCard.tsx`, `TaskCard.test.tsx`, `use-task.ts`
- Remove unused imports, variables, and dead code immediately

### Backward Compatibility
- Unless specifically instructed, assume no backward compatibility code is needed
- Delete unused code rather than commenting it out
