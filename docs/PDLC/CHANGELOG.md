# Changelog

All notable changes to the **CxMxC PDLC Framework** are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Added
- Top-level `README.md` orienting new builders to the repo: what it is, what's inside, three quickstart paths (new project / in-flight project / review of a finished project), the five mid-session prefixes, compliance posture, and contribution rules.

---

## [0.1.0] — 2026-05-08

Initial release of the CxMxC Product Development Lifecycle framework, seeded from the cxmxc-training reference implementation.

### Added
- `README.md` — framework overview, two-layer model, compliance posture, file map.
- `PHASES.md` — full definitions for Phases 0 through 6 (Discovery, Architecture, Foundation, Core Build, Hardening, Deployment, Iteration), each with objective, entry criteria, activities, role definitions, deliverables, exit gate, and reference implementation notes.
- `GATES.md` — phase-by-phase gate checklists, gate-failure guidance, and the list of actions Claude refuses to take when gates have not been passed.
- `CLAUDE_PROTOCOL.md` — definition of Claude's role inside the framework: creative-vs-protocol split, always-do/never-do lists, mid-session feedback prefixes (`[FEEDBACK]`, `[RULE]`, `[OVERRIDE]`, `[QUESTION]`, `[STOP]`), session start protocol, and NIST AI RMF mapping.
- `CXMXC_REFERENCE.md` — honest record of how the cxmxc-training project executed (and patched) each phase, including retroactive fixes and what the project does right.
- `NEW_PROJECT_TEMPLATE.md` — copy-paste starter `CLAUDE.md` for any new project, with phase tracker, non-negotiable rules, and session-start reminder.
- `CHANGELOG.md` — this file.

### Compliance
- Framework explicitly references conformance considerations for ISO 27001, ISO 9001, NIST SP 800-171, HIPAA, PCI DSS, CMMC Level 2, and NIST AI RMF.
- Phase 1 and Phase 4 gates require security and privacy artifacts; Phase 4 requires a signed compliance checklist.

### Notes
- This release codifies the protocol that emerged during the cxmxc-training build. Lessons from that project are preserved in `CXMXC_REFERENCE.md` rather than being smoothed over.
