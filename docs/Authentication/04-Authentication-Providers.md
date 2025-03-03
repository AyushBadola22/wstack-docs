---
id: authentication-providers
title: Authentication Providers
sidebar_label: Authentication Providers
---

# Authentication Providers

NextAuth.js supports a wide range of authentication providers, including OAuth providers like Google and GitHub, as well as email-based passwordless authentication. This guide will walk you through how to configure and use these providers in your Next.js application.

---

## Supported Providers

NextAuth.js supports the following types of authentication providers:

1. **OAuth Providers**: Google, GitHub, Facebook, etc.
2. **Email Providers**: Passwordless authentication via email.
3. **Credentials Provider**: Custom username/password authentication.

---

## Adding Authentication Providers

To add an authentication provider, you need to configure it in your NextAuth.js configuration file. Below are examples for some popular providers.

---

### 1. Google Provider

To enable Google authentication, you’ll need to create a project in the [Google Cloud Console](https://console.cloud.google.com/) and obtain your `Client ID` and `Client Secret`.

#### Configuration Example:

```javascript
import GoogleProvider from "next-auth/providers/google";

export const authOptions = {
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
  ],
};
```

#### Steps to Set Up Google Provider:

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Create a new project or select an existing one.
3. Navigate to **APIs & Services > Credentials**.
4. Click **Create Credentials** and select **OAuth Client ID**.
5. Set the **Authorized Redirect URI** to:
   ```
   http://localhost:3000/api/auth/callback/google
   ```
6. Copy the `Client ID` and `Client Secret` and add them to your `.env.local` file:
   ```env
   GOOGLE_CLIENT_ID=your-client-id
   GOOGLE_CLIENT_SECRET=your-client-secret
   ```

> **Note**: Never expose your `Client ID` or `Client Secret` in your codebase. Always use environment variables.

### 2. GitHub Provider

To enable GitHub authentication, you’ll need to register a new OAuth application in your [GitHub Developer Settings](https://github.com/settings/developers).

#### Configuration Example:

```javascript
import GitHubProvider from "next-auth/providers/github";

export const authOptions = {
  providers: [
    GitHubProvider({
      clientId: process.env.GITHUB_CLIENT_ID,
      clientSecret: process.env.GITHUB_CLIENT_SECRET,
    }),
  ],
};
```

#### Steps to Set Up GitHub Provider:

1. Go to your [GitHub Developer Settings](https://github.com/settings/developers).
2. Click **New OAuth App**.
3. Fill in the required details:
   - **Application Name**: Your app’s name.
   - **Homepage URL**: Your app’s URL (e.g., `http://localhost:3000`).
   - **Authorization Callback URL**:
     ```
     http://localhost:3000/api/auth/callback/github
     ```
4. Copy the `Client ID` and `Client Secret` and add them to your `.env.local` file:
   ```env
   GITHUB_CLIENT_ID=your-client-id
   GITHUB_CLIENT_SECRET=your-client-secret
   ```

> **Note**: GitHub requires you to set a callback URL. Make sure it matches the one in your NextAuth.js configuration.

### 3. Email Provider (Passwordless)

The Email provider allows users to sign in using a magic link sent to their email address.

#### Configuration Example:

```javascript
import EmailProvider from "next-auth/providers/email";

export const authOptions = {
  providers: [
    EmailProvider({
      server: process.env.EMAIL_SERVER,
      from: "Your App <no-reply@example.com>",
    }),
  ],
};
```

#### Steps to Set Up Email Provider:

1. Configure an email service (e.g., SendGrid, Postmark, or SMTP).
2. Add the email server details to your `.env.local` file:
   ```env
   EMAIL_SERVER=smtp://username:password@smtp.example.com:587
   EMAIL_FROM=Your App <no-reply@example.com>
   ```
3. Ensure your email service supports sending emails from the specified `from` address.

> **Note**: The Email provider is ideal for passwordless authentication, but it requires a working email service.

### 4. Credentials Provider

The Credentials provider allows you to implement custom username/password authentication.

#### Configuration Example:

```javascript
import CredentialsProvider from "next-auth/providers/credentials";

export const authOptions = {
  providers: [
    CredentialsProvider({
      name: "Credentials",
      credentials: {
        username: { label: "Username", type: "text" },
        password: { label: "Password", type: "password" },
      },
      async authorize(credentials) {
        // Add logic to verify credentials here
        const user = { id: 1, name: "John Doe", email: "john@example.com" };
        if (
          credentials.username === "john" &&
          credentials.password === "password"
        ) {
          return user;
        } else {
          return null;
        }
      },
    }),
  ],
};
```

> **Note**: The Credentials provider is less secure than OAuth or Email providers. Use it only if necessary and always hash passwords before storing them.

---

## Redirect URLs

Redirect URLs are crucial for OAuth providers. They determine where the user is redirected after authentication. Here’s how to configure them:

### Default Callback URL

NextAuth.js automatically handles callback URLs for OAuth providers. The default format is:

```
http://localhost:3000/api/auth/callback/[provider]
```

For example:

- Google: `http://localhost:3000/api/auth/callback/google`
- GitHub: `http://localhost:3000/api/auth/callback/github`

### Custom Redirect URL

If you want to redirect users to a specific page after login, you can use the `callbackUrl` parameter:

```javascript
signIn("google", { callbackUrl: "/dashboard" });
```
