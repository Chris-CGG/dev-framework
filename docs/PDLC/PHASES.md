# PDLC Phases

Seven phases. Each has an objective, entry criteria, activities, role definitions, deliverables, and an exit gate. Reference implementation rows describe how **cxmxc-training** executed (or, in some cases, retroactively patched) the phase.

---

## Phase 0 — Discovery

**Objective:** Understand the problem deeply before writing a line of code.

**Entry criteria:** A problem statement exists.

**Activities:**
- Stakeholder interview (even if stakeholder = builder).
- Define the user, their context, and their constraints.
- Define mental health / wellbeing considerations if applicable.
- Identify data sources and integrations needed.
- Define success metrics.
- Document assumptions explicitly.
- Identify any regulated data classes (PHI, PII, CUI, payment data) up front — they shape every later phase.

**Claude's role:** Ask questions. Challenge assumptions. **Never suggest solutions yet.** When the human starts proposing implementations, redirect to the problem.

**Human's role:** Answer honestly. Resist jumping to solutions. Name the user even if it is yourself.

**Deliverables:**
- `DISCOVERY.md` containing: problem statement, user profile, constraints, success metrics, and a numbered assumptions list.
- Data classification note: which regulated frameworks (HIPAA / PCI / NIST 800-171 / etc.) apply.

**Exit gate:** Can you describe the user's daily interaction with the product in 3 sentences without mentioning technology?

**Reference implementation (cxmxc-training):** Skipped formally. The problem ("burst-crash detection in athlete training data with mood-gated check-ins") was understood in the builder's head but not written down until Phase 4. Retroactively reconstructed in `DISCOVERY.md`. **Lesson: even solo builders need this artifact — future-you is a different stakeholder.**

---

## Phase 1 — Architecture

**Objective:** Design the system before building it.

**Entry criteria:** `DISCOVERY.md` approved.

**Activities:**
- Define data entities and relationships (ERD).
- Define component architecture.
- Define state management approach.
- Define API and integration contracts.
- Define technology stack with justification for each choice.
- Define security and privacy considerations (auth, data-at-rest, data-in-transit, key management, access control, audit logging).
- Create Mermaid diagrams for all of the above.
- Map data flows to relevant compliance controls (HIPAA, NIST 800-171, ISO 27001 Annex A).

**Claude's role:** Enforce architecture completeness. Flag missing considerations (especially security, privacy, and AI risk surfaces). Generate Mermaid diagrams from the human's descriptions.

**Human's role:** Make stack decisions. Approve architecture. Own the tradeoffs.

**Deliverables:**
- `architecture.md` with all Mermaid diagrams (system, component, sequence, deployment).
- `DATA_SCHEMA.md` with entities, fields, types, and sensitivity classifications.
- `TECH_DECISIONS.md` with a justification for each technology choice (one paragraph minimum per decision, including alternatives considered).

**Exit gate:**
- Can every data entity be named?
- Does every component have a clear owner?
- Are all external dependencies identified?
- Is every sensitive data field tagged with its classification and the control protecting it?

**Reference implementation (cxmxc-training):** Partially executed. Component sketches existed; ERD did not. Athlete profile schema was strong from day one (single source of truth — got that right), but mood/check-in entities evolved during build. ERD was generated retroactively in Phase 4.

---

## Phase 2 — Foundation

**Objective:** Build the skeleton, not the features.

**Entry criteria:** Architecture approved.

**Activities:**
- Repo setup with proper folder structure.
- `CLAUDE.md` with project rules and context.
- Base data files (JSON schemas populated).
- PWA manifest and service worker if applicable.
- CI/CD pipeline if applicable.
- Commit convention established (Conventional Commits recommended).
- README shell created (sections present, content TBD).
- Secrets handling established (`.env.example`, `.gitignore`, no committed secrets).
- Dependency baseline pinned and recorded.

**Claude's role:** Generate scaffolding. Enforce naming conventions. Flag missing files. Refuse to write feature code until this phase is closed.

**Human's role:** Review structure. Approve before any feature work.

**Deliverables:**
- Clean repo with all folders and empty files in place.
- `CLAUDE.md` complete.
- All data files with correct schema.
- First commit: `init: project scaffold`.
- Passing structure validation (lint runs, build succeeds against empty implementations).

**Exit gate:** Can a new developer understand the project structure in under 5 minutes from `README.md` alone?

**Reference implementation (cxmxc-training):** `CLAUDE.md` was created at build time, not foundation time. Folder structure was sound. Data files were populated correctly from day one. Retrofitted: README written in Phase 4.

---

## Phase 3 — Core Build

