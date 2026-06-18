# Validate Specialist

Use this lane after creating or editing a skill, and when a user reports that an orchestrator-style skill behaved poorly.

## Read

- `skill-journal.md`.
- [../references/forward-testing.md](../references/forward-testing.md).
- [../references/packaging-rules.md](../references/packaging-rules.md).
- The target skill's `SKILL.md` first, then only linked specialist/reference files needed to validate the orchestrator, lane table, journal contract, and reported failure.

Do not read all target references by default. First validate the orchestrator, lane table, journal contract, and linked files named by the target `SKILL.md`. Read additional target references only when validating a link, a claimed gate, or a failure.

## Steps

1. Run the system validator:
   ```bash
   python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" <path-to-skill-folder>
   ```
2. Inspect the target folder shape:
   - `SKILL.md` exists
   - `agents/openai.yaml` exists and mentions `$<skill-name>` in `default_prompt`
   - specialists exist when the orchestrator lane table references them
   - references exist when `SKILL.md` links them
   - no placeholder TODO text remains
   - no extra README/changelog/quick-reference docs were created
3. Check orchestrator behavior:
   - first move routes to grill when appropriate
   - lane table covers expected intents
   - specialists have exit contracts
   - journal/handoff rules are visible in orchestrator and specialist exits
   - each lane can continue from the journal plus its own specialist file and named references
   - deterministic or fragile work has scripts/assets/validators instead of prose only
4. Smoke-test scripts or validators if the target skill includes them.
5. Forward-test with a subagent when the skill is complex and a fresh pass is available. Do not leak the intended answer or your diagnosis.
6. Patch issues and rerun validation.

## Exit Contract

Before leaving this lane:

1. Update `skill-journal.md` with validation results, remaining risks, and follow-up fixes.
2. Check that the journal satisfies `Validate -> Create/Design/Complete` in the Context Sufficiency Standard.
3. Add a `## Handoff` block with current lane, completed work, recommended next lane, reason, exact artifacts to read, and one next action.
4. Return to the orchestrator lane table. Do not continue directly into another specialist.

Route to [create.md](create.md) if validation requires file edits.
Route to [design.md](design.md) if a behavioral flaw means the blueprint is wrong.
