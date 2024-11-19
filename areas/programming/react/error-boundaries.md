---
id: error-boundaries
aliases: []
tags: []
---

# Error Boundaries

> Reference: [Catching rendering errors with an error boundary](https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary)

Error boundaries are a way to catch errors in a component tree and display a fallback UI.

```tsx
import { ErrorBoundary } from "react";

const App = () => {
  return (
    <ErrorBoundary>
      <h1>Hello, world!</h1>
    </ErrorBoundary>
  );
};
```
