# Simplio3D pricing block types

| Type | What it does |
|---|---|
| `base-price` | A fixed starting price. Always present and can't be deleted. |
| `price-group` | A price per variant of one or more linked option blocks (dropdown, select-material, checkbox, toggle, carousel, modular, number-input). |
| `price-table` | A 1-D or 2-D lookup: the price at the intersection of two selections (for example Width × Height). An axis must be a single-choice block, a number input or a modular block. |
| `unique-price` | Modular projects: prices a module by how many are placed, optionally depending on another selection. |
| `variable` | A named number used in the formula: a slider value, or a value that depends on a selection. |

## Number inputs

When a price group, table axis or variable is linked to a number input, each numeric parameter's price is **per unit**: the shopper's value × the unit price.

## Formula

The formula combines blocks with `+ − × ÷` and parentheses. With no formula (or an invalid one), every enabled block is added up. With a formula, only the blocks it names count.

## SKUs

Price groups, variables, price tables and unique prices can each carry a SKU per variant or cell (Enterprise Modular projects). A Shopify "SKU-matched cart" checkout uses them to add real store products to the cart, so a missing or duplicate SKU breaks that line at checkout.

## Tax and display

Currency, symbol position, decimals and tax (inclusive or exclusive, with a rate) are project settings (`get_project_settings`). `calculate_price` applies them to its total.
