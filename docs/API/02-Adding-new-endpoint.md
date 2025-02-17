# Adding new endpoint

# New Endpoints

The API exposes various endpoints for interacting with the backend.

## 1. **Public Endpoints**
### `GET /api/hello`
Returns a simple greeting message.

**Request:**
```ts
app.get('/hello', (c) => {
  return c.json({ message: 'Hello from Hono API!' });
});
