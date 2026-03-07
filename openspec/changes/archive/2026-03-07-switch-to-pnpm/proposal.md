## Why

This starter repository currently uses Yarn, while many teams now standardize on pnpm for faster installs, better disk efficiency, and stricter dependency management. Switching now reduces tooling friction for new projects and keeps the starter aligned with modern JavaScript workflows.

## What Changes

- Replace Yarn as the package manager with pnpm for local development and CI usage.
- Update repository lockfile and package manager metadata to pnpm equivalents.
- Update setup, install, test, and build instructions to use pnpm commands.
- Remove Yarn-specific artifacts and references from project documentation and scripts.

## Capabilities

### New Capabilities
- `pnpm-package-management`: The starter supports dependency installation, script execution, and reproducible locking via pnpm.

### Modified Capabilities
- None.

## Impact

- Affected code and config: `package.json`, lockfile(s), and any CI/dev scripts that call package manager commands.
- Affected docs: `README.md` and any contributor/setup guidance.
- Dependencies and tooling: developers and automation must have pnpm available instead of Yarn.
