# Task Management: Icon Appearance Result

Use this screen state as the primary concrete result example for the type icon appearance preference flow.

## State

Start from the canonical Task Management screen and focus on the `<Task list>` / `<TaskItem>` cards. The task type/subtype icon in each card follows the system-wide icon appearance preference when that icon supports theming.

## Colorful Mode

- `Colorful` is the default.
- Task type/subtype icons use configured icon palette colors.
- Use variables from `components/icon/task_types/*` where applicable.

## Monochrome Mode

- Task type/subtype icons use neutral monochrome styling.
- Preserve icon shape, size, placement, and task-card metadata layout.
- Do not remove other card indicators such as urgent, frozen, attachments, related tasks, work status, or flow status.

## Drawing Rule

When drawing the full preference flow, include a Task Management result frame after the Appearance selection. Show either:

- one result frame with `Colorful` and `Monochrome` examples side by side, or
- two adjacent result frames if the requested output needs before/after comparison.

Do not edit the canonical Task Management component. Create an instance, duplicate, or new mockup frame.

## Related Flow

- `app/flows/type-icon-appearance-preference.md`
