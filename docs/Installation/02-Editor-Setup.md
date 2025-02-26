---
id: editor-setup
title: Editor Setup
sidebar_label: Editor Setup
---

# Editor Setup

To ensure a smooth development experience while working on Wstack project, it's important to set up your code editor properly. This guide focuses on **Visual Studio Code (VS Code)**, one of the most popular editors for web development. Follow the steps below to configure your editor for optimal productivity.

---

## 1. Install Visual Studio Code

If you haven't already installed VS Code, download and install it from the official website:

- [Download VS Code](https://code.visualstudio.com/)

---

## 2. Recommended Extensions

Extensions enhance the functionality of VS Code and make development easier.
Below are some **suggestions** of **essential extensions** for working with projects:

Here's a refactored version with better structure, clarity, and readability:

### 2.1. Code Formatting

#### **Pretti - Code Formatter**

Prettier ensures consistent code formatting across the project.

#### Installation

- Install Prettier via the **Extensions Marketplace** or run:
  ```bash
  ext install esbenp.prettier-vscode
  ```

#### Configuration in VS Code

1. **Enable Format on Save:**

   - Open **VS Code Settings** (`Ctrl + ,` or `Cmd + ,` on Mac).
   - Search for `"format on save"`.
   - Enable **Editor: Format On Save**.

2. **Set Prettier as the Default Formatter:**
   - Search for `"default formatter"` in settings.
   - Set it to **Prettier - Code formatter**.

### 2.2. Linting and Debugging

- **ESLint**  
  Integrates ESLint into VS Code for real-time linting and error detection.

  - Install via the Extensions Marketplace or use the command:
    ```bash
    ext install dbaeumer.vscode-eslint
    ```

- **Debugger for Chrome**  
  Allows you to debug your Next.js application directly in VS Code.
  - Install via the Extensions Marketplace or use the command:
    ```bash
    ext install msjsdiag.debugger-for-chrome
    ```

### 2.3. Themes for Better Readability

- **One Dark Pro**  
  A popular dark theme with excellent readability.

  - Install via the Extensions Marketplace or use the command:
    ```bash
    ext install zhuangtongfa.Material-theme
    ```

- **GitHub Theme**  
  Matches the look and feel of GitHub's syntax highlighting.
  - Install via the Extensions Marketplace or use the command:
    ```bash
    ext install github.github-vscode-theme
    ```

### 2.4. Other Useful Extensions

- **GitLens**  
  Supercharges Git capabilities within VS Code, providing insights into code changes and blame annotations.

  - Install via the Extensions Marketplace or use the command:
    ```bash
    ext install eamodio.gitlens
    ```

- **Path Intellisense**  
  Autocompletes file paths for faster navigation.

  - Install via the Extensions Marketplace or use the command:
    ```bash
    ext install christian-kohler.path-intellisense
    ```

- **Tailwind CSS IntelliSense**  
  If your project uses Tailwind CSS, this extension provides autocomplete and linting support.
  - Install via the Extensions Marketplace or use the command:
    ```bash
    ext install bradlc.vscode-tailwindcss
    ```
