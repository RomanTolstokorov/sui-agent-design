# Teletronics SUI - Color and Elevation Rules

**File key:** `F8J2cgGBsmyFLyw9OW6Njq`  
**Library key:** `lk-aa0ef88728038c9ae27427ca27125d4040269e8343ea19cae768b802c7fc9ecf88220850c53b2a7ea40759c96276770ecedda46f53ed26f2ec07071bab202408`  
**Foundations page node:** `11751:13526`  
**Colors Styles frame node:** `11835:7665`  
**Palette collection key:** `dea8e0b24ac6b1130d6aac352244bc931b31370f`

Use this file as the local source of truth for Teletronics SUI Light and Dark color/elevation decisions. Do not re-read Figma variables during routine mockup work unless the design system has changed.

## Runtime Rules

- Use only `Light` and `Dark` modes from the `palette` variable collection for routine drawings.
- Prefer binding/importing variables by key when the node should follow theme mode changes.
- Use `background/surface_*` tokens for app and container backgrounds instead of raw grays.
- Treat `background/surface_*` tokens as contextual surfaces, not a strict global elevation ladder. Any surface can appear after another when the composition needs it.
- Use `text/primary`, `text/secondary`, and `text/disabled` for text fills.
- Use `primary/main` for primary actions and `primary/contrastText` for text on primary fills.
- Use `divider` or `components/input/border` for strokes, not arbitrary border colors.
- Use Figma effect styles by key for elevations instead of manually inventing shadows.

## Text Tokens

| Token | Light | Dark | variableKey |
|-------|-------|------|-------------|
| `text/primary` | `#1b1d21` | `#f7f7f7` | `4d32b2f7a0c37b8f66994f71b32e0b9b3fa253fb` |
| `text/secondary` | `#1b1d21b2` | `#f7f7f7b2` | `a26d060dd55c952c6a727f682eaeb4717353fa5c` |
| `text/disabled` | `#1b1d214d` | `#f7f7f761` | `4cc5d32b04e2114f858c5c63cd90514a51ff6ab2` |
| `text/link` | `#3b6bf6` | `#81c1ff` | `bd1c75fd651840ea2f96d82c61ee50f5f6d98303` |

## Primary Tokens

| Token | Light | Dark | variableKey |
|-------|-------|------|-------------|
| `primary/main` | `#3b6bf6` | `#81c1ff` | `98959278111c805060b504594616f165ddd8e939` |
| `primary/dark` | `#163bf5` | `#6196f8` | `138bded53317ccec8ed3deb443672b7ba430ce9a` |
| `primary/light` | `#6196f8` | `#d8ecfd` | `c3322411d911dffc40bcfc5090dbb34e854b9389` |
| `primary/contrastText` | `#f7f7f7` | `#1b1d21` | `b88a4febb0cc830f76698643da725f6fb524f27f` |

## Secondary Tokens

| Token | Light | Dark | variableKey |
|-------|-------|------|-------------|
| `secondary/main` | `#232528` | `#c3c6ca` | `b18997940cce9b6fd77557d59cad1a2139fa348d` |
| `secondary/dark` | `#1b1d21` | `#9fa2a8` | `f7e62f0e7e000e2d29aad4a1244fd8736eb724e0` |
| `secondary/light` | `#3e4045` | `#f7f7f7` | `153e764a62c217407fb4106decd7618090401733` |
| `secondary/contrastText` | `#ffffff` | `#000000` | `8caffbd7c77c5c6b2dceb212b5931f4e40684b01` |

## Semantic Tokens

| Token | Light | Dark | variableKey |
|-------|-------|------|-------------|
| `error/main` | `#d83731` | `#d83731` | `ca3e360fd48ef071f0f0c728a44d288b57c331ec` |
| `error/dark` | `#95231f` | `#faaaa7` | `da1c1ad8f9918f6ced7c810265980f5e4b23b855` |
| `error/light` | `#f47a75` | `#b52520` | `cff2f017b14a67783b632905378eac7c04a05279` |
| `warning/main` | `#ef6c00` | `#e65100` | `dee3d1116efa22702f6a0210214985804712178b` |
| `warning/dark` | `#e65100` | `#ffb74d` | `a3070fac02eab971340a36a9b154bcb65daf8822` |
| `warning/light` | `#ff9800` | `#e65100` | `15cc9530a4f15536d59b98eb516a29b6017e0816` |
| `info/main` | `#0073ab` | `#00608d` | `37285ff658b1061b0b0cf03e9047707d8e3c5668` |
| `info/dark` | `#224f71` | `#2ccaff` | `cf89c6cd03d06f41481d84871a7a50fbbe63e04c` |
| `info/light` | `#00abeb` | `#14324b` | `f89c5e00df31740a6468745353217fe36fa1bb04` |
| `success/main` | `#3f8e50` | `#3f8e50` | `dc5b12cad3b4a98a5e8d72ce305f660fdf182736` |
| `success/dark` | `#24432b` | `#a0d5ab` | `10bc0cd3ed64dd68fbb7b3baa5ebf270b9c4f310` |
| `success/light` | `#a0d5ab` | `#24432b` | `cf182c775d6183f9e859399c5ac44184339dadda` |

All semantic `contrastText` tokens resolve to `#ffffff` in both Light and Dark.

## Background and Surface Tokens

