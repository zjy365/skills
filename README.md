# zjy365 Skills

[![skills.sh](https://skills.sh/b/zjy365/skills)](https://skills.sh/zjy365/skills)

Reusable agent skills for Codex and other tools supported by [skills.sh](https://www.skills.sh/).

This repository is meant to be installed directly with `npx skills`. You do not need to clone it.

## Install

Install all skills into the current project:

```bash
npx skills add zjy365/skills --all
```

Install only one skill:

```bash
npx skills add zjy365/skills --skill objective-crafter
```

Install globally for your user:

```bash
npx skills add zjy365/skills --global --all
```

Install for Codex explicitly:

```bash
npx skills add zjy365/skills --agent codex --all
```

Preview available skills without installing:

```bash
npx skills add zjy365/skills --list
```

## Available Skills

| Skill | Use When |
| --- | --- |
| `objective-crafter` | Turn a rough task into a strong Codex `/goal` with a measurable outcome, verification evidence, constraints, iteration policy, and blocked stop condition. |

The generated catalog is also available in [docs/SKILLS.md](docs/SKILLS.md).

## Common Commands

List installed project skills:

```bash
npx skills list
```

List global skills:

```bash
npx skills list --global
```

Update installed skills:

```bash
npx skills update
```

Remove installed skills:

```bash
npx skills remove
```

## Repository Structure

```text
skills/
  objective-crafter/
    SKILL.md
    agents/openai.yaml

.codex-plugin/plugin.json
docs/SKILLS.md
scripts/catalog-skills.mjs
```

Each skill lives in `skills/<skill-name>/` and must include a `SKILL.md` file with `name` and `description` frontmatter.

## Maintainers

Add or update a skill under `skills/<skill-name>/`, then refresh the catalog:

```bash
npm run catalog
```

Validate before publishing changes:

```bash
npm run validate
```

Check the public install surface:

```bash
npx skills add zjy365/skills --list
```

Do not commit secrets, credentials, cookies, or machine-specific private paths. Everything in this repository should be safe for public installation.
