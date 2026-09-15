# Git, Commits, and Pull Requests

Use Git history to make changes understandable and reversible.

## Branches

Prefer short-lived topic branches for non-trivial work. Keep one coherent concern per branch when practical.

## Commits

Commit at meaningful checkpoints, not every few lines and not only once at the end of a huge change.

A good commit should:
- represent one coherent change;
- leave the repository in a reasonably valid state when practical;
- have a clear imperative message describing intent;
- avoid mixing unrelated refactors, formatting churn, dependency upgrades, and feature behavior;
- include tests/docs/migrations that belong to the same change.

Do not create fake commits merely to appear active. Do not commit secrets, generated junk, build artifacts, or unrelated local files.

Prefer messages such as:
- `feat: add order cancellation flow`
- `fix: prevent duplicate payment capture`
- `refactor: isolate notification delivery`
- `test: cover inventory reservation races`
- `docs: record payment reconciliation design`

Conventional Commits are optional unless the project adopts them.

## Pull requests

PRs should be small enough to review coherently and focused on one purpose. Split large work by meaningful dependency layers instead of submitting an enormous mixed diff.

Before opening/requesting review:
- self-review the diff;
- remove debugging/dead code;
- run relevant tests/lint/type/build/security checks;
- confirm migrations and backwards compatibility;
- update `docs/PHASES.md` and `docs/CONTEXT.md`;
- explain what changed, why, how it was verified, risks, migration/deployment notes, and deferred work.

Use draft PRs for early collaboration when appropriate.

Do not merge with known critical failures merely because the feature appears to work manually.

## AI agent rule

An agent must not commit, push, open a PR, merge, or deploy unless the user/project instructions grant that authority. When authority exists, preserve human-readable history rather than batching unrelated work into a single giant commit.
