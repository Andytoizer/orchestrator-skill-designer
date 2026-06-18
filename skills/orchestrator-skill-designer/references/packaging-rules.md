# Packaging Rules

These are the condensed rules inherited from the system `skill-creator` skill.

## Required Shape

Every skill needs:

- `SKILL.md`
- YAML frontmatter with only `name` and `description`
- Markdown body with runtime instructions

Recommended:

- `agents/openai.yaml` with user-facing metadata

Optional:

- `specialists/` for orchestrator-style lanes
- `references/` for detailed guidance loaded only when needed
- `scripts/` for deterministic or repeated operations
- `assets/` for templates and output resources

## Naming

- Use lowercase letters, digits, and hyphens only.
- Keep names under 64 characters.
- Prefer short action-oriented names.
- Name the folder exactly after the skill name.

## Description

The description is the trigger surface. Include:

- what the skill does
- when Codex should use it
- important trigger phrases, contexts, file types, tools, or workflows

Do not put "when to use" only in the body; the body is loaded after triggering.

## Progressive Disclosure

- Keep `SKILL.md` lean and under 500 lines.
- Link every reference directly from `SKILL.md`; avoid deep reference chains.
- Put variant-specific details in references.
- Put detailed examples, schemas, rubrics, and API notes in references.
- Do not duplicate long guidance in both `SKILL.md` and references.

## Agents Metadata

`agents/openai.yaml` should include:

```yaml
interface:
  display_name: "<human title>"
  short_description: "<25-64 char UI blurb>"
  default_prompt: "Use $<skill-name> to <do the core thing>."
```

Quote strings. Ensure `default_prompt` includes `$<skill-name>`.

## Scaffolding

For new skills, use:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/init_skill.py" <skill-name> --path <output-directory> --resources references
```

Add `scripts` or `assets` only when the blueprint requires them.

## Validation

Run:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" <path-to-skill-folder>
```

Fix validation errors before claiming the skill is ready.

## Do Not Include

Do not create these unless they are truly runtime artifacts for the skill:

- `README.md`
- `INSTALLATION_GUIDE.md`
- `QUICK_REFERENCE.md`
- `CHANGELOG.md`
- process notes about how the skill was created
