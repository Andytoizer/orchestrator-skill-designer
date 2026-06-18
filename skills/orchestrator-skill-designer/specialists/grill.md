# Grill Specialist

Use this lane first for every new or meaningfully changed skill. Its job is to resolve the design tree before the build plan hardens.

## Read

- Runtime-specific grill helper when available: `${CODEX_HOME:-$HOME/.codex}/skills/grillme/SKILL.md` for Codex or `$HOME/.claude/skills/grill-me/SKILL.md` for Claude Code.
- `skill-journal.md` if it exists.
- [../references/skill-journal.md](../references/skill-journal.md).
- [../references/runtime-compatibility.md](../references/runtime-compatibility.md).

Do not read other specialists or references from this skill unless the orchestrator routes to them. If the journal is missing context, recover only the specific missing decision from user input, files, or session history, then write it into the journal.

## Rules

- Ask one question at a time and include your recommended answer.
- If the answer can be discovered from existing skills, code, session history, files, or user-provided examples, inspect those sources and write the answer into the journal instead of asking.
- Do not build or edit the target skill from this lane.
- Do not over-interview when the user has already given the critical decisions. Mark decisions as `assumed` or `resolved from context` and hand off.
- For meta-skill work, explicitly challenge whether the requested skill needs an orchestrator, specialists, frameworks, systems, durable artifacts, or all of them.
- If a runtime-specific grill helper is unavailable, run this lane's checklist inline instead of blocking.

## Grill Gate

Resolve these branches enough for design:

- Purpose: what should the skill reliably help the agent do?
- Trigger: what should the user say that invokes it?
- Runtime target: should the skill be `portable`, `codex`, or `claude`?
- Scope: one installable skill with internal specialists, or multiple separately triggered skills?
- Orchestrator authority: what decisions must stay centralized?
- Specialist lanes: what work should be isolated into focused files?
- Frameworks: what judgment, rubrics, examples, or templates should be reusable?
- Systems/tools: what should be deterministic through scripts, CLIs, validators, assets, or state stores?
- Journal/state: what compact state should survive compaction or handoff?
- Gates: where must the skill stop for user approval or validation?
- Risk: what could go wrong if the model improvises?

## Exit Contract

Before leaving this lane:

1. Update `skill-journal.md` with resolved decisions, assumptions, open questions, and the next best lane.
2. Check that the journal satisfies `Grill -> Design` in the Context Sufficiency Standard.
3. Add a `## Handoff` block with current lane, completed work, recommended next lane, reason, exact artifacts to read, and one next action.
4. Return to the orchestrator lane table. Do not continue directly into another specialist.

Route to [design.md](design.md) when the core branches are resolved enough to create a blueprint.
