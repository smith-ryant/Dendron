---
id: e9m5wkir6v95qzcnrxnjab7
title: State
desc: ""
updated: 1718833282175
created: 1718833276132
---

### What is State in React?

**State** refers to a built-in object that holds data or information about the component. The state can be considered the "memory" of a component. It is used to manage dynamic data that changes over time and can affect the rendering of the component.

### Key Characteristics of State

1. **Managed within the Component**: State is local to the component and cannot be accessed or modified outside of the component unless passed through props.
2. **Influences Rendering**: When the state changes, the component re-renders to reflect the updated state.
3. **Initial State**: When a component is first rendered, its state is set to an initial value.

### Example Scenario

Consider a simple counter application. The count value is a piece of data that changes based on user interaction (e.g., clicking a button to increase the count). This count value can be stored in the state of the component.

### Difference Between State and Props

- **State**: Holds data that may change over the lifetime of the component. It is managed within the component.
- **Props**: Short for properties, props are read-only data passed from parent components to child components. Props cannot be modified by the child component.

### Why Use State?

1. **Dynamic UI**: State allows you to create dynamic and interactive UIs. For example, showing or hiding elements, updating form inputs, or toggling classes.
2. **User Interaction**: State is essential for handling user inputs and actions. For example, updating a list of items when a user adds a new item.
3. **Component Lifecycle**: State helps track and manage the lifecycle of a component. For example, loading data when a component mounts and cleaning up when it unmounts.

### Example of State in a Functional Component

Here's an example to illustrate state usage in a functional component:

```javascript
import React, { useState } from "react";

function Counter() {
  // Declare a state variable 'count' initialized to 0
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

export default Counter;
```

### Breakdown of the Example

1. **Declaration**:

   ```javascript
   const [count, setCount] = useState(0);
   ```

   - `useState(0)`: Initializes the state variable `count` to `0`.
   - `count`: Holds the current state value.
   - `setCount`: A function to update the state value.

2. **Using State in JSX**:

   ```javascript
   <p>You clicked {count} times</p>
   ```

   - Displays the current value of `count`.

3. **Updating State**:
   ```javascript
   <button onClick={() => setCount(count + 1)}>Click me</button>
   ```
   - Calls `setCount` with `count + 1` to update the state and trigger a re-render.

### Visualizing State Changes

1. **Initial Render**:

   - `count` is initialized to `0`.
   - The component renders with the text "You clicked 0 times".

2. **State Update on Button Click**:
   - User clicks the button.
   - `setCount(count + 1)` is called.
   - `count` is updated to `1`.
   - The component re-renders with the text "You clicked 1 time".

### Summary

- **State** is a built-in object that stores dynamic data in a component.
- It is used to create interactive and dynamic UIs.
- State changes trigger re-renders, ensuring the UI stays in sync with the underlying data.
- Use the `useState` hook in functional components to declare and manage state.

Understanding state is crucial for building responsive and interactive applications in React. With practice, managing state and using it to drive your UI will become more intuitive.
