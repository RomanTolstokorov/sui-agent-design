# Drawing Modal Dialogs

Use this instruction for generic modal or dialog states. App, screen, and flow docs override this file when they describe a more specific workflow. For example, User Preferences uses a copied canonical authored dialog from `User-profile-settings`; follow `app/apps/user-preferences.md` and `app/screens/user-preferences/preferences-dialog.md` for that flow.

## 1. Create The Modal State Frame

Duplicate the target screen frame. The copy becomes the modal state frame. Name it `[original name] - Modal`. Do not edit the original screen state in place.

## 2. Layer Backdrop And Dialog

On top of the duplicated frame's contents:

1. Add the SUI `Backdrop` component from `figma/components/index.json`.
2. Set the backdrop as an overlay layer covering the entire duplicated frame.
3. Position the backdrop at `x=0`, `y=0`, resize it to the frame `width x height`, and use stretch constraints for left, right, top, and bottom when available.
4. Add the SUI `<Dialog>` component set from `figma/components/index.json` with `importComponentSetByKeyAsync`, then use its `defaultVariant`.
5. Place the `<Dialog>` instance above the backdrop and center it in the frame.

Do not leave the backdrop as a normal auto-layout child or only pinned to the top-left corner.

## 3. Fill Dialog Content Via Slot Swap

`<Dialog>` is a library component instance and must not be detached.

1. Create a dedicated page-local component for the dialog content, for example `Modal Content / <descriptive name>`.
2. Build the content component using SUI components only.
3. In the `<Dialog>` instance, navigate to the `_Library / Instance Slot` node inside `<DialogContent>`.
4. Call `swapComponent(formComp)` on the instance slot.

Do not edit nodes inside the `<Dialog>` instance directly except through supported instance behavior. The `<Dialog>` shell already provides `<DialogTitle>`, `<DialogContent>`, and `<DialogActions>`; only the content slot should be replaced.
