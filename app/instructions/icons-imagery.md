# Icons

Use this file when placing any icon in a Teletronics SUI screen. Every icon goes through the `<Icon>` wrapper component — never place a raw icon component directly on the canvas.

## The Icon Wrapper

The `<Icon>` component is a standardised size-and-instance container. It accepts an icon via INSTANCE_SWAP and controls the outer bounding box. This is the single correct way to place icons in SUI screens.

| Property | Key |
|----------|-----|
| Component set key | `89b4b8d62421765b68506d994ff843e190f726a0` |
| Figma file | `Teletronics-SUI` (`F8J2cgGBsmyFLyw9OW6Njq`) |
| Node | `6594:47648` |

### Size variants

| Variant (Size=) | Bounding box | When to use |
|-----------------|-------------|-------------|
| `Small` | 20 × 20 px | Compact rows, chips, badges, secondary controls |
| `Medium` | 24 × 24 px | **Default** — standard UI controls, buttons, list rows |
| `Large` | 32 × 32 px | Hero/prominent icons, empty states, feature callouts |
| `Inherit` | 16 × 16 px | Tight inline positions, small status indicators |

### Swapping the inner icon

The `<Icon>` wrapper contains one child instance (default: Star). Swap it using `swapComponent` — do **not** use `setProperties` for this; it does not accept ComponentNode values for this property.

```js
const inst = mediumComp.createInstance();
const inner = inst.findOne(n => n.type === "INSTANCE");
inner.swapComponent(iconComponentNode);
```

`iconComponentNode` is the component imported from the catalog. For variant-based icons (e.g. Chevron directions), import the component set and pick the variant from `.children`:

```js
const chevronSet = await figma.importComponentSetByKeyAsync("399373888321afba63acc45b5551c91b07574d73");
const upVariant = chevronSet.children.find(c => c.name === "Direction=Up");
inner.swapComponent(upVariant);
```

### Step-by-step: placing an icon

1. Import `<Icon>` set via `importComponentSetByKeyAsync("89b4b8d62421765b68506d994ff843e190f726a0")`.
2. Get the size variant: `set.children.find(c => c.name === "Size=Medium")`.
3. `mediumComp.createInstance()` — then append the instance to the target frame/node.
4. Import the target icon. For plain icons: `importComponentByKeyAsync(key)`. For variant-based icons (e.g. Chevron directions): import the component set, then pick from `.children`: `chevronSet.children.find(c => c.name === "Direction=Up")`.
5. `inst.findOne(n => n.type === "INSTANCE").swapComponent(iconComp)` — do not use `setProperties` for this swap.
6. Icon components come pre-wired: the leaf Vector inside every icon already has `components/icon/default` bound. For default color, nothing to do. To use `components/icon/secondary` (or any other variable): rebind the fill variable on the **leaf Vector node(s)** inside the swapped icon — call `findAll(n => n.type === "VECTOR")` on the `<Icon>` instance and apply `setBoundVariableForPaint` there. Do not bind on the `<Icon>` wrapper (it has zero fills) or on the swapped icon instance itself (binding there has no visual effect).

---

## Icon Color Variables

Never use raw hex values for icon fills. Standard rule: bind to `components/icon/default` (primary icon) or `components/icon/secondary` (subdued/helper icon). Both keys in `figma/foundations/colors.json → tokens.icons`.

Special icon sets have their own color variables — see their sections below.

## Icon Catalog

All icon instances live in the `↳ Icon` page of `Teletronics-SUI` (`F8J2cgGBsmyFLyw9OW6Njq`, page node `6594:47638`). Icons are plain COMPONENT nodes; use `importComponentByKeyAsync` to import them.

### General-purpose sections

Icons are named in PascalCase (e.g. `MagnifyingGlass`, `TrashSimple`, `ArrowRight`).

| Section | Icon count | Representative icons |
|---------|-----------|----------------------|
| Arrows | 101 | ArrowUpRight, ArrowLeft, ArrowCircleUp, ArrowURightDown |
| Office & Editing | 125 | Trash, TrashSimple, TextT, Tray |
| System & Devices | 140 | WifiX, Bell, Laptop, Monitor |
| Design | 112 | Triangle, Unite, TextAUnderline, Vignette |
| Media | 102 | Webcam, Play, MusicNote, Image |
| Finance & Math | 67 | TrendUp, TrendDown, XCircle, Percent |
| People | 54 | User, UsersThree, UserSwitch, Wheelchair |
| Maps & Travel | 78 | Van, Truck, Tram, TrainSimple |
| Communication | 61 | Translate, ThumbsUp, ThumbsDown, Voicemail |
| Security & Warnings | 41 | Warning, WarningCircle, Wall, ShieldCheck |
| Time | 21 | Timer, Watch, HourglassSimpleMedium |
| Education | 18 | GraduationCap, Student, Exam |
| Development | 25 | Terminal, Robot, TreeStructure |
| Others | 9 | FlagBanner_Filled, Star_Filled, Sub task, Wikipedia |
| Check | 2 | CheckCircle, Circle |
| Table Edit | 7 | Add Row Above, Add Row Below, Remove Row, Add Column Right, Remove Table |

