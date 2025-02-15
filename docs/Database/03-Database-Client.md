---
id: database-client
title: Database Client
sidebar_label: Database Client
---

# Database Client

This document provides information about the Database Client used in the project. The Database Client is responsible for managing connections to the database, executing queries, and handling transactions.

## Features

- Connection pooling
- Query execution
- Transaction management
- Error handling

## Configuration

To configure the Database Client, you need to set the following environment variables:

- `DB_HOST`: The hostname of the database server.
- `DB_PORT`: The port number on which the database server is listening.
- `DB_USER`: The username to connect to the database.
- `DB_PASSWORD`: The password to connect to the database.
- `DB_NAME`: The name of the database to connect to.

## Usage

Here is an example of how to use the Database Client in your application:

```javascript
const dbClient = require("path-to-db-client");

// Connect to the database
dbClient.connect();

// Execute a query
dbClient.query("SELECT * FROM users", (err, result) => {
  if (err) {
    console.error("Error executing query", err);
  } else {
    console.log("Query result", result);
  }
});

// Disconnect from the database
dbClient.disconnect();
```
