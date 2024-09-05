---
id: u3p8a43xflucxwvz2lhm426
title: Project4
desc: ''
updated: 1721501286270
created: 1721415201246
---

````markdown
# Project Overview

The app you’ll be working on in this unit is called **Social Mountain**. It is a basic social media app that allows anyone to see public text posts. In order to create a post, users must log in. They can also see their own private posts when they are logged in. You’ll get to practice authentication and build an entire server that interacts with your database.

## MVP Features

- User can login and logout
- User can create posts
- User can edit and delete their own posts
- User can view others’ posts

## Code

- Uses React context
- Uses JWT to authenticate users
- Uses an express server
- Uses Sequelize to connect to a database from the server
- Contains models for Post and User
- Uses middleware to authenticate protected endpoints

# Creating an Express Server

## Objectives

- Student can explain what NodeJS is
- Student can explain what Express is
- Student can setup a boilerplate Express Server
- Student can create endpoints and handle requests in a controller file
- Student understands the request/response model in Node
- Student understands Node Modules

## Summary

Creating servers with NodeJS and Express is essential as a Web Developer. Today you will review some of the material you already knew from foundations, and add some additional information in as well.

## Content

- NodeJS and Express

# Project Part 1: Creating your Server

## Goals

- Set up the Server File
- Set up your Endpoints
- Set up your Controller Files
- Set up server folder structure
- Create AuthContext File

## Steps

1. Download starter code and setup project
   - (/Users/ryansmith/Library/Mobile Documents/com~apple~CloudDocs/Dev/DevMountain/Specializations12/Specs-Unit4/react-proj-4.zip)
   1. Once you have downloaded the starter code, open a terminal and `cd` into the starter folder.
   2. Run `npm i` to install the needed packages.
2. Server Folder Structure
   1. Inside of your root folder, create a folder called `server`.
   2. Inside of `/server`, create a `util` folder, a `middleware` folder, a `models` folder, and a `controllers` folder.
3. Create Server File `index.js`
   1. Inside of `/server`, create an `index.js` file.
   2. Write out an express server that has the requirements at the top, middleware after that, and a listen statement at the bottom.

```javascript
const express = require("express");
const cors = require("cors");
const app = express();
const PORT = process.env.PORT || 4004;

app.use(express.json());
app.use(cors());

app.listen(PORT, () => console.log(`Running on Port ${PORT}`));
```

4. Create Auth Controller Functions
   1. Inside `/server/controllers`, create a file called `auth.js`.
   2. Inside, you will create two functions called `login` and `register`. The functions will handle `req` and `res` as parameters, will be asynchronous, and will only have two lines for each function. Add a `console.log` indicating the function name as a string (login or register), and a `res.sendStatus(200)`.

#### Sidenote/Explanation:

The purpose of creating the `login` and `register` functions inside `auth.js` with minimal implementation (a `console.log` statement and a `res.sendStatus(200)`) is to establish the basic structure and functionality of these endpoints in a simplified form. This allows you to verify that the server is correctly set up to handle authentication-related requests before implementing more complex logic. Here's a detailed breakdown of the purpose:

1. **Verify Endpoint Setup**:

   - By creating basic `login` and `register` functions that log their invocation and return a status code, you ensure that the endpoints are correctly defined and can be accessed. This helps catch any configuration or routing errors early.

2. **Simplify Debugging**:

   - Starting with minimal functionality makes it easier to isolate and identify problems. If the server fails to handle these requests correctly, you know the issue lies in the basic setup rather than in more complex logic.

3. **Incremental Development**:

   - Implementing endpoints incrementally allows you to build and test the application step-by-step. Once you confirm that the basic endpoints work, you can gradually add more complex features, such as user authentication, token generation, and database interactions, while ensuring that each part works correctly before moving on to the next.

4. **Clear Starting Point for Enhancements**:
   - With a basic but functional structure in place, you have a clear starting point for adding more sophisticated logic. You can replace the `console.log` and `res.sendStatus(200)` with actual authentication logic, such as checking user credentials, generating tokens, and handling errors.

Here's an example of what the initial setup might look like:

```javascript
// server/controllers/auth.js

module.exports = {
  login: async (req, res) => {
    console.log("login");
    res.sendStatus(200);
  },
  register: async (req, res) => {
    console.log("register");
    res.sendStatus(200);
  },
};
```

This minimal setup ensures that:

- The server can handle POST requests to the `/login` and `/register` endpoints.
- You receive console output (`login` or `register`) when these endpoints are hit, which confirms that the requests are routed correctly.
- The server responds with a status code `200`, indicating that the requests are successfully processed (even though no actual authentication logic is implemented yet).

Once this basic functionality is confirmed, you can proceed to implement the actual logic for user registration and login, knowing that the endpoints themselves are correctly set up and reachable.

5. Create Post Controller Functions
   1. Inside `/server/controllers`, create a file called `posts.js`.
   2. Inside, you will follow similar syntax as the `auth.js` controller file, but you will create five functions: `addPost`, `getAllPosts`, `getCurrentUserPosts`, `editPost`, and `deletePost`.

#### Sidenote/Explanation:

The purpose of creating the functions `addPost`, `getAllPosts`, `getCurrentUserPosts`, `editPost`, and `deletePost` inside the `posts.js` file with minimal implementation (a `console.log` statement and a `res.sendStatus(200)`) is similar to the purpose of the initial setup for the `auth.js` file. This approach helps establish and verify the basic structure and functionality of the CRUD (Create, Read, Update, Delete) operations for posts before implementing more complex logic. Here's a detailed breakdown of the purpose:

1. **Verify Endpoint Setup**:

   - By creating basic functions that log their invocation and return a status code, you ensure that the endpoints for handling posts are correctly defined and can be accessed. This helps catch any configuration or routing errors early.

2. **Simplify Debugging**:

   - Starting with minimal functionality makes it easier to isolate and identify problems. If the server fails to handle these requests correctly, you know the issue lies in the basic setup rather than in more complex logic related to post handling.

3. **Incremental Development**:

   - Implementing endpoints incrementally allows you to build and test the application step-by-step. Once you confirm that the basic endpoints work, you can gradually add more complex features, such as database interactions, user authentication checks, and data validation, while ensuring that each part works correctly before moving on to the next.

4. **Clear Starting Point for Enhancements**:
   - With a basic but functional structure in place, you have a clear starting point for adding more sophisticated logic. You can replace the `console.log` and `res.sendStatus(200)` with actual logic for creating, retrieving, updating, and deleting posts.

Here's an example of what the initial setup might look like:

```javascript
// server/controllers/posts.js

module.exports = {
  addPost: async (req, res) => {
    console.log("addPost");
    res.sendStatus(200);
  },
  getAllPosts: async (req, res) => {
    console.log("getAllPosts");
    res.sendStatus(200);
  },
  getCurrentUserPosts: async (req, res) => {
    console.log("getCurrentUserPosts");
    res.sendStatus(200);
  },
  editPost: async (req, res) => {
    console.log("editPost");
    res.sendStatus(200);
  },
  deletePost: async (req, res) => {
    console.log("deletePost");
    res.sendStatus(200);
  },
};
```

This minimal setup ensures that:

- The server can handle requests to the endpoints for adding, retrieving, updating, and deleting posts.
- You receive console output (e.g., `addPost`, `getAllPosts`, etc.) when these endpoints are hit, which confirms that the requests are routed correctly.
- The server responds with a status code `200`, indicating that the requests are successfully processed (even though no actual post handling logic is implemented yet).

Once this basic functionality is confirmed, you can proceed to implement the actual logic for each operation:

