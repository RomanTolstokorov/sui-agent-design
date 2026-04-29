# Application Composition Rules

Use this file for project-specific rules about how to build Teletronics SUI-based application screens. These rules are not design-system source metadata; they describe how this project composes screens, frames, flows, and content using the design system.

## Language and Direction

- Build all application screens in RTL.
- Use English labels and text as working copy/placeholders unless Arabic copy is provided.
- Preserve enough label length and layout flexibility for future Arabic translation.

## Surface Rules

- Every app, screen, modal, dialog, drawer, or nested application context must start from `background/surface_0` bound as a Figma variable, not a raw color value.
- Use `background/surface_*` tokens by local contrast need, not as a strict elevation ladder.
- Use `background/surface_3` for cards, panels, menus, and content containers when a stronger container contrast is needed.
- Add elevation effects only when an element should visually float above its current surface; surface number alone does not imply elevation depth.

## Layout Rules

- S-System is a data-heavy application with many sub-applications, controls, forms, previews, lists, and data panels.
- Application screens must prioritize fast scanning, compact information density, and predictable placement across small and large viewports.
- A separated functional unit is called an `island`; use islands for controls, forms, previews, lists, tables, details, and supporting panels.
- Islands follow a dense bento-style composition.
- The gap between sibling islands is always `spacing/1` (8px).
- Prefer `cornerRadius/2` (8px) for standard islands unless a component or overlay requires another radius.
- Do not use large decorative whitespace between islands in data-heavy screens.
- Keep related controls close to the content they affect.

## SUI-Only Drawing Rule

Never draw a UI element from primitives if a published Teletronics SUI component exists for it. Before placing anything in Figma, verify it is in `figma/components/index.json`. If no matching SUI component exists, stop and ask the user for permission before using a custom or primitive approach — describe exactly what is missing and why. Never silently fall back to hand-built elements.

## Common App Patterns

- Top bar plus one dominant content island and a narrow side island.
- Top bar plus main content island and right supporting panel.
- Top bar plus left navigation/list island, central preview/detail island, and right inspector/actions island.
- Top bar plus asymmetric bento grid for mixed controls, previews, summaries, and lists.
- Stacked top controls plus three-column working area.
