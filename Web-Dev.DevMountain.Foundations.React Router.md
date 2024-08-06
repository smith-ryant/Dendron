---
id: yvepwar46uet4dqhimkfh2m
title: React Router
desc: ""
updated: 1722790837709
created: 1722790811867
---

Here's the webpage content formatted in Markdown:

---

# On this Page

- [React Router](#react-router)
  - [What is React Router?](#what-is-react-router)
  - [Routes and createBrowserRouter](#routes-and-createbrowserrouter)
  - [The Route Component](#the-route-component)
  - [Nested Routes](#nested-routes)
  - [Setting Up the Router](#setting-up-the-router)
  - [Alternative Router Setup](#alternative-router-setup)
  - [RouterProvider](#routerprovider)
  - [Index Routes](#index-routes)
  - [Navigation with React Router](#navigation-with-react-router)
  - [Link](#link)
  - [Links in the Root Component](#links-in-the-root-component)
  - [Outlet](#outlet)
  - [Loading Data](#loading-data)
  - [useLoaderData](#useloaderdata)

---

## React Router

React Router is a library that enables client-side routing. It allows you to add pages and links to a single-page React app.

To download the demo code for this lecture, run the following:

```bash
dmget wb-react-router --demo
```

Then, `cd` into the project directory and use npm to install and run the dev server:

```bash
npm install
npm run dev
```

## What is React Router?

In traditional websites, the browser requests an HTML document from a web server, then renders that HTML. When the user clicks a link, it starts the process all over again for a new page.

React Router allows your app to update the URL (for example, when the user clicks a link) without making another request for another HTML document. This can enable faster user experiences. The browser doesn’t need to request an entirely new HTML file; it can just render different React components based on the URL.

## Routes and createBrowserRouter

## The Route Component

The `Route` component allows you to specify which React component should be displayed for a certain URL.

```jsx
<Route path="/about" element={<About />} />
```

Here we’re telling the UI to display the `<About />` component when the URL in our browser ends with 'about'.

### Path Matching in Previous Versions

In previous versions of React Router, the path didn’t match the route exactly. So you would often need to use the `exact` prop or a `<Switch>` component to differentiate between paths if one was a sub-path of another. This is no longer necessary.

## Nested Routes

It’s common to have a root component that contains the global layout for the site. We can set up a root route for that component and nest all the other routes inside of it.

```jsx
<Route path="/" element={<App />}>
  <Route path="/about" element={<About />} />
  <Route path="/users/:id" element={<UserProfile />} />
</Route>
```

## Setting Up the Router

Finally, we can use `createBrowserRouter` and `createRoutesFromElements` to set up our router.

```jsx
import {
  Route,
  createBrowserRouter,
  createRoutesFromElements,
} from "react-router-dom";

const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path="/" element={<App />}>
      <Route path="/about" element={<About />} />
      <Route path="/users/:id" element={<UserProfile />} />
    </Route>
  )
);
```

## Alternative Router Setup

Alternatively, we can use `createBrowserRouter` without `createRoutesFromElements`. In this case, we’ll need to use objects instead of `<Route>` components.

```jsx
const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
    children: [
      {
        path: "/about",
        element: <About />,
      },
      {
        path: "/users/:id",
        element: <UserProfile />,
      },
    ],
  },
]);
```

**Is one setup better?**

There’s no difference between defining routes with an object and defining them with React elements. It’s a matter of personal preference.

## RouterProvider

Finally, we’ll need to pass the router into a `<RouterProvider>` inside `ReactDOM.createRoot()`:

**src/main.jsx**

```jsx
import { RouterProvider } from "react-router-dom";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

Now, if you enter one of the path URLs into the browser, you should see the appropriate React component.

## Index Routes

In our current setup, there is nothing on the home page except the nav links. If we add content to the root component, it won’t just show up on the home page — it’ll show up on every page.

For content that ONLY shows up on the homepage, we can use an index route. An index route is like a “default child route.” Its URL path will always be the same as its parent.

**src/main.jsx**

```jsx
const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path="/" element={<App />}>
      <Route index element={<Home />} />
      <Route path="/about" element={<About />} />
      <Route path="/users/:id" element={<UserProfile />} />
    </Route>
  )
);
```

## Navigation with React Router

## Link

We can navigate to different routes inside of our application by using the `Link` component:

```jsx
<Link to="/about">About</Link>
```

This works very similarly to an `<a>` tag. The text for the link goes in between the tags.

**Link vs NavLink**

React Router also has a `NavLink` component, which is almost the same as `Link` except that it supports additional styling. For example, you can use `NavLink` to style the active link differently from the other links.

## Links in the Root Component

Let’s put all our nav links in the root component so they show up on every page:

**src/App.jsx**

```jsx
import { Link } from "react-router-dom";

export default function App() {
  return (
    <>
      <ul>
        <li>
          <Link to="/">Home</Link>
        </li>
        <li>
          <Link to="/about">About</Link>
        </li>
        <li>
          <Link to="/users/1">User 1</Link>
        </li>
        <li>
          <Link to="/users/2">User 2</Link>
        </li>
      </ul>
      <Outlet />
    </>
  );
}
```

## Outlet

We also need to put an `<Outlet>` in our root component. When we go to one of our routes, the `<Outlet>` tells React Router where on the page to render the component for that route.

**src/App.jsx**

```jsx
import { Outlet, Link } from "react-router-dom";

export default function App() {
  return (
    <>
      <ul>
        <li>
          <Link to="/">Home</Link>
        </li>
        <li>
          <Link to="/about">About</Link>
        </li>
        <li>
          <Link to="/users/1">User 1</Link>
        </li>
        <li>
          <Link to="/users/2">User 2</Link>
        </li>
      </ul>
      <Outlet />
    </>
  );
}
```

## Loading Data

## Loading Data

Previously, we used the `useEffect` hook to initially load data into a React component. Instead of doing that, we can define a loader function in React Router that will run whenever the component loads.

**src/App.jsx**

```jsx
<Route
  path="/users/:id"
  element={<UserProfile />}
  loader={(request) => {
    return users[request.params.id];
  }}
/>
```

The loader function takes the request as a parameter. We can also use destructuring to just get the parts of the request we want (in this case, the URL params):

```jsx
<Route
  path="/users/:id"
  element={<UserProfile />}
  loader={({ params }) => {
    return users[params.id];
  }}
/>
```

## useLoaderData

To access this data in the component, use `useLoaderData`:

**src/Components.jsx**

```jsx
import { useLoaderData } from "react-router-dom";

export function UserProfile() {
  const { name, hobby, funFact } = useLoaderData();
  return (
    <div>
      <h2>Name: {name}</h2>
      <h3>Hobby: {hobby}</h3>
      <h3>Fun Fact: {funFact}</h3>
    </div>
  );
}
```

---
