# SEO administration and publishing

## Admin management scope

Add SEO controls for public products, categories and content; keep private admin pages authenticated and excluded from public search features. The plugin remains admin-focused: change public rendering only for the minimal metadata/publishing contract requested. A stored SEO field has no effect until the public page actually consumes it.

Provide a focused SEO editor with title, description, slug, canonical URL, index/follow preference, social title/description/image, media alt text and locale-specific values when supported. Support draft previews and explicit publish permission. Show which values are overrides versus defaults. Provide a search/social preview as an approximation, not a promise of how search engines display the page. Character counts are editing aids, not guaranteed ranking rules.

## Content and URL rules

- Derive metadata defaults from genuine product/content fields and allow permission-controlled overrides.
- Validate slugs for conflicts, length and reserved routes. When a published URL changes, propose a redirect mapping rather than silently breaking links.
- Validate canonical/social URLs and asset references. Never allow untrusted script markup in metadata.
- For localized sites, store per-locale metadata and define canonical/hreflang relationships using supported routing. Do not add locales the application does not support.
- Define draft, preview and publication state consistently across content and SEO; preview must not expose private content through public caches or sitemaps.

## Rendering and technical SEO

Use the installed Next.js router's metadata mechanism: App Router metadata/generateMetadata and metadata routes, or the established Pages Router head/sitemap implementation. Avoid duplicated title/canonical tags. Preserve escaping and validate any structured data before embedding; safely serialize it so user input cannot terminate a script element.

Offer sitemap/robots management through safe structured settings rather than arbitrary files when appropriate. Include only intended public published URLs in sitemaps; exclude admin, private account data and preview URLs. Use noindex for admin pages as defense in depth alongside authentication. Robots rules are crawl instructions, not access controls, and blocking crawl alone does not reliably remove a URL from search results.

If product structured data is requested, derive price/currency/availability from real persisted data and only publish actual supported reviews/ratings. Follow current Google Search Central and schema requirements; do not fabricate review data or imply guaranteed rich results. Use redirect targets constrained to intended destinations, validate chains/loops and require publish/configure permission for production changes.

## SEO dashboard and checks

Optional audit views may flag missing titles/descriptions/alt text, slug conflicts, broken internal references, canonical inconsistencies, unpublished sitemap entries and redirects. Show reproducible findings and severity/action, not an invented universal SEO score. Keep crawling within authorized domains and scope, and bound background scans.

Verify field persistence, locale/default fallback, permitted publication, actual rendered metadata, canonical URLs, sitemap inclusion/exclusion, structured-data escaping and redirect behavior. Distinguish checks actually executed from suggested audits. Do not claim ranking improvements or full SEO parity with commercial WordPress plugins.
