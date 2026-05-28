---
name: goal-crafter
description: "Turn rough work requests into strong Codex /goal objectives with measurable outcomes, verification evidence, constraints, iteration policy, and blocked stop conditions. Use when the user asks to write, refine, strengthen, or translate a task into a Goal; says things like 帮我写 goal, 制定可执行目标, 收敛成 goal, turn this into /goal, keep working until done, continue until fixed, or wants Codex to persist across multiple turns until evidence says the task is complete."
---

# Goal Crafter

Create a concise, auditable `/goal` command. Do not implement the task. Do not start a Goal unless the user explicitly asks you to create it in the current thread.

## Fit Check

First decide whether a Goal is appropriate.

Use a Goal when the task has:

- a durable objective that may need multiple turns,
- an evidence-based finish line,
- an uncertain path where the next step depends on what Codex learns.

Good fits: performance tuning, flaky test investigation, bug hunts requiring reproduction, dependency migrations, multi-step refactors, benchmark-driven optimization, PR queue cleanup, release readiness audits, research reproduction, evidence-backed product or technical audits.

Poor fits: one-line edits, simple explanations, short code reviews, single command questions, vague wishes like "make this better", or tasks where the user wants one answer and then a stop.

If the task is a poor fit, say so briefly and provide the better normal prompt instead of forcing a Goal.

## Build the Goal Contract

Extract or ask for the six contract fields:

1. Outcome: what must be true when done.
2. Verification surface: tests, benchmark, command output, report, artifact, logs, source links, screenshots, or other evidence that proves it.
3. Constraints: what must not regress or what must stay unchanged.
4. Boundaries: allowed repos, files, tools, data, external systems, and forbidden actions.
5. Iteration policy: how Codex should choose and report the next action after each attempt.
6. Blocked stop condition: when to stop and what to report if no defensible path remains.

Ask at most three short questions only if a missing field would make the Goal unsafe or unverifiable. Otherwise make a conservative assumption and label it.

## Output Format

Return:

1. Recommendation: `Use a Goal` or `Use a normal prompt`.
2. Draft command: one copy-ready `/goal ...` block.
3. Why this is complete: 2-4 bullets mapping the command to evidence, constraints, and stop condition.
4. Optional tightening questions only if needed.

Keep the `/goal` compact but complete. Prefer one paragraph, not a long specification.

Use this pattern:

```text
/goal <desired end state>, verified by <specific evidence>, while preserving <constraints>. Use <allowed inputs, tools, or boundaries>. Between iterations, <how to choose and report the next best action>. If blocked or no valid paths remain, stop with <attempted paths, evidence gathered, blocker, and next input needed>.
```

## Research Goals

For research, reproduction, or market/audit work, require a final artifact and explicit uncertainty labels.

The Goal should ask Codex to:

- inventory claims or questions,
- map each claim to evidence,
- separate confirmed findings, proxy support, approximate reconstruction, blocked claims, and remaining uncertainty,
- cite or reference the evidence surface used.

Example:

```text
/goal Produce the strongest evidence-backed audit of <topic> using the available source materials and local resources, verified by a final report that maps each key claim to evidence. Attempt feasible reproductions or checks, separate confirmed findings, proxy support, blocked claims, and remaining uncertainty, and do not overstate approximate results as exact proof. If sources, data, or permissions block progress, stop with the claim inventory, evidence gathered, blockers, and the next inputs needed.
```

## Engineering Goals

For engineering work, name exact commands or artifact checks when possible. Include correctness constraints before optimization constraints.

Examples:

```text
/goal Make the checkout test suite pass on the current branch, verified by `pnpm test checkout`, while preserving public API behavior and avoiding unrelated refactors. Use the checkout service code, fixtures, and related tests only. Between iterations, record the failing signal, the change attempted, and the next most likely root cause. If the test cannot run or no valid fix remains, stop with the reproduction evidence, attempted paths, blocker, and required next input.
```

```text
/goal Reduce p95 checkout latency below 120 ms, verified by the checkout benchmark, while keeping the correctness suite green. Use only checkout service code, benchmark fixtures, and related tests. Between iterations, compare benchmark output, identify the current bottleneck, and try the smallest defensible experiment. If benchmarks are unavailable or no valid path remains, stop with the measurements, attempted optimizations, blocker, and next input needed.
```

## Guardrails

- Do not mark a Goal complete in the draft. Completion depends on future evidence.
- Do not hide uncertainty. If proxy evidence is allowed, label it as proxy evidence.
- Do not use Goals to bypass user approval for destructive commands, production changes, database writes, purchases, or credential use.
- Include budgets only when the user asks for a token/time budget or when the surrounding system supports explicit budgeted Goals.
- Keep lifecycle commands out of the draft unless the user asked how to manage Goals.
