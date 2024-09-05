---
id: u37vi9ofqr398uwc83qw20y
title: Code
desc: ""
updated: 1724108769694
created: 1724081168579
---

**Code Structure**

```lua
code-notes-app
|--> src/
|    |--> assets
|    |    |--> react.svg
|    |    |--> vite.svg
|    |--> components
|    |    |--> CodeNotes
|    |    |    |--> CodeNotes.css
|    |    |    |--> CodeNotes.jsx
|    |    |    |--> NoteEditor.jsx
|    |    |    |--> Notesist.css
|    |    |    |--> NotesList.jsx
|    |    |--> Header
|    |    |    |--> Header.css
|    |    |    |--> Header.jsx
|    |    |--> HomePage
|    |    |    |--> Home.css
|    |    |    |--> Home.jsx
|    |    |--> MarkdownEditor
|    |    |    |--> MarkdownEditor.css
|    |    |    |--> MarkdownEditor.jsx
|    |    |--> Spinner
|    |    |    |--> Spinner.css
|    |    |    |--> Spinner.jsx
|    |    |--> store
|    |    |    |--> authContext.jsx
|    |--> hooks
|    |    |--> useNotes.js
|    |--> services
|    |    |--> authServide.js
|    |    |--> noteService.js
|    |--> App.css
|    |--> App.jsx
|    |--> index.css
|    |--> main.jsx
|    |--> supabaseClient.js
```

---

## Overview of `supabaseClient.js`

```js
// code-notes-app/src/supabaseClient.js
// Date and Time: 2024-08-12 21:10:00

import { createClient } from "@supabase/supabase-js";

const supabaseUrl = import.meta.env.VITE_SUPABASE_URL;
const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY;

if (!supabaseUrl || !supabaseAnonKey) {
  throw new Error("Supabase URL or Anon Key not set in environment variables.");
}

export const supabase = createClient(supabaseUrl, supabaseAnonKey, {
  auth: {
    persistSession: false, // Disable session persistence
    autoRefreshToken: true, // Still allow auto-refreshing of tokens
  },
});

console.log("Supabase client initialized:", supabaseUrl);
```

`supabaseClient.js` is the initialization script for the Supabase client in your React application. This script is crucial for connecting your front-end React app with your Supabase backend services, including authentication, database operations, and more.

### Breakdown of the Code

#### 1. **Importing the Supabase Client**

```javascript
import { createClient } from "@supabase/supabase-js";
```

- **`createClient`**: This function is imported from the `@supabase/supabase-js` package. It’s used to create a new instance of the Supabase client, which will allow your React app to interact with the Supabase API.

#### 2. **Defining Supabase URL and Anon Key**

```javascript
const supabaseUrl = import.meta.env.VITE_SUPABASE_URL;
const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY;
```

- **`supabaseUrl`**: This is the base URL of your Supabase project. It's typically something like `https://your-project-ref.supabase.co`. This URL points to the instance of Supabase where your project's services (database, authentication, etc.) are hosted.
- **`supabaseAnonKey`**: This is the "anonymous" public API key provided by Supabase. It allows your application to interact with the Supabase services securely but with some limitations on access and permissions. It’s meant to be used on the client side.

Both `supabaseUrl` and `supabaseAnonKey` are expected to be stored in environment variables (in a `.env` file), which are accessed via `import.meta.env.VITE_SUPABASE_URL` and `import.meta.env.VITE_SUPABASE_ANON_KEY`. These environment variables help keep sensitive information (like API keys) out of your source code.

#### 3. **Environment Variable Check**

```javascript
if (!supabaseUrl || !supabaseAnonKey) {
  throw new Error("Supabase URL or Anon Key not set in environment variables.");
}
```

- This check ensures that both the `supabaseUrl` and `supabaseAnonKey` environment variables are properly set. If either is missing, an error is thrown. This is a safeguard to prevent the application from trying to interact with Supabase without the necessary configuration.

#### 4. **Creating the Supabase Client**

```javascript
export const supabase = createClient(supabaseUrl, supabaseAnonKey, {
  auth: {
    persistSession: false, // Disable session persistence
    autoRefreshToken: true, // Still allow auto-refreshing of tokens
  },
});
```

