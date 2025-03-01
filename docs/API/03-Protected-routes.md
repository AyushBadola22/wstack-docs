# Protected Routes

Hono has built-in support for [middlewares](https://hono.dev/docs/guides/middleware), which are functions that can be used to modify the context or execute code before or after a route handler is executed.

That's how we can secure our API endpoints from unauthorized access. Below are some examples of you can leverage middlewares to protect your API routes.

## Authenticated access

After validating the user's authentication status using next-auth, it automatically stores the user data in sessions object. This allows us to access the user's information in subsequent middleware and procedures without having to re-validate the session.

We have already provided with a auth middleware which yo can find at `server/middlewares/auth-middleware.ts` which provides with basic authenticated access.

```ts
import type { Context, Next } from 'hono'
import { auth } from '@/lib/auth'
import { log } from '@/lib/logger'

export const authMiddleware = async (c: Context, next: Next) => {
    try {
        const session = await auth();

        if (!session) {
            return c.json({ error: 'Unauthorized' }, 401)
        }

        c.set('user', session.user) // Attach user data to context
        await next()
    } catch (err) {
        console.error('Error in auth middleware:', err)
        log("error", "Error in auth middleware: " + err)
        return c.json({ error: 'Internal server error' }, 500)
    }
}
```


### **Applying Middleware**

To apply authentication to an endpoint, attach `authMiddleware` to the route definition:

```ts
app.get("/protected", authMiddleware, (c) => {
  const user: any = c.get("user");
  return c.json({ message: "Protected API Data", name: user.name });
});
```

## Feature-based access

To implement feature-based access, such as role-based access control (RBAC), you can define a middleware that checks the user's role before allowing access to certain routes.

Here's an example of how you can create a role-based access middleware:

```ts
import type { Context, Next } from 'hono'

export const roleMiddleware = (requiredRole: string) => {
  return async (c: Context, next: Next) => {
    const user: any = c.get('user')

    if (!user || user.role !== requiredRole) {
      return c.json({ error: 'Forbidden' }, 403)
    }

    await next()
  }
}
```

### **Applying Role-Based Middleware**

To apply role-based access control to an endpoint, attach `roleMiddleware` with the required role to the route definition:

```ts
app.get("/admin", authMiddleware, roleMiddleware('admin'), (c) => {
  return c.json({ message: "Admin API Data" });
});
```

In this example, only users with the role `admin` will be able to access the `/admin` route.

