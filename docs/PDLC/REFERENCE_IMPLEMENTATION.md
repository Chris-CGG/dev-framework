# reference-app — Reference Implementation

This document is an honest record of how the **reference-app** project executed each phase of the PDLC. It is intentionally domain-neutral: the lessons here apply to any project type — a web app, a backend service, a CLI tool, a library, a mobile app, a data pipeline, a hardware integration, or anything else a builder might ship with Claude.

Treat it as a worked example, not a story about a specific product. The structure (per-phase: how we executed it, what we got right, what we should have done differently, artifacts) is the part to copy.

> **Replace this with your own record.** Copy this file into your project as `docs/REFERENCE_IMPLEMENTATION.md`, swap "reference-app" for your project name, and fill each phase with what actually happened — not what you wish had happened. Keep the structure. Keep the honesty.

---

## Phase 0 — Discovery

**How we executed it:** Mostly skipped formally. The core problem and the primary user flow were understood in the builder's head but not written down until Phase 4. No `DISCOVERY.md` was created at the time.

**What we got right:**
- The user was clear from day one. We could name them, their context, and the constraint that made the problem worth solving.
- Domain-specific constraints — whatever they were for the project (regulatory, accessibility, performance, environmental, behavioral) — were treated as first-class design inputs, not afterthoughts.
- The core insight came from a real lived problem, not a feature wishlist.

**What we should have done differently:**
- Written the discovery down. The cost of not writing it: assumptions drifted between sessions, and Claude could not reliably enforce scope without a written reference.
- Identified data classification (PII / PHI / payment data / CUI / none) at the start, not at hardening. Whatever framework applies — it shapes every later phase.

**Artifacts that exist:** None at the time of build. `DISCOVERY.md` reconstructed retroactively in Phase 4.

**Artifacts that are missing:** Original assumption list (the retroactive one is best-effort).

**Current phase status:** Closed retroactively.

---

## Phase 1 — Architecture

**How we executed it:** Partial. Component sketches existed mentally. The primary entity schema was strong from day one — single source of truth, the right call. ERD was not created until after core build.

**What we got right:**
- The primary entity as the single source of truth for the project's core data. Everything else referenced it.
- Configuration and data files separated from logic — easy to swap or version data without touching code.
- The key behavioral or domain constraint was baked into the architecture, not bolted on as a feature flag later.

**What we should have done differently:**
- Drawn the ERD before writing data-touching code. Secondary entities evolved during build, which created small refactors that a 30-minute up-front diagram would have prevented.
- Tech decisions were not justified in writing. They were good decisions; they just lacked the paper trail.

**Artifacts that exist:** `architecture.md` (retroactive), primary entity schema (original).

**Artifacts that are missing:** Original tech decisions justification document. `TECH_DECISIONS.md` reconstructed in Phase 4.

**Current phase status:** Closed retroactively.

---

## Phase 2 — Foundation

**How we executed it:** Folder structure and configuration files were correct from the start. `CLAUDE.md` was not created until build time, which meant the first few sessions had to re-establish context manually.

**What we got right:**
- Clean folder structure.
- Configuration / data files populated with correct schema from day one.
- Build and distribution scaffolding present early (whatever applied — manifest, `package.json`, `Dockerfile`, `Makefile`, `pyproject.toml`, etc.).

**What we should have done differently:**
- `CLAUDE.md` should have been the second file in the repo, after `README.md`. Without it, Claude's behavior was inconsistent across sessions.
- Commit convention was not formalized until mid-build, which shows in early commit messages.

**Artifacts that exist:** Folder structure, configuration files, build scaffolding.

**Artifacts that are missing:** Initial `CLAUDE.md` (created later). `init: project scaffold` commit was not the first commit — feature commits preceded it.

**Current phase status:** Closed retroactively.

---

## Phase 3 — Core Build

**How we executed it:** This is where the project actually started. The load-bearing primary features were built first, which validated the central hypothesis quickly. Commit discipline was inconsistent until enforced mid-project.

**What we got right:**
- Built the right thing first. The features that prove the core hypothesis are the load-bearing ones; everything else is decoration.
- The central technical hypothesis held up under real use. The work spent validating it early paid back many times over.
- Tested in target environment regularly — whichever environment that meant for this project (browser, terminal, container, device, runtime).

