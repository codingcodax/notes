---
id: lazy
aliases: []
tags: []
---

# Lazy

> Reference: [lazy](https://react.dev/reference/react/lazy)

Lazy is a way to load a component lazily.

```tsx
import { lazy } from "react";

const Gallery = lazy(() => import("./Gallery"));

const Home = () => {
  return (
    <div>
      <Gallery />
    </div>
  );
};
```
