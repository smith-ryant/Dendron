---
id: en1x21ait1b6exrxjcbmwql
title: Testing React
desc: ""
updated: 1722791480683
created: 1722791463380
---

Here is the webpage content converted into Markdown:

---

# On this Page

- [Testing React](#testing-react)
  - [Testing React Components](#testing-react-components)
    - [Unit Tests for React Components](#unit-tests-for-react-components)
    - [Vitest](#vitest)
    - [Configuring Vitest](#configuring-vitest)
    - [Writing Tests](#writing-tests)
    - [Running Tests with Vitest](#running-tests-with-vitest)
  - [React Testing Library](#react-testing-library)
    - [Testing UI is Hard](#testing-ui-is-hard)
    - [Testing Library](#testing-library)
    - [Setting Up React Testing Library](#setting-up-react-testing-library)
    - [Testing a Component](#testing-a-component)
    - [A Simple Test](#a-simple-test)
    - [Types of Queries](#types-of-queries)
    - [Matching Text](#matching-text)
    - [Testing User Interactions](#testing-user-interactions)
    - [Simulating Users with user-event](#simulating-users-with-user-event)
    - [Firing DOM Events](#firing-dom-events)
  - [Mock Service Worker](#mock-service-worker)
    - [Recap: Why Mock APIs?](#recap-why-mock-apis)
    - [Recap: Mocking axios with Jest](#recap-mocking-axios-with-jest)
    - [Cons of Mocking](#cons-of-mocking)
    - [Mock Service Worker](#mock-service-worker-1)
    - [Using MSW](#using-msw)
  - [Looking Ahead](#looking-ahead)
  - [Resources](#resources)

---

## Testing React

Learn how to test React components with Vitest, React Testing Library, and Mock Service Worker.

To download the demo for this lecture:

```bash
dmget wb-testing-react
```

Then, `cd` into the project directory and run `npm install` to install the dependencies.

To run the app:

```bash
npm run dev
```

To run the tests:

```bash
npm run test
```

## Testing React Components

### Unit Tests for React Components

In addition to vanilla JavaScript code, we also want to write unit tests for React components.

- **Problem #1:** Our React code uses JSX syntax, transpiled by Vite into valid JS.
- **Problem #2:** It’s a lot of work to set up infrastructure for Jest and Vite to work together.

### Vitest

Vitest can do this for us!

- Has a Jest-like API (`describe`, `test`, `expect`, etc…)
- Works with all frameworks supported by Vite (React, Vue, Svelte, and more)
- Learn more about Vitest’s features [here](https://vitest.dev).

To install Vitest as a dev dependency:

```bash
npm install -D vitest
```

### Configuring Vitest

Vitest mostly works like Jest out-of-the-box, except it doesn’t support globals like Jest. By default, you have to import `describe`, `test`, etc. from Vitest in your tests.

You can change this in your Vite configuration file:

**vite.config.js**

```javascript
import react from "@vitejs/plugin-react";
import { defineConfig } from "vite";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  test: {
    globals: true,
  },
});
```

### Writing Tests

Writing tests works just like Jest:

**src/**tests**/example.test.js**

```javascript
test("it works", () => {
  expect(1).toBe(1);
});
```

### Running Tests with Vitest

**package.json**

```json
"scripts": {
  "test": "vitest"
}
```

Run the tests with:

```bash
npm run test
```

## React Testing Library

### Testing UI is Hard

Let’s say you have tests for a Subscribe button:

```html
<button>Subscribe</button>
```

During a UI redesign, you change the button to a link:

```html
<a>Subscribe</a>
```

This could cause your tests to fail even though the functionality of Subscribe hasn’t changed.

### Testing Library

Testing Library is a family of packages for writing tests in a user-centric way.

> **The more your tests resemble the way your software is used, the more confidence they can give you.**  
> – from Testing Library’s Guiding Principles

Testing Library includes APIs that allow you to:

- Render UI components in your tests
- Query for elements in a user-centric way
- Emulate user events like clicking on buttons

We’ll use the version of Testing Library for React: React Testing Library.

### Setting Up React Testing Library

Install the following dependencies:

```bash
npm install -D jsdom @testing-library/react @testing-library/user-event @testing-library/jest-dom
```

Create a `setup.js` file in your `__tests__` directory:

**src/**tests**/setup.js**

```javascript
import matchers from "@testing-library/jest-dom/matchers";
import { cleanup } from "@testing-library/react";
import { afterEach, expect } from "vitest";

// Add React Testing Library's Jest matchers
expect.extend(matchers);

// Clean up and reset components after each test
afterEach(() => {
  cleanup();
});
```

Add the following to `vite.config.js`:

**vite.config.js**

```javascript
import react from "@vitejs/plugin-react";
import { defineConfig } from "vite";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  test: {
    globals: true,
    environment: "jsdom",
    setupFiles: "./src/__tests__/setup.js",
  },
});
```

### Testing a Component

General steps for testing a component:

1. Render the component you’re testing.
2. Select an element with a query.
3. (Optional) Use the element to simulate user interactions with the page.
4. Use a Jest or jest-dom matcher to test the element.

### A Simple Test

**src/components/Counter.jsx**

```javascript
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

**src/**tests**/Counter.test.jsx**

```javascript
test("renders initial text", () => {
  render(<Counter />);
  expect(screen.getByText("Count: 0")).toBeInTheDocument();
});
```

- `render()` renders a component to the screen, which contains the DOM.
- `getByText()` is a query method provided by Testing Library.
- `toBeInTheDocument()` is a matcher that tests if the element appears in the DOM matcher.

### Types of Queries

Queries start with `getBy`, `queryBy`, or `findBy` (or `getAllBy`, `queryAllBy`, `findAllBy` for multiple elements).

Lots of ways to query depending on how users interact with your code:

- `getByLabelText`
- `getByTitle`
- `getByDisplayValue`

**Which query to use?**

Need help deciding which query to use? The Testing Library docs give a list of recommended queries for different scenarios here: [Testing Library: About Queries - Priority](https://testing-library.com/docs/queries/about/#priority).

- **`getBy:`** Return exactly one element or throw an error.  
  Good for testing that an element should appear.

- **`queryBy:`** Return one or zero elements.  
  Good for testing for an element that shouldn’t appear.

- **`findBy:`** Like `getBy` but asynchronous.  
  Good for finding elements that only appear after an asynchronous event (e.g., test that new posts load on scroll).

### Matching Text

Most queries search for elements via a TextMatch argument.

TextMatch === a string, regex (regular expression pattern), or a matcher function.

```html
<div>JavaScript</div>
```

**Matching with a string**

```javascript
screen.getByText("JavaScript"); // full string match
```

**Matching a regex**

```javascript
screen.getByText(/javascript/i); // substring match, ignore case
```

**Matching with a function**

```javascript
screen.getByText((content, element) => content.startsWith("Java"));
```

Unless you’re very sure you need an exact match, you should use `/search text/i`.

- It will match different casing:

  - Search Text
  - search text
  - sEaRch tExt

- It will match as long as search text appears somewhere in the text:
  - search text:
  - search text and close

### Testing User Interactions

#### Simulating Users with user-event

Simulate user interactions with the `@testing-library/user-event` library.

**src/**tests**/Counter.test.jsx**

```javascript
test("increments the count", async () => {
  render(<Counter />);
  const user = userEvent.setup();

  await user.click(screen.getByRole("button", { name: /increment/i }));

  expect(screen.getByText(/count: 1/i)).toBeInTheDocument();
});
```

- `userEvent.setup()` creates a user session for emulating user interactions.
- `getByRole()` is a query for finding interactive elements—finds the button labeled Increment Count.
- `await user.click()` clicks on the element.

#### Firing DOM Events

The

user-event package doesn’t support all events. If you can’t perform an interaction with `user-event`, you can fire a DOM event with `fireEvent`.

We want to test `SelectColor` by changing the value of `<select>`:

**src/components/SelectColor.jsx**

```javascript
import { useState } from "react";

export default function SelectColor() {
  const [favoriteColor, setFavoriteColor] = useState("red");

  const colorElements = {
    red: <span style={{ color: "red" }}>Red</span>,
    green: <span style={{ color: "green" }}>Green</span>,
    blue: <span style={{ color: "blue" }}>Blue</span>,
  };

  return (
    <div>
      <p>{colorElements[favoriteColor]}</p>
      <label htmlFor="fav-color">Select a color</label>
      <select
        id="fav-color"
        name="favoriteColor"
        onChange={(e) => setFavoriteColor(e.target.value)}
      >
        <option value="red">Red</option>
        <option value="green">Green</option>
        <option value="blue">Blue</option>
      </select>
    </div>
  );
}
```

**src/**tests**/SelectColor.test.jsx**

```javascript
test("changes colors", () => {
  render(<SelectColor />);

  // Change the value of <select> to 'green'
  fireEvent.change(screen.getByRole("combobox", { name: /select a color/i }), {
    target: { value: "green" },
  });

  // Check that the <span> has the text 'Green'
  expect(screen.getByText(/green/i, { selector: "span" })).toBeInTheDocument();
});
```

## Mock Service Worker

### Recap: Why Mock APIs?

Review: Why mock API requests?

- To isolate external code so we only test our code.

### Recap: Mocking axios with Jest

```javascript
jest.unstable_mockModule("axios", () => {
  return {
    default: {
      get: jest.fn().mockResolvedValue({
        data: "test data",
      }),
    },
  };
});
```

### Cons of Mocking

- The `axios.get` mock can only return one thing (unless we call `mockReturnValue`).
- What if we decide to refactor and use `fetch` instead of `axios.get`?
- Mocks aren’t realistic—it doesn’t simulate an actual REST API.

### Mock Service Worker

Mock Service Worker (MSW) intercepts requests on the network level. In other words, your app will think it’s getting responses from a real API.

### Using MSW

We want to test Fetch:

**src/components/Fetch.jsx**

```javascript
import axios from "axios";
import { useState } from "react";

export default function Fetch({ requestURL }) {
  const [data, setData] = useState(null);

  const fetchData = async () => {
    const res = await axios.get(requestURL);
    setData(res.data);
  };

  return (
    <div>
      <button onClick={fetchData}>Get data</button>
      <pre>{data ? JSON.stringify(data, null, 2) : "No data"}</pre>
    </div>
  );
}
```

To set up MSW for a test:

**src/**tests**/Fetch.test.jsx**

```javascript
const server = setupServer(
  // API is similar to Express!
  rest.get("/test", (req, res, ctx) => {
    return res(ctx.json("test data"));
  })

  // Can list more routes here
);

beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());
```

**src/**tests**/Fetch.test.jsx**

```javascript
test("renders with initial text", () => {
  render(<Fetch requestURL="/test" />);
  expect(screen.getByText(/no data/i)).toBeInTheDocument();
});

test("fetches data from request URL", async () => {
  render(<Fetch requestURL="/test" />);
  const user = userEvent.setup();

  await user.click(screen.getByRole("button", { name: /get data/i }));
  expect(screen.getByText(/test data/i)).toBeInTheDocument();
});
```

Learn more about defining REST API routes at the [MSW docs](https://mswjs.io/docs).

## Looking Ahead

## Resources

### Guides and Documentation

- [Query Guide](https://testing-library.com/docs/queries/about)
- [user-event](https://testing-library.com/docs/ecosystem-user-event)
- [Firing Events](https://testing-library.com/docs/queries/about)
- [List of jest-dom matchers](https://github.com/testing-library/jest-dom)

### Examples

- [React Example](https://github.com/testing-library/react-testing-library)
- [React Router Example](https://github.com/remix-run/react-router/tree/main/examples)

### Tools

- [Testing Library Query Playground](https://testing-playground.com/)
- The Chrome extension generates Testing Library queries via the Chrome Dev Tools.
- Testing Library Recorder extension: record clicks and generate Testing Library code.

---
