# Frameworks And Systems

Use this reference when deciding what kind of resource each piece of knowledge should become.

## Degrees Of Freedom

| Need | Resource | Freedom |
|---|---|---|
| Judgment, taste, strategy, evaluation, examples | `references/*.md` framework | High |
| Repeatable procedure with some variation | specialist checklist or pseudocode reference | Medium |
| Fragile transformation, validation, parsing, file generation, repeated code | `scripts/*` | Low |
| Boilerplate, canvas, templates, fonts, icons, media | `assets/*` | Low |
| Cross-lane memory, approvals, compact progress | durable artifact such as `skill-journal.md` | Medium |

## Frameworks

Use frameworks for:

- decision trees
- rubrics
- QA bars
- examples of good and bad output
- style/taste guidance
- strategy lenses
- policy/safety checks
- output templates

Frameworks should be loaded only when relevant.

## Systems / Tools

Use systems/tools for:

- validation
- manifest generation
- parsing or transforming structured files
- repeated scaffold creation
- deterministic rendering
- external API/CLI workflows
- state stores or queues
- smoke tests

If the same instructions would be rewritten repeatedly as code, make a script.

## Durable Artifacts

Use durable artifacts when:

- multiple specialists need shared state
- work may resume after compaction
- approvals or decisions matter
- a plan must be audited before execution
- the next lane needs a small packet instead of the whole transcript

Keep durable artifacts compact and current.

## Choosing Minimal Resources

Ask:

1. Would a future agent need this context every time? If yes, keep it in `SKILL.md`.
2. Would it need this only for one lane or variant? If yes, put it in `references/`.
3. Would prose be too fragile or inconsistent? If yes, use `scripts/` or `assets/`.
4. Is this project state rather than instruction? If yes, use a journal artifact.
