# Production Basics

Use this module when a project is moving beyond a throwaway prototype or when these concerns materially affect correctness.

## Configuration and environments

Keep deploy-specific configuration outside source code.

Use environment variables or the platform's secret/configuration system for values such as database connections, API keys, provider credentials, origins, and feature configuration.

Rules:
- never commit secrets;
- validate required configuration at startup where practical;
- fail clearly when mandatory configuration is missing;
- keep development, test, staging, and production configuration distinct;
- do not silently fall back to insecure production defaults;
- keep `.env.example` / config documentation synchronized with actual configuration reads;
- remove stale scaffold variables that the application no longer uses;
- document numeric pool/timeout defaults as defaults unless they come from measured/provider requirements.

## Deployment persistence

Verify what survives process/container restarts before choosing storage.

An ephemeral local filesystem is not durable application persistence. SQLite/local files are appropriate only when the deployment model provides the durability/concurrency properties the product requires.

Distinguish the database engine requirement from the hosting provider. For example, `PostgreSQL` or `managed PostgreSQL` may be the architectural requirement while Cloud SQL, Supabase, Neon, Railway, RDS, or another provider is a current implementation choice.

## Time, dates, and calendar semantics

Time bugs are common and subtle.

First identify what the value means:
- instant/timestamp: one exact point in time;
- local date-time: a wall-clock time in a particular zone/context;
- calendar date: a date such as `2026-09-17` with no time-of-day;
- duration: elapsed amount of time.

Rules:
- store timestamps in a consistent canonical form, usually UTC;
- convert to user-local time at presentation boundaries unless the business rule itself is local-zone based;
- store the relevant timezone when a business rule depends on local civil time;
- preserve date-only values as calendar dates when time-of-day is not part of the domain;
- explicitly define whether a due date becomes overdue at the start/end of the date or by another rule;
- do not let incidental `Date`/timezone parsing silently decide business semantics;
- do not assume every local day is exactly 24 hours where daylight-saving rules apply;
- use established platform APIs/libraries rather than custom timestamp arithmetic.

## Identifiers

Choose IDs based on actual requirements.

Sequential database IDs are often completely acceptable internally.

Use UUID/ULID-like identifiers when benefits such as distributed generation, non-guessable public identifiers, or merging data across systems justify them.

Do not switch identifier schemes merely because one appears more scalable.

Public exposure and database primary-key strategy may differ when appropriate.

External identity-provider IDs can coexist with internal numeric IDs when the mapping is deliberate and uniquely enforced.

## Feature flags

Feature flags let code be deployed while selected behavior remains disabled or limited.

Useful for:
- staged rollouts;
- risky migrations;
- beta features;
- emergency disable switches.

Rules:
- every flag needs an owner and removal condition;
- do not leave permanent dead flags scattered through the codebase;
- test important enabled and disabled paths;
- do not use flags as a substitute for proper authorization.

## Database migrations and deployment order

Schema and application changes must be deployable safely together.

Prefer backward-compatible staged changes for risky production migrations.

Example:

```text
1. Add new nullable column/table
2. Deploy code that can use old and new state
3. Backfill data if needed
4. Switch reads/writes to new state
5. Verify
6. Remove old column/code in a later deployment
```

Avoid deployments where new code requires a schema change that has not yet completed.

Large migrations should consider locking, table size, runtime, rollback/forward-fix strategy, and production traffic.

## Backups and restore

A backup is useful only if it can be restored.

For important systems:
- define what data is backed up;
- define backup frequency and retention;
- know where backups are stored;
- restrict backup access;
- periodically test restoration;
- document expected recovery point and recovery time where business requirements justify it.

Do not claim disaster recovery exists merely because the provider says backups are enabled.

## Health and readiness

Define what each endpoint promises.

Typical distinction:
- liveness: the process is running/responding;
- readiness: the instance can safely serve required traffic.

If an endpoint reports a database/provider as connected or healthy, perform an appropriate lightweight observed check. Do not hard-code dependency health.

Return failure status when the promised readiness property is unavailable. Keep checks bounded so health probes do not become a load source.

## Startup and shutdown

Applications should start and stop predictably.

Where relevant:
- validate config before serving traffic;
- establish required database/dependency connections deliberately;
- expose truthful health/readiness checks;
- stop accepting new work during graceful shutdown;
- allow in-flight critical work to finish within a bounded period;
- close connections cleanly.

## Rule of proportionality

These practices become stricter as lifecycle stage, user impact, financial exposure, and operational risk increase.

Do not build enterprise release machinery for a disposable prototype, but do not treat real production data as disposable simply because the product is still small.
