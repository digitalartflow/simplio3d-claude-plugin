# Changelog

All notable changes to the Simplio3D plugin for Claude. The plugin follows [semantic versioning](https://semver.org); the `version` in `.claude-plugin/plugin.json` is raised with every release.

## 1.2.0 — October 2, 2026

- The materials skill covers gemstones and glass: creating a stone from one of the 15 gem presets (`create_material` with `gemPreset`), glass materials, every gemstone field, assigning a stone only to a closed mesh, lighting a jewellery project (`update_project_settings` with `environmentSource: "jewelry"`), and why stones look see-through in AR and in the WordPress and Shopify storefront blocks.
- Audit finding codes for gemstone materials: `transmission-fallback-opaque`, `transmission-thickness-zero`, `material-snapshot-stale` and `transmission-device-fallback` (Simplio3D 1.14.0).

## 1.1.0 — October 1, 2026

- Configurator authoring covers Fixed Material blocks (`set_fixed_materials`), the order of options inside a block (`reorder_variants`) and rules triggered by the modules a shopper places.
- Number inputs that resize a model: list every part that changes, and mark parts that should move instead of stretch as "fixed". The earlier advice to check the model pivot first is removed — resizing does not use it.
- The materials skill explains removing a material from an option (`assign_material` with `clear`) and setting up Fixed Material blocks.
- Workspace navigation covers the AI change history: `list_ai_changes`, withdrawing a proposal (`withdraw_pending_change`) and proposing an undo (`undo_ai_change`), which the user approves.
- Audit finding codes updated for Simplio3D 1.13.0 (two retired number-input codes replaced).

## 1.0.2 — September 28, 2026

- Shopify guidance matches the product: the Simplio3D app for Shopify is installed from the Shopify App Store and managed from the Shopify admin; Dashboard → Integrations → Shopify is only for connecting your own Shopify app.

## 1.0.1 — September 28, 2026

- Added the plugin icon and the privacy policy link that Claude's plugin directory shows on the listing.
- The README shows the Simplio3D icon with Markdown image syntax.

## 1.0.0 — September 28, 2026

First release.

- Seven skills: workspace navigation, configurator audit, configurator authoring, pricing and CPQ, materials, publish readiness, and Simplio3D help.
- Connects to the Simplio3D connector at `https://app.simplio3d.ai/mcp` (OAuth sign-in, read-only by default).
- Works in Claude on the web, desktop, mobile and Cowork, and in Claude Code.
