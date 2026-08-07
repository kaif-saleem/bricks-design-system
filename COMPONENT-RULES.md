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
- Designer decisions from brief intake: Web and Mobile both required, both built as a Device variant axis. Title and chevron only, no leading icon or trailing badge. Group behavior is single-expand, collapsible (documented as a Behavior, not a variant, since it is group-level logic). Chevron sits to the right of the title (superseded 2026-08-07: initially built left-aligned per Carbon's accessibility guidance, moved to the right per the designer's explicit direction, matching the majority convention across shadcn/Radix, Fluent's default, and Chakra's examples).
- Anatomy: Container (vertical Auto Layout, no fill) > Header (horizontal Auto Layout, padding `s`/`m`, gap `s`) > Leading Icon (optional) + Title + Chevron (always visible) > Content Panel (only present when Open, padding `none`/`m`) > Divider (1px, boolean-controlled).
- Superseded 2026-08-07: the earlier build modeled Expansion (Expanded/Collapsed) and an interaction State (Default/Hover/Focus/Disabled) as two separate Variant axes, matching the Selection-vs-State precedent set by RadioButton. Per the designer's explicit direction, State was removed entirely: the only variant is Expansion, renamed `Collapsed`/`Open`. Hover, focus, and disabled are no longer baked into Figma variants; engineering must still implement them (a visible focus indicator remains required by Rulebook §12), and this is now called out as a Behavior in the component's documentation rather than a variant. Variant count dropped from 16 (Device x Expansion x State) to 4 (Device x Expansion).
- Superseded 2026-08-07 (second revision, same day): the designer clarified the optional icon belongs to the title, not the chevron, citing Uber's pattern of an optional leading icon before a list/row title with a fixed trailing disclosure indicator. Added a new Leading Icon layer before the Title. The chevron is no longer optional, it always shows since it is the component's primary open/closed signal. The `Show Icon` boolean was re-wired from the chevron to the new Leading Icon (`componentPropertyReferences`), so the property name did not need to change. `Show Divider` is unchanged.
- Container fill: added `surface/white` earlier in the day per the designer's direction, then removed again same day per further direction ("no fill"). Current state: no container fill, transparent.
- Chevron direction, superseded 2026-08-07 (third revision, same day): the chevron initially rotated between pointing right (Collapsed) and pointing down (Open), a 90 degree turn. Per the designer's direction it now points down when Collapsed and up when Open, a 180 degree flip, matching the common caret-flip convention.
- Tokens: Title text style `Body/default_medium` (Web or Mobile ramp), Content Panel text `Body/default_regular`. Divider `border/subtle`. Chevron and Leading Icon stroke both `icon/grey_3`.
- Known non-compliance: both the chevron (`lucide:chevron-right`, rotation -90deg Collapsed / 90deg Open) and the leading icon (`lucide:file-text`) are placeholder Lucide vectors, not instance swaps from the Iconography (Bricks) library, because the exact component names could not be looked up without switching the frontmost Figma file away from Bricks Design System (Rules §3). Same category of gap as the deleted Checkbox test build. Must be swapped before this can move to production.
- Known gaps (not invented, per Gaps.md): no motion/duration or easing token exists yet, so the expand/collapse transition timing is left unspecified rather than a made-up number. No stroke-width token exists; the 1px divider matches the ad hoc precedent already used elsewhere (InputField, RadioButton borders).

Status: unconfirmed proposal build (node 2436:489, page "Accordion"), fully bound and pipeline-audited except the icon instance swap gap above; awaiting Shashwat's review before promotion out of do-not-use
