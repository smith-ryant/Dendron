---
id: j0m864bnkchw19b6qkn97xq
title: Refs
desc: ""
updated: 1718832761136
created: 1718832739661
---

In React, a **ref** (short for reference) is a way to access and interact with DOM elements or React components directly. Refs provide a way to access the underlying DOM node directly or to hold a reference to a class component instance, allowing you to perform imperative actions like modifying the DOM or interacting with the component's methods.

### Creating Refs

Refs are created using the `React.createRef()` method and can be attached to React elements via the `ref` attribute. Here's a basic example of how to use refs:

#### Example with Class Components

```javascript
import React, { Component } from "react";

class MyComponent extends Component {
  constructor(props) {
    super(props);
    // Create a ref using React.createRef()
    this.myRef = React.createRef();
  }

  componentDidMount() {
    // Access the DOM element via the ref
    this.myRef.current.focus();
  }

  render() {
    return <input type="text" ref={this.myRef} />;
  }
}

export default MyComponent;
```

#### Example with Functional Components (using `useRef`)

In functional components, the `useRef` hook is used to create refs:

```javascript
import React, { useRef, useEffect } from "react";

const MyComponent = () => {
  // Create a ref using the useRef hook
  const myRef = useRef(null);

  useEffect(() => {
    // Access the DOM element via the ref
    myRef.current.focus();
  }, []);

  return <input type="text" ref={myRef} />;
};

export default MyComponent;
```

### Use Cases for Refs

1. **Accessing DOM elements**: You can use refs to directly access a DOM element and perform operations such as focus, measure, or modify the element.

2. **Managing focus, text selection, or media playback**: Refs are helpful for managing focus, text selection, or playing media in a controlled way.

3. **Triggering animations**: Refs can be used to trigger animations on a component.

4. **Integrating with third-party libraries**: Refs allow you to integrate React with non-React libraries that require direct access to the DOM.

5. **Holding a reference to a class component instance**: Although less common in modern React applications (which often use functional components), refs can still hold references to class component instances to call methods directly on the component.

### Important Points

- **Refs are not for managing state**: Refs should not be used as a substitute for state management. They do not trigger re-renders when updated.
- **Avoid overusing refs**: Relying too much on refs can make your code less declarative and harder to maintain. Use refs sparingly and prefer state and props for most interactions.

Refs provide a powerful way to interact with the DOM and components directly in React, allowing for more granular control when needed.
