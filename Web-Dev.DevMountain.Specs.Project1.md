---
id: malvi3mocvvld62varl6qr2
title: Project1
desc: ''
updated: 1721504940243
created: 1721504432101
---

# Welcome to React

## Introduction

Welcome to React! This week you will be introduced to your new coding language. React is built on top of Javascript, so it will be familiar in some ways, yet different in others! You will learn about creating new apps, components, state, and passing information from one file/component to another via props. Best of luck, and happy coding!

## Concepts and Objectives

### React 101

- Explain the React Framework
- Can use create-react-app
- Can explain what JSX is
- Understands SPA’s
- Students understand arrow functions, filter, map, and spread
- Student understands the pros and cons of React vs other frameworks
- Student can explain SPAs and the Virtual DOM

### React Basics and Working with Components & Props

- Student understands React Components
- Student can pass a prop from a parent to a child
- Student can explain JSX and how React components use it

### Managing State & Events

- Student can initialize state
- Student can modify state with an event
- Student understands binding in React
- Student can modify state from a child component

### Rendering Lists & Styling Components

- Student can render items in a list
- Student understands 3 different ways to style react components
- Student can use React Dev Tools
- Student understands and can use reusable components

### Review

- Student can initialize a project with create-react-app
- Student can create and render custom components
- Student can initialize state and modify it with events
- Student can pass props and render them in a child component
- Student can render a list of reusable components

## Project Overview

This project will introduce you to the basics of React - creating a React app, creating custom components, managing state, gathering user input, and passing props.

### MVP

#### Features

- User sees a 3x3 tic-tac-toe board on the screen
- The game alternates between placing an “X” and “O”
- The game checks to see if a player has won
- The game indicates which user has won, “X” or “O”

#### Code

- App has minimal custom styling
- App uses more than 2 components
- App uses useState
- App uses onClick
- App passes props
- App uses .map

## Enroll in Courses

Before you watch any content for this unit, ensure that you are enrolled in the following course(s) on Udemy. Once you’re enrolled, the links in the content sections of this page will take you to the correct sections of the course.

- One

## React 101

### Objectives

- Explain the React Framework
- Can use create-react-app
- Can explain what JSX is
- Understands SPA’s
- Students understand arrow functions, filter, map, and spread
- Student understands the pros and cons of React vs other frameworks
- Student can explain SPAs and the Virtual DOM

### Summary

In these videos you will be customizing your VS Code environment to better suit your future as a React developer! We will also be brushing up on a lot of Javascript and covering what React is.

### Content

- VS Code: React Extensions and Tips
  - Follow along with this video to get your VS Code set up for React!
- Getting Started (from React - The Complete Guide)
- JavaScript Refresher (from React - The Complete Guide)

### Project Part 1: Creating a React app

#### Goal

In part 1, you will create your first React application.

#### Concepts

- CRA
- Components
- State
- Props
- User Input

#### Steps

1. Create a new react app from the command line
   - Navigate in your command line to the location you want to create your app
   - Run `create-react-app@latest tic-tac-toe`
   - `npx create-react-app@latest tic-tac-toe`
