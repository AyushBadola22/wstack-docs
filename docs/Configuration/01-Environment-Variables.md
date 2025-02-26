---
id: environment-variables
title: Environment Variables
sidebar_label: Environment Variables
---

Here’s a detailed guide for setting up environment variables.

### **Setting Up Environment Variables**

#### **1. Create the `.env` File**

1. Copy the `.env.example` file.
2. Create a new `.env` file in the same directory.
3. Populate the `.env` file with the following variables:

```plaintext
DATABASE_URL="mongodb://localhost:27017/next-starter"
NEXTAUTH_SECRET="Generate a random string with openssl rand -base64 32"
GOOGLE_CLIENT_ID="GOOGLE_CLIENT_ID"
GOOGLE_CLIENT_SECRET="GOOGLE_CLIENT_SECRET"
GITHUB_CLIENT_ID="GITHUB_CLIENT_ID"
GITHUB_CLIENT_SECRET="GITHUB_CLIENT_SECRET"
REDIS_URL=redis://localhost:6379
SESSION_SECRET="Generate a random string with openssl rand -base64 32"
AWS_SECRET_ACCESS_KEY="AWS_SECRET_ACCESS_KEY"
AWS_ACCESS_KEY_ID="AWS_ACCESS_KEY_ID"
AWS_REGION="AWS_REGION"
```

---

#### **2. Install OpenSSL**

1. **Download OpenSSL**:
   - Visit the official OpenSSL website: [https://www.openssl.org/](https://www.openssl.org/).
   - Download the version compatible with your operating system.
2. **Install OpenSSL**:
   - Follow the installation instructions for your OS.
3. **Set Up OpenSSL Path**:
   - Add the OpenSSL installation path to your system’s environment variables.
4. **Verify Installation**:
   - Open a terminal or command prompt and run:
     ```bash
     openssl version
     ```
   - If the version is displayed, OpenSSL is installed correctly.

---

#### **3. Generate Random Strings for Secrets**

1. Generate a random string for `NEXTAUTH_SECRET`:
   ```bash
   openssl rand -base64 32
   ```
   - Copy the output and paste it as the value for `NEXTAUTH_SECRET` in the `.env` file.
2. Generate a random string for `SESSION_SECRET`:
   ```bash
   openssl rand -base64 32
   ```
   - Copy the output and paste it as the value for `SESSION_SECRET` in the `.env` file.

---

#### **4. Set Up MongoDB**

1. **Sign Up/Log In**:
   - Go to [MongoDB Cloud](https://cloud.mongodb.com/).
   - Sign up or log in to your account.
2. **Create a New Project**:
   - Click on **New Project**.
   - Name your project (e.g., `next-starter`).
   - Add yourself as a member.
3. **Create a Cluster**:
   - Click on **Build a Cluster**.
   - Select the free tier (`M0`).
   - Choose your preferred cloud provider and region.
   - Click **Create Cluster** (this may take ~5 minutes).
     ![MongoDB Create Cluster](/img/configuration_img/mongodb1.jpg)
4. **Set Up Database Access**:
   - Navigate to **Database Access** under **Security**.
   - Add a new database user with a username and password.
   - Assign the user the appropriate permissions (e.g., `Read and Write`).
5. **Set Up Network Access**:
   - Navigate to **Network Access** under **Security**.
   - Add your IP address or allow access from anywhere (`0.0.0.0/0`).
6. **Get Connection String**:
   - Navigate to **Database** > **Connect**.
   - Select **Connect your application**.
   - Choose the driver (e.g., `Node.js`) and version.
   - Copy the connection string.
   - Replace the `DATABASE_URL` in your `.env` file with the copied string. Update the username and password if necessary.
     ![MongoDB Create Cluster](/img/configuration_img/mongodb2.jpg)

---

#### **5. Set Up Google OAuth Credentials**

1. **Go to Google Cloud Console**:
   - Visit [Google Cloud Console](https://console.cloud.google.com/).
     ![MongoDB Create Cluster](/img/configuration_img/googleoauth1.jpg)
2. **Create or Select a Project**:
   - Create a new project or select an existing one.
     ![MongoDB Create Cluster](/img/configuration_img/googleoauth2.jpg)
3. **Enable OAuth API**:
   - Navigate to **APIs & Services** > **Library**.
   - Search for **Google+ API** and enable it.
4. **Create OAuth Credentials**:
   - Go to **APIs & Services** > **Credentials**.
   - Click **Create Credentials** > **OAuth 2.0 Client ID**.
   - Select **Web Application** as the application type.
     ![MongoDB Create Cluster](/img/configuration_img/googleoauth3.jpg)
5. **Configure Authorized Redirect URIs**:
   - Add the following URI for local testing:
     ```plaintext
     http://localhost:3000/api/auth/callback/google
     ```
     ![MongoDB Create Cluster](/img/configuration_img/googleoauth5.jpg)
6. **Copy Credentials**:
   - Copy the `Client ID` and `Client Secret`.
   - Paste them into the `.env` file as `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET`.
     ![MongoDB Create Cluster](/img/configuration_img/googleoauth6.jpg)

---

#### **6. Set Up GitHub OAuth Credentials**

1. **Go to GitHub Developer Settings**:
   - Visit [GitHub Developer Settings](https://github.com/settings/developers).
2. **Create a New OAuth App**:
   - Click **New OAuth App**.
   - Fill in the required fields:
     - **Application Name**: Your app name.
     - **Homepage URL**: `http://localhost:3000`.
     - **Authorization Callback URL**: `http://localhost:3000/api/auth/callback/github`.
3. **Copy Credentials**:
   - Copy the `Client ID` and `Client Secret`.
   - Paste them into the `.env` file as `GITHUB_CLIENT_ID` and `GITHUB_CLIENT_SECRET`.

---

#### **7. Set Up Redis**

1. **Install Redis**:
   - Download and install Redis from [https://redis.io/download](https://redis.io/download).
2. **Run Redis Locally**:
   - Start the Redis server:
     ```bash
     redis-server
     ```
   - Verify it’s running by connecting to it:
     ```bash
     redis-cli ping
     ```
   - If it responds with `PONG`, Redis is running correctly.
3. **Update `.env`**:
   - Use the default Redis URL:
     ```plaintext
     REDIS_URL=redis://localhost:6379
     ```

---

#### **8. Set Up AWS Credentials**

1. **Go to AWS Management Console**:
   - Visit [AWS Management Console](https://aws.amazon.com/console/).
2. **Create IAM User**:
   - Navigate to **IAM** > **Users** > **Add User**.
   - Set permissions (e.g., `AmazonS3FullAccess`).
   - Generate access keys (`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`).
3. **Update `.env`**:
   - Paste the access keys and your preferred region into the `.env` file:
     ```plaintext
     AWS_ACCESS_KEY_ID="your-access-key-id"
     AWS_SECRET_ACCESS_KEY="your-secret-access-key"
     AWS_REGION="your-region"
     ```

---

### **Next Steps**

1. Save the `.env` file.
2. Restart your development server to apply the changes.
3. Verify that all services (MongoDB, Redis, etc.) are running correctly.
4. Test your application to ensure everything is working as expected.
