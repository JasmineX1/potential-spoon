# Atmosphere System

## Principle

Represent atmosphere as scene data, not as a fixed global style. Permit daylight, night, futuristic, everyday, warm, premium, relaxed, and other project-appropriate directions without making any one direction the default.

## Resolution

Resolve atmosphere in this order:

1. Apply explicit user semantic descriptions.
2. Apply atmosphere or lighting references only when assigned to those aspects.
3. Infer conservatively from the base image only when helpful and label the result as inferred.
4. Leave unresolved dimensions unknown.

## Manifest dimensions

Keep atmosphere modular so later template mapping can combine or omit dimensions:

- time of day;
- weather and sky;
- light character and contrast;
- emotional tone;
- occupancy or everyday-life character;
- stylistic era or future-facing character;
- presentation tier or polish;
- free-form qualifiers;
- provenance and confidence.

Do not force labels into mutually exclusive categories. A scene may, for example, be both warm and premium. Avoid visual changes that would violate the base image's geometry or composition.

## Future extension point

Preserve structured fields for later rendering and QC stages, but do not translate them into image-generation parameters in V0.1.
