# Accessibility Standards Index

This folder contains the three frameworks that MUST be consulted when generating FRONTEND_DESIGN.md.

---

## Framework Roles

| Framework | Role |
|-----------|------|
| WCAG 2.1 | Legal/standard floor — always required, non-negotiable |
| APCA | Preferred contrast method — more accurate than WCAG 2.x ratios, especially for dark mode |
| HIG | Universal interaction design reference — applies to all platforms, not just Apple |

> HIG is included because Apple's interaction design standards represent the highest publicly documented bar for human-computer interaction. The principles translate directly to web, Android, desktop, and any other platform. Ignore the Apple-specific API names; adopt the principles.

---

## When to Read Each Document

| Document | Read when... |
|----------|-------------|
| `WCAG21.md` | Setting baseline compliance requirements |
| `APCA/APCAeasyIntro.md` | Understanding the contrast algorithm — read this first |
| `APCA/APCA_in_a_Nutshell.md` | Quick Lc value lookup by font size/weight |
| `APCA/minimum_compliance.md` | Verifying correct APCA implementation |
| `HIG/accessibility.md` | Perception and interaction targets |
| `HIG/color.md` | Semantic color, dark mode, color management |
| `HIG/typography.md` | Font size minimums, weight selection, scaling |
| `HIG/modality.md` | When interrupting the user is justified |
| `HIG/feedback.md` | Confirming actions, response timing |
| `HIG/loading.md` | Perceived performance, wait states |
| `HIG/motion.md` | Animation as communication |
| `HIG/alerts.md` | Destructive action patterns |
| `HIG/layout.md` | Visual hierarchy, spatial logic |
| `HIG/inclusion.md` | Inclusive design beyond accessibility |
| `HIG/writing.md` | UI copy clarity and tone |

---

## Key Values to Always Apply

### Contrast (APCA Lc — preferred)

| Use case | Minimum Lc |
|----------|-----------|
| Body text (columns, paragraphs) | Lc 75 |
| Content text (not body) | Lc 60 |
| Large headlines (36px normal / 24px bold) | Lc 45 |
| Spot-readable / placeholders / disabled | Lc 30 |
| Discernible non-text (dividers, decorative) | Lc 15 |
| Dark mode body text | Lc 75 (negative polarity) |

### Contrast (WCAG 2.1 AA — legal minimum fallback)

| Use case | Minimum ratio |
|----------|--------------|
| Normal text (< 18px / < 14px bold) | 4.5:1 |
| Large text (>= 18px / >= 14px bold) | 3:1 |
| UI components and graphics | 3:1 |

> WCAG 2.x ratios are unreliable for dark mode. Always use APCA Lc for dark mode decisions.

### Typography Minimums

| Platform | Default | Minimum |
|----------|---------|---------|
| Web (general) | 16px | 12px |
| iOS/iPadOS | 17pt | 11pt |
| macOS | 13pt | 10pt |
| tvOS | 29pt | 23pt |
| visionOS | 17pt | 12pt |
| watchOS | 16pt | 12pt |

### Touch Targets

- Apple HIG minimum: 44×44pt
- Web/Android equivalent: 48×48px recommended

---

## Compliance Hierarchy

```
WCAG 2.1 AA     — legal/standard floor, always required
     ↓
APCA Bronze     — preferred contrast method, use Lc values
     ↓
HIG principles  — interaction quality bar, platform-agnostic
     ↓
DESIGN.md       — project-specific overrides (must not drop below WCAG 2.1 AA)
```

No design decision may drop below WCAG 2.1 AA, regardless of DESIGN.md instructions.
