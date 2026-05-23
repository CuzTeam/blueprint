# Module: DESIGN.md Integration

Handles the relationship between a user-supplied Google-style `DESIGN.md` and the generated `FRONTEND_DESIGN.md`.

---

## Source Priority

When generating FRONTEND_DESIGN.md, source decisions in this order:

```
1. DESIGN.md (user-supplied) — highest authority
2. SPEC.md (feature list, user flows)
3. ARCHITECTURE.md (routes, components)
4. Project description from alignment interview
5. Agent inference — lowest authority, use only when nothing else covers it
```

Never invent a design decision that contradicts a higher-priority source.

---

## IF DESIGN.md is present

1. Read it fully before writing FRONTEND_DESIGN.md
2. Extract: design principles, color decisions, typography, component patterns, interaction rules
3. Map each DESIGN.md section to the corresponding FRONTEND_DESIGN.md section
4. Set frontmatter: `source: DESIGN.md`
5. Where DESIGN.md is silent, fill from SPEC.md/ARCHITECTURE.md or note as "TBD per design system"
6. Do not contradict DESIGN.md on any point — if a conflict exists with SPEC.md, flag it as an open question in README.md

## IF DESIGN.md is not present

1. Generate FRONTEND_DESIGN.md from SPEC.md features + ARCHITECTURE.md routes
2. Set frontmatter: `source: inferred`
3. For accessibility section, apply standards from `references/accessibility/` (see below)
4. Mark sections that would benefit from a DESIGN.md as: `<!-- Inferred — provide DESIGN.md for authoritative values -->`

---

## HIG as Universal Interaction Reference

Apple's Human Interface Guidelines are **not Apple-platform-exclusive**. The interaction principles within HIG represent some of the most rigorous publicly available thinking on human-computer interaction, and apply to **any platform** — web, Android, desktop, CLI, embedded.

When generating FRONTEND_DESIGN.md, always consult HIG for:

| HIG Topic | Universal Principle |
|-----------|-------------------|
| `modality.md` | When to interrupt the user vs. stay in flow |
| `feedback.md` | How and when to confirm user actions |
| `loading.md` | Managing perceived wait time |
| `offering-help.md` | Contextual help without cluttering the UI |
| `gestures.md` | Touch/pointer interaction patterns |
| `motion.md` | Animation as communication, not decoration |
| `entering-data.md` | Form UX and reducing input friction |
| `alerts.md` | Destructive action confirmation patterns |
| `notifications.md` | Interruption hierarchy and permission |
| `searching.md` | Search placement, behavior, feedback |
| `layout.md` | Visual hierarchy and spatial relationships |
| `typography.md` | Type scale, weight, readability |
| `color.md` | Semantic color usage, dark mode |
| `inclusion.md` | Inclusive design principles |
| `writing.md` | UI copy tone and clarity |

> HIG's platform-specific API names (e.g. `UIKit`, `SwiftUI`, `Dynamic Type`) should be translated to their platform-equivalent concepts. The **principle** is what matters, not the implementation name.

---

## Accessibility Standards (always apply)

When writing FRONTEND_DESIGN.md, the accessibility section is **non-negotiable** regardless of tier, platform, or source. Apply rules from:

- `references/accessibility/WCAG21.md` — baseline legal/standard compliance
- `references/accessibility/APCA/` — contrast calculation method (preferred over WCAG 2.x ratios for modern displays)
- `references/accessibility/HIG/accessibility.md` — interaction and perception targets (apply universally)
- `references/accessibility/HIG/color.md` — semantic color and dark mode rules
- `references/accessibility/HIG/typography.md` — font size and weight minimums

### Decorative Element Rule

Before applying any contrast exemption, the element must pass this check:

```
IF element conveys state, meaning, hierarchy, or affordance
  → Must meet minimum Lc 45 (APCA) / 3:1 (WCAG 2.1 AA) — no exemption
ELIF element is purely visual separation and removing it does not affect understanding
  → Lc 15 minimum acceptable
ELSE (element serves no perceivable purpose)
  → Remove it. "Decorative" is not a license to ship invisible noise.
```

This check must be documented for any element claimed as decorative in FRONTEND_DESIGN.md.

### Minimum Requirements to include in FRONTEND_DESIGN.md

```markdown
## Accessibility

### Contrast
- Body text (< 18px/400w): minimum Lc 75 (APCA) / 4.5:1 (WCAG 2.1 AA)
- Large text (>= 18px/400w or 14px/700w): minimum Lc 60 (APCA) / 3:1 (WCAG 2.1 AA)
- Non-text UI elements (icons, borders): minimum Lc 45 (APCA) / 3:1 (WCAG 2.1 AA)
- Disabled elements: minimum Lc 30 (APCA) — intentionally reduced, not an oversight
- Dark mode: recalculate all values — WCAG 2.x ratios unreliable for dark mode; use APCA Lc
- Decorative elements: must pass decorative element rule (see design-integration.md)

### Typography
- Minimum body font size: 16px (web) / 17pt (iOS) / 13pt (macOS)
- Avoid Ultralight, Thin, Light weights at small sizes (per HIG/typography.md)
- Support text scaling up to 200%
- Prefer Regular, Medium, Semibold, Bold — proven legibility weights across all platforms

### Color
- Never rely on color alone to convey state or meaning — pair with icon, label, or pattern (HIG)
- Provide light and dark mode variants for all custom colors
- Test under varied ambient lighting conditions
- Color must be semantically consistent — never use the same color to mean different things (HIG)

### Interaction
- All interactive elements must be keyboard-navigable
- Minimum touch/tap target: 44×44pt equivalent (HIG) — translate to px/dp per platform
- Focus indicators must meet Lc 45 minimum against adjacent colors
- Confirm destructive actions — never make them instantly irreversible (HIG/alerts.md)
- Modality used sparingly — interruptions must be earned (HIG/modality.md)

### Feedback
- Every user action must produce perceivable feedback within 100ms (HIG/feedback.md)
- Loading states required for any operation > 1 second (HIG/loading.md)
- Error messages must be specific — never generic "something went wrong" (HIG/offering-help.md)

### Motion
- Respect prefers-reduced-motion — static alternatives for all animations (HIG/motion.md)
- Animation must communicate, not decorate — every motion has a purpose
```

---

## End-of-run Prompt

Always output this after completing the skill, regardless of whether DESIGN.md was present:

```
> You can drop a Google DESIGN.md to /.docs/<planname>/DESIGN.md
> Run Blueprint again after dropping it to regenerate FRONTEND_DESIGN.md from your design doc.
```
