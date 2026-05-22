# skills

Personal Codex skills repository for collecting, reviewing, and distributing reusable workflows.

This repo is intentionally structured as a Codex plugin:

- `skills/` stores individual skills. Each skill lives in `skills/<skill-name>/SKILL.md`.
- `.codex-plugin/plugin.json` describes the distributable plugin package.
- `scripts/catalog-skills.mjs` generates a lightweight skill index from local skill frontmatter.

## Add a Skill

Create a new skill directory:

```bash
mkdir -p skills/my-skill
```

Add `skills/my-skill/SKILL.md`:

```markdown
---
name: my-skill
description: Use when the agent should follow this workflow.
---

# My Skill

## Workflow

1. Read the local context.
2. Run the relevant checks.
3. Return the result with evidence.
```

Then refresh the index:

```bash
npm run catalog
```

## Validate

Validate the plugin manifest and skill frontmatter with the local Codex validator:

```bash
python3 /Users/jingyang/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py .
```

## Distribution

This repo can be cloned directly or referenced as a source of skills for Codex/plugin workflows. Keep private or sensitive scripts out of this repository unless they are intentionally meant to be shared.
