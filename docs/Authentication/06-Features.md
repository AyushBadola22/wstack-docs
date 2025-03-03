---
id: features
title: Features
sidebar_label: Features
---

# Features

NextAuth.js provides a wide range of features to handle authentication in your Next.js application. This guide covers protecting routes, accessing user sessions, and exploring advanced features like custom adapters, callbacks, and theming.

---

## 1. Protecting Routes

To ensure that only authenticated users can access certain pages, you can protect routes using the `useSession` hook or server-side session handling.

### Example: Protect a Dashboard Page

Here’s how to protect a dashboard page so that only authenticated users can access it:

#### Client-Side Protection

```javascript
import { useSession } from "next-auth/react";

export default function Dashboard() {
  const { data: session, status } = useSession();

  if (status === "loading") {
    return <p>Loading...</p>;
  }

  if (!session) {
    return <p>Access Denied. Please sign in to view this page.</p>;
  }

  return (
    <div>
      <h1>Welcome, {session.user.name}!</h1>
      <p>You are now signed in.</p>
    </div>
  );
}
```

#### Server-Side Protection

For server-side protection, use the `getSession` function to check if the user is authenticated before rendering the page:

```javascript
import { getSession } from "next-auth/react";

export default function Dashboard({ session }) {
  return (
    <div>
      <h1>Welcome, {session.user.name}!</h1>
      <p>You are now signed in.</p>
    </div>
  );
}

export async function getServerSideProps(context) {
  const session = await getSession(context);

  if (!session) {
    return {
      redirect: {
        destination: "/auth/signin", // Redirect to the sign-in page
        permanent: false,
      },
    };
  }

  return {
    props: { session },
  };
}
```

---

## 2. Accessing User Session

You can access the user session on both the client and server sides to personalize the user experience.

### Client-Side Access

Use the `useSession` hook to access the session on the client side:

```javascript
import { useSession } from "next-auth/react";

export default function Profile() {
  const { data: session } = useSession();

  if (!session) {
    return <p>You are not signed in.</p>;
  }

  return (
    <div>
      <p>Welcome, {session.user.name}!</p>
      <p>Email: {session.user.email}</p>
    </div>
  );
}
```

### Server-Side Access

Use the `getSession` function to access the session on the server side:

```javascript
import { getSession } from "next-auth/react";

export default function Profile({ session }) {
  return (
    <div>
      <p>Welcome, {session.user.name}!</p>
      <p>Email: {session.user.email}</p>
    </div>
  );
}

export async function getServerSideProps(context) {
  const session = await getSession(context);

  if (!session) {
    return {
      redirect: {
        destination: "/auth/signin",
        permanent: false,
      },
    };
  }

  return {
    props: { session },
  };
}
```

---

## 3. Advanced Features

NextAuth.js offers several advanced features to customize and extend its functionality.

### Custom Adapters

Adapters allow you to connect NextAuth.js to your custom database or user storage system. For example, you can use a PostgreSQL or MongoDB database to store user data.

#### Example: Using a Custom Adapter

```javascript
import NextAuth from "next-auth";
import Providers from "next-auth/providers";
import { PrismaAdapter } from "@next-auth/prisma-adapter";
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

export default NextAuth({
  adapter: PrismaAdapter(prisma),
  providers: [
    Providers.Google({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
  ],
});
```

---

### Callbacks

Callbacks allow you to customize the behavior of NextAuth.js. For example, you can modify the JWT token or session object.

#### Example: Modifying the JWT Token

```javascript
import NextAuth from "next-auth";
import Providers from "next-auth/providers";

export default NextAuth({
  providers: [
    Providers.Google({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
  ],
  callbacks: {
    async jwt(token, user) {
      if (user) {
        token.id = user.id;
      }
      return token;
    },
    async session(session, token) {
      session.user.id = token.id;
      return session;
    },
  },
});
```

---

### Theming

You can customize the look and feel of the default NextAuth.js pages (e.g., sign-in, sign-out) by using the `theme` option.

#### Example: Customizing the Theme

```javascript
import NextAuth from "next-auth";
import Providers from "next-auth/providers";

export default NextAuth({
  providers: [
    Providers.Google({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
  ],
  theme: {
    colorScheme: "light", // or "dark"
    brandColor: "#2563EB", // Your brand color
    logo: "https://example.com/logo.png", // Your logo
  },
});
```

---

### Webhooks

Webhooks allow you to integrate NextAuth.js with external services. For example, you can trigger a webhook when a user signs in or signs out.

#### Example: Using Webhooks

```javascript
import NextAuth from "next-auth";
import Providers from "next-auth/providers";

export default NextAuth({
  providers: [
    Providers.Google({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
  ],
  events: {
    async signIn(message) {
      // Trigger a webhook when a user signs in
      await fetch("https://example.com/webhook/signin", {
        method: "POST",
        body: JSON.stringify(message),
      });
    },
    async signOut(message) {
      // Trigger a webhook when a user signs out
      await fetch("https://example.com/webhook/signout", {
        method: "POST",
        body: JSON.stringify(message),
      });
    },
  },
});
```