### Special-purpose icon sets

Use these only in their designated contexts.

#### Task type icons (`Task types icons`, 68 icons)

Used exclusively for task type and subtype identification in Task Management and related apps. Colorful mode binds each icon fill to a `components/icon/task_types/*` variable from `colors.json`; Monochrome mode uses neutral styling (no palette variable applied).

Sample task type icons and their keys:

| Icon name | Component key |
|-----------|--------------|
| AdHock | `61c1f984fc4e96f36eaaf484a0aefbd650e13d35` |
| Attachment | `18684e72a7a11efc8555e37b8b2bd80d3be12a2b` |
| Correspondence | `936eb2fa0129effb26a3decdb85199586572cfe0` |
| DiscoveryAccess | `2e5dd9741564bc69873fc3783493cb8d181729df` |
| Broken | `9166e3ea2d140c15a620c313922771893ac9b677` |

For palette variable keys see `figma/foundations/colors.json → tokens.taskTypeIcons`.

#### Navigation / sidebar icons (`Navigation menu`, 6 icons)

The filled app-navigation icons used inside `<SidebarMenuItem>`. Placed via INSTANCE_SWAP on the sidebar item — do not use as standalone icons elsewhere.

| Icon name | Component key |
|-----------|--------------|
| House-filled (Home) | `37946c18b36aa08edf1b9cb4ca8ae9f0bd46fb05` |
| CheckCircle-filled (Tasks) | `90bbdb275337579b5b06e87a3a2fe01f7c1403b9` |
| FileText-filled (Documents) | `f53ebd938b8e310ee535687e6ace8ff2bcb70d91` |
| TrayArrowDown-filled (Inbox/Search) | `02fb438710de250446b4ea32137827feffee0778` |
| MagnifyingGlass-filled (Search) | `4ad14ae6feb89a97038a8108eeb4c49dd3f6c27a` |
| AI chat | `d0aa8a5936fcef4942d42928a33b970b17c59387` |

#### Datasource group icons (5 icons)

Used in search results and record-type indicators. Bind fills to the matching `components/icon/datasource_group/*` variable; keys in `figma/foundations/colors.json → tokens.datasourceGroupIcons`.

Icons: Documents, Persons, Companies, Events, Other.

#### Filter operator icons (`Filter operator`, 12 icons)

Used inside `<AppFilters>` for condition/operator selectors on filter rows. Icons: contains, EndWith, StartWith, Equals, NotEquals, and related comparison operators.

#### File format icons (`File formats`, 7 icons)

Used as attachment or document-type indicators. Icons: Archive, Document, Image, S-Document, File, and related formats.

#### Inbox icons (`Inbox icons`, 10 icons)

Used in inbox/tab navigation: Documents, Correspondence, Ad-hoc, All, Correspondence-Filled, and related.

#### Entity icons (`Entities`, 9 icons)

Used in document metadata for entity-type labels: email, passport, person number, plate number, and related.

---

## Special icon components (with state variants)

These are full SUI component sets — import them via `importComponentSetByKeyAsync`, not as plain icon instances. Do not nest them inside `<Icon>`.

| Component | Set key | States |
|-----------|---------|--------|
| `✚Checkbox` | `b6621b791778c9bc9cd75b7ed8871e011ee9a33f` | OnFilled, Off, OnOutline, IndeterminateFilled, IndeterminateOutline |
| `✚RadioButton` | `498fddcd662530a156e020d78663e6a2e4eb39a0` | On, Off |

Refer to `figma/components/index.json` for the full `<Checkbox>` and `<Radio>` SUI component entries, which are separate from these icon variants.

---

## Rules summary

- Always use `<Icon>` (key `89b4b8d62421765b68506d994ff843e190f726a0`) to wrap any icon — never place raw icon components.
- Always set the icon via INSTANCE_SWAP (`Icon` property), never by replacing children directly.
- Always bind icon fills to color variables from `figma/foundations/colors.json` — never raw hex. Target the **leaf Vector node(s)** inside the swapped icon. The `<Icon>` wrapper has no fills; binding on the wrapper or the swapped icon instance has no visual effect.
- Task type icons in Colorful mode use `components/icon/task_types/*` variables.
- Navigation icons belong inside `<SidebarMenuItem>` — not as freestanding icons.
- Checkbox and RadioButton icon components are form elements, not `<Icon>` content.
