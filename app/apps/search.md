# Search App Knowledge

Use this file before drawing or modifying Search screens. Search is a core S-System app for finding documents, records, images, events, and related evidence across configured data sources.

## Canonical Reference

- **Figma file:** `Search`
- **File key:** `YFsunyZ8IDCjPBOJbVu6zO`
- **Canonical node:** `2882:27314` — `Search - Cannonocal`, 1920 x 1080 px
- **Canonical URL:** `https://www.figma.com/design/YFsunyZ8IDCjPBOJbVu6zO/Search?node-id=2882-27314`
- **Canonical layout preset:** `app/screens/search/canonical-layout.md`
- Treat this component as the default Search reference. Create a duplicate or new frame; do not edit the canonical component unless explicitly requested.

## Product Purpose

Search helps users find and review official information quickly. It combines query entry, search type selection, filters, saved searches, results, and a preview/detail panel in one dense workspace.

Records are the main things users can find in Search. A record can be linked or attached to a task. A record can also be linked to an entity; entities are special text items used in documents. This relationship is intentionally high level for now and should be refined when more domain details are provided.

Common search work:

- Start a quick, advanced, or image search.
- Choose data sources and search modes.
- Filter and sort results.
- Save or reopen searches.
- Select a result and review its preview/detail.
- Request access for blocked results when the screen state calls for it.

## Direction and Copy

- Build all Search screens RTL.
- Use English labels as working copy unless Arabic copy is provided.
- Preserve enough width and flexible text behavior for future Arabic labels.
- The canonical component may include Arabic labels/content; keep that behavior when it reflects the source screen.

## Canonical Layout

The canonical component is `1920 x 1080`. It follows the shared app shell with 8px outer padding.

- Right edge: `<Sidebar>` navigation rail, `64 x 1064`.
- Main application area: `1832 x 1064`, positioned to the left of the sidebar.
- Top: `<Application top-bar>` Search variant, `1832 x 64`.
- Search query island: `1832 x 64`, placed 8px below the top bar.
- Working area: `1832 x 920`, placed 8px below the query island.
- Working area split:
  - Preview/detail island on the left, `1046 x 920`.
  - Results and filters group on the right, `778 x 920`.
- Results and filters group:
  - Document/result list on the left of the group, `420 x 920`.
  - Filters panel on the right of the group, `350 x 920`.

Although the screen is RTL, the canonical Search workspace reads from right to left as filters, then results, then preview/detail.

## Main Regions

### Top Bar

Use the Search variant of `<Application top-bar>` as the starting point.

Observed canonical content:

- Search application title.
- Tabs for Search modes or top-level search sections.
- Action group for creating/opening, history, and saved-search actions.

Do not rebuild the top bar from primitives. Use it for global Search scope, search mode navigation, history, saved search entry points, and app-level actions.

### Search Query Island

The query island is the primary place for entering and shaping the current search.

Observed canonical structure:

- Search type controls.
- Keyword input.
- Optional column/view controls.
- Query clear/close affordance.
- Quick search controls grouped near the input.

Use this island for query text, search mode controls, and immediate query actions. Do not place persistent result filters here unless the feature is specifically about query construction.

### Results and Filters

The right-side group combines result discovery and filtering.

Use the result list for returned records, documents, or events. Each row should include enough signal for scanning:

- title or subject
- identifier
- date
- source/type
- selected state when it drives the preview
- blocked/no-access treatment when content is restricted

Use the filters panel for persistent search filters, data source refinements, and saved-search related filtering. Keep controls close to the result list they affect.

### Preview or Detail Area

The left island shows the selected result preview/detail. If no result is selected, show a concise instruction or empty state. If a result is selected, reflect the selected row with document/record details, metadata, and relevant actions.

## UX States

- **No query yet:** show the query island ready for input and an instructional preview/empty results state.
- **Loading:** keep the shell stable and show loading in the results/list region.
- **No results:** show an empty result state in the list area; keep filters visible for refinement.
- **Selected result:** show selected row state and matching preview/detail content.
- **Blocked/no access result:** show restricted row/detail state and a request access action when the flow asks for it.
- **Saved search:** show the saved-search name/state near the query or filters and keep edit/update actions close to saved-search controls.

## Feature Placement Rules

- Put query text and immediate query mode controls in the Search Query Island.
- Put persistent filters in the filters panel.
- Put result display toggles, sorting, and column/view controls near the list or query controls, matching the canonical pattern.
- Put selected-result content in the preview/detail island; do not duplicate full details inside list rows.
- Keep the canonical panel widths unless a requested feature clearly needs a new layout.
- Use published SUI components by `componentKey` from `figma/components/index.json`; if a Search-specific component is not indexed locally, inspect the canonical Search file before drawing and call out the gap.

## Common Feature Workflow

When the user asks for a Search feature:

1. Read `app/rules.md`, `app/rules.json`, this file, and `app/apps/search.json`.
2. Use `app/screens/search/canonical-layout.md` for frame structure.
3. Read local SUI component and foundation indexes before searching Figma.
4. Inspect the canonical Search node only when the preset does not provide enough content detail.
5. Create a duplicate or new mockup/version outside the canonical component unless instructed otherwise.

## Open Product Questions

- Exact tab labels and which Search mode should be active by default.
- Exact row component mapping for non-document result types.
- Which filters are always visible versus hidden behind additional controls.
- Detailed copy for no-results, blocked-result, and request-access states.
- Responsive behavior below the canonical `1920 x 1080` component.
