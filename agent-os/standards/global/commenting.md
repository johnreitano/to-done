## Code Commenting Standards

### Self-Documenting Code First
- Prefer descriptive names over comments
- Extract complex logic into well-named functions

```typescript
// Bad: Comment explaining unclear code
// Check if user can access paid features
if (user.tier === 'paid' && user.status === 'active') { ... }

// Good: Self-documenting
const canAccessPaidFeatures = user.tier === 'paid' && user.status === 'active';
if (canAccessPaidFeatures) { ... }
```

### When to Comment
- Complex business logic that isn't obvious from code
- Non-obvious "why" decisions (not "what")
- Workarounds for external limitations

```typescript
// Supabase RLS requires explicit user_id filter even with policies
const { data } = await supabase
  .from('tasks')
  .select('*')
  .eq('user_id', userId);
```

### Avoid
- Commenting out code (delete it instead)
- TODO/FIXME without associated tickets
- Comments that restate the code
- Change logs in comments (use git history)
