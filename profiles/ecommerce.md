# Ecommerce Profile

Use for stores selling physical or digital goods.

Priorities:
- model products, variants, pricing, inventory, carts, orders, payments, fulfillment, refunds, and notifications as distinct concepts;
- snapshot price, tax, discount, shipping, and item details at order time;
- make checkout and payment flows idempotent;
- prevent overselling with appropriate inventory consistency controls;
- treat order status transitions as an explicit state machine;
- verify payment provider callbacks server-side;
- separate catalog availability from inventory truth;
- support reconciliation between orders and payments;
- retain auditable financial history;
- design for pagination and indexed product queries;
- consider image/storage/CDN costs and bandwidth;
- define cancellation, return, refund, and partial-refund rules explicitly.

Never derive historical order totals from current product data.
