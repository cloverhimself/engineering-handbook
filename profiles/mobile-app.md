# Mobile App Profile

Use for native or cross-platform mobile applications.

Priorities:
- treat unreliable connectivity and offline/slow networks as normal;
- keep local state, cached state, and server source-of-truth responsibilities explicit;
- secure tokens and sensitive data using platform-appropriate secure storage;
- minimize startup time, network chatter, battery use, and unnecessary background work;
- design sync and retry behavior explicitly;
- handle app lifecycle transitions and interrupted operations safely;
- validate authorization server-side even when the mobile UI hides actions;
- use platform conventions for navigation, permissions, notifications, and accessibility;
- version APIs carefully because deployed clients cannot always update immediately;
- avoid shipping secrets in application bundles;
- monitor crash rates and key performance paths.
