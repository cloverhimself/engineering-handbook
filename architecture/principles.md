# Architecture Principles

Architecture exists to manage change, risk, scale, and operational constraints. It is not a competition to use the most patterns.

## Defaults

Use a modular monolith for a typical early-stage product unless separate services are justified by strong organizational, operational, security, or scaling boundaries.

Keep application servers stateless where practical. Put durable business state in durable systems.

Treat external systems as unreliable boundaries.

Prefer explicit interfaces at true boundaries: database, payment provider, email provider, storage provider, queue, external API. Avoid wrapping every internal function behind an interface.

## Tradeoff method

For major decisions record:
- context and constraints;
- chosen option;
- alternatives considered;
- benefits;
- drawbacks;
- operational cost;
- financial cost;
- security implications;
- migration/reversal difficulty;
- trigger for revisiting the decision.

A choice with no acknowledged downside probably has not been evaluated carefully enough.
