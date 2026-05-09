# cxmxc-training Reference Implementation

This document is an honest record of how the **cxmxc-training** project executed each phase of the PDLC. It includes what was done well, what was skipped, and what had to be patched retroactively. It is not a success story — it is a working record. The point is so the next project can be honest with itself about where it actually is.

---

## Phase 0 — Discovery

**How we executed it:** Mostly skipped formally. The problem was understood in the builder's head — burst-crash detection in athlete training data, with mood-gated check-ins to avoid forcing inputs during low-state days. No `DISCOVERY.md` was created at the time.

**What we got right:**
- The user was clear from day one (the builder, an athlete logging their own training).
- Mental health considerations were a first-class design constraint, not an afterthought.
- The "mood gate" concept came from a real lived constraint, not a feature wishlist.

**What we should have done differently:**
- Written the discovery down. The cost of not writing it: assumptions drifted between sessions, and Claude could not reliably enforce scope without a written reference.
- Identified data classification (wellness data borders on PHI under HIPAA depending on how it's shared) at the start, not at hardening.

**Artifacts that exist:** None at the time of build. `DISCOVERY.md` reconstructed retroactively in Phase 4.

**Artifacts that are missing:** Original assumption list (the retroactive one is best-effort).

**Current phase status:** Closed retroactively.

---

## Phase 1 — Architecture

**How we executed it:** Partial. Component sketches existed mentally. Athlete profile schema was strong from day one — single source of truth, the right call. ERD was not created until after core build.

**What we got right:**
- Athlete profile as the single source of truth for identity, baseline metrics, and preferences.
- Data files separated from logic — easy to swap or version data without touching code.
- Mood gate baked into the architecture, not bolted on.

**What we should have done differently:**
- Drawn the ERD before writing data-touching code. Mood and check-in entities evolved during build, which created small refactors that a 30-minute up-front diagram would have prevented.
- Tech decisions were not justified in writing. They were good decisions; they just lacked the paper trail.

**Artifacts that exist:** `architecture.md` (retroactive), athlete profile schema (original).

**Artifacts that are missing:** Original tech decisions justification document. `TECH_DECISIONS.md` reconstructed in Phase 4.

**Current phase status:** Closed retroactively.

---

## Phase 2 — Foundation

**How we executed it:** Folder structure and data files were correct from the start. `CLAUDE.md` was not created until build time, which meant the first few sessions had to re-establish context manually.

**What we got right:**
- Clean folder structure.
- Data files populated with correct schema from day one.
- PWA manifest and service worker present early.

**What we should have done differently:**
- `CLAUDE.md` should have been the second file in the repo, after `README.md`. Without it, Claude's behavior was inconsistent across sessions.
- Commit convention was not formalized until mid-build, which shows in early commit messages.

**Artifacts that exist:** Folder structure, data files, PWA shell.

**Artifacts that are missing:** Initial `CLAUDE.md` (created later). `init: project scaffold` commit was not the first commit — feature commits preceded it.

**Current phase status:** Closed retroactively.

---

## Phase 3 — Core Build

**How we executed it:** This is where the project actually started. Mood gate and stability score were built first, which validated the central hypothesis quickly. Commit discipline was inconsistent until enforced mid-project.

**What we got right:**
- Built the right thing first. Mood gate and stability score are the load-bearing UX features; everything else is decoration.
- Stability score as burst-crash detection — the original insight held up under real data.
- Tested in target environment (mobile browser, PWA-installed) regularly.

**What we should have done differently:**
- Committed more often and more cleanly. A few commits bundled multiple features and made it harder to bisect issues later.
- Started with at least a stub `CHANGELOG.md` to keep iteration visible from day one.

**Artifacts that exist:** Working MVP, feature commits (some bundled).

**Artifacts that are missing:** Clean per-feature commit history for the early features.

**Current phase status:** Complete.

---

## Phase 4 — Hardening

**How we executed it:** This phase did most of the documentation catch-up. README, ERD, `TECH_DECISIONS.md`, and `DISCOVERY.md` were all generated here. Security review caught one hardcoded value that should have been an env var.

**What we got right:**
- Honest about what was missing instead of papering over gaps.
- Generated diagrams from current state of the code, not aspirational state.
- Added input validation and error handling systematically.

**What we should have done differently:**
- Most of this work belonged in earlier phases. Doing it all at once in Phase 4 was expensive — the cost of patching forward.
- Accessibility review was lighter than it should have been. WCAG 2.2 AA target was set but not fully verified.

**Artifacts that exist:** README, ERD, security checklist, error handling.

**Artifacts that are missing:** Full WCAG audit report.

**Current phase status:** Complete.

---

## Phase 5 — Deployment

**How we executed it:** Deployed to GitHub Pages. PWA install verified on iOS and Android. First real check-in completed by the builder on their training device.

**What we got right:**
- Real-device testing before declaring deploy successful.
- Service worker scope was correct (one of the things that bites GitHub Pages PWAs).
- Backup path verified — data export works.

**What we should have done differently:**
- Monitoring was minimal. Production logging would have helped diagnose the first user-reported bug faster.

**Artifacts that exist:** Live URL, install confirmations, working data flow.

**Artifacts that are missing:** Production monitoring dashboard.

**Current phase status:** Complete.

---

## Phase 6 — Iteration

**How we executed it:** Ongoing. Weekly feedback cycle from the builder's own training data. Changes are small and tested before merge.

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
- **One hardcoded value migrated to env var** during Phase 4 security review.

These are documented as reconstructed/retroactive so future readers can distinguish original artifacts from catch-up artifacts.

---

## What This Project Does Right

These are the design choices that have held up under real use and are worth carrying forward to future projects:

- **Athlete profile as single source of truth.** All identity, baseline, and preference data lives in one schema. Everything else references it. Refactors that touched profile shape were small because the seam was clean.
- **Mental health considerations baked into architecture.** The mood gate is not a feature flag bolted onto a check-in form — it is the entry condition for the data flow. Low-state days do not force inputs.
- **Data files separate from logic.** JSON data files are versioned independently of code. Updating training programs or reference values does not require a code change.
- **Mood gate as primary UX driver.** The first interaction every day is "how are you?" — and the rest of the UX adapts from there. This is correct for the user and correct for the data quality.
- **Stability score as burst-crash detection.** The central hypothesis — that a rolling stability metric catches dangerous training patterns earlier than a raw load number — has been validated against real training data. Worth the engineering investment.

These five choices are the reason the product is useful. The lessons in the rest of this document are about *how the build went*; these are about *what the build is*. Carry both forward.
