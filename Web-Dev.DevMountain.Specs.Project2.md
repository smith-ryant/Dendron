---
id: 8m6sj931b5awqwdwle9ynyv
title: Project2
desc: ''
updated: 1721504425498
created: 1721504289487
---

# Movie Watchlist

## Introduction

This unit covers some interesting material, such as how to plan out your React Projects from the start, other hooks aside from useState, how API Requests work in React, and an introduction to some legacy React code you might encounter in the workforce!

## Concepts and Objectives

### Project Planning

- Student understands and can diagram a component tree including necessary props and state management

### React Fundamentals: Hooks

- Students can use the useRef hook
- Students can use the useEffect Hook
- Students can use .split and .join to manipulate arrays
- Student can explain and use react fragments

### Managing State with useContext and useReducer

- Student can manage state across multiple components with useContext
- Student can manage more complex state with useReducer

### Movie Watchlist

- Student can define the differences between class & functional Components
- Student can explain the useMemo and useCallback
- Students can explain the component lifecycle
- Students can implement lifecycle methods

### API Requests

- Student can connect to an external API
- Student can make get and post requests
- Student can handle loading states
- Student can make requests inside useEffect
- Student understands and can use async/await functions

## Project Overview

In this project, you will be creating a list of movies and displaying them on the screen. From here, you should be able to add different movies to a watchlist and cycle through pages of movies.

## MVP

### Features

- User sees movie titles on the screen
- User sees movie posters on the screen
- User can add movies to a watchlist
- User can see their watchlist on screen
- User can remove movies from a watchlist

### Code

- App uses useState to store Movies
- App makes HTTP Request to movie database
- App passes Props
- App has reusable component
- App has more than 3 components
- App has useEffect Hook

## Enroll in Courses

Before you watch any content for this unit, ensure that you are enrolled in the following course(s) on Udemy. Once you’re enrolled, the links in the content sections of this page will take you to the correct sections of the course.

- One

## Project Planning

### Summary

- Student understands and can diagram a component tree including necessary props and state management

A developer always follows the SDLC, but sometimes it’s hard to know where to begin with a React Project. The video will cover a start-to-finish concept of how to plan out a React project, and we have some great articles that cover planning as well.

### Content

- React Project Planning
- Thinking in React (from the React docs)

### Part 1: Get your basic app setup

#### Summary

This part will get you your API key, project created, CSS imported, and a few components made.

#### Concepts

- API Keys
- CRA
- Components
- npm i
- Project Organization

#### Steps

1. Go to [The Movie Database](https://www.themoviedb.org/) and sign up
2. Go to settings
3. Get your API Key
4. Create a new react app from the command line
5. Install your required modules
6. Create your components folder & .env
7. Create the Header component
8. Import the Header

## React Fundamentals: Hooks

### Summary

- Students can use the useRef hook
- Students can use the useEffect Hook
- Students can use .split and .join to manipulate arrays
- Student can explain and use react fragments

Understanding the benefits of different hooks is crucial to your career. You’ll cover useEffect as a lifecycle hook, useRef for referencing values, and Portals for creating entry points in your HTML document (quite useful for popups and prompts).

### Content

- Working with Refs & Portals
- Handling Side Effects & Working with the useEffect() Hook

### Part 2: Seeing Movies on the Screen

#### Summary

In Part 2 you will call the useEffect function to access the movie API and pass the info down to a component for display.

#### Concepts

- useEffect
- Axios
- Components
- Reusable Components
- Props
- Map

#### Steps

1. Import and use ‘useEffect’ and ‘axios’
2. Create a Component to Display Movies
3. Import MovieScreen into App; Pass Props to Movie Screen

Let's see some movies!

## Managing State with useContext and useReducer

### Summary

- Student can manage state across multiple components with useContext
- Student can manage more complex state with useReducer

State is very useful, but we want to avoid passing it down as a prop more than a few components deep. With the powerful combo of useContext and useReducer, we can give our whole application access to some crucial pieces of state!

### Content

- React’s Context API & useReducer

### Part 3: Seeing our Whole Movie

#### Summary

Seeing a movie title is cool, but it’s not enough. Let’s create a reusable component that will display more info about the movie.

#### Concepts

- Reusable Components
- Props

#### Steps

1. Create a Component called MovieCard.jsx
2. Replace the `<h2>` inside of our `.map`
3. Make MovieCard reusable

## Optimizing React Apps

### Summary

- Student can define the differences between class & functional Components
- Student can explain the useMemo and useCallback
- Students can explain the component lifecycle
- Students can implement lifecycle methods

You will learn more hooks, useMemo and useCallback, to handle more functionality in your application. You will also learn about the lifecycle of components and how it lives in the DOM. Original code from React in the form of Class Components will also be introduced.

### Content

- A Look Behind the Scenes of React & Optimization Techniques
- An Alternative Way of Building Components: Class-based Components

### Part 4: Adding a Watchlist

#### Summary

We can see some movies now, but we need a watchlist to add them to. We will create a watchlist component and place it on the screen.

#### Concepts

- Components

#### Steps

1. Create a Watchlist Component
2. Place Watchlist into App.js
3. Have Watchlist display movies from List state
4. Create addMovie Function

Let's add some movies!

## API Requests

### Summary

- Student can connect to an external API
- Student can make get and post requests
- Student can handle loading states
- Student can make requests inside useEffect
- Student understands and can use async/await functions

Connecting to APIs and servers is just as important in React as it was in Vanilla JS. You’ll learn how to connect to APIs, create a seamless experience for the user with loading states, as well as how to make code asynchronous.

### Content

- Sending HTTP Requests
- Practice Project: Building a Food Order App

### Part 5: Adding final functionality

#### Summary

Adding movies is great, but now we need to remove the movies from the list, as well as display a different button to remove the movie! We will also add the ability to cycle through pages of movies.

#### Concepts

- Props
- State
- Conditional Rendering
- Lifecycle Methods

#### Steps

1. Create a removeMovie function
2. Pass removeMovie down as props
3. Check if a movie is in our watchlist
4. Conditionally render a new button
5. Create Page Navigation Buttons
6. Create two functions

## Solution

You can download the solution for this project here:

- Solution Code

## Survey

Please complete this survey when you have finished this unit.

```

```
