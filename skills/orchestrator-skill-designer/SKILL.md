---
name: orchestrator-skill-designer
description: Design, create, update, and validate portable Codex and Claude Code skills using an orchestrator/specialist/frameworks/systems model. Use when the user wants to build a new skill, redesign an existing skill into an orchestrator-led skill, split a large skill into focused specialists, add grillme-style discovery, add durable journals or handoff gates, decide what belongs in references/scripts/assets, or create a self-contained skill folder that works across Codex, Claude Code, or both.
---

# Orchestrator Skill Designer

You are the orchestrator for designing and creating orchestrator-style skills for Codex, Claude Code, or both. Your job is to keep the top-level skill small, route through focused specialists, choose the target runtime deliberately, and use durable journal state so the next lane can continue without carrying the whole conversation.

The skill you create should usually be an example of this same pattern: orchestrator first, specialist lanes second, frameworks and systems as reusable resources, and explicit gates around ambiguous or fragile work.

## First Move

For every new or changed skill request:

1. Create or update `skill-journal.md` in the current workspace or skill-specific folder using [references/skill-journal.md](references/skill-journal.md).
2. Determine the target runtime (`portable`, `codex`, or `claude`) and record it in the journal. Default to `portable` unless the user asks for one runtime only.
3. Route first to [specialists/grill.md](specialists/grill.md), even if the user already gave a strong direction. The grill lane may conclude that enough is known and hand off immediately.
4. After grill completion, route to [specialists/design.md](specialists/design.md).
5. After design produces a coherent build plan, route to [specialists/create.md](specialists/create.md).
6. After creation or update, route to [specialists/validate.md](specialists/validate.md).

Do not skip the grill lane unless the user explicitly asks for a narrow mechanical edit to an existing skill and the answer is fully discoverable from files.

## Lane Table

| Need | Specialist |
|---|---|
| Stress-test the skill idea, resolve missing decisions, run grillme-style discovery | [specialists/grill.md](specialists/grill.md) |
| Turn decisions into an orchestrator/specialist/frameworks/systems blueprint | [specialists/design.md](specialists/design.md) |
| Scaffold or edit the actual skill folder and write runtime files | [specialists/create.md](specialists/create.md) |
| Validate, smoke-test, forward-test, and identify iteration fixes | [specialists/validate.md](specialists/validate.md) |

## Orchestration Contract

- The orchestrator owns lane selection. Specialists may recommend the next lane, but they must not chain directly into another specialist without returning to this table.
- Each specialist must update `skill-journal.md` before exiting with a compact `## Handoff` block: current lane, completed work, recommended next lane, reason, artifacts to read, and one next action.
- The next lane must read the journal handoff before loading additional references.
- The journal must name the target runtime before design, create, or validate does runtime-specific work.
- Do not pre-read every specialist or reference. The working set for any lane should be: this `SKILL.md`, `skill-journal.md`, exactly one current specialist file, and only the references named by that specialist for the current lane.
- If `skill-journal.md` is missing or too thin for the next lane, reconstruct the smallest useful state from the conversation or source files, update the journal, then continue. Do not compensate by loading the whole skill folder.
- Keep chat updates compact. Put detailed project state in the journal.
- If context is compacted or the session resumes, read `skill-journal.md` first, then route from the lane table.

## Design Model

Use this vocabulary consistently:

- **Orchestrator**: the loaded `SKILL.md`; owns intake, routing, sequencing, gates, and final synthesis.
- **Specialists**: focused markdown lanes under `specialists/`; own one kind of work and exit through a handoff.
- **Frameworks**: reusable judgment, rubrics, taste rules, strategy lenses, decision trees, examples, and templates under `references/`.
- **Systems / tools**: scripts, CLIs, validators, queues, state stores, templates, or assets that make fragile or repeated work deterministic.
- **Journal**: compact durable state used to avoid context overload across specialists and resumed sessions.
- **Runtime**: the agent environment the skill must run in: `codex`, `claude`, or `portable`.

## Hard Rules

- Keep `SKILL.md` lean. It should route and enforce gates, not become the whole skill.
- Treat context as a budget. Read only the current lane and its required references; leave other specialists closed until the orchestrator routes to them.
- Default to a portable core: `SKILL.md`, `specialists/`, `references/`, and optional `scripts/` or `assets/`.
- Treat `agents/openai.yaml` as Codex/OpenAI UI metadata. Include or maintain it for Codex and portable packages, but do not make Claude-only skills fail because it is absent.
- Do not require Codex-only scaffolding, validators, install paths, or metadata when the target runtime is Claude-only. Use runtime-available tooling or manual structural checks instead.
- Put detailed frameworks, examples, schemas, and rubrics in `references/`.
- Put deterministic repeated work in `scripts/` when text instructions are too fragile.
- Put output templates, boilerplate, icons, fonts, or media in `assets/`.
- Do not create README, installation guide, changelog, quick reference, or other auxiliary docs inside a skill unless they are runtime artifacts the skill itself needs.
- Use lowercase hyphenated skill names under 64 characters.
- Frontmatter must contain only `name` and `description`.
- The `description` is the trigger surface. Include what the skill does and when Codex or Claude Code should use it.
- Prefer one installable skill with internal specialists unless the user explicitly needs multiple separately triggered skills.
- Ask one question at a time when a missing decision changes the design, and include your recommended answer.
- If a question can be answered from existing files, session history, or the codebase, answer it yourself instead of asking the user.

## References

Load only what the current lane needs:

- [references/skill-journal.md](references/skill-journal.md): journal template and handoff contract.
- [references/runtime-compatibility.md](references/runtime-compatibility.md): target-runtime detection, install paths, metadata, scaffolding, and validation strategy for Codex and Claude Code.
- [references/orchestrator-pattern.md](references/orchestrator-pattern.md): target folder shape, lane contracts, and gates.
- [references/packaging-rules.md](references/packaging-rules.md): condensed rules inherited from `skill-creator`.
- [references/frameworks-and-systems.md](references/frameworks-and-systems.md): how to decide what belongs in frameworks, scripts, assets, and durable state.
- [references/forward-testing.md](references/forward-testing.md): validation and subagent testing guidance.
