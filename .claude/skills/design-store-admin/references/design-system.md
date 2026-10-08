# Look and feel

Use the supplied WordPress/WooCommerce screenshot as a navigation and density reference. Its defining elements are a near-black sidebar, slim dark top toolbar, pale-gray workspace, white outlined widgets, compact text, blue active navigation and blue action buttons. Translate these patterns into a coherent admin system; do not replicate plugin clutter, WordPress news, update nags or irrelevant public-store screens.

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

Default to the screenshot's light content workspace. Offer a full dark theme only when requested or already supported, using semantic tokens and equivalent contrast. A dark storefront preference does not automatically require a dark admin.
