# dev-framework

**A reusable Product Development Lifecycle (PDLC) framework for human-AI collaborative builds.**

This repository is the canonical home of the **Open PDLC** — a tight, repeatable, technology-agnostic protocol for shipping software with Claude as your engineering partner. It is designed to be copied into any new project, applied to any in-flight project, and reviewed against any finished project.

---

## Why this exists

Solo developers and small teams move fast with Claude. That is the upside. The downside is that without a protocol, projects drift: gates get skipped silently, documentation rots, scope creeps, security review gets pushed to "later." This framework is the protocol that prevents those failure modes — codified once, copied everywhere.

It was distilled from a real reference build — preserved here under the neutral name **reference-app**, with all domain specifics stripped. The lessons (good and bad) from that build are recorded in `docs/PDLC/REFERENCE_IMPLEMENTATION.md` at a level that applies to any project type: web app, backend service, CLI tool, library, mobile app, data pipeline, or anything else a builder might ship with Claude.

---

## What's in the box

```
dev-framework/
├── README.md                       <- you are here
├── CLAUDE.md                       <- governs this repo by its own framework
└── docs/
    └── PDLC/
        ├── README.md               <- framework overview, two-layer model
        ├── PHASES.md               <- the 7 phases (Discovery → Iteration)
        ├── GATES.md                <- exit checklists + what Claude refuses without them
        ├── CLAUDE_PROTOCOL.md      <- how Claude behaves inside the framework
        ├── REFERENCE_IMPLEMENTATION.md  <- honest record of the reference build (reference-app)
        ├── CHANGELOG.md            <- versioned history of the framework itself
        └── NEW_PROJECT_TEMPLATE.md <- copy-paste CLAUDE.md for new projects
```

## The 7 phases at a glance

| # | Phase | Exit gate (one-liner) |
|---|-------|----------------------|
| 0 | **Discovery** | Describe the user's daily interaction in 3 sentences without naming a technology. |
| 1 | **Architecture** | Every entity named, every component owned, every dependency identified. |
| 2 | **Foundation** | A new dev understands the structure in under 5 minutes from `README.md` alone. |
| 3 | **Core Build** | Product solves the problem in `DISCOVERY.md` with no extra features. |
| 4 | **Hardening** | You'd be comfortable making the repo public right now. |
| 5 | **Deployment** | A real user has completed one full workflow end-to-end on the target device. |
| 6 | **Iteration** | No exit. Steady state. |

Full definitions in [`docs/PDLC/PHASES.md`](./docs/PDLC/PHASES.md). Full gate checklists in [`docs/PDLC/GATES.md`](./docs/PDLC/GATES.md).

---

## Quickstart — starting a new project

```bash
# 1. Create your new project repo
mkdir my-new-project && cd my-new-project && git init

# 2. Copy the template into it as CLAUDE.md
curl -fsSL https://raw.githubusercontent.com/Chris-CGG/dev-framework/main/docs/PDLC/NEW_PROJECT_TEMPLATE.md > CLAUDE.md

# 3. Open CLAUDE.md, fill in the bracketed fields, tick the compliance boxes that apply
# 4. Start at Phase 0 — Discovery. Do not skip phases.
```

If you prefer not to fetch over the network, clone this repo and copy the file manually:

```bash
git clone https://github.com/Chris-CGG/dev-framework.git
cp dev-framework/docs/PDLC/NEW_PROJECT_TEMPLATE.md my-new-project/CLAUDE.md
```

When Claude joins your next session, the first thing it will do is read `CLAUDE.md`, identify the current phase, and ask whether to proceed. That is the protocol working.

## Quickstart — adopting the framework on an in-flight project

This is how reference-app adopted the framework. It works.

1. Read [`docs/PDLC/REFERENCE_IMPLEMENTATION.md`](./docs/PDLC/REFERENCE_IMPLEMENTATION.md) — it documents this exact recovery pattern.
2. Identify the highest phase you have *legitimately* completed (be honest).
3. Copy `NEW_PROJECT_TEMPLATE.md` to your project root as `CLAUDE.md`. Tick the corresponding box on the phase tracker.
4. Run the gate checklist in `docs/PDLC/GATES.md` for that phase. Anything unchecked is a retroactive deliverable — finish those before adding new features.
5. Resume forward motion only when the current phase gate is clean.

