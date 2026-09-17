# Supervisor Mode

Supervisor mode is an evidence-based self-review gate for substantial changes, phase completion, and release candidates. It does not replace human review, CI, security testing, production observation, or domain experts.

## When to use it

Mandatory for:
- completion of a substantial implementation phase;
- release candidates;
- security-sensitive work;
- payments/money movement;
- authentication/authorization changes;
- schema/data-integrity changes;
- destructive or irreversible operations;
- concurrency-sensitive logic.

It may be skipped or shortened only for trivial edits.

## Review dimensions

Score each dimension from 0 to 10 only when there is enough evidence:
- correctness;
- readability;
- maintainability;
- security;
- test coverage appropriate to risk;
- functional acceptance of affected user journeys;
- architecture fit;
- performance/capacity fit;
- failure handling;
- documentation/context accuracy;
- unnecessary complexity / over-engineering avoidance.

If a dimension cannot be verified, mark it `unverified` rather than inventing a score.

## Default threshold

Do not declare the change ready when any critical verified dimension is below 8/10 or the verified overall mean is below 8.5/10.

For financial movement, authentication/authorization, destructive operations, or high-risk migrations, require at least 9/10 for correctness and security before readiness is claimed.

Scores must be justified by evidence. Confidence, compilation, or a successful build alone are not evidence of business correctness.

## Evidence rules

Record what was actually verified and how.

Distinguish:
- automated tests/checks;
- manual/browser/device verification;
- repository inspection;
- runtime/provider verification;
- assumptions;
- unverified claims.

For discovery-based checks, include meaningful counts when they matter. Examples: tests discovered/passed, migrations found/applied, files checked, or lint/type errors. A command exiting successfully with zero relevant work discovered is not completion evidence.

Do not claim a check passed unless it was actually executed. Do not infer provider/runtime state from source code alone.

## Functional acceptance

Follow `workflow/functional-acceptance.md` for user-facing behavior.

Before approving a phase that adds or changes a critical user journey, verify that journey through the highest practical layer available. Backend/API tests alone are not enough when the failure could exist in UI state, payload shaping, routing, browser behavior, or client/server integration.

For a user-facing MVP/release, run a small smoke test of the primary journeys before calling the product complete.

If the affected critical journey is not exercised, mark functional acceptance `unverified` and do not describe the feature as fully functional.

## Review loop

1. Implement the smallest coherent change.
2. Run the applicable tests/checks.
3. Exercise affected critical user journeys according to `workflow/functional-acceptance.md`.
4. Review the diff, not only the final files.
5. Review high-risk invariants and failure paths explicitly.
6. Check that expected client errors are deliberate and unexpected internals are not leaked.
7. Check code organization: avoid both speculative abstraction and god files/modules whose responsibilities have diverged.
8. Check documentation/config examples against actual code, commands, routes, and configuration reads.
9. Score verified dimensions and list concrete defects/risks.
10. Fix material issues.
11. Re-run affected checks and acceptance journeys.
12. Re-score.
13. Stop iterating when thresholds are met or further changes would be speculative churn.

Do not game the score by repeatedly rewriting good code. Do not add abstractions, dependencies, infrastructure, defensive branches, or tests merely to increase a subjective score.

## Phase/release completion gate

Before declaring a phase or project complete, verify:
- the canonical repository contains the final state, not only an ephemeral/local workspace;
- critical user journeys introduced or changed in the phase have functional-acceptance evidence;
- `README.md`, environment examples, active context, phase state, and design docs do not contradict the implementation;
- the roadmap is reconciled rather than silently inventing a new phase;
- automated evidence is not presented as coverage for behavior it does not exercise;
- known manual-verification areas are stated honestly;
- stale comments, scaffold defaults, unused dependencies, and obsolete configuration have been reviewed.

## Required output

When supervisor mode completes, record:
- concrete findings;
- fixes made;
- final verified scores;
- exact checks actually run and useful discovery/pass counts;
- critical user journeys exercised and their result;
- what was automated, manually/browser verified, or unverified;
- remaining risks and assumptions;
- deferred items;
- documentation/context reconciled;
- whether the canonical repository contains the reviewed state;
- why any accepted non-critical concerns remain.
