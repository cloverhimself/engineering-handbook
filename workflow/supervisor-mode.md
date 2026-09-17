# Supervisor Mode

Supervisor mode is an evidence-based self-review gate for substantial changes and release candidates. It does not replace human review, CI, security testing, production observation, or domain experts.

## When to use it

Use for meaningful features, refactors, security-sensitive work, payments, schema changes, concurrency-sensitive logic, production incidents, phase completion, and release candidates. Skip or lighten it for trivial edits.

## Review dimensions

Score each dimension from 0 to 10 only when there is enough evidence:
- correctness;
- readability;
- maintainability;
- security;
- test coverage appropriate to risk;
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
- manual verification;
- repository inspection;
- runtime/provider verification;
- assumptions;
- unverified claims.

For discovery-based checks, include meaningful counts when they matter. Examples: tests discovered/passed, migrations found/applied, files checked, or lint/type errors. A command exiting successfully with zero relevant work discovered is not completion evidence.

Do not claim a check passed unless it was actually executed. Do not infer provider/runtime state from source code alone.

## Review loop

1. Implement the smallest coherent change.
2. Run the applicable tests/checks.
3. Review the diff, not only the final files.
4. Review high-risk invariants and failure paths explicitly.
5. Check that expected client errors are deliberate and unexpected internals are not leaked.
6. Check code organization: avoid both speculative abstraction and god files/modules whose responsibilities have diverged.
7. Check documentation/config examples against actual code, commands, routes, and configuration reads.
8. Score verified dimensions and list concrete defects/risks.
9. Fix material issues.
10. Re-run affected checks.
11. Re-score.
12. Stop iterating when thresholds are met or further changes would be speculative churn.

Do not game the score by repeatedly rewriting good code. Do not add abstractions, dependencies, infrastructure, defensive branches, or tests merely to increase a subjective score.

## Phase/release completion gate

Before declaring a phase or project complete, verify:
- the canonical repository contains the final state, not only an ephemeral/local workspace;
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
- what was automated, manually verified, or unverified;
- remaining risks and assumptions;
- deferred items;
- documentation/context reconciled;
- whether the canonical repository contains the reviewed state;
- why any accepted non-critical concerns remain.
