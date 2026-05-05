# Task Management App Knowledge

Use this file before drawing or modifying Task Management screens.

## Canonical Reference

- Figma file: `Task-Managment`
- File key: `OdNWALBR45nVe63thAAlEG`
- Canonical component node: `3915:129350` (`TaskManagment - Cannonical`)
- URL: `https://www.figma.com/design/OdNWALBR45nVe63thAAlEG/Task-Managment?node-id=3915-129350`
- Do not edit the canonical component — create an instance, duplicate, or new mockup frame.

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

## Canonical Layout

For exact frame construction, sizing behavior, token bindings, and component keys, use `app/screens/task-management/canonical-layout.md`.

At a product level, the default work queue reads from right to left (RTL): filters → task list → preview/detail.

## Main Regions

### Top Bar

Use `<Application top-bar>` with the Tasks application variant.

| Property | Value |
|----------|-------|
| componentKey (set) | `b6cde7cd669a24472f9645c0a38e57bab7d872e2` |
| Variant | `Application=Tasks` |
| Title | Tasks |
| Tabs | All, Created by me, Incoming |
| Active tab | Incoming (badge `34/357`) |
| Primary action | New task |
| View controls | columns/view mode toggle |
| Sort control | Sort by |

Do not rebuild the top bar from primitives. Only add controls when the feature belongs in global task navigation or global list control.

### Filters Panel

Use `<AppFilters>` as the default filter panel.

| Property | Value |
|----------|-------|
| componentKey (set) | `14eef66e973bc051e32f312ba45c31dec42e145e` |
| Default variant | `State=Filled in, Tab=Search` |
| Width | 320 px |
| Node ID | `2027:6819` |

Observed canonical filters:

| Filter | Control | Row pattern |
|--------|---------|-------------|
| Type | MultiSelect | AppFilterInput |
| Work status | MultiSelect | AppFilterInput |
| Color | MultiSelect | AppFilterInput |
| Flow status | MultiSelect | AppFilterInput |
| Creation Date | TextField | AppFilterInput |
| Country | Select | LinkedAppFilterInput parent |
| Sub-county | MultiSelect (disabled) | LinkedAppFilterInput child |
| Updated Date | MultiSelect | AppFilterInput |
| My groups | MultiSelect | AppFilterInput |

New filter default placement: inside `<AppFilters>` content, after Work status and before Color unless product guidance says otherwise. Preserve 16px vertical gap between filter rows.

### Task List

Use `<Task list>` as the default work queue list.

| Property | Value |
|----------|-------|
| componentKey | `59bdb48db0698778ebbdb04f0e4af7110dc0811a` |
| Width | 420 px |
| Node ID | `2614:64165` |

Each `<TaskItem>` row (`afadefcb4745e07f0074b3bc52db1b9b3b6ddef7`) is approximately 396 × 154 px with 16px vertical gap between cards.

Observed row fields: task ID, task type/subtype icon, work status indicator, attachment indicator, related/subtask count, urgent indicator, subject, secondary/EJS text, submission date, flow status, assignee avatar, from avatar.

Use the selected `<TaskItem>` state when the adjacent preview/detail area reflects that task. Include enough signal to make the queue scannable — ID, subject, type icon, status, date, avatars, and indicators.

Pagination is fixed to the bottom at 420 × 48 px.

#### Task Type/Subtype Icon Appearance

- `Colorful` mode: use palette colors from `components/icon/task_types/*`.
- `Monochrome` mode: neutral monochrome styling, preserve icon size and placement.
- Icon appearance is configured in User Preferences / Appearance, not via the Color filter.

For the full cross-app flow, read `app/flows/type-icon-appearance-preference.md`.

### Preview / Detail Area

| Property | Value |
|----------|-------|
| Width | 1076 px |
| Node ID | `2027:6789` |

Observed structure: actions bar, subject form block, inline text fields and chips, attachments, documents, author comment.

Avoid changing this area for filter-only work. If no task is selected, show a compact empty/instructional state rather than leaving the panel blank.

## Targeted Node IDs

Use these when a script needs to inspect or modify a specific region without touching the full canonical component.

| Region | Node ID |
|--------|---------|
| Top bar | `2027:6821` |
| Working area | `2027:6788` |
| Preview/detail | `2027:6789` |
| Task list + filters group | `2027:6817` |
| Task list | `2614:64165` |
| Filters | `2027:6819` |
| Sidebar | `2027:6786` |

## Common UX States

| State | Rule |
|-------|------|
| Selected task | One row selected; preview/detail reflects that task |
| Empty queue / no results | Keep filters visible; show clear empty state in list area |
| Loading | Keep shell stable; show loading inside list or preview region |
| Draft task | Show editable state and save/continue actions |
| Action required | Make primary next action visible near task detail or action bar |
| Validation/error | Show issue next to the task section or action that needs correction |

## Feature Placement Rules

- Add persistent filters inside `<AppFilters>` first.
- Add top-bar controls only for global scope, view mode, sorting, tabs, or creation actions.
- Add task row metadata only when the feature changes how individual tasks are represented.
- Keep filter controls close to the task list they affect.
- Preserve `spacing/1` (8 px) gap between the preview, list, and filter islands.
- Preserve canonical panel widths unless the feature cannot fit.
- Use `background/surface_0` for new screen bases, `background/surface_2` for task/list/filter islands, `background/surface_3` for cards/fields.
- Keep task actions close to the selected task context.

## Common Feature Workflow

1. Read `app/rules.md`, this file, and `app/screens/task-management/canonical-layout.md`.
2. Inspect the canonical component node `3915:129350` only when local docs don't provide enough content detail.
3. For targeted changes, use the node IDs in "Targeted Node IDs" above.
4. Create an instance, duplicate, or new mockup frame — do not modify the canonical component.
5. Use published SUI components by `componentKey`; never rebuild from primitives.
6. Bind fills, strokes, spacing, and radius to published variables by `variableKey`.

## Related Flows

- `app/flows/type-icon-appearance-preference.md` — User Preferences owns the icon appearance setting; Task Management is the downstream result example.

## Open Product Questions

- Which filters are mandatory versus optional under `More`.
- Whether active filters should appear as chips, inside the panel, above the list, or both.
- Exact empty, loading, error, and no-results states.
- Exact behavior of Saved Searches.
- Whether `Priority` and `Urgent` are separate product concepts.
- Responsive behavior below 1920 × 1080.