- `addPost`: Logic for adding a new post to the database.
- `getAllPosts`: Logic for retrieving all posts.
- `getCurrentUserPosts`: Logic for retrieving posts created by the currently logged-in user.
- `editPost`: Logic for updating an existing post.
- `deletePost`: Logic for deleting an existing post.

This approach helps you build a robust and scalable backend system by ensuring that each component works correctly before integrating more complex features.

6. Create RESTful Endpoints
   1. Inside of your `/server/index.js` file, we are going to create endpoints for our application. It will be helpful if you group them according to functionality or feature.
   2. Create a `post` request to `/register`, and link it to the register function we created in the `auth.js` controller file.
   3. Create a `post` request to `/login`, and link it to the login function we created in the `auth.js` controller file.
   4. Create a `get` request to `/posts`, and link it to the `getAllPosts` function we created in the `posts.js` controller file.
   5. Create a `get` request to `/userposts/:userId`, and link it to the `getCurrentUserPosts` function we created in the `posts.js` controller file. For this endpoint, the `userId` is a variable that can be accessed with `req.params`.
   6. Create a `post` request to `/posts`, and link it to the `addPost` function we created in the `posts.js` controller file.
   7. Create a `put` request to `/posts/:id`, and link it to the `editPost` function we created in the `posts.js` controller file. For this endpoint, the `id` is a variable that can be accessed with `req.params`.
   8. Create a `delete` request to `/posts/:id`, and link it to the `deletePost` function we created in the `posts.js` controller file. For this endpoint, the `id` is a variable that can be accessed with `req.params`.

#### Sidenote/Explanation Restful Endpoints

The purpose of creating endpoints for your application inside the `/server/index.js` file and grouping them according to functionality or feature is to organize and define the routes your server will handle. This setup ensures that your server can respond to specific HTTP requests made by clients, such as creating a post, retrieving posts, or handling user authentication. Here's a detailed breakdown of the purpose:

1. **Define Route Handlers**:

   - Each endpoint corresponds to a specific route and HTTP method (GET, POST, PUT, DELETE). By defining these routes, you specify how the server should handle different types of requests. For example, `app.post("/register", register);` tells the server to execute the `register` function whenever a POST request is made to the `/register` route.

2. **Organize Code by Feature**:

   - Grouping endpoints by functionality or feature (e.g., authentication-related routes, post-related routes) makes the code more organized and easier to maintain. This approach helps developers quickly locate and update specific parts of the codebase.

3. **Facilitate Incremental Development**:

   - Setting up basic endpoints allows you to incrementally develop and test each part of your application. Initially, these endpoints might just log messages or return simple status codes, but as development progresses, you can add more complex logic to handle database interactions, user authentication, and other features.

4. **Enable Client-Server Communication**:

   - Endpoints define how the client (e.g., a web or mobile app) interacts with the server. They provide a structured way for clients to request data, submit data, and perform actions. For example, `app.get("/posts", getAllPosts);` allows clients to retrieve all posts from the server.

5. **Handle Different HTTP Methods**:

   - Different HTTP methods (GET, POST, PUT, DELETE) are used for different types of operations. Defining endpoints with these methods ensures that your server can handle a variety of operations, such as creating new resources, retrieving existing resources, updating resources, and deleting resources.

Here's an example of what this setup might look like:

```javascript
// Import the necessary functions from the controllers
const {
  getAllPosts,
  getCurrentUserPosts,
  addPost,
  editPost,
  deletePost,
} = require("./controllers/posts");
const { register, login } = require("./controllers/auth");

// Define authentication-related routes
app.post("/register", register);
app.post("/login", login);

// Define post-related routes
app.get("/posts", getAllPosts);
app.get("/userposts/:userId", getCurrentUserPosts);
app.post("/posts", addPost);
app.put("/posts/:id", editPost);
app.delete("/posts/:id", deletePost);
```

### Detailed Explanation of Each Endpoint

1. **Authentication Endpoints**:

   - `app.post("/register", register);`: Handles user registration by executing the `register` function when a POST request is made to the `/register` route.
   - `app.post("/login", login);`: Handles user login by executing the `login` function when a POST request is made to the `/login` route.

2. **Post-Related Endpoints**:

   - `app.get("/posts", getAllPosts);`: Retrieves all posts by executing the `getAllPosts` function when a GET request is made to the `/posts` route.
   - `app.get("/userposts/:userId", getCurrentUserPosts);`: Retrieves posts created by a specific user by executing the `getCurrentUserPosts` function when a GET request is made to the `/userposts/:userId` route. The `:userId` is a route parameter that specifies which user's posts to retrieve.
   - `app.post("/posts", addPost);`: Adds a new post by executing the `addPost` function when a POST request is made to the `/posts` route.
   - `app.put("/posts/:id", editPost);`: Updates an existing post by executing the `editPost` function when a PUT request is made to the `/posts/:id` route. The `:id` is a route parameter that specifies which post to update.
   - `app.delete("/posts/:id", deletePost);`: Deletes an existing post by executing the `deletePost` function when a DELETE request is made to the `/posts/:id` route. The `:id` is a route parameter that specifies which post to delete.

By setting up these endpoints, you lay the foundation for your server's API, allowing clients to interact with the backend to perform various operations related to user authentication and post management.

# Understanding `AuthContext.js`

In short, context allows multiple components at different levels of our app access to the same information. For this application, we have combined `useContext` with `useReducer` to create a powerful state management system.

Notice the `initialState` object. This contains the key-value pairs that we want to start off our application using. Since we have neither a user nor a token, both are set to null.

The `initialState` is used by the `useReducer` hook to create an instance of state that can be consumed at large by simply referencing `state` followed by the key you wish to reference (such as `state.token`). The `reducer` function takes in the current value of state and an action as parameters. The state is whatever the current value of state is, and the action is an object that contains information about what state should be altered, how it should be altered, and any additional information that needs to be added or taken away from state.

By passing both the `reducer` function and the `initialState` to `useReducer`, we get one variable and one function returned to us in an array, `[state, dispatch]`. We then pass both of these values in as the values for our `AuthContext.Provider` to provide to our application.

#### Sidenote/Explanation:

Here's a more detailed explanation of `AuthContext`, its purpose, and how it works in conjunction with `useContext` and `useReducer` in a React application.

### Understanding `AuthContext`

`AuthContext` is a context object created using React's `createContext` function. It provides a way to share state (such as user authentication data) across multiple components in a React application without having to pass props down manually at every level.

### Key Concepts

1. **Context**:

   - Context allows you to create a global state that can be accessed by any component in the application.
   - `createContext` creates a context object that holds the global state and provides it to the components.

2. **useContext**:

   - `useContext` is a React hook that allows components to consume the context created by `createContext`.
   - It simplifies accessing the context value, avoiding the need to use the `Consumer` component.

3. **useReducer**:
   - `useReducer` is a React hook that provides an alternative to `useState` for managing complex state logic.
   - It takes a reducer function and an initial state as arguments and returns the current state and a dispatch function to trigger state updates.

### Setting Up `AuthContext`

1. **Initial State**:
   - The `initialState` object defines the initial values for the state properties. In an authentication context, it typically includes properties like `user` and `token`.

```javascript
const initialState = {
  user: null,
  token: null,
};
```

2. **Reducer Function**:
   - The `reducer` function defines how the state should be updated in response to different actions. It takes the current state and an action as parameters and returns the new state.

```javascript
const reducer = (state, action) => {
  switch (action.type) {
    case "LOGIN":
      return {
        ...state,
        user: action.payload.user,
        token: action.payload.token,
      };
    case "LOGOUT":
      return { ...state, user: null, token: null };
    default:
      return state;
  }
};
```

