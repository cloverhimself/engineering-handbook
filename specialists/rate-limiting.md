# Rate Limiting

Rate limiting is an abuse-control and capacity-protection tool, not a substitute for authorization or validation.

Apply stricter limits to sensitive operations such as login, password reset, OTP, signup, invite acceptance, expensive search, public write APIs, payment initialization, and verification endpoints.

Choose the limiting identity deliberately: IP, authenticated user, API key, tenant, device, endpoint, or a combination. IP-only limiting can punish users behind shared networks and can be bypassed by distributed attackers.

Return clear retry information when practical. Keep limits configurable.

Distributed applications require a consistent limiting strategy; do not assume process-local counters protect a multi-instance service.

Measure rejected traffic and false positives. Limits should reflect actual abuse/capacity needs rather than arbitrary numbers copied from another system.
