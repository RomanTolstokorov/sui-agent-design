# Teletronics SUI Agent Instructions

## What This Repo Is

Local structured knowledge for agents drawing **Teletronics SUI** Figma screens. There is no build system, test suite, or deployable app.

- `figma/` - design-system metadata, component keys, tokens, and source references
- `app/` - app composition rules, product knowledge, screen docs, flows, and drawing instructions

## Lookup Order

**Always read before starting any task:**

1. `app/rules.md`
2. `app/figma-map.json`
3. Product-specific docs from `app/apps/<app-id>.md` and `app/apps/<app-id>.json`
4. Screen docs from `app/screens/<app-id>/` (canonical layout + relevant state doc)

**Load on demand — only when the task touches these concerns:**

- `figma/components/index.json` — placing or verifying a SUI component
- `figma/components/form-blocks.json` — drawing task or document form blocks
- `figma/foundations/colors.json` — resolving a color or elevation variable
- `figma/foundations/typography.json` — resolving a text style
- `figma/foundations/layout.json` — resolving a spacing or corner-radius token
- `figma/source.json` — need the DS file key or variable collection IDs directly

Do not fetch canonical Figma nodes for frame structure when a local canonical layout exists.

## Knowledge Layout

Each app has four tiers of documentation:

- `app/apps/<id>.md` — product purpose, main regions, drawing rules, and screen inventory
- `app/apps/<id>.json` — machine-readable metadata: Figma file key, canonical node reference, important node IDs, and related flows
- `app/screens/<id>/canonical-layout.md` — step-by-step frame construction for the canonical screen layout; use as the starting point for any new screen
- `app/screens/<id>/<state>.md` — a specific screen state or variant; use alongside `canonical-layout.md` when the task targets that state

## Hard Rules

- All application screens are RTL. Use English labels unless Arabic copy is provided; preserve room for future Arabic translation.
- Treat the Teletronics SUI design-system file as read-only.
- Place UI elements from published SUI components only. Before placing anything in Figma, verify it is listed in `figma/components/index.json`. If no matching SUI component exists, stop and ask — describe exactly what is missing and why. Never silently fall back to primitives.
- Import components using the workflow in `app/instructions/sui-component-imports.md`.
- Bind fills and strokes to published variables by `variableKey`; apply elevation by importing effect styles by `styleKey`.
- Apply typography by importing published text styles by `styleKey`; do not set raw font family, size, weight, line height, or letter spacing when a matching style exists.
- For icons, use the `<Icon>` wrapper and follow `app/instructions/icons-imagery.md`; never color the wrapper or swapped inner icon instance container.
- An `island` is a separated functional unit (controls, forms, previews, lists, tables, details, supporting panels). Islands follow a dense bento-style composition with `spacing/1` (8 px) gaps between siblings.
- App, screen, and flow docs override generic instructions when they describe a more specific workflow.

## Detailed Instructions

- `app/instructions/component-instance-text.md` — editing text inside library component instances
- `app/instructions/figma-api-gotchas.md` — Figma API and `use_figma` scripting quirks
- `app/instructions/icons-imagery.md` — icon wrapper usage, size variants, and icon catalog
- `app/instructions/modal-dialogs.md` — generic modal/dialog drawing workflow
- `app/instructions/sui-component-imports.md` — importing SUI components and component sets safely
- `figma/components/form-blocks.json` — form block wrappers, content components, and ready variants for task and document forms

## Apps and Flows

Resolve all app names, aliases, canonical file references, screen doc paths, and related flows through `app/figma-map.json`.

User Preferences has no `canonical-layout.md` by design — it is modal-scoped; entry points and states are documented in `app/screens/user-preferences/*.md`.
