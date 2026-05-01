# Task Management App Knowledge

Use this file before drawing or modifying Task Management screens. It describes the product-level screen structure and the canonical Figma component reference. Use `app/apps/task-management.json` for machine-readable node IDs and component mappings.

## Canonical Reference

- Figma file: `Task-Managment`
- File key: `OdNWALBR45nVe63thAAlEG`
- Canonical component node: `3915:129350`
- Canonical component name in Figma: `TaskManagment - Cannonical`
- Canonical URL: `https://www.figma.com/design/OdNWALBR45nVe63thAAlEG/Task-Managment?node-id=3915-129350`
- Treat this component as the default Task Management reference for application mockups.
- Do not edit the canonical component unless the user explicitly asks to update it. Prefer creating an instance, duplicating it, or creating a new variant/mockup next to it.

## Product Purpose

Task Management is a dense work queue for reviewing, filtering, opening, and processing tasks. The default screen combines a selected task preview/detail area with a task list and a filter panel.

Tasks are the main actionable work units in S-System. Users use this app to find incoming work, inspect the task context, edit task data, create new tasks or drafts, and take available task actions.

Common task work:

- Review an incoming task from the list.
- Filter or search the queue to find the right task.
- Open a selected task and review its preview/detail content.
- Create a new task or continue editing a task draft.
- Update task sections such as linked records, documents, attachments, comments, or extra fields.
- Use visible action buttons to move the task forward when the screen state calls for it.

## Direction and Copy

- Build all Task Management screens RTL.
- Use English labels as working copy unless Arabic copy is provided.
- Preserve enough width and flexible text behavior for future Arabic labels.
- The canonical component currently mixes English control labels with Arabic task content. This is acceptable working-copy behavior.

## Canonical Layout

For exact frame construction, sizing behavior, token bindings, and component keys, use `app/screens/task-management/canonical-layout.md`. Use `app/apps/task-management.json` only when a script needs machine-readable node IDs, component keys, or layout values.

At a product level, the default work queue combines a right-side filter panel, a task list beside it, and a selected task preview/detail area on the left. Although the screen is RTL, the canonical work queue reads from right to left as filters, then task list, then preview/detail.

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
  - Saved searches tab displayed in Arabic in the canonical component
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

When drawing list rows, include enough business signal to make the queue scannable: task ID, subject, type/subtype icon, status, date, assignee/from avatars, attachments, urgency/freeze indicators when relevant, and selected state when the preview is tied to that row.

#### Task Type/Subtype Icon Appearance

The task type/subtype icon follows the system-wide icon appearance preference when the icon supports theming.

- `Colorful` mode uses configured icon palette colors from `components/icon/task_types/*`.
- `Monochrome` mode uses neutral monochrome styling.
- Preserve icon size, placement, and row metadata in both modes.
- Do not use the `Color` filter as the icon appearance control; icon appearance is configured in User Preferences / Appearance.

For the full cross-app flow, read `app/flows/type-icon-appearance-preference.md`.

### Preview or Detail Area

The canonical left area is a selected task preview/detail island.

Observed structure:

- `Draft Preview Scrollable: Full screen`
- Actions bar at top
- Main form content below
- Subject block
- Inline text fields and chips
- Attachment block
- Documents block
- Author comment block

When a requested feature only affects filtering or list discovery, avoid changing this preview area except to keep the selected task state coherent.

Use this area for the selected task's work context: subject, fields, attachments, related documents, comments, and action surfaces. If no task is selected, show a compact empty/instructional state rather than leaving the panel blank.

## Common UX States

- **Selected task:** one task row is selected and the preview/detail island reflects that task.
- **Empty queue / no results:** keep filters visible and show a clear empty state in the list area.
- **Loading:** keep the shell stable and show loading inside the list or preview region.
- **Draft task:** show editable state and save/continue actions.
- **Action required:** make the primary next action visible near the task detail or action bar.
- **Validation/error:** show the issue next to the task section or action that needs correction.

## Feature Placement Rules

- Add persistent filters inside `<AppFilters>` first.
- Add active/applied filter chips near the task list or inside the filter panel only when the request explicitly asks for applied-state visibility.
- Add top-bar controls only for global list scope, view mode, sorting, tab selection, or creation actions.
- Add task row metadata only when the feature changes how individual tasks are represented.
- Keep filter controls close to the task list they affect.
- Preserve the canonical `spacing/1` gap between the preview, list, and filter islands.
- Preserve the canonical panel widths unless the requested feature cannot fit in the existing pattern.
- Use `background/surface_0` for any new independent frame/screen base, `background/surface_2` for task/list/filter islands, and `background/surface_3` for cards/fields.
- Keep task actions close to the selected task context; do not put task-specific actions in global navigation unless the feature is explicitly global.

## Related Flows

- `app/flows/type-icon-appearance-preference.md`: User Preferences owns the icon appearance setting. Task Management is the downstream result example for task type/subtype icons.

## Common Feature Workflow

When the user asks for a Task Management feature:

1. Read `app/rules.md`, `app/rules.json`, this file, and `app/apps/task-management.json`.
2. Use `app/screens/task-management/canonical-layout.md` for exact frame structure.
3. Read the local SUI component and foundation indexes before searching Figma.
4. Inspect the canonical component node `3915:129350` in file `OdNWALBR45nVe63thAAlEG` only when local docs do not provide enough content detail.
5. If the change affects filters, inspect node `2027:6819`.
6. If the change affects list rows, inspect node `2614:64165`.
7. If the change affects global controls, inspect node `2027:6821`.
8. Create an instance, duplicate, or create a new mockup/version outside the canonical component unless instructed otherwise.
9. Use published SUI components by `componentKey`; do not rebuild design-system components from primitives.
10. Bind fills, strokes, spacing, and radius to published variables by `variableKey` where possible.
11. Call out any missing product rule or token gap instead of silently inventing a new pattern.

## Example: Adding a New Filter

For a request like `Add a Priority filter in Task Management`:

- Start from the canonical component `3915:129350`.
- Place the new filter in `<AppFilters>` content, not the top bar.
- Match the existing `<AppFilterInput>` row pattern.
- Use `<MultiSelect>` if Priority can have multiple values; use `<Select>` if it is single-choice.
- Insert it near similar task metadata filters. A reasonable default is after `Work status` and before `Color`, unless product guidance says otherwise.
- Keep the row height, 4px internal input/control gap, 16px vertical filter-stack gap, and RTL alignment.
- Optionally show applied state with a `<Chip>` only if requested.

## Open Product Questions

These are not fully defined by the current canonical component:

- Which filters are mandatory versus optional under `More`.
- Whether active filters should appear as chips, inside the panel, above the list, or both.
- Exact empty, loading, error, and no-results states.
- Exact behavior of Saved Searches.
- Whether `Priority` and `Urgent` are separate product concepts or one concept.
- Responsive behavior below the canonical `1920 x 1080` component.
