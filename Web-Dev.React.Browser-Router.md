---
id: rrr4z0ovxpu68n4ylg071zw
title: Browser-Router
desc: ""
updated: 1721349639907
created: 1721349574333
---

Setting up BrowserRouter in a React application involves installing the necessary packages and configuring your routes. Here are the steps to set it up:

### Step 1: Install React Router

First, you need to install `react-router-dom`, which is the package that includes BrowserRouter.

```bash
npm install react-router-dom
```

### Step 2: Import BrowserRouter

In your main application file (usually `index.js` or `App.js`), you need to import `BrowserRouter` from `react-router-dom` and wrap your application with it.

```jsx
// index.js or App.js
import React from "react";
import ReactDOM from "react-dom";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById("root")
);
```

### Step 3: Define Your Routes

In your `App.js` file (or another component), you will define your routes using `Route` and `Switch` components from `react-router-dom`.

```jsx
// App.js
import React from "react";
import { Switch, Route } from "react-router-dom";
import Home from "./components/Home";
import About from "./components/About";
import Contact from "./components/Contact";

function App() {
  return (
    <div>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
        <Route path="/contact" component={Contact} />
      </Switch>
    </div>
  );
}

export default App;
```

### Step 4: Create Your Components

Create the components you referenced in your routes (e.g., `Home`, `About`, `Contact`).

```jsx
// components/Home.js
import React from 'react';

function Home() {
  return <h1>Home Page</h1>;
}

export default Home;

// components/About.js
import React from 'react';

function About() {
  return <h1>About Page</h1>;
}

export default About;

// components/Contact.js
import React from 'react';

function Contact() {
  return <h1>Contact Page</h1>;
}

export default Contact;
```

### Step 5: Add Navigation Links (Optional)

You can add navigation links to navigate between different routes.

```jsx
// App.js
import React from "react";
import { Switch, Route, Link } from "react-router-dom";
import Home from "./components/Home";
import About from "./components/About";
import Contact from "./components/Contact";

function App() {
  return (
    <div>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/contact">Contact</Link>
          </li>
        </ul>
      </nav>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
        <Route path="/contact" component={Contact} />
      </Switch>
    </div>
  );
}

export default App;
```

### Step 6: Test Your Application

Run your application to ensure the routes work correctly.

```bash
npm start
```

Navigate to different routes using the links or directly in the browser's address bar to verify that each component renders correctly.

These steps will set up a basic routing system in your React application using `BrowserRouter` from `react-router-dom`.
