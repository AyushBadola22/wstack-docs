---
id: development
title: Development
sidebar_label: Development
---

# Development

Welcome to the development guide for this project! This document will walk you through the steps required to set up your local environment, run the development server, and contribute effectively using **pnpm**. Let’s get started!

---

## 1. Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Node.js (v18 or higher):** [Download Node.js](https://nodejs.org/)  
  <img src="https://upload.wikimedia.org/wikipedia/commons/d/d9/Node.js_logo.svg" alt="Node.js Logo" width="100"/>

- **pnpm:** Install **pnpm** globally using the following command:

  ```bash
  npm install -g pnpm
  ```

  <img src="https://upload.wikimedia.org/wikipedia/commons/c/c1/Pnpm_logo.svg" alt="pnpm Logo" width="100"/>

---

## 2. Setting Up the Development Environment

Follow these steps to set up your local development environment:

1. **Clone the Repository**

   ```bash
   git clone <https://github.com/MambaCodes/wstack.git>
   ```

2. **Install Dependencies**

   ```bash
   pnpm install
   ```

3. **Start the Development Server**

   ```bash
   pnpm dev
   ```

### ⚠️ Possible Issue: Missing `.env` File

If you encounter errors when running `pnpm dev`, it might be due to a missing `.env` file.

#### ✅ Setting Up the `.env` File:

1. Create a `.env` file in the root of your project.
2. Copy the required environment variables from `.env.example` (if available).
3. Fill in the necessary values based on your project’s requirements.
4. Restart the development server after setting up the `.env` file.

:::info Important  
For better understanding of configuration of the `.env` file, read configurations docs.
:::
