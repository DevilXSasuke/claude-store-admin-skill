# Optional GameX profile

Apply only when the project is GameX. Treat this as a user-provided direction and candidate capability list; verify current implementation before making changes.

- Store admin for gaming PCs, components, DEVO and EMG products; support product brands and configurable merchandising order, with DEVO before EMG when requested.
- English/Arabic product fields and admin locale, AED formatting, explicit Asia/Dubai store timezone. Do not assume every field already has a translation.
- Candidate stack: Next.js storefront, React admin, NestJS API, PostgreSQL, Redis, OpenSearch, pnpm monorepo. Preserve actual installed architecture.
- Candidate integrations: Network International, Tabby, Tamara, EMX shipping, D7 SMS and Wafeq accounting. Add provider configuration/status/log screens only when the corresponding server integration exists or implementation is explicitly requested.
- Keep sandbox/live provider state prominent and secrets masked. Do not send a real SMS, create a live shipment, refund a payment or issue an accounting document merely to test a redesign.
- Treat invoices, credit notes and refunds as distinct linked records. Preserve numbering, existing ledger history and backend permission rules.
- Offer shipping tracking, notification templates, invoice/credit-note links and integration retry visibility through verified capabilities. Restrict reports and finance links according to the actual role model.
- Optional Amazon/Noon marketplace reconciliation requires real settlement APIs/files and separate scope; do not promise it as a core WooCommerce feature.

The screenshot represents the former WordPress admin's visual direction. Plugin names in it are not requirements to reimplement WordPress plugins in Next.js.
