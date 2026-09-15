# Internal Tool Profile

Use for staff/admin/operations software used primarily inside an organization.

Priorities:
- optimize for correctness, speed of change, and clear permissions over public-scale complexity;
- use existing identity providers or organization auth where practical;
- enforce role/permission checks server-side even if the UI is private;
- audit destructive and high-impact administrative actions;
- make dangerous actions explicit, reviewable, and reversible where possible;
- keep data export/import tools bounded and validated;
- prefer straightforward CRUD and reporting patterns;
- avoid public-web scale infrastructure unless actual usage requires it;
- document operational ownership and who may perform sensitive workflows;
- protect internal secrets and production data from accidental exposure.
