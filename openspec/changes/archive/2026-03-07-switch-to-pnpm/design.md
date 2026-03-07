## Context

This starter currently uses Yarn (`yarn.lock`) and Yarn-based command examples. The goal is to move the project to pnpm so new consumers get deterministic installs with the pnpm lockfile format and standard pnpm workflows. The repository is small and self-contained, so migration can be completed in one pass without phased rollout.

Key constraints:
- Keep existing npm script names and behavior unchanged (only invocation method changes).
- Avoid introducing new runtime dependencies; this is a tooling migration.
- Keep contributor onboarding simple by documenting a single package manager.

## Goals / Non-Goals

**Goals:**
- Make pnpm the canonical package manager for install and script execution.
- Replace Yarn lock and references with pnpm equivalents.
- Ensure local development and CI commands are consistent with pnpm.
- Preserve existing build/test outputs and package behavior.

**Non-Goals:**
- Refactoring application code or changing component behavior.
- Changing Node.js runtime policy beyond what pnpm requires.
- Supporting multiple package managers simultaneously.

## Decisions

1. Adopt a single-package-manager policy (pnpm only).
   - Rationale: Mixed package manager support increases maintenance burden and can cause lockfile drift.
   - Alternative considered: Keep both Yarn and pnpm instructions. Rejected because it weakens reproducibility and complicates CI/docs.

2. Replace `yarn.lock` with `pnpm-lock.yaml` and set `packageManager` in `package.json`.
   - Rationale: Lockfile + packageManager metadata provides deterministic dependency graph and explicit tooling expectation.
   - Alternative considered: Keep lockfile implicit and document pnpm only. Rejected because tooling ambiguity can cause inconsistent installs.

3. Update all command references in docs and automation to pnpm command forms.
   - Rationale: Prevents onboarding friction and avoids stale instructions.
   - Alternative considered: Add translation notes ("use yarn/pnpm equivalent"). Rejected because it adds cognitive load for starter users.

4. Validate migration by reinstalling dependencies and running existing verification commands.
   - Rationale: Confirms no functional regressions from dependency resolution changes.
   - Alternative considered: Lockfile-only update without validation. Rejected due to higher risk of unnoticed breakage.

5. Treat verification as baseline parity, not greenfield correctness.
   - Rationale: This change is limited to package-manager migration and should preserve existing behavior, including known pre-existing test outcomes.
   - Alternative considered: Require all tests to pass as part of migration. Rejected because it mixes unrelated product/test fixes into this scoped tooling change.

## Risks / Trade-offs

- [Contributors without pnpm installed] -> Mitigation: Document installation prerequisite and include clear setup commands.
- [Dependency resolution differences between Yarn and pnpm] -> Mitigation: Regenerate lockfile cleanly and run test/build checks after migration.
- [Residual Yarn references in scripts/docs] -> Mitigation: Perform repository-wide search for `yarn` and replace all user-facing command references.
- [CI environment assumes Yarn availability] -> Mitigation: Update CI steps to use pnpm and verify cache/install paths if applicable.

## Migration Plan

1. Remove `yarn.lock` from the repository.
2. Install dependencies with pnpm to generate `pnpm-lock.yaml`.
3. Add/update `packageManager` metadata in `package.json` to pnpm.
4. Update README and any automation/configuration references from Yarn to pnpm.
5. Run validation commands (install, test, build) using pnpm.
6. If validation fails, restore previous lockfile state and address dependency or script incompatibilities before retrying.

## Open Questions

- Should CI enable Corepack explicitly, or assume pnpm is preinstalled in the execution environment?
- Is a minimum pnpm version required for this starter, and should it be documented in contributor setup guidance?
