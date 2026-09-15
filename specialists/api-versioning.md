# API Versioning

Use versioning only when a public or independently deployed API contract needs controlled evolution. Internal APIs can often evolve with coordinated callers.

Prefer backwards-compatible additive changes first. Avoid breaking field removals, type changes, semantic changes, and response-shape changes without a migration plan.

For public REST APIs, URI versioning such as `/v1/...` is acceptable and easy to operate. Header-based versioning is valid but adds operational complexity; use it only when requirements justify it.

Document deprecations, replacement endpoints, support windows, and migration steps. Do not run multiple API versions forever by default.

Treat API contracts as products: validate inputs, keep errors consistent, preserve documented semantics, and test backward compatibility when clients depend on it.
