# User Preferences: Avatar Menu

Use this screen state when drawing the first interaction in the type icon appearance preference flow.

## Starting Context

Start from any S-System app screen that uses the SUI `<Sidebar>`. Task Management is a good concrete example when the flow needs to show the affected task type/subtype icons later.

## State

- Sidebar avatar is pressed/open.
- User profile menu is visible near the sidebar avatar as the authored popup dialog.
- `Preferences` menu item is visible and selectable.
- The current app remains visible behind the menu.

## Figma Reference

- File: `User-profile-settings`
- File key: `kRLV8EyWZ1uhBtPwLDaGp4`
- Opened state frame: `62:11465`
- Popup dialog node: `62:11471`
- Opened state URL: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=62-11465`
- Popup dialog URL: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=62-11471`

## Drawing Notes

- Do not treat User Preferences as a separate app shell.
- Preserve the sidebar/avatar relationship.
- Use English working copy unless Arabic copy is provided.
- The avatar popup is an authored `<Dialog>` instance, not a menu rebuilt from `<Menu>` or `<MenuItem>` primitives.
- To draw the state in another file, copy popup dialog node `62:11471` from `User-profile-settings` into the target file, then duplicate or clone that copied instance into the target app frame.
- Place the copied popup in the same relationship as opened-state frame `62:11465`: in a `1920x1080` app frame, near the bottom-right sidebar avatar at `x=1531`, `y=768`, size `301x304`.
- The copied popup already includes the menu options: `Account`, `Theme`, `Preferences`, `Documentation`, and `Sign out`. Do not recreate these options as separate menu items.
- If copying is unavailable, stop and ask for the popup to be copied or made available; do not approximate the popup from primitives.
