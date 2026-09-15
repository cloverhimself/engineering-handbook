# Clover Engineering Handbook

A reusable, vendor-neutral engineering constitution for AI-assisted software development.

The goal is not maximum architectural sophistication. The goal is conventional, understandable, secure, maintainable software that can scale when evidence requires it.

## Core philosophy

- Prefer boring, proven technology.
- Follow framework and language conventions before inventing abstractions.
- Start simple; scale from measured constraints.
- Every major decision has tradeoffs. Record them.
- Money, permissions, user data, and destructive operations require extra rigor.
- Optimize for the next engineer being able to understand the system.
- AI may accelerate implementation; it does not relax engineering standards.

## How to use this repository

For each new project, put `AGENTS.md` in the project root and make the handbook available under `.engineering/` (copy, subtree, or submodule). The root `AGENTS.md` requires the coding agent to read the relevant handbook sections before implementation.

Before implementation, complete `templates/project-design.md`. For meaningful architectural decisions, create ADRs from `templates/adr.md`.

See `agent/USAGE.md` for recommended workflows.
