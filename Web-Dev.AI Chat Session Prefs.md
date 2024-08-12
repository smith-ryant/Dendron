---
id: rjsmkb8su3m21mzhnsika0f
title: AI Chat Session Prefs
desc: ""
updated: 1723430594309
created: 1722965444550
---

My Name is Ryan and I am a web developer student. Below are my general preferences for this chat session and my presentation:

Language and Frameworks: React/JavaScript
Database: Supabase with supabase authentication
Operating System: Mac OS

1. Please be as descriptive and thourough as possible.
2. The more detail the better.
3. When providing code, please provide complete files.
4. Include the relative path as a comment on the first line of each file provided. (This helps me know where the file goes.)
5. Please include todays date & the current time stamp as a comment on the second line of each file provided.
6. Please commit the following current code to memory, so you can help me with this project.
7. Do not provide any information in reference to windows operating system.

This application is called CodeNotes and it allows you to take notes using a markdown editor. Please provide a 500+ word explanation of the application.

Current Code: The following code is for a note taking application called CodeNotes.

```lua
code-notes-app
|-- src/
|   |-- assets
|   |   |-- react.svg
|   |   |-- vite.svg
|   |-- components
|   |   |-- CodeNotes
|   |   |   |--CodeNotes.css
|   |   |   |--CodeNotes.jsx
|   |   |   |--NoteList.css
|   |   |   |--NoteList.jsx
|   |   |-- Header
|   |   |   |-- Header.css
|   |   |   |-- Header.jsx
|   |   |-- Home
|   |   |   |-- Home.css
|   |   |   |-- Home.jsx
|   |   |-- MarkdownEditor
|   |   |   |-- MarkdownEditor.css
|   |   |   |-- MarkdownEditor.jsx
|   |   |-- Spinner
|   |   |   |-- Spinner.css
|   |   |   |-- Spinner.jsx
|   |   |-- store
|   |   |   |-- authContext.jsx
|   |-- App.css
|   |-- App.jsx
|   |-- index.css
|   |-- main.jsx
|   |-- supabaseClient.js
```

```css
/* src/components/CodeNotes/CodeNotes.css */
/* Date & Time: 2024-08-11 @ 18:00 */

/* CSS Variables for Repeated Values */
:root {
  --background-dark: #073642;
  --background-darker: #002b36;
  --text-light: #f0f0f0;
  --border-color: #ccc;
  --button-bg: #00606f;
  --button-hover-bg: #005055;
  --danger-bg: #d9534f;
  --danger-hover-bg: #c9302c;
}

.code-notes-container {
  display: flex;
  height: calc(
    100vh - 80px
  ); /* Subtracting the header height (assuming it's 80px) */
  width: 100vw;
  margin-top: 80px; /* Push content below the header */
  overflow: hidden;
  background-color: #073642; /* Dark background */
}

.notes-list {
  width: 25%;
  background-color: var(--background-darker);
  padding: 20px;
  overflow-y: auto;
  border-right: 1px solid var(--border-color);
  height: 100%;
  box-sizing: border-box;
}

.note-item {
  padding: 10px 0;
  color: var(--text-light);
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.2s;
}

.note-item:hover {
  background-color: #004050;
}

.code-notes-content {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  color: #f0f0f0;
  text-align: left;
  background-color: #073642; /* Dark background */
  overflow-y: hidden; /* Prevent scrolling outside the Markdown editor */
  margin: 0;
}

.code-notes-content h1 {
  margin: 15px 10px 0;
  font-size: 2rem;
  line-height: 1.2;
}

.button-group {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
}

.button-group button {
  flex: 1;
  padding: 10px;
  height: 40px;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
  font-size: 1rem;
  transition: background-color 0.3s;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.add-note-button,
.save-note-button {
  background-color: var(--button-bg);
}

.add-note-button:hover,
.save-note-button:hover {
  background-color: var(--button-hover-bg);
}

.delete-note-button {
  background-color: var(--danger-bg);
}

.delete-note-button:hover {
  background-color: var(--danger-hover-bg);
}

.add-note-button:focus,
.save-note-button:focus,
.delete-note-button:focus {
  outline: none;
}
```

