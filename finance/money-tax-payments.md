# Money, Tax, Billing, and Payments

Financial software must preserve exactness, history, explainability, and auditability.

## Money representation

Use integer minor units (for currencies where that model is correct) or exact fixed-precision decimals. Never rely on IEEE-754 floating-point for authoritative totals.

Store currency with monetary values. Do not assume every currency has two decimal places.

Define rounding policy explicitly and apply it at the correct stage.

## Order/pricing snapshots

Historical transactions should preserve the values used at purchase time, including product description/SKU where required, unit price, quantity, discounts, shipping, fees, tax basis, tax, currency, and final total.

Do not derive historical invoices from mutable catalog data.

## Payments

Keep internal order/payment identifiers distinct from provider references. Enforce uniqueness where provider semantics require it.

Payment initialization, callbacks/webhooks, and verification must be safe under duplicate delivery. Never mark an order paid based solely on a client redirect.

Verify provider signatures and/or server-to-server status as required by the provider.

Persist payment attempts and relevant provider state for reconciliation without storing prohibited card data.

Support explicit states such as pending, succeeded, failed, cancelled, refunded/partially refunded when the business requires them.

## Reconciliation

The system should be able to explain why internal financial state matches or differs from the payment provider. Reconciliation jobs/reports should identify missing, duplicated, mismatched, or unresolved transactions.

## Tax

Tax rules are not universal software constants.

Never guess:
- tax/VAT/GST rates;
- thresholds;
- nexus/place-of-supply rules;
- exemptions;
- inclusive vs exclusive treatment;
- withholding;
- invoice numbering/content requirements;
- filing/remittance obligations.

Treat jurisdictional tax requirements as verified business/legal/accounting inputs. Keep tax configuration versioned where historical reproducibility matters.

Store enough information to explain the calculation later: jurisdiction, category if relevant, taxable base, applied rate/rule identifier, tax amount, currency, and timestamp/config version.

External tax engines may be appropriate when jurisdictional complexity exceeds what the product should maintain internally.

## Fees and profitability

Model gross amount, processor fees, platform/service fees, refunds, chargebacks, taxes collected, taxes borne by the business, and net settlement separately when relevant.

Do not confuse revenue with cash received or payment volume.
