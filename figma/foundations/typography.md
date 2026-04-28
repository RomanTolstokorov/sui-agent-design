# Teletronics SUI - Typography Rules

**File key:** `F8J2cgGBsmyFLyw9OW6Njq`  
**Library key:** `lk-aa0ef88728038c9ae27427ca27125d4040269e8343ea19cae768b802c7fc9ecf88220850c53b2a7ea40759c96276770ecedda46f53ed26f2ec07071bab202408`  
**Foundations page node:** `11751:13526`  
**Typography frame node:** `11835:7604`

Use this file as the local source of truth for Teletronics SUI typography. Do not re-read Figma text styles during routine mockup work unless this file is stale or the design system has changed.

## Font Rules

- Load `Noto Kufi Arabic` before placing Teletronics SUI component instances that use body, label, input, button, caption, or paragraph text.
- Load `Alexandria` before placing heading text or components that use heading styles.
- Default app font stack follows the MUI theme: `Noto Kufi Arabic, Helvetica, Arial, sans-serif`.
- Heading variants `h1` through `h6` use `Alexandria`.
- Body, subtitle, caption, overline, paragraph, and button styles use `Noto Kufi Arabic`.
- Letter spacing below is recorded as Figma pixel values. The MUI theme converts some values to `em`.

## MUI Variant Mapping

| MUI variant | Figma text style | Family | Style | Weight | Size | Line height | Letter spacing |
|-------------|------------------|--------|-------|--------|------|-------------|----------------|
| `h1` | `typography/h1` | Alexandria | Light | 300 | 96 | 116.7% | -1.5px |
| `h2` | `typography/h2` | Alexandria | Light | 300 | 60 | 120% | -0.5px |
| `h3` | `typography/h3` | Alexandria | Regular | 400 | 48 | 116.7% | 0px |
| `h4` | `typography/h4` | Alexandria | SemiBold | 600 | 34 | 123.5% | 0.25px |
| `h5` | `typography/h5` | Alexandria | Bold | 700 | 24 | 140% | 0px |
| `h6` | `typography/h6` | Alexandria | Medium | 500 | 20 | 160% | 0.15px |
| `subtitle1` | `typography/subtitle1` | Noto Kufi Arabic | SemiBold | 600 | 16 | 175% | 0.15px |
| `subtitle2` | `typography/subtitle2` | Noto Kufi Arabic | SemiBold | 600 | 14 | 157% | 0.1px |
| `body1` | `typography/body1` | Noto Kufi Arabic | Regular | 400 | 16 | 175% | 0.1px |
| `body2` | `typography/body2` | Noto Kufi Arabic | Regular | 400 | 14 | 170% | 0.1px |
| `caption` | `typography/caption` | Noto Kufi Arabic | Regular | 400 | 12 | 150% | 0.1px |
| `overline` | `typography/overline` | Noto Kufi Arabic | Regular | 400 | 12 | 266% | 1px |

## Button Text Styles

Teletronics SUI has dedicated button text styles. Use these when creating or overriding button labels instead of generic `typography/button`.

| Button style | Family | Style | Weight | Size | Line height | Letter spacing | Text transform |
|--------------|--------|-------|--------|------|-------------|----------------|----------------|
| `button/large` | Noto Kufi Arabic | Medium | 500 | 15 | 26px | 0px | none |
| `button/medium` | Noto Kufi Arabic | Medium | 500 | 14 | 24px | 0px | none |
| `button/small` | Noto Kufi Arabic | Medium | 500 | 13 | 22px | 0px | none |

The MUI `button` variant in `s-system-ui` maps to the same family and weight as `button/medium`, with font size `14`, line height `1.714`, and `textTransform: none`.

## Paragraph Styles

Additional paragraph styles exist in the Teletronics SUI library for rich text blocks.

| Figma text style | Family | Style | Weight | Size | Line height | Letter spacing | Decoration |
|------------------|--------|-------|--------|------|-------------|----------------|------------|
| `typography/paragraph/regular` | Noto Kufi Arabic | Regular | 400 | 16 | 180% | 0% | none |
| `typography/paragraph/bold` | Noto Kufi Arabic | SemiBold | 600 | 16 | 180% | 0% | none |
| `typography/paragraph/underline` | Noto Kufi Arabic | Regular | 400 | 16 | 180% | 0% | underline |

## Figma Style Keys

| Figma text style | styleKey |
|------------------|----------|
| `typography/h1` | `af32c422982c0abb7593965f846a6a6dda844969` |
| `typography/h2` | `de548bc0add9441e87c0d53f0c039d64861d5cd7` |
| `typography/h3` | `88a56af7952e88eff38e85f695dbe62f74d6cbd1` |
| `typography/h4` | `5533bffb5c17cf8377e050bd31034085dacae5a4` |
| `typography/h5` | `b2767ae833d2048d84a6a8af6034f724e1cefc2c` |
| `typography/h6` | `719e26c5de7ba5251f466be3a88e9f81835fb98d` |
| `typography/subtitle1` | `a4b19621f2ae693d75f30b5c7dbbbd34030f890e` |
| `typography/subtitle2` | `04fab5bbc985c06650a7dd23369ae7da241f9f94` |
| `typography/body1` | `ba864006f7e839382b9ebe8b39743b81caee52c1` |
| `typography/body2` | `e387a23bfb7a81668b7d56a44e589c7b5b1009c3` |
| `button/large` | `55f1a71171b931bb91ad6bd44acc0004df3100e4` |
| `button/medium` | `320b4abb981d996ab141ec3620a11a27c96f8da0` |
| `button/small` | `e4fb34935bb8ef29abe503d5c1beed77bc769537` |
| `typography/caption` | `ac7180aee280c41e3ebf6481b1e4ce1e050d4a4b` |
| `typography/overline` | `5b3de4c6fee0555fe92ef401d8052751fbff2a91` |
| `typography/paragraph/bold` | `8d3c452b6562053d3f8dd8bc938da09edbcc2cf3` |
| `typography/paragraph/regular` | `6e0316783ec3633714f646782f5518f1c57fb1fc` |
| `typography/paragraph/underline` | `dad2b9ea098e4db38aea061d1ec26dc731b21bb9` |

## Runtime Notes

When using `use_figma`, load required fonts before creating or appending imported SUI component instances:

```js
await figma.loadFontAsync({ family: 'Noto Kufi Arabic', style: 'Regular' });
await figma.loadFontAsync({ family: 'Noto Kufi Arabic', style: 'Medium' });
await figma.loadFontAsync({ family: 'Alexandria', style: 'Light' });
await figma.loadFontAsync({ family: 'Alexandria', style: 'Regular' });
```

Add other Alexandria weights as needed for headings: `Medium`, `SemiBold`, `Bold`.