```jsx
// code-notes-app/src/components/CodeNotes/CodeNotes.jsx
// Date and Time: 2024-08-11 18:30:00

import React, { useState, useEffect } from "react";
import NotesList from "./NoteList";
import MarkdownEditor from "../MarkdownEditor/MarkdownEditor";
import { supabase } from "../../supabaseClient";
import Spinner from "../Spinner/Spinner";
import "./CodeNotes.css";

const CodeNotes = () => {
  const [notes, setNotes] = useState([]);
  const [user, setUser] = useState(null);
  const [newNoteContent, setNewNoteContent] = useState("");
  const [newNoteTitle, setNewNoteTitle] = useState("");
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");
  const [selectedNoteId, setSelectedNoteId] = useState(null);

  useEffect(() => {
    const fetchUser = async () => {
      try {
        const {
          data: { user },
          error,
        } = await supabase.auth.getUser();
        if (error) {
          console.error("Error fetching user:", error.message);
        } else {
          console.log("Fetched user:", user);
          setUser(user);
        }
      } catch (error) {
        console.error("Unexpected error fetching user:", error);
      }
    };

    fetchUser();
  }, []);

  useEffect(() => {
    if (user) {
      const fetchNotes = async () => {
        try {
          const { data, error } = await supabase
            .from("notes")
            .select("*")
            .eq("user_id", user.id)
            .order("id", { ascending: true });

          if (error) {
            console.error("Error fetching notes:", error.message);
          } else {
            console.log("Fetched notes:", data);
            setNotes(data);
          }
        } catch (error) {
          console.error("Unexpected error fetching notes:", error);
        }
      };

      fetchNotes();
    }
  }, [user]);

  useEffect(() => {
    const saveToLocalStorage = () => {
      localStorage.setItem("currentNoteTitle", newNoteTitle);
      localStorage.setItem("currentNoteContent", newNoteContent);
    };

    const loadFromLocalStorage = () => {
      setNewNoteTitle(localStorage.getItem("currentNoteTitle") || "");
      setNewNoteContent(localStorage.getItem("currentNoteContent") || "");
    };

    window.addEventListener("beforeunload", saveToLocalStorage);
    window.addEventListener("focus", loadFromLocalStorage);

    return () => {
      window.removeEventListener("beforeunload", saveToLocalStorage);
      window.removeEventListener("focus", loadFromLocalStorage);
    };
  }, [newNoteTitle, newNoteContent]);

  const handleNoteClick = (note) => {
    setNewNoteTitle(note.title);
    setNewNoteContent(note.content);
    setSelectedNoteId(note.id);
  };

  const handleSaveNote = async (event) => {
    event.preventDefault();

    if (!newNoteTitle || !newNoteContent) {
      setError("Both title and content are required.");
      return;
    }

    setLoading(true);
    setError("");

    try {
      if (!user) {
        setError("User not authenticated. Please log in again.");
        setLoading(false);
        return;
      }

      if (selectedNoteId) {
        const { data, error } = await supabase
          .from("notes")
          .update({
            title: newNoteTitle,
            content: newNoteContent,
          })
          .eq("id", selectedNoteId)
          .select("*");

        if (error) {
          console.error("Error updating note:", error.message);
          setError("Error updating note. Please try again.");
        } else {
          setNotes((prevNotes) =>
            prevNotes.map((note) =>
              note.id === selectedNoteId ? data[0] : note
            )
          );
        }
      } else {
        const { data, error } = await supabase
          .from("notes")
          .insert([
            {
              title: newNoteTitle,
              content: newNoteContent,
              user_id: user.id,
            },
          ])
          .select("*");

        if (error) {
          console.error("Error adding note:", error.message);
          setError("Error adding note. Please try again.");
        } else {
          setNotes((prevNotes) => [...prevNotes, data[0]]);
        }
      }

      setNewNoteContent("");
      setNewNoteTitle("");
      setSelectedNoteId(null);
    } catch (error) {
      console.error("Unexpected error saving note:", error);
      setError("Unexpected error. Please try again.");
    } finally {
      setLoading(false);
    }
  };

  const handleDeleteNote = async () => {
    if (!selectedNoteId) {
      setError("No note selected for deletion.");
      return;
    }

    setLoading(true);
    setError("");

    try {
      const { error } = await supabase
        .from("notes")
        .delete()
        .eq("id", selectedNoteId);

      if (error) {
        console.error("Error deleting note:", error.message);
        setError("Error deleting note. Please try again.");
      } else {
        setNotes((prevNotes) =>
          prevNotes.filter((note) => note.id !== selectedNoteId)
        );
        setNewNoteContent("");
        setNewNoteTitle("");
        setSelectedNoteId(null);
      }
    } catch (error) {
      console.error("Unexpected error deleting note:", error);
      setError("Unexpected error. Please try again.");
    } finally {
      setLoading(false);
    }
  };

  const handleAddNote = () => {
    setNewNoteContent("");
    setNewNoteTitle("");
    setSelectedNoteId(null);
  };

  return (
    <div className="code-notes-container">
      <NotesList notes={notes} onNoteClick={handleNoteClick} />
      <div className="code-notes-content">
        <h1>CodeNotes</h1>
        <div className="button-group">
          <button className="add-note-button" onClick={handleAddNote}>
            Add Note
          </button>
          <button
            className="save-note-button"
            onClick={handleSaveNote}
            disabled={loading}
          >
            {loading ? <Spinner /> : "Save Note"}
          </button>
          <button className="delete-note-button" onClick={handleDeleteNote}>
            Delete Note
          </button>
        </div>
        <MarkdownEditor
          content={newNoteContent}
          setContent={setNewNoteContent}
          setTitle={setNewNoteTitle}
        />
        {error && <p className="error-message">{error}</p>}
      </div>
    </div>
  );
};

export default CodeNotes;
```

