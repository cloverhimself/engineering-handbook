# Wallet Profile

Use for products that hold or represent balances, credits, stored value, or asset positions.

Priorities:
- treat the ledger as the source of truth for balances;
- prefer immutable double-entry or equivalent auditable postings for transferable value;
- separate available, pending, locked, and settled balances when the domain requires it;
- make every credit/debit operation idempotent;
- use unique transaction references and explicit state transitions;
- never update balances without a corresponding traceable transaction record;
- protect withdrawals/transfers with strong authorization and risk controls;
- design replay, duplicate webhook, timeout, and partial failure handling explicitly;
- reconcile external rails/providers against internal ledger entries;
- use exact numeric representations and explicit currencies/assets;
- document fee, spread, conversion, and rounding rules;
- never invent KYC, AML, custody, tax, or regulatory requirements.

For high-value systems, require independent review of ledger invariants and reconciliation logic before production launch.
