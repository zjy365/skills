---
name: ui-router
description: "Route UI, frontend, design-system, animation, accessibility, and visual-resource requests to the smallest useful set of publicly documented skills and resources. Use when a UI request needs a design direction, implementation path, library choice, or quality-review route before execution."
---

# UI Router

Use this skill as a public routing layer for UI work. Its reference map is shipped with the skill and contains only public skills, repositories, libraries, and tools. Do not read personal files, home-directory paths, environment variables, credentials, or private project notes.

## Public Resource Map

Read [`references/ui-resource-map.md`](references/ui-resource-map.md) before making a resource recommendation. Read only the sections needed for the current request; do not copy the whole map into the response.

The map is a public reference, not a guarantee that every listed tool is installed in the current environment. Verify local availability before presenting a skill as directly callable. If a candidate is not installed or is not included in the current skill package, label it as an external candidate and include its public installation or repository URL.

## Routing Workflow

1. Identify the work mode before choosing a route:
   - operate: desktop workbench, dashboard, table, settings, resource view, or high-frequency product UI
   - persuade: landing page, brand site, launch page, portfolio, or visual storytelling
   - prototype: compare materially different information architectures or visual directions
   - restore: screenshot-driven reconstruction or an existing UI redesign
   - motion: animation design, implementation, review, or performance
   - quality: accessibility, metadata, responsive behavior, performance, or final polish
   - resource: choose a component library, charting library, icon source, image tool, or design reference
2. Read the matching section in the public map. Use repository and author information when provenance or family compatibility matters; use the usage section when selecting by task.
3. Choose one primary route. Add at most two or three supporting routes when each has a distinct responsibility.
4. Keep visual direction singular. Do not combine competing taste systems such as Apple, brutalist, minimalist, high-end agency, or multiple generic taste systems unless the user explicitly asks for a comparison.
5. Separate judgment from implementation:
   - choose the product direction and constraints first;
   - choose the implementation skill or library second;
   - audit and polish after the implementation is concrete.
6. Check whether each selected skill is available in the current environment. Only available skills may appear as directly callable `Primary` or `Supporting` routes. Unavailable options must be listed as external candidates with a public source.
7. State the route before invoking or recommending skills.

## Public Route Defaults

These defaults use skills that are shipped in this repository. Verify availability at runtime because a user may install only part of the package:

| Request | Primary | Supporting |
| --- | --- | --- |
| Mac disk or cleanup workflow | `mole` | none |
| Turn a rough request into an executable objective | `objective-crafter` | none |
| Unclear UI request | `ui-router` | one available task-specific skill |

For UI-specific work, use the public map to select an external candidate by category, then report it as an external dependency unless the same skill is available locally. Do not invent a local fallback and do not present a missing skill as installed.

## Resource Selection Rules

- Treat external resources as references or implementation aids, not as the product's design system.
- Prefer public source ownership, maintenance status, accessibility, licensing, package weight, and framework fit over attractive screenshots.
- For React product UI, distinguish source-distribution systems such as shadcn/ui from third-party collections and generated examples.
- For charting, editors, grids, icons, and image tools, select by the actual interaction requirement and data scale; do not add a large specialist dependency for a static display.
- Preserve the target project's existing design tokens, security boundaries, information density, and interaction model when those constraints already exist.
- Do not claim benchmarks, customer outcomes, installation state, or maintenance status unless the public map or the user's project provides evidence.

## Output Contract

For a routing request, answer in this shape:

```markdown
**Route**
- Mode: <operate | persuade | prototype | restore | motion | quality | resource>
- Primary: `<available skill>` or external candidate
- Supporting: `<available skill>`, `<available skill>`

**Why**
<one or two sentences tied to the user's actual context>

**Read from the map**
- <relevant public section, author, repository, or resource>

**Availability**
- <available locally, or public installation/source URL for each external candidate>

**Boundary**
<what not to load, combine, or introduce yet>
```

If the request is already precise and implementation-ready, route briefly and proceed with the requested implementation. Do not turn a clear code edit into a design workshop.

## Maintenance

Keep the reference map limited to public information that can be distributed with this skill. When a public resource changes, update the reference map and this skill's defaults together. Never add personal paths, credentials, cookies, local installation records, or private project facts.