3. **Creating the Context**:
   - The context is created using `createContext`, and the provider component (`AuthContext.Provider`) is set up to provide the state and dispatch function to the rest of the application.

```javascript
import React, { createContext, useReducer } from "react";

const AuthContext = createContext();

const AuthProvider = ({ children }) => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <AuthContext.Provider value={{ state, dispatch }}>
      {children}
    </AuthContext.Provider>
  );
};

export { AuthContext, AuthProvider };
```

### Using `AuthContext` in Components

1. **Providing the Context**:
   - Wrap the component tree with the `AuthProvider` to make the context available to all nested components.

```javascript
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import { AuthProvider } from "./AuthContext";

ReactDOM.render(
  <AuthProvider>
    <App />
  </AuthProvider>,
  document.getElementById("root")
);
```

2. **Consuming the Context**:
   - Use the `useContext` hook to access the context value in any component.

```javascript
import React, { useContext } from "react";
import { AuthContext } from "./AuthContext";

const SomeComponent = () => {
  const { state, dispatch } = useContext(AuthContext);

  const handleLogin = () => {
    dispatch({ type: "LOGIN", payload: { user: "John Doe", token: "abc123" } });
  };

  return (
    <div>
      {state.user ? (
        <div>
          <h1>Welcome, {state.user}</h1>
          <button onClick={() => dispatch({ type: "LOGOUT" })}>Logout</button>
        </div>
      ) : (
        <button onClick={handleLogin}>Login</button>
      )}
    </div>
  );
};

export default SomeComponent;
```

### Summary

- **Context**: Provides a way to share state across the component tree without passing props down manually at every level.
- **useContext**: Allows components to consume context values easily.
- **useReducer**: Manages complex state logic by using a reducer function to handle state updates based on actions.
- **AuthContext**: Combines `useContext` and `useReducer` to manage global authentication state, making it accessible throughout the application.

By using `AuthContext`, you can manage user authentication state efficiently, ensuring that components at different levels of the application have access to the necessary authentication data. This approach leads to cleaner, more maintainable code by avoiding prop drilling and centralizing state management logic.

For more information on how this operates, see the React Docs for more information (scroll down to Examples of updating context).

## Making Auth Context Available App-wide

In `src/index.js`, import `AuthContextProvider` from the store.

Wrap your `App` component with the provider. (You can wrap it around `BrowserRouter` as well).

This will allow any component in your app to access the auth context with the `useContext` hook!

```javascript
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import { BrowserRouter } from "react-router-dom";
import { AuthContextProvider } from "./store/authContext";

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(
  <React.StrictMode>
    <AuthContextProvider>
      <BrowserRouter>
        <App />
      </BrowserRouter>
    </AuthContextProvider>
  </React.StrictMode>
);
```

#### Sidenote/Explanation

Let's break down the code provided and explain each part in detail:

### Explanation of `src/index.js` Setup

1. **Import Statements**:

   ```javascript
   import React from "react";
   import ReactDOM from "react-dom/client";
   import "./index.css";
   import App from "./App";
   import { BrowserRouter } from "react-router-dom";
   import { AuthContextProvider } from "./store/authContext";
   ```

   - **React**: This is the core library for building user interfaces in React.
   - **ReactDOM**: This library provides DOM-specific methods that allow you to mount React components into the DOM.
   - **"./index.css"**: This is where you import global CSS styles for your application.
   - **`App`**: This is the root component of your application, where most of your app's main functionality will reside.
   - **`BrowserRouter`**: This is a component from `react-router-dom` that enables client-side routing in your application, allowing you to navigate between different pages.
   - **`AuthContextProvider`**: This is a custom provider component from your context store. It will provide authentication state and functionality to the entire application.

2. **Creating the Root Element**:

   ```javascript
   const root = ReactDOM.createRoot(document.getElementById("root"));
   ```

   - `ReactDOM.createRoot` is a method from the `react-dom` package that creates a root DOM node for your React application. This is where your entire app will be mounted.
   - `document.getElementById("root")` is a standard DOM method that selects the HTML element with the id of "root". This element is usually defined in your `index.html` file and acts as the container for your React app.

3. **Rendering the Application**:
   ```javascript
   root.render(
     <React.StrictMode>
       <AuthContextProvider>
         <BrowserRouter>
           <App />
         </BrowserRouter>
       </AuthContextProvider>
     </React.StrictMode>
   );
   ```
   - **`React.StrictMode`**: This is a wrapper component provided by React that helps you write better React code. It activates additional checks and warnings for its descendants in development mode. It doesn't affect the production build.
   - **`AuthContextProvider`**: This is the context provider component for your authentication context. Wrapping your application with this component ensures that the authentication state and dispatch functions are available throughout your entire app. This allows any component within the app to access and update the authentication state using the `useContext` hook.
   - **`BrowserRouter`**: This component wraps your app and enables client-side routing. It listens to changes in the browser's address bar and renders the corresponding components. Wrapping your app with `BrowserRouter` makes routing features (like `Route`, `Link`, `NavLink`) available throughout your app.
   - **`App`**: This is your main application component, which contains the overall structure and logic of your app. It's the top-level component where you typically define your routes and major layout elements.

### Why This Setup Is Important

1. **Context and State Management**:

   - By wrapping your application with `AuthContextProvider`, you ensure that the authentication state is managed centrally and is accessible throughout your app. This makes it easier to manage and update authentication-related data, such as user information and JWT tokens, without having to pass props down multiple levels of the component tree (avoiding "prop drilling").

2. **Routing**:

   - `BrowserRouter` enables seamless client-side routing, allowing you to create a single-page application (SPA) where navigation to different views doesn't require a full page reload. This provides a smoother and faster user experience.

3. **Strict Mode**:
   - Using `React.StrictMode` helps you identify potential problems in your application during the development phase. It doesn't affect your app in production but can catch common issues and provide warnings to help you follow best practices.

### How It Works Together

- **Context Provider**:

  - When `AuthContextProvider` wraps the application, it makes the authentication state available to all components within the `App` component. Any component can then use the `useContext` hook to access or update the authentication state.

- **BrowserRouter**:

  - Wrapping the `App` component with `BrowserRouter` ensures that all components within `App` can use routing features. This allows you to define routes and navigation logic within `App` and its children.

- **Application Rendering**:
  - The `root.render` method mounts the entire application into the DOM element with the id "root". It ensures that the `App` component and all its children are rendered within this root element, with the context and routing features properly set up.

By following this setup, you create a robust foundation for your React application that supports global state management through context and efficient client-side routing, ensuring a scalable and maintainable codebase.

## Restrict Views in `App.js`

Now that users have the ability to log in, let’s change some of our pages to only be viewable if you’re logged in.

In `App.js`, import `useContext` from React and the `AuthContext` from your store.

Inside the component, destructure `{state}` from invoking `useContext` passing in `AuthContext`. This will allow the `App` component to hook into the auth context!

In the `Auth` route’s element prop, check if there is a `state.token` in context. If there isn’t, send users to `Auth`, if there is, use the `Navigate` component to send them to the home path.

Using a similar method (checking for the `state.token` and utilizing `Navigate`), send unauthenticated users to the authentication form if they try to view the form or profile pages.