| Token | Light | Dark | Recommended use |
|-------|-------|------|-----------------|
| `background/default` | `#ffffff` | `#232529` | Default layout/page background. Maps to `theme.palette.background.default`; use when the layout expects the MUI default background rather than the layered app-canvas surface. |
| `background/surface_0` | `#f2f2f2` | `#121317` | Base contextual surface token for independent composition contexts. Project-specific frame usage lives in `app/rules.md`. |
| `background/surface_1` | `#f7f7f7` | `#131416` | Contextual section or panel surface. Can be used before or after other surface tokens when the composition needs this contrast. |
| `background/surface_2` | `#fcfcfc` | `#1c1e21` | Contextual island, grouped-area, or highlight surface. It does not need to follow `surface_1`. |
| `background/surface_3` | `#ffffff` | `#232529` | Contextual container surface. Maps to `theme.palette.background.paper`; useful for cards, panels, menus, and content containers, but can be followed by lower-numbered surfaces inside it. |
| `background/surface_ai_1` | `#ffffff` | `#212121` | AI chat surface primary |
| `background/surface_ai_2` | `#f9f9f9` | `#181818` | AI chat surface secondary |

Surface sequence is flexible: valid compositions include `surface_0 -> surface_2 -> surface_1 -> surface_3`, `surface_3 -> surface_2`, and similar combinations. Add elevation effects only when the element should visually float above its current surface; surface number alone does not imply elevation depth.

## Action and Structure Tokens

| Token | Light | Dark | Use |
|-------|-------|------|-----|
| `action/active` | `#0e0f1299` | `#ffffff99` | Active icons and action states |
| `action/disabled` | `#0e0f1261` | `#ffffff61` | Disabled foreground |
| `action/disabledBackground` | `#0e0f121a` | `#ffffff1a` | Disabled control fill |
| `action/hover` | `#0e0f120d` | `#ffffff14` | Hover overlays |
| `action/selected` | `#0e0f1214` | `#ffffff29` | Selected overlays |
| `action/focus` | `#0e0f1226` | `#ffffff26` | Focus overlay |
| `action/focusStroke` | `#0e0f1233` | `#ffffff33` | Focus stroke |
| `divider` | `#1b1d211f` | `#ffffff1f` | Dividers and subtle strokes |
| `components/input/border` | `#e1e3e5` | `#60646c` | Text field and input borders |
| `components/appBar/defaultFill` | `#e1e3e5` | `#131416` | App bars |
| `components/tooltip/fill` | `#3e4045` | `#f7f7f7` | Tooltip fills |
| `components/snackbar/fill` | `#3e4045` | `#f7f7f7` | Snackbar fills |

## Elevation Variables

| Token | Light | Dark | variableKey |
|-------|-------|------|-------------|
| `elevation/inputShadow` | `#9670261f` | `#05063680` | `1ed2b8e1c9fbb7aeab370efcde89aa16c26b0f01` |
| `elevation/inputShadow-2` | `#a67e301a` | `#08112780` | `c9a2a938ab096471d6753709cf347ab16c04c0ac` |
| `elevation/inputShadow-3` | `#644b1b14` | `#00000014` | `89110427ebdaaa52d91dd22e1a317a26691d45d8` |
| `elevation/outlined` | `#e0e0e0` | `#ffffff1f` | `007f00a19c3e86b5aabf71656072f7b0b05d17a1` |

## Elevation Effect Styles

Use these keys with `figma.importStyleByKeyAsync(key)` and assign the imported style to `node.effectStyleId`.

| Effect style | styleKey | Notes |
|--------------|----------|-------|
| `elevation/1` | `4e891a16fb9b18afc92e930982803dde51f2cd73` | One low shadow, 0x1, radius 2 |
| `elevation/2` | `9838aa64780e18f17b8bc9d70801b7a31bc2f608` | Two low shadows |
| `elevation/3` | `22eb28591f6ffc3a5e6265e049ee98e857a77466` | Two medium shadows |
| `elevation/4` | `d06f0eb767a1a962547366bc6153e3674cc259a0` | Two medium shadows |
| `elevation/5` | `f393bc75b4854be8316b6d4f9b64ba3dfa3f1a16` | Larger card shadow |
| `elevation/6` | `332a850a24e7ec3707d6912f9249fb361ad09f37` | Three high shadows |
| `elevation/7` | `c2cf8beab68a2f14efc28462dc81cc7191ed850d` | Warm/input-style shadow using elevation variables |
| `elevation/8` | `89773891477918a080a17d672f9f30939fbdd8fa` | Three high shadows |
| `elevation/9` | `2cd94016f3bc06aa5448e7518b1410086ecd2812` | Three high shadows |
| `elevation/10` | `12260634ebd0e498e30a5aa9a5ea354c864b015f` | Three high shadows |
| `elevation/ai_chat_input` | `5a560bb4eb9b3309dc299c906bfd45b40b0e3c32` | AI input shadow |
| `elevation/error` | `f0c31dde78fbaa699e49baf2e28995b6c1ef85f3` | Error-state shadow |
| `elevation/prompt_input` | `d961d2eedf0e413688c279cbaa3d675c7f563d76` | Multi-layer prompt input shadow |

Additional elevation styles `elevation/11` through `elevation/23` exist for large overlay depths. Use the JSON index for their keys.

## Common Drawing Defaults

- Card/dialog surface: `background/surface_3`
- Main title: `text/primary`
- Supporting text: `text/secondary`
- Primary button fill: `primary/main`
- Text on primary button: `primary/contrastText`

Project-specific screen composition rules, including which surface starts app frames, live in `app/rules.md`.
- Input border: `components/input/border`
- Card shadow: `elevation/2` for subtle cards, `elevation/5` for stronger cards
