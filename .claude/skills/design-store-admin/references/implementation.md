# Tools, architecture and verification

## Tool selection

These are suggested tools, not mandatory dependencies. Inspect package.json and lockfile first; retain compatible installed choices and check current official documentation before adopting a new API. Avoid adding several competing UI or data frameworks.

| Need | Suggested option | Selection rule |
| --- | --- | --- |
| Application | Existing Next.js + React + TypeScript | Preserve router, monorepo and backend boundaries |
| Styling/components | Tailwind CSS + shadcn/ui | Reuse installed system; verify component accessibility rather than assuming it |
| Tables | TanStack Table | Use controlled server filtering/sorting/pagination for real datasets; do not sort only one fetched page |
| Server data | TanStack Query | Useful for interactive polling/mutations; preserve SWR or existing data layer instead of duplicating it |
| Forms | React Hook Form + Zod | Reuse established validators; enforce validation on backend too |
| Icons | Lucide React | Consistent size and accessible labels; reuse current icon set |
| Charts | Recharts or existing library | Optional and backed by actual data; provide accessible summaries |
| Localization | Existing i18n or next-intl | Implement both translations and RTL; avoid a framework migration for one screen |
| Rich content | Existing sanitized editor; Tiptap if needed | Limit allowed nodes and links; sanitize on the server |
| Tests | Existing runner; Vitest/RTL and Playwright if absent | Focus on commerce behavior, API authorization and usable screens |
| Component isolation | Storybook when already used | Optional; do not install solely for a small edit |

Do not assume MCP tools are installed. Use repository reads, shell, official docs and available browser/test tools as needed. Keep provider credentials out of Claude prompts, code, screenshots, browser bundles and logs.

## Boundaries and data contracts

Keep client interactivity in focused components. With App Router, use Server Components for authorized initial reads where appropriate; do not forward raw database models to clients. With Pages Router, use the project's established data-loading pattern. Keep private admin data out of static/public caches; verify cache keys and isolation across users/tenants.

If a NestJS/API service owns transactions, call it through the existing typed client; do not write directly to its database from the admin. Centralize DTOs or generated OpenAPI types where the project supports them. List APIs must implement matching filtering, sort, paging, total/count semantics, and stable identifiers. Restrict sort/filter fields server-side. Return field-level validation and a safe correlation ID for unexpected errors.

Check authentication and capability at each backend read/mutation, Server Action, Route Handler and export endpoint. A layout redirect or middleware check alone is insufficient. Authorize record/tenant ownership, allowlist writable fields and prevent mass assignment. Use the established secure session/cookie and CSRF/origin protections. Audit actor, target, operation, timestamp and safely redacted changes. Sanitize rich text and constrain uploads.

Keep provider integrations on the server. Validate webhook signatures, store event IDs, reconcile pending provider operations and make mutations idempotent. Treat order state, refund ledger, stock movements and accounting documents as coordinated domain operations rather than independent UI toggles.

For a missing backend capability, show a clearly unavailable action with the reason when useful, or omit it. Define the necessary endpoint contract and implement it only within scope. Do not create decorative success toasts that conceal missing persistence.

## Work sequence

1. Inspect repository and map requested capabilities to actual routes/services.
2. State a short implementation slice and reuse plan; continue unless a blocking decision exists.
3. Build/extend shared shell and table/form patterns only as needed.
4. Complete one list/detail/edit workflow with real APIs and all UI states.
5. Validate auth, state transitions, concurrency and errors; then extend modules in scope.
6. Run checks and inspect rendered layouts; report evidence and remaining gaps.

## Acceptance scenarios

Select the scenarios relevant to the change; use isolated fixtures and sandbox providers.

- Anonymous requests and users without a capability cannot retrieve protected data or mutate it by directly calling endpoints.
- Hidden navigation does not leave export/report/refund endpoints accessible to the wrong role; responses omit fields the viewer cannot read.
- Product edits persist, reload correctly, show invalid fields, preserve dirty input after failure and detect stale writes when supported.
- Server filtering, sorting, counts, saved views and export agree on the same dataset; table empty/loading/error states are usable.
- Variation edits do not overwrite sibling SKUs, prices or stock; bulk/import validation reports duplicates and partial failures.
- Order status changes obey the backend's transition matrix; purchased line-item snapshots survive catalog edits.
- Refund duplicate submission, gateway timeout/failure, partial refund and successful webhook settlement display correct persisted outcomes; manual records never claim money was transferred.
- Stock adjustments and optional restocking are audited and applied once, including retries.
- EN/AR labels, RTL layouts, LTR identifiers, keyboard focus, readable contrast and narrow tables remain usable.
- Rich-text/upload validation, private-data cache isolation and redacted integration errors hold for changed surfaces.
- Mock/demo fixtures cannot be mistaken for live records or shipped in production paths.

Run existing typecheck, lint and relevant build/test commands from package scripts, not invented commands. If the environment lacks backend access, browser tooling or sandbox credentials, report that limitation and mark affected scenarios unverified. Screenshot inspection complements automated tests; neither proves live payment correctness.
