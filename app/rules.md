# Application Composition Rules

Project-specific rules for composing Teletronics SUI-based application screens. Hard rules (RTL, English copy, SUI-only, read-only DS) live in `AGENTS.md`; this file covers composition specifics.

## Surface Rules

- Every app, screen, modal, dialog, drawer, or nested application context must start from `background/surface_0` bound as a Figma variable, not a raw color value.
- Use `background/surface_*` tokens by local contrast need, not as a strict elevation ladder.
- Use `background/surface_3` for cards, panels, menus, and content containers when a stronger container contrast is needed.
- Add elevation effects only when an element should visually float above its current surface; surface number alone does not imply elevation depth.

## Layout Rules

- S-System is a data-heavy application with many sub-applications, controls, forms, previews, lists, and data panels.
- Application screens must prioritize fast scanning, compact information density, and predictable placement across small and large viewports.
- Use Figma auto layout for layout containers wherever practical, including screen regions, islands, form stacks, button rows, list/table rows, and grouped controls. Use absolute positioning only for page-level placement, overlays/backdrops, intentionally layered elements, or cases where a SUI component instance cannot participate cleanly in auto layout.
- Islands follow a dense bento-style composition. The gap between sibling islands is always `spacing/1` (8 px). Prefer `cornerRadius/2` (8 px) for standard islands unless a component or overlay requires another radius.
- Do not use large decorative whitespace between islands in data-heavy screens.
- Keep related controls close to the content they affect.

## Figma API Workaround Rule

When a Figma API or `use_figma` scripting blocker is encountered during drawing (unexpected error, silent misplacement, property rejection, undocumented behavior, etc.):

1. Stop before working around it silently.
2. Propose a new entry for `app/instructions/figma-api-gotchas.md` using the entry format defined in that file: short symptom title, exact error string, cause if known, minimal workaround code, discovery date.
3. Wait for user approval of the entry text and target file.
4. On approval, append the entry to `app/instructions/figma-api-gotchas.md` before continuing the drawing task.

Do not re-derive the same workaround across sessions. Do not skip persistence even when the fix is obvious — future agents need the registry to avoid repeating discovery.

## Figma Delivery Rule

After drawing or updating a design in Figma, include a direct link to the Figma page that contains the latest created or updated design in the final response.

## Common App Patterns

- Top bar plus one dominant content island and a narrow side island.
- Top bar plus main content island and right supporting panel.
- Top bar plus left navigation/list island, central preview/detail island, and right inspector/actions island.
- Top bar plus asymmetric bento grid for mixed controls, previews, summaries, and lists.
- Stacked top controls plus three-column working area.
