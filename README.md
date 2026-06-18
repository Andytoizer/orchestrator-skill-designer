# Orchestrator Skill Designer

Orchestrator Skill Designer is a Codex skill for designing and creating other Codex skills with an orchestrator/specialist/frameworks/systems model.

Use it when a skill should behave like a small operating system rather than a single prompt file:

- an orchestrator owns intake, lane selection, gates, and final synthesis
- specialists own focused lanes of work
- frameworks hold reusable judgment, rubrics, examples, and templates
- systems/tools handle deterministic or fragile work
- a compact journal preserves state across specialist handoffs and context compaction

## Repository Contents

```text
skills/orchestrator-skill-designer/
├── SKILL.md
├── agents/openai.yaml
├── specialists/
│   ├── grill.md
│   ├── design.md
│   ├── create.md
│   └── validate.md
└── references/
    ├── forward-testing.md
    ├── frameworks-and-systems.md
    ├── orchestrator-pattern.md
    ├── packaging-rules.md
    └── skill-journal.md
```

## Install

Copy the skill folder into your Codex skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/orchestrator-skill-designer "${CODEX_HOME:-$HOME/.codex}/skills/"
```

Restart or refresh Codex if your environment does not automatically discover new skills.

## Usage

Invoke the skill explicitly:

```text
Use $orchestrator-skill-designer to design and create an orchestrator-style skill for my workflow.
```

The skill starts with a grill-style discovery lane, then designs the skill blueprint, creates or updates the skill files, and validates the result.

## Design Principles

The packaged skill is intentionally self-referential: it follows the same pattern it teaches.

- `SKILL.md` stays lean and acts as the orchestrator.
- `specialists/` contains focused lanes.
- `references/` contains reusable frameworks and packaging rules.
- `skill-journal.md` is created at runtime by the skill to track compact progress.
- Specialists must hand back to the orchestrator instead of cascading directly into each other.

## Context Discipline

The skill is designed to reduce avoidable context bloat:

- read the journal first
- load exactly one specialist lane at a time
- load only the references named by that lane
- repair a thin journal instead of reading the whole skill folder
- write exact handoff artifacts before changing lanes

## Validation

Run the Codex skill validator after installing or modifying the skill:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" \
  "${CODEX_HOME:-$HOME/.codex}/skills/orchestrator-skill-designer"
```

If your Python environment does not include `PyYAML`, install it into a temporary target and use `PYTHONPATH`:

```bash
python3 -m pip install --target /tmp/codex-pyyaml PyYAML
PYTHONPATH=/tmp/codex-pyyaml python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" \
  "${CODEX_HOME:-$HOME/.codex}/skills/orchestrator-skill-designer"
```

## Public Packaging Notes

This repository contains no secrets, private customer data, local `.env` files, or machine-specific paths. It is packaged as a reusable Codex skill.
