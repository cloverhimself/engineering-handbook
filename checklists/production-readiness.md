# Production Readiness Checklist

- Build, lint/typecheck, and tests pass.
- Production configuration validated.
- Secrets are not committed or logged.
- Database migrations reviewed and tested.
- Backups/restore expectations defined.
- Authentication and authorization reviewed.
- Rate limits/abuse controls applied where appropriate.
- Input validation and upload limits reviewed.
- External calls have timeouts/failure handling.
- Payment/webhook idempotency verified where applicable.
- Health/readiness behavior appropriate.
- Logs contain enough diagnostic context without secrets.
- Error responses do not leak internals.
- Critical audit events are captured.
- Capacity assumptions remain reasonable.
- Cost surprises/usage-based services reviewed.
- Rollback or forward-fix strategy exists.
- Documentation updated.
