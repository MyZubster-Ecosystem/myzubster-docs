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
- Define clear responsibilities for:
  - `myzubster` — Core / Space Station
  - `MyZubsterGateway` — API and payment gateway
  - `MyZubster-Marketplace` — marketplace and bounty flows
  - `MyZubster-App` — mobile client
  - `MyZubster-Robot` — robotics and edge integration
  - `myzubster-animal-registry` — animal registry
  - `myzubster-verifier` — verification layer
  - `myzubster-ai-bot` — AI assistant / automation layer
  - `myzubster-docs` — documentation hub
  - `myzubster-manuals` — operational manuals
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

### Exit criteria
- Core ↔ Gateway integration is covered by integration tests.
- Duplicate payment events are handled safely.
- Failed or delayed providers do not corrupt state.
- No production claim is made without a validated production environment.

---

## Phase 3 — Registry and Verifier

**Goal:** establish the first verifiable real-world workflow.

### Target flow

**Registration → Evidence → Verification → Approval → Reward → Reporting**

### Deliverables
- Define registry schemas and identifiers.
- Establish evidence requirements.
- Implement verifier decisions and audit history.
- Link approved verification events to reward eligibility.
- Start with animal registration as the first canonical use case.
- Design schemas so the same pattern can later support plants, gardens, sensors, robots, and environmental activities.

### Exit criteria
- One registration can be created, reviewed, verified, and reported end to end.
- Every verification decision is auditable.
- Reward eligibility is deterministic and documented.

---

## Phase 4 — MyZubster App

**Goal:** make the ecosystem usable from a mobile client.

### Deliverables
- User/account onboarding.
- Wallet or payment identity integration where appropriate.
- Registration submission.
- Photo/evidence capture.
- QR-based object or registration lookup.
- Mission and bounty views.
- Verification status tracking.
- Reward history.
- Notifications.
- Map/location features where required and privacy-appropriate.

### Exit criteria
- A user can complete the primary registry workflow without directly using GitHub or backend tools.
- App errors and offline/poor-network cases are handled predictably.

---

## Phase 5 — Marketplace and bounty economy

**Goal:** connect verified work to offers, bounties, services, escrow, and reputation.

### Canonical lifecycle

**Proposal → Validation → Approval → Funding → Activity → Verification → Reward → Reporting**

### Deliverables
- Marketplace listings and requests.
- Bounty lifecycle model.
- Skills and service profiles.
- Escrow/payment integration through Gateway.
- Reputation based on verified activity, not only self-declared ratings.
- Clear separation between proposed, funded, approved, completed, verified, and paid states.

### Exit criteria
- One bounty can move through the full lifecycle without manual database intervention.
- Payment state and verification state are independently auditable.

---

## Phase 6 — Robot and IoT

**Goal:** integrate physical devices and field telemetry into the ecosystem.

### Deliverables
- Define robot/device identity.
- Standardize telemetry payloads.
- Integrate Arduino/ESP-class environmental sensors where applicable.
- Add device health and connectivity reporting.
- Support field missions and evidence submission from devices.
- Add remote command authorization and safety boundaries.
- Document hardware/software compatibility.

### Exit criteria
- At least one real or controlled test device reports telemetry through the supported stack.
- Device data is traceable to a registered device identity.
- Remote actions are authenticated and logged.

---

## Phase 7 — AI Bot / Eva Ioni

**Goal:** add intelligence above the verified platform rather than making AI a trusted system of record.

### Deliverables
- Telemetry summarization and anomaly assistance.
- Contributor and user support.
- Documentation assistance.
- Suggested missions or workflows.
- Repository and issue triage support.
- Guardrails for sensitive, financial, and state-changing actions.

### Architectural rule

AI may recommend and orchestrate, but critical economic, verification, and authorization decisions must remain enforceable through deterministic services and auditable rules.

### Exit criteria
- AI actions are permission-bounded and logged.
- Critical state transitions do not depend solely on model output.

---

## Phase 8 — Real pilot

**Goal:** validate one complete MyZubster use case in the real world.

### Recommended approach
Choose exactly one narrowly scoped pilot, for example:
- animal registration and verification;
- plant/tree registration;
- community garden monitoring;
- environmental sensor mission.

### Required end-to-end path

**App/Robot → Gateway → Core → Registry → Verifier → Reward → Reporting**

### Exit criteria
- The complete flow works with real users or real devices in a controlled pilot.
- Operational failures, support needs, costs, and data quality are measured.
- Pilot outcomes are documented before expansion.

---

## Phase 9 — Public ecosystem and scale

**Goal:** make the project repeatable, maintainable, and ready for broader participation.

### Deliverables
- Stable versioned releases.
- Public API/SDK documentation.
- Contributor onboarding.
- Maintainer and governance documentation.
- Bounty operations and reporting.
- Monitoring and alerting.
- Backup and restore procedures.
- Security review and dependency hygiene.
- Deployment runbooks and rollback procedures.
- Public ecosystem dashboard where appropriate.
- International/pilot expansion only after the core flow is validated.

### Exit criteria
- A new contributor can understand, run, test, and contribute to the project from public documentation.
- A deployment can be reproduced and rolled back.
- Operational ownership is clear for every critical component.

---

## Cross-cutting tracks

These workstreams apply throughout all phases:

### Security
- No secrets, private keys, wallet seeds, or credentials in repositories.
- Dependency scanning and patching.
- Authentication and authorization testing.
- Audit logging for critical operations.

### Reliability
- Health checks.
- Structured logging.
- Retries and timeout policies.
- Backup and restore tests.
- Failure-mode testing.

### Documentation
- Keep architecture, API contracts, onboarding, and operational docs synchronized with implementation.
- Mark experimental, simulated, testnet, and production-ready functionality explicitly.

### Governance and claims
- Clearly distinguish proposals from approved partnerships.
- Clearly distinguish bounty creation, completion, verification, and actual payment.
- Record externally verifiable approvals and funding separately from internal project plans.

### Testing
- Unit tests for business logic.
- Integration tests between repositories/services.
- End-to-end tests for canonical workflows.
- Pilot acceptance tests before scaling.

---

## Near-term execution order

1. Finalize `ARCHITECTURE.md` and architecture assets.
2. Merge repository ownership/submodule alignment after review.
3. Audit Core startup, tests, CI, and environment configuration.
4. Freeze the Core ↔ Gateway API contract.
5. Implement and test the Registry ↔ Verifier workflow.
6. Connect the mobile App to that first end-to-end workflow.
7. Add Marketplace/bounty integration only after verification works reliably.
8. Add Robot/IoT field integration.
9. Add AI assistance with explicit permission boundaries.
10. Run one narrow real-world pilot and use its findings to define the scaling plan.

---

## Definition of success

MyZubster should be considered structurally mature when a contributor or user can trace a real action from creation through verification, settlement/reward where applicable, and reporting, with every critical state transition documented, testable, and auditable.
