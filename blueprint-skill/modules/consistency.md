# Module: Consistency Check

Run this check **after all files are written**, before presenting results to the user. Fix any failures before outputting.

---

## Checklist

### Cross-file Integrity

- [ ] Every feature `##` in SPEC.md has at least one corresponding entry in CHECKLIST.md
- [ ] Every CHECKLIST entry's `→ SPEC.md#anchor` points to a heading that actually exists
- [ ] PLAN.md Non-Goals do not appear as features in SPEC.md (if they do, either remove from SPEC or remove from Non-Goals)
- [ ] No file contradicts another on any factual claim (API paths, field names, user flows)

### ARCHITECTURE.md (if present)

- [ ] Every component defined in ARCHITECTURE.md appears in at least one SPEC.md feature or sub-feature
- [ ] Directory structure in ARCHITECTURE.md includes the `/.docs/<planname>/` folder itself
- [ ] All API endpoints in ARCHITECTURE.md have a corresponding error-handling block in SPEC.md

### DATAMODEL.md (if present)

- [ ] Every model field referenced in SPEC.md IF/ELIF/ELSE logic exists in DATAMODEL.md
- [ ] Enum values used in SPEC.md match DATAMODEL.md enum definitions
- [ ] ARCHITECTURE.md database layer matches tech stack used in DATAMODEL.md (if both present)

### FRONTEND_DESIGN.md (if present)

- [ ] Every page/route in FRONTEND_DESIGN.md corresponds to a feature in SPEC.md
- [ ] No design decision in FRONTEND_DESIGN.md contradicts DESIGN.md (if DESIGN.md was used as source)
- [ ] FRONTEND_DESIGN.md accessibility section references WCAG 2.1 AA as minimum standard

### SPEC.md Internal Consistency

- [ ] Every `###` sub-feature has a `#### Tests` section
- [ ] Every `#### Tests` section has at least one test per logical branch (one per IF/ELIF/ELSE)
- [ ] Every error branch specifies: error type + HTTP status code + user-facing message
- [ ] No feature in SPEC.md is described without at least one IF/ELIF/ELSE or explicit single-path behavior

---

## On Failure

For each failed check:
1. Identify the specific inconsistency
2. Determine which file is the "source of truth" (PLAN > SPEC > others)
3. Update the dependent file to match
4. Re-run only the affected checks after fixing

Do not present results to the user until all checks pass.
