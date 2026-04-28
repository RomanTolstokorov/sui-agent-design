# Task Management App Knowledge

Use this file before drawing or modifying Task Management screens. It describes the product-level screen structure and the canonical Figma reference. Use `app/apps/task-management.json` for machine-readable node IDs and component mappings.

## Canonical Reference

- Figma file: `Task-Managment`
- File key: `OdNWALBR45nVe63thAAlEG`
- Canonical screen node: `2027:6784`
- Canonical screen name in Figma: `Read only`
- Canonical URL: `https://www.figma.com/design/OdNWALBR45nVe63thAAlEG/Task-Managment?node-id=2027-6784`
- Treat this frame as the default Task Management reference for application mockups.
- Do not edit the canonical frame unless the user explicitly asks to update it. Prefer duplicating it or creating a new variant/mockup next to it.

## Product Purpose

Task Management is a dense work queue for reviewing, filtering, opening, and processing tasks. The default screen combines a selected task preview/detail area with a task list and a filter panel.

## Direction and Copy

- Build all Task Management screens RTL.
- Use English labels as working copy unless Arabic copy is provided.
- Preserve enough width and flexible text behavior for future Arabic labels.
- The canonical frame currently mixes English control labels with Arabic task content. This is acceptable working-copy behavior.

## Canonical Layout

The canonical frame is `1920 x 1080`. It contains an inner app shell with 8px outer padding.

- Right edge: `<Sidebar>` navigation rail, `64 x 1064`.
- Main application area: `1832 x 1064`, positioned to the left of the sidebar.
- Top: `<Application top-bar>`, `1832 x 64`.
- Below top bar: working area starts 8px below the top bar, `1832 x 992`.
- Working area is split into:
  - Main preview/detail island on the left, `1076 x 992`.
  - Task/list/filter group on the right, `748 x 992`.
- The task/list/filter group uses an 8px gap:
  - `<Task list>` on the left side of that group, `420 x 992`.
  - `<AppFilters>` on the right side of that group, `320 x 992`.

Although the screen is RTL, the canonical work queue reads from right to left as filters, then task list, then preview/detail.

## Main Regions

### Top Bar

Use `<Application top-bar>` with the Tasks application variant as the starting point.

Observed canonical content:

- Title: `Tasks`
- Tabs: `All`, `Created by me`, `Incoming`
- Active tab: `Incoming`, with badge value `34/357`
- Primary action: `New task`
- View controls: small toggle button group for columns/view mode
- Sort control: `Sort by`

Do not rebuild the top bar from primitives for routine Task Management work. Use the published top-bar component and only modify/add controls when the requested feature belongs in global task navigation or global list control.

### Filters Panel

Use `<AppFilters>` as the default filter panel. It is the primary place for adding persistent task filters.

Observed canonical structure:

- Panel width: `320`
- Surface: `background/surface_2`
- Radius: `cornerRadius/2`
- Header with collapse icon and tabs
- Tabs:
  - `Search` active
  - Saved searches tab displayed in Arabic in the canonical frame
- Search field below tabs
- Filter heading with `More` text button
- Filter content stack with 16px vertical gap

Observed canonical filters:

- `Type`
- `Work status`
- `Color`
- `Flow status`
- `Creation Date`
- `Country`
- `Sub-county`, disabled/dependent under Country
- `Updated Date`
- `My groups`

Most filter rows use an app-filter input pattern: a field on the left and a borderless medium `<ToggleButtonGroup>`/drag or condition control on the right. Preserve this row structure when adding new filters.

Use `<MultiSelect>` for categorical filters, `<TextField>` for date/text filters, and `<Select>` for single-choice parent filters when matching the canonical pattern. Use dependent linked filter layout for fields like Country/Sub-county.

### Task List

Use `<Task list>` as the default work queue list.

Observed canonical structure:

- Panel width: `420`
- Surface: `background/surface_2`
- Radius: `cornerRadius/2`
- List container uses 12px horizontal padding, 12px top padding, 8px bottom padding
- Task cards are stacked with 16px vertical gap
- Pagination is fixed to the bottom, `420 x 48`

Each `<TaskItem>` card is about `396 x 154` or `396 x 156`, with:

- ID and task type/subtype icon
- Work status indicator
- Optional attachment and related/subtask indicators
- Optional urgent icon
- Subject line
- Optional secondary/EJS text
- Submission date
- Flow status
- Assignee/from avatar pair

Use the selected task item state when the adjacent preview/detail area reflects that task.

### Preview or Detail Area

The canonical left area is a selected task preview/detail island.

Observed structure:

- `Draft Preview Scrollable: Full screen`, `1076 x 992`
- Actions bar at top, `1000 x 72`
- Main form content below, `1000` wide with inner `968` content width
- Subject block
- Inline text fields and chips
- Attachment block
- Documents block
- Author comment block

When a requested feature only affects filtering or list discovery, avoid changing this preview area except to keep the selected task state coherent.

## Feature Placement Rules

- Add persistent filters inside `<AppFilters>` first.
- Add active/applied filter chips near the task list or inside the filter panel only when the request explicitly asks for applied-state visibility.
- Add top-bar controls only for global list scope, view mode, sorting, tab selection, or creation actions.
- Add task row metadata only when the feature changes how individual tasks are represented.
- Keep filter controls close to the task list they affect.
- Preserve the `8px` gap between the preview, list, and filter islands.
- Preserve the canonical panel widths unless the requested feature cannot fit in the existing pattern.
- Use `background/surface_0` for any new independent frame/screen base, `background/surface_2` for task/list/filter islands, and `background/surface_3` for cards/fields.

## Common Feature Workflow

When the user asks for a Task Management feature:

1. Read `app/rules.md`, `app/rules.json`, this file, and `app/apps/task-management.json`.
2. Read the local SUI component and foundation indexes before searching Figma.
3. Inspect the canonical frame node `2027:6784` in file `OdNWALBR45nVe63thAAlEG`.
4. If the change affects filters, inspect node `2027:6819`.
5. If the change affects list rows, inspect node `2614:64165`.
6. If the change affects global controls, inspect node `2027:6821`.
7. Duplicate or create a new mockup/version outside the canonical frame unless instructed otherwise.
8. Use published SUI components by `componentKey`; do not rebuild design-system components from primitives.
9. Bind fills, strokes, spacing, and radius to published variables by `variableKey` where possible.
10. Call out any missing product rule or token gap instead of silently inventing a new pattern.

## Example: Adding a New Filter

For a request like `Add a Priority filter in Task Management`:

- Start from the canonical frame `2027:6784`.
- Place the new filter in `<AppFilters>` content, not the top bar.
- Match the existing `<AppFilterInput>` row pattern.
- Use `<MultiSelect>` if Priority can have multiple values; use `<Select>` if it is single-choice.
- Insert it near similar task metadata filters. A reasonable default is after `Work status` and before `Color`, unless product guidance says otherwise.
- Keep the row height, 4px internal input/control gap, 16px vertical filter-stack gap, and RTL alignment.
- Optionally show applied state with a `<Chip>` only if requested.

## Open Product Questions

These are not fully defined by the current canonical frame:

- Which filters are mandatory versus optional under `More`.
- Whether active filters should appear as chips, inside the panel, above the list, or both.
- Exact empty, loading, error, and no-results states.
- Exact behavior of Saved Searches.
- Whether `Priority` and `Urgent` are separate product concepts or one concept.
- Responsive behavior below the canonical `1920 x 1080` frame.
