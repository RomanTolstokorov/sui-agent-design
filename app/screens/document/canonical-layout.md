# Documents — Canonical Layout Preset

Use this file when building any new Documents screen or variant. Follow the steps below in order — no Figma fetch needed for frame structure.

**Frame:** 1920 × 1080 px | Direction: RTL | Figma ref:** `ugiudOIGQo98cMUrItDpMI` node `2076:7821`

---

## Default List Layout

### Step 1 — Root frame
Create a frame 1920 × 1080 px. Apply:
- Auto-layout: **HORIZONTAL**, `primaryAxisSizingMode = FIXED`, `counterAxisSizingMode = FIXED`
- Padding all sides bound to `spacing/1` (8 px)
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- Fill bound to `background/surface_0`

> The HORIZONTAL auto-layout + padding=`spacing/1` creates the 8 px inset on all sides and places children left-to-right. Do **not** manually position children with x/y offsets.

Children order (left → right): `Main Content` first, `<Sidebar>` second (sidebar appears on the right — RTL start).

### Step 2 — Sidebar
Place `<Sidebar>` as the **second** child of the root (right side). Same SUI component as all S-System apps.

| Property | Value |
|----------|-------|
| componentKey | `12ede44857f7ed4ba7f2685ba56af26209767210` |
| Size | 64 × 1064 px |

### Step 3 — Main Content
Create a frame as the **first** child of the root. Apply:
- Auto-layout: **VERTICAL**, `primaryAxisSizingMode = AUTO`, `counterAxisSizingMode = FIXED` (1832 px)
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- No padding, no fill
- Name: **Main Content**

### Step 4 — Top bar
Place `<Application top-bar>` as the **first** child of Main Content.

| Property | Value |
|----------|-------|
| componentKey (set) | `b6cde7cd669a24472f9645c0a38e57bab7d872e2` |
| Variant key | `e85c1b140056545b74a5b5f0e6ed0295b5e75b2c` (`Application=Documents`) |
| Size | 1832 × 64 px |
| Title | Documents |
| Active tab | **Drafts** |
| Other tabs | Shared with me (badge 34), Created by me |

### Step 5 — Content Area
Create a frame as the **second** child of Main Content. Apply:
- Auto-layout: **HORIZONTAL**, `primaryAxisSizingMode = FIXED` (1832 px), `counterAxisSizingMode = FIXED` (992 px)
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- No padding, no fill
- Name: **Content Area**

Children order (left → right): `Document Preview` first, `Document List` second.

#### Step 5a — Document Preview (left, RTL end)
Create a frame as the **first** child of Content Area.

| Property | Value |
|----------|-------|
| Size | **1076 × 992 px** |
| Fill | bound to `background/surface_2` |
| Corner radius | all 4 corners bound to `cornerRadius/2` |
| Name | **Document Preview** |

Contains (top to bottom): action bar (Edit, Delete, view toggles), document header (avatar + ID + date), metadata tabs (Comments / Keywords / Tasks / Attachments / Entities / Reply / Document), content area (chips/tags, form fields), pagination.

Default active metadata tab: **Document**.

#### Step 5b — Document List (right, RTL start)
Create a frame as the **second** child of Content Area. Apply:
- Auto-layout: **HORIZONTAL**, `primaryAxisSizingMode = AUTO`, `counterAxisSizingMode = FIXED` (992 px)
- Gap (`itemSpacing`) bound to `spacing/1` (8 px)
- No padding, no fill
- Name: **Document List**

| Property | Value |
|----------|-------|
| Size | **748 × 992 px** |

Contains scrollable list of document items with metadata (title, ID, date, status).

---

## Variable bindings summary

| Frame | Property | Variable |
|-------|----------|----------|
| Root | fills | `background/surface_0` |
| Root | padding (all 4) | `spacing/1` |
| Root | itemSpacing | `spacing/1` |
| Main Content | itemSpacing | `spacing/1` |
| Content Area | itemSpacing | `spacing/1` |
| Document Preview | fills | `background/surface_2` |
| Document Preview | all corner radii | `cornerRadius/2` |

---

## Default State
- Top bar active tab: **Drafts**
- Document metadata tab: **Document** (active with bottom border indicator)
- Document Preview: one document selected and visible
- Pagination: page 1 selected

---

## Notes
- Do not edit the canonical component (`2076:7821`) — create a duplicate or new frame.
- **Never use raw hex or raw pixel values** for fills, gaps, padding, or radii — bind to variables.
- Child order within auto-layout determines visual position. Sidebar second = right side (RTL start).
- The root is HORIZONTAL, same as Task Management.
- See `app/apps/document.md` for document list fields, tab contents, and drawing rules.