```css
/* code-notes-app/src/components/CodeNotes/NoteList.css */
/* Date & Time: 2024-08-11 @ 16:10 */

.notes-list {
  width: 25%; /* 25% of the screen */
  background-color: #002b36; /* Dark background */
  padding: 5px;
  overflow-x: auto;
  overflow-y: auto; /* Enable vertical scrolling */
  border-right: 1px solid #ccc; /* Divider line */
  height: calc(100vh - 80px); /* Full height minus header */
  box-sizing: border-box;
}

.note-item {
  padding: 0px 0; /* Reduce padding to bring items closer */
  color: #f0f0f0; /* Light text color */
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.2s;
  border-bottom: none !important; /* Remove bottom border */
  border-top: none !important; /* Remove top border just in case */
  margin-bottom: 0px; /* Small margin between items */
}

.note-item:hover {
  background-color: #004050; /* Slightly darker background on hover */
}

.head-text {
  padding: 3px 0;
  color: #f0f0f0; /* Light text color */
  font-size: 1rem;
  border-bottom: 1px solid #ddd;
  cursor: pointer;
  transition: background-color 0.2s;
}
```

```jsx
// code-notes-app/src/components/CodeNotes/NotesList.jsx
// Date & Time: 2024-08-11 @ 16:00

import React from "react";
import "./NoteList.css";

const NotesList = ({ notes, onNoteClick }) => {
  // Sort the notes alphabetically by title
  const sortedNotes = [...notes].sort((a, b) => a.title.localeCompare(b.title));

  return (
    <div className="notes-list">
      <h2 className="head-text">Notes</h2>
      <ul>
        {sortedNotes.map((note) => (
          <li
            key={note.id}
            className="note-item"
            onClick={() => onNoteClick(note)}
          >
            <strong>{note.title}</strong>
          </li>
        ))}
      </ul>
    </div>
  );
};

export default NotesList;
```

