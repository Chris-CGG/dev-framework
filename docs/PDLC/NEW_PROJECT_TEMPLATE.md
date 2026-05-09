# CLAUDE.md — [PROJECT NAME]

> **How to use this file:** Copy this template into a new repo as `CLAUDE.md`. Fill in the bracketed fields. Start at Phase 0. Do not skip phases.

---

## Project

- **Name:** [PROJECT NAME]
- **Owner:** [HUMAN NAME / TEAM]
- **Started:** [YYYY-MM-DD]
- **Repo:** [REPO URL]
- **Deployment target:** [GitHub Pages / Vercel / Netlify / Other]

## Problem statement

[One paragraph. What problem are we solving? For whom? Why does it matter?]

## User profile

- **Primary user:** [WHO]
- **Context:** [WHEN/WHERE they use it]
- **Constraints:** [Device, environment, attention, accessibility, etc.]
- **Mental health / wellbeing considerations:** [If applicable]

## Tech stack

- **Frontend:** [TBD]
- **Backend:** [TBD or N/A]
- **Data:** [TBD]
- **Hosting:** [TBD]
- **Other key dependencies:** [TBD]

Tech decisions are justified in `docs/TECH_DECISIONS.md`.

## Data classification

Identify regulated data classes that apply to this project. Tick all that apply:

- [ ] None — purely public data
- [ ] PII (general)
- [ ] PHI under HIPAA
- [ ] Payment data under PCI DSS
- [ ] CUI under NIST 800-171 / CMMC Level 2
- [ ] Other: [SPECIFY]

Applicable controls are documented in `docs/architecture.md` security section.

---

## Phase tracker

Tick the current phase. Only one phase is "in progress" at a time.

- [ ] Phase 0 — Discovery
- [ ] Phase 1 — Architecture
- [ ] Phase 2 — Foundation
- [ ] Phase 3 — Core Build
- [ ] Phase 4 — Hardening
- [ ] Phase 5 — Deployment
- [ ] Phase 6 — Iteration

Gate criteria for each phase live in `docs/PDLC/GATES.md`. Phase definitions live in `docs/PDLC/PHASES.md`.

---

## Non-negotiable rules (universal)

These apply to every project using this framework. Do not edit.

1. **Read this file at the start of every session.**
2. **Never skip a phase gate without an `[OVERRIDE]` from the human.**
3. **Commit after every working feature.** One feature, one commit, Conventional Commits message.
4. **No feature N+1 before feature N is committed and tested.**
5. **No hardcoded secrets, tokens, or credentials. Ever.**
6. **Test in target environment before committing.**
7. **Document as you build. A feature without docs is incomplete.**
8. **Surface security and privacy concerns even when not asked.**
9. **One change at a time during iteration.** Bundled drops are not allowed.
10. **No destructive operations as a shortcut.** Diagnose root causes; do not bypass safety checks.

## Project-specific rules

[Add rules unique to this project. Examples:]

- [e.g., "All timestamps stored in ISO-8601 UTC."]
- [e.g., "User-facing copy goes in `i18n/en.json`, never inline."]
- [e.g., "No external network calls from the client."]
- [Add as needed.]

---

## Session start reminder for Claude

At the start of every session, Claude must:

1. Read this `CLAUDE.md` file end to end.
2. Identify the current phase from the phase tracker above.
3. Review the last 3 commits.
4. Report back to the human:
   - Current phase
   - Last change made
   - Next action expected per the phase plan
5. Ask: *"Ready to proceed, or do you want to review first?"*

Claude does not write feature code until the human confirms.

---

## Gate checklist shortcuts

- **Phase 0 exit:** Can you describe the user's daily interaction in 3 sentences without naming a technology?
- **Phase 1 exit:** Can every data entity be named? Every component owned? Every dependency identified?
- **Phase 2 exit:** Can a new developer understand the structure in under 5 minutes from `README.md` alone?
- **Phase 3 exit:** Does the product solve the core problem from `DISCOVERY.md` without any additional features?
- **Phase 4 exit:** Would you be comfortable sharing this repo publicly right now?
- **Phase 5 exit:** Has a real user completed one full workflow end to end on the target device?
- **Phase 6:** No exit. Steady state.

Full checklists are in `docs/PDLC/GATES.md`.

---

## Mid-session feedback prefixes

Use these in the prompt to control Claude's behavior:

| Prefix | Meaning |
| --- | --- |
| `[FEEDBACK]` | Non-code instruction. Adjust behavior, do not edit files. |
| `[RULE]` | Add a permanent rule to this `CLAUDE.md`. |
| `[OVERRIDE]` | Consciously bypass a gate. Logged in `CHANGELOG.md`. |
| `[QUESTION]` | Ask without triggering action. |
| `[STOP]` | Halt immediately and wait for direction. |

---

## Compliance posture (fill in)

Tick the frameworks this project must conform to:

- [ ] ISO 27001
- [ ] ISO 9001
- [ ] NIST SP 800-171
- [ ] HIPAA
- [ ] PCI DSS
- [ ] CMMC Level 2
- [ ] NIST AI RMF
- [ ] Other: [SPECIFY]

Phase 4 hardening gate requires a signed checklist for each ticked framework.

---

## Override log

Any `[OVERRIDE]` issued by the human is logged here in addition to `CHANGELOG.md`.

| Date | Phase | Gate skipped | Justification | Human |
| --- | --- | --- | --- | --- |
| — | — | — | — | — |
