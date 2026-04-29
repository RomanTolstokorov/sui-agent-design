# User Preferences: Appearance Icon Mode

Use this screen state for the active Appearance tab in the icon appearance preference flow.

## State

- Preferences dialog is open.
- `Appearance` tab is active.
- Icon appearance section is visible.
- Radio options:
  - `Colorful`, selected by default.
  - `Monochrome`.
- Preview area shows how supported icons render in the selected mode.

## Figma References

- Preferences tabs base: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=12-9611`
- Preferences dialog content: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=5-29244`
- SUI `<RadioGroup>`: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=6558-39344`
- SUI `<FormControlLabel> | Radio`: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=634-100262`
- Supported type/subtype icons: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=18034-218248`

## Component Requirements

- Use `<RadioGroup>`, component key `ddc023ebe5609db2db3e401039902eaa782369cc`.
- Use `<FormControlLabel> | Radio`, component key `e722314e98724d857b604322368a624ab5a963d0`.
- Use task type icon palette variables from `components/icon/task_types/*` for colorful preview.
- Use neutral monochrome styling for monochrome preview.

## Behavior Notes

- The preference applies system-wide to icons that support theming.
- Changing theme, language, or other preferences must not reset this value.
- Icons must remain distinguishable in both modes.