```css
/* code-notes-app/src/components/Header/Header.css */
/* Date & Time: 2024-08-06 @ 21:00 */

/* Header Styling */
.header {
  position: fixed; /* Fix the header at the top */
  top: 0;
  left: 0;
  width: 100%;
  height: 80px;
  background-color: #002b36;
  border-bottom: 2px solid #f0f0f0;
  color: #f0f0f0;
  padding: 0 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  z-index: 1000; /* Ensure the header is above other elements */
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  box-sizing: border-box; /* Include padding in width/height */
}

/* Logo Styling */
.logo {
  height: 30px;
  width: auto; /* Maintain aspect ratio */
  max-height: 30px; /* Constrain max height */
  max-width: 30px; /* Constrain max width */
  margin-right: 20px;
  object-fit: contain; /* Ensure it fits within the set dimensions */
}

/* Ensure specificity */
.logo-title-container .logo {
  height: 30px !important;
  width: auto !important;
  max-height: 30px !important;
  max-width: 30px !important;
  margin-right: 25px;
}

/* Logo and Title Container */
.logo-title-container {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  flex-shrink: 0;
  overflow: hidden; /* Prevent shrinking */
}

/* Logo Styling */
.logo {
  height: 30px;
}

/* Main Navigation */
.main-nav {
  display: flex;
  list-style: none;
  padding: 0;
  margin: 0;
  flex-grow: 1; /* Allow navigation to grow */
  justify-content: flex-end; /* Align links to the right */
  flex-wrap: wrap; /* Wrap links if necessary */
  overflow-x: auto; /* Allow horizontal scrolling if needed */
}

/* Navigation Links */
.main-nav li {
  margin: 0 15px;
}

.main-nav a {
  color: #f0f0f0;
  text-decoration: none;
  transition: 0.3s;
  white-space: nowrap; /* Prevent text wrap */
}

.main-nav a:hover {
  color: #f57145;
}

/* Logout Button */
.logout-btn {
  color: #f0f0f0;
  background: transparent;
  border: 1px solid #002b36;
  border-radius: 5px;
  padding: 5px 15px;
  margin-left: 15px;
  font-size: 1rem;
  cursor: pointer;
  transition: 0.3s;
  white-space: nowrap; /* Prevent text wrap */
}

.logout-btn:hover {
  color: #f57145;
  border-color: #f57145;
}

/* Ensure content below header is visible */
.content {
  padding-top: 100px;
}

/* Responsive Design */
@media (max-width: 768px) {
  .header {
    flex-direction: column;
    align-items: flex-start;
    padding: 10px 20px;
    height: auto;
  }

  .main-nav {
    justify-content: center; /* Center links on smaller screens */
  }

  .main-nav li {
    margin: 10px 0;
  }

  .logout-btn {
    margin-top: 10px;
  }
}

/* Add this CSS to your existing file */

/* Centering the button in the login-container */
.login-container {
  display: flex;
  flex-direction: column; /* Stack children vertically */
  align-items: center; /* Center children horizontally */
  justify-content: center; /* Center children vertically */
  height: 100vh; /* Full viewport height */
  margin: 0 auto; /* Center the container if there's additional horizontal space */
  text-align: center; /* Align text to center */
  max-width: 400px; /* Optional: constrain the max width */
  padding: 20px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  background-color: #004050; /* Optional: Background color for the container */
  border-radius: 10px; /* Optional: Rounded corners */
}

/* Ensure the login button is centered */
form {
  width: 100%;
}

/* Center the button specifically */
.login-btn {
  width: 100%; /* Make the button take full width of its container */
  max-width: 200px; /* Optional: Limit the max width of the button */
  margin: 20px auto; /* Center the button with top and bottom margin */
  padding: 10px;
  background-color: #00606f; /* Your preferred button color */
  border: none;
  border-radius: 5px; /* Rounded corners for the button */
  color: white;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.login-btn:hover {
  background-color: #005055; /* Darker shade on hover */
}

@media (max-width: 768px) {
  .login-container {
    padding: 10px; /* Adjust padding for smaller screens */
    width: 90%; /* Allow more width on smaller screens */
  }

  .login-btn {
    max-width: 100%; /* Allow full width on smaller screens */
  }
}
```

```jsx
// code-notes-app/src/components/Header/Header.jsx
// Date & Time: 2024-08-11 @ 21:00

import React, { useContext } from "react";
import { NavLink, useLocation } from "react-router-dom";
import "./Header.css";
import AuthContext from "../store/authContext";
import logo from "../../assets/react.svg";
import logo2 from "../../assets/vite.svg";
import { supabase } from "../../supabaseClient";

const Header = () => {
  const { state, dispatch } = useContext(AuthContext);
  const location = useLocation();

  const handleLogout = async () => {
    try {
      const { error } = await supabase.auth.signOut();
      if (error) throw error;
      console.log("Logged out successfully");
      dispatch({ type: "LOGOUT" });
    } catch (error) {
      console.error("Logout error:", error.message);
    }
  };

  const styleActiveLink = ({ isActive }) => ({
    color: isActive ? "#f57145" : "#f0f0f0",
  });

  return (
    <header className="header">
      <div className="logo-title-container">
        {/* Link to the React and Vite websites */}
        <a
          href="https://reactjs.org/"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img src={logo} alt="react-logo" className="logo" />
        </a>
        <a href="https://vitejs.dev/" target="_blank" rel="noopener noreferrer">
          <img src={logo2} alt="vite-logo" className="logo" />
        </a>
        <h2>CodeNotes</h2>
      </div>
      <nav>
        <ul className="main-nav">
          <li>
            <NavLink style={styleActiveLink} to="/">
              Home
            </NavLink>
          </li>
          {state.isAuthenticated && location.pathname !== "/codenotes" && (
            <li>
              <NavLink style={styleActiveLink} to="/codenotes">
                CodeNotes
              </NavLink>
            </li>
          )}
        </ul>
      </nav>
    </header>
  );
};

export default Header;
```

