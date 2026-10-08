# Claude Store Admin Skill

A Claude Code skill for designing and implementing an admin-only Next.js/React ecommerce panel inspired by WooCommerce. It is a reusable instruction package, not a working admin application or a WordPress dependency.

## Purpose

Guide Claude Code to create or improve a feature-rich admin panel with familiar WooCommerce look and feel: hierarchical dark sidebar, compact top bar, light workspace, actionable dashboard widgets, operational tables, product-data sections and focused settings. Generate reusable, typed, accessible Next.js/React components connected to the consuming project's actual APIs. Keep the work limited to admin management.

## Scope

Products and variations, orders and refunds, stock, customers, coupons, analytics, content/media, provider integrations, settings, staff permissions and audit trails. Includes a WooCommerce-inspired visual system, EN/AR and RTL requirements, tool-selection guidance and acceptance scenarios. The plugin is generic across businesses, brands, countries and providers; discover each application's configuration and integrations from its own code and explicit requirements.

## Install from the Claude Code marketplace

Run these commands in your terminal:

```bash
claude plugin marketplace add DevilXSasuke/claude-store-admin-skill
claude plugin install store-admin@store-admin-marketplace
```

Or inside Claude Code:

```text
/plugin marketplace add DevilXSasuke/claude-store-admin-skill
/plugin install store-admin@store-admin-marketplace
```

Then invoke the installed plugin skill:

```text
/store-admin:design-store-admin Design my WooCommerce-style admin panel for Next.js/React with English and Arabic support. Inspect existing APIs and permissions first.
```

This repository hosts a self-managed marketplace. It is not an Anthropic official-directory listing. No MCP servers, credentials, hooks or executable install scripts are required.

To receive future releases:

```bash
claude plugin marketplace update store-admin-marketplace
claude plugin update store-admin@store-admin-marketplace
```

## Manual installation (alternative)

Copy `.claude/skills/design-store-admin` from this repository into the same path in your website repository. Keep its `references` folder beside `SKILL.md`.

For all local projects, copy the complete folder instead to `~/.claude/skills/design-store-admin`.

## Use in Claude Code

```text
/design-store-admin Design and implement my admin products and orders screens. Inspect the existing Next.js/React UI and NestJS API first. Follow the WooCommerce-style light workspace and dark sidebar. Support English/Arabic and preserve existing roles and backend contracts.
```

For design without code changes:

```text
/design-store-admin Design-only: propose admin navigation, screens, component states and API requirements for my store. Do not modify code.
```

## Contents

- `SKILL.md`: inspection, design, implementation and handoff workflow.
- `references/features.md`: navigation and management features.
- `references/design-system.md`: visual tokens, screen patterns, accessibility and RTL.
- `references/implementation.md`: recommended tools, boundaries and verification.
- `references/sources.md`: official documentation and provenance.

## RBAC, security, APIs and SEO

Version 1.2.0 adds role/capability matrices, record/tenant/field constraints, staff and API-client management guidance, security implementation and denial tests, backend endpoint/OpenAPI creation, and SEO editor-to-public-renderer wiring. These are instructions to generate and verify code; they do not certify an application, provision accounts/credentials or guarantee WordPress plugin parity.

```text
/store-admin:design-store-admin Build the admin products and orders workflows, define RBAC permissions, implement missing APIs in the existing backend, and add product/page SEO management. Preserve the WooCommerce-style shell and verify security and persistence.
```

- `references/rbac-security.md`: capability matrix, sessions, security controls and negative tests.
- `references/api-design.md`: endpoints, OpenAPI, domain services, jobs and external API clients.
- `references/seo-content.md`: metadata editors, publishing, redirects, sitemaps and rendering checks.

## Defaults and limits

Retain installed libraries and existing APIs. Proposed tools include Tailwind/shadcn, TanStack Table/Query, React Hook Form/Zod and Playwright when appropriate. Do not invent API success, widen permissions or issue live payments/shipping/SMS as part of UI testing. The skill does not configure or require any MCP service.

Official documentation research checked 2026-10-08. Syntax validation and a design-only scenario check passed; no store implementation or live provider testing is included.
