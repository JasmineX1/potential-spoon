# Architectural Visualization Prompt Template (V0.1)

## Purpose

This document records the user's existing prompt-writing logic without turning any example project into a global default. Compile a completed or explicitly partial Scene Manifest into one Chinese-language architectural-visualization prompt. The compiler must describe observed content first and then apply strong visualization-style language.

## Required output structure

Emit the following headings exactly, in this order, with one descriptive passage under each heading:

```text
主要提示词：

色调和光线：

建筑的特征：

材质细节：

环境与配景：

负面提示词：
```

The content beneath `主要提示词：` must begin exactly with:

```text
根据这张图片生成一张建筑效果图，不要更换视角，严格遵守原图的构图, 超级写实，高级的建筑渲染图，高分辨率，高度详细，清晰对焦，8k resolution，masterpiece，intricate details，photorealistic，detailed texture，保留输入图像的视角和内容，将这张图像转换为
```

Continue the sentence after `转换为`; do not insert a placeholder, plus sign, or a new heading there. Preserve the quality terms in this exact opening. After the opening, the generated continuation must establish the scene before adding any further rendering-quality language.

### `主要提示词` internal sequence

Within `主要提示词`, compile content in this strict order:

1. **Fixed opening:** emit the exact clause above, including its original visualization-quality language.
2. **Actual image content:** describe the visible scene itself—what the image depicts and the building's apparent attributes and function—before introducing any rendering-quality or style language.
3. **Building composition:** describe massing, façade organization, structure, openings, roof and ground interfaces.
4. **Spatial hierarchy:** move coherently through foreground, architectural subject, midground, surroundings, and background while stating relative positions and building-site relationships.
5. **Architectural objects:** identify visible architectural elements, site structures, landscape elements, and other objects in their spatial context.
6. **Rendering-quality intensification:** only after the actual image content, spatial hierarchy, and architectural objects are fully described in steps 2–5, append `超级写实，高级的建筑渲染图，高分辨率，高度详细，清晰对焦，8k resolution，masterpiece，intricate details，photorealistic，detailed texture` and the applicable CCD/MIR presentation direction.

Beyond the quality language required in the fixed opening, do not lead the generated scene continuation with additional quality tags, interleave style tags with architectural observations, or allow rendering language to replace concrete scene content.

## Fixed master-template instructions

- Use architectural-design language and write concrete, image-grounded details rather than a generic style list.
- Preserve the base image's viewpoint, framing, composition, geometry, objects, content, and spatial relationships.
- Describe the architecture's attributes and likely function, all visible objects and structures, their relative relationships, the building-to-site relationship, and the composition of the background.
- Describe every visible architectural object and surface material in detail before emphasizing the final image style.
- Infer material names, colors, finish, texture, reflectance, translucency, and light response conservatively. Maintain material consistency with the base image, including realistic curtain-wall glazing and other distinct surfaces.
- Endow the result with the polish, tension, focus, resolution, detail, and photoreal material/light behavior of a top-tier architectural visualization.
- Use `CCD` and `MIR` only as rendering-quality and presentation references. They must not authorize changes to geometry, program, materials, context, or composition.
- Do not state uncertain inferences as facts. Omit unresolved details or qualify them naturally.

## Dynamic field ownership

### Inferred from the BASE IMAGE

- Building type/attributes and cautiously inferred program or function.
- Geometry, massing, façade organization, structural expression, openings, roof and ground interfaces.
- Camera, viewpoint, projection, framing, composition, and all relative spatial relationships.
- Visible objects, site features, landscape, circulation, foreground/midground/background organization, and building-context relationships.
- Material observations: surface location, likely material, color, texture, finish, reflectance/transparency, weathering, and light response.
- Existing tonal, lighting, weather, and occupancy cues when not superseded by an authorized source.

### Controlled by REFERENCE IMAGES

A reference image controls only its declared `assigned_aspects`, such as `material`, `lighting`, `atmosphere`, `landscape`, or `rendering_quality`. Map each applied decision to `reference:<id>`. A reference must never silently change base-controlled geometry, camera, composition, content, or spatial relationships.

### Dynamic atmosphere variables

Resolve time of day, weather/sky, color palette, light direction and character, contrast, emotional tone, occupancy character, era character, presentation tier, and free-form qualifiers through the atmosphere authority rules. These are variables, not fixed defaults.

### Project-specific anchors

Building program cues, signature forms, façade systems, individual materials, furnishings, vegetation, people, vehicles, water, signage, landmarks, and contextual/background elements belong only to the current Scene Manifest. Never copy them into this master template as universal content.

### User semantic overrides

Apply explicit user semantics before visual inference. Record the target field and any superseded value in `authority.overrides`. A semantic request cannot silently override base-image geometry authority; flag such a conflict for clarification.

### Negative constraints

Compile scene-specific exclusions plus these preservation constraints: no viewpoint change, no composition change, no geometry redesign, no relocation/addition/removal of image content without an explicit approved override, no material inconsistency, no implausible glazing or surface response, and no unsupported invented detail. Also derive targeted anti-misinterpretation constraints from `high_risk_misinterpretations` on current-project anchors. Keep each constraint project-local and evidence-based; never promote a scene-specific anchor to a global default. Negative constraints should prevent common rendering defects without erasing intentional scene features.

## Section mapping

| Output section | Manifest sources | Writing intent |
| --- | --- | --- |
| `主要提示词` | `scene.camera`, `scene.composition`, `scene.spatial_relationships`, `scene.objects_and_structures`, `scene.project_elements`, `scene.background`, `scene.building`, `scene.rendering_quality` | Start with the preservation opening; establish image content, building composition, spatial hierarchy, and architectural objects in that order; only then intensify rendering quality and visualization style. |
| `色调和光线` | `atmosphere`, authorized lighting/atmosphere references, relevant user overrides | State palette, time/weather cues, illumination, shadow, contrast, and mood. |
| `建筑的特征` | `scene.building`, `scene.geometry`, `scene.spatial_relationships` | Describe attributes, cautiously inferred function, massing, façade/structure, and building-site relationships. |
| `材质细节` | `scene.materials`, authorized material references | Organize descriptions by architectural element or surface location—not as an abstract material list—then state each surface's identity, color, finish/texture, optical behavior, and light response. |
| `环境与配景` | `scene.environment`, `scene.landscape`, `scene.background`, `scene.objects_and_structures`, occupancy atmosphere | Describe foreground through background, circulation, landscape, entourage, and context. |
| `负面提示词` | `negative_constraints`, preservation rules, `authority.conflicts`, high-risk `scene.project_elements` | State applicable prohibitions and project-local anti-misinterpretation constraints concisely; never negate an intentional manifest feature. |

## Compilation contract

1. Consume the resolved Scene Manifest; do not independently re-infer facts that contradict it.
2. Apply authority in this order: explicit user semantics, base image for spatial properties, explicitly assigned reference aspects, then labeled conservative inference.
3. Use material-specific architectural observations where relevant, but enforce the content-first `主要提示词` sequence before rendering-quality language.
4. Do not print provenance, confidence values, nulls, YAML keys, or unresolved placeholders in the final prompt.
5. When a required value is unknown, omit the unsupported claim and add its field path to `prompt_compilation.unresolved_fields`.
6. Store the compiled six-section text in `prompt_compilation.final_prompt` without implementing image generation or any V0.2 stage.
