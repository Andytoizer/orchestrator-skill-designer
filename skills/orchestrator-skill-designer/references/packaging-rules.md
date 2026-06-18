# Packaging Rules

These are the condensed rules inherited from the system `skill-creator` skill.

## Required Shape

Every skill needs:

- `SKILL.md`
- YAML frontmatter with only `name` and `description`
- Markdown body with runtime instructions

Recommended for Codex/OpenAI UI packages:

- `agents/openai.yaml` with user-facing metadata

Optional for Claude-only skills:

- `agents/openai.yaml` if the same package is also meant to be used by Codex

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
- when Codex, Claude Code, or another skill-aware agent should use it
- important trigger phrases, contexts, file types, tools, or workflows

Do not put "when to use" only in the body; the body is loaded after triggering.

## Progressive Disclosure

- Keep `SKILL.md` lean and under 500 lines.
- Link every reference directly from `SKILL.md`; avoid deep reference chains.
- Put variant-specific details in references.
- Put detailed examples, schemas, rubrics, and API notes in references.
- Do not duplicate long guidance in both `SKILL.md` and references.

## Agents Metadata

`agents/openai.yaml` is Codex/OpenAI UI metadata. For Codex or portable packages, it should include:

```yaml
interface:
  display_name: "<human title>"
  short_description: "<25-64 char UI blurb>"
  default_prompt: "Use $<skill-name> to <do the core thing>."
```

Quote strings. Ensure `default_prompt` includes `$<skill-name>`.

For Claude-only skills, do not require this file. Keep runtime instructions in `SKILL.md` and references so Claude Code can use the skill without OpenAI metadata.

## Scaffolding

For new Codex skills, use the scaffold when it exists:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/init_skill.py" <skill-name> --path <output-directory> --resources references
```

Add `scripts` or `assets` only when the blueprint requires them.

For Claude-only skills, or portable work where the Codex scaffold is unavailable, create the portable core files manually.

## Validation

For Codex or portable packages, run the validator when it exists:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" <path-to-skill-folder>
```

Fix validation errors before claiming the skill is ready.

For Claude-only skills, use Claude Code's available skill checks or manual structural validation. Do not fail solely because Codex validator scripts or `agents/openai.yaml` are absent.

## Do Not Include

Do not create these unless they are truly runtime artifacts for the skill:

- `README.md`
- `INSTALLATION_GUIDE.md`
- `QUICK_REFERENCE.md`
- `CHANGELOG.md`
- process notes about how the skill was created
