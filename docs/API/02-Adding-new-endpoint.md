# Adding a New Endpoint to the API

## Overview

This guide will walk you through adding a new API endpoint using the Hono framework for your server-side application. Follow the steps below to create new routes and handle API requests efficiently.

### Steps to Add a New Endpoint

#### 1. **Navigate to the `routes/api.ts` File**

The primary location for defining your API routes is in the `server/routes/api.ts` file. This is where all core API endpoints should be defined.

#### 2. **Define the New Route**

Use Hono’s routing methods (`app.get`, `app.post`, `app.put`, etc.) to define a new route. Each route corresponds to an HTTP method and a URL pattern.

#### 3. **Implement Logic in the Handler Function**

In the handler function, implement the necessary logic to process the request. You can access request data, query parameters, headers, and more.

#### 4. **Return a JSON Response**

Ensure that your endpoint responds with a JSON object, especially for API responses. Hono's context (`c`) makes it easy to return structured JSON responses.

## Creating a New Router File

If your application grows and you need to organize your routes better, you can create a new file for each module (e.g., routes/users.ts). This can help maintain a clean structure as the project expands.

### Steps to create a new router file

#### 1. **Create a new file**

In the server/routes/ directory. For example, you can create server/routes/users.ts for user-related routes.

#### 2. **Define your routes**

using Hono’s routing methods (app.get, app.post, etc.) in the new file.

#### 3. **Import and use the new router**

 in the main server configuration file (e.g., server.ts).


### Example of creating a ` Users ` router

Create a file, `server/routes/users.ts`, where you define routes related to user management:

```ts
import { Hono } from 'hono';

const app = new Hono();

app.get('/api/users', (c) => {
  // Logic to retrieve all users
  const users = getAllUsers();  // Assume this function fetches user data
  return c.json(users);  // Return the response as JSON
});

export default app;
```

Then, ensure that the `users.ts` router is imported and used in the main server setup `server.ts`

File: ` server.ts `

```ts
import { Hono } from 'hono';
import users from './routes/users.ts'

const app = new Hono();

app.router('/api/users', users);

export default app;
```

You can also define a router file for defining all the routes and then importing the file in `server.ts`. For more best 
practices regarding hono you can refer to their official docs [Hono Best Practices](https://hono.dev/docs/guides/best-practices).