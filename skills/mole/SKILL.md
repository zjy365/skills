---
name: mole
description: "Safely operate the Mole (`mo`) macOS-only cleanup CLI for disk analysis, cleanup previews, app uninstall, project artifact cleanup, installer removal, optimization, status, and history. Use on macOS when a user asks to inspect disk usage, free storage, clean caches or old projects, remove an app, find installers, diagnose Mac health, or review what Mole changed; do not use on Windows or Linux."
---

# Mole

Use the installed `mo` CLI as a safety-first interface to Mac maintenance. This
skill is for Mole users, not Mole source development.

## Non-Negotiable Rules

1. Never replace Mole with `rm`, `find -delete`, or a generated deletion script.
2. Run every destructive workflow in dry-run mode first.
3. Show the user the exact current deletion plan before changing anything.
4. Stop after preview. Execute only after a later user message explicitly
   confirms that displayed plan.
5. Never infer confirmation from the original request, prior sessions, or a
   generic reply such as "continue" when the candidate set has changed.
6. Never use `--permanent` unless the user explicitly requests permanent
   deletion after seeing the preview.
7. When evidence is incomplete or ambiguous, skip the item or stop the run.

Read [references/SAFETY.md](references/SAFETY.md) before any operation that may
delete files, uninstall software, modify system state, or update Mole.

## Preflight

Before any Mole command:

```bash
uname -s
command -v mo
mo --version
mo <command> --help
```

Continue only when `uname -s` returns exactly `Darwin`. Mole's supported
mainline CLI and this skill's safety guarantees are macOS-specific; the
experimental Windows branch and Linux are out of scope. Use the installed `mo`
on `PATH`, never a source checkout. If the platform is unsupported or Mole is
missing, report it and stop. Trust live help when flags differ without weakening
these safety rules.

## Route the Request

| User intent | First command |
| --- | --- |
| Find disk usage | `mo analyze --json` or `mo analyze <path> --json` |
| Check Mac health | `mo status --json` |
| Review past actions | `mo history --json --limit 20` |
| Free disk space | `mo clean --dry-run` |
| Remove an app | `mo uninstall --dry-run <exact-app-name>` |
| Remove project artifacts | `mo purge --dry-run` |
| Remove installer files | `mo installer --dry-run` |
| Run maintenance | `mo optimize --dry-run` |

Prefer JSON and non-interactive output. Do not scrape full-screen TUI frames.
Use `mo uninstall --list` to resolve an exact app name before uninstalling.

## Preview Report

For `clean`, read `~/.config/mole/clean-list.txt` after the dry run. For other
commands, capture the complete dry-run output. Report:

- the exact paths selected for deletion,
- per-item and total sizes when known,
- whether each item is rebuildable, recoverable through Trash, or permanent,
- protected or skipped items,
- scan timeouts, unknown sizes, and partial results,
- clues that Mole only reported but did not add to the deletion plan.

Do not present Docker reclaimable space, simulator data, or other diagnostic
clues as cleanup candidates unless their exact paths are in the current plan.

End a successful preview with a bounded confirmation statement naming the
command, candidate count, known total size, permanent count, Trash count, and
uncertainties. Do not execute in the same turn.

## Execute and Verify

After explicit confirmation, revalidate the plan as defined in
[references/SAFETY.md](references/SAFETY.md). If it changed, show a new preview
and stop for new confirmation. Otherwise run the matching command without
`--dry-run`, then inspect:

```bash
mo history --json --limit 20
```

Report previewed versus actual item counts and sizes, removed versus trashed
items, skips, failures, and the audit-log paths. Never claim reclaimed space
from the preview alone.

## High-Risk Operations

Do not perform `mo update`, `mo update --nightly`, `mo remove`, `mo touchid`, or
any `--permanent` operation unless the user explicitly asks for that exact
state-changing action. Explain its effect first and follow the confirmation
rules in the safety reference.
