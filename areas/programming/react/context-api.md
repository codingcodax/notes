---
id: context-api
aliases: []
tags: []
---

# Context API

> Reference: [Context Hooks](https://react.dev/reference/react/hooks#context-hooks)

Context is a way to share data between components without passing props through every level of the component tree.

```tsx
const App = () => {
  return (
    <div>
      <Context.Provider value={value}>
        <Button />
      </Context.Provider>
    </div>
  );
};
```
