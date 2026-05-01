# Documents App

## Overview

The Documents app is an S-System sub-app for reviewing, browsing, and managing documents. It follows the same dense bento-style island layout as other S-System apps, with a document list on the right (RTL start) and a document preview/detail panel on the left (RTL end).

Documents represent correspondence and related working content: drafts, submitted documents, replies, responses, attachments, classifications, keywords, linked tasks, and imported data. Users use Documents to review existing correspondence, continue draft work, edit document content, and submit completed drafts.

Common document work:

- Browse or filter documents and drafts.
- Select a document from the list and review its preview/detail.
- Open a draft or document inside a task-centric editor.
- Edit document body, metadata, attachments, related tasks, keywords, or imported data.
- Save progress manually or through autosave status.
- Submit a draft when the document is ready.
- Adjust sharing or classification when that control is part of the requested screen.

## Canonical Reference

- **Figma file:** `Document-applications`, key `ugiudOIGQo98cMUrItDpMI`
- **Canonical node:** `2076:7821` — "Documents - Canonical", 1920 × 1080 px
- **Canonical layout preset:** `app/screens/document/canonical-layout.md`
- **Edit policy:** Treat as reference. Create a duplicate or new frame — do not edit the canonical component directly.

## Canonical Layout

For exact frame construction, sizing behavior, token bindings, and component keys, use `app/screens/document/canonical-layout.md`. Use `app/apps/document.json` only when a script needs machine-readable canonical references or layout values.

At a product level, the default Documents workspace combines a document list on the right side of the working area and a selected document preview/detail panel on the left. Keep the list row and preview content coherent when a document is selected.

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

When no document is selected, show a compact empty/instructional state. When a document is selected, keep the list row and preview content coherent.

## Document List Panel

Scrollable list of document items. Each item shows document metadata (title, ID, date, status). Exact row component key to be confirmed from Figma.

Rows should show enough business signal for scanning: document subject/title, ID, date, draft/submitted/read status where relevant, and selected state when the preview reflects that item.

## Common UX States

- **Draft:** editable work with visible save status and submit affordance.
- **Saved:** edited draft with saved state shown near the editor controls.
- **Submitted/read-only:** submitted correspondence with review actions rather than editing-first controls.
- **Selected document:** selected row drives the preview/detail panel.
- **No access:** keep the document context visible where possible and show a restricted-content state.
- **Validation/error:** show the issue near the document section or action that needs correction.
- **Empty/no results:** keep filters/list structure visible and show an empty state in the list or preview area.

## Drawing Rules

1. Read `app/rules.md` and `app/figma-map.json` first.
2. Read this file and `app/apps/document.json` before drawing any Documents feature.
3. Use `app/screens/document/canonical-layout.md` as the layout blueprint; do not fetch the Figma canonical node just to determine frame structure.
4. Use published SUI components by `componentKey` from `figma/components/index.json`.
5. Sidebar and top bar use the same shared SUI components as all other S-System apps.
6. Keep RTL alignment and preserve Arabic expansion space.
7. Use the canonical `spacing/1` island gaps. Use `background/surface_2` for list/preview islands.
8. Create a duplicate or new frame — do not modify the canonical component.
9. Keep document-specific actions close to the document preview/editor context.
10. Show draft/saved/submitted state when the requested screen involves document editing.

## Open Questions

- Full top bar tab list (only "Draft" confirmed as default).
- Document list item component key.
- Filter panel — whether Documents has an `<AppFilters>` panel like Task Management.
- Empty, loading, error, and no-results states.
- Responsive behavior below 1920 × 1080.
