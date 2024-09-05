---
id: v0vwd71bl2vi8jvwtiatjpq
title: How React Works
desc: ""
updated: 1722791213353
created: 1722791032710
---

Here's the webpage content converted into Markdown:

---

# On this Page

- [How React Works](#how-react-works)
  - [Intro](#intro)
  - [Goals](#goals)
  - [Rendering in React](#rendering-in-react)
    - [How Rendering Works in React](#how-rendering-works-in-react)
      - [Step 1: A Render is Triggered](#step-1-a-render-is-triggered)
      - [Step 2: Components are Rendered by React](#step-2-components-are-rendered-by-react)
      - [Step 3: React Commits Changes to the DOM](#step-3-react-commits-changes-to-the-dom)
      - [What Happens When You Click the Button?](#what-happens-when-you-click-the-button)
  - [State as a Snapshot](#state-as-a-snapshot)
    - [What Happens When React Re-renders?](#what-happens-when-react-re-renders)
    - [State Lives in React](#state-lives-in-react)
    - [Rendering Takes a Snapshot in Time](#rendering-takes-a-snapshot-in-time)
    - [Example: What Will alert() Show?](#example-what-will-alert-show)
  - [Recap](#recap)
  - [Making State Work for You](#making-state-work-for-you)
    - [Structuring State](#structuring-state)
    - [Principles for Structuring State](#principles-for-structuring-state)
      - [Group Related State](#group-related-state)
      - [Avoid Contradictions](#avoid-contradictions)
      - [Avoid Redundancies](#avoid-redundancies)
      - [Avoid Data Duplication](#avoid-data-duplication)
      - [Avoid Deeply Nested State](#avoid-deeply-nested-state)
  - [Recap](#recap-1)
  - [Looking Ahead](#looking-ahead)
    - [Coming Up](#coming-up)

---

## How React Works

In order to develop React apps that are easy to maintain and debug, you’ll need to think in React. This means understanding what happens when state updates occur and how React renders and commits to the DOM, as well as how to design well-structured state.

To download the demo for this lecture:

```bash
dmget wb-react-works --demo
```

## Intro

## Goals

- Learn how rendering works in React.
- Tips for designing well-structured state.
- Later: use this knowledge to understand how to think in React and design effective UI.

## Rendering in React

### How Rendering Works in React

In React, rendering is the process of requesting and serving UI. It happens in three steps:

1. A render is triggered
2. Components are rendered
3. The final result is committed to the DOM

#### Step 1: A Render is Triggered

A render can be triggered for two reasons.

- **Initial render:** When your app starts, and you call `render()`.

  ```jsx
  // src/main.jsx
  ReactDOM.createRoot(document.getElementById("root")).render(
    <React.StrictMode>
      <App />
    </React.StrictMode>
  );
  ```

- **Re-render:** When you call a set function and update the state.

  ```jsx
  // src/components/Counter.jsx
  <button
    onClick={() => {
      setCount(count + 1);
    }}
  >
    Count is {count}
  </button>
  ```

#### Step 2: Components are Rendered by React

Once a render is triggered, React calls your components to figure out what to display.

- For **initial renders**, React will call the root component.
- For **re-renders**, React will call the component responsible for updating the state.

This happens recursively, all the way down the component hierarchy.

- So if the updated component has children, React will call each child component.
- ...and if the child has children, React will call those components too.
- ...and so on until there are no more nested components.

**React is smart about this:**

- During initial renders, React will create the DOM nodes required to display the UI.
- During re-renders, React will calculate which properties have changed. It won’t actually display anything until the next step.

#### Step 3: React Commits Changes to the DOM

After calling your components, React will modify the DOM.

- React only changes the DOM if there’s a difference between renders.
- And it will only calculate these differences based on the latest rendering output.

#### What Happens When You Click the Button?

```jsx
// src/components/Counter.jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button
      onClick={() => {
        setCount(count + 1);
      }}
    >
      Count is {count}
    </button>
  );
}
```

Here’s what happens when you click the button:

1. The `onClick` event handler executes.
2. `setCount(count + 1)` sets `count` and queues a new render.
3. React re-renders (calls) the component according to the new `count` value.
4. Changes are committed to the DOM, and the browser repaints the screen.

## State as a Snapshot

### What Happens When React Re-renders?

We learned that React renders by calling your component, which is a function. That function returns a snapshot of the UI in time, calculated based on state.

### State Lives in React

State isn’t a regular variable—it lives outside your function, where React can access it.

**State values are like post-it notes:**  
State values are kind of like post-it notes that React can reference and edit.

### Rendering Takes a Snapshot in Time

When you tell React to update state with a set function…

- React updates the state value.
- React passes the state values into the component.
- React calls the component, which creates a UI “snapshot” based on the given state.
- React updates the screen to match the snapshot.

The snapshot is calculated based on state at the time of render.

### Example: What Will alert() Show?

What will the alert display when we submit the form?

```jsx
// src/components/ShoutIt.jsx
function ShoutIt() {
  const [message, setMessage] = useState("hello world");

  const shoutMessage = (e) => {
    e.preventDefault();
    unfocusAllFields(e.target);

    setMessage(message.toUpperCase());
    alert(message);
  };

  return (
    <form onSubmit={shoutMessage}>
      <textarea value={message} onChange={(e) => setMessage(e.target.value)} />
      <button type="submit">SHOUT IT IN ALL CAPS!</button>
    </form>
  );
}
```

For the initial render, React creates a snapshot where `message = 'hello world'`.

```jsx
const shoutMessage = (e) => {
  e.preventDefault();
  unfocusAllFields(e.target);

  setMessage("hello world".toUpperCase());
  alert("hello world");
};
```

When the form submits, `alert` displays, “hello world”

Now, `message = 'HELLO WORLD'`, which results in this snapshot:

```jsx
const shoutMessage = (e) => {
  e.preventDefault();
  unfocusAllFields(e.target);

  setMessage("HELLO WORLD".toUpperCase());
  alert("HELLO WORLD");
};
```

If we submit the form (as long as `setMessage` doesn’t get called again), we’ll see “HELLO WORLD”

**How do we fix the bug?**

```jsx
const shoutMessage = (e) => {
  e.preventDefault();
  unfocusAllFields(e.target);

  alert(message.toUpperCase());
};
```

## Recap

Think of state as a snapshot that React stores outside of your component.

- Calling `useState` will give you a snapshot of state for that render.
- Event handlers created in the past will have state values from the render in which they were created.

## Making State Work for You

### Structuring State

Understanding how state works is only one part of React development.

You’ll also need to apply this knowledge to design good state values.

Your state can make the difference between an app that’s maintainable and easy to debug and one that’s a debugging nightmare.

### Principles for Structuring State

It takes practice and experience to develop a sense for designing state!

We’ll talk through some tips to keep in mind as you design React apps.

#### Group Related State

Let’s say we need to store a color as state.

```jsx
const [red, setRed] = useState(0);
const [green, setGreen] = useState(0);
const [blue, setBlue] = useState(0);
```

This will work, but you might forget to keep all three values in sync.

Since changing the color will change all three values, it’s better to use a single state value:

```jsx
const [color, setColor] = useState({
  red: 0,
  green: 0,
  blue: 0,
});
```

#### Avoid Contradictions

The `FileUploader` component that keeps track of `isUploading` and `isSent`:

```jsx
function FileUploader() {
  const [isUploading, setIsUploading] = useState(false);
  const [isSent, setIsSent] = useState(false);
}
```

This can cause a contradiction if `isUploading` and `isSent` are both set to `true`.

We can avoid possible

bugs by refactoring to use one `status` state variable:

```jsx
function FileUploader() {
  const [status, setStatus] = useState("waiting");

  // isUploading and isSent can be derived from status.
  const isUploading = status === "uploading";
  const isSent = status === "sent";
}
```

#### Avoid Redundancies

What could be redundant about the component below?

```jsx
function FullNameForm() {
  const [firstName, setFirstName] = useState("");
  const [lastName, setLastName] = useState("");
  const [fullName, setFullName] = useState("");
}
```

Since `fullName` can be derived from `firstName` and `lastName`, we don’t actually need it to be a state variable!

```jsx
function FullNameForm() {
  const [firstName, setFirstName] = useState("");
  const [lastName, setLastName] = useState("");
  const fullName = `${firstName} ${lastName}`;
}
```

#### Avoid Data Duplication

`MovieWidget` displays your top five films and allows you to choose one favorite.

```jsx
function MovieWidget() {
  const [topFive, setTopFive] = useState([
    { title: "Gremlings", id: 2 },
    { title: "The Black Knight Rises", id: 10 },
    { title: "The Gabgadook", id: 7 },
    // etc.
  ]);
  const [fav, setFav] = useState("Gremlings");
}
```

The `'Gremlings'` movie is stored in two places: `topFive` and `fav`. This can cause the data to go out of sync.

Instead, store the ID of the favorite and derive `fav` from the `topFive` array:

```jsx
function MovieWidget() {
  const [topFive, setTopFive] = useState([
    { title: "Gremlings", id: 2 },
    { title: "The Black Knight Rises", id: 10 },
    { title: "The Gabgadook", id: 7 },
    // etc.
  ]);
  const [favId, setFavId] = useState(2);

  const fav = topFive.find((movie) => movie.id === favId);
}
```

#### Avoid Deeply Nested State

Nested objects are very difficult to work with, so try to keep your data as flat as possible.

```jsx
const socialNetwork = {
  id: 0,
  name: "Clive",
  friends: [
    {
      id: 1,
      name: "Jill",
      friends: [
        {
          id: 2,
          name: "Joshua",
          friends: [],
        },
      ],
    },
    {
      id: 3,
      name: "Cid",
      friends: [
        {
          id: 4,
          name: "Benedikta",
          friends: [],
        },
      ],
    },
  ],
};
```

One way to flatten `socialNetwork` is to store friend IDs instead of friend objects:

```jsx
const socialNetwork = {
  0: {
    id: 0,
    name: "Clive",
    friendIds: [1, 3],
  },
  1: {
    id: 1,
    name: "Jill",
    friendIds: [0, 2],
  },
  2: {
    id: 2,
    name: "Joshua",
    friendIds: [],
  },
  3: {
    id: 3,
    name: "Cid",
    friendIds: [4],
  },
  4: {
    id: 4,
    name: "Benedikta",
    friendIds: [],
  },
};
```

## Recap

Make state work for you!

- Structure your state to make it easy to update and reduce chances for mistakes.
- Group related state together.
- Avoid creating opportunities for contradictory state.
- Avoid redundancies and data duplication (use IDs!).
- Rearrange nested objects so they’re easier to work with.

## Looking Ahead

### Coming Up

- Code Along: Thinking in React

---
