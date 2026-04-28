# Teletronics SUI - Layout Rules

**File key:** `F8J2cgGBsmyFLyw9OW6Njq`  
**Library key:** `lk-aa0ef88728038c9ae27427ca27125d4040269e8343ea19cae768b802c7fc9ecf88220850c53b2a7ea40759c96276770ecedda46f53ed26f2ec07071bab202408`

Use this file as the local source of truth for Teletronics SUI spacing and corner radius variables. Do not re-read Figma variables during routine mockup work unless the design system has changed.

Project-specific application composition rules live in `app/rules.md`.

## Variable Collections

| Collection | collectionKey | Mode | Purpose |
|------------|---------------|------|---------|
| `spacing` | `92ba5b54bdeb4897c220ede407b916b59619fa61` | `Mode 1` | Auto-layout gaps and spacing scale |
| `shape` | `982a9360d94e957d2682b3137ddc3a6883fea382` | `Mode 1` | Corner radius values |

## Spacing Scale

Spacing variable names follow an 8px unit scale. The `0,5` token is the 4px half step.

| Token | Value | variableKey |
|-------|-------|-------------|
| `spacing/0,5` | 4 | `5802cf7607e39effe71efce8093e672a2b1ac981` |
| `spacing/1` | 8 | `05f16dfdb7691d84b93e41f57f8338034f530343` |
| `spacing/1,5` | 12 | `78d54912a641d67dd437790692191b9715012091` |
| `spacing/2` | 16 | `97b5cb898072ccb63ac14e7e6472f43a32d1e001` |
| `spacing/3` | 24 | `3bfbf5953284e1e1510a69677ea44d7c7c8f549b` |
| `spacing/4` | 32 | `f49304b24cb0da129e012c9c7c1e1d438389c282` |
| `spacing/5` | 40 | `1ace127c38896311edee8b215bc712e71a764dfa` |
| `spacing/6` | 48 | `fd0ba5ba157ec4f8accb5d5cb96b9f28f0820740` |
| `spacing/7` | 56 | `900c217fb0568e69caf71bbf7285ec4c9a1e4c77` |
| `spacing/8` | 64 | `a387fd5e64f3903a57aebd84929b5abcc4db1756` |
| `spacing/9` | 72 | `39cd6b7f6f5b9a72d92954cf9a23c7b4db1f784c` |
| `spacing/10` | 80 | `40cc272b78e9f851372fa32e359f7c89616e9478` |
| `spacing/11` | 88 | `ab7a55a6b79838c68f1dff18e0e04874a3507bb7` |
| `spacing/12` | 96 | `5ad2b78e0110b7de3912f2d5214b5bd42b5e6c43` |

## Corner Radius Scale

| Token | Value | variableKey |
|-------|-------|-------------|
| `cornerRadius/none` | 0 | `9fa38cac7d8f76f8aa8dfbfce8bf322d75cae714` |
| `cornerRadius/1` | 4 | `f73da7c2a208efeeefa31cfb68f89bed5f1a73ad` |
| `cornerRadius/2` | 8 | `58435501f96e75ab1c3e1be3be567a8d5dd52a50` |
| `cornerRadius/3` | 16 | `cdbb2d4d6b0d0de8268cdcb8a524e6b73fe719f0` |
| `cornerRadius/4` | 24 | `7ae48e502a4cc79b6ecbc80d0cab8be9a30b8ad5` |
| `cornerRadius/5` | 32 | `f327d0fe9a1f1c300365286398d67fecdfc2766d` |
| `cornerRadius/6` | 40 | `378ccc048165d31372e1df0d9053d7cbe74e731a` |
| `cornerRadius/7` | 48 | `09139cb6924bd25e156337d4cc4b123a00272624` |
| `cornerRadius/8` | 56 | `245de2403e634831a35ef8d8bd36ad65a0fa9ee0` |
| `cornerRadius/9` | 72 | `9cb8acb2f64b57bc9b4845bccf5e30a4a7f2c04b` |
| `cornerRadius/10` | 1000 | `bb99c7bb8d0d59afbb02d79e37d01190db32655a` |

## Common Drawing Defaults

- Compact internal gap: `spacing/1` (8px)
- Island-to-island gap: `spacing/1` (8px)
- Field-to-field gap: `spacing/2` (16px) or `spacing/3` (24px) depending density
- Card padding: `spacing/6` (48px) for roomy forms, `spacing/4` (32px) for compact forms
- Page section padding: `spacing/8` (64px) or higher
- Standard card radius: `cornerRadius/2` (8px)
- Dialog/sheet radius: `cornerRadius/3` (16px)
- Pills and fully rounded controls: `cornerRadius/10` (1000px)

## Runtime Notes

Import variables by key when binding spacing or corner radius in `use_figma`:

```js
const radius8 = await figma.variables.importVariableByKeyAsync('58435501f96e75ab1c3e1be3be567a8d5dd52a50');
node.setBoundVariable('cornerRadius', radius8);

const space24 = await figma.variables.importVariableByKeyAsync('3bfbf5953284e1e1510a69677ea44d7c7c8f549b');
node.setBoundVariable('itemSpacing', space24);
```
