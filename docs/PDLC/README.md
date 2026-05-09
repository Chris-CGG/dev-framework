# Open Product Development Lifecycle Framework

**A repeatable protocol for human-AI collaborative builds**

---

## Overview

This framework was distilled from a real-world reference build — a small wellness PWA where a single builder collaborated with Claude to ship from problem statement to deployed application. The lessons, friction points, and recovery patterns from that build (preserved as **reference-app** in `REFERENCE_IMPLEMENTATION.md`) are codified here so they don't have to be re-learned on the next project.

It is designed for:

- **Solo developers** building with Claude as their engineering partner.
- **Small teams** who need a shared protocol without the overhead of enterprise SDLC tooling.
- **Builders who want creative freedom** but recognize that protocol prevents avoidable mistakes.

## Two layers

The framework is intentionally split into two layers:

1. **The process** — tight, repeatable, technology-agnostic. Lives in `PHASES.md`, `GATES.md`, `CLAUDE_PROTOCOL.md`, and `NEW_PROJECT_TEMPLATE.md`.
2. **The reference implementation** — how reference-app executed (or skipped) each phase, what worked, what didn't. Lives in `REFERENCE_IMPLEMENTATION.md`.

The process layer is meant to be copied into any new repo. The reference layer is a historical record — read it once for the lessons, then leave it.

## Core principles

- **Every phase has a gate.** You cannot proceed without passing it. Gates are not bureaucracy; they are the difference between a product that ships and a product that drifts.
- **Claude enforces protocol. Humans make creative decisions.** When the two collide, discuss — never silently skip protocol.
- **Documentation is part of the build, not a clean-up step.** A feature without docs is incomplete by definition.
- **One feature at a time.** No feature N+1 before N is committed and tested.
- **Commit discipline is non-negotiable.** Every working feature gets its own commit with a meaningful message.
- **Compliance is baked in, not bolted on.** Security, privacy, and quality reviews are gate criteria — not a Phase 4 surprise.

## Compliance posture

This framework is designed to operate in environments that require conformance with:

- **ISO 27001** (information security management)
- **ISO 9001** (quality management)
- **NIST SP 800-171** (controlled unclassified information)
- **HIPAA** (when health/wellness data is in scope)
- **PCI DSS** (when payment data is in scope)
- **CMMC Level 2** (controlled unclassified information for defense contractors)
- **NIST AI RMF** (AI risk management — relevant whenever Claude or another model is in the build loop)

Phase gates explicitly call out which controls are evaluated at each transition. See `GATES.md`.

## File map

| File | Purpose |
| --- | --- |
| `README.md` | This file. Framework overview. |
| `PHASES.md` | The 7 phases — entry, activities, deliverables, exit. |
| `GATES.md` | Phase gate checklists and what Claude refuses to do without them. |
| `CLAUDE_PROTOCOL.md` | How Claude behaves inside the framework. |
| `REFERENCE_IMPLEMENTATION.md` | Reference implementation: how reference-app did each phase. |
| `CHANGELOG.md` | Versioned record of changes to this framework. |
| `NEW_PROJECT_TEMPLATE.md` | Copy-paste starter for a new project. |

## How to use this framework on a new project

1. Copy `NEW_PROJECT_TEMPLATE.md` into the new repo root as `CLAUDE.md`.
2. Fill in the bracketed fields (project name, problem statement, user profile, tech stack).
3. Start at **Phase 0 — Discovery**. Do not skip.
4. At each phase boundary, run the checklist in `GATES.md`.
5. When in doubt, re-read `CLAUDE_PROTOCOL.md`.

## How to use it on an in-flight project

If you are mid-build when you adopt the framework (this is how reference-app adopted it):

1. Read `REFERENCE_IMPLEMENTATION.md` first — it documents this exact recovery pattern.
2. Identify the highest phase you have legitimately completed.
3. Run the gate checklist for that phase. Anything unchecked is a retroactive deliverable.
4. Catch up the gates before adding new features.
5. Resume forward motion only when the current phase gate is clean.

## A word on honesty

The reference implementation includes a list of things reference-app got wrong. This is intentional. A framework that pretends every project executed it perfectly is a framework no one trusts. The point of writing this down is so the next project can be honest with itself about where it actually is, and what it actually skipped.
