# Look and feel

Use WordPress/WooCommerce administration as a navigation and density reference. If a screenshot is supplied, inspect its structural layout without treating its store identity or installed plugins as requirements. Its defining elements are a near-black sidebar, slim dark top toolbar, pale-gray workspace, white outlined widgets, compact text, blue active navigation and blue action buttons. Translate these patterns into a coherent admin system; do not replicate plugin clutter, WordPress news, update nags or irrelevant public-store screens.

## Suggested tokens

These are proposed defaults, not WooCommerce's official design tokens. Reuse existing project tokens when appropriate. Verify final rendered contrast, including hover/disabled states.

| Token | Light default | Purpose |
| --- | --- | --- |
| Sidebar | `#181B20` | Stable navigation surface |
| Workspace | `#F3F4F6` | Main background |
| Panel | `#FFFFFF` | Forms, cards and tables |
| Text | `#111827` | Primary copy |
| Muted text | `#4B5563` | Secondary information |
| Border | `#D1D5DB` | Separators and input edges |
| Primary | `#1D4ED8` | Selected navigation and primary action |
| Danger | `#B91C1C` | Destructive actions/errors |
| Success | `#047857` | Successful operational state |
| Warning | `#92400E` | Attention state text |

Use a 4px spacing scale, 6–8px control radius, 8–10px panel radius, subtle borders and minimal shadow. Use an existing UI font, or system sans-serif; use an installed Arabic-capable font for Arabic. Default body text to 14px, page headings to 24–28px, sidebar width to about 224px, top bar to 48–56px, and table rows to 44–48px. Keep one primary action per screen and secondary actions visually quieter.

## Screen composition

- Dashboard: small metric strip followed by action queues, stock alerts and recent orders. Optional sales trend only when real data exists. Hide widgets outside the viewer's permissions. Do not fill space with generic news or a blank drag zone.
- List page: title and create action, status tabs, filter/search toolbar, table, pagination. Display applied-filter chips and reset. Keep URL state shareable and exclude secrets from URLs.
- Product editor: broad main column and narrower publication sidebar; section navigation for inventory, shipping and variants. Keep save/publish state visible, show invalid field summaries and scroll/focus to the field.
- Order detail: order identity and lifecycle at top; items/totals, customer/address and payment/fulfillment panels; timeline alongside or below; refund controls permission-gated.
- Settings: section navigation and focused forms. Group related fields and explain consequences near consequential switches.

Prefer inline validation over toast-only errors. Use text plus icon for status; never rely on color alone. Keep primary save buttons visible without covering form fields. Add confirmations for consequential actions with record identity and consequence. Restore focus when dialogs close, support Escape and keyboard traversal, and label all icon buttons.

## Responsive, RTL and optional dark theme

At desktop widths show the sidebar and full tables. At tablet/mobile widths use an accessible navigation drawer and preserve essential record actions; allow horizontal scrolling within table regions rather than clipping the whole page. Test 1440px, 1024px, 768px and 390px layouts.

For Arabic use document/section direction, logical CSS properties, mirrored navigation and appropriate labels. Keep SKU, email, transaction IDs and mixed numeric content in isolated LTR spans; do not blindly reverse icons, charts or number strings. Store language selection separately from currency and timezone. Format dates with an explicit store timezone.

Default to the screenshot's light content workspace. Offer a full dark theme only when requested or already supported, using semantic tokens and equivalent contrast. Choose the admin theme from the current project's requirements independently of the storefront theme.

## Sidebar hierarchy and behavior

Use a persistent navigation rail with icons, short labels, selected-page highlight, nested items, and optional actionable-count badges. Keep menu order stable across roles; omit sections the role cannot access. Distinguish expansion from navigation: a group disclosure toggles children; a page link changes routes. Highlight the exact selected child and its parent. Restore expansion/collapse preference per staff account where supported. In collapsed mode, keep accessible names, tooltips and keyboard-reachable submenus. Do not make hover the only way to open a submenu. On narrow screens, trap focus in the open drawer, close it after navigation and return focus to its trigger.

| Section | Suggested children | Show when |
| --- | --- | --- |
| Dashboard | Overview, activity | Authorized summary data exists |
| Orders | All orders, returns/refunds, shipments | Related backend capabilities exist |
| Products | All products, add product, categories, tags, attributes, brands | Each taxonomy/type is supported |
| Inventory | Stock overview, adjustments, movement history | Inventory is managed |
| Customers | All customers, segments | Segmentation is optional |
| Discounts | Coupons, promotions | Rule engine supports them |
| Analytics | Overview, sales, orders, products, inventory, customers, taxes | Each report is authorized and implemented |
| Content | Pages, menus, banners, optional posts | Editable site content exists |
| Media | Library, uploads | Staff can manage assets |
| Integrations | Connected providers, sync jobs | Providers are configured in this project |
| Settings | General, localization, shipping, tax, payments, notifications, staff, audit/system | Capability-gated sections only |

Prefer a normal link for a section with no children. Keep account/sign-out controls at a predictable location. Use a badge for an actual actionable count, never an invented notification. Preserve a concise primary menu; move advanced configuration into settings rather than duplicating controls.

## WooCommerce-style interaction details

Give list pages status tabs with counts, a compact search box, filter dropdowns, bulk-action selector and Apply button, table checkboxes, readable row actions, pagination and column preferences. Expose row actions on focus as well as hover, and keep essential actions available on touch. Use explicit column labels, right-align numeric amounts in LTR layouts, and distinguish display identifiers from internal database keys.

Use editor sections resembling familiar product-data tabs and publication panels: basic content/media in the main area; status, visibility and save/publish actions in the side panel. Keep long forms navigable with section links and an unsaved-changes indicator. Use nested variation rows with explicit expansion, per-variation validation and manageable batch actions.

Use dashboard widgets for real operational information with clear titles and links. Make optional widget collapse/reordering accessible through controls in addition to dragging, and persist layout only when the requested scope warrants it. Provide screen preferences and contextual help as modern equivalents of WordPress Screen Options and Help; do not copy WordPress system controls that the backend cannot support.

Keep the admin visually dense enough for daily work while maintaining readable spacing. Avoid marketing hero sections, oversized headings, heavy gradients, decorative glass effects, huge KPI cards and storefront shopping patterns.
