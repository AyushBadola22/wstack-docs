---
id: introduction
title: Introduction
sidebar_label: Introduction
---

## 1. Introduction to NextAuth.js

**NextAuth.js** is a complete authentication library for Next.js applications. It simplifies the process of adding authentication (login, sign-up, etc.) to your app by providing built-in support for popular authentication providers like Google, GitHub, Facebook, and more. It also supports email/passwordless authentication and custom databases.

### Key Features:

- **Easy Integration**: Seamlessly integrates with Next.js.
- **OAuth Support**: Works with providers like [Google](https://developers.google.com/identity), [GitHub](https://docs.github.com/en/developers/apps), and more.
- **Session Management**: Built-in session handling for secure user management.
- **Scalable and Secure**: Implements industry-standard security practices.
- **Extensible**: Customize with adapters and callbacks.

---

## 2. Why Use NextAuth.js?

- **Saves Time**: No need to build authentication from scratch.
- **Secure**: Implements best practices for security.
- **Flexible**: Supports multiple authentication providers.
- **Community Support**: Actively maintained and widely used in the Next.js ecosystem.

---

## 3. Installation and Setup

### Step 1: Install NextAuth.js

Run the following command in your Next.js project directory:

```bash
pnpm add next-auth
```

### Step 2: Folder Structure

1. Create an `auth` folder in your project.
2. Inside the `auth` folder, create a dynamic route folder named `[...nextauth]` (using square brackets for dynamic routing).
3. Add the following files inside the `[...nextauth]` folder:
   - A TypeScript file (`[...nextauth].ts`)
   - A route file (`route.ts`) inside the `api` directory.

Here’s an example of the folder structure:

![Folder Structure](/img/authentication_img/folder_structure.jpg)

---

## 4. Credential Providers in Next.js

NextAuth.js supports three types of authentication providers:

1. **[Credentials-based Login](https://next-auth.js.org/configuration/providers/credentials)**: Email/Password or Username/Password.
2. **[Email Login](https://next-auth.js.org/configuration/providers/email)**: Standard Email-Password authentication.
3. **[OAuth Login](https://next-auth.js.org/configuration/providers/oauth)**: Integration with providers like Google, GitHub, etc.

### Configuring a Provider

1. Navigate to the **[Providers](https://next-auth.js.org/providers/)** tab in your NextAuth.js configuration.
2. Choose the provider you want to integrate (e.g., [Google](https://developers.google.com/identity), [GitHub](https://docs.github.com/en/developers/apps)).
3. For **GitHub login**, obtain the **Client ID** and **Client Secret** from GitHub’s developer settings.
4. Add these details to your Next.js authentication configuration.

### Defining Providers in Code

- Use **square brackets (`[...]`)** to define supported providers.
- Example: For GitHub authentication, use `GitHubProvider`.
- For multiple providers, specify them accordingly (e.g., `GoogleProvider`, `FacebookProvider`).

---

## 5. Important: Security Best Practices

:::info  
We highly encourage the use of **OAuth credentials** over traditional credentials (email/password) for the following reasons:
:::

- **Enhanced Security**: OAuth tokens are short-lived and can be revoked, reducing the risk of unauthorized access.
- **No Password Storage**: Eliminates the need to store sensitive user passwords on your server.
- **User Convenience**: Users can log in with their existing accounts (e.g., Google, GitHub) without creating new credentials.

---

### Disadvantages of Using Credential-Based Authentication

While credential-based authentication (email/password or username/password) is a common approach, it comes with several security risks and challenges:

#### 1. **Password Storage Risks**

- **Vulnerability**: Storing passwords in your database makes your application a target for attacks like **SQL injection** or **data breaches**.
- **Attack Scenario**: If an attacker gains access to your database, they can steal plain-text or weakly hashed passwords.

#### 2. **Credential Leakage**

- **Vulnerability**: Credentials sent over insecure connections (e.g., HTTP) can be intercepted by attackers.
- **Attack Scenario**: A man-in-the-middle (MITM) attack can capture login credentials during transmission.

#### 3. **Brute Force Attacks**

- **Vulnerability**: Weak passwords or lack of rate-limiting can make your application susceptible to brute force attacks.
- **Attack Scenario**: Attackers use automated tools to guess passwords repeatedly until they succeed.

#### 4. **Phishing Attacks**

- **Vulnerability**: Users may fall victim to phishing attacks, where attackers trick them into revealing their credentials.
- **Attack Scenario**: Attackers create fake login pages that mimic your application.

#### 5. **CORS and Origin Security Issues**

- **Vulnerability**: Misconfigured **Cross-Origin Resource Sharing (CORS)** policies can expose your authentication endpoints to abuse.
- **Attack Scenario**: Attackers can exploit CORS misconfigurations to perform **cross-site request forgery (CSRF)** or **cross-origin attacks**.

#### 6. **Session Hijacking**

- **Vulnerability**: If session tokens are not properly secured, attackers can hijack user sessions.
- **Attack Scenario**: Attackers steal session cookies through **XSS (Cross-Site Scripting)** or **network sniffing**.

---

### Why OAuth is a Better Alternative

OAuth-based authentication addresses many of the above issues:

- **Short-Lived Tokens**: OAuth tokens expire quickly, reducing the risk of misuse.
- **Built-In Security**: OAuth providers implement robust security measures, including encryption and secure token handling.

:::danger **Warning**
Credential-based authentication is inherently less secure than OAuth. Use it only when absolutely necessary and always follow security best practices.
:::

---

### Resources

- **[OWASP Authentication Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html)**: Best practices for secure authentication.
- **[NextAuth.js Documentation](https://next-auth.js.org/)**: Learn how to implement secure authentication.
- **[OAuth 2.0 Explained](https://oauth.net/2/)**: A beginner-friendly guide to OAuth.
