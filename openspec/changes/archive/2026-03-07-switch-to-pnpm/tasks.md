## 1. Package Manager Migration

- [x] 1.1 Remove `yarn.lock` and generate `pnpm-lock.yaml` via a clean pnpm install
- [x] 1.2 Update `package.json` with pnpm package manager metadata
- [x] 1.3 Verify dependency install succeeds from a fresh state using pnpm only

## 2. Command and Automation Updates

- [x] 2.1 Replace Yarn command usage with pnpm in repository docs and setup instructions
- [x] 2.2 Update any project scripts or CI/dev automation references that invoke Yarn
- [x] 2.3 Confirm no remaining user-facing Yarn references in the repository

## 3. Validation

- [x] 3.1 Run test and build workflows through pnpm command invocation
- [x] 3.2 Verify outputs remain functionally equivalent to pre-migration expectations
- [x] 3.3 Document pnpm prerequisite/version expectations for contributors
