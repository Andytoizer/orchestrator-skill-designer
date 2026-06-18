# Design Specialist

Use this lane after grill discovery to turn the idea into an orchestrator-style skill blueprint.

## Read

- `skill-journal.md`.
- [../references/orchestrator-pattern.md](../references/orchestrator-pattern.md).
- [../references/packaging-rules.md](../references/packaging-rules.md).
- [../references/frameworks-and-systems.md](../references/frameworks-and-systems.md).

Do not read create/validate/grill specialist files while designing. The journal should contain the discovery output from grill; if it does not, route back to grill or repair the journal with the smallest missing facts.

## Rules

- Design the skill before creating files.
- Keep the target `SKILL.md` as a router and contract, not a long manual.
- Prefer one installable orchestrator skill with internal specialists unless the user needs independent triggering.
- Require a journal for any skill with multiple lanes, multi-step work, approval gates, or likely session resumption.
- Use frameworks for judgment and systems/tools for deterministic work.
- Decide the minimum resource set. Do not add scripts, assets, or references just to make the folder look complete.
- If the user requested creation and the plan is coherent, hand off to creation without asking for a second approval. Ask only when a missing decision would change the file structure or behavior.

## Blueprint

Write the build plan into `skill-journal.md` using this compact shape:

```markdown
## Skill Blueprint

Name: `<skill-name>`
Location: `<path>`
Trigger description: <one concise paragraph>

### Orchestrator
- <Responsibilities and gates>

### Specialists
| Lane | File | Owns | Exits To |
|---|---|---|---|
| <lane> | `specialists/<lane>.md` | <work> | <next lane options> |

### Frameworks
| Reference | Purpose | Read When |
|---|---|---|
| `references/<file>.md` | <purpose> | <condition> |

### Systems / Tools
| Resource | Purpose | Degree of Freedom |
|---|---|---|
| `scripts/<script>` or `assets/<asset>` | <purpose> | <high/medium/low> |

### Durable Artifacts
- `skill-journal.md`: <what it tracks>
- <other artifact>: <why it exists>

### Gates
- <approval, validation, safety, or handoff gate>
```

## Exit Contract

Before leaving this lane:

1. Update `skill-journal.md` with the blueprint and any unresolved decisions.
2. Check that the journal satisfies `Design -> Create` in the Context Sufficiency Standard.
3. Add a `## Handoff` block with current lane, completed work, recommended next lane, reason, exact artifacts to read, and one next action.
4. Return to the orchestrator lane table. Do not continue directly into another specialist.

Route to [create.md](create.md) when the blueprint is coherent.
Route back to [grill.md](grill.md) if a structural decision is still unresolved.
