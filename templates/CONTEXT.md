# Project Context Handoff

This file is the durable handoff between AI agents, developers, and new chat sessions. Keep it concise, factual, and current.

## Project

Name:
Purpose:
Primary users:
Current stack:
Repository/branch:

## Current state

Current phase:
Last completed milestone:
What is working now:
What is partially implemented:
Known broken/incomplete areas:

## Important architecture

Key modules/services:
Database/storage:
Authentication/authorization:
External integrations:
Deployment/runtime:

## Decisions that must not be rediscovered

- Decision:
  Reason:
  Reference/ADR:

## Active assumptions

- Assumption:
  Confidence:
  Needs confirmation from:

## Verification state

Last verified commit:
Tests actually run:
Checks actually run:
Known failing checks:
Unverified claims from prior work:

## Current task

Goal:
Files/areas likely involved:
Constraints:
Definition of done:

## Next actions

1.
2.
3.

## Risks / watch-outs

- 

## Handoff protocol

Before ending a meaningful work session, update this file with the new state and verification results.

When starting a new session or switching agents:
1. read root `AGENTS.md`;
2. read `docs/CONTEXT.md`;
3. read `docs/PHASES.md`;
4. inspect referenced ADRs/design docs;
5. verify Git branch/status before changing code;
6. never assume a previous agent's stated test result is current if the code has changed since.

Do not turn this into a chat transcript. Store only durable facts, decisions, verified state, assumptions, and the immediate handoff.
