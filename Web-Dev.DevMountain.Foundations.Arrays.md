---
id: x3x09j5ltruz30wolbryzb5
title: Arrays
desc: ""
updated: 1722788993664
created: 1722788769495
---

Here is the webpage content formatted in Markdown:

---

# On this Page

- [Arrays and Looping](#arrays-and-looping)
  - [Intro](#intro)
  - [Goals](#goals)
  - [Arrays](#arrays)
    - [Types We've Seen So Far](#types-weve-seen-so-far)
    - [Multiple Foods](#multiple-foods)
    - [Arrays](#arrays-1)
    - [Accessing Items by Index](#accessing-items-by-index)
    - [Adding to Arrays: Push](#adding-to-arrays-push)
    - [Removing from Arrays: Pop](#removing-from-arrays-pop)
    - [Array Length](#array-length)
    - [Indexes Out of Bounds](#indexes-out-of-bounds)
    - [Task: Track Student Signups for a Course](#task-track-student-signups-for-a-course)
    - [Other Array Methods](#other-array-methods)
- [Strings and Indexes](#strings-and-indexes)
- [Loops](#loops)
  - [Tea Break](#tea-break)
  - [While Loops](#while-loops)
  - [Danger](#danger)
  - [The Break Statement](#the-break-statement)
  - [For Loops](#for-loops)
  - [Looping Through Arrays](#looping-through-arrays)
  - [Three Parts of a For Loop](#three-parts-of-a-for-loop)
  - [for…of Loops](#forof-loops)
  - [Nested Arrays and For Loops](#nested-arrays-and-for-loops)
  - [Nested Arrays](#nested-arrays)
  - [Nested For Loops](#nested-for-loops)
- [Looking Ahead](#looking-ahead)
  - [Coming Up](#coming-up)

---

# Arrays and Looping

To download the demo code for this lecture:

```bash
dmget wb-arrays-looping --demo
```

## Intro

## Goals

- Keep track of multiple items in arrays
- Examine and manipulate arrays
- Loop over arrays item-by-item
- Understand different methods of looping

## Arrays

### Types We've Seen So Far

- **String**
- **Integer**
- **Float**
- **Boolean** (true/false)
- **null**
- **undefined**

**What's the best data type to use for...**

- Name of a food dish
- Whether a dish is vegetarian or not
- Number of servings for a dish
- Cost of ingredients for a dish

### Multiple Foods

Say you want to keep track of meals you make each night:

```javascript
let meals = "artichokes, bbq, chili, donuts";
```

- Adding new items would be a pain
- Searching for or removing items would be quite hard

### Arrays

Arrays can contain multiple items:

```javascript
const meals = ["artichokes", "bbq", "chili", "donuts"];
```

- Here, each item is a string
- But you can put items of any type in an array
- Separate with commas and surround with `[ ]`
- Arrays are ordered (you can keep track of the order you make each dish)
- Arrays can contain duplicates (you might make a dish more than once)
- Good to use plural nouns for array variable names

### Accessing Items by Index

```javascript
const meals = ["artichokes", "bbq", "chili", "donuts"];
```

- Use square brackets `[ ]` to access an index
- **Warning!** Indexes start with 0
- `meals[0]` is "artichokes"
- Read as “meals at 0”

**Questions:**

- What is `meals[2]`?
- What is the index of "donuts"?

You can also change items in an array using the index:

```javascript
const meals = ["artichokes", "bbq", "chili", "donuts"];
meals[0] = "apple pie";

console.log(meals); // ["apple pie", "bbq", "chili", "donuts"]
```

#### Modifying a const array

Even if an array is a `const`, we can still modify the array by changing individual items in it.

```javascript
const meals = ["artichokes", "bbq", "chili", "donuts"];
meals[0] = "apple pie"; // OK! array is modified, not reassigned.
```

However, it won’t work to reassign the entire array:

```javascript
const meals = ["artichokes", "bbq", "chili", "donuts"];
meals = ["pasta", "pizza", "calzones"]; // error!
```

### Adding to Arrays: Push

To add an item to the end: `myArray.push(itemToAdd)`

```javascript
const meals = ["artichokes", "bbq", "chili", "donuts"];

meals.push("eggs");
meals.push("fajitas");

console.log(meals);
// ['artichokes', 'bbq', 'chili', 'donuts', 'eggs', 'fajitas']
```

### Removing from Arrays: Pop

To remove the last item in an array: `myArray.pop()`

This also returns the removed item.

```javascript
const meals = ["artichokes", "bbq", "chili", "donuts"];

const lastMeal = meals.pop();
console.log(lastMeal); // 'donuts'

console.log(meals); // ['artichokes', 'bbq', 'chili']
```

### Array Length

To get the length of an array: `myArray.length`

Note that since array indexes start at 0, the index of the last item in the array is actually the length minus 1.

```javascript
const meals = ["grits", "hummus", "ice cream"];
console.log(meals.length); // 3

console.log(meals[meals.length - 1]); // 'ice cream'
```

### Indexes Out of Bounds

If you try to access an item at an index that’s out-of-bounds, you’ll get `undefined` (not an error):

```javascript
const meals = ["artichokes", "bbq", "chili", "donuts"];
console.log(meals[4]); // undefined
```

### Task: Track Student Signups for a Course

Say we’re using an array called `students`.

1. **How would we create an empty list?**

```javascript
students = [];
```

2. **How would we add a student?**

```javascript
students.push("Jane");
```

3. **How do we access the first student to sign up?**

```javascript
students[0];
```

4. **How do we find how many students have signed up?**

```javascript
students.length;
```

### Other Array Methods

- **unshift** and **shift**: add or remove items from the beginning of an array

```javascript
// .unshift() adds an element to the beginning of an array
meals.unshift("tacos");
console.log(meals); // ['tacos', 'artichokes', 'bbq', 'chili']

// .shift() removes the first element from an array
const firstMeal = meals.shift();
console.log(firstMeal); // tacos
console.log(meals); // ['artichokes', 'bbq', 'chili']
```

- **includes**: returns true if an item is in an array and false otherwise

```javascript
// .includes()
console.log(meals.includes("bbq")); // true
console.log(meals.includes("dim sum")); // false
```

- **indexOf**: returns the index of the item in the array, or -1 if it’s not there

```javascript
// .indexOf()
console.log(meals.indexOf("chili")); // 2
console.log(meals.indexOf("dim sum")); // -1
```

- **slice**: get a sub-array (does NOT modify the array)

```javascript
// .slice() with a start and end index returns a subarray
const mealsSubset = meals.slice(1, 3);
console.log(mealsSubset); // ['bbq', 'chili']
```

- **splice**: removes items from an array (and optionally adds new items)

```javascript
// .splice() removes elements from an array and optionally adds new elements
meals.splice(1, 1); // remove 1 element at index 1
console.log(meals); // ['artichokes', 'chili']
```

## Strings and Indexes

You can also use indexes to get individual characters in a string:

```javascript
const str = "software";
console.log(str[2]); // "f"
```

Strings also have a `.length`:

```javascript
console.log(str.length); // 8
```

However, none of the array methods (e.g. push, pop) will work on strings.

You also cannot reassign individual characters in a string.

## Loops

### Tea Break

If our tea is too hot, we’ll add a chip of ice.

Keep checking if it’s too hot and keep adding ice until it’s perfect.

```javascript
const perfectTemp = 125;
let teaTemp = 130;

if (teaTemp > perfectTemp) {
  // add a chip of ice
  teaTemp = teaTemp - 1;
}
if (teaTemp > perfectTemp) {
  // add a chip of ice
  teaTemp = teaTemp - 1;
}
// keep going ...
```

This is very repetitive.

You also won’t know how many `if` statements you need.

### While Loops

Instead, we can use a `while` loop which will repeat code over and over as long as a certain condition is true.

```javascript
const perfectTemp = 125;
let teaTemp = 130;

while (teaTemp > perfectTemp) {
  // add a chip of ice
  teaTemp -= 1;
  console.log("Tea temperature is now", teaTemp);
}
```

What if we mistakenly wrote `<` instead of `>`? What will happen?

```javascript
const perfectTemp = 125;
let teaTemp = 130;

while (teaTemp < perfectTemp) {
  // add a chip of ice
  teaTemp = teaTemp - 1;
}
```

What if we mistakenly wrote `+` instead of `-`? What will happen?

```javascript
const perfectTemp = 125;
let teaTemp = 130;

while (teaTemp > perfectTemp) {
  // add a chip of ice
  teaTemp = teaTemp + 1;
}
```

### Danger

Be careful to avoid an infinite loop!

> Skeleton waiting for an infinite loop.

### The Break Statement

`break` immediately exits a loop. For example, say we’re looking for Bob in a class of students:

```javascript
const students = ["Alice", "Bob", "Charlie", "Diana"];

let i = 0; // i stands for index
while (i < students.length) {
  console.log(students[i]);

  if (students[i] === "Bob") {
    console.log("Hi Bob!");
    break; // we found Bob, no need to loop any further!
  }
  i += 1;
}
```

## For Loops

### Looping Through Arrays

**Using a while loop:**

```javascript
const meals = ["artichokes", "bbq", "chili", "donuts"];

let i = 0;
while (i < meals.length) {
  console.log(meals[i]);
  i += 1;
}
```

**Using a for loop:**

```javascript
const meals = ["artichokes", "bbq", "chili", "donuts"];

for (let i = 0; i < meals.length; i += 1) {
  console.log(meals[i]);
}
```

### Three Parts of a For Loop

There are three parts to a `for` loop:

1. **Start condition.** Start with `i = 0`.
2. **Stop condition.** (Same as the condition for a `while` loop). Keep going as long as `i < meals.length`.
3. **Increment.** After each time through the loop, increment `i` by 1.

These types of `for` loops are sometimes called “generic” `for` loops.

```javascript
for (let n = 0; n < 10; n += 2) {
  console.log(n);
}
```

| **Iteration no.** | **n** | **Next value** |
| ----------------- | ----- | -------------- |
| 0                 |       |
| 1                 |       |
| 2                 |       |
| 3                 |       |
| 4                 |       |

After iteration no. 4, the next value for `n` is 10, which fails the condition `n < 10`, so the loop stops. As a result, the loop will output 0, 2, 4, 6, and 8.

`for` loops can also count down:

```javascript
for (let n = 10; n > 0; n -= 1) {
  console.log(n);
}
console.log("Blast off!");
```

**[MDN docs on for loops](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration#for_statement)**

### i++

Especially in `for` loops, you will often see the shorthand `i++`. This does exactly the same thing as `i += 1`. For example:

```javascript
for (let i = 0; i < meals.length; i++) {
  console.log(meals[i]);
}
```

Less commonly, you might also see `i--`, which is a shorthand for `i -= 1`.

### for…of Loops

The `for...of` statement is a special `for` loop which allows you to iterate through each element in an array.

It’s often easier to use if you don’t care about the indices.

```javascript
for (const meal of meals) {
  console.log(meal); // artichokes, bbq, chili
}
```

Since strings have indexes, you can loop through strings with generic `for` loops.

You can also use `for...of` loops with strings:

```javascript
const str = "Hello";
for (const letter of str) {
  console.log(letter); // H, e, l, l, o
}
```

## Nested Arrays and For Loops

### Nested Arrays

Arrays can be nested to make a two-dimensional grid:

```javascript
const grid = [
  ["A", "B", "C"],
  ["D", "E", "F"],
  ["G", "H", "I"],
];

console.log(grid[0]); // ['A', 'B', 'C']
console.log(grid[0][1]); // 'B'
console.log(grid[1][0]); // 'D'

grid[2][2] = "J"; // changes 'I' to 'J'
```

### Nested For Loops

To get all the items in a nested array, use two nested `for` loops:

```javascript
// Print all the letters in the grid on separate lines
for (const row of grid) {
  for (const letter of row) {
    console.log(letter);
  }
}
```

Or you can use nested generic `for` loops:

```javascript
// Alternative using generic for loops
for (let row = 0; row < grid.length; row += 1) {
  for (let col = 0; col < grid[row].length; col += 1) {
    console.log(grid[row][col]);
  }
}
```

## Looking Ahead

### Coming Up

- Functions
- Objects

---

This Markdown format organizes the content with headings, code blocks, and lists for better readability and structure.
