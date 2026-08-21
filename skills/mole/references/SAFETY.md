# Mole Safety Protocol

Apply this protocol whenever Mole may delete data, uninstall software, change
system configuration, or update itself. The governing principle is: reclaiming
less space is acceptable; deleting user state by mistake is not.

## Platform Gate

Run `uname -s` before any Mole command. Continue only when the output is exactly
`Darwin`. Mole's supported mainline CLI, filesystem rules, Trash behavior,
application model, and safety assumptions are specific to macOS.

Do not run this skill on Windows or Linux. Do not treat Mole's experimental
Windows branch as compatible with this protocol; it requires separately
verified commands and deletion guarantees. On an unsupported platform, report
the limitation and stop without installing, updating, or invoking Mole.

## Risk Classes

### Read-only

These may run without destructive confirmation:

```bash
mo --version
mo <command> --help
mo analyze --json
mo analyze <path> --json
mo status --json
mo history --json --limit <1-200>
mo uninstall --list
```

Bound long-running status watches by duration or sample count. Do not leave a
monitor running in the background.

### Preview required

These commands may discover candidates but must not change them during review:

```bash
mo clean --dry-run
mo uninstall --dry-run <exact-app-name>
mo purge --dry-run
mo installer --dry-run
mo optimize --dry-run
```

Never remove `--dry-run` until the user has seen and confirmed the resulting
plan in a later message.

### Explicit exact-action approval required

Treat these as separate high-risk operations:

```bash
mo uninstall --permanent <exact-app-name>
mo update
mo update --nightly
mo remove
mo touchid enable
mo touchid disable
```

Approval for cleanup or uninstall does not authorize update, self-removal,
Touch ID configuration, or permanent deletion.

## Classify Preview Evidence

Keep these values separate in every report:

1. **Deletion candidates**: exact paths in the current dry-run plan.
2. **Known candidate total**: sum of candidates whose sizes were measured.
3. **Mole estimate**: a summary estimate that may be rounded or partial.
4. **Diagnostic clues**: Docker storage, simulator data, backups, large files,
   or other items Mole reports for investigation but did not select.
5. **Unknown or partial data**: candidates without reliable size, scans that
   timed out, or sections Mole skipped.

Only deletion candidates belong in "will be removed." Never add diagnostic
clues to the total. Do not add overlapping parent and child paths twice.

For `mo clean --dry-run`, treat `~/.config/mole/clean-list.txt` as the candidate
ledger. Read the complete file. Ignore comments and summary lines when counting
paths, preserve paths exactly, and group them by the section headers Mole wrote.
If the ledger is missing, unreadable, malformed, stale, or inconsistent with
the terminal summary, stop without deleting.

For `uninstall`, `purge`, `installer`, and `optimize`, use the complete dry-run
output. If the installed version does not expose enough detail to identify the
exact targets and effects, report that limitation and keep the workflow in
preview-only mode.

## Sensitive and Ambiguous Data

Call out and default to preserving any candidate that may contain:

- credentials, tokens, authentication state, sessions, cookies, or databases,
- user documents, project source, Git worktrees, ignored private files, or
  unsynced content,
- AI/developer-tool workspaces, virtual machines, model data, config, or active
  runtime state,
- `Application Support` data without exact app evidence,
- package/toolchain stores that may contain more than rebuildable downloads,
- external, removable, network, cloud-synced, or backup volumes,
- an active application's files or a path currently held open by a process.

Do not decide safety from a directory name such as `cache`, `tmp`, `old`, or
`orphaned` alone. If recovery and ownership are unclear, recommend whitelist or
manual inspection and exclude the item from approval.

## Confirmation Contract

After preview, show a confirmation block containing:

```text
Command to run: <exact command without --dry-run>
Candidates: <count>
Known size: <size, explicitly excluding unknowns>
Permanent deletion: <count and size>
Move to Trash: <count and size>
Preserved/skipped: <count and reasons>
Diagnostic clues not included: <count and examples>
Uncertainties: <none, or exact limitations>
```

Then stop. A destructive command can run only after the user replies in a later
message with explicit approval tied to this plan. "Delete only X" authorizes a
new narrowed preview, not immediate deletion. Silence, prior approval, and a
different command's approval do not count.

## Revalidate Before Execution

Immediately before the real command:

1. Confirm the resolved `mo` executable and version match the preview.
2. Confirm the real command matches the previewed command except `--dry-run`.
3. Confirm the candidate ledger or captured output is the approved version.
4. Confirm each candidate still exists with the same object type.
5. Refuse candidates that became symlinks or whose resolved location changed.
6. Check sensitive application/process state again when it affected approval.
7. Treat material size, path, candidate-count, or recovery-mode changes as a
   new plan that requires another preview and confirmation.

Do not hand individual paths to raw deletion commands. Let Mole re-discover and
apply its own path validation, whitelist, app protection, and deletion routing.

## Fail Closed

Stop without making changes when:

- the dry run exits nonzero or is interrupted,
- output is truncated, malformed, contradictory, or cannot be parsed safely,
- a scan timed out or produced only partial candidates,
- target sizes are unknown in a way that affects the user's decision,
- `mo` changed version or executable since preview,
- targets changed identity, type, ownership, mount, or symlink state,
- the real command would require flags absent from the preview,
- Mole requests authorization or an interactive choice that the user has not
  already reviewed,
- the audit log is unavailable for a destructive run.

Explain the exact cause and the safest next action. Do not work around Mole's
refusal with `sudo`, raw filesystem commands, or a custom script.

## Verify the Outcome

After execution, run `mo history --json --limit 20` and identify the matching
session. Report:

- the exact command and completion status,
- previewed and actual candidate counts,
- removed, trashed, skipped, and failed counts,
- previewed known size versus the recorded actual size,
- deletion and operations log paths,
- any mismatch, partial failure, or item that remained.

If no matching history entry exists, say verification is incomplete. Do not
claim success or reclaimed space solely because the command exited zero.
