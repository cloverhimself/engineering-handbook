# Project Structure Guidance

Folder structure should reduce cognitive load, make ownership obvious, and follow the conventions of the chosen framework before introducing custom architecture.

## General rules

- Start with the framework's normal layout.
- Group by feature/domain once the application becomes non-trivial.
- Keep transport, business rules, persistence, and infrastructure concerns distinguishable without forcing artificial layers.
- Do not create empty architectural layers just to mirror diagrams.
- Avoid giant global `utils`, `helpers`, `common`, or `services` folders.
- Keep tests close enough to the code that ownership is obvious, or use the ecosystem's standard test layout.
- Infrastructure-specific code should not leak throughout domain logic.
- The project root should remain understandable at a glance.

## Small application

A small application may legitimately use a simple structure:

```text
src/
  routes/
  controllers/
  db/
  middleware/
  app.ts
  server.ts
```

Do not force repositories, interfaces, adapters, or domain packages into a tiny CRUD application unless they solve a real problem.

## Growing backend

As domains and business rules grow, prefer feature grouping:

```text
src/
  modules/
    auth/
      auth.routes.ts
      auth.controller.ts
      auth.service.ts
      auth.schema.ts
    orders/
      order.routes.ts
      order.controller.ts
      order.service.ts
      order.repository.ts
      order.schema.ts
    payments/
      payment.routes.ts
      payment.controller.ts
      payment.service.ts
      payment.provider.ts
  infrastructure/
    database/
    email/
    storage/
  middleware/
  config/
  app.ts
  server.ts
```

Repositories are appropriate when persistence logic is substantial enough to deserve a boundary. A service should contain actual business rules or orchestration, not simply forward calls from controller to repository.

## Frontend / full-stack application

Prefer the framework's routing and component conventions. Organize shared UI separately from feature-specific UI.

Example:

```text
src/
  app/ or routes/
  features/
    checkout/
    account/
    catalog/
  components/
    ui/
  lib/
  services/
  styles/
```

Do not put every component into a global `components` directory when it belongs to one feature.

## Domain boundaries

A module should own the business concepts it changes. Cross-module calls should use clear public boundaries rather than reaching into another module's internals.

Circular dependencies are a sign that boundaries may be wrong.

## File splitting

Split a file when:
- it has multiple unrelated reasons to change;
- readers must scroll through unrelated concepts to find the relevant logic;
- a section has its own stable abstraction or responsibility;
- testability improves materially;
- merge conflicts repeatedly occur because unrelated work touches the same file.

Do not split merely because a file crosses a fixed line count.

## Generated and configuration files

Keep generated files clearly identified and do not manually edit them unless the tool expects it.

Separate environment-specific configuration from code. Never commit secrets.

## Naming

Use the naming conventions of the language/framework consistently. File names should make their role and domain obvious.

Avoid ambiguous names such as `misc`, `stuff`, `new`, `temp`, `final2`, and generic `manager` classes that accumulate unrelated behavior.

## Monorepos

Use a monorepo only when multiple applications/packages benefit from coordinated development and shared tooling. Do not create a monorepo for a single deployable simply because it looks scalable.

If using one, keep deployable apps and reusable packages explicit:

```text
apps/
  web/
  api/
packages/
  shared-types/
  ui/
```

Shared packages must not become a dumping ground for domain logic that should belong to one application.

## Decision rule

The best structure is the least surprising structure that lets a developer locate code by domain and responsibility without needing a map from the original author.