```javascript
import { useContext } from "react";
import { Routes, Route, Navigate } from "react-router-dom";
import "./App.css";

import Header from "./components/Header";
import Home from "./components/Home";
import Auth from "./components/Auth";
import Form from "./components/Form";
import Profile from "./components/Profile";

import AuthContext from "./store/authContext";

const App = () => {
  const { state } = useContext(AuthContext);

  return (
    <div className="app">
      <Header />
      <Routes>
        <Route path="/" element={<Home />} />
        <Route
          path="/auth"
          element={!state.token ? <Auth /> : <Navigate to="/" />}
        />
        <Route
          path="/form"
          element={state.token ? <Form /> : <Navigate to="/auth" />}
        />
        <Route
          path="/profile"
          element={state.token ? <Profile /> : <Navigate to="/auth" />}
        />
        <Route path="*" element={<Navigate to="/" />} />
      </Routes>
    </div>
  );
};

export default App;
```

#### Sidenote/Explanation:

Certainly! Let's break down the provided code and explain each part in detail, focusing on how the `AuthContext` is used to control access to different routes in the application.

### Explanation of the Code in `App.js`

1. **Import Statements**:

   ```javascript
   import { useContext } from "react";
   import { Routes, Route, Navigate } from "react-router-dom";
   import "./App.css";

   import Header from "./components/Header";
   import Home from "./components/Home";
   import Auth from "./components/Auth";
   import Form from "./components/Form";
   import Profile from "./components/Profile";

   import AuthContext from "./store/authContext";
   ```

   - **`useContext`**: A React hook that allows you to consume context values. It is used here to access the authentication state from `AuthContext`.
   - **`Routes`, `Route`, `Navigate`**: Components from `react-router-dom` that enable client-side routing. `Routes` is a container for all route definitions, `Route` defines individual routes, and `Navigate` is used to programmatically navigate to different routes.
   - **`"./App.css"`**: CSS file for styling the `App` component.
   - **Component Imports (`Header`, `Home`, `Auth`, `Form`, `Profile`)**: These are the main components rendered in different routes of the application.
   - **`AuthContext`**: The authentication context created using `createContext` in your context store. This context provides the authentication state and dispatch functions.

2. **Defining the `App` Component**:

   ```javascript
   const App = () => {
     const { state } = useContext(AuthContext);
   ```

   - **`useContext(AuthContext)`**: This line uses the `useContext` hook to access the current value of `AuthContext`. By destructuring `{ state }`, you get the current authentication state which includes the `token` indicating if the user is authenticated.

3. **Rendering the Application**:

   ```javascript
     return (
       <div className="app">
         <Header />
         <Routes>
           <Route path="/" element={<Home />} />
           <Route
             path="/auth"
             element={!state.token ? <Auth /> : <Navigate to="/" />}
           />
           <Route
             path="/form"
             element={state.token ? <Form /> : <Navigate to="/auth" />}
           />
           <Route
             path="/profile"
             element={state.token ? <Profile /> : <Navigate to="/auth" />}
           />
           <Route path="*" element={<Navigate to="/" />} />
         </Routes>
       </div>
     );
   };

   export default App;
   ```

### Detailed Breakdown

1. **Component Structure**:

   - The `App` component is the main component of the application, containing the layout and routing logic.
   - It renders the `Header` component and a `Routes` component that defines the route paths and their corresponding components.

2. **Routes Configuration**:
   - **`<Route path="/" element={<Home />} />`**: This route renders the `Home` component when the path is `/`. It is accessible to all users.
   - **`<Route path="/auth" element={!state.token ? <Auth /> : <Navigate to="/" />} />`**: This route renders the `Auth` component when the path is `/auth`, but only if `state.token` is `null` (i.e., the user is not authenticated). If `state.token` exists (i.e., the user is authenticated), it navigates to the home page (`/`) using the `Navigate` component.
   - **`<Route path="/form" element={state.token ? <Form /> : <Navigate to="/auth" />} />`**: This route renders the `Form` component when the path is `/form`, but only if `state.token` exists (i.e., the user is authenticated). If `state.token` is `null` (i.e., the user is not authenticated), it navigates to the authentication page (`/auth`) using the `Navigate` component.
   - **`<Route path="/profile" element={state.token ? <Profile /> : <Navigate to="/auth" />} />`**: This route renders the `Profile` component when the path is `/profile`, but only if `state.token` exists (i.e., the user is authenticated). If `state.token` is `null` (i.e., the user is not authenticated), it navigates to the authentication page (`/auth`) using the `Navigate` component.
   - **`<Route path="*" element={<Navigate to="/" />} />`**: This route acts as a catch-all for any undefined paths, redirecting them to the home page (`/`).

### Purpose and Functionality

1. **Conditional Routing Based on Authentication State**:

   - The `useContext(AuthContext)` hook provides access to the current authentication state (`state`). By checking the presence of `state.token`, the application can determine if the user is authenticated.
   - This setup ensures that certain routes (like `/form` and `/profile`) are only accessible to authenticated users. If an unauthenticated user tries to access these routes, they are redirected to the `/auth` page to log in.

2. **User Experience**:

   - By redirecting unauthenticated users to the login page, the application ensures that only authenticated users can access sensitive or personalized pages, enhancing security and user experience.
   - Authenticated users are redirected to the home page if they try to access the login page, providing a seamless experience by avoiding unnecessary access to the login page once they are logged in.

3. **Centralized Authentication Logic**:
   - The logic for checking authentication and redirecting users is centralized in the `App` component, making it easier to manage and update as needed.
   - This approach promotes a clean and maintainable codebase, as the authentication checks and redirections are handled in one place rather than scattered across multiple components.

Overall, this code ensures that your React application has a robust authentication flow, controlling access to different routes based on the user's authentication status. This setup enhances both the security and usability of your application.

## CHALLENGE: Restrict Links in `Header`

Using similar logic used in creating our routes, restrict the `Header` component to only display Profile and Add Post if there is a token stored inside of state.

```javascript
const Header = () => {
  const { state, dispatch } = useContext(AuthContext);

  const styleActiveLink = ({ isActive }) => {
    return {
      color: isActive ? "#f57145" : "",
    };
  };

  return (
    <header className="header flex-row">
      <div className="flex-row">
        <img src={logo} alt="dm-logo" className="logo" />
        <h2>Social Mountain</h2>
      </div>
      <nav>
        {state.token ? (
          <ul className="main-nav">
            <li>
              <NavLink style={styleActiveLink} to="/">
                Home
              </NavLink>
            </li>
            <li>
              <NavLink style={styleActiveLink} to="profile">
                Profile
              </NavLink>
            </li>
            <li>
              <NavLink style={styleActiveLink} to="form">
                Add Post
              </NavLink>
            </li>
            <li>
              <button
                className="logout-btn"
                onClick={() => dispatch({ type: "LOGOUT" })}
              >
                Logout
              </button>
            </li>
          </ul>
        ) : (
          <ul className="main-nav">
            <li>
              <NavLink style={styleActiveLink} to="/">
                Home
              </NavLink>
            </li>
            <li>
              <NavLink style={styleActiveLink} to="/auth">
                Login or Sign Up
              </NavLink>
            </li>
          </ul>
        )}
      </nav>
    </header>
  );
};
```

#### Sidenote/Explanation:

Sure! Let's break down the provided `Header` component code and explain each part in detail, focusing on how it uses the authentication state to conditionally render navigation links.

### Explanation of the `Header` Component

1. **Import Statements and Context Setup**:

   ```javascript
   import React, { useContext } from "react";
   import { NavLink } from "react-router-dom";
   import AuthContext from "./store/authContext";
   import logo from "./path/to/logo"; // Assuming you have the logo file

   const Header = () => {
     const { state, dispatch } = useContext(AuthContext);
   ```

   - **`useContext`**: A React hook that allows you to consume context values. It is used here to access the authentication state and dispatch function from `AuthContext`.
   - **`NavLink`**: A component from `react-router-dom` that provides navigation links with active styling. It is used to create links that can highlight the current active route.
   - **`AuthContext`**: The authentication context created using `createContext` in your context store. This context provides the authentication state and dispatch functions.
   - **`logo`**: An import statement for the logo image file. This is used to display the logo in the header.

