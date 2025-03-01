---
id: configuration
title: Configuration
sidebar_label: Configuration
---

# Configuration

NextAuth.js is highly configurable and allows you to set up authentication quickly. This guide will walk you through creating the API route, configuring providers, and setting up environment variables.

---

## 1. Create the API Route

NextAuth.js requires an API route to handle authentication requests. This route will manage sign-in, sign-out, and session handling.

### Steps to Create the API Route

1. Create a directory for the authentication API route:
   ```bash
   mkdir -p pages/api/auth
   ```
2. Create a dynamic route file named `[...nextauth].js` inside the `pages/api/auth` directory:
   ```bash
   touch pages/api/auth/[...nextauth].js
   ```

This file will act as the entry point for all authentication-related requests.

---

## 2. Basic Configuration

### Configure NextAuth.js

Open the `[...nextauth].js` file and add the following code to set up NextAuth.js:

```javascript
import NextAuth from "next-auth";
import Providers from "next-auth/providers";

export default NextAuth({
  // Configure one or more authentication providers
  providers: [
    Providers.Google({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
    // Add more providers here
  ],

  // Optional: Customize the look and feel of the login page
  theme: "light",

  // Optional: Enable debug mode for development
  debug: process.env.NODE_ENV === "development",
});
```

#### Explanation:

- **Providers**: Add one or more authentication providers (e.g., Google, GitHub, Email).
- **Theme**: Customize the appearance of the default login page (`light` or `dark`).
- **Debug**: Enable debug mode during development to log detailed information.

---

### Add Environment Variables

NextAuth.js requires certain environment variables to function properly. These variables store sensitive information like provider credentials and should never be exposed in your codebase.

1. Create a `.env.local` file in the root of your project:
   ```bash
   touch .env.local
   ```
2. Add the following environment variables to the `.env.local` file:
   ```env
   GOOGLE_CLIENT_ID=your-google-client-id
   GOOGLE_CLIENT_SECRET=your-google-client-secret
   NEXTAUTH_URL=http://localhost:3000
   ```

#### Explanation of Variables:

- **GOOGLE_CLIENT_ID** and **GOOGLE_CLIENT_SECRET**: Credentials obtained from your Google Cloud Console.
- **NEXTAUTH_URL**: The base URL of your application (e.g., `http://localhost:3000` for development).

---

:::danger **Important Security Note**:

- Never commit your `.env.local` file to version control (e.g., Git). Add it to your `.gitignore` file to prevent accidental exposure of sensitive credentials.
- Use HTTPS in production to encrypt communication between the client and server.
  :::

---

## 3. Adding More Providers

NextAuth.js supports a wide range of authentication providers. Here’s how to add additional providers:

### Example: Adding GitHub Provider

1. Register a new OAuth application in your [GitHub Developer Settings](https://github.com/settings/developers).
2. Add the GitHub provider to your `[...nextauth].js` file:

   ```javascript
   import GitHubProvider from "next-auth/providers/github";

   export default NextAuth({
     providers: [
       GitHubProvider({
         clientId: process.env.GITHUB_CLIENT_ID,
         clientSecret: process.env.GITHUB_CLIENT_SECRET,
       }),
     ],
   });
   ```

3. Add the GitHub credentials to your `.env.local` file:
   ```env
   GITHUB_CLIENT_ID=your-github-client-id
   GITHUB_CLIENT_SECRET=your-github-client-secret
   ```

---

## 4. Optional Configuration

### Customizing the Login Page

You can customize the default login page by using the `theme` option:

```javascript
export default NextAuth({
  theme: {
    colorScheme: "light", // or "dark"
    brandColor: "#2563EB", // Your brand color
    logo: "https://example.com/logo.png", // Your logo
  },
});
```

### Enabling Debug Mode

Debug mode is useful during development to log detailed information about authentication requests:

```javascript
export default NextAuth({
  debug: process.env.NODE_ENV === "development",
});
```

---

## 5. Testing Your Configuration

1. Start your Next.js development server:
   ```bash
   npm run dev
   ```
2. Visit the default login page at `http://localhost:3000/api/auth/signin`.
3. Test the authentication flow with your configured providers.
