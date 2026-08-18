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
| `extensions` | Required | Inactive placeholders for future pipeline stages. |

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

## Extension policy

Keep `extensions.cropping`, `extensions.tiled_rendering`, `extensions.image_generation`, `extensions.stitching`, and `extensions.quality_control` disabled in V0.1. Later versions may add configuration beneath these keys without changing the manifest-first workflow.
