---
id: troubleshooting
title: Troubleshooting
sidebar_label: Troubleshooting
---

### 1. Common Issues & Fixes

- **pnpm command not found**

  - Ensure `pnpm` is installed globally: `npm install -g pnpm`.

- **Port already in use**

  - Kill the process using the port: `npx kill-port 3000`.
  - By using Netstat command: `netstat -ano | findstr :<PORT>`.

  For more information, refer to the [Stackoverflow](https://stackoverflow.com/questions/39632667/how-can-i-close-some-specific-port-on-linux).

- **Dependency issues**
  - Run `pnpm install --force` to reinstall dependencies.

---
