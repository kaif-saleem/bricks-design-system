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

- Anatomy: single rounded container (244×60, `radius/m`) showing 4 digits with wide letter-spacing — not four separate per-digit boxes. Padding `spacing/s` (vertical) / `spacing/l` (horizontal), gap between characters `spacing/4xl`.
- Colors bound to the real published Bricks library (`color_Usage` collection), not this file's local token collections: container fill `background/neutral/primary`, border `stroke/primary` (Empty) / `stroke/grey1` (Filled), text `others/tag_1` (Empty placeholder) / `text/grey/grey1` (Filled digit).
- Two states exist: Empty (placeholder dashes) and Filled (digits). Empty/Filled currently differ in both border token and digit font size (32 vs 22) — unconfirmed whether intentional.
- Originally 5 instances of the shared `Input Fields` library component (3 of them exact duplicates, since removed). That master component is read-only from this file (published library), so it was detached to allow padding/gap/radius token binding — no live link back to the library component anymore.
- Not a reusable component yet: static frames, no variant/component-set structure, no Focus/Error/Disabled states.
- Uses one letter-spaced box rather than the more common per-digit-cell OTP pattern (Material, iOS, most banking apps) — no visual indication of current cursor position. Flagged as a design choice worth a deliberate call.

Status: unconfirmed test build (node 2242:879); tokens mapped and documented, pending Shashwat's review of the anatomy/state choices above

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
