---
name: archviz-prompt-generator
description: Generate standardized, modular architectural visualization prompts from a geometry-authoritative base image, optionally assigned reference images, and user semantic descriptions. Use when Codex needs to inventory architectural scene inputs, create or review a Scene Manifest, or compile a manifest with a user-supplied architectural visualization prompt template.
---

# Archviz Prompt Generator

## Status

Treat this V0.1 skill as an architecture scaffold. Do not generate images, create a UI, crop or tile images, stitch outputs, or perform automated quality control. Do not invent or replace the project's prompt-writing philosophy. Request the user's existing prompt template before compiling a production prompt.

## Workflow

1. Inventory one `BASE IMAGE`, zero or more `REFERENCE IMAGES`, and optional user semantic descriptions.
2. Assign authority according to [image-role-rules.md](references/image-role-rules.md). Preserve the base image's geometry, camera, composition, and spatial relationships.
3. Detect project-specific elements from the current inputs. Record them in the manifest; never promote them to global defaults.
4. Resolve atmosphere dynamically with [atmosphere-system.md](references/atmosphere-system.md), giving explicit user semantics priority over visual inference.
5. Create a Scene Manifest using [scene-manifest-schema.md](references/scene-manifest-schema.md) and [scene-manifest-template.yaml](assets/scene-manifest-template.yaml). Keep unknown values explicit rather than guessing.
6. After the user supplies the existing prompt template, record its structure in [prompt-template.md](references/prompt-template.md) and compile the approved manifest through that template.
7. Keep future pipeline stages behind explicit extension points; do not implement them in V0.1.

## Authority Order

Apply the following precedence when inputs conflict:

1. Explicit user semantic descriptions
2. Base image for geometry, camera, composition, and spatial relationships
3. Reference images only for their explicitly assigned aspects
4. Conservative inference, labeled as inferred

Never allow a reference image to silently alter base-image-controlled properties.

## Resources

- Read [prompt-template.md](references/prompt-template.md) when importing or compiling the user's existing prompt template.
- Read [image-role-rules.md](references/image-role-rules.md) when classifying images or resolving authority conflicts.
- Read [atmosphere-system.md](references/atmosphere-system.md) when representing atmosphere and mood.
- Read [scene-manifest-schema.md](references/scene-manifest-schema.md) when creating or validating a manifest.
- Copy [scene-manifest-template.yaml](assets/scene-manifest-template.yaml) as the starting artifact for each scene.
