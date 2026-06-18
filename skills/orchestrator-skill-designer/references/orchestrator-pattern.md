# Orchestrator Pattern

Use this reference when designing the target skill structure.

## Target Shape

```text
skill-name/
├── SKILL.md
├── agents/                 # Codex/OpenAI metadata; omit for Claude-only skills
│   └── openai.yaml
├── specialists/
│   ├── grill.md
│   ├── design.md
│   ├── create.md
│   └── validate.md
├── references/
│   ├── skill-journal.md
│   ├── frameworks.md
│   └── packaging-rules.md
├── scripts/
│   └── <deterministic helpers only when needed>
└── assets/
    └── <templates or output resources only when needed>
```

Use only the directories the skill actually needs.

## Orchestrator Responsibilities

- Own intake and trigger interpretation.
- Create or read the journal.
- Route to the smallest matching specialist.
- Keep the active context to the journal, one specialist, and only that specialist's named references.
- Enforce gates and approval rules.
- Keep the top-level context small.
- Reassert control between lanes.
- Summarize final results to the user.

## Specialist Responsibilities

- Own one narrow lane of work.
- Read the journal before additional references.
- Read only files needed for the current lane; do not pre-read other specialists.
- Do the lane work.
- Update the journal.
- Write a compact handoff.
- Return to the orchestrator lane table.

## Handoff Rule

Specialists may recommend the next lane. Only the orchestrator selects and enters the next lane.

Every specialist should end with:

```markdown
## Exit Contract

1. Update `skill-journal.md`.
2. Check that the journal has enough compact state for the next lane to continue without the transcript.
3. Add a `## Handoff` block with current lane, completed work, recommended next lane, reason, exact artifacts to read, and one next action.
4. Return to the orchestrator lane table. Do not continue directly into another specialist.
```

## Gates

Use explicit gates where models tend to skip ahead:

- Grill gate before a fuzzy skill idea becomes a file structure.
- Design gate before creation when structure, trigger, or state model is unclear.
- Creation gate before validation when files are incomplete.
- Validation gate before claiming the skill is ready.
- Approval gate before state-changing external actions or live writes.

## When Not To Use This Pattern

Avoid a full orchestrator/specialist split when the skill is tiny, single-action, and low risk. A one-file skill is better for narrow operations like "format this type of note" unless it needs durable state, tools, or multiple lanes.
