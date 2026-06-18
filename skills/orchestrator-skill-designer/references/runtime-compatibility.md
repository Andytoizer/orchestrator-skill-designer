# Runtime Compatibility

Use this reference when a skill should work in Codex, Claude Code, or both.

## Runtime Target

Record one target in `skill-journal.md` before design, create, or validate does runtime-specific work:

| Target | Use When | Default Behavior |
|---|---|---|
| `portable` | The user wants the skill to work in both Codex and Claude Code, or has not specified a runtime | Build a runtime-neutral core and make platform extras optional |
| `codex` | The user explicitly wants a Codex skill or Codex package | Use Codex install paths, Codex validator, and `agents/openai.yaml` |
| `claude` | The user explicitly wants Claude Code compatibility or a Claude-only install | Use Claude skill paths and avoid Codex-only validators or metadata requirements |

If the user asks for "both", "portable", "Claude and Codex", or "cross-runtime", choose `portable`.

## Portable Core

These pieces should work in both runtimes:

- `SKILL.md` with YAML frontmatter containing only `name` and `description`.
- Markdown runtime instructions.
- Relative links from `SKILL.md` to `specialists/`, `references/`, `scripts/`, or `assets/`.
- Lowercase hyphenated skill folder names.
- Optional specialists and references that do not depend on one platform's tool names.

Avoid hard-coded machine paths in portable packages. Use environment variables or describe the runtime-specific path choice in prose.

## Install Locations

Use the user's requested path when provided. Otherwise:

| Runtime | Common Install Location |
|---|---|
| Codex | `${CODEX_HOME:-$HOME/.codex}/skills/<skill-name>` |
| Claude Code personal skill | `$HOME/.claude/skills/<skill-name>` |
| Claude Code project skill | `<project>/.claude/skills/<skill-name>` when the user wants project-local behavior |

For portable packages, keep the repository layout neutral, such as `skills/<skill-name>/`, and document runtime-specific copy commands outside the skill folder.

## Metadata

`agents/openai.yaml` is Codex/OpenAI UI metadata.

- For `codex`: create or maintain `agents/openai.yaml`.
- For `portable`: include `agents/openai.yaml` when packaging for Codex, but keep all actual runtime instructions in `SKILL.md` and references so Claude can ignore it.
- For `claude`: do not require `agents/openai.yaml`. If it exists in a shared package, treat it as harmless Codex metadata.

Never put instructions required by Claude only in `agents/openai.yaml`.

## Scaffolding

For Codex, use the system skill-creator scripts when available:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/init_skill.py" <skill-name> --path <output-directory> --resources references
```

For Claude Code or portable work where that script is missing, create the folder and files manually using the same portable core shape. Do not block Claude compatibility on Codex-only scaffolding.

## Validation

Validate the portable core first:

- `SKILL.md` exists.
- Frontmatter contains only `name` and `description`.
- Name matches the folder and uses lowercase hyphens.
- All links from `SKILL.md` resolve.
- Specialist files named by the lane table exist.
- References named by `SKILL.md` or the current specialist exist.
- No required runtime behavior lives only in `agents/openai.yaml`.
- No Codex-only script, path, or tool is required for a Claude-only run.

Then validate runtime extras:

- `codex`: run `quick_validate.py` when available and check `agents/openai.yaml` includes `$<skill-name>` in `default_prompt`.
- `portable`: run Codex validation when available, and also inspect for Claude-blocking assumptions such as required Codex scripts, absolute `.codex` paths, or mandatory OpenAI metadata.
- `claude`: use Claude Code's available skill tooling or manual structural checks. Do not fail solely because Codex validator scripts or `agents/openai.yaml` are absent.

## Helper Skills

Helper skills may have different names across runtimes. For example, a discovery helper might be named `grillme` in Codex and `grill-me` in Claude Code. Treat helpers as optional accelerators:

- Use them when present.
- Fall back to the embedded checklist when absent.
- Do not make a portable skill depend on a helper skill that exists only in one runtime.
