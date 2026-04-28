# Teletronics SUI Agent Instructions

## Project Context

- This project is Arabic-oriented and all application design must be RTL.
- The team does not know Arabic, so use English labels and text as working copy/placeholders unless Arabic copy is provided.
- This repository exists only as local context for code agents working with the Teletronics SUI Figma design library.

## Required Lookup Order

- Read `app/rules.md` and `app/rules.json` for application-specific composition rules.
- Read `app/figma-map.json` to resolve app names, aliases, canonical Figma references, and important app nodes.
- For product-specific app work, read `app/apps/<app-id>.md` and `app/apps/<app-id>.json` before drawing. For Task Management, read `app/apps/task-management.md`, `app/apps/task-management.json`, and `app/screens/task-management/default.md`.
- Read `figma/source.json` for Figma file, library, and node metadata.
- Use `figma/components/index.md` and `figma/components/index.json` before searching the Figma design system for components.
- Use `figma/foundations/typography.md` and `figma/foundations/typography.json` before querying Figma text styles.
- Use `figma/foundations/colors.md` and `figma/foundations/colors.json` before querying Figma color variables, surfaces, and elevations.
- Use `figma/foundations/layout.md` and `figma/foundations/layout.json` before querying Figma spacing, radius, or application layout variables.

## Figma Safety Rules

- Treat the Teletronics SUI design system file as read-only.
- Import and use published components, variables, and styles, but do not create, edit, detach, rename, move, or delete anything inside the design system file unless the user explicitly asks to maintain the design system.
- The components overview frame in Figma is organized into `ATOMS`, `MOLECULES`, and `ORGANISMS`.
- Use `componentKey` values from the local component index when inserting/searching library components.
- Bind Figma fills and strokes to published variables/tokens by `variableKey`; do not apply raw hex/RGB values except as a temporary fallback when a required token is missing.

## MCPs

Example MCP server wiring lives in [mcps/mcp.json](mcps/mcp.json). Merge it into the editor or agent MCP settings as needed.

- **teletronics-mcp** - MCP for the **s-system knowledge base**.
- **atlassian-jira** - Jira issue and workflow access from agents. 


## Help

| Topic | Description |
| ----- | ----------- |
| [Jira MCP environment setup](docs/jira-mcp-env-setup.md) | Set `JIRA_URL`, `JIRA_USERNAME`, and `JIRA_API_TOKEN` on Windows and macOS; supports `.env` or system environment; includes notes on running the MCP locally. |
