---
id: wywy3qzf8354wp07bzntdj7
title: Rest_Operator
desc: ""
updated: 1722187588189
created: 1722187289485
---

In React, the "rest property" (also known as the "rest operator") is a feature introduced in ECMAScript 2015 (ES6) that allows you to collect the remaining properties of an object after some have been destructured. It is particularly useful for handling props in React components.

Here's how it works:

### Destructuring with the Rest Property

When you destructure an object, you can use the rest property to collect all remaining properties into a new object. This is helpful when you want to separate some specific props from the rest.

#### Example:

```javascript
const person = {
  name: "John",
  age: 30,
  city: "New York",
  country: "USA",
};

const { name, age, ...rest } = person;

console.log(name); // 'John'
console.log(age); // 30
console.log(rest); // { city: 'New York', country: 'USA' }
```

In this example, `name` and `age` are extracted, and the rest of the properties (`city` and `country`) are collected into the `rest` object.

### Using Rest Property in React Components

In React, the rest property is often used to handle component props, especially when you want to pass down some props to child components without explicitly specifying each one.

#### Example:

```javascript
import React from "react";

const MyComponent = ({ title, ...otherProps }) => {
  return (
    <div>
      <h1>{title}</h1>
      <AnotherComponent {...otherProps} />
    </div>
  );
};

const AnotherComponent = (props) => {
  return (
    <div>
      <p>{props.description}</p>
      <p>{props.extraInfo}</p>
    </div>
  );
};

// Usage
<MyComponent
  title="Hello"
  description="This is a description."
  extraInfo="Some extra info."
/>;
```

In this example:

- `MyComponent` receives `title`, `description`, and `extraInfo` as props.
- It destructures `title` and collects the remaining props (`description` and `extraInfo`) into `otherProps`.
- The `otherProps` object is then spread into `AnotherComponent`, which receives `description` and `extraInfo`.

### Benefits

1. **Clean Code**: It makes your code cleaner and avoids redundancy when passing multiple props.
2. **Flexibility**: Easily pass down props to child components without explicitly listing each one.
3. **Maintainability**: If new props are added to the parent component, they can automatically be passed down to the child component without modifying the code.

The rest property is a powerful feature that helps you manage and pass props efficiently in your React applications.
