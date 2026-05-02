# CLAUDE.md

## What This Repo Is

Local structured knowledge for Claude Code agents drawing **Teletronics SUI** Figma screens. There is no build system, test suite, or deployable app.

- `figma/` - design-system metadata, component keys, tokens, and source references
- `app/` - app composition rules, product knowledge, screen docs, flows, and drawing instructions

## Required Lookup Order

Before drawing any Figma screen, read:

1. `app/rules.md`
2. `app/figma-map.json`
3. Product-specific docs from `app/apps/<app-id>.md` and `app/apps/<app-id>.json`
4. For new screens, `app/screens/<app-id>/canonical-layout.md`
5. `figma/source.json`
6. `figma/components/index.json`
7. `figma/foundations/colors.json`
8. `figma/foundations/typography.json`
9. `figma/foundations/layout.json`

Use local indexes for typography, color, spacing, and component keys during routine mockup work. Do not fetch canonical Figma nodes just to determine frame structure when a local canonical layout exists.

## Hard Rules

- All application screens are RTL.
- Use English labels unless Arabic copy is provided; preserve room for future Arabic translation.
- Treat the Teletronics SUI design-system file as read-only.
- Insert UI elements from published SUI components listed in `figma/components/index.json`; use the safe import workflow in `app/instructions/sui-component-imports.md`.
- Never draw a custom UI element when a SUI component exists. If no matching SUI component exists, stop and ask before using primitives.
- Bind fills and strokes to published variables by `variableKey`; apply elevation by importing effect styles by `styleKey`.
- App, screen, and flow docs override generic instructions when they describe a more specific workflow.

## Detailed Instructions

- `app/instructions/component-instance-text.md` - editing text inside library component instances
- `app/instructions/modal-dialogs.md` - generic modal/dialog drawing workflow
- `app/instructions/sui-component-imports.md` - importing SUI components and component sets safely

## Active Apps and Flows

- Task Management: `app/apps/task-management.md`, `app/screens/task-management/canonical-layout.md`
- Documents: `app/apps/document.md`, `app/screens/document/canonical-layout.md`
- Search: `app/apps/search.md`, `app/screens/search/canonical-layout.md`
- User Preferences: `app/apps/user-preferences.md`, `app/screens/user-preferences/*.md`
- Type Icon Appearance Preference flow: `app/flows/type-icon-appearance-preference.md`

Resolve app names, aliases, canonical references, and related flows through `app/figma-map.json`.

## Sibling Instruction File

`AGENTS.md` mirrors this file for non-Claude agents (Codex, etc.). Keep both in sync when editing either.
