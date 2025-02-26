---
id: managing-dependencies
title: Managing Dependencies
sidebar_label: Managing Dependencies
---

To manage dependencies, use the following commands with `pnpm`:

### Installing a Package

To install a package, run:

```bash
pnpm add <package-name>
```

### Uninstalling a Package

To uninstall a package, run:

```bash
pnpm remove <package-name>
```

### Installing Dev Dependencies

To install a package as a development dependency, run:

```bash
pnpm add -D <package-name>
```

### Updating Dependencies

To update a package to its latest version, run:

```bash
pnpm update <package-name>
```

### Installing All Dependencies

To install all dependencies listed in `package.json`, run:

```bash
pnpm install
```

### Global Installation

To install a package globally, run:

```bash
pnpm add -g <package-name>
```

### Why Use `pnpm`?

- **Faster Installations**: `pnpm` uses a content-addressable filesystem, making installations faster and more efficient.
- **Disk Space Efficiency**: It avoids duplicating packages by using a single copy of each package across projects.
- **Strict Dependency Resolution**: Ensures a consistent and reliable dependency tree.

For more information, refer to the [pnpm documentation](https://pnpm.io/).
