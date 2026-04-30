---
type: flow
id: type-icon-appearance-preference
jira: AIQSS-15797
source: jira, figma, teletronics-mcp
primary_apps: user-preferences
result_example_apps: task-management
updated: 2026-04-30
---
# Type Icon Appearance Preference Flow

Use this file when a user asks to draw, update, explain, or recreate the icon appearance preference flow. This is a **User Preferences** flow: the preference is opened from any app through the sidebar avatar menu, configured in User Preferences, and applied system-wide to themed icons. Task Management type/subtype icons are the primary concrete result example, but the flow itself belongs to User Preferences.

## Source Priority

1. Jira `AIQSS-15797` is the upstream requirement source.
2. Figma references are the visual source for menu, dialog, tabs, supported icons, and component structure.
3. teletronics-mcp provides product/domain context.
4. Local `app/` and `figma/` files are the reproducible drawing cache for agents.

## Requirement Summary

Users can choose whether supported UI icons render in `Colorful` or `Monochrome` style.

- Default for new users and users without a saved value: `Colorful`.
- The preference is saved per account and survives sign-out/sign-in and session refresh.
- The setting applies system-wide to standard UI icons that support theming.
- Changing unrelated preferences such as theme or language must not reset icon appearance.
- Icons must remain distinguishable and usable in both modes.
- Use `Colorful` as the canonical label. Treat shorthand `color` as `Colorful`.

## Figma References

- User profile/avatar menu: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=62-11471`
- Preferences dialog content: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=5-29244`
- Preferences tabs base component: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=12-9611`
- SUI `<Dialog>`: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=6586-47183`
- SUI `Backdrop`: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=6643-52207`
- SUI `<RadioGroup>`: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=6558-39344`
- SUI `<FormControlLabel> | Radio`: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=634-100262`
- Supported type/subtype icons: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=18034-218248`

## User Flow

1. User is in any S-System app that uses the SUI sidebar.
2. User presses the avatar at the bottom of the sidebar.
3. User profile menu opens as the authored popup dialog from `User-profile-settings`.
4. User clicks `Preferences`.
5. A modal opens over the current app using SUI `Backdrop` and the copied canonical Preferences dialog from `User-profile-settings`, opened on the `Document` tab by default.
6. User opens the `Appearance` tab in the Preferences dialog.
7. User selects one of the icon appearance radio options:
   - `Colorful`
   - `Monochrome`
8. The preview updates to show how supported icons will render.
9. The selected appearance applies system-wide. Task Management task type/subtype icons can be shown as the downstream result example.

## Drawing Rule

When asked to draw or update this flow, prioritize the User Preferences journey. Create full preference-flow frames, not a single dialog:

- Any app screen with SUI sidebar and avatar visible.
- Avatar menu opened from the sidebar avatar.
- Preferences item selected.
- Preferences dialog opened over the current app with SUI Backdrop and the canonical copied Preferences dialog on the `Document` tab.
- Appearance tab active in the next state.
- Icon appearance section with `Colorful` selected by default and `Monochrome` as the alternate choice.
- Preview showing colorful versus monochrome icon rendering.
- Optional result frame showing system-wide icon impact, with Task Management type/subtype icons as the primary concrete example.

Use RTL composition for all application frames. Use English working copy unless Arabic copy is provided.

## Canonical User Preferences Drawing Sequence

When drawing this flow in a file outside `User-profile-settings`, do not rebuild the popup or Preferences dialog from lower-level primitives.

1. Start from an app frame with the SUI sidebar visible. The avatar at the bottom of the sidebar is the entry point.
2. For the avatar menu state, copy the authored popup/dialog from `User-profile-settings`:
   - Opened state frame: `62:11465`
   - Popup dialog node: `62:11471`
   - Placement in a `1920x1080` app frame: `x=1531`, `y=768`, size `301x304`
   - The copied popup already contains the user menu options: `Account`, `Theme`, `Preferences`, `Documentation`, and `Sign out`
   - Do not draw or rebuild those options separately; copy the whole popup and place it next to the bottom sidebar avatar
3. For the Preferences modal state, copy the canonical dialog from `User-profile-settings`:
   - Dialog node: `5:29244`
   - Inner component set reference: `12:9611`
   - Placement in a `1920x1080` app frame: `x=448`, `y=183.5`, size `1024x648`
   - Default opened tab: `Document`
4. Add SUI `Backdrop` behind the copied dialog at `x=0`, `y=0`, size `1920x1080`.
5. For the later icon appearance state, change the nested `<DialogInners> Preferences` instance properties on the copied dialog to `Tab=Appearance` and `Linked Entities=Yes`.

If the canonical popup or Preferences dialog has not been copied into the target file and its inner components cannot be imported, stop and ask for a copy. Do not approximate the dialog from `<Dialog>`, `<Menu>`, `<MenuItem>`, or primitive frames.

## Related Local Files

- `app/apps/user-preferences.md`
- `app/apps/task-management.md`
- `app/screens/user-preferences/avatar-menu.md`
- `app/screens/user-preferences/preferences-dialog.md`
- `app/screens/user-preferences/appearance-icon-mode.md`
- `app/screens/task-management/icon-appearance-result.md`
- `figma/components/index.json`
- `figma/foundations/colors.json`
