## Accessibility with Radix UI

### Radix UI Provides Built-in Accessibility
Radix primitives handle ARIA attributes, keyboard navigation, and focus management automatically.

```tsx
// Radix Dialog handles focus trap, Escape key, ARIA automatically
import * as Dialog from '@radix-ui/react-dialog';

<Dialog.Root>
  <Dialog.Trigger>Open</Dialog.Trigger>
  <Dialog.Portal>
    <Dialog.Overlay className="fixed inset-0 bg-black/50" />
    <Dialog.Content>
      <Dialog.Title>Edit Task</Dialog.Title>
      <Dialog.Description>Update task details</Dialog.Description>
      {/* Content */}
      <Dialog.Close>Cancel</Dialog.Close>
    </Dialog.Content>
  </Dialog.Portal>
</Dialog.Root>
```

### Required Accessibility Practices
- **Always include Dialog.Title and Dialog.Description** for screen readers
- **Use semantic HTML:** `<button>`, `<nav>`, `<main>`, `<form>`
- **Provide alt text** for images: `<Image alt="Task completed checkmark" />`
- **Label all form inputs:** Use `<label htmlFor="...">` or `aria-label`

### Keyboard Navigation
- All interactive elements must be keyboard accessible (Radix handles this)
- Visible focus indicators: Tailwind's `focus:ring-2 focus:ring-blue-500`
- Logical tab order (avoid positive tabindex values)

### Color and Contrast
- Minimum 4.5:1 contrast ratio for normal text
- Don't rely solely on color (add icons or text labels)
- Test with color blindness simulators

### Testing
- Tab through all interactive elements
- Test with VoiceOver (Mac) or NVDA (Windows)
- Use Chrome DevTools Accessibility panel
