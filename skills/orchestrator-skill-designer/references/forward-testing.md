# Forward Testing

Use this reference when validating complex orchestrator-style skills.

## Basic Validation

For Codex or portable packages, run this validator when it exists:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" <path-to-skill-folder>
```

Then check:

- no TODO placeholders remain
- linked specialist and reference files exist
- `agents/openai.yaml` names the skill correctly for Codex or portable packages
- `default_prompt` includes `$<skill-name>` when `agents/openai.yaml` exists
- no extra user-facing docs were added
- scripts compile or run on a small representative input
- Claude-only skills do not require Codex-only scripts, install paths, validators, or OpenAI metadata
- portable skills keep runtime instructions in `SKILL.md` and references, not only in platform metadata

## Behavioral Validation

Read the target skill as if you are a fresh agent and ask:

- Does the first move tell the agent what to do?
- Does the orchestrator choose lanes, or do specialists cascade freely?
- Does each specialist know what to read?
- Does each specialist avoid reading unrelated specialists and references?
- Does each specialist know when to stop?
- Is there a journal/handoff packet for context reduction?
- Does the journal contain enough state for each next lane to continue without the transcript?
- Are fragile steps enforced by scripts, validators, or gates?
- Would a model know when to ask the user versus inspect files?
- Would the skill still work if `agents/openai.yaml` were ignored by Claude Code?
- Would the skill still validate in Codex when packaged with OpenAI metadata?

## Forward-Test With Subagents

Use fresh subagents when available and useful. Treat them as real users of the skill, not reviewers.

Good prompt shape:

```text
Use $<skill-name> at <path> to <perform realistic task>.
```

Avoid:

```text
Review this skill and tell me if my intended fix works.
```

Pass raw artifacts and realistic requests. Do not pass your diagnosis, expected answer, or hidden rubric unless the test explicitly requires it.

Ask the user before forward-testing if the test could be slow, require approvals, or modify live production systems.
