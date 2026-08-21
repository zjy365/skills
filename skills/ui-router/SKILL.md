---
name: ui-router
description: "Choose and use the right UI skills for frontend design, implementation, redesign, animation, accessibility, responsive layout, and visual quality work. Use whenever a UI request could benefit from specialized design skills, especially when the user is unsure which skill to use or gives a broad request such as build, redesign, improve, polish, animate, audit, or recreate an interface."
---

# UI Router

Route UI work to the smallest effective set of specialized UI skills. The goal is to use the right skills in the right order, not to produce a routing report.

Read [`references/ui-skill-catalog.md`](references/ui-skill-catalog.md) when the request needs skill selection. The catalog lists public UI skills, their purposes, and source repositories.

## Route the Work

1. Identify the product context and current phase:
   - new UI: establish direction, then implement;
   - existing UI: critique before changing broad visual behavior;
   - defined problem: route directly to the narrow repair skill;
   - completed implementation: audit, then polish.
2. Choose one primary skill that owns the main decision or implementation.
3. Add supporting skills only when they have separate jobs. Two or three skills are normally enough.
4. Keep one visual direction. Do not combine Apple, minimalist, brutalist, high-end, and other competing taste skills unless the user asks to compare directions.
5. If the user asks for implementation, invoke the primary skill and proceed. Apply supporting skills in sequence when their phase arrives.
6. If the user only asks which skill to use, answer with the primary skill, optional supporting skills, and one short reason.

## Default Routes

Start with the first skill, then add the next skill only when that phase is needed. Keep a route to three skills or fewer.

| UI task | Route |
| --- | --- |
| Build a production UI from requirements | `design` → `audit` → `polish` |
| macOS or Apple-platform product | `apple-design` → `design` → `audit` |
| SaaS, dashboard, or operational tool | `design-taste-frontend` → `design` → `audit` |
| Landing page, launch page, or portfolio | `high-end-visual-design` → `design` → `polish` |
| Minimal or content-first interface | `minimalist-ui` → `design` → `polish` |
| Industrial or brutalist direction | `industrial-brutalist-ui` → `design` → `audit` |
| Redesign an existing product | `critique` → `redesign-existing-projects` → `audit` |
| Existing UI feels rough or inconsistent | `baseline-ui` → the specific repair skill → `polish` |
| Establish or recover a design system | `create-design-md` → `design` → `audit` |
| Build a brand system and product UI together | `brandkit` → `create-design-md` → `design` |
| Compare multiple UI directions | `prototype` → the chosen direction skill → `design` |
| Recreate a screenshot or design image | `image-to-code` → `layout` → `polish` |
| Choose a component library | `pick-ui-library` → `create-design-md` |
| Fix layout or responsive behavior | `layout` → `adapt` |
| Fix typography and information hierarchy | `typeset` → `polish` |
| Improve accessibility | `fixing-accessibility` → `audit` |
| Review overall UI quality | `audit` → the specific repair skill → `polish` |
| Decide where animation helps | `find-animation-opportunities` → `emil-design-eng` → an implementation skill |
| Implement simple interaction motion | `css-animations` or `waapi` → `review-animations` |
| Implement complex timelines or scroll stories | `gsap` → `review-animations` → `fixing-motion-performance` |
| Improve existing animation | `improve-animations` → `review-animations` → `fixing-motion-performance` |

## Selection Rules

- Use a direction skill before a broad implementation skill when visual direction is undecided.
- Use `critique` before a broad redesign, but skip it for a narrow, already diagnosed defect.
- Use `audit` to find and verify problems. Use `polish` only after structural, accessibility, responsive, and performance issues are addressed.
- Use `layout`, `typeset`, `adapt`, `colorize`, `quieter`, `bolder`, `distill`, or `clarify` for a specific visible weakness instead of restarting the design.
- Use `emil-design-eng` for motion judgment; use `css-animations`, `waapi`, `animejs`, or `gsap` for implementation according to complexity.
- If the ideal skill is unavailable, recommend it with its public repository from the catalog. Use an installed substitute only when it performs the same UI job without changing the intended direction.
- Never route to an unrelated skill merely because it ships in the same repository. Do not install external skills unless the user asks or installation is already authorized.

## Response Behavior

For implementation requests, keep routing brief and start the work:

```markdown
Using `critique` first to identify the redesign problems, then `redesign-existing-projects` to implement the chosen direction.
```

For skill-selection questions, answer concisely:

```markdown
Primary: `apple-design`
Supporting: `layout`, `typeset`, `audit`

This is an Apple-platform workbench, so interaction behavior and native structure should be decided before layout and final quality checks.
```

Do not expose internal routing categories, availability bookkeeping, or catalog-reading steps unless the user asks for them.
