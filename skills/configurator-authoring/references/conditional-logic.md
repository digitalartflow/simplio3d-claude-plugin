# Conditional logic in Simplio3D

A rule lives **on the block it affects** and watches one or more source blocks.

Example: "show *Footrest* only when *Frame* is *Deluxe*" is a rule on the *Footrest* block with `action: show` and a condition on *Frame*.

## Actions

- `show`: the target starts **hidden** and appears only while the conditions match.
- `hide`: the target starts **visible** and disappears while the conditions match.

Picking the wrong one is the most common mistake. "Only when" wording means `show`. "Unless" or "not when" wording usually means `hide`.

## Scope (what the rule affects)

| targetScope | Affects |
|---|---|
| `block` | The whole option block |
| `variants` | Specific choices inside the block (not supported on "From Category" material blocks) |
| `3d` | Whole 3D objects (model roots or named groups) |
| `3d-parts` | Individual meshes inside a model |
| `materials` | Material choices |

For `3d` and `3d-parts`, every name is checked against the real model file. Get names from `list_model_parts`, `get_scene_hierarchy` or `find_scene_objects`.

## Conditions

- `is-selected`, `is-not-selected`: a source variant is or isn't chosen.
- `greater-than`, `less-than`, `equals`, `between`: a number input's value.
- `operator: all` needs every condition (AND); `any` needs one (OR).

A rule with no conditions never fires. An `all` rule that requires the same variant to be both selected and not selected never fires either.

## Checking a rule

`evaluate_conditions` with a set of selections tells you which rules fire. It evaluates `is-selected` and `is-not-selected` only, so for number ranges and modular connections, ask the user to confirm in Preview.

## Modular projects

A modular rule can react to modules snapped onto each other. When a rule's source is its own block ("this block"), it acts per placed module:

- By default it changes only the module that the new module snapped **onto** (the host), never the one just added.
- `selfSnapApplyTo` widens this: `both` (host and the new module), `chain` (the host's whole run of identical modules), `host-parent` (the module two connections back).
- These self-snap rules only support the `3d` and `3d-parts` scopes.

Which faces modules may connect on is a separate thing: see `modular.md` and `set_snap_side_constraint`.
