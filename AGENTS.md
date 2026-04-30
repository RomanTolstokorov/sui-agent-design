# Teletronics SUI Agent Instructions

This file provides guidance to code agents working in this repository.

## What This Repo Is

Local context for agents working with the **Teletronics SUI** Figma design library. There is no build system, test suite, or deployable application; the repo is pure structured knowledge consumed by agents doing Figma design work.

- `figma/` - design system metadata, components, foundations, and source references
- `app/` - product-level rules, app-specific knowledge, screen docs, and user flows
- `.codex/config.toml` - MCP server configuration for Atlassian Jira and Teletronics MCP

## Required Lookup Order

Before drawing any Figma screen, read in this order:

1. `app/rules.md` - application composition rules: surface hierarchy, island layout, spacing defaults
2. `app/figma-map.json` - resolves app names, aliases, Figma file keys, canonical node IDs, and related flows
3. For product-specific work: `app/apps/<app-id>.md` and `app/apps/<app-id>.json`
4. For building a new screen: `app/screens/<app-id>/canonical-layout.md` - use this as the layout blueprint for frame dimensions, island split, and component keys. Do not fetch the Figma canonical node just to determine frame structure; open Figma only for content details or when the preset is explicitly insufficient.
5. `figma/source.json` - Teletronics SUI file key, library key, collection keys, and important node IDs
6. `figma/components/index.json` - all published component keys before searching Figma
7. `figma/foundations/colors.json` - color and elevation tokens and variable keys
8. `figma/foundations/typography.json` - text style keys and font loading requirements
9. `figma/foundations/layout.json` - spacing and corner radius variable keys

Do not query Figma for typography, color, spacing, or component keys during routine mockup work; all tokens are cached in the local indexes.

## Design System Key Facts

- **Figma file:** `Teletronics SUI`, key `F8J2cgGBsmyFLyw9OW6Njq`
- **Library key:** `lk-aa0ef88728038c9ae27427ca27125d4040269e8343ea19cae768b802c7fc9ecf88220850c53b2a7ea40759c96276770ecedda46f53ed26f2ec07071bab202408`
- **Variable collections:** `palette`, `spacing`, `shape` (keys in `figma/source.json`)
- **Component tiers:** `ATOMS` -> `MOLECULES` -> `ORGANISMS` (all keys in `figma/components/index.json`)

## Language and Direction

- All application screens must be **RTL**.
- Use **English** labels as working copy unless Arabic copy is provided; the team does not know Arabic.
- Design for future Arabic translation: preserve label width and layout flexibility.
- Fonts: `Noto Kufi Arabic` for body, label, button, and caption; `Alexandria` for headings h1-h6.

## Editing Text Inside Library Component Instances

When changing any text in a placed library component instance, always walk the **instance tree** to reach the TEXT node and set `.characters` directly, the same as a designer double-clicking and typing in Figma.

- Load all fonts used by the target text nodes via `figma.loadFontAsync` before writing.
- Use a recursive tree-walk on the instance to find the TEXT node, then set `.characters`.
- Do **not** use `setProperties` for text content. While it updates the property value, it does not reliably render in Figma. Direct `.characters` assignment on the TEXT node is the correct approach.
- Never edit the main component to change instance text, and never create a new component just to change a text value.

## Figma Safety Rules

- Treat the Teletronics SUI design system file as **read-only**.
- Never create, edit, detach, rename, move, or delete nodes inside the design system file unless the user explicitly asks to maintain the design system.
- Insert library components using `componentKey` values from `figma/components/index.json`.
- Bind fills and strokes to published variables by `variableKey`; never apply raw hex/RGB unless a required token is genuinely missing, and call out the gap.
- Apply elevation by importing effect styles by `styleKey`, not by manually creating shadows.

## SUI-Only Drawing Rule

**Never draw, create, or compose any element from scratch if a published Teletronics SUI component exists for it.**