- **`createClient(supabaseUrl, supabaseAnonKey, { ... })`**: This function creates and configures the Supabase client. The first two arguments are the URL and the anonymous key, which are necessary for connecting to your specific Supabase project.
- **`persistSession: false`**: This setting in the `auth` configuration determines whether or not Supabase will automatically persist the user session in `localStorage` or `sessionStorage`. When set to `false`, Supabase will not save session data across browser reloads. This can be useful if you want to handle session management manually or if you want users to log in again each time they visit your app.

- **`autoRefreshToken: true`**: This setting enables automatic refreshing of the user's authentication token. Supabase will automatically handle refreshing tokens when they expire, without requiring the user to log in again. This helps maintain a smooth user experience.

#### 5. **Logging Initialization**

```javascript
console.log("Supabase client initialized:", supabaseUrl);
```

- This `console.log` statement outputs a confirmation message to the browser's console when the Supabase client is successfully initialized. It also logs the `supabaseUrl` to confirm which Supabase instance the client is connected to. This is mainly for debugging and ensuring that your application is connecting to the correct backend services.

### How It Works in the Application

1. **Initialization**: When your React app starts, this script runs to initialize the Supabase client. This client is then used throughout your app to interact with Supabase's services, like authentication and database queries.

2. **Environment-Specific Configuration**: By using environment variables (`VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`), the script ensures that your app can be easily configured for different environments (e.g., development, staging, production) without changing the source code.

3. **Interacting with Supabase**: Once initialized, the `supabase` client allows you to make authenticated requests to your Supabase backend, such as querying the database, inserting data, managing users, and more.

4. **Security**: By using the `anon` key, the app interacts with Supabase with limited permissions suitable for client-side operations. More sensitive operations can be restricted on the server side or require specific API keys.

### Summary

- The **Supabase client initialization script** is a crucial part of your React app, enabling it to connect and interact with your Supabase backend.
- It **fetches configuration details** from environment variables to ensure the app connects to the correct Supabase instance.
- It **configures** how authentication is handled, particularly how sessions are persisted and tokens are refreshed.
- Finally, it **exports** the `supabase` client instance so it can be used throughout the app for various operations like fetching data, handling authentication, and more.

---

## Overview of `noteService.js`

```js
// src/services/noteService.js
// Date and Time: 2024-08-18 @ 14:00

import { supabase } from "../supabaseClient";

export const fetchNotes = async (userId) => {
  try {
    const { data, error } = await supabase
      .from("notes")
      .select("*")
      .eq("user_id", userId)
      .order("id", { ascending: true });

    if (error) throw new Error(`Error fetching notes: ${error.message}`);

    return data;
  } catch (err) {
    console.error(err);
    throw err; // Ensure the error is properly thrown to be caught in the hook
  }
};

export const saveNote = async (note, userId) => {
  const { id, title, content } = note;

  if (id) {
    const { data, error } = await supabase
      .from("notes")
      .update({ title, content })
      .eq("id", id)
      .select("*");

    if (error) throw error;
    return data[0];
  } else {
    const { data, error } = await supabase
      .from("notes")
      .insert([{ title, content, user_id: userId }])
      .select("*");

    if (error) throw error;
    return data[0];
  }
};

export const deleteNote = async (noteId) => {
  const { error } = await supabase.from("notes").delete().eq("id", noteId);
  if (error) throw error;
};
```

The `noteService.js` file is a service module in your React application that encapsulates the logic for interacting with the Supabase database specifically for note-related operations. This service abstracts the details of how data is fetched, saved, and deleted from the database, making the rest of your application simpler and more maintainable.

### Breakdown of the Code

#### 1. **Importing the Supabase Client**

```javascript
import { supabase } from "../supabaseClient";
```

- **`supabase`**: This is the Supabase client instance that was initialized in your `supabaseClient.js` file. It provides methods to interact with your Supabase project, such as querying tables, performing CRUD (Create, Read, Update, Delete) operations, and handling authentication.

#### 2. **`fetchNotes` Function**

