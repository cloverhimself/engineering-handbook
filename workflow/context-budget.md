# Context Budget and Agent Handoffs

AI agents work better when the context they repeatedly receive is small, current, and relevant.

Long chat histories, large always-on instruction files, unnecessary open files, and repeated repository exploration can consume context/tokens without improving the current task.

This workflow keeps project knowledge durable while minimizing repeated reading.

## Core principle

**Store durable project state in the repository, not in chat history. Read the minimum context required for the current task.**

Do not use one giant context file as an append-only transcript.

## Context layers

A project should separate context into layers:

```text
AGENTS.md
  ↓ always-on rules and project conventions

docs/NOW.md
  ↓ tiny active-task handoff

docs/CONTEXT.md
  ↓ stable project state and architecture facts

docs/PHASES.md
  ↓ roadmap; read when planning/status matters

docs/project-design.md + ADRs
  ↓ deeper decisions; read only when relevant

source code / tests / migrations
  ↓ inspect only for the current task
```

## 1. `AGENTS.md` — always-on instructions

Keep this concise because it may be loaded frequently.

Include only:
- project purpose in one or two sentences;
- stack;
- important commands;
- universal project constraints;
- selected handbook/profile/lifecycle references;
- high-risk invariants;
- where to find deeper context.

Do not duplicate the full handbook.

## 2. `docs/NOW.md` — active task context

This should be the smallest and most frequently refreshed context file.

It answers:
- What are we doing right now?
- Why?
- What files/areas matter?
- What is already done?
- What remains?
- What checks were actually run?
- What should the next agent do first?

Target: roughly 30–80 lines in ordinary projects. Shorter is better when complete.

Overwrite stale task details instead of endlessly appending.

## 3. `docs/CONTEXT.md` — stable project context

Store durable facts that a new agent should not need to rediscover:
- architecture summary;
- lifecycle stage;
- selected profiles;
- important domain invariants;
- auth/permission model;
- database/storage choices;
- important integrations;
- deployment model;
- accepted decisions/ADR references;
- known long-lived constraints.

Do not store session-by-session activity here.

Target: keep it concise enough to scan quickly. If a section grows large, move details into an ADR/design document and leave a short pointer.

## 4. `docs/PHASES.md` — roadmap, not session memory

Read this when:
- choosing the next milestone;
- checking project completion status;
- changing scope;
- finishing a phase.

Do not require every small coding task to reread the full roadmap.

## 5. Design docs and ADRs — on-demand context

Do not load every ADR/design document at session start.

`CONTEXT.md` or `NOW.md` should reference the exact ADR or design section needed for the current task.

Example:

```text
Relevant decisions:
- ADR-004: payment verification and webhook ownership
- ADR-007: tenant isolation strategy
```

The agent opens those documents only if the task touches those decisions.

## Cold-start protocol

When beginning a new chat/agent session:

1. Read root `AGENTS.md`.
2. Read `docs/NOW.md`.
3. Read `docs/CONTEXT.md`.
4. Verify Git branch/status and recent relevant diff/commit.
5. Read only the source files/tests explicitly relevant to the active task.
6. Open `PHASES.md`, project design, ADRs, or specialist handbook modules only when the active task requires them.

Do **not** reread old chats to reconstruct project state when the repository context files are current.

## Session-close protocol

Before ending a meaningful work session:

1. Update `docs/NOW.md` with the exact current task state.
2. Update `docs/CONTEXT.md` only if a durable fact/decision changed.
3. Update `docs/PHASES.md` only if phase status/scope changed.
4. Create/update an ADR only for a meaningful architectural decision.
5. Record checks actually run and their current result.
6. Remove stale next-actions and completed blockers.

## Context hygiene rules

- Do not paste whole chat summaries into repository context files.
- Do not duplicate information across `AGENTS.md`, `NOW.md`, `CONTEXT.md`, `PHASES.md`, and ADRs.
- Prefer links/references to detailed docs over copying them.
- Delete stale context rather than preserving it "just in case"; Git history already preserves previous versions.
- Keep always-on instructions short and broadly applicable.
- Use task/path-specific instructions when supported rather than loading stack-specific rules globally.
- Do not attach/open unrelated large files for a small task.
- After switching to an unrelated problem, start a fresh chat/session when practical.
- If an agent supports compaction/summarization, compact long sessions before continuing them indefinitely.

## Multiple agents

When several agents work on the same repository:

- `CONTEXT.md` is shared stable understanding.
- `PHASES.md` is shared roadmap.
- `NOW.md` reflects the active task on the current branch/workstream.
- Git commits/branches are the source of truth for actual code state.

For parallel independent work, each branch may maintain its own `NOW.md` until integration. Do not let one agent overwrite another branch's active-task context blindly.

## Preventing stale claims

Context files are hints, not proof that the code still matches them.

A new agent must verify claims that matter to its task against:
- current code;
- current schema/migrations;
- test output;
- Git diff/status.

Never assume "tests pass" from an old context entry after code changed.

## Context budget decision rule

Before reading another file, ask:

> Is this information needed to make the current change correctly?

If no, defer it.

The goal is not minimum knowledge. It is **minimum sufficient context**.