# Simplio3D finding codes

Codes returned by `validate_project` and `get_project_health`. "Safe fix" means the `repair-project` workflow or `apply_safe_repairs` can remove it without changing what shoppers see. Everything else needs the user's decision.

## 3D models and targets

| Code | What it means | Typical fix |
|---|---|---|
| model-missing-source | A scene model has neither a library asset nor an uploaded file, so it may not load. | Re-add the model from the Assets library. |
| model-asset-not-in-library | The model references a library asset that is no longer in this workspace's library (often after copying a template). | Usually harmless if it still loads; re-add from the library if it doesn't. |
| duplicate-model-id | Two scene models share an id. | Remove the duplicate model in the editor. |
| variant-target-model-missing / block-target-model-missing | An option targets a 3D model that is no longer in the scene. | Retarget the option to a model that exists, or delete the dead option. |
| part-target-unknown | An option targets a mesh name the model file doesn't contain (deep check only). | Pick a real part name with `list_model_parts`. |
| texture-target-missing | A text or image-upload target names no 3D part, so nothing renders. | Set the mesh that should carry the text or image. |
| scenery-model-missing | The Scenery block lists a model that is no longer in the scene. | Remove it from the Scenery selection. Removing the last one turns the scenery camera off, so check the camera afterwards. |
| scenery-camera-deactivated | Scenery camera settings exist but no scenery model is selected, so they have no effect. | Select a scenery model and apply, or ignore. |
| multiple-scenery-blocks | More than one Scenery block. | Keep one. |

## Options and variants

| Code | What it means | Typical fix |
|---|---|---|
| duplicate-block-id, duplicate-variant-value, duplicate-field-id | Two items share an identifier, so one of them can't be addressed. | Rename or remove the duplicate. |
| default-variant-missing | The block's default points at a variant that no longer exists. | **Safe fix**, or pick a new default. |
| category-block-missing-category | A Select Material block in "From Category" mode has no category, so it shows no swatches. | Choose a material category. |
| numeral-flat-range | A number input's minimum equals its maximum, so the shopper can't change it. | Widen the range. |
| numeral-scaling-no-targets / numeral-scaling-no-axis | A number input is meant to resize the model but names no parts or no axis. | Add the parts and axis, or turn scaling off. |
| numeral-scaling-contradictory-part | The same part is listed both as stretching and as fixed. | Keep hardware (handles, hinges) in the fixed list only. |
| numeral-scaling-default-pivot | Parts scale around the model's centre, so they grow in both directions. | Informational; check the pivot if growth should be one-sided. |
| visibility-hides-own-parts | A variant hides the very parts that represent it, so choosing it shows nothing new. | Use `set_variant_visibility` with `exclusiveParts` so each option hides the others' parts. |
| visibility-exclusive-disjoint | Every option hides a completely separate set of parts, so no option ever hides another option's geometry and alternatives stay visible together. | Same as above. |
| visibility-mixed-mode | A visibility setting names both whole objects and parts; the part names are ignored. | Use one mode. |
| visibility-show-noop | A variant "shows" parts that are already visible. | Hide them by default with a rule, or remove the setting. |
| visibility-uniform-object-target | Every variant shows or hides the same object, so the choice changes nothing. | Give each variant its own target. |

## Conditional rules

| Code | What it means | Typical fix |
|---|---|---|
| rule-empty-conditions | A rule has no conditions and never fires. | Add a condition or delete the rule. |
| rule-source-block-missing / rule-source-variant-missing | A rule watches a block or variant that no longer exists. | Point it at the right block or delete it. |
| rule-target-variant-missing | A rule shows or hides a variant that no longer exists. | Update or delete the rule. |
| rule-part-unknown / rule-3d-object-unresolved | A rule targets a 3D part or object name that doesn't exist. | Choose a real name with `list_model_parts` or `find_scene_objects`. |
| rule-parts-bucket-stale | A 3D-parts rule is keyed to a model file that was replaced, so it does nothing. | Re-select the parts on the current model. |
| rule-material-missing | A rule references a deleted material. | Update or delete the rule. |
| rule-circular-reference | Rules depend on each other in a loop. | Break the loop. |
| rule-contradictory-conditions | An "all" rule requires a variant to be both selected and not selected, so it can never fire. | Fix the conditions. Sometimes intentional as a permanent hide. |
| variants-scope-on-category-block | A per-variant rule on a "From Category" material block; those variant ids change, so it is unreliable. | Use a block-level rule, or switch the block to Manual mode. |
| modular-self-snap-wrong-scope | A modular rule that reacts to its own block uses a scope that only works for 3D objects or parts. | Change the rule's scope. |
| disable-rule-block-missing / disable-rule-variant-missing | A modular "disable snap sides" rule references a module that no longer exists. | Update or delete it. |

## Materials

| Code | What it means | Typical fix |
|---|---|---|
| variant-material-missing | A variant uses a material that was deleted from the library. | Assign an existing material. |
| variant-material-data-missing | A Select Material variant has no material, so it renders as a flat placeholder. | Assign one. |
| variant-material-ref-dangling | A variant points at a shared material entry that is missing. Error. | Re-assign the material named in the finding. |
| material-missing-pbr-data | A variant has a material id but no saved material data, so it renders as a plain colour. | Re-assign the material. |
| material-variant-target-drift | Variants of one material option paint different parts; usually every finish should paint the same parts. | Align the targets. |
| material-color-variant-missing | A variant selects a colour that isn't one of its colour options, so the first colour is shown instead. | Re-pick the colour. |

## Pricing and SKUs

| Code | What it means | Typical fix |
|---|---|---|
| pricing-variant-unpriced | A variant in a priced option has no price. | Add a price (a proposed change the user approves). |
| pricing-variant-key-unknown | A price is stored for a variant that no longer exists. | **Safe fix.** |
| sku-variant-missing | A SKU is stored for a variant that no longer exists. | **Safe fix.** |
| pricing-linked-block-missing | A pricing block links to a deleted option block. | Relink or delete the pricing block. |
| formula-invalid / formula-block-missing | The pricing formula can't be parsed or references a deleted pricing block. | Fix the formula. |
| formula-disabled-block | The formula uses a disabled pricing block, which counts as 0. | Enable the block or remove it from the formula. |
| formula-block-orphaned | A formula exists but leaves out an enabled pricing block, so that block adds 0 to the total while still appearing in the breakdown. Error. | Add the block to the formula, or disable it. |
| formula-orphaned-variable / variable-summed-without-formula | A pricing variable is unused, or is summed into the total as if it were money. | Reference it in the formula as intended. |
| price-table-axis-no-selection | A price table axis uses a block type the table can't read (for example a checkbox), so every cell is dead. | Use a single-choice block for the axis. |

## Form and display

| Code | What it means | Typical fix |
|---|---|---|
| form-no-submit | The form has no Submit or Add to Cart button. | Add one. |
| form-dropdown-no-options | A dropdown form field has no options. | Add options. |
| save-config-required | A Save Configuration field is marked required, which blocks the whole form. Error. | Make it optional. |
| sidebar-disabled-with-blocks | The options sidebar is turned off, so shoppers can't see any options. Error. | Turn the sidebar back on. |
| animation-target-missing / animation-part-unknown | An animation targets a missing model or part. | Retarget or delete it. |
| internal-validator-error | One check failed to run. | Report it; the rest of the results still stand. |
