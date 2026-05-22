# Repository Guidelines

This repository stores reusable personal Codex skills for organization and distribution.

## Structure

- Put each skill under `skills/<skill-name>/`.
- Every skill must include `SKILL.md` with YAML frontmatter containing `name` and `description`.
- Keep optional files local to the skill directory, such as `scripts/`, `references/`, `templates/`, `assets/`, and `evals/`.
- Keep `.codex-plugin/plugin.json` valid; it is the plugin distribution manifest.

## Editing Rules

- Do not commit secrets, local credentials, API keys, cookies, or private machine paths unless they are examples.
- Prefer small, self-contained skills over broad collections of unrelated instructions.
- When importing an existing local skill, review it for private data and hard-coded paths before adding it here.
- Run `npm run catalog` after adding, renaming, or deleting skills.
- Run the plugin validator before publishing changes.

## Skill Quality Bar

- The trigger description should say when to use the skill, not just what it is called.
- Workflows should be concrete enough for another agent to execute.
- References and scripts should be included only when they reduce ambiguity or repeated manual work.
