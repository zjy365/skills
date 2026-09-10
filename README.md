# zjy365 Skills

Reusable agent skills for Codex and other tools supported by [skills.sh](https://skills.sh/).

[中文说明](README.zh-CN.md)

## What You Can Do

| Skill | Use it for |
| --- | --- |
| `ui-router` | Choose the right UI skills for design, implementation, redesign, motion, accessibility, and visual quality work. |
| `mole` | Analyze disk usage, check system status, clean caches, uninstall apps, and free space on macOS. Destructive actions are previewed and require confirmation. |
| `media-tools` | Compress, convert, resize, and prepare local images and videos for X/Twitter, Instagram, WhatsApp, email, or the web without uploading the media. |
| `objective-crafter` | Turn a rough idea into an executable Codex `/goal` with a measurable outcome, verification steps, constraints, and stop conditions. It writes the Goal but does not execute it. |

## Install

```bash
npx skills add zjy365/skills
```

## Use

After installation, describe your task naturally or mention a skill explicitly.

Choose the right UI skills:

```text
Use $ui-router to decide which UI skills should come first when redesigning this SaaS dashboard.
```

Safely inspect and clean a Mac:

```text
Use $mole to check what can be safely cleaned on my Mac. Show me a preview and do not delete anything yet.
```

Prepare a local video for X/Twitter:

```text
Use $media-tools to process ./demo.mov for X/Twitter.
```

Create an executable objective:

```text
Use $objective-crafter to turn "make this project faster" into a verifiable /goal.
```

## Common Commands

List installed skills:

```bash
npx skills list
```

Update installed skills:

```bash
npx skills update
```

Remove installed skills:

```bash
npx skills remove
```

## Safety

`mole` supports macOS only. For cleanup, uninstall, or system changes, it creates a preview first and waits for explicit confirmation of the exact plan. A cleanup approval does not automatically authorize permanent deletion or other high-risk operations.
