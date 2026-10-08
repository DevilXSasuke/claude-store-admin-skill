---
name: design-store-admin
description: Design, implement, or improve an admin-only ecommerce control panel for Next.js and React using familiar WooCommerce and WordPress management workflows. Use for store back-office screens, product and variation editors, orders, inventory, refunds, customers, coupons, analytics, content, integrations, settings, RBAC and security, backend API creation, and SEO management. Exclude public storefront design.
---

# Design Store Admin

Build an operational store admin with familiar WooCommerce navigation and modern React implementation. Treat WooCommerce as a workflow reference, not a required backend. Keep the plugin generic across stores, industries, currencies, brands and providers. Derive business-specific settings only from the current user's explicit requirements and the inspected project; do not import personal memory, earlier unrelated projects, or screenshot account/plugin names into reusable instructions. Keep work scoped to staff administration; change public storefront code only when a requested admin capability needs a shared contract, and explain that dependency.

## Read the relevant references

- Read [features.md](references/features.md) for navigation, feature priorities, and detailed screen requirements.
- Read [design-system.md](references/design-system.md) before creating screens or changing visual style.
- Read [implementation.md](references/implementation.md) for tool selection, API boundaries, security, and validation.
- Read [rbac-security.md](references/rbac-security.md) for roles, capability matrices, security implementation, and negative tests.
- Read [api-design.md](references/api-design.md) when creating backend endpoints, OpenAPI contracts, integrations, or API-client management.
- Read [seo-content.md](references/seo-content.md) when adding SEO editors, metadata publication, redirects, or sitemap controls.
- Read [sources.md](references/sources.md) when checking a WooCommerce behavior or library capability. Distinguish sourced behavior from this skill's proposed design.

## 1. Inspect before designing

Read CLAUDE.md, AGENTS.md, package manifests, lockfile, existing admin routes, UI components, API clients, schemas, auth, permissions, localization, and tests. Use rg to locate existing patterns. Determine App Router versus Pages Router and preserve the established backend and package manager. Do not replace a working NestJS API with Next.js Server Actions merely to follow this skill.

Record a short route/capability map with existing, missing, and optional features. Compare any supplied screenshot with actual project components. If a screenshot is unavailable, say so and use the documented visual defaults; never claim to have inspected it.

Ask only for a missing decision that blocks implementation. Resolve routine design choices independently. Implement the requested slice; do not treat the feature catalog as authorization for a complete rewrite.

## 2. Establish the admin shell

Use a charcoal sidebar, slim top bar, pale workspace, white bordered panels, compact typography, restrained blue primary actions, and readable status badges. Include store name, environment badge, permission-aware quick create, breadcrumb, staff menu, and accessible sidebar collapse. Use real environment data, not a hardcoded Live label.

Organize navigation around Dashboard, Orders, Products, Inventory, Customers, Discounts, Analytics, Content, Media, Integrations, and Settings. Follow the sidebar hierarchy, interaction rules and page recipes in design-system.md. Adapt optional modules to the verified backend rather than hardcoding a particular business. Show authorized sections only; enforce the same permissions on the server. Keep diagnostic/developer controls inside restricted system settings.

Offer saved table views, column visibility, persistent filters, date ranges, search, pagination, and explicit bulk selection scope. Prefer operational tables and focused forms over oversized cards and decorative charts.

## 3. Plan capabilities and generate correct code

Use the feature catalog to propose a coherent admin architecture before generating screens. Map reusable AdminShell, SidebarNav, PageHeader, DataTable, FilterToolbar, StatusBadge, FormSection, MediaPicker, ActivityTimeline and ConfirmDialog components to the project's existing equivalents. Specify typed props, accessible interaction, server data contracts and state ownership. Prefer composable components over separate ad hoc implementations for each module.

For a new admin, scaffold the shell and a representative complete workflow first, then extend the authorized module set. For an existing admin, evolve compatible components and routes. Treat missing API/auth capabilities as explicit implementation work or documented gaps; never assume that a polished screen has made them functional. Keep product-specific feature flags and provider adapters outside the generic design system.

## 4. Build a complete vertical slice

For a design-only request, deliver annotated screen layouts, component states, navigation, and API requirements without implying functional integration. For an implementation request, connect a requested screen to existing authorized endpoints, then complete its loading, empty, error, validation, success, and denied states. Isolate and label any demo fixtures; never silently substitute fake API success.

Start with Orders or Products unless the user specifies another area. Include detail and edit views rather than only list mockups. Use full pages for complex order/product editing; drawers for small read-only previews; dialogs for focused confirmations.

Make save state explicit. Keep dirty fields after a failed save, prevent repeated submission, and detect concurrent edits using the backend's version/ETag contract when available. Invalidate affected queries after success. Use optimistic updates only for operations with a safe rollback, not refunds, stock adjustments, or irreversible actions.

## 5. Preserve commerce correctness

Use server-calculated totals and persisted order snapshots. Handle money in the backend's exact decimal/minor-unit representation; do not calculate payment totals with floating-point JavaScript. Render currency and locale explicitly. Keep payment, fulfillment, and order lifecycle states distinct and honor the existing transition rules.

Require backend permissions and audit events for edits, exports, integration changes, refunds, and stock adjustments. Separate gateway refunds from accounting/manual refund records. Display pending and failed gateway states honestly; never mark an order refunded solely because an administrator clicked a button. Verify duplicate submissions and webhook deliveries cannot produce duplicate effects.

Never turn an admin redesign into permission widening, production data deletion, migration execution, or automatic payment capture. Stay within the user's authorized task; produce reviewable changes before any separate deployment approval that the project requires.

## 6. Implement permissions, APIs and SEO when in scope

Use the relevant references to turn management capabilities into working server behavior. Define RBAC capabilities and resource constraints before wiring actions. Build missing APIs through the established backend rather than inventing frontend persistence. Treat SEO as admin-managed public metadata with a verified rendering path, while keeping admin pages private. Keep role management, external API credentials and publishing controls separately permissioned. Provide meaningful negative tests and report missing infrastructure instead of claiming full security or WordPress feature parity.

## 7. Verify and hand off

Run repository checks appropriate to the changed slice. Exercise the acceptance scenarios in implementation.md with isolated test data. Inspect rendered desktop and narrow layouts, keyboard interaction, Arabic RTL when enabled, and at least one role with restricted access. Record actual commands, results, and unavailable checks; do not claim visual or live gateway verification without performing it.

Report what changed, routes affected, verified behavior, remaining API gaps, and relevant risks in concise language. Identify deferred modules instead of showing dead navigation links or buttons that appear to work.
