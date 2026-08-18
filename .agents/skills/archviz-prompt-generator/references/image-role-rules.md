# Image Role Rules

## Base image

Require exactly one base image for a scene. Treat it as authoritative for:

- geometry and massing;
- camera position, view direction, projection, and framing;
- composition;
- spatial relationships and placement.

Do not use a reference image to redesign, add, remove, or relocate geometry unless the user explicitly changes the semantic brief and acknowledges the geometric change.

## Reference images

Allow zero or more reference images. Give every reference an explicit identifier and one or more assigned influence aspects, such as:

- lighting;
- atmosphere;
- material;
- landscape;
- rendering quality.

Apply a reference only to its assigned aspects. Do not infer blanket style authority from its presence. Record which scene decision each reference supports so provenance remains inspectable.

## User semantics

Treat explicit user descriptions as higher priority than visual inference. Record overrides in the manifest, including the affected field and superseded inference when known. Ask for clarification when an instruction would unintentionally conflict with base-image geometry authority.

## Dynamic project elements

Detect project-specific architecture, site features, objects, materials, and program cues per scene. Store them as scene observations with provenance and confidence. Never hard-code a detected project element as a global rule for later projects.

## Ambiguity

Mark uncertain observations as `unknown` or inferred with a confidence note. Do not convert ambiguity into an unqualified fact.