```javascript
export const fetchNotes = async (userId) => {
  try {
    const { data, error } = await supabase
      .from("notes")
      .select("*")
      .eq("user_id", userId)
      .order("id", { ascending: true });

    if (error) throw new Error(`Error fetching notes: ${error.message}`);

    return data;
  } catch (err) {
    console.error(err);
    throw err; // Ensure the error is properly thrown to be caught in the hook
  }
};
```

- **Purpose**: This function is responsible for fetching all notes associated with a specific user from the "notes" table in Supabase.

- **Parameters**:

  - `userId`: The unique identifier of the user whose notes you want to fetch. This `userId` is used to filter the notes in the database so that only the notes belonging to the logged-in user are retrieved.

- **How It Works**:
  1. **Querying the Database**: The function uses the Supabase client's `from` method to specify the "notes" table. The `select("*")` method indicates that it retrieves all columns from the table.
  2. **Filtering by `user_id`**: The `.eq("user_id", userId)` method filters the results to only include rows where the `user_id` matches the provided `userId`.
  3. **Ordering the Results**: The `.order("id", { ascending: true })` method sorts the notes by their `id` in ascending order.
  4. **Error Handling**: If there’s an error during the query, it throws an error with a custom message. The error is caught in the `catch` block, logged to the console, and then re-thrown so that it can be handled elsewhere (e.g., in a hook or component).
  5. **Returning Data**: If successful, the function returns the `data` (the array of notes) fetched from the database.

#### 3. **`saveNote` Function**

```javascript
export const saveNote = async (note, userId) => {
  const { id, title, content } = note;

  if (id) {
    const { data, error } = await supabase
      .from("notes")
      .update({ title, content })
      .eq("id", id)
      .select("*");

    if (error) throw error;
    return data[0];
  } else {
    const { data, error } = await supabase
      .from("notes")
      .insert([{ title, content, user_id: userId }])
      .select("*");

    if (error) throw error;
    return data[0];
  }
};
```

- **Purpose**: This function handles both creating new notes and updating existing ones in the "notes" table.

- **Parameters**:

  - `note`: An object containing the note data (`id`, `title`, `content`). If `id` is present, the function updates an existing note; if `id` is missing, it creates a new note.
  - `userId`: The `user_id` of the user who owns the note. This is necessary when creating a new note to associate it with the correct user.

- **How It Works**:
  1. **Check if Updating or Creating**:
     - If the `note` has an `id`, the function assumes it’s an existing note that needs to be updated.
     - If `id` is absent, it assumes this is a new note that needs to be created.
  2. **Updating a Note**:
     - The `.update({ title, content })` method updates the note with the new title and content where the `id` matches the provided `id`.
     - It then retrieves the updated note using `.select("*")` to return the updated data.
  3. **Creating a New Note**:
     - The `.insert([{ title, content, user_id: userId }])` method creates a new note in the database with the given title, content, and `user_id`.
     - It uses `.select("*")` to return the newly created note.
  4. **Error Handling**:
     - If an error occurs during either operation, the error is thrown, caught, and re-thrown to be handled by the calling code.
  5. **Returning Data**:
     - Whether updating or creating, the function returns the note data (the first item in the array of results).

#### 4. **`deleteNote` Function**

```javascript
export const deleteNote = async (noteId) => {
  const { error } = await supabase.from("notes").delete().eq("id", noteId);
  if (error) throw error;
};
```

- **Purpose**: This function deletes a note from the "notes" table.

- **Parameters**:

  - `noteId`: The unique identifier (`id`) of the note to be deleted.

- **How It Works**:
  1. **Deleting a Note**:
     - The `.delete()` method removes the note from the "notes" table where the `id` matches the provided `noteId`.
  2. **Error Handling**:
     - If an error occurs during deletion, it’s thrown so that it can be handled by the calling code.

### Summary

The `noteService.js` file abstracts the CRUD operations related to notes, making it easier to interact with the Supabase database from your React components or hooks. Here's how it functions in the application:

