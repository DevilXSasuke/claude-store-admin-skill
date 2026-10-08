# Official sources and provenance

Research checked 2026-10-08. Recheck official documentation for the installed version when implementing. The feature priorities, color tokens, proposed routes and optional extension guidance are authored recommendations, not official WooCommerce requirements.

| Official source | What it informs |
| --- | --- |
| https://code.claude.com/docs/en/skills | SKILL.md format, supporting resources, project/personal skill locations and slash-command invocation |
| https://woocommerce.com/document/managing-orders/ | Order management scope and detail workflows |
| https://woocommerce.com/document/managing-orders/overview-and-bulk-management/ | Order lists and bulk management patterns |
| https://woocommerce.com/document/managing-products/ | Product administration reference |
| https://woocommerce.com/document/product-csv-importer-exporter/ | Product CSV import/export and mapping concepts |
| https://woocommerce.com/document/woocommerce-refunds/ | Manual versus provider-supported refunds |
| https://woocommerce.com/document/woocommerce-analytics/ | Analytics metrics, report filters and exports |
| https://nextjs.org/docs/app/guides/authentication | Authentication and server authorization boundaries |
| https://nextjs.org/docs/app/guides/data-security | Server/client data security and Server Action access checks |
| https://ui.shadcn.com/docs/components/data-table | Composable table UI patterns |
| https://tanstack.com/query/latest/docs/framework/react/overview | Server-state fetching and cache management |

Do not assume WooCommerce core includes every commerce provider or all optional modules; many require extensions or custom integration. No WordPress installation is needed to use this skill with an existing custom backend.

## Security, APIs and SEO sources

| Official source | What it informs |
| --- | --- |
| https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html | Least privilege, default deny, request-level authorization and resource constraints |
| https://owasp.org/API-Security/editions/2023/en/0x11-t10/ | Object/function/property access, resource consumption and API integration risks |
| https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html | Secure sessions, cookie attributes, expiry and revocation |
| https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html | Upload validation, storage separation and access protection |
| https://docs.nestjs.com/security/authorization | Guards, role/capability checks and authorization patterns |
| https://spec.openapis.org/oas/latest.html | API contract and security-scheme documentation; use a toolchain-supported version |
| https://nextjs.org/docs/app/getting-started/metadata-and-og-images | App Router metadata and social image implementation |
| https://developers.google.com/search/docs/fundamentals/seo-starter-guide | Public-page indexing, metadata and SEO limitations |

The sample matrices, API paths, workflows and deliverable requirements are this plugin's proposed engineering guidance. Verify project-specific controls and consult current primary documentation for each implementation.
