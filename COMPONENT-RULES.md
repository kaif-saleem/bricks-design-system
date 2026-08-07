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

## Accordion

- Benchmarked against Material (legacy M1 only, no current M3 spec), Ant Design, Carbon, Atlassian, Polaris, Fluent UI, Radix/shadcn, and Chakra before building, per the designer's request. Cross-system consensus: chevron indicator (not plus/minus), button-semantics trigger with aria-expanded/aria-controls, Enter/Space to toggle, arrow keys plus Home/End between headers (W3C ARIA APG accordion pattern). No consensus on single vs multiple expand default, or icon side.
- Designer decisions from brief intake: Web and Mobile both required. Title and chevron only, no leading icon or trailing badge. Group behavior is single-expand, collapsible (documented as a Behavior, not a variant, since it is group-level logic). Chevron sits left of the title, per Carbon's accessibility guidance that a left-aligned indicator sits closer to the title it controls.
- Anatomy: Container (vertical Auto Layout) > Header (horizontal Auto Layout, padding `s`/`m`, gap `s`) > Icon + Title > Content Panel (only present when Expanded, padding `none`/`m`) > Divider (1px, boolean-controlled).
- Expansion (Expanded/Collapsed) and State (Default/Hover/Focus/Disabled) are modeled as two separate Variant axes, not merged, matching the Selection-vs-State precedent already set by RadioButton above.
- Tokens: Default no fill; Hover `surface/subtle`; Focus 4px `purple/300` ring (same treatment already confirmed for RadioButton and production Button); Disabled `surface/disabled` fill and `text/muted` title, matching InputField's disabled convention. Divider `border/subtle`. Title text style `Body/default_medium` (Web or Mobile ramp), Content Panel text `Body/default_regular`.
- Known non-compliance: the chevron is a placeholder Lucide vector (`lucide:chevron-right`, rotated -90deg when expanded), not an instance swap from the Iconography (Bricks) library, because the exact chevron component name could not be looked up without switching the frontmost Figma file away from Bricks Design System (Rules §3). Same category of gap as the deleted Checkbox test build. Must be swapped before this can move to production.
- Known gaps (not invented, per Gaps.md): no motion/duration or easing token exists yet, so the expand/collapse transition timing is left unspecified rather than a made-up number. No stroke-width token exists; the 1px divider matches the ad hoc precedent already used elsewhere (InputField, RadioButton borders).

Status: unconfirmed proposal build (node 2436:489, page "Accordion"), fully bound and pipeline-audited except the icon instance swap gap above; awaiting Shashwat's review before promotion out of do-not-use
