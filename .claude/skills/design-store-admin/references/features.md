# Admin feature catalog

Use this as a capability menu, not a requirement to implement everything at once. Preserve existing route conventions; the paths below are proposed defaults.

| Module / route | Core management tools | Detail and operational behavior |
| --- | --- | --- |
| Dashboard `/admin` | Date-range sales summary, orders needing action, low/out-of-stock counts, recent activity | Link each metric to its filtered list; show freshness, currency, timezone, comparison period, and real integration alerts; make widget arrangement optional |
| Orders `/admin/orders` | Status views, search by order/customer/email/SKU, date/payment/fulfillment filters, sortable table, bulk actions, export | Detail page with immutable purchased item snapshots, addresses, totals, discounts, shipping, payment reference, timeline, internal notes versus customer notes; manual order creation only with server totals |
| Products `/admin/products` | Search, filters, thumbnails, SKU, type, price, stock, publication status, category/brand, bulk edit, import/export | Editor sections: General, Inventory, Shipping, Attributes, Variations, Linked products, SEO, Translations; draft/publish controls, media ordering, validation, safe preview |
| Inventory `/admin/inventory` | Stock by SKU/variation, low-stock thresholds, backorders, movement history | Adjustments require quantity, reason, actor and version; show reserved versus available stock if the backend supports it; do not restock twice after refunds |
| Customers `/admin/customers` | Search, order count, total spend, last order, guest/account distinction | Profile, addresses, order history, consent visibility; restrict personal data and exports; never show passwords or provider secrets |
| Discounts `/admin/discounts` | Fixed/percentage coupons, start/end dates, limits, eligible products/categories, minimum spend | Define timezone, stacking, exclusions and usage counts; validate rules server-side; show draft/active/expired status |
| Analytics `/admin/analytics` | Sales, orders, products, stock, coupons, customers and tax summaries when supported | Filters and CSV exports share the same dataset and permission rules; define gross/net/refunds/tax/shipping formulas and excluded statuses; multiple currencies require separate reporting or documented conversion |
| Content `/admin/content` | Pages, menus, banners, homepage sections, policy text, optional blog | Draft preview, scheduled publication only if supported, version history and locale status; expose allowed structured blocks rather than arbitrary executable code |
| Media `/admin/media` | Upload, search, alt text, image selection, usage information | Validate size/type on server, authorize access, process images safely, confirm before deleting referenced assets |
| Reviews `/admin/reviews` | Pending/approved/rejected views, moderation, product links | Preserve author and verification metadata; show review moderation only if product reviews exist |
| Integrations `/admin/integrations` | Provider status, last sync, masked configuration, retry/error history | Separate sandbox/live mode; redact request/response logs; display background job state and documented retry scope |
| Settings `/admin/settings` | Store identity, currency/locale, shipping, tax configuration, notifications, staff roles | Permission-gated sections, masked secrets, audited changes, explicit save; display operational tax settings without claiming legal compliance |
| System `/admin/settings/system` | Audit history, job status, import history, health diagnostics | Restrict to authorized staff; list actual services and redact sensitive diagnostics; represent deployments/backups as external systems unless integrated |

## Product and variation rules

Support simple and variable products when the data model supports them; make grouped/external/digital products optional. Include price, scheduled sale, SKU uniqueness, stock mode, dimensions, shipping class, categories, tags, brand, short/long descriptions, gallery, publication and visibility. Keep product-level defaults distinct from variation overrides. Avoid uncontrolled combinatorial variation creation; preview generated combinations first.

For CSV import, provide upload, column mapping, validation preview, explicit create/update matching rules, job progress, per-row error download and completion summary. Validate duplicate identifiers and variation-parent relationships. Use a dry run before mutation and bounded background processing for large files. Escape formula-leading cells in spreadsheet exports. Do not claim WooCommerce CSV compatibility unless the implemented schema and tests establish it.

## Order and refund rules

Map the actual backend states before exposing actions. WooCommerce-inspired labels may include Pending payment, Processing, On hold, Completed, Cancelled, Failed and Refunded; do not force these onto an incompatible state model.

Refund UI: choose eligible line quantities/amounts, display refundable balance, separate shipping/tax treatment, require reason, offer restock only when supported, select gateway versus manual record, confirm amount/currency/method, then show persisted result. Preserve gateway failure codes and correlation IDs with sensitive fields redacted. Manual records do not transfer money. Partial refunds remain visible separately from full-order status. Bound retries and use server idempotency.

Bulk actions must state whether selection means this page or all filtered records. Show affected count, allowed action, confirmation where consequential, background progress and partial failures. Recheck permission and record state for every item on the server.

## Role model

Reuse existing role names and capabilities. If absent, propose: owner/super admin, store manager, catalog editor, order support, fulfillment and analyst. Define capability-level access such as product.write, order.read, refund.create, customer.export, analytics.read, integration.configure and staff.manage. Do not equate order support access with permission to issue refunds. Exclude unauthorized data from response payloads as well as navigation.

## Delivery priority

1. Existing shell/auth integration, products and orders with detail/edit states.
2. Inventory, customers, discounts, imports/exports and operational integrations.
3. Analytics, content/media, staff settings, audit history.
4. Optional saved dashboard layouts, advanced segmentation, additional provider adapters and domain-specific extensions.

Change this ordering to match the requested task and verified backend readiness.

## Generic capability extensions

Expose these only when requested and backed by a real data/service contract: returns/RMA, downloadable products, subscriptions, multi-location inventory, multistore/tenant management, shipping labels, abandoned checkout reporting, scheduled promotions, automated notifications and accounting reconciliation. Show extension configuration as supported provider modules rather than WordPress plugin installation controls.

Keep store name, currency, tax labels, timezone, locale, brands, product categories and provider names configurable. Do not select a country, gateway, accounting service, product industry or brand without current project evidence. Maintain a reusable generic core and add business-specific adapters in the consuming application.

## RBAC, APIs, SEO and administration extensions

| Module | Management functions | Read for implementation |
| --- | --- | --- |
| Staff and roles | Invitations, account state, permission matrix, scoped grants, session revocation, audit history | rbac-security.md |
| Security settings | Existing MFA/session policy, privileged-action controls, security events and redacted diagnostics | rbac-security.md |
| API access | API documentation, scoped integration clients, expiry/rotation/revocation, usage and errors | api-design.md |
| SEO | Product/page/category metadata, defaults/overrides, publication, slug changes, redirects, sitemap status | seo-content.md |
| Operations | Imports/exports, background tasks, notification templates, integration failures and authorized retries | api-design.md and implementation.md |

Keep API documentation and client management distinct from implementing the backend itself. Keep SEO on products/content editors plus optional centralized audits, rather than adding redundant standalone settings for every field. Expose only settings that the actual services can enforce.
