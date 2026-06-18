# Create Specialist

Use this lane to scaffold or edit the actual skill folder from the approved or coherent blueprint.

## Read

- `skill-journal.md`.
- [../references/packaging-rules.md](../references/packaging-rules.md).
- [../references/orchestrator-pattern.md](../references/orchestrator-pattern.md).
- If updating an existing skill, read the target `SKILL.md` first, then only the target specialist/reference files named in the journal or directly involved in the current edit.

Do not read validate/grill/design specialist files unless routed back to those lanes. Use the blueprint in the journal as the source of truth. If implementation reveals missing structure, update the journal and route back to design rather than loading every reference.

## Steps

1. Confirm the target skill name and location from `skill-journal.md`. If absent, default to `${CODEX_HOME:-$HOME/.codex}/skills`.
2. If creating a new skill, run the system scaffold:
   ```bash
   python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/init_skill.py" <skill-name> --path <output-directory> --resources references
   ```
   Add `scripts` or `assets` only when the blueprint needs them.
3. Create `specialists/` manually when the blueprint includes lanes.
4. Replace the scaffolded `SKILL.md` with a lean orchestrator:
   - frontmatter with only `name` and `description`
   - first move
   - lane table
   - orchestration/handoff contract
   - hard rules
   - reference index
5. Write specialist files with:
   - purpose
   - files to read
   - lane rules
   - sequence or checklist
   - exit contract that writes `## Handoff` and returns to the orchestrator
6. Write reference files for frameworks, packaging rules, domain knowledge, examples, templates, or journal format.
7. Write scripts only when reliability, repetition, validation, or fragile transformations justify low freedom.
8. Update `agents/openai.yaml` so `display_name`, `short_description`, and `default_prompt` match the final skill.
9. Delete placeholder examples and unused resource directories.

## File Rules

- Use `apply_patch` for manual edits.
- Do not create README, installation guide, changelog, or quick reference files inside the skill.
- Do not duplicate long rules across `SKILL.md` and references. Put details in one place and link from the orchestrator.
- Keep references one level from `SKILL.md`; avoid deep reference chasing.
- For files over 100 lines, add a short table of contents or section list near the top.

## Exit Contract

Before leaving this lane:

1. Update `skill-journal.md` with files created/changed, validation still needed, and the next best lane.
2. Check that the journal satisfies `Create -> Validate` in the Context Sufficiency Standard.
3. Add a `## Handoff` block with current lane, completed work, recommended next lane, reason, exact artifacts to read, and one next action.
4. Return to the orchestrator lane table. Do not continue directly into another specialist.

Route to [validate.md](validate.md) after creating or editing files.
Route back to [design.md](design.md) if implementation reveals a blueprint mismatch.
