---
id: s2ibxvkhnwrqqk76fakqotu
title: Supabase-Setup
desc: ""
updated: 1719165121427
created: 1719163012895
---

To set up a Supabase database and use it with Sequelize, along with using `dotenv` to manage environment variables, follow these steps:

1. **Create a Supabase Project:**

   - Go to [Supabase](https://supabase.io/) and sign in or sign up.
   - Create a new project by providing a project name, selecting a database region, and creating a strong password.

2. **Get Your Database Connection Details:**

   - Once the project is created, go to the "Settings" tab in your project dashboard.
   - Under "Database", you'll find the connection string that looks something like this:
     ```
     postgresql://username:password@host:port/database_name
     ```

3. **Install Necessary Packages:**
   Ensure you have the necessary packages installed for Sequelize, PostgreSQL, and dotenv:

   ```bash
   npm install sequelize pg pg-hstore dotenv
   ```

4. **Create a `.env` File:**
   Create a `.env` file in the root directory of your project and add your Supabase connection details to it:

   ```env
   DATABASE_URL=postgresql://username:password@host:port/database_name
   ```

5. **Update Your Code to Use Supabase and dotenv:**
   Modify your existing Sequelize setup to use the connection details from the `.env` file. Here’s how you can do it:

```javascript
require("dotenv").config(); // Load environment variables from .env file
const { Sequelize, DataTypes } = require("sequelize");

// Use the DATABASE_URL from the .env file
const sequelize = new Sequelize(process.env.DATABASE_URL, {
  dialect: "postgres",
  protocol: "postgres",
  logging: false, // Disable logging; default: console.log
});

const User = sequelize.define("user", {
  name: DataTypes.TEXT,
  favoriteColor: {
    type: DataTypes.TEXT,
    defaultValue: "green",
  },
  age: DataTypes.INTEGER,
  cash: DataTypes.INTEGER,
});

(async () => {
  try {
    await sequelize.authenticate();
    console.log("Connection has been established successfully.");
    await sequelize.sync({ force: true });
    // Code here
  } catch (error) {
    console.error("Unable to connect to the database:", error);
  }
})();
```

**Key points to note:**

- **Environment Variables:**
  Using `dotenv`, the connection details are stored in a `.env` file and accessed via `process.env.DATABASE_URL`. This keeps your credentials secure and makes it easier to manage different environments (development, production, etc.).

- **Sequelize Configuration:**
  The Sequelize instance is configured using the database URL from the `.env` file. The `dialect: 'postgres'` and `protocol: 'postgres'` ensure Sequelize uses PostgreSQL as the database dialect.

- **Error Handling:**
  The try-catch block handles errors during the connection and synchronization process.

By following these steps, you'll have your Sequelize models set up and connected to your Supabase PostgreSQL database, with environment variables managed by `dotenv`.
