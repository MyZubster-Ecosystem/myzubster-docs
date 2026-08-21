# MyZubster Documentation Hub

<p align="center">
  <img src="assets/readme/myzubster-docs.png" alt="MyZubster documentation overview" width="100%">
</p>

> 🌍 **Understand MyZubster in your language:** [Global multilingual guide](https://github.com/MyZubster-Ecosystem/myzubster/blob/main/docs/i18n/README.md) — English, Italiano, Español, Français, Deutsch, Português, 中文, 日本語, 한국어, العربية, हिन्दी, Русский, Türkçe, Bahasa Indonesia, Polski, Українська, বাংলা, اردو, فارسی, Kiswahili.
>
> MyZubster connects real-world observations, verifiable evidence, collaborative bounties and platform rewards. **MYZ is currently an internal reward/accounting ledger; external XMR/token/blockchain settlement is separate and independently verified.**

MyZubster is an open-source ecosystem in active development and validation for documenting real-world observations, coordinating verifiable bounty work, publishing selected public state through content-addressed infrastructure, and experimenting with applications, robotics, IoT and privacy-oriented integrations.

This repository is the cross-project documentation hub. The canonical technical architecture and bounty rules live in the main [`myzubster`](https://github.com/MyZubster-Ecosystem/myzubster) repository.

## Current project positioning

MyZubster is **not** defined by a single blockchain, robot or payment rail. Different repositories have different maturity levels: operational MVP components, prototypes, simulations, private service boundaries and proposed integrations coexist in the organization.

Claims in historical issues or posts should not be interpreted as proof that a feature is production-ready or that a bounty was paid.

## Ecosystem map

| Repository | Responsibility | Positioning |
|---|---|---|
| [`myzubster`](https://github.com/MyZubster-Ecosystem/myzubster) | Core ecosystem, API/workflows, gardens, bounty/reward logic, public architecture, digital Time Machine | Primary source of truth / Time Machine MVP in draft PR |
| [`MyZubsterGateway`](https://github.com/MyZubster-Ecosystem/MyZubsterGateway) | Gateway/integration and settlement boundary | Active validation; external settlement requires independent verification |
| [`MyZubster-Marketplace`](https://github.com/MyZubster-Ecosystem/MyZubster-Marketplace) | Marketplace/service experiments | Development |
| [`MyZubster-App`](https://github.com/MyZubster-Ecosystem/MyZubster-App) | Mobile/client application | Development |
| [`MyZubsterWeb`](https://github.com/MyZubster-Ecosystem/MyZubsterWeb) | Web presence | Repository bootstrap/synchronization track |
| [`myzubster-animal-registry`](https://github.com/MyZubster-Ecosystem/myzubster-animal-registry) | Animal/NFC registry experiment | Experimental; no blanket blockchain-storage claim |
| [`MyZubster-Robot`](https://github.com/MyZubster-Ecosystem/MyZubster-Robot) | Robotics + Physical Time Machine demonstrator | Prototype/simulation/hardware-integration research |
| [`EVA-IONI`](https://github.com/MyZubster-Ecosystem/EVA-IONI) | EVA IONI robotics/software | Experimental |
| [`myzubster-space-station`](https://github.com/MyZubster-Ecosystem/myzubster-space-station) | Software vertical slice/telemetry | MVP track; not a physical-space-station claim |
| [`myzubster-manuals`](https://github.com/MyZubster-Ecosystem/myzubster-manuals) | Manuals/runbooks | Documentation bootstrap |
| `ai-automation`, `myzubster-ai-bot`, `myzubster-escrow-api`, `myzubster-verifier` | Internal service boundaries | Private/internal tracks |

The complete repository map, including `myzubster-platform`, `MyZubster-Robot-Stack` and the external/upstream `tari` dependency, is maintained in [`docs/ECOSYSTEM.md`](https://github.com/MyZubster-Ecosystem/myzubster/blob/main/docs/ECOSYSTEM.md).

## MyZubster Time Machine program

The Time Machine program has two explicitly separated layers.

### Digital Time Machine

The core [`myzubster`](https://github.com/MyZubster-Ecosystem/myzubster) repository contains the draft implementation in [PR #560](https://github.com/MyZubster-Ecosystem/myzubster/pull/560). It records timestamped snapshots with provenance and SHA-256 integrity metadata, supports plants/sensors/maps/robots as canonical domains, and provides a read-only visual timeline/map at `/time-machine`.

The digital layer reconstructs **recorded historical project state**. It does not claim to change physical history, and missing historical states must not be invented or interpolated as facts.

### Physical Time Machine Demonstrator v1

The [`MyZubster-Robot`](https://github.com/MyZubster-Ecosystem/MyZubster-Robot) repository tracks a physical, reproducible temporal-measurement apparatus under [Epic #135](https://github.com/MyZubster-Ecosystem/MyZubster-Robot/issues/135).

Workstreams:

- [#136 — precision clock and drift measurement](https://github.com/MyZubster-Ecosystem/MyZubster-Robot/issues/136)
- [#137 — propagation delay and time-of-flight](https://github.com/MyZubster-Ecosystem/MyZubster-Robot/issues/137)
- [#138 — synchronized physical sensor-state recorder](https://github.com/MyZubster-Ecosystem/MyZubster-Robot/issues/138)
- [#139 — robot/device telemetry bridge and historical replay](https://github.com/MyZubster-Ecosystem/MyZubster-Robot/issues/139)
- [#140 — completion bounty](https://github.com/MyZubster-Ecosystem/MyZubster-Robot/issues/140)

The physical demonstrator is scientifically scoped to measurable phenomena such as clock drift, synchronization offset, propagation delay/time-of-flight and timestamped sensor/robot telemetry. It **does not claim backward time travel, faster-than-light propagation or alteration of past physical events**.

Bounty #140 is currently **UNFUNDED for external settlement**. Its stated **2,500 MYZ** is an internal MyZubster reward/accounting amount that may be recorded only after successful verification; it is not a guaranteed cash/XMR/token payment or a claim of on-chain value.

## Bounty system

The canonical policy is [`BOUNTIES.md`](https://github.com/MyZubster-Ecosystem/myzubster/blob/main/BOUNTIES.md).

The work lifecycle is deliberately separated from settlement:

```text
PROPOSED -> VALIDATED -> APPROVED -> FUNDED -> ACTIVE
         -> SUBMITTED -> UNDER_REVIEW -> VERIFIED
         -> REWARD_RECORDED -> SETTLEMENT_PENDING / SETTLED
```

Important rules:

- an issue, PR or merge does not prove payment;
- MYZ in the current core platform is an **internal reward/accounting ledger**;
- external XMR/token settlement must remain pending/unsettled until independently verified;
- no adapter/provider response alone may declare a payment final;
- sensitive work requires explicit authorization, privacy controls and appropriate review.

## IPFS public-state layer

The core platform can publish sanitized public snapshots to IPFS/IPNS, including indexes for photos, bounties, reward records, crawler observations and discoveries.

IPFS provides immutable content addressing and replication. It does **not** by itself decentralize authorization, review, application consensus or financial settlement. Operational application state still uses service/database layers while public snapshots are independently addressable.

Never publish secrets, private user identifiers, confidential research or sensitive infrastructure details into public IPFS metadata.

## Documentation principles

Documentation in every MyZubster repository should:

1. describe what is actually implemented;
2. distinguish `production`, `development`, `testnet`, `simulation`, `experimental` and `proposed` states;
3. avoid treating historical bounty amounts as proof of payment;
4. keep security-sensitive data and secrets out of repositories;
5. link to the canonical architecture and bounty policy rather than redefining incompatible rules locally;
6. for Time Machine material, distinguish directly recorded physical measurements, public recorded state, derived values and simulation.

## Getting started

Start with the main repository:

```bash
git clone https://github.com/MyZubster-Ecosystem/myzubster.git
cd myzubster
npm ci
```

Then read the repository-specific README and `.env.example` before starting a component. Never copy production secrets into GitHub issues, examples or documentation.

## Contributing

1. Select an open issue or propose a narrowly scoped change.
2. Verify the repository's current status and setup instructions.
3. Add tests/evidence appropriate to the work.
4. Open a PR linked to the issue.
5. Treat bounty verification and external settlement as separate steps.

For bounty work, read the canonical bounty policy before claiming a reward.

## Transparency & automation

MyZubster uses automation to assist with issue triage, documentation and development workflows. Automated output does not replace maintainer/security review for sensitive changes, bounty verification or settlement decisions.

## Security

Never commit or paste:

- private keys or wallet seed phrases;
- production passwords/tokens;
- private infrastructure credentials;
- confidential user/research data.

For security findings, use the repository's responsible-disclosure process rather than publishing unpatched exploit details in a public issue.

## License

Repository-specific licenses remain authoritative. Check the target repository before reusing code or documentation.
