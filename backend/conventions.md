# Backend Conventions

Prefer the normal conventions of the language and framework.

For a conventional HTTP backend, keep responsibilities clear:
- routes map HTTP endpoints and middleware;
- middleware handles cross-cutting request concerns;
- controllers translate HTTP input/output;
- services contain use-case/business orchestration when that logic is substantial;
- repositories/data-access modules isolate non-trivial persistence access where this adds value;
- schemas/validators define external input contracts;
- domain modules own domain-specific logic.

Small applications do not need every layer. A controller calling a data-access function directly may be cleaner than empty pass-through layers.

Controllers should not contain large business workflows. Database queries should not be scattered unpredictably across HTTP code.

Use consistent error handling and a centralized error-to-response boundary.
