# MyZubster Ecosystem Architecture

_Last verified: 2026-08-18_

This document is the canonical high-level map of the MyZubster ecosystem. It aligns the repository structure with the architecture/storyboard work maintained in Google Drive.

## 1. Architecture at a glance

```text
MyZubster Ecosystem
├── myzubster                  # Core / Space Station MVP
│   ├── backend                # API and business logic
│   ├── dashboard              # Web UI
│   ├── simulator              # Eva Ioni simulator
│   ├── gateway                # Gateway integration boundary
│   └── docs                   # Core technical documentation
├── MyZubsterGateway           # API gateway, payments, webhooks
├── MyZubster-Marketplace      # Skills/services marketplace
├── MyZubster-App              # Mobile application
├── MyZubster-Robot            # Robot code / hardware-facing layer
├── myzubster-animal-registry  # Animal registry service
├── myzubster-verifier         # Verification service
├── myzubster-ai-bot           # AI/bot service
├── myzubster-docs             # Canonical documentation hub
└── myzubster-manuals          # Manuals and operator/user guides
```

## 2. Repository responsibilities

| Repository | Canonical responsibility | Integration role |
|---|---|---|
| `myzubster` | Core orchestration / Space Station MVP | Central service coordinating missions, telemetry, dashboard and integrations |
| `MyZubsterGateway` | Gateway and payment integration | Boundary for external APIs, Monero/payment flows and webhooks |
| `MyZubster-Marketplace` | Marketplace | Skills, services and exchange workflows |
| `MyZubster-App` | Mobile client | User-facing mobile access |
| `MyZubster-Robot` | Robotics layer | Robot software, DNA/schema and hardware integration |
| `myzubster-animal-registry` | Registry | Animal identity/registration domain |
| `myzubster-verifier` | Verification | Validation/verification workflows |
| `myzubster-ai-bot` | AI automation | Bot and AI-assisted workflows |
| `myzubster-docs` | Documentation source of truth | Cross-repository architecture, onboarding, contracts and guides |
| `myzubster-manuals` | Manuals | Operational and end-user manuals |

## 3. Core service boundaries

### Core (`myzubster`)
Owns orchestration, backend APIs, telemetry, dashboards, simulation and integration points. It should not duplicate the full implementation of independent services when those services have dedicated repositories.

### Gateway
Owns external API/payment boundaries, settlement integrations and webhooks. The core repository should consume it through a clear interface rather than maintaining competing copies.

### Marketplace
Owns marketplace-specific domain logic and UI/API concerns. The core repository should reference it as an ecosystem component.

### Registry and Verifier
Registry owns the record lifecycle; Verifier owns independent validation of records or activities. Keeping these boundaries separate makes auditability and future scaling easier.

### Robot and App
Robot is the hardware/edge-facing layer. App is the human-facing mobile layer. Both should rely on documented APIs rather than direct coupling to internal core implementation details.

### Documentation
`myzubster-docs` is the canonical place for ecosystem-wide architecture and repository relationships. Repository-specific operational details remain in each repository README/docs.

## 4. Current structural gaps

1. The ecosystem architecture visuals exist outside GitHub and are not yet mirrored into the documentation assets.
2. The main repository currently uses Git submodule references for Gateway and Marketplace that should point to organization-owned repositories.
3. Documentation currently describes overlapping project identities (for example “Space Station MVP” versus the wider robot/Monero ecosystem) and needs one explicit hierarchy: **ecosystem → core platform → services/clients**.
4. Several newer repositories are not yet listed in the documentation hub repository table.
5. Production-readiness status should be maintained per component rather than inferred from repository existence.

## 5. Target hierarchy

Use this naming hierarchy consistently:

- **MyZubster Ecosystem** — the whole organization and product family.
- **MyZubster Core / Space Station MVP (`myzubster`)** — central orchestration platform.
- **Services** — Gateway, Marketplace, Registry, Verifier, AI Bot.
- **Clients / Edge** — App and Robot.
- **Knowledge layer** — Docs and Manuals.

## 6. Integration direction

```text
App -----------┐
Robot ---------┤
Marketplace ---┤
Registry ------┼--> Gateway / documented APIs --> Core / Space Station
Verifier ------┤                              ├--> telemetry / missions
AI Bot --------┘                              └--> reporting / rewards

Docs + Manuals describe the contracts across all layers.
```

Exact runtime routing may evolve, but every cross-repository integration should have a documented API/event contract and a single owner.

## 7. Documentation asset plan

Create `assets/architecture/` and mirror the approved Drive diagrams there using stable names:

```text
assets/architecture/
├── ecosystem-overview.jpg
├── ecosystem-storyboard.png
├── repository-architecture.jpg
├── repository-storyboard.png
└── repository-visualization.png
```

After the files are mirrored, embed the current approved diagrams in this document and remove obsolete duplicates.

## 8. Next cleanup sequence

1. Correct organization-owned repository links/submodules.
2. Mirror approved architecture images into `myzubster-docs/assets/architecture/`.
3. Update the documentation hub README repository table with all active components.
4. Add API/event ownership documentation for cross-repository integrations.
5. Audit duplicate code between the core repository and dedicated service repositories.
6. Mark each component as experimental, development, testnet, staging or production-ready using evidence from its own repository.

This file should be updated whenever repository ownership, service boundaries, or the canonical ecosystem architecture changes.
