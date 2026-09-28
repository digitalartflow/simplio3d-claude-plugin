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

Scaling happens around the model's pivot. Call `get_model_pivots` first; a centred pivot makes a part grow in both directions. Keep rigid hardware (handles, hinges) in the fixed "position" parts only, never in both lists (finding: numeral-scaling-contradictory-part).

## Text and image printing

`set_text_input_targets` and `set_file_upload_targets` need the mesh that carries the print, and that mesh needs a UV map. New image-upload targets keep the shopper's image in proportion by default.
