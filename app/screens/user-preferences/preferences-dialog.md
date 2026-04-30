# User Preferences: Preferences Dialog

Use this screen state after the user clicks `Preferences` in the avatar menu.

## State

- The current app remains visible in the background.
- SUI `Backdrop` is applied over the app.
- The canonical User Profile Settings `<Dialog>` is centered over the backdrop.
- User Profile Settings preferences content appears inside the dialog exactly as authored in the User-profile-settings file.

## Figma References

- Preferences dialog content: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=5-29244`
- Preferences dialog inner component set: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=12-9611`
- SUI `<Dialog>`: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=6586-47183`
- SUI `Backdrop`: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=6643-52207`

## Component Requirements

- Use `Backdrop`, component key `4271be8c7d2699b8ec5a8a5b30feb3d5eab219e7`.
- Treat `User-profile-settings` node `5:29244` as the canonical Preferences dialog.
- Copy the whole canonical dialog instance into the target file, then duplicate or clone that copied instance for modal states.
- Do not recreate the Preferences dialog by importing `<Dialog>` and rebuilding/swapping the inner content unless working in the original `User-profile-settings` file.
- The copied dialog exposes `<DialogInners> Preferences` inside `<DialogContent>`. The default opened modal state uses `Tab=Document` and `Linked Entities=Yes`.
- Change `<DialogInners> Preferences` properties only when drawing a later state, for example switching to `Tab=Appearance` for the icon appearance preference.
- Treat SUI as read-only: import instances; do not modify source components.

## Drawing Notes

- This is a modal overlay state, not a new page.
- Keep RTL composition and preserve room for Arabic labels.
- Place the copied Preferences dialog at `x=448`, `y=183.5`, size `1024x648` inside a `1920x1080` app frame.
- Add `Backdrop` behind the copied dialog at `x=0`, `y=0`, size `1920x1080`.
- If the canonical dialog or its inners cannot be copied into the target file, stop and ask for the component to be copied or made available. Do not silently rebuild the dialog from primitives.
- Future design-system maintenance may redraw or refactor the dialog in its original `User-profile-settings` file; until then, agents should copy the canonical dialog instance.
