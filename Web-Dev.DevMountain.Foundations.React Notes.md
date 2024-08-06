---
id: x2wi9ezy86fhljuajc1j7vk
title: React Notes
desc: ""
updated: 1722789747317
created: 1722789367312
---

Here's the webpage content formatted in Markdown:

---

# On this Page

- [Homework: React State and Hooks](#homework-react-state-and-hooks)
- [Review Questions: Intro to React](#review-questions-intro-to-react)
- [Readings and Materials](#readings-and-materials)

---

## Homework: React State and Hooks

## Review Questions: Intro to React

### What is the difference between props and state?

**Solution**

- **Props** are information given to your component and cannot be changed (they are immutable).
- **State** can be changed.

### Consider the following code:

```javascript
import { useState } from "react";

[count, setCount] = useState(0);
```

What is `count`? What is `setCount`? Why do we pass the value `0` into `useState()`?

**Solution**

- `count` is the state variable.
- `setCount` is the function you must use to update the state.
- `0` is the initial value of the state.

### What is wrong with the highlighted line of code?

```javascript
function Counter(props) {
  const [count, setCount] = useState(0);
  if (props.updateCount) {
    count += 1;
  }
}
```

**Solution**

State variables cannot be updated directly. If you do so, React will not re-render the component based on the state change. Instead, you must use the `setCount` function.

## Readings and Materials

These materials will prepare you for our upcoming lesson on React.

- [Updating Objects in State](https://react.dev/learn/updating-objects-in-state)
- [Updating Arrays in State](https://react.dev/learn/updating-arrays-in-state)
- [Reacting to Input with State](https://react.dev/learn/reacting-to-input-with-state)
- [Keeping Components Pure](https://react.dev/learn/keeping-components-pure)
- [Rendering Lists](https://react.dev/learn/rendering-lists)
- [Synchronizing with Effects](https://react.dev/learn/synchronizing-with-effects)
- [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)

---

This Markdown version provides a clean and organized format, including headings, code blocks, and bullet points for easy readability and navigation.