2. **Helper Function for Active Link Styling**:

   ```javascript
   const styleActiveLink = ({ isActive }) => {
     return {
       color: isActive ? "#f57145" : "",
     };
   };
   ```

   - **`styleActiveLink`**: A helper function that applies a specific style to active navigation links. If a link is active, it sets the color to `#f57145`; otherwise, it leaves the color unset.

3. **Header Component Return Statement**:

   ```javascript
     return (
       <header className="header flex-row">
         <div className="flex-row">
           <img src={logo} alt="dm-logo" className="logo" />
           <h2>Social Mountain</h2>
         </div>
         <nav>
           {state.token ? (
             <ul className="main-nav">
               <li>
                 <NavLink style={styleActiveLink} to="/">
                   Home
                 </NavLink>
               </li>
               <li>
                 <NavLink style={styleActiveLink} to="profile">
                   Profile
                 </NavLink>
               </li>
               <li>
                 <NavLink style={styleActiveLink} to="form">
                   Add Post
                 </NavLink>
               </li>
               <li>
                 <button
                   className="logout-btn"
                   onClick={() => dispatch({ type: "LOGOUT" })}
                 >
                   Logout
                 </button>
               </li>
             </ul>
           ) : (
             <ul className="main-nav">
               <li>
                 <NavLink style={styleActiveLink} to="/">
                   Home
                 </NavLink>
               </li>
               <li>
                 <NavLink style={styleActiveLink} to="/auth">
                   Login or Sign Up
                 </NavLink>
               </li>
             </ul>
           )}
         </nav>
       </header>
     );
   };

   export default Header;
   ```

### Detailed Breakdown

1. **Conditional Rendering Based on Authentication State**:

   - The component uses a conditional (`state.token ? ... : ...`) to determine which navigation links to display. This is based on whether `state.token` exists in the authentication state.
   - **`state.token` exists (User is authenticated)**:
     - **Navigation Links**:
       - `Home`: Links to the home page.
       - `Profile`: Links to the user's profile page.
       - `Add Post`: Links to a form for adding a new post.
     - **Logout Button**: A button that, when clicked, dispatches a `LOGOUT` action to the `AuthContext` to log the user out.
   - **`state.token` does not exist (User is not authenticated)**:
     - **Navigation Links**:
       - `Home`: Links to the home page.
       - `Login or Sign Up`: Links to the authentication page where users can log in or sign up.

2. **Navigation Styling**:

   - The `styleActiveLink` function is used to style active navigation links. The `NavLink` component applies this function to determine the link's style based on whether it is active.
   - This provides visual feedback to users about which page they are currently on by changing the link color when it is active.

3. **Component Structure**:
   - **`<header>`**: The main container for the header section, styled with a `flex-row` class for layout purposes.
   - **Logo and Title**:
     - **Logo**: An image element that displays the logo, with the `logo` class for styling.
     - **Title**: A heading element (`<h2>`) displaying the title "Social Mountain".
   - **Navigation (`<nav>`)**:
     - The `nav` element contains an unordered list (`<ul>`) of navigation links.
     - The links are conditionally rendered based on the user's authentication status, ensuring that only relevant links are shown to the user.

### Purpose and Functionality

1. **User Experience**:

   - By conditionally rendering navigation links based on the authentication state, the header component ensures that users only see relevant options. Authenticated users can access their profile and add new posts, while unauthenticated users are prompted to log in or sign up.
   - This improves the user experience by providing clear and relevant navigation options based on the user's current state.

2. **Security**:

   - Restricting access to certain links (like `Profile` and `Add Post`) ensures that only authenticated users can access these features. This helps prevent unauthorized access to sensitive or user-specific pages.

3. **Centralized State Management**:

   - Using `useContext` to access the authentication state allows the component to react dynamically to changes in the user's authentication status. This promotes a clean and maintainable codebase, as the authentication logic is centralized and easy to manage.

4. **Responsive Navigation**:
   - The use of `NavLink` and the `styleActiveLink` function provides a responsive navigation experience, giving users clear visual feedback about their current location within the application.

Overall, this code ensures that the `Header` component dynamically adapts to the user's authentication status, providing a seamless and secure navigation experience in the React application.

# Add JWT Authentication

## Objectives

- Students can define what a token is
- Students can define the purpose of a JWT
- Student can create JWT in the backend

## Summary

JWT is a commonly used technology for authentication. Similar to a passport for travel, a token allows you to persist your logged-in state and save some credentials for your app to use.

## Content

- JWT Basics
- Project Part 2: Setting Up Tokens with JWT

## Goals

- Create tokens in the backend
- Save the tokens to `localStorage`
- Validate the tokens in the backend

## Steps

### Create your `.env` file

At the root of your project, create a `.env` file.

Inside of the `.env` file, create a `SECRET` and set it equal to a random string of your choosing. For `.env` syntax, you do not declare using `let` or `const`, and you do not wrap the string in quotes either. Simply write the name and use an equal sign to add the value.

```
SECRET = My_Random_String
```

### Create Function for Generating Tokens

Inside of your `/server/controllers/auth.js` file, you will require `jwt` at the top of the page. You will also add the line `require('dotenv').config()` which will configure this file to use environment variables.

Now add a line that requires `SECRET` from `process.env.SECRET`. This will allow us to use the `SECRET` in our code.

Now create a function outside of the `module.exports` called `createToken`, and it will take in `username` and `id` as parameters. (Because we have not implemented a database yet, the `id` will temporarily be a password we pass in as an argument).

`createToken` will return the `jwt.sign()` method. Inside of the method, pass 3 arguments. The first argument is an object that contains both `username` and `id`. The second argument will be the `SECRET` variable. The third argument is an object that contains a key of `expiresIn` and its value is a string of `2 days`.

```javascript
require("dotenv").config();
const SECRET = process.env.SECRET;
const jwt = require("jsonwebtoken");

const createToken = (username, id) => {
  return jwt.sign(
    {
      username,
      id,
    },
    SECRET,
    {
      expiresIn: "2 days",
    }
  );
};
```

#### Sidenote/Explanation:

Let's break down the steps involved in creating a function for generating JSON Web Tokens (JWTs) in your `/server/controllers/auth.js` file, including detailed explanations for each part.

### Detailed Explanation of Creating a Function for Tokens

1. **Loading Environment Variables**:

   ```javascript
   require("dotenv").config();
   ```

   - **`dotenv`**: This package loads environment variables from a `.env` file into `process.env`.
   - **`require("dotenv").config()`**: This line configures the `dotenv` package to load the environment variables. It reads the `.env` file and adds the variables to `process.env`, making them accessible throughout your application. This is important for managing sensitive information like secret keys, database credentials, etc.

2. **Importing the JWT Library and Secret Key**:

   ```javascript
   const SECRET = process.env.SECRET;
   const jwt = require("jsonwebtoken");
   ```

   - **`SECRET`**: This variable retrieves the secret key from the environment variables (`process.env.SECRET`). The secret key is used to sign the JWT, ensuring that the token is secure and can be verified.
   - **`jsonwebtoken`**: This package is used for creating and verifying JSON Web Tokens. It provides methods for signing (creating) and verifying tokens.