2. Download CSS for this project
   - You can download the CSS for this project here:
     - [Tic Tac Toe CSS](https://example.com/css)

## React Basics and Working with Components & Props

### Objectives

- Student understands React Components
- Student can pass a prop from a parent to a child
- Student can explain JSX and how React components use it

### Summary

Today you will learn what makes React so versatile as a language! Not only will you cover conceptual topics regarding React (such as JSX, how React actually works, etc), but you will learn about creating components, and passing information to them with props!

### Content

- React Basics & Working with Components (from React - The Complete Guide)

### Project Part 2: Creating Components & Working with Props

#### Goal

In Part 2 you will create your first custom component and pass props from a parent to a child.

#### Concepts

- Components
- Props

#### Steps

1. Create a new file named Square.jsx
   - In the `src` folder of your tic-tac-toe project create a new file and name it `Square.jsx`
   - In VSCode right click the `src` folder, click New File and type `Square.jsx`
   - In the terminal navigate to your tic-tac-toe app, `cd` to `src` and type `touch Square.jsx`
2. Create a functional React Component in Square.jsx and export it

   - `import React from react`
   - Create an arrow function called Square
   - Outside of the function export it as default
   - In the return statement of the function create a `div` with a class name of `square`
   - Inside the `div` display the word square

   ```jsx
   import React from "react";

   const Square = () => {
     return <div className="square">square</div>;
   };

   export default Square;
   ```

3. Render the square component in App.js

   - Remove all HTML except the `div` with className of `App` from App.js
   - Import Square.js into App.js
   - Render the Square component inside of the App `div`

   ```jsx
   import "./App.css";
   import Square from "./Square";

   return <Square />;
   ```

4. Create a variable in App.js and pass it as props to the square component

   - Above the return statement, create a variable of your choice and assign it a value of a string of your choice
   - In the return, on the Square component create an attribute called `propVar` and set it equal to the variable you created in the previous step using JSX

   ```jsx
   const propVariable = 'This is a prop'

   <Square propVar={propVariable}/>
   ```

5. Render the prop variable in the Square component

   - In Square.jsx take props as an argument to your Square function
   - In the returned `<div>` replace the word square with `props.variableName` (variableName being the variable you created in Step 4)

   ```jsx
   import React from "react";

   const Square = (props) => {
     return <div className="square">{props.propsVar}</div>;
   };

   export default Square;
   ```

## Managing State & Events

### Objectives

- Student can initialize state
- Student can modify state with an event
- Student understands binding in React
- Student can modify state from a child component

### Summary

React State will be your best friend moving forward! You will learn how to initialize state, and why we use it! You will also learn how to handle events in React (hint: It’s SO much easier than with vanilla JS).

### Content

- React State & Working with Events (from React - The Complete Guide)

### Project Part 3: Managing State

#### Goal

In Part 3 you will create and manage state variables and pass them as props.

#### Concepts

- State
- Props

#### Steps

1. In App.js destructure useState from react
   - At the top of App.js add `import { useState } from 'react'`
   ```jsx
   import { useState } from "react";
   import "./App.css";
   import Square from "./Square";
   ```
2. Initialize state variables for the game board and the player turn
   - Using array destructuring initialize the state for the games squares to an array of 9 empty strings
   - Using the same method initialize state of the player variable to a boolean of true
   ```jsx
   const [squares, setSquares] = useState(["", "", "", "", "", "", "", "", ""]);
   const [player, setPlayer] = useState(true);
   ```
3. Pass the state variables and setters as props to the square component
   - Add a prop of squares that is equal to the squares state variable to the Square component
   - Add a prop of setSquares that is equal to the setSquares function to the Square component
   - Add a prop of player that is equal to the player state variable to the Square component
   - Add a prop of setPlayer that is equal to the setPlayer function to the Square component
   - Remove the existing prop from the Square component
   ```jsx
   <Square
     squares={squares}
     setSquares={setSquares}
     player={player}
     setPlayer={setPlayer}
   />
   ```
4. Verify the props are being passed correctly
   - In Square.jsx remove the render of the previous variable
   ```jsx
   console.log(props.squares, props.player);
   ```
   - Result: `(9) ['', '', '', '', '', '', '', '', ''] true`

## Rendering Lists & Styling Components

### Objectives

- Student can render items in

a list

- Student understands 3 different ways to style react components
- Student can use React Dev Tools
- Student understands and can use reusable components

### Summary

Creating lists of items from an array is present in nearly every React project. You will learn now to render these lists effectively as well as the different options you have to style your React Projects!

### Content

- Rendering Lists & Conditional Content (from React - The Complete Guide)
- Styling React Components (from React - The Complete Guide)

### Project Part 4: Rendering a component with .map() and handling user click events

#### Goal

In part 4 we will learn to reuse a component multiple times by rendering it once for each item in an array and handle click events.

#### Concepts

- Reusable Components
- Array Methods
- Handling events

#### Steps

1. Map over the squares array and render the Square.jsx component for each item in the array
   - In the return statement of App.js remove the comment out the Square component
   - Inside of the div with the className of “App” create a new div with a className of “container”
   - Inside this div render a jsx block - `{}`
   - Inside this jsx invoke the `.map` array method on the squares array and take in the value and index as arguments to the callback function
   - In the callback function return the Square component with all of its previous props, but with two more, squareValue which is equal to the value argument, and index which is equal to the index
   ```jsx
   return (
     <div className="App">
       <div className="container">
         {squares.map((val, index) => {
           return (
             <Square
               setSquares={setSquares}
               index={index}
               squareValue={val}
               squares={squares}
               player={player}
               setPlayer={setPlayer}
             />
           );
         })}
       </div>
     </div>
   );
   ```
2. Write logic to handle when a user clicks on any individual square
   - In Square.jsx create a function named handleClick
   - Check if there is a value in `props.squareValue`
   - If there is no value, but the player state that is passed through props is true, change the value of `props.squares` at `props.index` to “X”, invoke the `setSquares` function from props passing the new squares array, and toggle the value of `props.player`
   - Otherwise change the value at `props.index` to “O”, invoke `props.setSquares` with the new value of `props.squares` and toggle the value of `props.player`
   ```jsx
   const handleClick = () => {
     if (!props.squareValue) {
       if (props.player) {
         props.squares.splice(props.index, 1, "X");
         props.setSquares(props.squares);
         props.setPlayer(!props.player);
       } else {
         props.squares.splice(props.index, 1, "O");
         props.setSquares(props.squares);
         props.setPlayer(!props.player);
       }
     }
   };
   ```
3. Listen for an onClick event on the div with the className of square, and invoke the handleClick function
   ```jsx
   <div className="square" onClick={handleClick}>
     ...
   </div>
   ```
4. Using a ternary, render an O or X based on the props.squareValue
   - Inside the square div render jsx
   - Inside that jsx write a ternary statement that evaluates if `props.squareValue` is equal to a string of “O”
   - If so, render text of O or an image of the Devmountain Logo (you can use this link for the logo: `https://cdn.discordapp.com/attachments/830137099042816080/984895322184634448/devcircle_1.png`)
   - If the value is not “O”, render the value of `props.squareValue`
   ```jsx
   {
     props.squareValue === "O" ? (
       <img src="https://cdn.discordapp.com/attachments/830137099042816080/984895322184634448/devcircle_1.png" />
     ) : (
       props.squareValue
     );
   }
   ```
5. Write a function in App.js that will reset the board when a button is clicked

   - In App.js create a function named handleClick
   - In this function invoke setSquares passing it an array with 9 empty strings
   - Invoke setPlayer passing a boolean of true
   - Inside the div with className of “App” render a button with an onClick equal to handleClick with text of ‘Reset’

   ```jsx
   // 1
   const handleClick = () => {
     setSquares(["", "", "", "", "", "", "", "", ""]);
     setPlayer(true);
   };

   // 2
   <button onClick={handleClick}>Reset</button>;
   ```

## Review

### Objectives

- Student can initialize a project with create-react-app
- Student can create and render custom components
- Student can initialize state and modify it with events
- Student can pass props and render them in a child component
- Student can render a list of reusable components

### Summary

Debugging in React is similar to Vanilla JS, except you have a couple tools to add to your arsenal. You will learn how best to debug a React application, as well as review all the concepts you’ve learned so far with a small project. Best of luck, and happy coding!

### Content

- Debugging React Apps (from React - The Complete Guide)
- A Complete Practice Project (from React - The Complete Guide)

### Project Part 5: Calculating a winner

#### Goal

In part 5 you will write logic to evaluate if a player has won the game and display that winner.

#### Concepts

- Conditionals
- Loops
- Logic

#### Steps

1. Write a function that will check if there is a winner
   - Create a function called calculateWinner that takes in an array
   - In that function, create a variable called lines that is equal to an array.
   - Each item in the array will be a sub array of winning combinations
   - ie: `[0, 1, 2]` is the top row horizontally of the board, `[0, 3, 6]` is the diagonal from top left to bottom right, etc
   - Loop over the lines variable
   - Inside the loop destructure the values of each subArray from lines[i] – `const [a, b, c] = lines[i]`
   - Check if the values of the array at the indexes a, b, and c match. If so, return a string that declares that the value in arr[a] won. Otherwise, return a string of “Who will win?”.
   ```jsx
   function calculateWinner(arr) {
     const lines = [
       [0, 1, 2],
       [3, 4, 5],
       [6, 7, 8],
       [0, 3, 6],
       [1, 4, 7],
       [2, 5, 8],
       [0, 4, 8],
       [2, 4, 6],
     ];
     for (let i = 0; i < lines.length; i++) {
       const [a, b, c] = lines[i];
       if (arr[a] && arr[a] === arr[b] && arr[a] === arr[c]) {
         return `${arr[a]} won!`;
       }
     }
     return "Who will win?";
   }
   ```
2. Invoke the calculate winner function
   - Create a span element as a child of the “App” div
   - Inside the span render jsx that is equal to calculateWinner invoked with the squares array as the argument
   ```jsx
   <span>{calculateWinner(squares)}</span>
   ```

## Solution

You can download the solution for this project here:

- [Solution Code](https://example.com/solution)

## Survey

Please complete this survey when you have finished this unit.

```

```
