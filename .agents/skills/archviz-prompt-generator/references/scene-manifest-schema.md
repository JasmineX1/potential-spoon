# Scene Manifest Schema

## Purpose

Use the Scene Manifest as the inspectable intermediate representation between input analysis and prompt compilation. Start from `../assets/scene-manifest-template.yaml`.

## Top-level fields

| Field | Requirement | Purpose |
| --- | --- | --- |
| `schema_version` | Required | Manifest contract version. |
| `scene_id` | Required | Project-local stable scene identifier. |
| `inputs` | Required | Base image, assigned references, and user semantics. |
| `authority` | Required | Effective precedence and explicit overrides. |
| `scene` | Required | Base-controlled properties and dynamic observations. |
| `atmosphere` | Required | Modular, provenance-aware atmosphere description. |
| `prompt_compilation` | Required | Template readiness and unresolved mappings. |
| `negative_constraints` | Required | Global preservation rules and scene-specific exclusions. |
| `extensions` | Required | Inactive placeholders for future pipeline stages. |

## Scene fields

`scene` separates base-image observations so the prompt can preserve the supplied template's descriptive order without losing provenance:

- `building`: architectural attributes and a cautiously inferred function/program, each with confidence and provenance;
- `geometry`, `camera`, `composition`, and `spatial_relationships`: base-authoritative spatial facts;
- `objects_and_structures`: visible items, locations, and relations to other scene elements;
- `materials`: one item per visible material/surface zone, including likely identity, color, texture, finish, optical properties, and light response;
- `environment`: site condition, circulation, and the building's relationship to surrounding space;
- `landscape`: visible softscape and hardscape observations;
- `background`: background layers, context, skyline, and depth composition;
- `project_elements`: generic Project Anchors with identity, location, visual characteristics, preservation requirements, continuity, and high-risk misinterpretations. Each anchor contains `id`, `name`, `semantic_identity`, `description`, `location`, `visual_characteristics`, `preservation_priority`, `preserve_geometry`, `preserve_material_identity`, `continuity_required`, `high_risk_misinterpretations`, `provenance`, and `confidence`. Anchors remain current-project data and must never become template defaults.

Use item-level `provenance` and `confidence` for inferred attributes, functions, objects, materials, and context. Material inference must remain consistent with visible base-image evidence unless an explicitly assigned material reference or user override controls it.

## Input rules

- `inputs.base_image` must identify exactly one asset.
- Each `inputs.reference_images` item must have a unique `id` and non-empty `assigned_aspects`.
- `inputs.user_semantics` may be empty; each item should retain its original text and target scope.
- Use provenance values such as `user`, `base_image`, `reference:<id>`, or `inferred`.

## Value-state rules

Use `null` for unknown scalar values and empty lists only when no items are present. Attach notes and confidence to inferred observations. Do not represent assumptions as user-approved values.

## Authority validation

- Geometry, camera, composition, and spatial relationships must resolve to the base image unless an explicit user-approved override is recorded.
- A reference may affect only aspects listed in `assigned_aspects`.
- Explicit user semantics override visual inference.
- Project-specific elements remain within the current manifest.

## Prompt compilation fields

- `template_status` is `ready` once this V0.1 template is available.
- `template_id` identifies the template contract, currently `archviz-v0.1`.
- `section_order` preserves the six required Chinese headings.
- `fixed_opening` preserves the user's exact required beginning of `主要提示词`, including visualization-quality language in its original position.
- `main_prompt_sequence` records the required content-first order: image content, building composition, spatial hierarchy, architectural objects, then rendering-quality intensification.
- `quality_intensifier` preserves the supplied quality vocabulary for insertion only after the scene is clearly established.
- `unresolved_fields` contains manifest paths omitted from prose because evidence was insufficient.
- `final_prompt` remains `null` until a particular scene is compiled.

## Atmosphere fields

`atmosphere` represents lighting and mood as independent, project-neutral decisions. It contains `time_of_day`, `weather_and_sky`, structured `natural_light` (`direction`, `altitude`, `character`, `color_temperature`), structured `artificial_light` (`interior`, `facade`, `landscape`, `commercial`), `color_palette`, `white_balance`, `saturation`, `contrast`, `atmospheric_depth`, `emotional_tones`, `occupancy_character`, `presentation_tier`, and `qualifiers`. Do not encode atmosphere presets in the schema.

Every atmosphere leaf uses a field-level decision object with `value`, `provenance`, and `confidence`. This permits separate user instructions or assigned references to control sky, natural light, artificial-light groups, palette, or mood without claiming authority over the entire atmosphere. Lists remain inside `value`; do not replace field-level provenance with a generic atmosphere provenance list.

## Negative constraints

`negative_constraints.preservation` holds global base-preservation prohibitions from the supplied template. `negative_constraints.scene_specific` holds exclusions justified by the current inputs or explicit user semantics. Do not place project-specific objects or styles in the global list, and do not negate intentional manifest content.

## Extension policy

Keep `extensions.cropping`, `extensions.tiled_rendering`, `extensions.image_generation`, `extensions.stitching`, and `extensions.quality_control` disabled in V0.1. Later versions may add configuration beneath these keys without changing the manifest-first workflow.
