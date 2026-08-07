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

## OTPField

- Built on its own OTP field Figma page as an `OTPField` component set (node 2243:1229). Variant axis: State (Default, Filled, Error). 1 dimension, 3 variants, all built.
- Anatomy: single rounded Container (Auto Layout, horizontal, fixed 244x60, padding `spacing/l` horizontal and `spacing/s` vertical, gap `spacing/4xl` between characters, radius `radius/m`, 1px border) holding 4 Character text nodes directly. No separate per-digit boxes.
- Default and Filled pull fill, border, and text colors from the published Bricks library (`color_Usage`, a remote collection outside this file's 5 local collections): container fill `background/neutral/primary`, border `stroke/primary` (Default) or `stroke/grey1` (Filled), text `others/tag_1` at 32px (Default placeholder) or `text/grey/grey1` at 22px (Filled digit).
- Error pulls border and text from this file's own local `color_tokens` instead: border `semantic_border/danger`, text `semantic_text/danger` at 22px. This is a mixed source, not a single one. Confirm with the designer which source Error should use once the published library has a matching error token.
- Originally 5 instances of the shared `Input Fields` library component (3 of them exact duplicates, since removed). That master component is read-only from this file (published library), so it was detached to allow padding, gap, and radius token binding. No live link back to the library component remains.
- Uses one letter-spaced text box rather than the more common per-digit-cell OTP pattern seen in Material, iOS, and most banking apps. No visual indication of current cursor position. A deliberate design choice worth confirming, not a bug.
- No focus state, no per-character caret, and no auto-advance between characters is built. This is a static display of three states, not yet a working input.
- Known gap: digit text has no shared text style bound (`textStyleId` is empty on every character), only a raw font size. Needs a real text style before this ships.
- Full documentation, including Overview, Purpose, When to use, When not to use, Properties, Variants, Behaviors, Accessibility, Specs, and Do's and Don'ts, lives in the Documentation frame on the OTP field page, following the structure in `templates/documentation-template.md` (RULEBOOK §13).

Status: unconfirmed test build (node 2243:1229); pending Shashwat's review of the anatomy, state, and mixed token source choices above

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
