# Dependency Discipline

Every dependency becomes part of the product's attack surface, maintenance burden, upgrade path, build graph, and operational risk.

Before adding a package, check in this order:
1. Can the language/runtime standard library do it clearly?
2. Can the existing framework do it?
3. Does the project already have a dependency that solves it?
4. Is a small local implementation simpler and safer than a new package?
5. If a package is still justified, is it actively maintained, compatible with the current runtime/framework, well-documented, appropriately scoped, and widely trusted for this use case?

Do not install multiple packages for the same concern without a documented reason.

Avoid abandoned, experimental, obscure, or unsupported libraries in production paths unless the project explicitly accepts the risk.

Do not install large frameworks to solve tiny problems.

Before replacing an existing dependency, compare migration cost, compatibility, security, maintenance, bundle/runtime cost, and actual benefit.

Pin and update dependencies according to ecosystem norms. Remove unused packages. Never add a dependency only because an AI agent is more familiar with it.
