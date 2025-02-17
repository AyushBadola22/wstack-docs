# Protected Routes

Some API routes require user authentication to access.

## Middleware-Based Protection

We use the `authMiddleware` to enforce authentication for specific routes.

### **Middleware: `authMiddleware`**

Located at `src/server/middlewares/auth-middleware.ts`, this middleware ensures that only authenticated users can access protected routes.

### **Applying Middleware**

To apply authentication to an endpoint, attach `authMiddleware` to the route definition:

```ts
app.get("/protected", authMiddleware, (c) => {
  const user: any = c.get("user");
  return c.json({ message: "Protected API Data", name: user.name });
});
