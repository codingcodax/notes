---
id: state
aliases: []
tags: []
---

# State

> Reference: [State: A Component's Memory](https://react.dev/learn/state-a-components-memory)

State is the data that is stored in a component. It is used to keep track of the component's data and to update the component's UI.
The state is used when a simple variable is not enough to represent the component's data.

```tsx
import { useState } from "react";

const Counter = ({ text, count }: { text: string; count: number }) => {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <button onClick={increment}>{text}</button>
      <p>Count: {count}</p>
    </div>
  );
};
```
