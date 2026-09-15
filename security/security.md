# Security Standard

Use OWASP-style secure-design principles: secure defaults, least privilege, defense in depth, minimized attack surface, safe failure, and explicit trust boundaries.

## Mandatory review areas

Authentication, sessions/tokens, authorization, admin functions, password reset, email/phone verification, uploads, webhooks, payment callbacks, APIs, secrets, dependency risk, logs, and destructive operations.

Use deny-by-default RBAC/ABAC rules. Resource ownership checks must happen server-side.

Sensitive mutations should be protected against replay/duplication where applicable.

Do not expose whether an account exists when doing so materially increases abuse risk.

Secrets belong in environment/secret management, never source control.
