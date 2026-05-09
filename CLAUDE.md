# CLAUDE.md — dev-framework

> This repository hosts the **Open Product Development Lifecycle Framework** (Open PDLC). It governs itself by its own framework. The full framework lives in `docs/PDLC/`.

---

## Project

- **Name:** dev-framework
- **Owner:** Chris (Chris-CGG)
- **Started:** 2026-05-08
- **Repo:** https://github.com/Chris-CGG/dev-framework.git
- **Deployment target:** N/A — documentation repository

## Problem statement

Solo developers and small teams building with Claude need a tight, repeatable protocol that balances creative freedom with engineering rigor. Without one, projects drift, documentation rots, and gates that should have been enforced get skipped silently. This repository defines that protocol once so it can be copied into every future project, with the reference-app build serving as the honest reference implementation.

## User profile

- **Primary user:** Solo developers and small teams using Claude as their engineering partner.
- **Context:** Starting a new project, recovering an in-flight project, or reviewing a finished one against a known protocol.
- **Constraints:** Must be technology-agnostic. Must support regulated environments (HIPAA, PCI, NIST 800-171, CMMC L2). Must be readable cold by a future builder who has never seen the project.
- **Mental health / wellbeing considerations:** N/A for the framework repo itself. The framework explicitly supports projects where these are first-class design constraints (see `REFERENCE_IMPLEMENTATION.md`).

## Tech stack

- **Format:** Markdown (CommonMark + GitHub-flavored Mermaid where used).
- **Hosting:** GitHub.
- **Tooling:** None required to consume; standard git workflow to maintain.

## Data classification

- [x] **None — purely public documentation.**
- [ ] PII (general)
- [ ] PHI under HIPAA
- [ ] Payment data under PCI DSS
- [ ] CUI under NIST 800-171 / CMMC Level 2

This repo contains no regulated data. The *projects that adopt this framework* may carry such data — the framework is built to support them.

---

## Phase tracker

- [ ] Phase 0 — Discovery
- [ ] Phase 1 — Architecture
- [ ] Phase 2 — Foundation
- [ ] Phase 3 — Core Build
- [ ] Phase 4 — Hardening
- [ ] Phase 5 — Deployment
- [x] Phase 6 — Iteration

v0.1.0 was published on 2026-05-08. The framework is now in steady-state iteration: changes happen in response to real-project feedback, one at a time, with `CHANGELOG.md` updated every time.

Gate criteria for each phase live in `docs/PDLC/GATES.md`. Phase definitions live in `docs/PDLC/PHASES.md`.

---

## Non-negotiable rules (universal)

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

- **The framework documents itself.** Any change to `docs/PDLC/*.md` must update `docs/PDLC/CHANGELOG.md` in the same commit.
- **Honesty over polish.** `REFERENCE_IMPLEMENTATION.md` documents what was skipped or patched. Future reference implementations follow the same pattern — do not rewrite history to look cleaner than it was.
- **Compliance references stay current.** When a referenced standard publishes a major revision (e.g., NIST 800-171 Rev. 3), update the framework rather than letting references drift.
- **Use Conventional Commits with the `pdlc` scope** for changes inside `docs/PDLC/` (e.g., `docs(pdlc): clarify Phase 1 gate`).
- **No emojis** in framework files unless explicitly requested.
- **Do not invent new phases.** If a real-world need surfaces, propose it in conversation, park it in a draft, and let it bake before adding to the canonical seven.

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

Claude does not write feature code (or, in this repo's case, content additions) until the human confirms.

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

| Prefix | Meaning |
| --- | --- |
| `[FEEDBACK]` | Non-code instruction. Adjust behavior, do not edit files. |
| `[RULE]` | Add a permanent rule to this `CLAUDE.md`. |
| `[OVERRIDE]` | Consciously bypass a gate. Logged in `CHANGELOG.md`. |
| `[QUESTION]` | Ask without triggering action. |
| `[STOP]` | Halt immediately and wait for direction. |

---

## Compliance posture

The framework itself is conformant to:

- [x] ISO 9001 (quality management — applies to the framework's documentation discipline)
- [x] NIST AI RMF (Claude participated in authoring this framework; the protocol explicitly maps to Govern / Map / Measure / Manage)
- [ ] ISO 27001 (no information assets in scope at the framework-repo level)
- [ ] NIST SP 800-171
- [ ] HIPAA
- [ ] PCI DSS
- [ ] CMMC Level 2

Projects that *adopt* this framework will tick the boxes that apply to them and carry their own Phase 4 compliance checklist.

---

## Override log

| Date | Phase | Gate skipped | Justification | Human |
| --- | --- | --- | --- | --- |
| — | — | — | — | — |
