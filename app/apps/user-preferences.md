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

## Avatar Popup Composition

The avatar menu is an authored popup dialog in `User-profile-settings`; it is not assembled from menu primitives during routine flow drawing.

- Opened state frame: node `62:11465`, URL `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=62-11465`
- Popup dialog to copy: node `62:11471`, URL `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=62-11471`
- Placement in a `1920x1080` app frame: `x=1531`, `y=768`, size `301x304`

When drawing in another file, copy node `62:11471` into the target file, then duplicate or clone that copied instance into the app frame near the bottom-right sidebar avatar. The copied popup already contains the `Account`, `Theme`, `Preferences`, `Documentation`, and `Sign out` options. Do not recreate those options with `<Menu>`, `<MenuItem>`, list items, or primitives.

If the popup has not been copied into the target file and cannot be imported, stop and ask for it to be copied or made available.

## Product Purpose

User Preferences contains personal settings that affect the current user's S-System experience across apps. It is not a standalone app shell; it is a modal settings surface opened from the sidebar avatar.

Use User Preferences for personal display, appearance, profile, and experience choices. Do not place app-specific filters or task/document actions here.

## Dialog Composition

User Preferences modal states are based on the authored canonical Preferences dialog in the `User-profile-settings` file, not a fresh rebuild.

- Canonical Preferences dialog: node `5:29244`, URL `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=5-29244`
- Preferences inner component set: node `12:9611`, URL `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=12-9611`
- SUI `Backdrop`, node `6643:52207`, component key `4271be8c7d2699b8ec5a8a5b30feb3d5eab219e7`

When drawing in another file, first copy the whole canonical Preferences dialog instance from `User-profile-settings` into the target file. Then duplicate or clone that copied dialog for modal states and place it over a SUI `Backdrop`. The default opened Preferences modal uses `Tab=Document` and `Linked Entities=Yes`.

Do not recreate the Preferences dialog by importing SUI `<Dialog>` and trying to import or rebuild `<DialogInners> Preferences` in another file. The inner content is authored in `User-profile-settings`; copying the whole dialog preserves the reachable `<DialogInners> Preferences` instance and its component properties.

Use the copied dialog at `x=448`, `y=183.5`, size `1024x648` inside a `1920x1080` app frame. Place the `Backdrop` behind it at `x=0`, `y=0`, size `1920x1080`.

If the canonical dialog has not been copied into the target file and the inner component cannot be imported, stop and ask for the dialog to be copied or made available. Do not approximate the dialog from primitives.

## Preferences Tabs

Use the base preferences tabs component/reference node `12:9611` for dialog tab structure. The `Appearance` tab is the relevant tab for icon appearance settings.

When drawing the icon appearance flow:

- First show the Preferences modal opened on `Document`.
- In the next state, set the nested `<DialogInners> Preferences` instance property `Tab` to `Appearance`.
- Set `Linked Entities` according to the requested state; use `Yes` for the canonical icon-appearance preview state unless specified otherwise.
- Show a section for icon appearance.
- Use `<RadioGroup>` with `<FormControlLabel> | Radio` options.
- Use `Colorful` and `Monochrome` as the option labels.
- `Colorful` is selected by default unless the requested state says otherwise.
- Show a preview of the icon rendering result.

The type icon appearance flow belongs to User Preferences. Task Management may be used as the downstream result example because task type/subtype icons are the clearest affected UI element.

## Common UX States

- **Avatar menu open:** current app remains visible behind the profile menu.
- **Preferences modal open:** current app remains visible under the backdrop, with the copied canonical Preferences dialog centered at `1024x648`.
- **Appearance active:** Appearance tab is active and shows display-related settings.
- **Unsaved or changed setting:** show the changed control state clearly; use dialog actions when the interaction requires explicit confirmation.
- **Preview:** show how the selected preference affects UI elements when a setting changes visual appearance.

## Related Flows

- `app/flows/type-icon-appearance-preference.md`: User Preferences flow for configuring system-wide icon appearance. Task Management is only the downstream result example.

## Drawing Rules

- Open User Preferences from the bottom avatar in the app sidebar; do not draw it as a standalone app shell.
- Copy the authored avatar popup/dialog and canonical Preferences dialog from `User-profile-settings` when drawing in another file.
- Keep the current app visible behind the modal backdrop.
- Preserve RTL application composition.
- Use English labels as working copy unless Arabic copy is provided.
- Use published SUI components by component key.
- Treat the Teletronics SUI design system file as read-only.
