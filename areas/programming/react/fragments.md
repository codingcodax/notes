---
id: fragments
aliases: []
tags: []
---

# Fragments

> Reference: [<Fragment> (<>...</>)](https://react.dev/reference/react/Fragment)

Fragments are a way to group multiple elements without adding extra nodes to the DOM.
Can be used to return multiple elements from a function.

- `<>` is the fragment tag
- `<React.Fragment>` is the fragment component

```tsx
const App = () => {
  return (
    <>
      <h1>Hello, world!</h1>
      <p>This is a paragraph.</p>
      <p>This is another paragraph.</p>
    </>
  );
};
```