```css
/* code-notes-app/src/components/HomePage/Home.css */

/* Main body styling */
body {
  font-family: "Roboto", sans-serif;
  background-color: #073642; /* Dark background for contrast */
  color: #f0f0f0;
  margin: 0;
  display: flex;
  justify-content: center; /* Center contents horizontally */
  align-items: center; /* Center contents vertically */
  height: 100vh; /* Full viewport height */
}

/* Main container for the authentication components */
.auth-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #002b36; /* Background color for the container */
  border-radius: 20px; /* Rounded corners */
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3); /* Increased shadow for depth */
  padding: 40px; /* Space around the container */
  max-width: 400px; /* Maximum width for responsiveness */
  width: 100%; /* Full width within the max-width */
  margin: 20px; /* Center the container vertically if necessary */
}

/* Title styling */
.auth-title {
  font-size: 2rem; /* Large title size */
  margin-bottom: 20px; /* Space below title */
  color: #f0f0f0;
  text-align: center; /* Center text */
}

/* Form styling */
.auth-form {
  width: 100%; /* Full width within the container */
  display: flex;
  flex-direction: column;
  align-items: center; /* Center form contents */
}

/* Input group styling */
.input-group {
  width: 100%; /* Full width for input group */
  margin-bottom: 20px; /* Space between input fields */
}

/* Input field styling */
.input-field {
  width: 100%; /* Full width for inputs */
  padding: 12px;
  font-size: 1rem;
  border: none;
  border-radius: 5px;
  outline: none;
  background-color: #1e1e1e; /* Input background */
  color: #f0f0f0; /* Input text color */
  border: 2px solid #444; /* Border color */
  transition: border-color 0.3s;
  text-align: center; /* Center the text in the input fields */
}

.input-field:focus {
  border-color: #f0f0f0; /* Highlight border on focus */
}

/* Button styling */
.auth-button {
  width: 80%; /* Relative width for buttons */
  padding: 12px;
  background-color: #094554; /* Primary button color */
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3); /* Shadow for depth */
  color: #ffffff;
  border: none;
  border-radius: 5px;
  font-size: 1.1rem;
  font-weight: bold; /* Bold text for button */
  cursor: pointer;
  transition: background-color 0.3s;
  outline: none; /* Remove outline on focus */
  margin-top: 20px; /* Space above the button */
  max-width: 200px; /* Limit the max width to avoid over-stretching */
}

.auth-button:hover {
  background-color: #62767b; /* Darker on hover */
  box-shadow: 0 6px 10px rgba(0, 0, 0, 0.3); /* Enhanced shadow on hover */
}

.auth-button:focus {
  outline: none; /* Remove outline on focus */
}

/* Switch button styling */
.switch-button {
  width: 80%; /* Relative width for buttons */
  padding: 12px;
  background-color: transparent; /* Transparent background for contrast */
  box-shadow: none; /* No shadow for secondary button */
  color: #f57145;
  border: 1px solid #f57145; /* Border to match text color */
  border-radius: 5px;
  font-size: 0.9rem;
  font-weight: bold; /* Bold text for button */
  cursor: pointer;
  transition: background-color 0.3s, color 0.3s;
  margin-top: 15px; /* Space above the button */
  max-width: 200px; /* Limit the max width */
  text-align: center; /* Center text */
  text-decoration: none; /* Remove text underline */
}

.switch-button:hover {
  background-color: #f57145; /* Darker on hover */
  color: #ffffff; /* Change text color on hover */
}

.switch-button:focus {
  outline: none; /* Remove outline on focus */
}

/* Message styling */
.auth-message {
  margin-top: 20px;
  color: #f57145; /* Color for messages */
  font-size: 1rem;
  text-align: center;
  font-weight: bold; /* Emphasize message */
}
```

