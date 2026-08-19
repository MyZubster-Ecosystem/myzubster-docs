# MyZubster Roadmap

## Guiding principle

**Architecture → Core → Gateway/Payments → Tari/MYZ Wallet → Registry/Verifier → App → Marketplace → Robot/IoT → AI → Pilot → Scale**

Every phase must finish with reproducible tests and documented evidence before the next layer is considered stable.

---

## Phase 0 — Architecture consolidation

- Finalize `ARCHITECTURE.md`.
- Upload architecture visuals under `assets/architecture/`.
- Align repositories and submodules under `MyZubster-Ecosystem`.
- Keep the Canva/Drive ecosystem visuals available for later project/video integration.

**Exit:** canonical architecture documented and repository responsibilities unambiguous.

---

## Phase 1 — Core / Space Station

- Stabilize backend, MongoDB, dashboard, telemetry, gardens, missions and simulator.
- Validate clean-clone startup and Docker configuration.
- Keep CI reproducible on supported Node versions.
- Add health checks, structured logs and configuration validation.

**Exit:** Core CI green and smoke-tested.

---

## Phase 2 — Gateway, Payments and Tari/MYZ — CURRENT PRIORITY

### 2.1 MyZubsterGateway dependency/CI recovery

**Blocker:** Gateway CI currently fails before tests because `package.json` and `package-lock.json` are out of sync.

Actions:
1. On PC/VPS checkout the affected Gateway branch.
2. Use the project-supported Node/npm version.
3. Run `npm install` to regenerate/synchronize `package-lock.json`.
4. Review the lockfile diff and ensure only expected dependency resolution changes are present.
5. Run `npm ci`, lint/typecheck and the complete local test suite from a clean state.
6. Commit the corrected lockfile.
7. Push and require GitHub CI, CI Boost, lint/typecheck and security checks to pass.

**Exit:** clean `npm ci` and all required Gateway checks green.

### 2.2 Gateway escrow lifecycle — PR #1349

Actions:
1. From a maintainer session on PC/VPS, approve the pending GitHub Actions workflows (`Approve and run workflows`).
2. Run all required CI/security workflows against the latest PR commit.
3. Re-check escrow persistence and transaction ownership.
4. Re-check admin authorization.
5. Re-check state-machine transitions and idempotency.
6. Re-check failure/retry handling.
7. Re-check monetary validation.
8. Do not bypass required checks.
9. Merge PR #1349 only after required checks are green and review blockers are resolved.

**Exit:** escrow lifecycle verified by CI and review.

### 2.3 Tari repository Docker build recovery

**Blocker:** the `Build docker images` workflow on the Tari `development` branch failed during the build environment setup for the escrow/robot-payment work.

Actions:
1. Re-open the failed workflow and retrieve the complete failing job log.
2. Identify whether failure comes from runner/toolchain configuration, Docker/buildx, dependencies, repository state or the escrow changes.
3. Reproduce locally/VPS where practical.
4. Apply the smallest deterministic fix.
5. Re-run the workflow.
6. Verify Docker image creation and multi-architecture manifest generation.

**Exit:** Tari Docker workflow green and reproducible.

### 2.4 MYZ asset visibility/balance in Tari wallet — BLOCKER

**Problem:** MYZ is not being loaded/displayed correctly in the Tari wallet. This must be fixed before the MYZ payment path is considered usable.

Diagnostic plan:
1. Identify the exact Tari wallet build/version and network used by the affected wallet.
2. Confirm the expected MYZ asset/resource identifier from the authoritative deployment/configuration source; never guess or hard-code an unverified identifier.
3. Confirm wallet and MYZ asset are on the same network/environment.
4. Trace MYZ creation/mint/transfer output from the originating transaction through the Gateway/Tari integration.
5. Verify the transaction is finalized and that the output belongs to the expected wallet/account.
6. Inspect wallet asset discovery/import/indexing logic.
7. Inspect balance query logic and any cache/indexer synchronization path.
8. Check whether MYZ exists on-chain but is not rendered by the UI, or whether the wallet never received/indexed the asset.
9. Check decimals/amount representation and resource-address mapping.
10. Add diagnostic logging without exposing seeds, private keys or sensitive wallet credentials.

