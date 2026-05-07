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

### Page node target has no geometry

**Symptom:** Inspecting or positioning against a user-provided target node fails or returns unusable geometry when the target is a Figma page, because page nodes do not expose `x` / `y` placement fields.

**Cause:** A page node is a container for frames, not a drawable scene node. When a user sends a page node ID as the target, it means "draw on this page", not "draw inside this positioned node".

**Workaround:** preflight the target node type before any geometry reads. If the target is a page, switch to that page and create the screen frame on it. Only read `x` / `y` after checking that the target supports geometry.
```js
const target = await figma.getNodeByIdAsync(targetNodeId);

if (target?.type === "PAGE") {
  await figma.setCurrentPageAsync(target);
  const screen = figma.createFrame();
  screen.name = "New screen";
  screen.resize(1920, 1080);
  target.appendChild(screen);
  screen.x = 0;
  screen.y = 0;
} else if ("x" in target && "y" in target) {
  // Safe to position relative to target geometry.
} else {
  throw new Error(`Unsupported drawing target type: ${target?.type ?? "missing"}`);
}
```

**Discovered:** 2026-05-04

---

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

---

### New frames default to raw white fill

**Symptom:** Frames created with `figma.createFrame()` receive a default white `SOLID` fill, usually `{ r: 1, g: 1, b: 1 }`, with no variable binding. Container frames that should be transparent can therefore end up with a hardcoded `#ffffff` paint that violates the no-raw-color rule and is easy to miss visually.

**Cause:** Figma initializes newly created frame nodes with a white fill by default. The Plugin API does not provide a creation option to disable this.

**Workaround:**
```js
const frame = figma.createFrame();

// For layout-only/container frames:
frame.fills = [];

// For actual surfaces:
frame.fills = [{
  type: "SOLID",
  color: { r: 1, g: 1, b: 1 },
  boundVariables: {
    color: { type: "VARIABLE_ALIAS", id: surfaceVariable.id }
  }
}];
```

**Discovered:** 2026-05-06

---

### Shared plugin data namespace rejects hyphens

**Symptom:** `setSharedPluginData()` fails when the namespace contains a hyphen, with the error `The namespace can only consist of alphanumeric characters, _ or .`

**Cause:** Figma shared plugin data namespaces are restricted to letters, numbers, underscores, and dots.

**Workaround:** define a stable namespace constant before writing shared plugin data. Use `_` or `.` as word separators; do not use `-`.
```js
const namespace = "agent_design"; // valid
// const namespace = "agent-design"; // invalid

node.setSharedPluginData(namespace, "entity", "task");
```

**Discovered:** 2026-05-06

---

### Resize leaves auto-layout frames fixed and clipped

**Symptom:** An auto-layout frame that should hug its children keeps a fixed height or width after `resize()`. Imported instances are correct, but the parent frame can clip or hide content because its sizing mode no longer follows the content.

**Cause:** `resize()` writes explicit dimensions. For auto-layout frames, the intended hug or fill behavior must be restored with sizing mode properties after the resize and, when the frame is inside another auto-layout parent, after append.

**Workaround:**
```js
const stack = figma.createFrame();
stack.layoutMode = "VERTICAL";
stack.resize(2200, 100);
stack.primaryAxisSizingMode = "AUTO";
stack.counterAxisSizingMode = "FIXED";

const row = figma.createFrame();
row.layoutMode = "HORIZONTAL";
row.resize(100, 100);
row.primaryAxisSizingMode = "AUTO";
row.counterAxisSizingMode = "AUTO";

parent.appendChild(stack);
stack.layoutSizingHorizontal = "FILL";
stack.primaryAxisSizingMode = "AUTO";
```

**Discovered:** 2026-05-06

---

### Library import session hits LiveGraph subscription limit

**Symptom:** Repeated `importComponentByKeyAsync` / `importComponentSetByKeyAsync` calls in one `use_figma` script start failing with `LivegraphSubscriptionLimitError: LiveGraph subscription limit (100) exceeded for session (next view: StateGroupByKeyWithDestinationAsset)`.

**Cause:** Importing many remote library components in one plugin execution can exhaust Figma's live graph subscription budget for that session.

**Workaround:**
```js
// Import large component inventories in small batches across separate use_figma calls.
// Keep each batch well below the observed limit, e.g. 20-30 library assets.
const batch = entries.slice(start, end);
for (const entry of batch) {
  const instance = await createSuiInstance(entry.componentKey, entry.name);
  target.appendChild(instance);
}
```

**Discovered:** 2026-05-07