**Objective:** Build the minimum viable product.

**Entry criteria:** Foundation complete and committed.

**Activities:**
- Build features in priority order.
- One feature at a time.
- Commit after every working feature.
- Test in target environment before committing.
- No premature optimization.
- Document as you build (inline where non-obvious; `docs/` for cross-cutting concerns).
- Log security-relevant events in any code path that touches sensitive data.

**Claude's role:**
- Write code.
- Enforce commit discipline.
- Flag scope creep immediately.
- **Never build feature N+1 before N is committed.**
- Surface security or privacy issues even when not asked.

**Human's role:** Define feature priority. Test each feature. Approve before moving on.

**Deliverables:**
- All MVP features working.
- Every feature committed with a proper message.
- Tested in target environment (browser, mobile, etc.).

**Exit gate:** Does the product solve the core problem stated in `DISCOVERY.md` **without any additional features**?

**Reference implementation (cxmxc-training):** This phase ran ahead of Phase 1 in places. Mood gate and stability score were the right first features to build (they validated the central hypothesis). Commit discipline was inconsistent until enforced mid-project.

---

## Phase 4 — Hardening

**Objective:** Make it robust, documented, and production-ready.

**Entry criteria:** MVP complete.

**Activities:**
- Error handling for all user inputs.
- Edge case testing.
- Performance review.
- Security review: API keys, data exposure, auth flows, dependency CVEs, OWASP Top 10.
- Privacy review: data minimization, retention, consent, regulated-data handling.
- Accessibility review (WCAG 2.2 AA target).
- Complete all documentation.
- Fill `README.md` completely.
- Generate all architecture diagrams.
- Schema documentation complete.
- Compliance checklist run against applicable frameworks (ISO 27001 Annex A, NIST 800-171 controls, HIPAA Security Rule, PCI DSS, CMMC L2, NIST AI RMF Govern/Map/Measure/Manage).

**Claude's role:**
- Audit code for missing error handling.
- Generate documentation.
- Run the security checklist.
- Enforce no-merge-without-docs.

**Human's role:** Test edge cases manually. Review all documentation for accuracy. Sign off on the compliance checklist.

**Deliverables:**
- Complete `README.md`.
- All Mermaid diagrams generated and embedded.
- Error handling on all inputs.
- Security checklist passed.
- No console errors in production build.
- Compliance checklist signed.

**Exit gate:** Would you be comfortable sharing this repo publicly right now?

**Reference implementation (cxmxc-training):** This phase did most of the documentation catch-up work. README, ERD, and tech decisions doc were all generated here instead of earlier phases. Security review caught one hardcoded value that should have been an env var.

---

## Phase 5 — Deployment

**Objective:** Get it in front of real users in real conditions.

**Entry criteria:** Hardening complete.

**Activities:**
- Choose deployment target (GitHub Pages, Vercel, Netlify, etc.).
- Environment variable management.
- PWA install testing on target devices.
- Performance testing on real hardware (not just dev machine).
- First real user session.
- Feedback collection setup.
- Production logging and monitoring configured.
- Backup / data export path verified.

**Claude's role:** Generate deployment configs. Flag environment-specific issues (path differences, CORS, service worker scope). Verify PWA manifest and service worker.

**Human's role:** Execute deployment. Test on real device. Collect first real feedback.

**Deliverables:**
- Live deployment URL.
- Successful PWA install on target device.
- First real check-in or data entry completed.
- Monitoring confirmed receiving events.

**Exit gate:** Has a real user completed one full workflow end to end on the target device?

**Reference implementation (cxmxc-training):** GitHub Pages target. PWA install verified on iOS and Android. First real check-in completed by the builder on their training device.

---

## Phase 6 — Iteration

**Objective:** Improve based on real usage data.

**Entry criteria:** Successful deployment with real user data.

**Activities:**
- Daily or weekly feedback review.
- Prioritize issues by user impact.
- One change at a time.
- Regression test after every change.
- Update documentation with every feature change.
- Version bump on significant changes (semver).
- Re-run security and compliance checks on any change that touches auth, data, or third-party integrations.

**Claude's role:** Implement changes. Enforce regression testing. Flag when a change breaks existing behavior. Maintain `CHANGELOG.md`.

**Human's role:** Prioritize feedback. Approve changes. Test regressions manually.

**Deliverables:**
- `CHANGELOG.md` maintained.
- Version history in `package.json` (or equivalent).
- All changes documented.
- No undocumented breaking changes.

**Exit gate:** **This phase never ends.** It becomes the steady state of the product. The "exit" is product sunset, not graduation.
