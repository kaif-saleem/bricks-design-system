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

- Built on its own Icon Button Figma page as an `IconButton` component set (node 2415:2338, key `7a5e861c267757507c4c8d5f7c3682c6fcd09abd`). Variant axes: Variant (Primary, Secondary, Tertiary) x Size (S 32x32, M 36x36, L 40x40) x State (Default, Disabled). 3 dimensions, 18 variants, all built.
- Anatomy: Container (Auto Layout, horizontal, hugs its one child, centers it, padding `spacing/xs` all sides, radius `radius/m`) holds Icon (instance swap from the Iconography library, scales with Size: 16px S, 20px M, 24px L).
- Token choices mirror production Button exactly: Primary fill `surface/brand` and icon `text/inverse`; Secondary transparent fill, `border/brand` stroke, icon `text/brand`; Tertiary transparent fill, no stroke, icon `text/brand`. Padding bound to the real `spacing` collection, not `radius`, after the spacing/radius collection-collision bug was found and fixed across this and two other already-shipped components. See [[feedback-bricks-rulebook-compliance]] for the full trap.
- Disabled matches production Button's convention exactly, not the DS-wide 40%-opacity muted pattern used elsewhere (for example Toggle's ReadOnly): full opacity, with distinct disabled tokens. Primary and Secondary fill `surface/disabled`, Secondary stroke `border/disabled`, Tertiary stays transparent, icon color `grey_neutral/4` uniformly across all three variants.
- Known gap: touch target is 32/36/40px, short of Material's 48dp and Apple HIG's 44pt minimum recommended touch target for icon-only controls. Researched and flagged, not yet implemented, pending a decision between transparent hit-area padding and accepting the smaller size for dense toolbar and list-row contexts.
- Known gap: no named `INSTANCE_SWAP` component property is exposed for the icon. Swapping it today means selecting the nested instance directly, not using a component property.
- No Hover, Pressed, or Focus-visible states are built yet (WCAG 2.4.7 needs a Focus-visible state before this ships to keyboard users, same gap as Toggle).
- Documentation format, superseded 2026-08-07, with Shashwat's/Sreejita's sign-off obtained for this specific change: the Documentation frame on the Icon Button page was rebuilt to match production Button's actual style (title in `purple/700` bold, section header + grey subtitle, light-grey-header data tables, divider rules between sections, closing checkmark/cross usage examples) instead of the plain Rulebook §13 prose template used in the original build. Same content as before (when to use, anatomy, properties, specs, states, behaviors, accessibility, known gaps, industry reference, usage), restructured only. Nothing on the `IconButton` component set (node 2415:2338) or Page kit was touched.
- QA Grid added 2026-08-07 (node 2459:10443, page "Icon Button", named "IconButton - QA Grid"): a reference grid of live instances of the built component set, grouped by Variant (Primary, Secondary, Tertiary) as rows, then every Size x State combination (S/M/L x Default/Disabled, 6 combinations) as one labeled card per row, 18 cards total. All three properties on this component are Variant axes, none are separate booleans, so every combination is a genuinely distinct case; confirmed empirically on a real instance that Tertiary's Default vs Disabled states differ (icon stroke color changes from `text/brand` to a muted grey) even though the container fill and stroke are both empty in both states, so no case was collapsed. Matches the documentation page's visual language. The component set and its documentation frame were not touched, verified by direct position/size/child-count comparison before and after (a minor x-position drift on the component set was observed and is not from any write this session — no eval call in this session ever wrote to that node).

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
