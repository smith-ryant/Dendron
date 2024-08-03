---
id: 4b5812x2cjcxzd2cqjp6sus
title: Capstone
desc: ""
updated: 1722636301016
created: 1722447852209
---

### Supabase

Specs-Capstone
password: Rts@52c8dfe2

project URL: https://ngygafxkmmautarqouqr.supabase.co
Project anon key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im5neWdhZnhrbW1hdXRhcnFvdXFyIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MjI0NDc4MDksImV4cCI6MjAzODAyMzgwOX0.cxKkX8hS7kFMwyvDIVOsxelXs_RO2m37v2bdaZwAvx8

This was going to be an airplane viewer, but I am not going to be able to finish.

Backend:

1. **./util/database.js:**

This file likely contains the configuration and initialization of the Sequelize instance, which is used to interact with the database. It might include the database connection details and any necessary setup for Sequelize.

2. **./models/user.js:**

This file defines the User model using Sequelize. It specifies the structure of the User table in the database, including the fields and their data types, as well as any associations or relationships with other models.

3. **./models/post.js:**

Similar to user.js, this file defines the Post model. It outlines the structure of the Post table, including its fields and data types, and any associations with other models, such as the relationship with the User model.

4. **./controllers/posts.js:**

This file contains the controller functions for handling post-related operations. These functions include getAllPosts, getCurrentUserPosts, addPost, editPost, and deletePost. Each function corresponds to a specific route and handles the logic for interacting with the Post model.

5. **./controllers/auth.js:**

This file includes the controller functions for authentication, specifically register and login. These functions handle user registration and login processes, including creating new users and validating user credentials.

6. **./middleware/isAuthenticated.js:**

This file defines middleware that checks if a user is authenticated before allowing access to certain routes. The isAuthenticated function is used to protect routes that require the user to be logged in, ensuring that only authenticated users can perform certain actions.
These files work together to create a full-featured Express application with user authentication, post management, and database interactions using Sequelize.