- **`fetchNotes(userId)`**: Retrieves all notes for a given user from the database.
- **`saveNote(note, userId)`**: Creates a new note or updates an existing one based on whether the note has an `id`.
- **`deleteNote(noteId)`**: Deletes a note from the database by its `id`.

These functions allow the application to manage notes efficiently, while also ensuring that the interactions with the database are handled consistently and with proper error handling. By encapsulating these operations in a service, the application becomes more modular and easier to maintain.

---

## Overview of **`useNotes.js`**

```js
// src/hooks/useNotes.js
// Date and Time: 2024-08-18 @ 14:00

import { useState, useEffect } from "react";
import { fetchNotes, saveNote, deleteNote } from "../services/noteService";

export const useNotes = (user) => {
  const [notes, setNotes] = useState([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");

  useEffect(() => {
    const loadNotes = async () => {
      setLoading(true);
      try {
        const data = await fetchNotes(user.id);
        setNotes(data);
      } catch (err) {
        setError("Failed to load notes. Please try again.");
      } finally {
        setLoading(false); // Ensure loading is set to false after the attempt
      }
    };

    if (user) {
      loadNotes();
    }
  }, [user]);

  const saveCurrentNote = async (note) => {
    setLoading(true);
    setError("");
    try {
      const updatedNote = await saveNote(note, user.id);
      setNotes((prevNotes) =>
        note.id
          ? prevNotes.map((n) => (n.id === note.id ? updatedNote : n))
          : [...prevNotes, updatedNote]
      );
    } catch (err) {
      setError("Failed to save the note. Please try again.");
    } finally {
      setLoading(false);
    }
  };

  const deleteCurrentNote = async (noteId) => {
    setLoading(true);
    setError("");
    try {
      await deleteNote(noteId);
      setNotes((prevNotes) => prevNotes.filter((n) => n.id !== noteId));
    } catch (err) {
      setError("Failed to delete the note. Please try again.");
    } finally {
      setLoading(false);
    }
  };

  return { notes, loading, error, saveCurrentNote, deleteCurrentNote };
};
```

The above code defines a custom React hook named `useNotes`, which is responsible for managing the lifecycle of notes in the application. This hook encapsulates all the logic for fetching, saving, and deleting notes, as well as handling loading states and errors. By using this custom hook, we can easily manage note-related operations in your React components without duplicating code.

### Breakdown of the Code

#### 1. **Importing Dependencies**

```javascript
import { useState, useEffect } from "react";
import { fetchNotes, saveNote, deleteNote } from "../services/noteService";
```

- **`useState` and `useEffect`**: These are React hooks. `useState` is used for managing component state, and `useEffect` is used for performing side effects, such as data fetching, in function components.
- **`fetchNotes`, `saveNote`, `deleteNote`**: These are service functions imported from `noteService.js`. They handle the actual interactions with the Supabase database for fetching, saving, and deleting notes.

#### 2. **Defining the `useNotes` Hook**

```javascript
export const useNotes = (user) => {
  const [notes, setNotes] = useState([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");
```

- **`useNotes`**: This is the custom hook that you will use in your components to manage notes.
- **`user`**: This parameter represents the current authenticated user. The user's `id` is used to fetch, save, and delete notes associated with this user.
- **State Variables**:
  - **`notes`**: Holds the list of notes fetched from the database.
  - **`loading`**: Tracks whether a data operation (fetch, save, delete) is in progress.
  - **`error`**: Stores any error message if an operation fails.

#### 3. **Fetching Notes (`useEffect`)**

```javascript
useEffect(() => {
  const loadNotes = async () => {
    setLoading(true);
    try {
      const data = await fetchNotes(user.id);
      setNotes(data);
    } catch (err) {
      setError("Failed to load notes. Please try again.");
    } finally {
      setLoading(false); // Ensure loading is set to false after the attempt
    }
  };

  if (user) {
    loadNotes();
  }
}, [user]);
```

