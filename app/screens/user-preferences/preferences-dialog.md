# User Preferences: Preferences Dialog

Use this screen state after the user clicks `Preferences` in the avatar menu.

## State

- The current app remains visible in the background.
- SUI `Backdrop` is applied over the app.
- SUI `<Dialog>` is centered over the backdrop.
- User Profile Settings preferences content appears inside the dialog.

## Figma References

- Preferences dialog content: `https://www.figma.com/design/kRLV8EyWZ1uhBtPwLDaGp4/User-profile-settings?node-id=5-29244`
- SUI `<Dialog>`: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=6586-47183`
- SUI `Backdrop`: `https://www.figma.com/design/F8J2cgGBsmyFLyw9OW6Njq/Teletronics-SUI?node-id=6643-52207`

## Component Requirements

- Use `Backdrop`, component key `4271be8c7d2699b8ec5a8a5b30feb3d5eab219e7`.
- Use `<Dialog>`, component key `fccf45793ec542d2e3b09e635d23466412e7f095`.
- Treat SUI as read-only: import instances; do not modify source components.

## Drawing Notes

- This is a modal overlay state, not a new page.
- Keep RTL composition and preserve room for Arabic labels.
