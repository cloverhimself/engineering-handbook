# Defensive Programming Without Paranoia

Defensive programming should protect real trust boundaries and plausible failure modes, not multiply branches for states the system's own invariants already make impossible.

Add checks when:
- data crosses an external trust boundary;
- concurrency can invalidate assumptions;
- external services can fail or return unexpected data;
- persisted legacy/corrupt data is realistically possible;
- security or financial impact justifies defense in depth.

Avoid duplicate impossible-state checks when a stronger invariant already guarantees the condition through types, validated construction, database constraints, or a tightly controlled internal call path.

Do not silently recover from programmer bugs by returning fake defaults. Fail loudly in development and surface invariant violations clearly.

Before adding a defensive branch, ask:
1. Can this state actually occur in production?
2. What mechanism prevents it?
3. Is that mechanism local and trustworthy?
4. Would this extra check improve safety, or merely hide a bug and add noise?

Prefer making invalid states hard to represent over repeatedly checking them everywhere.
