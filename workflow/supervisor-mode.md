# Supervisor Mode

Supervisor mode is an optional self-review gate for substantial changes. It does not replace human review, CI, security testing, or domain experts.

## When to use it

Use for meaningful features, refactors, security-sensitive work, payments, schema changes, concurrency-sensitive logic, production incidents, and release candidates. Skip or lighten it for trivial edits.

## Review dimensions

Score each dimension from 0 to 10:
- correctness
- readability
- maintainability
- security
- test coverage appropriate to risk
- architecture fit
- performance/capacity fit
- failure handling
- documentation/context accuracy
- unnecessary complexity / over-engineering avoidance

## Default threshold

Do not declare the change ready when any critical dimension is below 8/10 or the overall mean is below 8.5/10.

For financial movement, authentication/authorization, destructive operations, or high-risk migrations, require at least 9/10 for correctness and security before readiness is claimed.

Scores must be justified by evidence. A high score cannot be based on confidence alone.

## Loop

1. Implement the smallest coherent change.
2. Run the applicable tests/checks.
3. Review the diff, not only the final files.
4. Score each dimension and list concrete defects/risks.
5. Fix material issues.
6. Re-run affected checks.
7. Re-score.
8. Stop iterating when thresholds are met or when further changes would be speculative/churn rather than meaningful improvement.

Do not game the score by repeatedly rewriting good code. Do not add abstractions or defensive branches merely to improve a subjective score.

## Required output

When supervisor mode completes, record:
- final scores;
- checks actually run;
- remaining risks;
- deferred items;
- why remaining sub-threshold non-critical concerns were accepted, if any.

If the agent cannot verify a dimension, mark it `unverified` rather than inventing a score.
