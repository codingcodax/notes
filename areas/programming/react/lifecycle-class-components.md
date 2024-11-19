---
id: lifecycle-class-components
aliases: []
tags: []
---

# Lifecycle (class components)

> Reference: [Adding lifecycle methods to a class component ](https://react.dev/reference/react/Component#adding-lifecycle-methods-to-a-class-component)

The lifecycle of a component is the set of methods that are called at different stages of the component's life. The lifecycle methods are:

- constructor
- render
- componentDidMount
- componentDidUpdate
- componentWillUnmount

```tsx
class Button extends React.Component<{}, State> {
  componentDidMount() {
    console.log("componentDidMount");
  }

  componentDidUpdate() {
    console.log("componentDidUpdate");
  }

  componentWillUnmount() {
    console.log("componentWillUnmount");
  }

  render() {
    return (
      <div>
        <button>Click me</button>
      </div>
    );
  }
}
```