3. **Creating the `createToken` Function**:
   ```javascript
   const createToken = (username, id) => {
     return jwt.sign(
       {
         username,
         id,
       },
       SECRET,
       {
         expiresIn: "2 days",
       }
     );
   };
   ```
   - **Function Definition**:
     - **`createToken`**: This function is defined to generate a JWT. It takes `username` and `id` as parameters. In a real application, `id` would be the user's ID from the database. For now, it can be any identifier, such as a password, until the database is implemented.
   - **Returning the Signed Token**:
     - **`jwt.sign`**: This method creates a new JWT.
       - **First Argument**: An object containing the payload of the token. The payload is the data that you want to include in the token. Here, it includes `username` and `id`.
       - **Second Argument**: The secret key (`SECRET`). This key is used to sign the token, ensuring that it can be verified and trusted.
       - **Third Argument**: An options object. Here, it specifies the expiration time of the token with the `expiresIn` key. In this example, the token is set to expire in "2 days".

### Purpose and Functionality

1. **Environment Variables**:

   - **Security**: Storing sensitive information like the secret key in environment variables enhances security. It keeps the secret key out of your source code and makes it easier to manage different configurations for different environments (e.g., development, testing, production).

2. **JWT Signing**:
   - **Payload**: The payload contains the data you want to include in the token. In this case, `username` and `id` are included, which can be used to identify the user.
   - **Secret Key**: The secret key is used to sign the token, ensuring its integrity and authenticity. Only the server with the same secret key can verify the token.
   - **Expiration**: The `expiresIn` option sets an expiration time for the token. This is important for security because it limits the validity period of the token. After expiration, the token can no longer be used, and the user will need to log in again to get a new token.

### Example Usage in Authentication Flow

1. **User Login**:

   - When a user logs in successfully, the server generates a JWT using the `createToken` function and sends it back to the client.
   - The client stores the token (typically in local storage or cookies) and includes it in subsequent requests to access protected resources.

2. **Protected Routes**:
   - For routes that require authentication, the server verifies the token included in the client's request headers.
   - If the token is valid, the server allows access to the protected resource. If the token is invalid or expired, the server denies access.

### Full Code Example

Here's how you might use the `createToken` function in a complete `auth.js` file:

```javascript
// Load environment variables
require("dotenv").config();
const SECRET = process.env.SECRET;
const jwt = require("jsonwebtoken");

// Function to create a JWT
const createToken = (username, id) => {
  return jwt.sign(
    {
      username,
      id,
    },
    SECRET,
    {
      expiresIn: "2 days",
    }
  );
};

// Example of using the createToken function in a login handler
module.exports = {
  login: async (req, res) => {
    const { username, password } = req.body;

    // Example validation (replace with actual validation logic)
    if (username === "user" && password === "pass") {
      // Create token
      const token = createToken(username, password);

      // Send token to client
      res.json({ token });
    } else {
      res.status(401).json({ error: "Invalid credentials" });
    }
  },
  register: async (req, res) => {
    // Registration logic (e.g., save user to database)
    res.sendStatus(200);
  },
};
```

### Summary

- **Environment Variables**: Securely manage sensitive information like the secret key.
- **JWT Signing**: Create tokens with a payload, secret key, and expiration time.
- **Authentication Flow**: Use tokens to authenticate users and protect routes.

By following this approach, you can implement a secure authentication system using JWTs in your application.

### Generate Token

Inside of `server/controllers/auth.js`, we will code inside of the `login` function. Destructure `username` and `password` from `req.body`. Now create a variable called `token`, and set it equal to `createToken` invoked, passing in `username` and `password` as arguments.

Now alter your `res.sendStatus` to become `res.status(200).send(token)`. This allows us to declare a status code as well as send back information to the front end.

```javascript
login: async (req, res) => {
  let { username, password } = req.body;
  const token = createToken(username, password);
  res.status(200).send(token);
};
```

#### Sidenote/Explanation:

Let's break down the provided code snippet and explain each part in detail.

### Detailed Breakdown of the Code

1. **Function Definition and Parameters**:

   ```javascript
   login: async (req, res) => {
   ```

   - **`login`**: This is the name of the function. It's intended to handle user login requests.
   - **`async`**: This keyword indicates that the function is asynchronous, meaning it can perform asynchronous operations using `await`.
   - **`req`**: This is the request object, which contains information about the HTTP request, including any data sent by the client.
   - **`res`**: This is the response object, which is used to send a response back to the client.

2. **Destructuring `username` and `password` from `req.body`**:

   ```javascript
   let { username, password } = req.body;
   ```

   - **Destructuring Assignment**: This syntax allows you to extract properties from objects and assign them to variables. Here, `username` and `password` are extracted from `req.body`.
   - **`req.body`**: This contains the data sent by the client in the body of the request. In a login request, this would typically include the username and password entered by the user.

3. **Creating a Token**:

   ```javascript
   const token = createToken(username, password);
   ```

   - **`createToken`**: This is a function that generates a JSON Web Token (JWT). It is assumed to be defined elsewhere in the code.
   - **Invocation**: The `createToken` function is called with `username` and `password` as arguments.
   - **Token Creation**: The function generates a JWT that includes the `username` and `password` in its payload and signs it with a secret key. The generated token is stored in the `token` variable.

4. **Sending the Token in the Response**:
   ```javascript
   res.status(200).send(token);
   ```
   - **`res.status(200)`**: This sets the HTTP status code of the response to 200, which means "OK". It indicates that the request was successful.
   - **`.send(token)`**: This sends the token as the response body. The client will receive the token as part of the response, which can then be used for authentication in subsequent requests.

### Purpose and Functionality

1. **Handling Login Requests**:

   - This function handles login requests by processing the provided `username` and `password`. It assumes that the credentials are correct and generates a JWT for the user.

2. **Token Generation**:

   - The generated token includes the user's `username` and `password` in its payload and is signed with a secret key. This token can be used to authenticate the user in future requests.

3. **Sending the Token to the Client**:
   - By sending the token in the response, the server provides the client with a token that can be stored (typically in local storage or cookies) and used for authenticating subsequent requests to protected routes.

### Full Code Example in Context

Here's an example of how this `login` function might fit into a complete `auth.js` controller file, including the `createToken` function:

```javascript
// Load environment variables
require("dotenv").config();
const SECRET = process.env.SECRET;
const jwt = require("jsonwebtoken");

// Function to create a JWT
const createToken = (username, id) => {
  return jwt.sign(
    {
      username,
      id,
    },
    SECRET,
    {
      expiresIn: "2 days",
    }
  );
};

// Login function
module.exports = {
  login: async (req, res) => {
    let { username, password } = req.body;

    // Example validation (replace with actual validation logic)
    if (username === "user" && password === "pass") {
      // Create token
      const token = createToken(username, password);

      // Send token to client
      res.status(200).send(token);
    } else {
      res.status(401).json({ error: "Invalid credentials" });
    }
  },
  register: async (req, res) => {
    // Registration logic (e.g., save user to database)
    res.sendStatus(200);
  },
};
```

### Summary

- **Destructuring**: Extracts `username` and `password` from `req.body`.
- **Token Creation**: Uses the `createToken` function to generate a JWT with the `username` and `password`.
- **Sending Response**: Sends the generated token back to the client with a 200 status code.

This setup allows the server to handle login requests, generate a JWT for authenticated users, and send the token back to the client for use in subsequent authenticated requests.

### Test with Postman

Open up your Postman Application (must be the downloaded one, cannot be the website), and create a new request. This will need to be a POST request to your server, endpoint `/login` (URL is `http://localhost:PORT_NUMBER_FOR_YOUR_SERVER`).

Add a body to the request by clicking on the body tab around the middle of the page. Then click raw, then change the option from text to json. Create a JSON object with `username` and `password` inside of it. You can make up the values, so long as they are a string.

