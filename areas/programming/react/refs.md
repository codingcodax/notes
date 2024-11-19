---
id: refs
aliases: []
tags: []
---

# Refs

> Reference: [Referencing Values with Refs](https://react.dev/learn/referencing-values-with-refs)

Refs are used to remember some information, but we don't want that information to trigger new renders.

```tsx
import { useRef } from "react";

const Button = ({ text }: { text: string }) => {
  const buttonRef = useRef(null);

  const handleClick = () => {
    console.log(buttonRef.current);
  };

  return (
    <button ref={buttonRef} onClick={handleClick}>
      {text}
    </button>
  );
};
```
