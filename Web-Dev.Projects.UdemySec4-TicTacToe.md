---
id: s2ph0fzltyq9yyo1x9tu2lr
title: UdemySec4-TicTacToe
desc: ""
updated: 1722371303033
created: 1722366491329
---

New Project, New Concepts

1. Multiple State Values
2. Nested Lists
3. Array & Object States
4. Lifting State Up
5. Derived State
6. Component Functions vs Normal Functions

## The `public/` Folder

As shown in the previous lecture you can store images in the `public/` folder and then directly reference them from inside your `index.html` or `index.css` files.

The reason for that is that images (or, in general: files) stored in `public/` are made publicly available by the underlying project development server & build process. Just like `index.html`, those files can directly be visited from inside the browser and can therefore also be requested by other files.

If you try loading `localhost:5173/some-image.jpg`, you'll be able to see that image (if it exists in the `public/` folder, of course).

## The `src/assets/` Folder

You can also store images in the `src/assets/` folder (or, actually, anywhere in the `src` folder).

So what's the difference compared to `public/`?

Any files (of any format) stored in `src` (or subfolders like src/assets/) are not made available to the public. They can't be accessed by website visitors. If you try loading `localhost:5173/src/assets/some-image.jpg`, you'll get an error.

Instead, files stored in `src/` (and subfolders) can be used in your code files. Images imported into code files are then picked up by the underlying build process, potentially optimized, and kind of "injected" into the public/ folder right before serving the website. Links to those images are automatically generated and used in the places where you referenced the imported images.

## Which Folder Should You Use?

You should use the `public/` folder for any images that should not be handled by the build process and that should be generally available. Good candidates are images used directly in the `index.html` file or favicons.

On the other hand, images that are used inside of components should typically be stored in the `src/` folder (e.g., in `src/assets/`).

# Using State to Manage Input Fields

```js
import { useState } from "react";

export default function Player({ name, symbol }) {
  const [isEditing, setIsEditing] = useState(false);
  return (
    <li>
      <span className="player">
        <span className="player-name">{name}</span>
        <span className="player-symbol">{symbol}</span>
      </span>
      <button>Edit</button> // When this button is pressed, the name field should
      become editable. The button should change to Save so the user can confirm the
      name. So we will need to use state to manage the edit mode.
    </li>
  );
}
```

Exercise:

1. Add a function that's triggered when the <button> is clicked
2. Change isEditing to true in that function.
3. Show the <span className="player-name"> only when isEditing is false.
4. Show an <input> element if isEditing is true.

```js
// Import the useState hook from React, which allows you to add state to functional components.
import { useState } from "react";

// Define the Player component, which takes props { name, symbol }.
export default function Player({ name, symbol }) {
  // useState hook to create a state variable 'isEditing' and a function 'setIsEditing' to update it.
  // Initially, 'isEditing' is set to false.
  const [isEditing, setIsEditing] = useState(false);

  // Function to handle the click event on the Edit button.
  // When called, it sets 'isEditing' to true.
  function handleEditClick() {
    setIsEditing(true);
  }

  // Variable to hold the JSX for displaying the player's name.
  // Initially, it's set to a span element that displays the player's name.
  let playerName = <span className="player-name">{name}</span>;

  // If 'isEditing' is true, update playerName to an input field instead of a span.
  if (isEditing) {
    playerName = <input type="text" required />;
  }

  // The return statement contains the JSX to render the Player component.
  return (
    // The component returns a list item (li) element.
    <li>
      {/* The span element groups the player's name and symbol. */}
      <span className="player">
        {/* Render the playerName variable, which will be either a span or an input field based on 'isEditing'. */}
        {playerName}
        {/* Display the player's symbol in a span element. */}
        <span className="player-symbol">{symbol}</span>
      </span>
      {/* Button to trigger the edit mode. When clicked, it calls handleEditClick, which sets 'isEditing' to true. */}
      <button onClick={handleEditClick}>Edit</button>
    </li>
  );
}
```

### Key Points:

1. **Import Statement**: The `useState` hook from React is imported to manage state within the functional component.
2. **Player Component**: A functional component that takes `name` and `symbol` as props to display a player's information.
3. **useState Hook**: Creates a state variable `isEditing` and a setter function `setIsEditing`. Initially, `isEditing` is set to `false`, indicating the component is not in edit mode.
4. **handleEditClick Function**: When the Edit button is clicked, this function sets `isEditing` to `true`, switching the component to edit mode.
5. **playerName Variable**: Holds the JSX for displaying the player's name. By default, it is a `span` element. If `isEditing` is `true`, it becomes an `input` field.
6. **JSX Structure**: The component returns a `li` element containing:
   - A `span` for the player's name, which can switch between a `span` and an `input` field based on `isEditing`.
   - A `span` for the player's symbol.
   - An `Edit` button that toggles the edit mode.
7. **Dynamic Content**: The player's name display switches between a static `span` and an editable `input` field depending on the `isEditing` state. This demonstrates how state can be used to dynamically change the rendered content in a React component.
