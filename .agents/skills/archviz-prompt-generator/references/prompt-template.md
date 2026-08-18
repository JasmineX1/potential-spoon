# Prompt Template Integration

## V0.1 status

The project prompt template has not yet been supplied. Do not invent substitute prompt sections, prose rules, ordering rules, or a new prompt-writing philosophy.

## Intake placeholder

When the user provides the existing template:

1. Preserve its terminology, section order, constraints, and output style unless the user requests changes.
2. Map Scene Manifest fields to template slots without changing input authority.
3. Identify required template values that the manifest does not yet represent.
4. Extend the manifest schema in a backward-compatible way where practical.
5. Document compilation rules here, separating literal template text from field-mapping instructions.

## Compilation contract

Compilation must consume a completed or explicitly partial Scene Manifest. It must not re-infer scene facts that contradict the manifest. Unknown values must follow the supplied template's eventual missing-value policy.