Hit the send button. If we have coded everything correctly, we should see a token appear in our Postman application 🥳

```json
{
  "username": "devmountain",
  "password": "webdev123$$"
}
```

### Create file for Validating Token (Middleware)

We will set up a middleware function that will run on every request that requires a user to be authenticated to run. This middleware function makes use of the token the user will have. If they don’t pass this middleware, then they won’t be able to make the request.

In `server/middleware` folder, create a file called `isAuthenticated.js`.

Copy and paste the code below into your file.

Read through the code and write at least 5 comments explaining different parts of the code. Break it down piece by piece, and even pull in a peer or your tech lead to rubber duck.

```javascript
require("dotenv").config();
const jwt = require("jsonwebtoken");
const { SECRET } = process.env;

module.exports = {
  isAuthenticated: (req, res, next) => {
    const headerToken = req.get("Authorization");

    if (!headerToken) {
      console.log("ERROR IN auth middleware");
      res.sendStatus(401);
    }

    let token;

    try {
      token = jwt.verify(headerToken, SECRET);
    } catch (err) {
      err.statusCode = 500;
      throw err;
    }

    if (!token) {
      const error = new Error("Not authenticated.");
      error.statusCode = 401;
      throw error;
    }

    next();
  },
};
```

### Attach Middleware to Endpoints

Inside `server/index.js`, locate your post, put, and delete endpoints for `/posts`. These are sensitive and delicate endpoints that we need to ensure a user is indeed authenticated before we run any functions, so we will add our `isAuthenticated` function in the middle of the endpoint, and the corresponding function.

```javascript
app.post("/posts", isAuthenticated, addPost);
app.put("/posts/:id", isAuthenticated, editPost);
app.delete("/posts/:id", isAuthenticated, deletePost);
```

### Test with Postman

Certainly! Here's how you can format the testing instructions for Postman as a markdown document:

---

# Testing with Postman

## Step 1: Test Unauthorized Access

### Making a POST request to `/posts`

