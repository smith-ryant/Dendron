---
id: g23qtj0xkqqh8nsbznqk2dq
title: Framework
desc: ""
updated: 1718832698781
created: 1718832662061
---

React itself is not a framework but a JavaScript library for building user interfaces. However, when people refer to the "React framework," they usually mean the ecosystem of tools and libraries that work together with React to build complete web applications. This ecosystem can be considered a framework in a broader sense because it provides a structured way to develop applications. Here's an overview of what this includes:

### Core Concepts of the React Ecosystem

1. **React Library**

   - **React**: The core library used to create and manage the UI components of an application.

2. **React Router**

   - **React Router**: A library for managing navigation and routing in React applications. It allows you to define multiple routes in your application and handle dynamic URL parameters, nested routes, and more.

     ```bash
     npm install react-router-dom
     ```

     Example usage:

     ```jsx
     import { BrowserRouter as Router, Route, Switch } from "react-router-dom";

     function App() {
       return (
         <Router>
           <Switch>
             <Route path="/home" component={Home} />
             <Route path="/about" component={About} />
           </Switch>
         </Router>
       );
     }
     ```

3. **State Management**

   - **Redux**: A popular state management library for managing the state of the entire application in a predictable way.

     ```bash
     npm install redux react-redux
     ```

     Example usage:

     ```jsx
     import { createStore } from "redux";
     import { Provider } from "react-redux";
     import rootReducer from "./reducers";

     const store = createStore(rootReducer);

     function App() {
       return (
         <Provider store={store}>
           <YourMainComponent />
         </Provider>
       );
     }
     ```

   - **Context API**: A built-in feature in React for managing state that can be shared across components without passing props manually at every level.

     ```jsx
     const MyContext = React.createContext();

     function App() {
       const [state, setState] = useState(initialState);

       return (
         <MyContext.Provider value={{ state, setState }}>
           <YourMainComponent />
         </MyContext.Provider>
       );
     }
     ```

4. **Side Effects**

   - **Redux Saga/Redux Thunk**: Middleware libraries for handling side effects in Redux.
     ```bash
     npm install redux-saga redux-thunk
     ```
   - **React Query**: A library for fetching, caching, and updating data in React applications.
     ```bash
     npm install react-query
     ```

5. **Styling**

   - **CSS-in-JS**: Libraries like styled-components and emotion allow you to write CSS directly in your JavaScript files.

     ```bash
     npm install styled-components
     ```

     Example usage:

     ```jsx
     import styled from "styled-components";

     const Button = styled.button`
       background-color: blue;
       color: white;
     `;

     function App() {
       return <Button>Click me</Button>;
     }
     ```

6. **Build Tools and Bundlers**

   - **Create React App**: A tool to set up a new React project with a standard structure and configuration.
     ```bash
     npx create-react-app my-app
     ```
   - **Webpack**: A module bundler for JavaScript applications.
   - **Babel**: A JavaScript compiler that transforms modern JavaScript into a format compatible with older browsers.

7. **Server-Side Rendering (SSR)**

   - **Next.js**: A React framework for server-side rendering, static site generation, and API routes.
     ```bash
     npx create-next-app
     ```
     Example usage:
     ```jsx
     // pages/index.js
     export default function Home() {
       return <h1>Hello, Next.js!</h1>;
     }
     ```

8. **TypeScript**
   - **TypeScript**: A strongly typed programming language that builds on JavaScript, often used with React to add static types.
     ```bash
     npx create-react-app my-app --template typescript
     ```

### Conclusion

While React itself is a library focused on building UI components, the broader React ecosystem provides a full set of tools and libraries to manage state, handle routing, perform side effects, and style components, essentially acting as a framework for building complex, large-scale applications. The combination of these tools offers a structured and efficient way to develop modern web applications.
