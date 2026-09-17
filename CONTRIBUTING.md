# Contributing

Contributions are welcome, especially when they come from real project usage.

The handbook should evolve from observed engineering problems, not from adding rules for their own sake.

## Good contributions

Useful contributions include:

- correcting inaccurate or weak engineering guidance;
- improving unclear wording;
- reporting cases where an AI agent followed the handbook but still produced poor engineering decisions;
- adding missing guidance that repeatedly matters across real projects;
- improving source attribution;
- improving stack-specific guidance without forcing one language's conventions onto another;
- simplifying rules that create unnecessary complexity.

## Before opening a pull request

For a small correction, open a focused pull request directly.

For a substantial new rule, profile, workflow, or specialist module, open an issue first so the problem and evidence can be discussed before more handbook surface area is added.

## What to include

A good issue or pull request should explain:

1. the engineering problem;
2. what happened in a real or reproducible project;
3. why the current handbook guidance was insufficient, incorrect, or ambiguous;
4. the proposed change;
5. supporting sources when the change makes a factual or technical claim;
6. tradeoffs or cases where the proposed rule should not apply.

## Source quality

Prefer sources in roughly this order when they apply:

1. official language, framework, database, protocol, platform, or provider documentation;
2. recognized standards and security guidance;
3. established engineering books and primary technical writing;
4. experienced practitioner engineering blogs and conference material;
5. community discussions such as Reddit, forums, Medium, or social posts as supporting evidence rather than authority.

Community experience is valuable, but anecdotes should not silently become universal rules.

See [`SOURCES.md`](./SOURCES.md) for the handbook's sourcing approach.

## Keep the handbook lean

Do not add a new file or rule merely because it may be useful someday.

Prefer extending an existing section when the concern fits naturally there. Add a specialist module only when the topic has enough distinct decisions and failure modes to justify one.

The handbook should remain selective enough that AI agents can load only what they need.

## Style

Write guidance that is:

- direct;
- practical;
- language-aware but not unnecessarily language-specific;
- explicit about tradeoffs;
- clear about what is a default versus a hard requirement;
- resistant to unnecessary complexity;
- understandable by another developer without the original author's context.

Avoid presenting personal preference as industry fact.

## Verification

When changing behavior-oriented guidance, explain how the change could be validated against an AI coding agent or project scenario.

Do not claim that tests, experiments, or source verification happened if they did not.

## Pull requests

Keep pull requests focused. Avoid bundling unrelated cleanup, new modules, rewrites, and source changes into one review unless they are inseparable.

Describe what changed, why, what evidence supports it, and any meaningful downside.

By contributing, you agree that your contribution may be distributed under the repository's MIT License.
