# Search — Canonical Layout Preset

Use this file when building any new Search screen or variant. Follow the steps below in order. Use the Figma canonical node only for content detail that is not captured here.

**Frame:** 1920 x 1080 px | Direction: RTL | Figma ref: `YFsunyZ8IDCjPBOJbVu6zO` node `2882:27314`

---

## Default Search Layout

### Step 1 — Root frame

Create a frame 1920 x 1080 px. Apply:

- Auto-layout: **HORIZONTAL**, `primaryAxisSizingMode = FIXED`, `counterAxisSizingMode = FIXED`
- Padding all sides bound to `spacing/1` (8 px)
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- Fill bound to `background/surface_0`

Children order (left to right): `App Container` first, `Sidebar` second. The sidebar appears on the right for RTL.

### Step 2 — Sidebar

Place `<Sidebar>` as the second child of the root.

| Property | Value |
| --- | --- |
| componentKey | `12ede44857f7ed4ba7f2685ba56af26209767210` |
| Size | 64 x 1064 px |

### Step 3 — App Container

Create a frame as the first child of the root. Apply:

- Auto-layout: **VERTICAL**, fixed 1832 x 1064 px
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- No padding, no fill
- Name: **App Container**

### Step 4 — Top bar

Place `<Application top-bar>` as the first child of App Container.

| Property | Value |
| --- | --- |
| Component | `<Application top-bar>` |
| Variant | `Application=Search` |
| Size | 1832 x 64 px |

### Step 5 — Search Query Island

Place or recreate the canonical `<SearchQueryIsland>` region as the second child of App Container.

| Property | Value |
| --- | --- |
| Name | `<SearchQueryIsland>` |
| Size | 1832 x 64 px |
| Fill | bound to `background/surface_2` |

Use this island for search type controls, keyword input, query clear action, and immediate query/view controls.

### Step 6 — Working Area

Create a frame as the third child of App Container. Apply:

- Auto-layout: **HORIZONTAL**, fixed 1832 x 920 px
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- No padding, no fill
- Name: **Document Previews**

Children order (left to right): `Draft Preview Scrollable: Full screen` first, `Filters and Document List` second.

#### Step 6a — Preview / detail island

Create a frame as the first child of the working area.

| Property | Value |
| --- | --- |
| Name | `Draft Preview Scrollable: Full screen` |
| Size | 1046 x 920 px |
| Fill | bound to `background/surface_2` |
| Purpose | Selected result preview/detail, or instructional empty state when no result is selected |

#### Step 6b — Results and filters group

Create a frame as the second child of the working area. Apply:

- Auto-layout: **HORIZONTAL**, fixed 778 x 920 px
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- No padding, no fill
- Name: **Filters and Document List**

Children order (left to right): `Document List` first, `Filters` second. In RTL reading order this appears as filters, results, then preview/detail.

##### Step 6b-i — Document List

Place the canonical document/result list as the first child.

| Property | Value |
| --- | --- |
| Name | `Document List` |
| Size | 420 x 920 px |
| Fill | bound to `background/surface_2` |

##### Step 6b-ii — Filters

Create or use the canonical filters panel as the second child.

| Property | Value |
| --- | --- |
| Name | `Filters` |
| Size | 350 x 920 px |
| Fill | bound to `background/surface_2` |

---

## Variable Bindings Summary

| Frame | Property | Variable |
| --- | --- | --- |
| Root | fills | `background/surface_0` |
| Root | padding (all 4) | `spacing/1` |
| Root | itemSpacing | `spacing/1` |
| App Container | itemSpacing | `spacing/1` |
| Working Area | itemSpacing | `spacing/1` |
| Results and filters group | itemSpacing | `spacing/1` |
| Query island | fills | `background/surface_2` |
| Preview / detail island | fills | `background/surface_2` |
| Document List | fills | `background/surface_2` |
| Filters | fills | `background/surface_2` |

---

## Default State

- Search app top bar is visible.
- Query island is ready for input.
- Results/list region is visible next to filters.
- Preview/detail island shows selected result content or an instructional empty state.

## Notes

- Do not edit the canonical component (`2882:27314`) unless explicitly requested.
- Never use raw hex or raw pixel values for fills, gaps, padding, or radii when a variable exists.
- Search-specific components such as `<SearchQueryIsland>` and document-list internals may not all be present in the local SUI component index. Inspect the Search canonical file before recreating those internals.
