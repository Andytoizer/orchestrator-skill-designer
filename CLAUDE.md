# CLAUDE.md

This repository packages a portable skill for Codex and Claude Code. Keep the package public-ready and avoid adding private context, secrets, local machine paths, customer names, or personal workflow data.

## Working Rules

- Keep runtime skill behavior inside `skills/orchestrator-skill-designer/`.
- Do not add README, changelog, install guide, or quick reference files inside the skill folder itself.
- Root documentation is allowed for repository packaging.
- Preserve the orchestrator/specialist/context-discipline model.
- Run runtime-appropriate validation before publishing changes.

## Validation

For Codex or portable packages, run:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" skills/orchestrator-skill-designer
```

Use a temporary PyYAML install if the local Python lacks `yaml`. For Claude Code, also confirm the portable core works without relying on `agents/openai.yaml` or Codex-only validator paths.
