# Changelog

All notable changes to the **Open PDLC Framework** are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Changed
- **Renamed framework from "CxMxC PDLC Framework" to "Open PDLC Framework"** to remove personal-initial branding and present a neutral, universally adoptable identity. Full name is now "Open Product Development Lifecycle Framework."
- Renamed `CXMXC_REFERENCE.md` → `REFERENCE_IMPLEMENTATION.md` and replaced project-specific identifiers (athlete profile, mood gate, stability score, burst-crash detection, training device) with neutral placeholders (user profile, state gate, primary derived metric, anomaly detection, target device). Reference project is now called **reference-app**.
- **Stripped remaining domain-flavored language** (wellness, PWA-only framing, check-in, state-gate, mood) from `REFERENCE_IMPLEMENTATION.md`, `PHASES.md` Phase 5 activities/role/deliverables, `PHASES.md` Phase 2 build-scaffolding activity, `GATES.md` Phase 2 and Phase 5 gate items, `README.md` (root and `docs/PDLC/`), and `CLAUDE.md`. The framework and reference now read as project-type-agnostic — equally applicable to web apps, backend services, CLI tools, libraries, mobile apps, data pipelines, and other project types.
- Phase 2 / Phase 5 examples now enumerate multiple project types (PWA, container, CLI, mobile, package, etc.) instead of leading with one.
- "What This Project Does Right" lessons in `REFERENCE_IMPLEMENTATION.md` reframed at a level that applies to any domain (e.g., "Domain constraints baked into architecture, not bolted on" replaces "Wellbeing considerations baked into architecture").
- Updated all framework files to use the new name and reference identifier.

### Added
- Top-level `README.md` orienting new builders to the repo: what it is, what's inside, three quickstart paths (new project / in-flight project / review of a finished project), the five mid-session prefixes, compliance posture, and contribution rules.

---

## [0.1.0] — 2026-05-08

Initial release of the framework (originally published as "CxMxC PDLC Framework"; renamed to "Open PDLC Framework" in the Unreleased entry above), seeded from the reference-app implementation.

### Added
- `README.md` — framework overview, two-layer model, compliance posture, file map.
- `PHASES.md` — full definitions for Phases 0 through 6 (Discovery, Architecture, Foundation, Core Build, Hardening, Deployment, Iteration), each with objective, entry criteria, activities, role definitions, deliverables, exit gate, and reference implementation notes.
- `GATES.md` — phase-by-phase gate checklists, gate-failure guidance, and the list of actions Claude refuses to take when gates have not been passed.
- `CLAUDE_PROTOCOL.md` — definition of Claude's role inside the framework: creative-vs-protocol split, always-do/never-do lists, mid-session feedback prefixes (`[FEEDBACK]`, `[RULE]`, `[OVERRIDE]`, `[QUESTION]`, `[STOP]`), session start protocol, and NIST AI RMF mapping.
- `REFERENCE_IMPLEMENTATION.md` — honest record of how the reference-app project executed (and patched) each phase, including retroactive fixes and what the project does right.
- `NEW_PROJECT_TEMPLATE.md` — copy-paste starter `CLAUDE.md` for any new project, with phase tracker, non-negotiable rules, and session-start reminder.
- `CHANGELOG.md` — this file.

### Compliance
- Framework explicitly references conformance considerations for ISO 27001, ISO 9001, NIST SP 800-171, HIPAA, PCI DSS, CMMC Level 2, and NIST AI RMF.
- Phase 1 and Phase 4 gates require security and privacy artifacts; Phase 4 requires a signed compliance checklist.

### Notes
- This release codifies the protocol that emerged during the reference-app build. Lessons from that project are preserved in `REFERENCE_IMPLEMENTATION.md` rather than being smoothed over.