```jsx
// code-notes-app/src/components/HomePage/Home.jsx
// Date and Time: 2024-08-07 22:00:00

import React, { useState, useEffect } from "react";
import { useAuth } from "../store/authContext";
import "./Home.css";
import Spinner from "../Spinner/Spinner";
import { useNavigate } from "react-router-dom";

const Home = () => {
  const { state, login, register, logout } = useAuth();
  const [isLogin, setIsLogin] = useState(true);
  const [username, setUsername] = useState("");
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [message, setMessage] = useState("");
  const [loading, setLoading] = useState(false);
  const navigate = useNavigate();

  const toggleAuthMode = () => {
    setIsLogin(!isLogin);
    setUsername("");
    setEmail("");
    setPassword("");
    setMessage("");
  };

  const validateEmail = (email) => {
    const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return re.test(email);
  };

  const validatePassword = (password) => {
    return password.length >= 8;
  };

  const handleSubmit = async (e) => {
    e.preventDefault();

    if (!validateEmail(email)) {
      setMessage("Invalid email format.");
      return;
    }

    if (!validatePassword(password)) {
      setMessage("Password must be at least 8 characters.");
      return;
    }

    setLoading(true);
    setMessage("");
    console.log("Form submitted:", { email, isLogin });

    try {
      if (isLogin) {
        const result = await login(email, password);
        if (result.success) {
          console.log("Login successful:", email);
          setMessage("Login successful!");
          setTimeout(() => {
            setMessage("");
            navigate("/codenotes");
          }, 1000);
        }
      } else {
        const result = await register(email, password, username);
        if (result.success) {
          console.log("Registration successful:", email);
          setMessage("Sign up successful! Please log in.");
          setUsername("");
          setEmail("");
          setPassword("");
          setIsLogin(true);
        }
      }
    } catch (error) {
      setMessage(`Error: ${error.message}`);
      console.error("Submission error:", error.message);
    } finally {
      setLoading(false);
      console.log("Finished login/register process");
    }
  };

  const handleLogout = async () => {
    await logout();
    setMessage("You have been logged out.");
    navigate("/"); // Ensure we navigate to the home page on logout
  };

  useEffect(() => {
    if (state.isAuthenticated) {
      console.log(
        "User is authenticated, stopping spinner and showing logout."
      );
      setLoading(false);
      if (state.userProfile?.username) {
        setMessage(`Welcome, ${state.userProfile.username}!`);
      } else {
        setMessage(`Welcome, ${email}!`);
      }
    } else {
      console.log("User is not authenticated, showing login/signup form.");
    }
  }, [state.isAuthenticated, state.userProfile, email]);

  return (
    <div className="auth-container">
      <h1 className="auth-title">
        {state.isAuthenticated
          ? `Welcome, ${state.userProfile?.username || "Back!"}`
          : isLogin
          ? "Welcome Back!"
          : "Create An Account"}
      </h1>
      {!state.isAuthenticated ? (
        <form className="auth-form" onSubmit={handleSubmit}>
          {!isLogin && (
            <div className="input-group">
              <input
                className="input-field"
                type="text"
                placeholder="Username"
                value={username}
                onChange={(e) => setUsername(e.target.value)}
                required
              />
            </div>
          )}
          <div className="input-group">
            <input
              className="input-field"
              type="email"
              placeholder="Email"
              value={email}
              onChange={(e) => setEmail(e.target.value)}
              required
            />
          </div>
          <div className="input-group">
            <input
              className="input-field"
              type="password"
              placeholder="Password"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
              required
            />
          </div>
          <button type="submit" className="auth-button" disabled={loading}>
            {loading ? <Spinner /> : isLogin ? "Login" : "Sign Up"}
          </button>
        </form>
      ) : (
        <div>
          <button onClick={handleLogout} className="auth-button">
            Logout
          </button>
        </div>
      )}

      {message && !state.isAuthenticated && (
        <p className="auth-message">{message}</p>
      )}

      {!state.isAuthenticated && (
        <button onClick={toggleAuthMode} className="switch-button">
          {isLogin ? "Need to Register?" : "Switch to Login"}
        </button>
      )}
    </div>
  );
};

export default Home;
```

