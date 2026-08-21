# Public UI Resource Map

This reference is distributed with `ui-router`. It contains public resources only. Availability, installation state, package versions, and framework compatibility must be checked against the user's project before adoption.

## Public UI Skills and Design References

| Resource | Public source | Use when | Boundary |
| --- | --- | --- | --- |
| `apple-design` | [emilkowalski/skills](https://github.com/emilkowalski/skills) | macOS, native-feeling, or Apple-platform interaction patterns | External skill; do not treat it as installed unless the current environment provides it. |
| `baseline-ui` | [ibelick/ui-skills](https://github.com/ibelick/ui-skills) | Baseline UI quality, layout, and component refinement | Use as a review or implementation aid, not as a replacement for a product design system. |
| `brandkit` | [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | Brand direction and visual identity work | Verify the repository's current contents and licensing before use. |
| `critique` | [UI skills directory](https://skills.sh/) | Reviewing an existing interface before redesign | External candidate; pair with the actual product constraints and evidence. |
| `create-design-md` | [UI skills directory](https://skills.sh/) | Capturing project-specific design tokens and conventions | The resulting design document must describe the target project, not this public map. |
| `image-to-code` | [UI skills directory](https://skills.sh/) | Reconstructing an interface from a screenshot or visual reference | Preserve responsive behavior and semantics instead of tracing pixels blindly. |
| `layout` | [UI skills directory](https://skills.sh/) | Information architecture, spacing, and responsive structure | Choose based on the target workflow and content density. |
| `polish` | [UI skills directory](https://skills.sh/) | Final visual refinement after implementation | Do not use polish to hide unresolved interaction or accessibility problems. |
| `ui-skills-root` | [UI skills directory](https://skills.sh/) | General UI skill discovery when no narrower route fits | External candidate; never use it as a private fallback. |

## Public Libraries and Component Sources

| Category | Public resources | Selection note |
| --- | --- | --- |
| Components | [shadcn/ui](https://ui.shadcn.com/), [Radix Primitives](https://www.radix-ui.com/primitives), [React Aria](https://react-spectrum.adobe.com/react-aria/) | Prefer accessible primitives and source ownership that fit the project's framework and styling model. |
| Design references | [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/), [Material Design](https://m3.material.io/), [Nielsen Norman Group](https://www.nngroup.com/articles/) | Use principles as evidence; do not copy a complete visual system without checking product context. |
| Icons | [Lucide](https://lucide.dev/), [Heroicons](https://heroicons.com/), [Phosphor](https://phosphoricons.com/) | Check icon style consistency, license, accessibility labels, and bundle impact. |
| Charts | [Recharts](https://recharts.org/), [Apache ECharts](https://echarts.apache.org/), [Visx](https://airbnb.io/visx/) | Select by interaction complexity, rendering model, data scale, and framework fit. |
| Editors | [Tiptap](https://tiptap.dev/), [Lexical](https://lexical.dev/), [ProseMirror](https://prosemirror.net/) | Select by schema needs, collaboration requirements, extensibility, and accessibility. |
| Data grids | [TanStack Table](https://tanstack.com/table), [AG Grid](https://www.ag-grid.com/), [Handsontable](https://handsontable.com/) | Use a grid only when the workflow needs structured editing, sorting, filtering, or virtualization. |
| Animation | [Motion](https://motion.dev/), [GSAP](https://gsap.com/), [Web Animations API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API) | Match the implementation to the interaction: CSS or WAAPI for simple transitions, a timeline library for complex choreography. |

## Public Visual and Prototyping Tools

| Resource | Public source | Use when | Boundary |
| --- | --- | --- | --- |
| LogoCreator | [logo-creator.io](https://www.logo-creator.io/) | Exploring logo directions from a company name, industry, or style | Treat generated marks as explorations; verify originality, licensing, and brand fit. |
| Lovable | [lovable.dev](https://lovable.dev/) | Quickly prototyping a web product from a natural-language brief | Review generated code, dependencies, authentication, data models, and security before production use. |
| v0 | [v0.dev](https://v0.dev/) | Exploring React and shadcn-style interface concepts | Generated output is a starting point and requires project-specific review. |

## Routing Boundaries

- Public URLs do not prove that a resource is installed, maintained, accessible, or suitable for a specific product. Verify those claims before recommending adoption.
- Do not combine multiple competing visual-direction systems by default. Choose one direction and use implementation libraries only to support it.
- Do not recommend a large editor, grid, or charting dependency for a static display.
- Do not include personal installation lists, machine paths, credentials, private project context, or private benchmark data in this map.
