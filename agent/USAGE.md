# Using the Handbook with Coding Agents

## Recommended project setup

Keep this handbook as a central repository. In each product repository, expose the rules locally so the agent does not need to rely on external memory.

### Option A — copy the standards (simplest)
Copy `AGENTS.md` and the relevant handbook folders into `.engineering/` in the project. This is easy and works offline, but updates are manual.

### Option B — git submodule (central updates)
Add the handbook as `.engineering/` using a Git submodule, then keep a root `AGENTS.md` in the project that says the agent must read `.engineering/AGENTS.md` and the relevant sections before substantial work.

### Option C — git subtree (often easiest for teams)
Vendor the handbook into `.engineering/` with `git subtree`. The files behave like normal project files, and updates can be pulled from the source repository without submodule friction.

## Project root AGENTS.md

Do not make the project root instruction file enormous. Use it for project-specific rules and to import the constitution conceptually:

```md
# Project Agent Instructions

Before substantial implementation, read `.engineering/AGENTS.md`.
Read the relevant `.engineering/` documents for architecture, database, security, finance, reliability, and testing.

Project-specific decisions override the general handbook only when explicitly documented here or in an accepted ADR.

Before a new major feature, inspect `docs/project-design.md` and existing ADRs.
Never silently change established architecture or business rules.
```

## Starting a new project

1. Create the repository.
2. Add the handbook as `.engineering/` (copy/submodule/subtree).
3. Put a small project-specific `AGENTS.md` at the project root.
4. Copy `templates/project-design.md` to `docs/project-design.md`.
5. Give the agent the product idea and require it to complete the design document before substantial implementation.
6. Review important assumptions and business rules.
7. Let the agent implement in small coherent phases.
8. Require tests/checks before each phase is called complete.
9. Record major deviations or architecture changes in `docs/adr/`.

## Example first instruction to an agent

"Read AGENTS.md and the engineering handbook before modifying the project. Inspect the existing repository first. Complete/update docs/project-design.md for this product, including expected scale, database invariants, security boundaries, cost drivers, and money/tax/payment concerns if applicable. Use conventional framework-native patterns and the simplest architecture that satisfies the requirements. Do not start substantial implementation until the design is coherent. Then implement V1 in small verifiable phases and run the relevant checks after each phase."

## Updating the handbook

When an AI agent makes a recurring mistake, do not merely fix that one project. Ask whether the failure reveals a general principle. If yes, add a concise rule/checklist/example to this handbook and version the change.

Avoid rules based on personal preference alone. The handbook should encode reasons and tradeoffs.