```css
/* code-notes-app/src/components/MarkdownEditor/MarkdownEditor.css */
/* Date & Time: 2024-08-11 @ 22:00 */

.markdown-editor {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  height: 100%; /* Full height of the parent */
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow-y: scroll;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  background-color: #002b36;
}

.react-markdown-editor-lite .md-editor {
  display: flex;
  flex-direction: column;
  height: 100%; /* Full height within the markdown-editor container */
}

.react-markdown-editor-lite .md-editor .md-editor-area {
  background-color: #073642 !important;
  color: #f0f0f0 !important;
  flex-grow: 1;
  min-height: 0;
  overflow-y: auto; /* Allow scrolling when content overflows */
}

.react-markdown-editor-lite .md-editor .md-editor-area textarea {
  background-color: #073642 !important;
  color: #f0f0f0 !important;
  border: none;
  height: 100%; /* Full height of the editor */
}

.react-markdown-editor-lite .md-editor-toolbar {
  background-color: #002b36 !important;
  color: #f0f0f0 !important;
}

.react-markdown-editor-lite .md-editor-toolbar .button {
  color: #f0f0f0 !important;
}

.react-markdown-editor-lite .md-editor .md-preview {
  background-color: #073642 !important;
  color: #f0f0f0 !important;
  flex-grow: 1;
  overflow-y: auto; /* Allow scrolling in the preview */
}
```

```jsx
// code-notes-app/src/components/MarkdownEditor/MarkdownEditor.jsx
// Date & Time: 2024-08-11 @ 22:00

import React, { useEffect } from "react";
import MarkdownIt from "markdown-it";
import MdEditor from "react-markdown-editor-lite";
import "react-markdown-editor-lite/lib/index.css";
import "./MarkdownEditor.css";

const mdParser = new MarkdownIt(/* Markdown-it options */);

const MarkdownEditor = ({ content, setContent, setTitle }) => {
  const handleEditorChange = ({ text }) => {
    setContent(text);

    // Set the title based on the first line of the content
    const firstLine = text.split("\n")[0];
    setTitle(firstLine || ""); // Set title to the first line or empty if not available
  };

  useEffect(() => {
    if (!content) {
      // Add placeholder text if content is empty
      setContent("# Enter your note title here\n\nYour note content...");
    }
  }, [content, setContent]);

  return (
    <div className="markdown-editor">
      <MdEditor
        value={content}
        style={{ flexGrow: 1 }} // Ensure it fills the container
        renderHTML={(text) => mdParser.render(text)}
        onChange={handleEditorChange}
        placeholder="Enter your Markdown note here..."
      />
    </div>
  );
};

export default MarkdownEditor;
```

```css
/* src/components/Spinner/Spinner.css */
/* Date and Time: 2024-08-06 10:30:00 */

.spinner {
  border: 8px solid #f3f3f3;
  border-top: 8px solid #3498db;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  animation: spin 1s linear infinite;
  margin: auto;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
```

```jsx
// src/components/Spinner/Spinner.jsx
// Date and Time: 2024-08-06 10:30:00

import React from "react";
import "./Spinner.css";

const Spinner = () => {
  return <div className="spinner"></div>;
};

export default Spinner;
```

