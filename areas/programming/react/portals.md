---
id: portals
aliases: []
tags: []
---

# Portals

> Reference: [createPortal](https://react.dev/reference/react-dom/createPortal)

Portals are a way to render a component outside of the normal DOM tree.

```tsx
import { createPortal } from "react-dom";

const Portal = ({ children }: { children: React.ReactNode }) => {
  return createPortal(children, document.getElementById("portal"));
};

const App = () => {
  return (
    <div>
      <Portal>
        <p>Hello, world!</p>
      </Portal>
    </div>
  );
};
```
