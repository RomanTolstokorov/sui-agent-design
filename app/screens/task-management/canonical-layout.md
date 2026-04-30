# Task Management — Canonical Layout Preset

Use this file when building any new Task Management screen or variant. Follow the steps below in order — no Figma fetch needed for frame structure.

**Frame:** 1920 × 1080 px | Direction: RTL | Figma ref:** `OdNWALBR45nVe63thAAlEG` node `3915:129350`

---

## Default List Layout

### Step 1 — Root frame
Create a frame 1920 × 1080 px. Apply:
- Auto-layout: **HORIZONTAL**, `primaryAxisSizingMode = FIXED`, `counterAxisSizingMode = FIXED`
- Padding all sides bound to `spacing/1` (8 px)
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- Fill bound to `background/surface_0`

> The HORIZONTAL auto-layout + padding=`spacing/1` creates the 8 px inset and places children left-to-right. Do **not** manually position children with x/y offsets.

Children order (left → right): `App Container` first, `Sidebar` second (sidebar appears on the right — RTL start).

### Step 2 — Sidebar
Place `<Sidebar>` as the **second** child of the root (right side).

| Property | Value |
|----------|-------|
| componentKey | `12ede44857f7ed4ba7f2685ba56af26209767210` |
| Size | 64 × 1064 px |

### Step 3 — App Container
Create a frame as the **first** child of the root. Apply:
- Auto-layout: **VERTICAL**, `primaryAxisSizingMode = AUTO`, `counterAxisSizingMode = FIXED` (1832 px)
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- No padding, no fill
- Name: **App Container**

### Step 4 — Top bar
Place `<Application top-bar>` as the **first** child of App Container.

| Property | Value |
|----------|-------|
| componentKey (set) | `b6cde7cd669a24472f9645c0a38e57bab7d872e2` |
| Variant key | `9d20828730ff7b2399c4fd53b97221481369d931` (`Application=Tasks`) |
| Size | 1832 × 64 px |
| Title | Tasks |
| Active tab | Incoming |
| Incoming badge | 34/357 |
| Other tabs | All, Created by me |

### Step 5 — Content Area
Create a frame as the **second** child of App Container. Apply:
- Auto-layout: **HORIZONTAL**, `primaryAxisSizingMode = FIXED` (1832 px), `counterAxisSizingMode = FIXED` (992 px)
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- No padding, no fill
- Name: **Content Area**

Children order (left → right): `Task preview` first, `Task List and Filters Container` second.

#### Step 5a — Task preview (left, RTL end)
Create a frame as the **first** child of Content Area.

| Property | Value |
|----------|-------|
| Size | 1076 × 992 px |
| Fill | bound to `background/surface_2` |
| Corner radius | all 4 corners bound to `cornerRadius/2` |
| Name | **Task preview** |

#### Step 5b — Task List and Filters Container (right, RTL start)
Create a frame as the **second** child of Content Area. Apply:
- Auto-layout: **HORIZONTAL**, `primaryAxisSizingMode = AUTO`, `counterAxisSizingMode = FIXED` (992 px)
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- No padding, no fill
- Name: **Task List and Filters Container**

| Property | Value |
|----------|-------|
| Size | 748 × 992 px |

##### Step 5b-i — Task list
Place `<Task list>` as **first** child.

| Property | Value |
|----------|-------|
| componentKey | `59bdb48db0698778ebbdb04f0e4af7110dc0811a` |
| Size | 420 × 992 px |

##### Step 5b-ii — Filters
Place `<AppFilters>` as **second** child.

| Property | Value |
|----------|-------|
| componentKey (set) | `14eef66e973bc051e32f312ba45c31dec42e145e` |
| Variant | `State=Filled in, Tab=Search` |
| Size | 320 × 992 px |

---

## Variable bindings summary

| Frame | Property | Variable |
|-------|----------|----------|
| Root | fills | `background/surface_0` |
| Root | padding (all 4) | `spacing/1` |
| Root | itemSpacing | `spacing/1` |
| App Container | itemSpacing | `spacing/1` |
| Content Area | itemSpacing | `spacing/1` |
| Task List and Filters Container | itemSpacing | `spacing/1` |
| Task preview | fills | `background/surface_2` |
| Task preview | all corner radii | `cornerRadius/2` |

---

## Default State
- Top bar active tab: **Incoming**, badge 34/357
- Filters panel tab: **Search**, panel expanded
- Task list: one item in selected state
- Task preview: reflects the selected task

---

## Notes
- Do not edit the canonical component (`3915:129350`) — create a duplicate or new frame.
- **Never use raw hex or raw pixel values** for fills, gaps, padding, or radii — bind to variables.
- Child order within auto-layout determines visual position. Sidebar second = right side (RTL start).
- See `app/apps/task-management.md` for filter contents, task row fields, and drawing rules.
