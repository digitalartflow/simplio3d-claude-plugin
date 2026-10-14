# 3D visibility and part targeting

Simplio3D targets 3D geometry **by mesh name**. A wrong name doesn't raise an error in the shopper's browser; it silently does nothing. That's why names must come from the model, never from guessing.

## Get the names

- `list_model_parts`: every mesh in a model, with its path.
- `get_scene_hierarchy`: the full tree, including groups.
- `find_scene_objects`: search by words ("door", "leg", "cushion").
- `get_object_details`, `get_object_spatial_context`: size, position, neighbours, symmetry. Use these to tell "left" from "right"; don't infer it from names alone.

Materials, variant visibility, number-input scaling and text/image targets all act on **meshes**. A group name matches nothing for them. Conditional rules with the `3d-parts` scope are the one feature that can hide a whole named group.

## Options that swap geometry (door count, body style, with/without)

When each choice represents different geometry and only one should be visible, use `set_variant_visibility` with `exclusiveParts`: a map from each variant to the meshes **that choice represents**. Simplio3D then hides the other choices' meshes automatically.

Don't configure each variant to hide its own parts. That hides the geometry the shopper just chose and leaves the alternatives on screen (finding: visibility-hides-own-parts).

## Options that recolour the same geometry (finishes, colours)

Every variant of a material option normally paints the **same** parts. If variants target different parts, confirm that is intended (finding: material-variant-target-drift).

## Number inputs that resize

Only a parameter whose value type is **dimension** moves geometry. List **every** mesh the value affects in `targetPartNames`; each one stretches unless it is also listed in `positionParts` with behavior `fixed` (handles, hinges, legs), which makes it keep its size and move with the change. A `positionParts` entry that is not a target does nothing (finding: numeral-position-part-not-target), and `set_numeral_variants` adds such parts to the targets for you.

Each stretching part keeps its **Edit Axis pivot** fixed: its own pivot, else the pivot of the group or model it is in, else its origin from the 3D file. A `fixed` part keeps its size and moves from its group's or model's pivot. So if a part grows the wrong way, set the pivot on the side that must stay put — `set_object_pivot` with a preset such as `right`, `center` or `bottom-front-right` — after checking it with `get_model_pivots` (`preview`). Put one pivot on the group that contains everything that should move together. Two parameters on the same part and axis multiply (finding: numeral-scaling-axis-conflict).

## Text and image printing

`set_text_input_targets` and `set_file_upload_targets` need the mesh that carries the print, and that mesh needs a UV map. New image-upload targets keep the shopper's image in proportion by default.
