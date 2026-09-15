# Ledger and Reconciliation

For systems that move, hold, or account for money, model financial history as append-only records rather than mutable balance fields alone.

Prefer double-entry or equivalent balanced ledger semantics when money moves between accounts or internal balances. Every posting should have a unique immutable identifier, currency, amount, timestamp, business reference, and status/context needed for audit.

A displayed balance may be cached or materialized for speed, but authoritative balance must be derivable from durable ledger entries or an equally rigorous source of truth.

Never silently edit historical financial entries. Corrections should be new compensating/reversal entries with traceable references.

Separate pending, available, reserved/held, settled, refunded, reversed, failed, and disputed states where the business requires them.

Reconciliation compares internal records against external provider/bank records. It must detect missing transactions, duplicates, amount/currency mismatches, unexpected states, and timing differences. Reconciliation jobs should be repeatable and idempotent.

Provider webhooks are evidence, not sole truth. Verify signatures and provider references; when needed, confirm authoritative status with the provider API.

Never invent accounting, tax, AML/KYC, safeguarding, or regulatory treatment. Those requirements must be verified for the jurisdiction and business model.
