# Observability and SLOs

Production systems should expose enough information to answer: is it working, is it slow, is it failing, and why?

Use structured logs, metrics, traces where they add value, error reporting, and health/readiness checks appropriate to the service.

For important services, track the four golden signals: latency, traffic, errors, and saturation.

Define SLIs around actual user-visible behavior. Define SLOs only when the product needs explicit reliability targets; do not invent enterprise-grade SLO machinery for a tiny internal tool.

Alert on symptoms that require action, not every noisy metric. Prefer actionable alerts tied to user impact or exhausted error budget.

Do not log secrets, passwords, full tokens, payment credentials, or unnecessary personal data.

Audit logs are separate from debug logs: preserve who did what, to which resource, and when for important business/security events.
