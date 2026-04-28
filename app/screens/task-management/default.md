# Task Management Default Screen

Canonical Figma reference:

- File key: `OdNWALBR45nVe63thAAlEG`
- Node ID: `2027:6784`
- URL: `https://www.figma.com/design/OdNWALBR45nVe63thAAlEG/Task-Managment?node-id=2027-6784`

## Screen Anatomy

The default screen is a 1920 x 1080 RTL Task Management workspace.

| Region | Node | Size | Notes |
| --- | --- | --- | --- |
| Canonical frame | `2027:6784` | `1920 x 1080` | Named `Read only` |
| App shell | `3915:126156` | `1904 x 1064` | 8px inset from frame |
| Main app area | `3915:126153` | `1832 x 1064` | Top bar plus working area |
| Sidebar | `2027:6786` | `64 x 1064` | Right edge |
| Top bar | `2027:6821` | `1832 x 64` | Tasks title, tabs, actions |
| Working area | `2027:6788` | `1832 x 992` | Starts at y=72 |
| Preview/detail | `2027:6789` | `1076 x 992` | Selected task content |
| Task/list/filter group | `2027:6817` | `748 x 992` | 8px gap |
| Task list | `2614:64165` | `420 x 992` | Work queue |
| Filters | `2027:6819` | `320 x 992` | Search/filter panel |

## Default State

- Top-bar active task tab: `Incoming`
- Incoming badge: `34/357`
- Filter panel tab: `Search`
- Filters panel is expanded.
- Task list has a selected item.
- Preview/detail area shows the selected task.

## Use As Starting Point

When asked to create or change a Task Management screen, inspect or duplicate this screen first. For narrow feature work, change only the relevant region:

- Filters or search: start from `2027:6819`.
- Task list cards, row states, or pagination: start from `2614:64165`.
- Top-level task controls: start from `2027:6821`.
- Preview/detail form content: start from `2027:6789`.
