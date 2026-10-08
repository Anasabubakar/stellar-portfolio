# Stellar portfolio

Coordination repository for seven Stellar developer tools. Each project is a core library or CLI plus a static demo app, so there are 14 repositories in total. Owner: [Anasabubakar](https://github.com/Anasabubakar). Everything is MIT licensed, runs on testnet or locally, and claims no audit, endorsement or funding status (see [HANDOFF.md](HANDOFF.md)).

Current release: **0.1.1** (EventParity engine and studio: **0.1.2**) (see [RELEASE-0.1.1.md](RELEASE-0.1.1.md) for source commits, checksums and pairings). 0.1.0 tags are preserved.

| Project | What it does | Core repo | Package | App repo | Live demo | Docs |
|---|---|---|---|---|---|
| ContractAtlas | Checks whether the WASM live on chain matches the audit scope a project declared | [contractatlas-core](https://github.com/Contract-Atlas/contractatlas-core) | [`@anas.abubakar/contractatlas-core`](https://www.npmjs.com/package/@anas.abubakar/contractatlas-core) | [contractatlas-studio](https://github.com/Contract-Atlas/contractatlas-studio) | [demo](https://contractatlas-studio-anasamasama.vercel.app) | [core](https://stellar-developer-tools.gitbook.io/contractatlas-core/) · [studio](https://stellar-developer-tools.gitbook.io/contractatlas-studio/) |
| AnchorTrace | Explains SEP-24 and classic-payment reconciliation outcomes | [anchortrace-sdk](https://github.com/Anchor-Trace/anchortrace-sdk) | [`@anas.abubakar/anchortrace-sdk`](https://www.npmjs.com/package/@anas.abubakar/anchortrace-sdk) | [anchortrace-studio](https://github.com/Anchor-Trace/anchortrace-studio) | [demo](https://anchortrace-studio-anasamasama.vercel.app) | [sdk](https://stellar-developer-tools.gitbook.io/anchortrace-sdk/) · [studio](https://stellar-developer-tools.gitbook.io/anchortrace-studio/) |
| EventParity | Compares Horizon and RPC payment ingestion over a ledger range | [eventparity-engine](https://github.com/Event-Parity/eventparity-engine) | Go module `github.com/Event-Parity/eventparity-engine` | [eventparity-studio](https://github.com/Event-Parity/eventparity-studio) | [demo](https://eventparity-studio-anasamasama.vercel.app) | [engine](https://stellar-developer-tools.gitbook.io/eventparity-engine/) · [studio](https://stellar-developer-tools.gitbook.io/eventparity-studio/) |
| RailLab | Deterministic SEP-24 consumer incident simulator | [raillab-engine](https://github.com/Rail-L-b/raillab-engine) | [`@anas.abubakar/raillab-engine`](https://www.npmjs.com/package/@anas.abubakar/raillab-engine) | [raillab-workbench](https://github.com/Rail-L-b/raillab-workbench) | [demo](https://raillab-workbench-anasamasama.vercel.app) | [engine](https://stellar-developer-tools.gitbook.io/raillab-engine/) · [workbench](https://stellar-developer-tools.gitbook.io/raillab-workbench/) |
| AuthMatrix | Soroban authorization interpretation and cross-SDK vectors | [authmatrix-core](https://github.com/Auth-Matrix/authmatrix-core) | [`@anas.abubakar/authmatrix-core`](https://www.npmjs.com/package/@anas.abubakar/authmatrix-core) | [authmatrix-inspector](https://github.com/Auth-Matrix/authmatrix-inspector) | [demo](https://authmatrix-inspector-anasamasama.vercel.app) | [core](https://stellar-developer-tools.gitbook.io/authmatrix-core/) · [inspector](https://stellar-developer-tools.gitbook.io/authmatrix-inspector/) |
| ChargeGuard | Replay-protection testing for Stellar MPP charges across workers | [chargeguard-runner](https://github.com/Charge-Guard/chargeguard-runner) | [`@anas.abubakar/chargeguard-runner`](https://www.npmjs.com/package/@anas.abubakar/chargeguard-runner) | [chargeguard-workbench](https://github.com/Charge-Guard/chargeguard-workbench) | [demo](https://chargeguard-workbench-anasamasama.vercel.app) | [runner](https://stellar-developer-tools.gitbook.io/chargeguard-runner/) · [workbench](https://stellar-developer-tools.gitbook.io/chargeguard-workbench/) |
| UpgradeLab | Executable Soroban upgrade and migration rehearsal | [upgradelab-runner](https://github.com/Upgrade-Lab/upgradelab-runner) | [`upgradelab-runner`](https://crates.io/crates/upgradelab-runner) (crates.io) | [upgradelab-studio](https://github.com/Upgrade-Lab/upgradelab-studio) | [demo](https://upgradelab-studio-anasamasama.vercel.app) | [runner](https://stellar-developer-tools.gitbook.io/upgradelab-runner/) · [studio](https://stellar-developer-tools.gitbook.io/upgradelab-studio/) |

## Playbook documents

| Phase | Document |
|---|---|
| 1. Ecosystem reconnaissance | [docs/phase-1-landscape.md](docs/phase-1-landscape.md) |
| 5. Contract specifications | [UpgradeableFixture](docs/contracts/contractatlas-upgradeable-fixture.md), [nested auth](docs/contracts/authmatrix-nested-auth-fixture.md), [vault v1 and v2](docs/contracts/upgradelab-vault.md) |
| 6. Contract coding-agent prompts | [docs/agent-prompts/](docs/agent-prompts/) (`contract-*.md`) |
| 7. App coding-agent prompts | [docs/agent-prompts/](docs/agent-prompts/) (`app-*.md`, one per app) |
| 12. Submission text (no demo video) | [docs/submission/](docs/submission/): [ContractAtlas](docs/submission/contractatlas.md), [AnchorTrace](docs/submission/anchortrace.md), [EventParity](docs/submission/eventparity.md), [RailLab](docs/submission/raillab.md), [AuthMatrix](docs/submission/authmatrix.md), [ChargeGuard](docs/submission/chargeguard.md), [UpgradeLab](docs/submission/upgradelab.md) |
| 13. Changes after approval | [docs/phase-13-iteration.md](docs/phase-13-iteration.md) |

Phases 5 to 7 describe contracts and apps that already exist, so the prompts are for rebuilding, reviewing or extending them. Phases 2, 3, 4, 8 to 11 were done as part of building and publishing the repositories and have no separate document.

## Contents

- [HANDOFF.md](HANDOFF.md): repositories, pairings, verification record, evidence locations, limitations, owner-only items.
- [RELEASE-0.1.1.md](RELEASE-0.1.1.md): the coordinated patch release with commits, checksums and pairings.

Demos show recorded or synthetic data and run no user code. Core/app pairing is by committed tarball or vendored schema plus stamp, recorded in each app's `pairing.json` or `compat.json`.