## Quickstart — reviewing a finished project against this framework

1. Pick a phase (usually Phase 4 — Hardening — for a "ship-ready" check).
2. Open the gate checklist in `docs/PDLC/GATES.md`.
3. Walk the project against the boxes. Each unchecked box is a finding.
4. Findings get triaged into either *block-the-release* or *iteration backlog*.

---

## Working with Claude inside this framework

Five mid-session prefixes give you precise control. Use them in your prompt:

| Prefix | What it does |
|--------|--------------|
| `[FEEDBACK]` | Adjust behavior. No file edits. |
| `[RULE]` | Add a permanent rule to `CLAUDE.md`. |
| `[OVERRIDE]` | Skip a gate consciously. Logged in `CHANGELOG.md`. |
| `[QUESTION]` | Ask without triggering action. |
| `[STOP]` | Halt immediately and wait. |

Full protocol — including what Claude will always do, will never do, and how it handles things going wrong — lives in [`docs/PDLC/CLAUDE_PROTOCOL.md`](./docs/PDLC/CLAUDE_PROTOCOL.md).

---

## Compliance

The framework is designed to operate inside organizations that require conformance with one or more of:

- **ISO 27001** — information security management
- **ISO 9001** — quality management
- **NIST SP 800-171** — controlled unclassified information
- **HIPAA** — protected health information
- **PCI DSS** — payment card data
- **CMMC Level 2** — defense supply chain
- **NIST AI RMF** — AI risk management (always relevant when Claude is in the build loop)

Phase gates explicitly call out which controls are evaluated at each transition. Phase 4 (Hardening) requires a signed compliance checklist before deployment is permitted. See [`docs/PDLC/GATES.md`](./docs/PDLC/GATES.md) for the gate-level mapping and [`docs/PDLC/CLAUDE_PROTOCOL.md`](./docs/PDLC/CLAUDE_PROTOCOL.md) §7 for the NIST AI RMF mapping specifically.

---

## Contributing changes to the framework

This repo governs itself by its own framework. It is currently in **Phase 6 — Iteration**.

Rules for changing the framework itself:

1. One change per commit. Use the `pdlc` Conventional Commits scope: `docs(pdlc): clarify Phase 1 gate`.
2. Every change to `docs/PDLC/*.md` must update `docs/PDLC/CHANGELOG.md` in the same commit.
3. Do not invent new phases. If you have a real-world need, propose it in conversation, park it as a draft, and let it bake before adding to the canonical seven.
4. Honesty over polish. The reference implementation documents what was skipped and patched — future references should follow the same pattern.
5. When a referenced standard publishes a major revision (e.g., NIST 800-171 Rev. 3), update the framework rather than letting references drift.

Full project rules in [`CLAUDE.md`](./CLAUDE.md).

---

## Versioning

The framework follows [Semantic Versioning](https://semver.org/). Current version: **v0.1.0** (released 2026-05-08). Full history in [`docs/PDLC/CHANGELOG.md`](./docs/PDLC/CHANGELOG.md).

## License

No license file is currently committed. Treat the contents as "all rights reserved" until a license is added. If you want to use this framework on a project, copy the documents and apply your own license to your project — the framework is meant to live inside your repo, not be linked from it.

## Where to start reading

- New here and starting a project? → [`docs/PDLC/NEW_PROJECT_TEMPLATE.md`](./docs/PDLC/NEW_PROJECT_TEMPLATE.md)
- Want the framework's rationale? → [`docs/PDLC/README.md`](./docs/PDLC/README.md)
- Want to understand what each phase does? → [`docs/PDLC/PHASES.md`](./docs/PDLC/PHASES.md)
- Want to know how Claude behaves? → [`docs/PDLC/CLAUDE_PROTOCOL.md`](./docs/PDLC/CLAUDE_PROTOCOL.md)
- Want a real-world example, warts and all? → [`docs/PDLC/REFERENCE_IMPLEMENTATION.md`](./docs/PDLC/REFERENCE_IMPLEMENTATION.md)
