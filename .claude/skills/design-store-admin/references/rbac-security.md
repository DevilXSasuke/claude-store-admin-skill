# RBAC and security

## Permission design

Treat RBAC as role-based access control. Derive an explicit capability matrix from current requirements; do not create privileged accounts, grant roles, or broaden existing permissions during a UI redesign. Use roles for permission bundles and combine them with record ownership, tenant, resource state and approved business constraints. Deny unknown capabilities by default. Authenticate and authorize each request server-side, including reads, mutations, exports, downloads, jobs and webhooks.

Propose the following baseline only when no role model exists. A dash means denied, and Scoped means explicitly allowed fields/records/actions, not blanket access. Adapt role names to the application.

| Capability | Owner | Catalog editor | Order support | Fulfillment | Finance | Analyst |
| --- | --- | --- | --- | --- | --- | --- |
| Product read/edit/publish | Yes | Yes | Read | Read | Read | Read |
| Order read | Yes | — | Scoped | Scoped | Scoped | Aggregate |
| Order update | Yes | — | Scoped | Fulfillment only | — | — |
| Refund create | Yes | — | — | — | Yes | — |
| Stock adjust | Yes | — | — | Yes | — | — |
| Customer personal data | Scoped | — | Scoped | Shipping only | Billing only | — |
| Personal-data export | Separate grant | — | — | — | Separate grant | — |
| Analytics read | Yes | Product only | — | Stock only | Financial | Aggregate |
| SEO edit/publish | Yes | Separate grant | — | — | — | — |
| Provider secrets / API clients | Yes | — | — | — | — | — |
| Staff / roles / security policy | Yes | — | — | — | — | — |

Separate read, create, update, delete, publish, export, configure and approval permissions. Model stable keys such as product.read, product.write, product.publish, order.read, order.update, refund.create, stock.adjust, customer.pii.read, customer.export, analytics.read, seo.write, seo.publish, api-client.manage and staff.manage. In each module distinguish the authenticated actor from user IDs, tenant IDs or roles sent by the client.

Build staff/role screens with invited/active/disabled state, permission groups, scoped grants, role change history and session revocation when the backend supports them. Prevent self-escalation, unauthorized delegation and accidental removal of the last authorized owner. Restrict audit access and redact personal data. Do not use frontend navigation visibility as enforcement.

## Security implementation surfaces

- Sessions: reuse established auth; support MFA/step-up for privileged actions where required. Use secure cookie settings suitable for the deployment, server-enforced expiry, rotation and revocation. Recheck changed permissions rather than trusting stale cached grants. Do not invent an identity provider or homegrown authentication scheme.
- API/object access: check action plus target record and tenant; apply field-level response projection and writable-field allowlists. Bound paging, uploads and jobs; rate-limit expensive and sensitive operations according to deployment needs. Prevent duplicate financial effects with idempotency and transactions.
- Browser inputs: validate on server, sanitize rich content, use parameterized queries, and prohibit arbitrary script/template execution from content/settings. Configure CSRF/origin protection for cookie-authenticated mutations; narrow CORS to trusted clients. Review CSP/frame protection and cache isolation in the current runtime.
- Uploads: restrict permitted types and size, validate content beyond the filename, generate safe storage identifiers, isolate untrusted files and authorize access. Use scanning or safe image processing when supported. Reject traversal and executable content; do not trust client MIME declarations.
- Integrations: keep secrets on the server, mask configuration values and logs, and use least-privilege provider credentials. Authenticate webhook sources, deduplicate events and validate payloads. For URL fetching or callbacks, validate destinations and block unsafe private-network access where appropriate.
- Operations: record actor, action, target, result and correlation ID for privileged activity, and protect audit retention/access. Inspect dependency vulnerabilities and secret exposure using available project tooling; report evidence and fixes without claiming certification.

These are engineering requirements to implement and verify, not a guarantee that a generated application is secure or OWASP-compliant.

## Required negative tests

Select meaningful tests for changed surfaces: anonymous call; wrong-role direct call; another tenant's ID; forbidden fields in update/export; disabled account; stale role after revocation; self-role escalation; last-owner removal; CSRF attempt where applicable; stored-script input; invalid/oversized upload; replayed webhook; duplicate refund; unbounded export. Confirm rejected operations change neither records nor inventory/payment ledgers, and log safe evidence without secrets.
