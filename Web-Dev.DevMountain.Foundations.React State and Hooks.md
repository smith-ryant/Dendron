---
id: nkguzluhaffxlk2bclku5al
title: React State and Hooks
desc: ""
updated: 1722790676578
created: 1722790622201
---

Here is the webpage content formatted in Markdown:

---

# On this Page

- [React 2: State and Hooks](#react-2-state-and-hooks)
- [What We’ll Cover](#what-well-cover)
- [Review: Props and State](#review-props-and-state)
- [What are Hooks?](#what-are-hooks)
- [Two Rules of Hooks](#two-rules-of-hooks)
- [The useState Hook](#the-usestate-hook)
- [Quiz!](#quiz)
- [Review: Updating State](#review-updating-state)
- [Example: Dice](#example-dice)
- [Keeping Components “Pure”](#keeping-components-pure)
- [Forms/User Inputs in React](#formsuser-inputs-in-react)
- [Example: Movie List](#example-movie-list)
- [The key Prop](#the-key-prop)
- [Why do we need Keys?](#why-do-we-need-keys)
- [Example: Emojis](#example-emojis)
- [A Good Key](#a-good-key)
- [Multiple State Updates](#multiple-state-updates)
- [A Broken Counter](#a-broken-counter)
- [Queueing Multiple State Updates](#queueing-multiple-state-updates)
- [The useEffect Hook](#the-useeffect-hook)
- [useEffect](#useeffect)
- [Skipping Effects](#skipping-effects)
- [Coming Up](#coming-up)

---

## React 2: State and Hooks

This section covers how to render lists of components, handle forms and user input, and introduces a new hook called `useEffect`.

To download the demo code for this lecture, run:

```bash
dmget wb-react-2 --demo
```

Then, `cd` into the project directory and use npm to install and run the dev server:

```bash
npm install
npm run dev
```

## What We’ll Cover

- Review props, state, and the `useState` hook
- Forms in React
- The `key` prop
- Multiple state updates
- The `useEffect` hook

## Review: Props and State

- **Props** are used to pass information to a component.

  - They are immutable and can be used to customize components.

- **State** values can be changed by the component.
  - When the state changes, React will re-render the component.
  - If a component receives different props (from its parent), that will also cause a re-render.

## What are Hooks?

- Hooks allow us to access various React features when using functional components.
- They replace the need for class-based components.
- Today we will focus on two hooks: `useState` and `useEffect`.
  - (The others are less important for now)

## Two Rules of Hooks

1. **Only call hooks in React functional components** (not in plain JavaScript functions or classes).
2. **Only call hooks from the top level** (never inside loops, conditions, or nested functions).

## The useState Hook

```javascript
import { useState } from "react";

const [count, setCount] = useState(0);
```

- `count` is the state variable.
- `setCount` is the function we must call to update the state.
- `0` is the initial state. (The initial state should have the same data type as the state variable.)

## Quiz!

**What is `count`?**  
**What is `setCount`?**  
**What is the `0` doing?**

- `count` is the state variable.
- `setCount` is the function used to update the state.
- `0` is the initial state value.

## Review: Updating State

To update the state, we must use the function that `useState` returns.

- For example, to increment the value of `count` in the above example, we must call the `setCount` function: `setCount(count + 1)`.

- **Never update state directly** with `count = count + 1`! If you do, React will not detect that the state has changed and will not re-render the component.

## Example: Dice

We’re making a role-playing game, Dunder & Dragons, and we need dice components for users to roll!

- Dice come in different numbers of sides (4, 6, 8, 10, 12, 20).

- A die’s number of sides never changes. **Should this be props or state?**

- Users should click on a die to “roll” it & see results. This value can change every time the die is rolled – **should this be props or state?**

**wb-react-2-demo/src/Die.jsx**

```javascript
import { useState } from "react";
import "./dice.css";

function getRandomNum(upperLimit) {
  return Math.ceil(Math.random() * upperLimit);
}

export default function Die(props) {
  const [diceValue, setDiceValue] = useState("?");

  const roll = () => {
    const rollResult = getRandomNum(props.sides);
    setDiceValue(rollResult);
  };

  return (
    <button type="button" className="die" onClick={roll}>
      <i>sides={props.sides}</i>
      <b>{diceValue}</b>
    </button>
  );
}
```

## Keeping Components “Pure”

A React component should be a “pure” function. This means:

- **It minds its own business.** It does not change any objects or variables that existed before it was called.
- **Same inputs, same output.** Given the same inputs, a pure function should always return the same result.
- Components should never modify global variables or manipulate the DOM directly with `document.querySelector`. That would make them impure.

There are two ways to change things in React:

1. **Inside an event handler**, by calling a set function to update the state.
2. **With the `useEffect` hook**, as a last resort.

## Forms/User Inputs in React

React components often contain forms and/or `<input>` elements.

- We need to store the value entered by the user. A good way to do this is by using state:

```javascript
const [inputValue, setInputValue] = useState("");

return (
  <input
    value={inputValue}
    onChange={(e) => setInputValue(e.target.value)}
    type="text"
  />
);
```

- The `onChange` handler is used to update the state (and thus update the DOM) when the input value changes.

## Example: Movie List

**wb-react-2-demo/src/MovieList.jsx**

```javascript
export default function MovieList() {
  const [movies, setMovies] = useState([
    "Alien",
    "Predator",
    "Alien Vs. Predator",
  ]);
  // This initializes our state value movies as an array with 3 items.

  const [inputValue, setInputValue] = useState("");
  // This will be used to hold the value of our input box.

  const moviesDisplay = movies.map((movie) => <h5 key={movie}>{movie}</h5>);
  return (
    <div>
      <h2>Movie List</h2>
      {moviesDisplay}

      <input
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
        type="text"
      />

      <button
        style={{ marginLeft: "5px" }}
        onClick={() => {
          setMovies([...movies, inputValue]);
          setInputValue("");
        }}
      >
        Add Movie
      </button>
    </div>
  );
}
```

## The key Prop

In the Movie List example, you may have noticed this:

```javascript
const moviesDisplay = movies.map((movie) => <h5 key={movie}>{movie}</h5>);
return (
  <div>
```

When we render a list in React, we need to give each item a **key** — a string or a number that uniquely identifies it among other items in that array.

- If you don’t have a key, you’ll get this warning in the browser console:

> **Key Warning**

## Why do we need Keys?

- When component state changes, React gets a new tree of UI elements to render.
- React needs to figure out which elements are different from before so it can update the DOM.
- When comparing two lists, React iterates over both lists and compares the children in order.
- So if the order of the list items changes and we don’t have keys, we can get bugs.

## Example: Emojis

Demo time! (`MissingKey.jsx`)

1. Rate only the 😘 emoji as “Very good.”
2. Delete the 😘 emoji.
3. We have a problem…

## A Good Key

- We need a unique value to identify each list item so React knows exactly which item changed.
- **Don’t use the index for the key** — you’ll get the same bug.

Here we can use the id to fix the problem:

```javascript
<li className="emoji-item" key={emoji.id}>
```

## Multiple State Updates

### A Broken Counter

This seems like it should increment the counter three times, but it doesn’t:

**wb-react-2-demo/src/Counters.jsx**

```javascript
function BrokenCounter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h3>{number}</h3>
      <button
        onClick={() => {
          setNumber(number + 1);
          setNumber(number + 1);
          setNumber(number + 1);
        }}
      >
        +3
      </button>
    </>
  );
}
```

## Queueing Multiple State Updates

- Each state change request is handled separately.
- So for each state change request, React will figure out the new state value from the old one, and update it.
- We need to tell React to use the new state value to determine the next one, by passing a **function** to the state update method:

```javascript
function WorkingCounter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h3>{number}</h3>
      <button
        onClick={() => {
          setNumber((oldNumber) => oldNumber + 1);
          setNumber((oldNumber) => oldNumber + 1);
          setNumber((oldNumber) => oldNumber + 1);
        }}
      >
        +3
      </button>
    </>
  );
}
```

## The useEffect Hook

### useEffect

**useEffect** is a hook that lets you run code outside of rendering a component.

```javascript
import { useEffect } from "react";

function MyComponent() {
  useEffect(() => {
    // This code will run after the component renders

    return () => {
      // This code will run when the component is removed from the DOM
    };
  }, []);
}
```

- The first argument is a function to run after rendering the component.
- The second argument is an array of variables to watch for changes. If empty, it runs once after the component is mounted.

## Skipping Effects

- The `useEffect` hook runs after every render by default.
- But if we pass an array of variables, it only runs when one of those variables changes.
- If you pass an empty array, the effect will only run once after the component is first rendered.

---

## Coming Up

- The `useContext` hook
- React Router

---
