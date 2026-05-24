# Module: Research Phase

Runs after Alignment, before writing any files. Ensures Agent arrives at document generation with comprehensive, multi-source knowledge rather than relying solely on built-in references.

---

## Search Capability Check

Before starting research:

```
IF Agent has web search capability (search tool, Firecrawl, browser, or equivalent)
  → Run Full Research (see below)
  → Do NOT skip this phase
ELSE
  → Run Degraded Research (see below)
  → Warn user: "⚠️ No search capability detected. Research will be limited to built-in
    references (WCAG, APCA, HIG). Results may miss project-specific standards,
    library docs, or recent best practices. Consider enabling web search."
```

**Full Research is mandatory when search is available. There are no exceptions.**

---

## Full Research Protocol

### Step 1 — Domain Inference

From the project description, tech stack (if known), and enabled extensions, derive a list of research domains. Be exhaustive — err on the side of more domains, not fewer.

Examples of domain inference:

| Project signal | Research domains to add |
|----------------|------------------------|
| Payment / checkout mentioned | PCI DSS, Stripe/payment provider docs, fraud patterns |
| Auth / login / user accounts | OWASP auth guidelines, OAuth 2.0 / OIDC specs |
| Healthcare / medical data | HIPAA, HL7 FHIR if applicable |
| React / Next.js in stack | React Server Components docs, Next.js App Router patterns, Vercel deployment constraints |
| Tailwind in stack | Tailwind v4 design tokens, utility-first constraints |
| Mobile / PWA | PWA checklist, iOS/Android viewport quirks |
| File uploads | MIME type security, size limits, virus scanning patterns |
| Real-time features | WebSocket vs SSE tradeoffs, connection management |
| i18n / localization | Unicode CLDR, RTL layout considerations |
| AI / LLM integration | Rate limiting, prompt injection risks, streaming UX |
| E-commerce | Accessibility for shopping flows, cart state management |
| HOP extension enabled | Verify HOP naming and structure patterns against current project language |

Always include regardless of project type:
- Current best practices for the detected tech stack
- Known security considerations for the feature set
- Accessibility implications specific to the UI patterns in scope

### Step 2 — Research Execution

For each domain, search and read. Do not summarize prematurely — read enough to actually understand the standard, not just confirm it exists.

```
FOR each domain in research list:
  1. Search for: "<domain> best practices <current year>"
     AND: "<domain> specification" or "<domain> official docs"
  2. Read at minimum 2 sources per domain
  3. IF sources conflict → note the conflict explicitly (see Step 3)
  4. IF a source is outdated (>2 years) → search for newer version
  5. Cross-reference: does this domain interact with another domain already researched?
     IF yes → note the interaction point
```

**Do not stop at the first result. Do not assume you know the answer before searching.**

### Step 3 — Conflict Detection and Resolution

When two sources, standards, or extensions contradict each other:

```
IF conflict is between a legal/compliance standard and a design preference
  → Legal/compliance wins, no user input needed. Note it.

IF conflict is between two design standards (e.g., HIG says X, Material says Y)
  → Note both positions, recommend the one better suited to project platform,
    present to user for confirmation

IF conflict is between an extension's injected rule and a core Blueprint rule
  → Core Blueprint rule wins (see modules/extensions.md core rules).
    Note the conflict in Research Brief.

IF conflict cannot be resolved by priority
  → Surface to user with both positions clearly stated. Do not silently pick one.
```

### Step 4 — Produce Research Brief

After all domains are researched, write a Research Brief to `/.docs/<planname>/.research/brief.md`.

This file is **internal** — it is Agent working memory, not a user-facing deliverable. It does not appear in README.md's Documentation Index.

```markdown
# Research Brief: <planname>
generated: <datetime>
search_capability: full | degraded

## Domains Researched

| Domain | Sources consulted | Key findings | Conflicts noted |
|--------|------------------|--------------|-----------------|
| ... | ... | ... | ... |

## Key Standards Applied

<!-- One section per major standard or finding that will affect document generation -->

### <Standard Name>
- Source: <url>
- Applies to: <which Blueprint files>
- Key rules: bullet list
- Conflicts with: <other standard if any> → Resolution: <how resolved>

## Conflicts Requiring User Input

<!-- Only conflicts that could not be auto-resolved -->
- [ ] Conflict: <description> → Options: A or B → Awaiting user decision

## Research Gaps

<!-- Domains where search returned insufficient results -->
- <domain>: insufficient sources found. Falling back to <built-in reference or inference>.

## Extensions Validated

<!-- Confirm extension content is consistent with research findings -->
- hop: consistent / inconsistent (note if inconsistent)
- <other ext>: consistent / inconsistent
```

### Step 5 — Resolve Open Conflicts with User

```
IF Research Brief has items in "Conflicts Requiring User Input"
  → Present each conflict clearly
  → Wait for user decision before proceeding
  → Record decision in brief.md
ELSE
  → Proceed to file writing
```

---

## Degraded Research Protocol

When no search capability is available:

1. Warn the user (see Search Capability Check above)
2. List the built-in references that will be used instead:
   - `references/accessibility/WCAG21.md`
   - `references/accessibility/APCA/`
   - `references/accessibility/HIG/`
   - Any enabled extension content
3. Note which domains have NO built-in coverage (e.g., framework-specific docs, compliance requirements)
4. Write a minimal Research Brief marking all entries as `source: built-in` or `source: inferred`
5. Proceed to file writing

---

## Research Brief Lifecycle

- **Created**: during Research Phase, before file writing
- **Read by**: write-order step (Agent reads brief before writing each file)
- **Updated**: if user resolves conflicts mid-session, update brief accordingly
- **On re-run**: if project already has a brief, check its `generated` date
  - IF brief is < 7 days old → ask user: "Existing research brief found. Re-research or reuse?"
  - IF brief is > 7 days old → automatically re-research and overwrite

---

## How Research Feeds Into File Generation

When writing each Blueprint file, Agent must:

1. Re-read the Research Brief before writing that file
2. Apply relevant findings to that file's content
3. Where a finding contradicts a Blueprint default, the finding wins (unless it violates a core rule)
4. Cite the source in a `<!-- research: <domain> -->` comment where a non-obvious standard is applied

Example in SPEC.md:
```markdown
#### Error Handling
- Invalid card number → HTTP 400, message: "Please check your card number"
<!-- research: PCI DSS — never echo back card digits in error messages -->
```