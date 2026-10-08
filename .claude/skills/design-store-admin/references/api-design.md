# API creation and backend guidance

## Scope and backend choice

Create APIs only for requested admin capabilities or missing backend contracts identified during inspection. Reuse the current API architecture, database, auth, validation and job infrastructure. For an existing NestJS service, add controllers/services/DTOs/guards there. For a Next.js-owned backend, use Route Handlers or the established Pages API routes. Server Actions may support internal UI mutations but are not a documented external integration API. Avoid two services independently owning the same commerce transactions.

Distinguish two requests: building application endpoints for the admin, and adding an API-client management screen for external integrations. Neither means an unrestricted code generator or arbitrary SQL console inside the admin. Enable external access only within the user's authorized scope.

## Contract before code

For each operation define method/path, authentication, capability, tenant/object constraints, request/response schemas, validation, pagination/filter/sort semantics, errors, concurrency behavior and side effects. Use existing path conventions; the following are examples.

| Example operation | Capability | Main rules |
| --- | --- | --- |
| GET /api/admin/products | product.read | Bounded pagination, allowed filters/sorts, scoped fields |
| POST /api/admin/products | product.write | Allowlisted DTO, unique SKU handling, draft default |
| PATCH /api/admin/products/:id | product.write | Object scope, stale version detection, field validation |
| POST /api/admin/products/:id/publish | product.publish | Required content checks, atomic state transition |
| GET /api/admin/orders/:id | order.read | Tenant/record scope, personal-data projection |
| POST /api/admin/orders/:id/refunds | refund.create | Eligible balance, exact money, idempotency, provider state |
| POST /api/admin/inventory/adjustments | stock.adjust | Reason, actor, stock invariants, transactional ledger |
| POST /api/admin/imports | product.import | Dry-run/job workflow, bounded size, row-level outcomes |
| POST /api/admin/exports | Separate resource export grant | Same filters/scope as read, authorized download |
| PATCH /api/admin/content/:id/seo | seo.write | Supported metadata schema, URL and locale validation |
| POST /api/admin/api-clients | api-client.manage | Server-issued credentials, explicit scopes, audited lifecycle |

Use structured validation failures, safe error codes and correlation IDs. Preserve project conventions for 401/403 and choose consistent 404 behavior when record existence must be hidden. Define conflict responses for stale edits, retries for transient failures and limits for large jobs. Do not reveal stack traces, SQL or provider secrets.

Document APIs with OpenAPI using a version supported by the installed tooling, then generate or maintain typed clients through the project's existing process. Describe security schemes and operation-level requirements. Generate controllers, domain services, persistence boundaries and tests together; docs alone do not enforce authentication. Verify the documented contract matches actual responses.

## Transactions and integrations

Use validated domain services for order transitions, totals, refunds and stock. Store exact money and immutable purchase snapshots. Coordinate database transactions and durable provider/job state; a database rollback cannot undo a payment provider request. Add idempotency keys with actor/resource scoping, same-payload replay behavior and conflict detection. Handle provider timeouts as unknown/pending until reconciled, not automatic success or definitive failure.

Use background jobs for long imports/exports/sync operations with authorization at enqueue and execution, status/progress, safe cancellation and partial failure reporting. Preserve authorization on download artifacts. Deduplicate signed webhooks, reconcile state transitions and audit retries.

## External API clients

If requested, provide scoped clients with name, owner, allowed operations, expiry, last use, rotation and revocation. Generate credentials on the server using the established auth platform; show secret material once and never log it. For opaque local API tokens, store a secure verifier rather than retrievable raw tokens. Do not replace an established OAuth service with custom tokens. Document rate limits and separate sandbox/live access. Test scope enforcement, cross-tenant denial and revocation.

## Validation and delivery

Test schema validation, permission and object/tenant boundaries, pagination, concurrency, job authorization and duplicate effects. Run contract/type checks and targeted integration tests. Mark endpoints unavailable when dependencies are missing. Never seed production users, reveal credentials or apply database migrations merely to demonstrate generated code.