1. **Open Postman**.
2. **Create a new POST request**.
3. **Set the URL to**: `http://localhost:<PORT>/posts` (replace `<PORT>` with your server's port number).
4. **Send the request**.
5. **Expected Response**:
   - Status: `401 Unauthorized`
   - Body: `Unauthorized`

## Step 2: Get a Valid Token

### Making a POST request to `/login`

1. **Create a new POST request**.
2. **Set the URL to**: `http://localhost:<PORT>/login` (replace `<PORT>` with your server's port number).
3. **Set the Body** to `raw` and select `JSON` format.
4. **Add the following JSON to the body**:
   ```json
   {
     "username": "user",
     "password": "pass"
   }
   ```
5. **Send the request**.
6. **Expected Response**:
   - Status: `200 OK`
   - Body: `{ "token": "<YOUR_TOKEN>" }` (copy the token from the response)

## Step 3: Test Authorized Access

### Making a POST request to `/posts` with a valid token

1. **Go back to the POST request for `/posts`**.
2. **Go to the Headers tab** (right next to the Body tab).
3. **Add a new header**:
   - **Key**: `Authorization`
   - **Value**: `Bearer <YOUR_TOKEN>` (replace `<YOUR_TOKEN>` with the token you copied from the login response)
4. **Send the request**.
5. **Expected Response**:
   - Status: `200 OK`
   - Body: `OK`

---

Using Sequelize

## Objectives

- Student can explain a relational database
- Student can list some advantages and disadvantages of relational vs non-relational databases
- Student can create database tables
- Student can add data to tables
- Student can modify tables
- Student can select data from a table that meets certain conditions
- Student can describe and use aggregate functions
- Student can select data from multiple tables using JOIN statements

## Summary

Sequelize not only provides a way for us to connect with databases, it’s also a fully functional Object Relational Mapper (ORM). It allows us to use JavaScript to interact with our databases. In these videos, you’ll review SQL concepts and learn about many of the helpful methods that Sequelize offers us.

## Content

- SQL Refresher
- Understanding Sequelize as an ORM
- Setting up Local PostgreSQL Databases
- Download Postgres & PGAdmin
- Project Part 3: Creating a Database

## Goals

- Set up a local PostgreSQL Database
- Create 2 Sequelize Models
- Use Sequelize to sync and generate the tables
- View the tables in PGAdmin

## Steps

### Create new PGAdmin Database

We will be using PGAdmin to create and host our local database. If you have not watched the video on setting up PGAdmin, please do so now.

Inside of your PGAdmin, create a new database for your Unit 4 project called `social_mountain`.

Create the URI String. If you followed the instructions in the video, your URI string should look like this: `postgresql://postgres:admin@localhost:5432/social_mountain` (If you altered your username and password while setting up PGAdmin, then change `postgres` to your username, and `admin` to your password).

Place your URI String inside of your `.env` file and call it `CONNECTION_STRING`.

### Setup Sequelize Connection

In your `/server/util` folder, create a file called `database.js` - this is where we’ll connect to the database with Sequelize.

Import and configure `dotenv` at the top of the file.

Additionally, import the `CONNECTION_STRING` from your `.env` and the `Sequelize` class, which is the default export from the package.

Create a new instance of the Sequelize class, passing in the database connection string and a configuration object. You can call the

instance `sequelize` with a lowercase “s”.

The configuration object should have a `dialect` property whose value is “postgres”.

Don’t forget to export `sequelize`.

TIP: If you were to connect to an external DB (Heroku, AWS, Cockroach Labs, etc.) you would need to include the following. Under your `dialectOptions`, add an additional property called `dialectOptions` whose value is an object. That object should contain a property called `ssl` whose value is also an object. The innermost object should have a `rejectUnauthorized` property whose value is false. This is required for nearly all external databases. Remember to come back here when you want to connect to one and host your capstone 😉

```javascript
require("dotenv").config();
const { CONNECTION_STRING } = process.env;
const Sequelize = require("sequelize");

const sequelize = new Sequelize(CONNECTION_STRING, {
  dialect: "postgres",
});

module.exports = {
  sequelize,
};
```

### Create a User Model

In your `server/models` folder, create a `user.js` file.

The `user.js` file is where you’ll define what your user objects should look like. Because we’re using Sequelize, this is how we’ll be defining our tables. Sequelize will take our models and set up the database for us.

In `user.js`, import `DataTypes` from `sequelize`.

Import your Sequelize connection, `sequelize`, from the `util/database` file.

Set up a `module.exports` object with one property: `User`. In the value of this property, we will call a function from Sequelize to set up what the user objects should look like.

The value of `User` should be set to `sequelize.define` passing in the string “user”, which is the name of the table, and an object with three properties: `id`, `username`, and `hashedPass`.

The value of `id` should be a configuration object with `type`, `autoIncrement`, `allowNull`, and `primaryKey` properties. The value of `type` should be `DataTypes.INTEGER` and the other three should be boolean values. Determine those values based on what you know about ids in databases.

The `username` and `hashedPass` properties should both be strings. Don’t forget to use the Sequelize `DataTypes` to define those.

```javascript
const { DataTypes } = require("sequelize");

const { sequelize } = require("../util/database");

module.exports = {
  User: sequelize.define("user", {
    id: {
      type: DataTypes.INTEGER,
      autoIncrement: true,
      allowNull: false,
      primaryKey: true,
    },
    username: DataTypes.STRING,
    hashedPass: DataTypes.STRING,
  }),
};
```

### Create a Post Model

Using your User model as a guide, create a Post model in your `post.js` file. Make sure to include the following properties on your object:

- `id`
- `title`
- `content`
- `privateStatus`

```javascript
const { DataTypes } = require("sequelize");

const { sequelize } = require("../util/database");

module.exports = {
  Post: sequelize.define("post", {
    id: {
      type: DataTypes.INTEGER,
      autoIncrement: true,
      allowNull: false,
      primaryKey: true,
    },
    title: DataTypes.STRING,
    content: DataTypes.TEXT,
    privateStatus: DataTypes.BOOLEAN,
  }),
};
```

### Connect to the Database

Now that we have the outline for the database, we want to actually have our server connect to it when the server starts up. We’ll also set up the relationship between our User and Post models in this step.

In `index.js` in your server, import `sequelize` from `util/database` and each of your models from their respective files.

Somewhere above your endpoints and below the imports, let’s set up the relationships for `User` and `Post`. In our application, users can post as much as they would like and each post only has one author. Using Sequelize, we can define those relationships with the `.hasMany` and `.belongsTo` methods.

Now, at the bottom of your file, we’ll use the `.sync` method to connect to our database. Call `sequelize.sync`, which is an asynchronous function, so you’ll want to follow that up with a `.then`. Pass the `.then` a callback function and move your `app.listen` line inside that callback. This will make it so when you run your file with `nodemon`, it will sync up with the database before the server starts up.

You can test this by running `nodemon` and then opening up SQL Tabs, Postico, or a similar app and connecting to your database. You can then view what tables are available - there won’t be any data yet though.

```javascript
const {sequelize} = require('./util/database')
const {User} = require('./models/user')
const {Post} = require('./models/post')

...

User.hasMany(Post)
Post.belongsTo(User)

...

// the force: true is for development -- it DROPS tables!!!
// you can use it if you like while you are building.
// sequelize.sync({ force: true })
sequelize.sync()
.then(() => {
   app.listen(PORT, () => console.log(`db sync successful & server running on port ${PORT}`))
})
.catch(err => console.log(err))
```

### Register

Right now, our authentication functions are just basic endpoints that don’t really do much. We are going to change these functions to use JSON web tokens and Sequelize methods to authenticate users.

In `controllers/auth.js`, import the `User` model and the `bcryptjs` package.

In the `register` function, we are going to check to see if a user already exists with the username being sent. If they do, we’ll send a message that we can’t create the user. If there isn’t anyone with that name yet, then we’ll store the user in our database, create a token for them, and send the username, their id, their token, and its expiration back to the front end.

Now in your `register` function, let’s delete the console.log and `res.sendStatus` and replace it with a `try catch`.

Before we move on with the functionality, add a `console.error(error)` to the `catch` block so that you can catch errors.

We’re going to use the `async/await` keywords in these functions, go ahead and add the `async` keyword now to the beginning of your function definition if you did not already. This will allow us to perform asynchronous actions in the function using the `await` keyword.

In the `try` block, destructure `username` and `password` off of `req.body` - this will make them easier to access for the rest of the function.

Then create a variable called `foundUser` that’s set equal to `await User.findOne({where: {username: username}})` which is using the asynchronous `findOne` method that’s built into our Sequelize `User` model. We then are passing it an object that adds a WHERE clause to our query and looks for usernames matching the one coming from `req.body`.

Next, write an `if/else` that checks if `foundUser` is true. If it is, that means we already have a user with that name in the database, so we’ll want to send a 400 error and a message back to the front.

If it isn’t true, then we’ll do all the work of making a user! First, create a salt and a hashed password using methods from `bcrypt`:

```javascript
const salt = bcrypt.genSaltSync(10);
const hash = bcrypt.hashSync(password, salt);
```

Next, create a new user using the `.create` method on our `User` model. The `create` method is asynchronous and expects an object with the properties defined on the model. So, create a variable called `newUser` that is equal to `await User.create({username: username, hashedPass: hash})`.

Then, make a variable called `token` that is equal to the invocation of the `createToken` method, passing in `newUser.dataValues.username` and `newUser.dataValues.id`. You can see the `dataValues` by `console.logging newUser`.

We’ll also need to make our own expiration time since the `JWT` sign method only returns the actual token. You can do that with this line:

```javascript
const exp = Date.now() + 1000 * 60 * 60 * 48;
```

This uses the JavaScript `Date` object and adds a number of milliseconds to it to equal two days, which is the expiry we assigned to the token earlier.

Finally, we can send an object to the front end using `res.status(200).send(OBJECT)`. The object should have four properties: `username` whose value should be `newUser.dataValues.username`, `userId` whose value should be `newUser.dataValues.id`, `token` whose value should be the `token` variable you created, and `exp` whose value should be the `exp` variable you created.

The `register` function is complete! Go ahead and test it with Postman, similar to how we tested the login function in a previous project part.

### Login

Set up the skeleton of your `login` function similarly to how we set up `register`. Make it `async`, add a `try catch`, log something to the console in the `catch` block, destructure `username` and `password`, create a `foundUser` variable, and an `if/else` that checks if `foundUser` is truthy.

This time though, since we are trying to log someone in, all the functionality will go in the `

if` portion. First, we’ll check to see if the username and password match what’s stored in the database. We can do that with this line:

```javascript
const isAuthenticated = bcrypt.compareSync(password, foundUser.hashedPass);
```

Now we’ll need an inner `if/else` that checks if `isAuthenticated` is truthy.

If it is, create a `token` and `exp` variables like we did in `register` and then send an object on the response with the same properties as in `register`.

In both the inner `else` block, send a message that says `Password is incorrect`.

In the outer `else` block, send a message that says `User does not exist`.

Our `login` function is done! Test your login using Postman! (Make sure you have created a user first before “logging in”).

```javascript
login: async (req, res) => {
   try {
   let { username, password } = req.body;
   let foundUser = await User.findOne({ where: { username: username } });
   if (foundUser) {
      const isAuthenticated = bcrypt.compareSync(
      password,
      foundUser.hashedPass
      );
      if (isAuthenticated) {
      let token = createToken(
            foundUser.dataValues.username,
            foundUser.dataValues.id
      );
      const exp = Date.now() + 1000 * 60 * 60 * 48;
      const data = {
            username: foundUser.dataValues.username,
            userId: foundUser.dataValues.id,
            token: token,
            exp: exp,
      };
      res.status(200).send(data);
      } else {
      res.status(400).send("Password is incorrect");
      }
   } else {
      res.status(400).send("User does not exist.");
   }
   } catch (error) {
   console.error(error);
   res.status(400).send(error);
   }
},
```

# REST

## Objectives

- Student can define RESTful in the context of APIs
- Student can know what CRUD stands for
- Student knows the four primary HTTP methods
- Student can explain middleware
- Student can build a server that listens for requests
- Student can create endpoints that listen for the four main HTTP methods

## Summary

In these videos, you’ll learn more about what makes an API RESTful and how to build one.

## Content

- Working with REST APIs - The Basics
- Working with REST APIs - The Practical Application
- Project Part 4: Building Out Endpoint Methods

## Goals

- Connect Front-end code with Back-end code
- Create Posts
- Get Posts
- Alter Post Privacy

## Steps

### Connect our Login Form

### Add a Post

### Getting Posts

### Edit a Post

### Delete a Post

## OPTIONAL Challenge - Notifications

### Goals

- Set up a notification for users on unsuccessful register or login

### Steps

#### Create a Notification

In `Auth.js`, set up a notification that will run when the axios request catches an error. You can add text to the page, use the `alert()` function, create your own modal, or use a package from npm.

## Solution

You can download the solution for this project here:

/Users/ryansmith/Library/Mobile Documents/com~apple~CloudDocs/Dev/DevMountain/Specializations12/Specs-Unit4/react-proj-4-solution.zip
````