- **`useEffect`**: This hook runs the `loadNotes` function when the component is first rendered or when the `user` changes.
- **`loadNotes` Function**:
  - **`setLoading(true)`**: The `loading` state is set to `true` to indicate that a data operation is in progress.
  - **`fetchNotes(user.id)`**: This function is called to fetch the notes from the database. It uses the `user.id` to ensure only the notes associated with this user are retrieved.
  - **Error Handling**: If an error occurs during the fetch, the error message is set in the `error` state.
  - **`finally` block**: Regardless of whether the fetch was successful or failed, `loading` is set to `false` to indicate that the operation has finished.

#### 4. **Saving a Note**

```javascript
const saveCurrentNote = async (note) => {
  setLoading(true);
  setError("");
  try {
    const updatedNote = await saveNote(note, user.id);
    setNotes((prevNotes) =>
      note.id
        ? prevNotes.map((n) => (n.id === note.id ? updatedNote : n))
        : [...prevNotes, updatedNote]
    );
  } catch (err) {
    setError("Failed to save the note. Please try again.");
  } finally {
    setLoading(false);
  }
};
```

- **`saveCurrentNote`**: This function is responsible for saving a note to the database.
  - **Parameters**:
    - `note`: The note object that is either being created or updated.
  - **`setLoading(true)`**: Sets the `loading` state to `true` to indicate that the save operation is in progress.
  - **`saveNote(note, user.id)`**: Calls the `saveNote` service function to save the note to the database.
  - **Updating State**:
    - If the note has an `id`, it's an existing note, so the existing note in the `notes` state is updated.
    - If the note does not have an `id`, it's a new note, so it’s added to the `notes` array.
  - **Error Handling**: If the save operation fails, an error message is set in the `error` state.
  - **`finally` block**: Resets the `loading` state to `false` after the save operation completes.

#### 5. **Deleting a Note**

```javascript
const deleteCurrentNote = async (noteId) => {
  setLoading(true);
  setError("");
  try {
    await deleteNote(noteId);
    setNotes((prevNotes) => prevNotes.filter((n) => n.id !== noteId));
  } catch (err) {
    setError("Failed to delete the note. Please try again.");
  } finally {
    setLoading(false);
  }
};
```

- **`deleteCurrentNote`**: This function is responsible for deleting a note from the database.
  - **Parameters**:
    - `noteId`: The ID of the note to be deleted.
  - **`setLoading(true)`**: Sets the `loading` state to `true` to indicate that the delete operation is in progress.
  - **`deleteNote(noteId)`**: Calls the `deleteNote` service function to remove the note from the database.
  - **Updating State**:
    - After successfully deleting the note from the database, the note is also removed from the `notes` state by filtering it out.
  - **Error Handling**: If the delete operation fails, an error message is set in the `error` state.
  - **`finally` block**: Resets the `loading` state to `false` after the delete operation completes.

#### 6. **Returning the Hook's State and Functions**

```javascript
return { notes, loading, error, saveCurrentNote, deleteCurrentNote };
```

- **`notes`**: The array of notes currently loaded from the database.
- **`loading`**: A boolean indicating whether a fetch, save, or delete operation is currently in progress.
- **`error`**: A string containing any error message that may have occurred during one of the operations.
- **`saveCurrentNote`**: The function to save a note.
- **`deleteCurrentNote`**: The function to delete a note.

### How It Works in Your Application

1. **Fetching Notes**: When the `useNotes` hook is used in a component, it automatically fetches the notes for the specified user when the component is mounted.
2. **Saving Notes**: The `saveCurrentNote` function can be called from a component to save a new note or update an existing one. The notes are then updated in the component’s state.
3. **Deleting Notes**: The `deleteCurrentNote` function can be called to remove a note, which updates the component’s state by removing the deleted note.
4. **Handling Loading and Errors**: The hook manages loading states and errors internally, providing the necessary information to the component so it can, for example, show a loading spinner or an error message to the user.

### Summary

- The `useNotes` custom hook simplifies the management of notes by providing a reusable, encapsulated way to fetch, save, and delete notes.
- It handles all the state management (`notes`, `loading`, `error`) and interacts with the `noteService.js` functions to perform the actual operations on the Supabase database.
- By using this hook, your components can easily integrate note management features without having to deal directly with Supabase or repetitive logic. This keeps your components clean and focused on rendering the UI.

---
