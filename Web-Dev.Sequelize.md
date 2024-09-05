---
id: i20ob1vg4bcd8mtrgaem3je
title: Sequelize
desc: "A primer for setting up Sequelize"
updated: 1719162641939
created: 1719160243651
---

## Sequelize (PostgreSQL)

To modify the code to use a PostgreSQL database instead of SQLite or MySQL, you need to change the Sequelize instance creation to connect to a PostgreSQL database. You'll also need to ensure that you have the PostgreSQL driver (`pg` and `pg-hstore`) installed.

First, install the necessary packages if you haven't already:

```bash
npm install pg pg-hstore
```

Then, update the code as follows:

```javascript
const { Sequelize, Model, DataTypes } = require("sequelize");
const sequelize = new Sequelize("database_name", "username", "password", {
  host: "localhost",
  dialect: "postgres",
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
  await sequelize.sync({ force: true });
  // Code here
})();
```

Here are the key changes:

1. **Creating a new Sequelize instance with PostgreSQL connection details:**
   ```javascript
   const sequelize = new Sequelize("database_name", "username", "password", {
     host: "localhost",
     dialect: "postgres",
   });
   ```
   - Replace `'database_name'` with the name of your PostgreSQL database.
   - Replace `'username'` with your PostgreSQL username.
   - Replace `'password'` with your PostgreSQL password.
   - Replace `'localhost'` with your PostgreSQL server host if it's different.

## This configuration tells Sequelize to use the PostgreSQL dialect and connects to the specified database using the provided credentials. The rest of the code remains the same and works the same way as it did with SQLite and MySQL.

---

## Sequelize (mysql)

To modify the code to use a MySQL database, you need to change the Sequelize instance creation to connect to a MySQL database. You'll also need to ensure that you have the MySQL driver (`mysql2`) installed.

First, install the `mysql2` package if you haven't already:

```bash
npm install mysql2
```

Then, update the code as follows:

```javascript
const { Sequelize, Model, DataTypes } = require("sequelize");
const sequelize = new Sequelize("database_name", "username", "password", {
  host: "localhost",
  dialect: "mysql",
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
  await sequelize.sync({ force: true });
  // Code here
})();
```

Here are the key changes:

1. **Creating a new Sequelize instance with MySQL connection details:**
   ```javascript
   const sequelize = new Sequelize("database_name", "username", "password", {
     host: "localhost",
     dialect: "mysql",
   });
   ```
   - Replace `'database_name'` with the name of your MySQL database.
   - Replace `'username'` with your MySQL username.
   - Replace `'password'` with your MySQL password.
   - Replace `'localhost'` with your MySQL server host if it's different.

This configuration tells Sequelize to use the MySQL dialect and connects to the specified database using the provided credentials. The rest of the code remains the same and works the same way as it did with SQLite.

1. Install Sequelize

```bash
npm install --save sequelize
```

2. Connect to a mysql database
   `database.js`

```js
Const Sequelize = require('sequelize');

const sequelize = new Sequelize('NameOfDatabase', 'UserName', 'Password', {dialect: 'mysql', host: 'localhost'

});

module.exports = sequelize;
```

2. Create a model

```js
const Sequelize = require("sequelize");

const sequelize = require("../util/database");

const Product = sequelize.define("product", {
  id: {
    type: Sequelize.INTEGER,
  },
});
```
