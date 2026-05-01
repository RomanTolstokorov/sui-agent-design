# Editing Text Inside Library Component Instances

Use this instruction whenever text must change inside a placed Teletronics SUI library component instance, including button labels, dialog titles, list items, chips, tabs, menu items, and form labels.

## Required Method

Always walk the instance tree to reach the target `TEXT` node and set `.characters` directly, the same way a designer double-clicks into an instance and types.

1. Load every font used by the target text nodes with `figma.loadFontAsync`.
2. Recursively walk the component instance tree.
3. Find the intended `TEXT` node.
4. Set the node's `.characters` directly.

## Do Not

- Do not use `setProperties` for visible text content; it can update the property value without reliably rendering in Figma.
- Do not edit the main component to change instance text.
- Do not create a new component only to change text.
- Do not detach a library instance just to edit text.

## Notes

When multiple text nodes exist inside the same instance, identify the target by current text, node name, position, or surrounding component structure before writing.
