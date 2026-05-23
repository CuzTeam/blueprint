# Module: Alignment Interview

Run this interview **before writing any files**. Do not skip or abbreviate. The goal is to gather everything needed so no assumptions have to be made during file generation.

---

## Questions to Ask (in order)

### Q1 — Project Name
Ask for a project name. This becomes `<planname>` — the folder name and the identifier used across all docs.

Rules:
- Must be a single slug: lowercase, hyphens allowed, no spaces (e.g. `my-app`, `payment-service`)
- If the user gives a name with spaces, suggest a slugified version and confirm

### Q2 — Project Description
Ask for a brief description: what does it do, who uses it, why does it exist?

- One to three sentences is ideal
- This populates PLAN.md Overview and README.md description
- If vague, ask one follow-up: "Is this user-facing, internal tooling, or an API?"

### Q3 — Tier Selection
Present the tier table from `modules/tiers.md`. State your recommendation and why. Ask the user to confirm or choose a different tier.

> Example: "Based on your description, I'd recommend **T2 (Standard)** — it's a web app with backend logic but no design system yet. Does that work, or would you like T1 or T3?"

Do not proceed until the user confirms a tier.

### Q4 — Optional Add-ons
After tier is confirmed, ask:
- "Would you like to add any optional files from higher tiers?" (list what's available for their tier)
- "Do you need any custom files beyond the standard set?"

If they add a file with a reserved name, remind them: it must follow the standard in `references/file-standards.md`.
If they add a custom file, confirm the name won't cause confusion.

### Q5 — Existing Directory Check
Ask (or check silently if possible): does `/.docs/<planname>/` already exist?

- IF yes → warn the user: "This directory already exists. Do you want to overwrite, merge, or abort?"
- IF no → proceed

### Q6 — DESIGN.md Check
If `FRONTEND_DESIGN.md` is in scope (T3 or opted-in):
- Check if `DESIGN.md` already exists at `/.docs/<planname>/DESIGN.md`
- IF yes → confirm with user: "I found a DESIGN.md — I'll use it as the source for FRONTEND_DESIGN.md."
- IF no → note that you'll generate FRONTEND_DESIGN.md from context, and remind them they can drop one in later

---

## After Alignment

Summarize what you're about to generate:

```
Here's what I'll create at /.docs/<planname>/:

Tier: T2 (Standard)
Files:
  ✅ README.md
  ✅ PLAN.md
  ✅ SPEC.md
  ✅ CHECKLIST.md
  ✅ ARCHITECTURE.md
  ➕ DATAMODEL.md (opted in)

Shall I proceed?
```

Wait for confirmation before writing.

---

## Q3.5 — Extension Check (runs after Q3, before Q4)

Read `modules/extensions.md` fully, then scan the `extensions/` directory.

Present results inline during alignment — do not make the user ask about extensions separately.

After summarizing the pre-flight (Step: After Alignment), add an extensions block:

```
Extensions available:
  ✅ hop (embedded) — Human-Oriented Programming coding standards
  📦 vercel-react (not installed) — Vercel React/Next.js best practices

Would you like to enable any? For uninstalled ones, I can run the install command.
```

Follow the lifecycle defined in `modules/extensions.md` for install prompts and conflict resolution.