- Before placing anything in Figma, check `figma/components/index.json` to confirm whether a SUI component covers the need.
- If no matching SUI component exists, stop and ask the user for permission before proceeding with a custom or primitive approach. Describe exactly what is missing and why, so the user can decide.
- This applies to every element: frames used as islands are acceptable, but anything that resembles a UI component (buttons, inputs, chips, cards, list rows, bars, panels, etc.) must come from the SUI library or be explicitly approved by the user first.
- Never silently fall back to hand-built primitives.

## Surface and Layout Defaults

- Every independent app frame starts from `background/surface_0` bound as a Figma variable.
- Island-to-island gap: always `spacing/1` (8px).
- Standard island radius: `cornerRadius/2` (8px).
- Use `background/surface_2` for task, list, and filter islands; `background/surface_3` for cards, panels, and menus.
- A separated functional unit is called an **island**; screens use dense bento-style island composition.

## Drawing Modal Windows

When any screen or flow requires showing a dialog or modal, always follow this exact sequence.

### 1. Create the modal state frame

Duplicate the target screen frame. The copy becomes the modal state frame. Name it `[original name] - Modal`. Never edit the original frame in place.

### 2. Layer backdrop and dialog

On top of the duplicated frame's contents:

1. Add the `Backdrop` SUI component. It must cover the entire duplicated frame and stay stretched in all directions: set it to absolute overlay positioning in the root frame, position it at `x=0`, `y=0`, resize it to the frame `width x height`, and use stretch constraints for left, right, top, and bottom when available. Do not leave it as a normal auto-layout child or merely stuck to the top-left corner.
2. Add the `<Dialog>` SUI component on top of the backdrop, centered in the frame.

Both are library components; import by `componentKey` from `figma/components/index.json`. `<Dialog>` is a component set; use `importComponentSetByKeyAsync` and take `defaultVariant`.

### 3. Fill dialog content via instance slot swap

`<Dialog>` is a component instance and must **never be detached**. To put content inside it:

1. Create a dedicated component on the page for the dialog's contents, for example `Modal Content / <descriptive name>`. This is the modal innards component. Design everything inside it using SUI components.
2. Swap the instance slot: navigate to the `_Library / Instance Slot` node inside `<DialogContent>`, nested inside the `<Dialog>` instance, and call `swapComponent(formComp)` on it. Do not edit any node inside the `<Dialog>` instance directly.

The `<Dialog>` already provides `<DialogTitle>`, `<DialogContent>` with the swappable slot, and `<DialogActions>` with buttons. Only the content inside the slot needs to be designed.

## Active Apps and Flows

| App | Knowledge files |
| --- | --- |
| Task Management | `app/apps/task-management.md`, `.json`, `app/screens/task-management/default.md`, `app/screens/task-management/canonical-layout.md` |
| Documents | `app/apps/document.md`, `.json`, `app/screens/document/canonical-layout.md` |
| User Preferences | `app/apps/user-preferences.md`, `.json`, `app/screens/user-preferences/*.md` |

| Flow | Knowledge files |
| --- | --- |
| Type Icon Appearance Preference | `app/flows/type-icon-appearance-preference.md`, `.json` |

Resolve app names and aliases via `app/figma-map.json` before reading app-specific files.

## MCP Servers

Example MCP server wiring lives in `mcps/mcp.json`. Merge it into the editor or agent MCP settings as needed.

- **teletronics-mcp** - s-system knowledge base (`search_knowledge`, `search_glossary`, `get_feature_file`; all require approval)
- **atlassian-jira** - Jira issue and workflow access from agents; current local endpoint is `http://localhost:4040/mcp`

## Help

| Topic | Description |
| ----- | ----------- |
| [Jira MCP environment setup](docs/jira-mcp-env-setup.md) | Set `JIRA_URL`, `JIRA_USERNAME`, and `JIRA_API_TOKEN` on Windows and macOS; supports `.env` or system environment; includes notes on running the MCP locally. |
