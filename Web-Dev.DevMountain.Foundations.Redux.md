---
id: v78grc04fhw0e4iqrp6aqlg
title: Redux
desc: ""
updated: 1722791244970
created: 1722791235842
---

Here's the webpage content formatted into Markdown:

---

# On this Page

- [Redux Intro](#redux-intro)
- [What is Redux?](#what-is-redux)
- [Redux Dataflow](#redux-dataflow)
  - [Actions](#actions)
  - [Reducers](#reducers)
  - [Store](#store)
- [React Redux](#react-redux)
  - [Adding the Store and Reducer](#adding-the-store-and-reducer)
  - [Subscribing A Component](#subscribing-a-component)
  - [Action Creators](#action-creators)
  - [Async Operations](#async-operations)
    - [Async Thunks](#async-thunks)

---

## Redux Intro

An introduction to Redux.

To download the demo code for this lecture, run:

```bash
dmget wb-redux --demo
```

Then, `cd` into the project directory and use npm to install and run the dev server:

```bash
npm install
npm install @reduxjs/toolkit react-redux
npm run dev
```

## What is Redux?

- A library for managing and updating application state, using events called actions.
- Centralized store for state that needs to be used across your entire application.
- Has rules ensuring that state can only be updated in a predictable fashion.

## Redux Dataflow

### Redux Dataflow

In React, data flows unidirectionally. This means that we can only pass data from a parent to a child component. This can become a hassle and pretty complex when we start dealing with large-scale applications. Data may need to be passed down through several levels of child components until it reaches the desired destination.

Redux allows us to store our state in a single place called the store. Components can subscribe to the store to gain access to state values directly. This prevents having to pass that data from component to component. Components will then dispatch changes to the store to update the state values. All components that are subscribed to the store will receive those state updates.

### Actions

An action is a plain JavaScript object that has a `type` field. You can think of an action as an event that describes something that happened in the app.

An action object can also store additional information about what happened. By convention, we put that information in a field called `payload`.

```javascript
const addTodoAction = {
  type: "todoAdded",
  payload: "Buy milk",
};
```

### Reducers

In Redux, we write a function called a reducer to handle all state updates.

- The reducer will take in the current state object and an action object.
- It cannot modify the existing state directly. It must either return a new state value or modify a copy of the state.

**wb-redux-demo/src/reducer.js**

```javascript
const initialState = { count: 0 };

// eslint-disable-next-line default-param-last
export default function reducer(state = initialState, action) {
  switch (action.type) {
    case "increment":
      // reassign value of "count", leave rest of state unchanged
      return { ...state, count: state.count + 1 };
    case "decrement":
      return { ...state, count: state.count + action.payload };
    default:
      return state; // return the existing state unchanged
  }
}
```

### Store

The store is what holds the global state for our application. The only way to change the values on this state is to dispatch an action to it.

- The store is created by calling the `configureStore` function and passing in our reducer.

**wb-redux-demo/src/store.js**

```javascript
import { configureStore } from "@reduxjs/toolkit";
import reducer from "./reducer.js";

// this function creates the store and we pass our root reducer to it
export default configureStore({
  reducer: reducer,
});
```

## React Redux

React Redux is the official binding for using Redux in a React application. This means that the `react-redux` package was created and is maintained by the React team, specifically for using React & Redux together.

We will now add our store and reducer to our app using `react-redux`.

### Adding the Store and Reducer

Inside `main.jsx`, we will wrap our App component inside of a `Provider`. The `Provider` is a higher-order component that will provide the redux store to our app.

**wb-redux-demo/src/main.jsx**

```javascript
import { Provider } from "react-redux";
import App from "./App.jsx";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

### Subscribing A Component

Now that we have redux set up, let’s go ahead and get our App component subscribed to the redux store. We will be using two hooks for this, `useSelector` and `useDispatch`.

- `useSelector` subscribes our component to the store and allows it to access state values. For instance:

  ```javascript
  const count = useSelector((state) => state.count);
  ```

- `useDispatch` returns a function that allows us to dispatch actions to the store.

  ```javascript
  const dispatch = useDispatch();

  <button onClick={() => dispatch({'type': 'decrement'})}>Decrement</button>
  <button onClick={() => dispatch({'type': 'increment'})}>Increment</button>
  ```

When we dispatch an action, the store runs the reducer and calculates the updated state based on the action that was dispatched.

### Action Creators

To make our actions more flexible, we can return them inside functions called action creators. This allows us to take in additional arguments which can be passed to the action’s payload:

```javascript
function addAmount(amount) {
  return { type: "incrementByAmount", payload: amount };
}
```

To dispatch the action, just do `dispatch(addAmount(amount))`.

### Async Operations

#### Async Operations with Redux

Redux reducers cannot perform any kind of asynchronous operation. If we want to perform an asynchronous operation to update the state, we need to put that operation in a separate async function, called a thunk.

When we set up the store with `configureStore()`, we automatically set up the `redux-thunk` middleware which handles these async functions.

#### Async Thunks

An async thunk will take the `dispatch` function as a parameter and invoke this function to dispatch actions to the store. For example:

```javascript
// A mock function to mimic making an async request for data
function fetchAmount(amount) {
  return new Promise((resolve) => {
    setTimeout(() => resolve(Number(amount)), 1000);
  });
}

export const incrementAsync = async (dispatch) => {
  const result = await fetchAmount(1);
  dispatch({ type: "incrementByAmount", payload: result });
};
```

We can then dispatch the thunk like an action object:

```javascript
<button onClick={() => dispatch(incrementAsync)}>Increment Async</button>
```

We can also put the thunk inside an action creator:

**wb-redux-demo/src/async.js**

```javascript
export default function addAmountAsync(amount) {
  return async (dispatch) => {
    const result = await fetchAmount(amount);
    dispatch({ type: "incrementByAmount", payload: result });
  };
}
```

And dispatch it like this:

```javascript
dispatch(addAmountAsync(incrementAmount));
```

---
