---
id: to8zjbpgqrwrstbdharqszn
title: Hooks
desc: ""
updated: 1722022861236
created: 1722022698125
---

React hooks have specific rules to ensure they work correctly and predictably. Here are the key rules for using React hooks:

### 1. **Only Call Hooks at the Top Level**

Hooks should be called at the top level of your React function. This means they should not be called inside loops, conditions, or nested functions. This ensures that hooks are called in the same order each time a component renders, which is essential for React to correctly preserve the state of hooks between multiple `useState` and `useEffect` calls.

**Example:**

```javascript
// Correct
function MyComponent() {
  const [count, setCount] = useState(0);
  // other hooks
}

// Incorrect
function MyComponent() {
  if (someCondition) {
    const [count, setCount] = useState(0); // This is incorrect
  }
}
```

### 2. **Only Call Hooks from React Functions**

Hooks should only be called from React function components or custom hooks. They should not be called from regular JavaScript functions.

**Example:**

```javascript
// Correct
function MyComponent() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    // effect
  }, []);
}

// Incorrect
function someRegularFunction() {
  const [count, setCount] = useState(0); // This is incorrect
}
```

### 3. **Use Custom Hooks to Encapsulate Logic**

If you have logic that you want to reuse across multiple components, you can extract it into a custom hook. Custom hooks are JavaScript functions whose names start with "use" and that may call other hooks.

**Example:**

```javascript
// Custom Hook
function useCustomHook() {
  const [value, setValue] = useState(initialValue);
  // custom logic
  return [value, setValue];
}

// Using the custom hook in a component
function MyComponent() {
  const [value, setValue] = useCustomHook();
}
```

### 4. **Hooks Must Be Named with the `use` Prefix**

Custom hooks must be named starting with the `use` prefix. This convention ensures that React can automatically check for violations of the rules of hooks.

**Example:**

```javascript
// Correct
function useCustomHook() {
  // logic
}

// Incorrect
function customHook() {
  // This is incorrect
  // logic
}
```

### 5. **Don’t Call Hooks from Regular JavaScript Functions**

Hooks should only be called within React function components and custom hooks, not from regular JavaScript functions.

**Example:**

```javascript
// Correct
function MyComponent() {
  const [count, setCount] = useState(0);
  return <div>{count}</div>;
}

// Incorrect
function regularFunction() {
  const [count, setCount] = useState(0); // This is incorrect
}
```

### Commonly Used React Hooks

1. **`useState`**: Adds state to functional components.
2. **`useEffect`**: Performs side effects in function components.
3. **`useContext`**: Accesses the context value.
4. **`useReducer`**: An alternative to `useState` for more complex state logic.
5. **`useCallback`**: Returns a memoized callback.
6. **`useMemo`**: Returns a memoized value.
7. **`useRef`**: Returns a mutable ref object.
8. **`useLayoutEffect`**: Similar to `useEffect`, but fires synchronously after all DOM mutations.
9. **`useImperativeHandle`**: Customizes the instance value that is exposed when using `ref`.

Following these rules ensures that your hooks are used correctly and your components behave as expected. If you need a deeper understanding or have specific questions about using hooks in certain scenarios, feel free to ask!
