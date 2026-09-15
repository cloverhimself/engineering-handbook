# SaaS Profile

Use for software delivered continuously to multiple customers or organizations.

Priorities:
- define tenant boundaries explicitly;
- choose single-tenant vs multi-tenant architecture intentionally;
- enforce tenant scoping in every data-access path;
- model roles and permissions per tenant;
- isolate tenant configuration from global configuration;
- design subscription/plan entitlements separately from authorization;
- record audit events for administrative actions;
- plan onboarding, suspension, cancellation, export, and deletion workflows;
- avoid per-tenant infrastructure unless justified by isolation or scale requirements;
- track cost per tenant when infrastructure or third-party usage is material.

For multi-tenant databases, prefer explicit tenant identifiers and constraints that prevent cross-tenant uniqueness mistakes. Never rely only on UI filtering for isolation.
