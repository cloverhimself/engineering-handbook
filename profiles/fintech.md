# Fintech Profile

Use for products that calculate, authorize, store, report, route, or reconcile financial value.

Priorities:
- treat money movement as a ledgered, auditable state transition;
- use exact monetary representations, never binary floating point;
- distinguish authorization, capture, settlement, refund, reversal, chargeback, and reconciliation states;
- use idempotency for externally retried operations;
- verify webhook signatures and provider references;
- separate balances derived from ledger entries from mutable display fields;
- preserve immutable financial history;
- require explicit authorization for sensitive transactions;
- apply least privilege and separation of duties where risk warrants it;
- log security-relevant administrative actions;
- reconcile internal records against processors/banks/providers;
- design duplicate, delayed, reordered, and partially failed events as normal failure cases;
- do not invent tax, accounting, KYC, AML, licensing, or regulatory rules;
- document jurisdiction and compliance dependencies separately from implementation.

Financial correctness takes priority over convenience and apparent simplicity.
