# <App Name> — <Screen / State Name>

Use this file when building [describe when to use this screen vs. the canonical layout].

**Frame:** 1920 × 1080 px | Direction: RTL | Figma ref: `<file-key>` node `<node-id>`

---

## Frame Tree

List top-level frames and their children in DOM order (which determines visual order under RTL auto-layout).

```
Root (HORIZONTAL, surface_0)
├── Main Content (VERTICAL)
│   ├── Top bar
│   └── Working Area (HORIZONTAL)
│       ├── Island A
│       └── Island B
└── Sidebar
```

## Important Nodes

List named nodes an agent will need to reference when placing or swapping components.

| Name | Node ID | Purpose |
|------|---------|---------|
| example | `0000:00000` | describe what it holds |

## States and Variants

List the screen states this doc covers, and any that are documented separately.

- **Default** — described in this file
- **<Other state>** — see `app/screens/<app-id>/<state>.md`

## Step-by-step Construction

### Step 1 — Root frame

### Step 2 — ...

## Variable Bindings Summary

| Frame | Property | Variable |
|-------|----------|----------|
| Root | fills | `background/surface_0` |

## Default State

Describe what is visible and active in the default render of this screen.

## Edge Cases

Note anything that deviates from the standard island/layout rules or that has caused agent mistakes before.

## Notes

- Do not edit the canonical component — duplicate or create a new frame.
- Never use raw hex or raw pixel values for fills, gaps, padding, or radii — bind to variables.
