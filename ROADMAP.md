# MyZubster Roadmap

This roadmap defines the recommended execution order for the MyZubster ecosystem. The goal is to consolidate the existing architecture first, stabilize the MVP, validate a complete end-to-end workflow, and only then expand the ecosystem.

## Guiding principle

Build one verified layer at a time:

**Architecture → Core → Gateway → Registry/Verifier → App → Marketplace → Robot/IoT → AI → Pilot → Scale**

Each phase should produce a testable, documented result that integrates with the previous phase. Avoid developing all repositories in parallel without a validated integration path.

---

## Phase 0 — Architecture consolidation

**Goal:** establish one canonical structure for the ecosystem.

### Deliverables
- Finalize the canonical ecosystem architecture in `ARCHITECTURE.md`.
- Store architecture visuals under `assets/architecture/`.
- Align repository ownership and submodule references with `MyZubster-Ecosystem`.
- Define clear responsibilities for Core, Gateway, Marketplace, App, Robot, registries, Verifier, AI Bot, Docs, and Manuals.
- Document service boundaries and ownership rules.

### Exit criteria
- Architecture is documented and visible from the documentation hub.
- Repository links and ownership references are consistent.
- No major component has an ambiguous responsibility.

---

## Phase 1 — Core / Space Station MVP

**Goal:** make `myzubster` the stable operational center of the ecosystem.

### Deliverables
- Stabilize backend APIs and business logic.
- Validate MongoDB persistence and environment configuration.
- Stabilize dashboard and telemetry flows.
- Validate gardens, missions, and simulator integration.
- Standardize local development and Docker startup.
- Maintain reproducible CI for supported Node.js versions.
- Add health checks, error handling, logging, and configuration validation.

### Exit criteria
- Core can start from a clean clone using documented steps.
- CI is green.
- Core APIs have smoke tests.
- Dashboard and simulator communicate reliably with the backend.

---

## Phase 2 — Gateway, identity, and payments

**Goal:** connect the Core to a well-defined external integration layer.

### Deliverables
- Define versioned API contracts between Core and Gateway.
- Add authentication and authorization boundaries.
- Define wallet/account identity model.
- Validate XMR and MYZ payment flows in simulation/test environments first.
- Implement webhook verification, idempotency, retries, and audit logs.
- Define settlement state transitions and failure handling.
- Document secrets management and environment separation.

### Immediate Gateway checkpoint — PR #1349
- From a maintainer session on PC/VPS, approve the currently pending GitHub Actions workflows for `MyZubsterGateway` PR #1349 (`Approve and run workflows`).
- Allow all required CI/security workflows to execute against the latest escrow-lifecycle commits.
- Review any failing job and fix the implementation or tests before merge; do not bypass required checks.
- Re-review escrow persistence, transaction ownership, admin authorization, state-machine/idempotency behavior, failure/retry handling, and monetary validation after CI completes.
- Merge PR #1349 only when required checks are green and the review blockers are resolved.

### Exit criteria
- Core ↔ Gateway integration is covered by integration tests.
- Duplicate payment events are handled safely.
- Failed or delayed providers do not corrupt state.
- No production claim is made without a validated production environment.

---

## Phase 3 — Registry and Verifier

**Goal:** establish the first verifiable real-world workflow.

**Registration → Evidence → Verification → Approval → Reward → Reporting**

### Deliverables
- Define registry schemas and identifiers.
- Establish evidence requirements.
- Implement verifier decisions and audit history.
- Link approved verification events to reward eligibility.
- Start with animal registration as the first canonical use case.
- Extend the same pattern to plants, gardens, sensors, robots, environmental activities, and field observations.

### Exit criteria
- One registration can be created, reviewed, verified, and reported end to end.
- Every verification decision is auditable.
- Reward eligibility is deterministic and documented.

---

## Phase 4 — MyZubster App

**Goal:** make the ecosystem usable from a mobile client.

### Deliverables
- User/account onboarding.
- Wallet/payment identity integration where appropriate.
- Registration and photo/evidence submission.
- QR-based object lookup.
- Mission and bounty views.
- Verification status and reward history.
- Notifications and privacy-appropriate map/location features.

---

## Phase 5 — Marketplace and bounty economy

**Goal:** connect verified work to offers, bounties, services, escrow, and reputation.

**Proposal → Validation → Approval → Funding → Activity → Verification → Reward → Reporting**

### Deliverables
- Marketplace listings and requests.
- Bounty lifecycle model.
- Skills and service profiles.
- Escrow/payment integration through Gateway.
- Reputation based on verified activity.
- Auditable separation of proposed, funded, approved, completed, verified, and paid states.

---

## Phase 6 — Robot and IoT

**Goal:** integrate physical devices and field telemetry.

### Deliverables
- Device identity and standardized telemetry.
- Arduino/ESP-class environmental sensors where applicable.
- Device health/connectivity reporting.
- Field missions and device evidence submission.
- Authenticated and logged remote commands.

---

## Phase 7 — AI Bot / Eva Ioni

**Goal:** add intelligence above the verified platform rather than making AI the trusted system of record.

AI may recommend and orchestrate, but critical economic, verification, and authorization decisions must remain enforceable through deterministic services and auditable rules.

---

## Phase 8 — Real pilot

**Goal:** validate one complete MyZubster use case in the real world.

Candidate pilots include animal registration, plant/tree registration, community garden monitoring, environmental observations, and sensor missions.

**App/Robot → Gateway → Core → Registry → Verifier → Reward → Reporting**

---

## Phase 9 — Public ecosystem and scale

**Goal:** make the project repeatable, maintainable, and ready for broader participation.

### Deliverables
- Stable versioned releases and public API/SDK documentation.
- Contributor onboarding and governance documentation.
- Monitoring, backup/restore, security review, deployment and rollback runbooks.
- Public ecosystem dashboard where appropriate.
- International/pilot expansion only after the core flow is validated.

---

## Cross-cutting tracks

### Security
No secrets, private keys, wallet seeds, or credentials in repositories; maintain dependency scanning, authentication/authorization tests, and audit logging.

### Reliability
Health checks, structured logging, retries/timeouts, backup/restore tests, and failure-mode testing.

### Documentation
Keep architecture, API contracts, onboarding, and operational docs synchronized with implementation; mark experimental, simulated, testnet, and production-ready functionality explicitly.

### Governance and claims
Distinguish proposals from approved partnerships and distinguish bounty creation, completion, verification, and actual payment.

### Testing
Unit, integration, end-to-end, and pilot acceptance tests before scaling.

---

## Near-term execution order

1. Finalize `ARCHITECTURE.md` and architecture assets.
2. Merge repository ownership/submodule alignment after review.
3. Audit Core startup, tests, CI, and environment configuration.
4. **PC/VPS: approve and run the pending workflows for MyZubsterGateway PR #1349; inspect results and merge only after required checks are green.**
5. Freeze the Core ↔ Gateway API contract after the escrow lifecycle is validated.
6. Implement and test the Registry ↔ Verifier workflow.
7. Connect the mobile App to that first end-to-end workflow.
8. Add Marketplace/bounty integration only after verification works reliably.
9. Add Robot/IoT field integration.
10. Add AI assistance with explicit permission boundaries.
11. Run one narrow real-world pilot and use its findings to define the scaling plan.

---

## Definition of success

MyZubster should be considered structurally mature when a contributor or user can trace a real action from creation through verification, settlement/reward where applicable, and reporting, with every critical state transition documented, testable, and auditable.
