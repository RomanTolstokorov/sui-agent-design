# User Preferences App Knowledge

Use this file before drawing or modifying User Preferences screens. User Preferences is not a standalone app shell; it is opened from any S-System app through the sidebar avatar menu.

## Canonical References

- Figma file: `User-profile-settings`
- File key: `kRLV8EyWZ1uhBtPwLDaGp4`
- Avatar/profile menu node: `62:11471`
- Preferences dialog content node: `5:29244`
- Preferences tabs base component node: `12:9611`
- Avatar menu URL: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=62-11471`
- Preferences dialog content URL: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=5-29244`
- Preferences tabs base URL: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=12-9611`

## Entry Point

User Preferences opens from the user avatar at the bottom/actions area of the SUI `<Sidebar>`. The avatar is available from any app that uses the standard application shell.

Default interaction:

1. User presses the sidebar avatar.
2. User profile menu opens.
3. User clicks `Preferences`.
4. Preferences opens as a modal dialog over the current app.

## Product Purpose

User Preferences contains personal settings that affect the current user's S-System experience across apps. It is not a standalone app shell; it is a modal settings surface opened from the sidebar avatar.

Use User Preferences for personal display, appearance, profile, and experience choices. Do not place app-specific filters or task/document actions here.

## Dialog Composition

Use published SUI overlay components for the modal state:

- `Backdrop`, node `6643:52207`, component key `4271be8c7d2699b8ec5a8a5b30feb3d5eab219e7`
- `<Dialog>`, node `6586:47183`, component key `fccf45793ec542d2e3b09e635d23466412e7f095`

Place the User Profile Settings dialog content inside the dialog. Do not rebuild the base modal behavior from primitives when the SUI components can be used.

## Preferences Tabs

Use the base preferences tabs component/reference node `12:9611` for dialog tab structure. The `Appearance` tab is the relevant tab for icon appearance settings.

When drawing the icon appearance flow:

- Set `Appearance` as active.
- Show a section for icon appearance.
- Use `<RadioGroup>` with `<FormControlLabel> | Radio` options.
- Use `Colorful` and `Monochrome` as the option labels.
- `Colorful` is selected by default unless the requested state says otherwise.
- Show a preview of the icon rendering result.

The type icon appearance flow belongs to User Preferences. Task Management may be used as the downstream result example because task type/subtype icons are the clearest affected UI element.

## Common UX States

- **Avatar menu open:** current app remains visible behind the profile menu.
- **Preferences modal open:** current app remains visible under the backdrop.
- **Appearance active:** Appearance tab is active and shows display-related settings.
- **Unsaved or changed setting:** show the changed control state clearly; use dialog actions when the interaction requires explicit confirmation.
- **Preview:** show how the selected preference affects UI elements when a setting changes visual appearance.

## Related Flows

- `app/flows/type-icon-appearance-preference.md`: User Preferences flow for configuring system-wide icon appearance. Task Management is only the downstream result example.

## Drawing Rules

- Keep the current app visible behind the modal backdrop.
- Preserve RTL application composition.
- Use English labels as working copy unless Arabic copy is provided.
- Use published SUI components by component key.
- Treat the Teletronics SUI design system file as read-only.