**What we should have done differently:**
- Committed more often and more cleanly. A few commits bundled multiple features and made it harder to bisect issues later.
- Started with at least a stub `CHANGELOG.md` to keep iteration visible from day one.

**Artifacts that exist:** Working MVP, feature commits (some bundled).

**Artifacts that are missing:** Clean per-feature commit history for the early features.

**Current phase status:** Complete.

---

## Phase 4 — Hardening

**How we executed it:** This phase did most of the documentation catch-up. README, ERD, `TECH_DECISIONS.md`, and `DISCOVERY.md` were all generated here. Security review caught one hardcoded value that should have been an environment variable.

**What we got right:**
- Honest about what was missing instead of papering over gaps.
- Generated diagrams from the current state of the code, not aspirational state.
- Added input validation and error handling systematically.

**What we should have done differently:**
- Most of this work belonged in earlier phases. Doing it all at once in Phase 4 was expensive — the cost of patching forward.
- Accessibility and usability review was lighter than it should have been. The standard was set; not all of it was verified.

**Artifacts that exist:** README, ERD, security checklist, error handling.

**Artifacts that are missing:** Full accessibility / usability audit report (project-type dependent).

**Current phase status:** Complete.

---

## Phase 5 — Deployment

**How we executed it:** Deployed to the target environment. Distribution and access were verified on the actual systems users would use. First real workflow completed end-to-end by the builder before anyone else touched it.

**What we got right:**
- Real-environment testing before declaring the deploy successful.
- Platform-specific gotchas were caught during real-environment testing (every platform has them — service worker scope on web, IAM and cold-start on serverless, packaging and signing on mobile, install paths on CLI tools, image size on containers).
- Backup, data export, and rollback paths verified.

**What we should have done differently:**
- Monitoring was minimal. Production logging would have helped diagnose the first user-reported bug faster.

**Artifacts that exist:** Live deployment, install / access confirmations, working data flow.

**Artifacts that are missing:** Production monitoring dashboard.

**Current phase status:** Complete.

---

## Phase 6 — Iteration

**How we executed it:** Ongoing. Weekly feedback cycle from real usage. Changes are small and tested before merge.

**What we got right:**
- Treating real-usage feedback as the priority signal.
- One change at a time. No bundled drops since the post-deploy stabilization.

**What we should have done differently:**
- `CHANGELOG.md` was started late. Versioning has been consistent since then.

**Current phase status:** In steady state.

---

## Retroactive Fixes Applied

When the project adopted this framework mid-flight, the following retroactive fixes were applied to bring earlier phase gates into compliance:

- **README created in Phase 4** instead of Phase 2.
- **ERD created after core build** instead of before.
- **Commit discipline enforced mid-project**, with a documented "from this commit forward" boundary.
- **`CLAUDE.md` created at build time, not discovery time.**
- **`DISCOVERY.md` reconstructed retroactively** with a clear note that it is reconstructed.
- **`TECH_DECISIONS.md` written retroactively** to capture choices that had already been made.
- **One hardcoded value migrated to environment variable** during Phase 4 security review.

These are documented as reconstructed / retroactive so future readers can distinguish original artifacts from catch-up artifacts.

---

## What This Project Does Right

These are the design choices that have held up under real use and are worth carrying forward to future projects. They are framed at a level that applies to any project type — pick the version of each that fits your domain:

- **Single source of truth for the primary entity.** All identity, configuration, or state for the project's core concept lives in one schema. Everything else references it. Refactors that touched the primary entity were small because the seam was clean.
- **Domain constraints baked into architecture, not bolted on.** When a constraint matters — regulatory, behavioral, performance, accessibility, environmental — it should be the entry condition for the relevant data flow, not a flag on a form or a check buried in a handler.
- **Configuration and data separated from logic.** Versioned independently. Updating a value or a reference dataset does not require a code change.
- **Primary user interaction designed first.** The first thing the user does (a command, a form, a request, an API call, a screen) sets the frame for everything else. Get that interaction right and the rest follows; get it wrong and every subsequent feature fights upstream.
- **Derived signals over raw inputs.** When the goal is to detect or react to a pattern, design the derivation early. Raw inputs are noisier than the signal you actually care about, regardless of domain.

These five choices are the reason the product is useful. The lessons in the rest of this document are about *how the build went*; these are about *what the build is*. Carry both forward.
