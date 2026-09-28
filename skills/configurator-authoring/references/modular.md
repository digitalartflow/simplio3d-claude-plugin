# Modular (snap-together) configurators

In a Modular project, shoppers drag modules (shelves, walls, roof sections) into the scene and they snap together. Modular projects need a Pro or Enterprise plan; on Starter, creating one is refused.

## What you can author

| Goal | Tool |
|---|---|
| Palette and snapping behaviour for a modular block (snap distance, one module per side, rotation) | `configure_modular_settings` |
| A module the shopper can place | `create_modular_variant`; it references a 3D model already in the scene |
| Change a module (label, thumbnail, snap sides, offsets) | `update_modular_variant` |
| Which faces of a host module another module may snap onto | `set_snap_side_constraint` |
| Remove a module | `delete_modular_variant`, a proposal the user approves. It lists every price, SKU and rule that would be left pointing at the removed module. |

A module's value never changes once created.

## Snap sides

Each module has faces: `left`, `right`, `front`, `back`, `top`, `bottom`. A snap happens when a face of the dragged module meets the opposite-facing face of a placed one.

- Enable only the faces that should connect. A roof section that only sits on walls needs `bottom` on the roof and `top` on the wall.
- `set_snap_side_constraint` blocks faces **of the host**: "Left Extra may only attach to the Main's left side" blocks every other face of the Main for that module.

## Rules you must follow

- **Ask which faces connect.** Don't work them out from bounding boxes or model names. A wrong snap graph fails silently in the shopper's view.
- Verify placement in the Simplio3D **Preview**. The editor viewport doesn't run snapping.
- Don't edit bespoke `custom` modular blocks (their modules are generated from their own settings).
- Placing modules for the shopper isn't something you author; shoppers do that in the configurator.

## Starting from scratch

With `start_workflow`, the `create-modular-configurator` workflow creates the project, inspects every module's geometry (parts, sizes, duplicate names) and reports what to configure. It deliberately stops before snapping; continue with the tools above once the user has said which faces connect.
