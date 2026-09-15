# Authentication, Sessions, and JWTs

Authentication proves identity; authorization decides what that identity may do. Keep them separate.

Prefer the framework/platform's established authentication primitives before custom protocols.

For browser applications, secure server-backed sessions are often simpler than JWTs. Use JWTs when stateless verification or service boundaries genuinely require them; do not choose JWTs merely because they are popular.

Sessions/tokens must have explicit expiry, rotation/revocation strategy, secure transport/storage, and logout behavior. Regenerate session identifiers after authentication or privilege changes where applicable.

Keep access tokens short-lived when practical. Protect refresh tokens more strongly and rotate them when appropriate. Never place secrets or sensitive user data in readable JWT claims.

Password reset, email verification, invitations, and one-time actions require single-use, expiring tokens and safe consumption semantics.

Authorization must be enforced server-side for every protected action and object, including ownership/tenant boundaries.
