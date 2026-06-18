# Skill Journal

Use `skill-journal.md` whenever skill design, creation, validation, or iteration spans more than one lane or may resume after context compaction.

The journal is compact durable state. It is not a transcript and not a replacement for source files.

## Rules

- Create `skill-journal.md` in the current workspace or in a skill-specific working folder.
- Update it after every user decision, discovered constraint, blueprint change, file creation, validation result, and lane exit.
- Keep entries short enough that the next specialist can recover the project without reading the entire chat.
- Keep entries complete enough that the next specialist can start from the journal, its own specialist file, and only the references named in the handoff.
- Do not store secrets, tokens, private exports, or long raw transcripts.
- Always keep a current `## Handoff` block at the bottom.
- In `Artifacts to read`, name the exact next specialist file and required references. Do not write vague entries such as `all specialists`, `all references`, or `whole skill folder`.

## Context Sufficiency Standard

Before a lane exits, the journal must answer what the next lane needs without loading unrelated files:

- **Grill -> Design**: purpose, trigger, scope, orchestrator authority, proposed specialists, frameworks, systems/tools, durable artifacts, gates, open questions.
- **Design -> Create**: target name, location, trigger description, folder shape, lane table, reference list, systems/tools list, durable artifacts, gates.
- **Create -> Validate**: target path, files created or changed, expected orchestrator behavior, expected specialist exits, validation commands to run, known risks.
- **Validate -> Create/Design/Complete**: validation results, failures, files needing edits, behavior risks, exact next lane or completion status.

If the journal fails this standard, repair the journal before leaving the lane.

## Template

```markdown
# Skill Journal: <skill name or objective>

Updated: <ISO timestamp>
Lane: <orchestrator | grill | design | create | validate | blocked>
Status: <discovering | designing | creating | validating | complete | blocked>

## Objective

<What the skill should help Codex do, in two or three sentences.>

## Success Criteria

- <What must be true for the skill to be usable.>
- <What behavior should future agents reliably follow.>

## Current Artifacts

| Artifact | Path | Notes |
|---|---|---|
| Target skill | `<path>` | <new/update/status> |
| Journal | `skill-journal.md` | This file. |

## Decisions

| Decision | Choice | Status | Notes |
|---|---|---|---|
| <question> | <answer> | <approved | assumed | open | superseded> | <why> |

## Skill Blueprint

<Compact blueprint from the design lane.>

## Completed

- <Discovery, design, file edit, validation, or test already done.>

## Open Questions

- <One unresolved question with recommended answer. Use `None` if clear.>

## Blockers

- <Blocking issue, owner, and required unlock. Use `None` if clear.>

## Next Recommended Step

<Exactly one next action.>

## Handoff

Current lane: `<lane>`
Completed work: <one or two lines>
Recommended next lane: `<lane>`
Reason: <why that lane owns the next action>
Artifacts to read: `<paths>`
One next action: <single action>
```

## Resume Rule

When resuming, read `skill-journal.md` first, then return to the orchestrator lane table. Load only the specialist and reference files named in the handoff. If the handoff is missing or vague, rebuild the smallest viable handoff from the journal and current user request before reading more files.
