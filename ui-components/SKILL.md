---
name: ui-components
description: Implement React components in maintainable, effortless and consistent way. Use when you implement React components for your application.
---

# UI Components

## Component Library

We use shadcn/ui components which can be installed with `pnpm dlx shadcn@latest add {component name}`. 

When you need a new component, use one of the following three methods in order of this priority.

1. use shadcn/ui components with their default style
2. use shadcn/ui components with custom style
3. create components by composing shadcn/ui components
4. implement components by yourself

## Styling rules

### Layout by CSS Modules, shapes and colors by Tailwind CSS

Use tailwind css only for styling shapes and colors of HTML elements and texts. Never use it for defining layouts and placements of elements.

Use css modules only for defining layouts and placements of elements. Never use it for styling shapes and colors.

These rules typically results in a structure like this:

```tsx
import styles from './MyComponent.module.css';

export function MyComponent() {
  return (
    <div className={styles.container}>
      <h1 className={cn(
        styles.header,
        "text-2xl font-bold text-center text-blue-500"
      )}>
        Hello World
      </h1>
      <p className={cn(styles.content, "text-gray-700")}>
        This is a sample component.
      </p>
    </div>
  );
}
```

```css
/* MyComponent.module.css */
.container {
  display: grid;
  grid-template-areas:
    "header"
    "content";
  gap: 16px;
}
.header {
  grid-area: header;
}
.content {
  grid-area: content;
}
```

### Prefer grid over any other layout methods

Prefer grid layout over other methods such as flex and, if applicable, the best way is to use `grid-template-areas`.
