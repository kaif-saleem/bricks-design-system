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

## Toggle

- Built on its own Toggle Figma page as a `Toggle` component set (node 1729:82). Variant axes: Size (Medium, Small) x Value (Off, On) x State (Default, ReadOnly). 3 dimensions, 8 variants, all built.
- Anatomy: Container (Auto Layout, horizontal, centers its one child, fixed width matching the track, fixed height 48) holds Track (Auto Layout, horizontal, fixed 52x32 Medium or 44x24 Small, padding `spacing/2xs` all sides, radius `radius/l`) holds Thumb (Ellipse, fixed 24x24 Medium or 18x18 Small).
- Track fill: `border/default` (Off), `surface/brand` (On). Thumb: `surface/white`, subtle drop shadow. No stroke on the track.
- ReadOnly uses the DS-wide muted-state convention (DESIGN.md §8: 40% opacity, no pointer events). This is the same treatment as every other atom's non-interactive state, not a separate Disabled state.
- Container height is fixed at 48px, matching the common 48px minimum tap target. Container width equals the track width (52px Medium, 44px Small), so this is not a full 48x48 touch target on the horizontal axis. Flagged as a known gap, not corrected yet.
- Off and On are shown by thumb position, not by track color alone. Clicking a Default-state variant plays a 150ms Smart Animate transition: the thumb slides to the opposite edge and the track fill swaps at the same time. ReadOnly variants have no click reaction.
- No built-in label or icon slot. Every instance needs an external visible label for `aria-labelledby`.
- Known gap: no Focus-visible variant is built (WCAG 2.4.7). Needed before this ships to keyboard users.
- Full documentation, including Overview, Purpose, When to use, When not to use, Properties, Variants, Behaviors, Accessibility, Specs, and Do's and Don'ts, lives in the Documentation frame on the Toggle page, following the structure in `templates/documentation-template.md` (RULEBOOK §13).

Status: unconfirmed test build (node 1729:82); pending Shashwat's review
