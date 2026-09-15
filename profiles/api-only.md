# API-Only Profile

Use for backend services exposing APIs without a first-party user interface.

Priorities:
- define API contracts, versioning, validation, status codes, and error shapes explicitly;
- keep controllers/handlers thin and move business rules into cohesive domain/service logic;
- authenticate and authorize at server boundaries;
- document pagination, filtering, sorting, and rate limits;
- make write operations idempotent when retries are plausible;
- use stable request/response schemas and backward-compatible evolution where required;
- expose health/readiness endpoints appropriate to deployment needs;
- keep transport concerns separate from persistence details;
- avoid leaking database models directly as public API contracts when that creates coupling;
- bound expensive endpoints and avoid unbounded queries;
- provide OpenAPI or equivalent contract documentation when useful.