```jsx
// code-notes-app/src/components/store/authContext.jsx
// Date and Time: 2024-08-11 20:45:00

import React, { createContext, useReducer, useContext, useEffect } from "react";
import { supabase } from "../../supabaseClient";

const AuthContext = createContext();

const initialState = {
  userProfile: null,
  token: null,
  isAuthenticated: false,
};

const authReducer = (state, action) => {
  switch (action.type) {
    case "LOGIN":
      return {
        ...state,
        token: action.payload.token,
        userProfile: action.payload.userProfile,
        isAuthenticated: true,
      };
    case "LOGOUT":
      return {
        ...state,
        token: null,
        userProfile: null,
        isAuthenticated: false,
      };
    default:
      return state;
  }
};

export const AuthProvider = ({ children }) => {
  const [state, dispatch] = useReducer(authReducer, initialState);

  const login = async (email, password) => {
    try {
      console.log("Attempting to login user:", email);

      const { data, error } = await supabase.auth.signInWithPassword({
        email,
        password,
      });

      if (error) {
        console.error("Login error:", error.message);
        throw new Error(`Login error: ${error.message}`);
      }

      const user = data.user;
      if (!user) {
        console.error("Login failed, no user returned.");
        throw new Error("Login failed, no user returned.");
      }

      console.log("User logged in successfully:", user);

      // Simplified version without fetching user profile
      dispatch({
        type: "LOGIN",
        payload: { token: user.access_token, userProfile: null },
      });

      console.log(
        "User token dispatched successfully. User is now authenticated."
      );

      return { success: true };
    } catch (err) {
      console.error(`Login failed: ${err.message}`);
      throw err;
    }
  };

  const logout = async () => {
    try {
      const { error } = await supabase.auth.signOut();
      if (error) throw error;
      dispatch({ type: "LOGOUT" });
      console.log("User logged out successfully");
    } catch (error) {
      console.error("Logout error:", error.message);
    }
  };

  useEffect(() => {
    const checkUser = async () => {
      try {
        const {
          data: { user },
          error,
        } = await supabase.auth.getUser();

        if (error) {
          console.error("Error checking user:", error.message);
          return;
        }

        if (user) {
          console.log("User detected on initial load:", user);
          dispatch({
            type: "LOGIN",
            payload: { token: user.access_token, userProfile: null },
          });
        } else {
          console.log("No user session found on initial load.");
        }
      } catch (err) {
        console.error("Unexpected error checking user:", err.message);
      }
    };

    checkUser();

    const { data: authListener } = supabase.auth.onAuthStateChange(
      async (event, session) => {
        console.log(`Auth state changed: ${event}`);
        if (event === "SIGNED_IN" && session) {
          dispatch({
            type: "LOGIN",
            payload: { token: session.access_token, userProfile: null },
          });
        } else if (event === "SIGNED_OUT") {
          dispatch({ type: "LOGOUT" });
        }
      }
    );

    const handleFocus = async () => {
      const {
        data: { user },
        error,
      } = await supabase.auth.getUser();
      if (error || !user) {
        console.error("User session expired or not found:", error?.message);
        dispatch({ type: "LOGOUT" });
      } else {
        dispatch({
          type: "LOGIN",
          payload: { token: user.access_token, userProfile: null },
        });
      }
    };

    window.addEventListener("focus", handleFocus);

    // Listen for page unload or close to clear auth state
    const handleBeforeUnload = () => {
      logout(); // Automatically log out
    };

    window.addEventListener("beforeunload", handleBeforeUnload);

    return () => {
      if (authListener) {
        authListener.subscription.unsubscribe();
      }
      window.removeEventListener("focus", handleFocus);
      window.removeEventListener("beforeunload", handleBeforeUnload);
    };
  }, []);

  return (
    <AuthContext.Provider value={{ state, dispatch, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => {
  const context = useContext(AuthContext);
  if (context === undefined) {
    throw new Error("useAuth must be used within an AuthProvider");
  }
  return context;
};

export default AuthContext;
```

```jsx
// code-notes-app/src/App.jsx
// Date and Time: 2024-08-07 19:55:00

import React from "react";
import {
  BrowserRouter as Router,
  Route,
  Routes,
  Navigate,
} from "react-router-dom";
import { AuthProvider, useAuth } from "./components/store/authContext";
import Home from "./components/HomePage/Home";
import CodeNotes from "./components/CodeNotes/CodeNotes"; // Import the CodeNotes component
import Header from "./components/Header/Header";

const ProtectedRoute = ({ children }) => {
  const { state } = useAuth();
  return state.isAuthenticated ? children : <Navigate to="/" />;
};

function App() {
  return (
    <AuthProvider>
      <Router>
        <div className="App">
          <Header />
          <Routes>
            <Route path="/" element={<Home />} />
            <Route
              path="/codenotes"
              element={
                <ProtectedRoute>
                  <CodeNotes />
                </ProtectedRoute>
              }
            />
            <Route path="*" element={<Navigate to="/" />} />{" "}
            {/* Catch-all route */}
          </Routes>
        </div>
      </Router>
    </AuthProvider>
  );
}

export default App;
```

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { AuthProvider } from "./components/store/authContext.jsx";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <AuthProvider>
      <App />
    </AuthProvider>
  </React.StrictMode>
);
```

```js
// code-notes-app/src/supabaseClient.js
// Date and Time: 2024-08-11 18:30:00

import { createClient } from "@supabase/supabase-js";

const supabaseUrl = import.meta.env.VITE_SUPABASE_URL;
const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY;

if (!supabaseUrl || !supabaseAnonKey) {
  throw new Error("Supabase URL or Anon Key not set in environment variables.");
}

export const supabase = createClient(supabaseUrl, supabaseAnonKey, {
  auth: {
    persistSession: true, // Enable session persistence
    autoRefreshToken: true, // Enable auto-refresh of session tokens
  },
});

console.log("Supabase client initialized:", supabaseUrl);
```
