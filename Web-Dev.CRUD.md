---
id: n7sm7e1e113qqkzlb0feyxq
title: CRUD
desc: ""
updated: 1722784441898
created: 1722784320485
---

CRUD is an acronym that stands for **Create, Read, Update, and Delete**. These are the four basic operations that can be performed on data in a database or any other data storage system. Here's a brief overview of each operation:

1. **Create:** This operation involves adding new data or records to the database. For example, adding a new user to a user database.

2. **Read:** This operation involves retrieving or reading data from the database. For example, fetching the details of a specific user or listing all users in the database.

3. **Update:** This operation involves modifying existing data in the database. For example, updating a user's email address or changing their password.

4. **Delete:** This operation involves removing data from the database. For example, deleting a user from the user database.

CRUD operations are fundamental to many applications and are often implemented using SQL (Structured Query Language) in relational databases. Here's a quick look at how CRUD operations might be implemented in SQL:

- **Create:**

  ```sql
  INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');
  ```

- **Read:**

  ```sql
  SELECT * FROM users WHERE id = 1;
  ```

- **Update:**

  ```sql
  UPDATE users SET email = 'newemail@example.com' WHERE id = 1;
  ```

- **Delete:**
  ```sql
  DELETE FROM users WHERE id = 1;
  ```

In web development, CRUD operations are often mapped to HTTP methods in RESTful APIs:

- **POST** -> Create
- **GET** -> Read
- **PUT/PATCH** -> Update
- **DELETE** -> Delete

CRUD is a fundamental concept in software development, especially for applications that interact with databases, as it provides a basic framework for handling data.
