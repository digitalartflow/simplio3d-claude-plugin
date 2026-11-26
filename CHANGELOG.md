# Changelog

All notable changes to the Simplio3D plugin for Claude. The plugin follows [semantic versioning](https://semver.org); the `version` in `.claude-plugin/plugin.json` is raised with every release.

## 1.6.0 — November 26, 2026

- New skill: UV mapping and placement regions (Simplio3D 1.19.0 — on every Simplio3D server since November 26, 2026). It follows the tools' order — inspect with `get_uv_mappings` / `get_placement_regions`, preview with `preview_uv_change` and its private preview link, then save to the draft with `set_uv_mapping` / `set_placement_regions` — explains the conventions (UV right / down, clockwise rotation, model-space frames, square = box), which changes are proposals the user approves, `restore_uv_mapping`, and that shoppers see a change only after the user publishes it from the Share dialog. Jersey personalization uses the `set-up-personalization` workflow, whose preview link arrives whole in the question's `link`. A garment modelled as one mesh has no separate back panel for a preset to find; the skill says so and asks where the panel sits instead. When the tools aren't on the user's server, the skill says so instead of improvising.

## 1.5.1 — November 23, 2026

- Proposed changes now wait 7 days for the user's approval in Dashboard → AI Changes (Simplio3D 1.17.6), not about 15 minutes, and are checked against the project when the user approves them. The pricing and workspace skills say so.
- The configurator audit explains `pricing-module-moved` (Simplio3D 1.17.3): a Unique Price or Price Table block still points at a modular block its modules moved out of, so those modules are not charged and never reach a cart. Re-pointing the block keeps its prices and SKUs but raises live totals, so the audit asks the user first.

## 1.5.0 — October 14, 2026

- Configurator authoring covers Edit Axis pivots (Simplio3D 1.17.0): number inputs now resize a part about its pivot — its own, else its group's or model's, else its origin in the 3D file — and parts set to "fixed" move from their group's or model's pivot. A part that grows the wrong way is fixed with `set_object_pivot` (a preset such as `right`, `center` or `bottom-front-right`) after checking the result with `get_model_pivots` and `preview`. One pivot on a group covers every part inside it. The earlier advice that the pivot does not affect resizing is withdrawn.
- Audit finding codes for number inputs (Simplio3D 1.17.0): `numeral-scaling-axis-conflict` (two parameters resize the same part on the same axis and multiply), `numeral-zero-reference` (a resizing input's default is 0 or unset), `numeral-nonpositive-range` (it allows 0 or less) and `numeral-min-above-max`.

## 1.4.1 — October 14, 2026

- Audit finding `material-snapshot-stale`: the fix is to assign the material to the option again (or open the variant's Appearance section in the editor so it reloads the library material). Saving the project alone doesn't refresh the option's copy; the earlier advice said it did.

## 1.4.0 — October 12, 2026

- The materials skill covers cut-out materials for logos, labels and stickers on a PNG with transparent areas (Simplio3D 1.15.2): `create_material` / `update_material` with `alphaCutoff` (0.01–1; 0 removes it), why a Transparent logo cuts a square out of an image the shopper uploads, hiding a "No logo" option with variant visibility instead of an invisible material, and assigning the material again so options pick up the change.

## 1.3.0 — October 7, 2026

- The pricing skill covers the advanced pricing steps of Pro and Enterprise (Simplio3D 1.15.0): markup and margin from a private cost, quantity tiers, discounts, setup and labor charges, shipping options and tax — created with `create_pricing_block` / `update_pricing_block` and `config`, the order quantity with `set_order_quantity`, and the staged result and status returned by `calculate_price`. Tax rates are always the user's to give; exemptions are never promised.
- Selling a project with these steps through the WordPress plugin needs plugin 2.2.0 or later (pricing and publish-readiness skills).

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
