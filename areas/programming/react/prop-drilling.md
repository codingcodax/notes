---
id: prop-drilling
aliases: []
tags: []
---

# Prop drilling

> Reference [Passing Data Deeply with Context](https://react.dev/learn/passing-data-deeply-with-context#)

Prop drilling is a way to pass props down to child components.

```tsx
const Button = ({ text }: { text: string }) => {
  return <button>{text}</button>;
};

const App = () => {
  return <Button text="Click me" />;
};
```
