# Component-Specific Rules

Styling decisions for individual components, dictated by the designer over time. One section per component, PascalCase, matching the component name in `REGISTRY.md`. Append new sections as they are given. Do not remove or soften an existing rule without the designer's confirmation.

Format per component:

```
## ComponentName
- rule
- rule
Status: confirmed | unconfirmed
```

---

## InputField

- Anatomy: Container > Label (12 Medium, `text/secondary`) > Field (280w, padding `m`/`s`, radius `m`, `surface/white`, 1.5px `border/default`) > Helper Text (12 Regular, `text/muted`).
- States on one `State` axis: Default, Hover (`border/brand`), Focus (`border/brand` + 4px `purple/300` outside ring), Filled (`text/primary` value), Error (`semantic_border/danger` border, `semantic_text/danger` helper), Disabled (`surface/disabled`, `border/disabled`, muted text).
- No icons yet (needs Iconography instance swap), no Show Label / Show Helper Text booleans wired yet, single size only.

Status: unconfirmed test build (node 1459:2134); every choice above pending Shashwat's review

## IconButton

- Built on its own Icon Button Figma page as an `IconButton` component set (node `2415:2338`, key `7a5e861c267757507c4c8d5f7c3682c6fcd09abd`). Variant axes: Variant (Primary, Secondary, Tertiary) x Size (S 32×32, M 36×36, L 40×40) x State (Default, Disabled) — 18 variants.
- Icon scales with Size — S=16px, M=20px, L=24px — matching the icon-button scale validated against Carbon's equivalent component. Icon is a real instance-swap of the Iconography library, never a recreated vector.
- Token choices mirror production Button exactly: Primary fill `surface/brand` + icon `text/inverse`; Secondary transparent fill + `border/brand` stroke + icon `text/brand`; Tertiary transparent fill, no stroke, icon `text/brand`. Corner radius `radius/m` (12px) on all variants. Padding `spacing/xs` (8px) — bound to the real `spacing` collection, not `radius`, after the spacing/radius collection-collision bug was found and fixed across this and two other already-shipped components (see the standing RULEBOOK-compliance note for the full trap).
- Disabled matches production Button's convention exactly, not the DS-wide 40%-opacity muted pattern used elsewhere (e.g. Toggle's ReadOnly): full opacity, with distinct disabled tokens — Primary/Secondary fill `surface/disabled`, Secondary stroke `border/disabled`, Tertiary stays transparent, icon color `grey_neutral/4` uniformly across all three variants.
- Known gap: touch target is 32/36/40px — short of Material's 48dp and Apple HIG's 44pt minimum recommended touch target for icon-only controls. Researched and flagged; not yet implemented pending a decision on transparent hit-area padding (Toggle precedent: 48×48 via padding around a smaller visible control) vs. accepting the smaller size for dense toolbar/list-row contexts.
- Known gap: no named `INSTANCE_SWAP` component property exposed for the icon — consumers cannot pick an icon from the properties panel; swapping the icon today means manually detaching/replacing the instance, breaking the live library link.
- No Hover/Pressed/Focus states built yet (WCAG 2.4.7 focus-visible still missing — same gap as Toggle).

Status: unconfirmed test build (node 2415:2338); pending Shashwat's review

## Checkbox

- Stroke uses the primary stroke color token (`border/default`).
- Checked and active fill uses `lavender_mist/2`.

Status: unconfirmed (stated once, not yet applied to a built component)

## RadioButton

- Stroke uses the primary stroke color token (`border/default`).
- Checked and active fill uses `lavender_mist/2`.
- Selected dot: `icon/brand_1`. Disabled: `surface/disabled` + `border/disabled`, dot `icon/grey_3`. Hover: stroke `border/brand`. Focus: 4px ring `purple/300`, matching the production Button's focus treatment.
- Control size 20px, dot 8px, full radius.

Status: confirmed for stroke + active fill (dictated by Shashwat in session, applied in test build node 1459:2077); dot/disabled/hover/focus/size choices pending his review of the test build
