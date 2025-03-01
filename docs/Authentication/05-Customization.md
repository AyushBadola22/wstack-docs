---
id: customization
title: Customization
sidebar_label: Customization
---

# Customizing the Login Page

NextAuth.js provides a default login page, but you can fully customize it to match your application’s design and branding. This guide will walk you through creating a custom sign-in page, adding multiple providers, styling the page, and handling advanced use cases.

---

## Why Customize the Login Page?

- **Branding**: Match the login page to your app’s design and branding.
- **User Experience**: Provide a seamless and intuitive login experience.
- **Flexibility**: Add custom logic, such as redirects or additional authentication options.

---

## Step 1: Create a Custom Sign-In Page

To create a custom sign-in page, follow these steps:

1. Create a file named `signin.js` in the `pages/auth` directory.
2. Use the `signIn` function from `next-auth/client` to handle authentication.

### Example: Basic Custom Sign-In Page

```javascript
import { signIn } from "next-auth/react";

export default function SignIn() {
  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h1>Welcome to My App</h1>
      <p>Please sign in to continue.</p>
      <button
        onClick={() => signIn("google")}
        style={{
          padding: "10px 20px",
          margin: "10px",
          backgroundColor: "#4285F4",
          color: "white",
          border: "none",
          borderRadius: "5px",
          cursor: "pointer",
        }}
      >
        Sign in with Google
      </button>
      <button
        onClick={() => signIn("github")}
        style={{
          padding: "10px 20px",
          margin: "10px",
          backgroundColor: "#333",
          color: "white",
          border: "none",
          borderRadius: "5px",
          cursor: "pointer",
        }}
      >
        Sign in with GitHub
      </button>
    </div>
  );
}
```

---

## Step 2: Redirect to the Custom Page

To use your custom sign-in page, update the `[...nextauth].js` file to specify the custom page path:

```javascript
import NextAuth from "next-auth";
import Providers from "next-auth/providers";

export default NextAuth({
  providers: [
    Providers.Google({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
    Providers.GitHub({
      clientId: process.env.GITHUB_CLIENT_ID,
      clientSecret: process.env.GITHUB_CLIENT_SECRET,
    }),
  ],
  pages: {
    signIn: "/auth/signin", // Redirect to your custom sign-in page
  },
});
```

---

## Step 3: Advanced Customization

### 1. Add Multiple Providers Dynamically

You can dynamically render buttons for all configured providers using the `providers` array from `next-auth/react`.

#### Example:

```javascript
import { signIn, providers } from "next-auth/react";

export default function SignIn({ providers }) {
  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h1>Welcome to My App</h1>
      <p>Please sign in to continue.</p>
      {Object.values(providers).map((provider) => (
        <div key={provider.name}>
          <button
            onClick={() => signIn(provider.id)}
            style={{
              padding: "10px 20px",
              margin: "10px",
              backgroundColor: "#333",
              color: "white",
              border: "none",
              borderRadius: "5px",
              cursor: "pointer",
            }}
          >
            Sign in with {provider.name}
          </button>
        </div>
      ))}
    </div>
  );
}

export async function getServerSideProps(context) {
  return {
    props: {
      providers: await providers(context),
    },
  };
}
```

---

### 2. Customize the Page Layout

You can use CSS frameworks like Tailwind CSS or styled-components to style your login page.

#### Example with Tailwind CSS:

```javascript
import { signIn } from "next-auth/react";

export default function SignIn() {
  return (
    <div className="flex flex-col items-center justify-center min-h-screen bg-gray-100">
      <h1 className="text-3xl font-bold mb-4">Welcome to My App</h1>
      <p className="mb-8">Please sign in to continue.</p>
      <button
        onClick={() => signIn("google")}
        className="bg-blue-500 text-white px-6 py-2 rounded-lg mb-4 hover:bg-blue-600"
      >
        Sign in with Google
      </button>
      <button
        onClick={() => signIn("github")}
        className="bg-gray-800 text-white px-6 py-2 rounded-lg hover:bg-gray-900"
      >
        Sign in with GitHub
      </button>
    </div>
  );
}
```

---

### 3. Add a Redirect After Sign-In

You can redirect users to a specific page after they sign in by passing the `callbackUrl` parameter.

#### Example:

```javascript
import { signIn } from "next-auth/react";

export default function SignIn() {
  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h1>Welcome to My App</h1>
      <p>Please sign in to continue.</p>
      <button
        onClick={() => signIn("google", { callbackUrl: "/dashboard" })}
        style={{
          padding: "10px 20px",
          margin: "10px",
          backgroundColor: "#4285F4",
          color: "white",
          border: "none",
          borderRadius: "5px",
          cursor: "pointer",
        }}
      >
        Sign in with Google
      </button>
    </div>
  );
}
```

---

### 4. Handle Errors and Messages

You can display error messages or custom messages on the sign-in page.

#### Example:

```javascript
import { signIn, useSession } from "next-auth/react";
import { useRouter } from "next/router";

export default function SignIn() {
  const { error } = useRouter().query;

  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h1>Welcome to My App</h1>
      <p>Please sign in to continue.</p>
      {error && <p style={{ color: "red" }}>Error: {error}</p>}
      <button
        onClick={() => signIn("google")}
        style={{
          padding: "10px 20px",
          margin: "10px",
          backgroundColor: "#4285F4",
          color: "white",
          border: "none",
          borderRadius: "5px",
          cursor: "pointer",
        }}
      >
        Sign in with Google
      </button>
    </div>
  );
}
```

---

## Step 4: Testing and Deployment

1. **Test Locally**: Ensure your custom sign-in page works as expected in your development environment.
2. **Deploy**: Deploy your app and verify that the custom login page functions correctly in production.

---
