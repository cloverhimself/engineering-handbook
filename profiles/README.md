# Project Profiles

Profiles add project-type-specific guidance on top of the core handbook.

An AI agent should first follow the root `AGENTS.md`, then select one or more profiles that match the product. Profiles are overlays, not separate architectures.

Available profiles:

- `saas.md`
- `ecommerce.md`
- `fintech.md`
- `marketplace.md`
- `wallet.md`
- `content-platform.md`
- `internal-tool.md`
- `portfolio-static-site.md`
- `mobile-app.md`
- `api-only.md`
- `dashboard.md`

A project may use multiple profiles. Example: a multi-vendor commerce product may combine `saas`, `marketplace`, `ecommerce`, and `dashboard`.

The agent should state which profiles it selected and why in `docs/project-design.md`.
