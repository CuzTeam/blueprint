# Module: Tier System

Defines the available documentation tiers. The user must select a tier. Agent may recommend one based on project description, but cannot proceed without user confirmation.

---

## Tiers

| Tier | Name | For |
|------|------|-----|
| T1 | Minimal | Scripts, small tools, personal projects, quick experiments |
| T2 | Standard | Mid-size web apps, APIs, solo-dev products |
| T3 | Full | Team projects, complex systems, client deliverables |

---

## Required Files per Tier

| File | T1 | T2 | T3 |
|------|----|----|-----|
| `README.md` | ✅ | ✅ | ✅ |
| `PLAN.md` | ✅ | ✅ | ✅ |
| `CHECKLIST.md` | ✅ | ✅ | ✅ |
| `SPEC.md` | ✅ | ✅ | ✅ |
| `ARCHITECTURE.md` | — | ✅ | ✅ |
| `FRONTEND_DESIGN.md` | — | — | ✅ |
| `DATAMODEL.md` | — | — | ✅ |

---

## Opt-in Rules

- Users may add optional files from **higher** tiers (e.g. T2 user adds `DATAMODEL.md`) — allowed.
- Users may add custom-named files at any tier — allowed.
- Custom files that use a **reserved filename** must conform to that file's standard in `references/file-standards.md`.
- Custom files that do **not** match a reserved filename may use any structure — but must not contradict other docs.
- Files cannot be selectively removed from a tier's required set unless the user explicitly confirms a downgrade.

---

## Reserved Filenames

These names are standardized. Any file using them must follow `references/file-standards.md`:

`README.md` `PLAN.md` `CHECKLIST.md` `SPEC.md` `ARCHITECTURE.md` `FRONTEND_DESIGN.md` `DATAMODEL.md` `DESIGN.md`

---

## Recommendation Logic

Base your tier recommendation on:

- "script", "tool", "quick", "simple", "personal" → suggest T1
- "app", "API", "service", "product", "web" → suggest T2
- "team", "client", "complex", "enterprise", "system", "platform" → suggest T3
- Presence of UI/design mentions → nudge toward T3 or T2+FRONTEND_DESIGN.md opt-in
- Presence of data/models/schema mentions → nudge toward T3 or T2+DATAMODEL.md opt-in

Always present your recommendation as a suggestion, not a decision.
