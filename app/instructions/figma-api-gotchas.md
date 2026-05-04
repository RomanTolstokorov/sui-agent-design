# Figma API Gotchas and Workarounds

Central registry of Figma API / `use_figma` scripting quirks encountered while drawing Teletronics SUI screens. Read this before starting any drawing session that runs scripts. Every entry is a workaround that has been validated in this codebase.

When you hit a new blocker, follow the **Figma API Workaround Rule** in `app/rules.md`: propose a new entry here, get user approval, then append.

## Entry Format

```
### <Short symptom title>
**Symptom:** <error or behavior observed, exact error string quoted>
**Cause:** <root cause if known>
**Workaround:**
​```js
// minimal code
​```
**Discovered:** <YYYY-MM-DD>
```

## Entries

### Page placement — nodes land on wrong page

**Symptom:** `createInstance()` and other node creators silently append to `figma.currentPage` instead of the intended target page. Querying `page.children` from a non-active page returns empty.

**Cause:** Figma API operates on the active page; `currentPage` is not switched implicitly when you reference another page object.

**Workaround:**
```js
await figma.setCurrentPageAsync(targetPage);
// only now create nodes or read targetPage.children
```

**Discovered:** pre-2026-05-02 (migrated from `sui-component-imports.md`)

---

### INSTANCE_SWAP rejects ComponentNode on wrapper components

**Symptom:** `setProperties` rejects `ComponentNode` values for INSTANCE_SWAP properties on wrapper components in this codebase. Validated against `<Icon>`.

**Cause:** Wrapper instance's INSTANCE_SWAP property does not accept a raw imported component as a value.

**Workaround:** call `swapComponent` on the inner instance directly:
```js
const inner = inst.findOne(n => n.type === "INSTANCE");
inner.swapComponent(importedComponent);
```

**Discovered:** pre-2026-05-02 (migrated from `sui-component-imports.md`)

---

### Text edits require loaded fonts

**Symptom:** editing text content or text metrics fails with errors like `Cannot write to node with unloaded font "Noto Kufi Arabic Regular". Please call figma.loadFontAsync({ family: "Noto Kufi Arabic", style: "Regular" }) and await the returned promise first.` It also fails after applying an imported text style if that style's font was not loaded, for example `Cannot write to node with unloaded font "Alexandria Bold".`

**Cause:** Figma requires every font used by a `TEXT` node to be loaded before changing `.characters`. This applies even when the text node already exists, and importing/applying a text style by `styleKey` does not load that style's font. Typography styles are already declared in the DS; do not work around this by setting raw font values or text metrics.

**Workaround:**
```js
const dsFonts = [
  { family: "Noto Kufi Arabic", style: "Regular" },
  { family: "Noto Kufi Arabic", style: "Medium" },
  { family: "Noto Kufi Arabic", style: "SemiBold" },
  { family: "Alexandria", style: "Light" },
  { family: "Alexandria", style: "Regular" },
  { family: "Alexandria", style: "Medium" },
  { family: "Alexandria", style: "SemiBold" },
  { family: "Alexandria", style: "Bold" },
  { family: "Inter", style: "Regular" }
];

for (const font of dsFonts) {
  await figma.loadFontAsync(font);
}
```

**Discovered:** 2026-05-02
