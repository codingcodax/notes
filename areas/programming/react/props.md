---
id: props
aliases: []
tags: []
---

# Props

> Reference: [Passing Props to a Component](https://react.dev/learn/passing-props-to-a-component#passing-props-to-a-component)

Props are the data that is passed to a component. They are used to customize the component's behavior.

```tsx
const Button = ({ text }: { text: string }) => {
  return <button>{text}</button>;
};
```
