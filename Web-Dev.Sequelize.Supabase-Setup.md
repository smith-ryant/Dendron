---
id: s2ibxvkhnwrqqk76fakqotu
title: Supabase-Setup
desc: ""
updated: 1722458486598
created: 1719163012895
---

### Step 1: Setting Up Supabase

1. **Create a Supabase Account and Project**

   - Go to [Supabase](https://supabase.io/).
   - Sign up and create a new project.
   - Note the `API URL` and `anon key` from the project settings.

2. **Create the `userProfile` Table**

   - Navigate to the SQL editor in the Supabase dashboard.
   - Run the following SQL query to create the `userProfile` table:

     ```sql
     CREATE TABLE userProfile (
         id serial PRIMARY KEY,
         username varchar(255) NOT NULL,
         email varchar(255) UNIQUE NOT NULL,
         created_at timestamp with time zone DEFAULT now()
     );
     ```

### Step 2: Setting Up the Backend with Express and Sequelize

1. **Initialize a Node.js Project**

   - Open your terminal.
   - Navigate to your project directory and run the following commands:

     ```sh
     mkdir supabase-react-backend
     cd supabase-react-backend
     npm init -y
     ```

2. **Install Dependencies**

   - Install Express, Sequelize, and other necessary packages:

     ```sh
     npm install express sequelize pg pg-hstore dotenv
     ```

3. **Setup Sequelize**

   - Create a `.env` file in your project root and add your Supabase database credentials:

     ```env
     DB_HOST=supabase-db-host
     DB_NAME=supabase-db-name
     DB_USER=supabase-db-user
     DB_PASSWORD=supabase-db-password
     DB_PORT=5432
     ```

   - Initialize Sequelize:

     ```sh
     npx sequelize-cli init
     ```

   - Configure `config/config.json`:

     ```json
     {
       "development": {
         "username": process.env.DB_USER,
         "password": process.env.DB_PASSWORD,
         "database": process.env.DB_NAME,
         "host": process.env.DB_HOST,
         "dialect": "postgres"
       }
     }
     ```

4. **Create the `userProfile` Model**

   - Generate the model for `userProfile`:

     ```sh
     npx sequelize-cli model:generate --name userProfile --attributes username:string,email:string,created_at:date
     ```

   - Update the generated migration file in `migrations/` to match the Supabase table definition:

     ```js
     "use strict";
     module.exports = {
       up: async (queryInterface, Sequelize) => {
         await queryInterface.createTable("userProfiles", {
           id: {
             allowNull: false,
             autoIncrement: true,
             primaryKey: true,
             type: Sequelize.INTEGER,
           },
           username: {
             type: Sequelize.STRING,
             allowNull: false,
           },
           email: {
             type: Sequelize.STRING,
             unique: true,
             allowNull: false,
           },
           created_at: {
             allowNull: false,
             type: Sequelize.DATE,
             defaultValue: Sequelize.literal("CURRENT_TIMESTAMP"),
           },
         });
       },
       down: async (queryInterface, Sequelize) => {
         await queryInterface.dropTable("userProfiles");
       },
     };
     ```

   - Run the migration to create the table:

     ```sh
     npx sequelize-cli db:migrate
     ```

5. **Setup Express Server**

   - Create a new file `server.js` and add the following code:

     ```js
     const express = require("express");
     const { Sequelize, DataTypes } = require("sequelize");
     require("dotenv").config();

     const app = express();
     const port = 3001;

     // Database connection
     const sequelize = new Sequelize(
       process.env.DB_NAME,
       process.env.DB_USER,
       process.env.DB_PASSWORD,
       {
         host: process.env.DB_HOST,
         dialect: "postgres",
       }
     );

     // Test connection
     sequelize
       .authenticate()
       .then(() => console.log("Connection has been established successfully."))
       .catch((err) =>
         console.error("Unable to connect to the database:", err)
       );

     // Define userProfile model
     const userProfile = sequelize.define(
       "userProfile",
       {
         username: {
           type: DataTypes.STRING,
           allowNull: false,
         },
         email: {
           type: DataTypes.STRING,
           unique: true,
           allowNull: false,
         },
         created_at: {
           type: DataTypes.DATE,
           defaultValue: Sequelize.literal("CURRENT_TIMESTAMP"),
           allowNull: false,
         },
       },
       {
         timestamps: false,
       }
     );

     // Routes
     app.get("/userProfiles", async (req, res) => {
       const users = await userProfile.findAll();
       res.json(users);
     });

     // Start server
     app.listen(port, () => {
       console.log(`Server is running on http://localhost:${port}`);
     });
     ```

### Step 3: Setting Up the Frontend with React

1. **Create a React App**

   - In your terminal, navigate to your projects directory and run:

     ```sh
     npx create-react-app supabase-react-frontend
     cd supabase-react-frontend
     ```

2. **Install Axios**

   - To make HTTP requests to your Express server:

     ```sh
     npm install axios
     ```

3. **Fetch Data from Backend**

   - In `src/App.js`, add the following code to fetch and display data from your backend:

     ```jsx
     import React, { useEffect, useState } from "react";
     import axios from "axios";

     function App() {
       const [users, setUsers] = useState([]);

       useEffect(() => {
         axios
           .get("http://localhost:3001/userProfiles")
           .then((response) => {
             setUsers(response.data);
           })
           .catch((error) => {
             console.error("There was an error fetching the data!", error);
           });
       }, []);

       return (
         <div className="App">
           <h1>User Profiles</h1>
           <ul>
             {users.map((user) => (
               <li key={user.id}>
                 {user.username} - {user.email}
               </li>
             ))}
           </ul>
         </div>
       );
     }

     export default App;
     ```

### Step 4: Running the Application

1. **Start the Backend**

   - In the `supabase-react-backend` directory, run:

     ```sh
     node server.js
     ```

2. **Start the Frontend**

   - In the `supabase-react-frontend` directory, run:

     ```sh
     npm start
     ```

### Step 5: Testing the Application

- Open your browser and go to `http://localhost:3000`.
- You should see the list of user profiles fetched from your Supabase database displayed in your React application.

This consolidated setup should provide a comprehensive guide to get you started with Supabase, React, Sequelize, and Express. Let me know if you need any further assistance!
