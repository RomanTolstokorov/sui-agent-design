# Importing SUI Components Safely

Use this instruction before inserting any published Teletronics SUI component into a Figma file.

## Why

Entries in `figma/components/index.json` can point to either:

- a single Figma component, imported with `figma.importComponentByKeyAsync`
- a Figma component set, imported with `figma.importComponentSetByKeyAsync`

Some summary entries use the field name `componentKey` even when the key resolves as a component set. Do not assume the import API from the field name alone.

## Required Import Helper

In `use_figma` scripts, use one helper for all SUI imports:

```js
async function createSuiInstance(key, name, variantMatcher) {
  try {
    const component = await figma.importComponentByKeyAsync(key);
    const instance = component.createInstance();
    if (name) instance.name = name;
    return instance;
  } catch (componentError) {
    const set = await figma.importComponentSetByKeyAsync(key);
    const component = variantMatcher
      ? set.children.find(variantMatcher)
      : null;
    const selected = component || set.defaultVariant || set.children[0];
    const instance = selected.createInstance();
    if (name) instance.name = name;
    return instance;
  }
}
```

## Variant Selection

When a component set needs a specific variant, pass a matcher:

```js
const topBar = await createSuiInstance(
  "b6cde7cd669a24472f9645c0a38e57bab7d872e2",
  "<Application top-bar> / Tasks",
  component => component.name === "Application=Tasks"
);
```

If no matcher is provided, use the set's `defaultVariant`, then fall back to the first child.

## Rules

- Prefer specific variant keys from app or screen docs when they are provided.
- If only a general SUI key is available, use `createSuiInstance` rather than choosing `importComponentByKeyAsync` or `importComponentSetByKeyAsync` manually.
- Return created instance IDs from every Figma script.
- Do not detach imported SUI instances to work around import or variant issues.

## Scripting gotchas

See `app/instructions/figma-api-gotchas.md` for all Figma API quirks and validated workarounds (page placement, INSTANCE_SWAP, etc.).
