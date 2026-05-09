# Phase Gate Checklist

Every phase has a gate. You may not enter the next phase until every box is checked. If you cannot check a box, you cannot proceed — you must go back, never skip forward.

---

## Phase 0 Gate — Discovery Complete

- [ ] Problem statement is written and one paragraph long
- [ ] User profile is documented (role, context, constraints, environment)
- [ ] Mental health / wellbeing considerations documented (if applicable)
- [ ] Data sources and integrations identified
- [ ] Success metrics defined and measurable
- [ ] Assumptions list is numbered and complete
- [ ] Regulated data classes identified (HIPAA / PCI / NIST 800-171 / CUI / none)
- [ ] User's daily interaction can be described in 3 sentences without naming a technology
- [ ] `DISCOVERY.md` exists and is approved

**Gate failure:** Go back. Do not start architecture. The most common failure here is "I know it in my head" — write it down anyway. If you cannot, the problem is not yet understood.

---

## Phase 1 Gate — Architecture Complete

- [ ] ERD exists with every entity named
- [ ] Component architecture diagram exists
- [ ] State management approach documented
- [ ] API and integration contracts defined
- [ ] Tech stack decisions justified in `TECH_DECISIONS.md`
- [ ] Security considerations documented (auth, encryption at rest, encryption in transit, key management, access control, audit logging)
- [ ] Privacy considerations documented (data minimization, retention, consent)
- [ ] AI risk surfaces identified per NIST AI RMF (where the model touches code, data, or user-facing output)
- [ ] Mermaid diagrams generated for system, component, and data flow
- [ ] Every external dependency identified and license-checked
- [ ] Every sensitive data field tagged with classification + protective control

**Gate failure:** Go back to Discovery if any entity surprises you. Architecture failures usually trace to incomplete discovery. Do not write code yet.

---

## Phase 2 Gate — Foundation Complete

- [ ] Repo folder structure matches architecture
- [ ] `CLAUDE.md` exists and is filled out
- [ ] Base data files / schemas populated
- [ ] Build / distribution scaffolding present for the project type (e.g., `package.json`, `Dockerfile`, PWA manifest, app store config — whichever applies)
- [ ] CI/CD pipeline configured (if applicable)
- [ ] Commit convention documented (Conventional Commits or equivalent)
- [ ] README shell exists with empty section headings
- [ ] `.gitignore` excludes secrets, build artifacts, OS files
- [ ] `.env.example` exists; no real secrets committed
- [ ] First commit (`init: project scaffold`) made
- [ ] Lint and build run cleanly against the empty implementation
- [ ] A new developer can understand the structure in under 5 minutes from README alone

**Gate failure:** Do not start feature work. Missing scaffolding compounds during the build. Fix the foundation first.

---

## Phase 3 Gate — Core Build Complete

- [ ] Every MVP feature in `DISCOVERY.md` is implemented
- [ ] Every feature has its own commit with a meaningful message
- [ ] Every feature has been tested in the target environment
- [ ] No feature N+1 was started before feature N was committed
- [ ] No scope creep — features beyond MVP are parked in `ROADMAP.md`, not built
- [ ] Product solves the core problem stated in `DISCOVERY.md` without additional features
- [ ] No `TODO`/`FIXME` markers in critical paths

**Gate failure:** If the product needs "one more feature" to solve the core problem, the problem was misstated — go back to Discovery. If features are partially built, finish them before moving on.

---

## Phase 4 Gate — Hardening Complete

- [ ] All user inputs have validation and error handling
- [ ] Edge cases tested (empty state, max state, network failure, bad data)
- [ ] Performance reviewed against target hardware
- [ ] Security checklist passed (see below)
- [ ] Privacy review passed (data minimization, retention, consent flows)
- [ ] Accessibility reviewed (WCAG 2.2 AA target)
- [ ] No console errors in production build
- [ ] Documentation complete: README, architecture, schema, decisions
- [ ] All Mermaid diagrams generated and embedded
- [ ] Compliance checklist signed for applicable frameworks (ISO 27001, ISO 9001, NIST 800-171, HIPAA, PCI, CMMC L2, NIST AI RMF)
- [ ] You would be comfortable sharing this repo publicly right now

### Security checklist (subset — full list lives in repo's SECURITY.md once generated)

- [ ] No hardcoded secrets, tokens, or credentials
- [ ] No secrets in commit history
- [ ] All third-party dependencies scanned for known CVEs
- [ ] Auth flows reviewed against OWASP ASVS
- [ ] Data-at-rest encryption documented and enabled where required
- [ ] Data-in-transit encryption (TLS 1.2+) for all network calls
- [ ] Audit logging enabled on sensitive code paths
- [ ] Input validation prevents injection (SQL, command, XSS)
- [ ] Rate limiting / throttling on public endpoints
- [ ] Error messages do not leak internal state

**Gate failure:** Do not deploy. A hardening gate failure that ships becomes a production incident.

---

## Phase 5 Gate — Deployment Complete

- [ ] Deployment target chosen and configured
- [ ] Environment variables managed via the platform's secret store
- [ ] Install / access verified on target environment(s) (PWA install, package install, container deploy, mobile sideload, CLI install path, API smoke test — whichever applies)
- [ ] Performance verified on real hardware
- [ ] First real user session completed end to end
- [ ] Feedback collection mechanism live
- [ ] Production logging and monitoring confirmed receiving events
- [ ] Backup / data export path verified
- [ ] Rollback plan documented

**Gate failure:** Roll back. Do not leave a half-deployed product running. If the first real user cannot complete the workflow, the deploy did not succeed regardless of what the dashboard says.

---

## Phase 6 Gate — Iteration Steady State

This phase has no exit gate. It does have a *running* gate that every change must pass:

- [ ] Change is tied to a piece of real user feedback or a real defect
- [ ] One change at a time (no bundled feature drops)
- [ ] Regression test run after the change
- [ ] Documentation updated
- [ ] `CHANGELOG.md` updated
- [ ] Version bumped per semver if behavior changed
- [ ] Security and compliance checks re-run if the change touched auth, data, or third-party integrations

**Gate failure:** Revert. Diagnose. Re-attempt with the gate respected.

---

## Gates Claude Will Enforce Automatically

Claude will refuse the following actions when the corresponding gate has not been passed:

- **Will not write feature code before `CLAUDE.md` exists.** (Phase 2 gate)
- **Will not build feature N+1 before N is committed.** (Phase 3 gate)
- **Will not deploy before README is complete.** (Phase 4 gate)
- **Will not merge or commit code without error handling on user inputs.** (Phase 4 gate)
- **Will not skip commit messages.** Every commit must have a meaningful Conventional Commits message.
- **Will not hardcode data that belongs in config files.** Secrets, environment-specific values, and feature flags go in `.env` or config, never in source.
- **Will not bypass the security checklist before a Phase 4→5 transition.**
- **Will not silently skip a gate.** If the human asks Claude to skip, Claude will require an explicit `[OVERRIDE]` prefix and will log the override in `CHANGELOG.md`.
- **Will not introduce a new third-party dependency without flagging the license, CVE history, and footprint.**
- **Will not write or modify code in a regulated data path without naming the applicable controls.** (HIPAA, PCI, NIST 800-171, CMMC L2.)

These are not suggestions. They are the protocol. The human can override any one of them with the `[OVERRIDE]` prefix described in `CLAUDE_PROTOCOL.md` — and that override goes on the record.
