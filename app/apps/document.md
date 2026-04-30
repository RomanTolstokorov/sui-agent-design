# Documents App

## Overview

The Documents app is an S-System sub-app for reviewing, browsing, and managing documents. It follows the same dense bento-style island layout as other S-System apps, with a document list on the right (RTL start) and a document preview/detail panel on the left (RTL end).

## Canonical Reference

- **Figma file:** `Document-applications`, key `ugiudOIGQo98cMUrItDpMI`
- **Canonical node:** `2076:7821` — "Documents - Canonical", 1920 × 1080 px
- **Canonical layout preset:** `app/screens/document/canonical-layout.md`
- **Edit policy:** Treat as reference. Create a duplicate or new frame — do not edit the canonical component directly.

## Layout Structure

| Zone | Size (px) | Notes |
|------|-----------|-------|
| Outer frame | 1920 × 1080 | RTL, fill `background/surface_0` |
| App shell | 1904 × 1064 | 8 px padding from outer frame |
| Sidebar | 64 × 1064 | Right edge (RTL start), shared SUI component |
| Top bar | 1832 × 64 | Full content-column width |
| Working area | 1832 × 992 | y=72, flex row, 8 px gap |
| Document Preview panel | 1076 × 992 | Left (RTL end), `background/surface_2`, `cornerRadius/2` |
| Document List panel | 748 × 992 | Right (RTL start) |

## Top Bar

- **Title:** Documents
- **Default active tab:** Draft
- **Actions:** (to be documented from Figma)

## Document Preview Panel

The preview panel shows the selected document's full content. Sections observed in the canonical frame:

- **Action bar** — Edit (outlined), Delete (text), view mode toggles
- **Document header** — user avatar, document ID, creation date, report icon
- **Metadata tabs** — Comments, Keywords, Tasks, Attachments, Entities, Reply, Document
- **Content area** — chips/tags (e.g. country tags), form input fields
- **Pagination** — numbered pages, page 1 selected by default

Default active metadata tab: **Document**.

## Document List Panel

Scrollable list of document items. Each item shows document metadata (title, ID, date, status). Exact row component key to be confirmed from Figma.

## Drawing Rules

1. Read `app/rules.md` and `app/figma-map.json` first.
2. Read this file and `app/apps/document.json` before drawing any Documents feature.
3. Use `app/screens/document/canonical-layout.md` as the layout blueprint — do not fetch the Figma canonical node just to determine frame structure.
4. Use published SUI components by `componentKey` from `figma/components/index.json`.
5. Sidebar and top bar use the same shared SUI components as all other S-System apps.
6. Keep RTL alignment and preserve Arabic expansion space.
7. Keep 8 px island gaps. Use `background/surface_2` for list/preview islands.
8. Create a duplicate or new frame — do not modify the canonical component.

## Open Questions

- Full top bar tab list (only "Draft" confirmed as default).
- Document list item component key.
- Filter panel — whether Documents has an `<AppFilters>` panel like TPM.
- Empty, loading, error, and no-results states.
- Responsive behavior below 1920 × 1080.
