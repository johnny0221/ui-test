## ADDED Requirements

### Requirement: Repository uses pnpm as the package manager
The repository SHALL define pnpm as the canonical package manager and MUST provide a pnpm lockfile for reproducible installs.

#### Scenario: Fresh clone install
- **WHEN** a developer clones the repository and installs dependencies using pnpm
- **THEN** dependency installation succeeds using `pnpm-lock.yaml` without requiring Yarn artifacts

### Requirement: Project scripts remain executable via pnpm
All existing project workflows for development, test, and build SHALL remain executable through pnpm script invocation without changing script intent, and outcomes MUST remain equivalent to the pre-migration baseline.

#### Scenario: Script parity after migration
- **WHEN** a developer runs the documented pnpm commands for test and build
- **THEN** the repository executes the same underlying npm scripts and the observed outcomes match pre-migration behavior (including any known pre-existing failures)

### Requirement: User-facing instructions reference pnpm commands
Project documentation and automation examples SHALL use pnpm command syntax and MUST NOT instruct users to run Yarn commands for standard setup and verification.

#### Scenario: Onboarding instructions consistency
- **WHEN** a new contributor follows setup and verification instructions from repository docs
- **THEN** all package-manager commands are pnpm-based and can be executed without translating from Yarn