Fix acceptance tests:
- A controlled MYZ test amount is issued/transferred to a fresh test wallet.
- The transaction reaches finality.
- The wallet discovers/imports MYZ without manual database edits.
- The displayed MYZ balance equals the authoritative balance.
- Restart/resync does not lose the asset or duplicate the balance.
- A second transfer updates the balance correctly.
- Failure/retry does not double-credit MYZ.
- Gateway/verifier records agree with wallet state.

**Exit:** MYZ is reliably visible in Tari wallet and balance updates are proven end-to-end.

### 2.5 End-to-end MYZ payment test

After 2.1–2.4 are green, run one controlled canonical path:

**MYZ issuance/source → Tari transaction → finality → wallet discovery → balance → Gateway → Verifier → application/reporting**

Capture transaction IDs, timestamps, network/environment and verification result in a test report. Never commit wallet seeds or private keys.

**Phase 2 exit:** Gateway CI green, escrow validated, Tari build green, MYZ wallet visibility fixed, and one MYZ end-to-end test passes without manual state manipulation.

---

## Phase 3 — Registry and Verifier

**Registration → Evidence → Verification → Approval → Reward → Reporting**

- Define schemas and identifiers.
- Maintain auditable verifier decisions.
- Support animal registry plus plants, gardens, environmental observations, sensors and robots.
- Connect reward eligibility only to deterministic verified state.

**Exit:** one registration completes the full audited workflow.

---

## Phase 4 — MyZubster App

- User/account onboarding.
- Wallet/payment identity integration.
- Photo/evidence capture and registration.
- QR lookup, missions, verification status, rewards and notifications.
- Privacy-appropriate maps/location.

**Exit:** primary workflow usable without direct backend/GitHub interaction.

---

## Phase 5 — Marketplace and bounty economy

**Proposal → Validation → Approval → Funding → Activity → Verification → Reward → Reporting**

- Listings, requests and bounty lifecycle.
- Gateway escrow integration.
- Verified reputation.
- Independently auditable payment and verification states.

---

## Phase 6 — Robot and IoT

- Device identity and telemetry schemas.
- Environmental sensors and device health.
- Field missions/evidence.
- Authenticated and logged remote commands.
- Connect robot-payment escrow only after Phase 2 is stable.

---

## Phase 7 — AI Bot / Eva Ioni

AI can assist, summarize, propose and orchestrate, but critical economic, authorization and verification transitions must remain deterministic, permission-bounded and auditable.

---

## Phase 8 — Real-world pilot

Run one narrow pilot such as plant/tree registration, community garden monitoring, animal registration or environmental sensing.

**App/Robot → Gateway → Core → Registry → Verifier → Reward → Reporting**

Measure failures, support needs, costs and data quality before expansion.

---

## Phase 9 — Public ecosystem and scale

- Stable releases and API/SDK documentation.
- Contributor onboarding and governance.
- Monitoring, backups, security review and rollback procedures.
- Public ecosystem dashboard where appropriate.
- Expand only after the canonical flow is reproducible.

---

## Cross-cutting rules

### Security
Never commit secrets, wallet seeds, private keys or credentials. Audit authorization and critical economic operations.

### Reliability
Use health checks, structured logs, retries/timeouts, deterministic CI and failure-mode tests.

### Documentation
Keep architecture, contracts and operational docs synchronized with implementation. Clearly label simulation, testnet and production status.

### Testing
Require unit, integration and end-to-end tests. Financial/payment state must never be declared working solely from UI behavior.

---

## Immediate PC/VPS execution queue

1. Upload remaining architecture images/assets.
2. Fix MyZubsterGateway `package-lock.json` synchronization and obtain green CI.
3. Approve and execute PR #1349 workflows; fix any remaining escrow failures.
4. Retrieve and diagnose the Tari Docker workflow failure.
5. Restore a green Tari Docker build.
6. Reproduce the MYZ-not-visible wallet bug with a controlled test wallet.
7. Verify MYZ resource/asset identifier and network configuration.
8. Trace transaction finality, wallet discovery/indexing and balance calculation.
9. Implement the wallet/Gateway fix and regression tests.
10. Run the complete MYZ end-to-end acceptance test.
11. Only then freeze the Core ↔ Gateway ↔ Tari/MYZ payment contract.
12. Continue Registry/Verifier and App integration.

---

## Definition of success

MyZubster is structurally mature when a real action can be traced from creation through deterministic verification, payment/reward where applicable, wallet-visible settlement and reporting, with every critical transition testable and auditable.
