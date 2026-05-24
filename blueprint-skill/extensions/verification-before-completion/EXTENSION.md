---
name: verification-before-completion
version: remote
author: obra (superpowers)
type: remote
install: npx skills add https://github.com/obra/superpowers --skill verification-before-completion
conflicts: []
activation:
  keywords: [verify, verification, quality, testing, done, complete, checklist, review]
  always: true
---

## Summary

Enforces explicit verification gates before any task is marked complete. Prevents Agent from self-certifying work as done without running actual checks. When enabled, every CHECKLIST.md item gets a mandatory verification protocol: what to run, what output to expect, and who/what confirms it passed.

## Affects

- `CHECKLIST.md` — strengthens completion criteria with explicit verification steps
- `SPEC.md` — appends verification contract to every `#### Tests` section

## Inject Points

- `CHECKLIST.md` → every `- [ ]` task item (append verification gate)
- `SPEC.md` → every `#### Tests` block (append verification execution method)

## Notes

Not yet installed. Run install command above to fetch full content.
`activation.always: true` — this extension is suggested for every project regardless of keywords,
because verification discipline applies universally.
Pairs well with `subagent-driven-development` for multi-agent handoff verification.