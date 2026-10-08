# Stellar portfolio

Coordination repository for seven Stellar developer tools. Each project is a core library or CLI plus a static demo app, so there are 14 repositories in total. Owner: [Anasabubakar](https://github.com/Anasabubakar). Everything is MIT licensed, runs on testnet or locally, and claims no audit, endorsement or funding status (see [HANDOFF.md](HANDOFF.md)).

Current release: **0.1.1** (EventParity engine and studio: **0.1.2**) (see [RELEASE-0.1.1.md](RELEASE-0.1.1.md) for source commits, checksums and pairings). 0.1.0 tags are preserved.

| Project | What it does | Core repo | Package | App repo | Live demo |
|---|---|---|---|---|---|
| ContractAtlas | Checks whether the WASM live on chain matches the audit scope a project declared | [contractatlas-core](https://github.com/Anasabubakar/contractatlas-core) | [`@anas.abubakar/contractatlas-core`](https://www.npmjs.com/package/@anas.abubakar/contractatlas-core) | [contractatlas-studio](https://github.com/Anasabubakar/contractatlas-studio) | [demo](https://contractatlas-studio-anasamasama.vercel.app) |
| AnchorTrace | Explains SEP-24 and classic-payment reconciliation outcomes | [anchortrace-sdk](https://github.com/Anasabubakar/anchortrace-sdk) | [`@anas.abubakar/anchortrace-sdk`](https://www.npmjs.com/package/@anas.abubakar/anchortrace-sdk) | [anchortrace-studio](https://github.com/Anasabubakar/anchortrace-studio) | [demo](https://anchortrace-studio-anasamasama.vercel.app) |
| EventParity | Compares Horizon and RPC payment ingestion over a ledger range | [eventparity-engine](https://github.com/Anasabubakar/eventparity-engine) | Go module `github.com/Anasabubakar/eventparity-engine` | [eventparity-studio](https://github.com/Anasabubakar/eventparity-studio) | [demo](https://eventparity-studio-anasamasama.vercel.app) |
| RailLab | Deterministic SEP-24 consumer incident simulator | [raillab-engine](https://github.com/Anasabubakar/raillab-engine) | [`@anas.abubakar/raillab-engine`](https://www.npmjs.com/package/@anas.abubakar/raillab-engine) | [raillab-workbench](https://github.com/Anasabubakar/raillab-workbench) | [demo](https://raillab-workbench-anasamasama.vercel.app) |
| AuthMatrix | Soroban authorization interpretation and cross-SDK vectors | [authmatrix-core](https://github.com/Anasabubakar/authmatrix-core) | [`@anas.abubakar/authmatrix-core`](https://www.npmjs.com/package/@anas.abubakar/authmatrix-core) | [authmatrix-inspector](https://github.com/Anasabubakar/authmatrix-inspector) | [demo](https://authmatrix-inspector-anasamasama.vercel.app) |
| ChargeGuard | Replay-protection testing for Stellar MPP charges across workers | [chargeguard-runner](https://github.com/Anasabubakar/chargeguard-runner) | [`@anas.abubakar/chargeguard-runner`](https://www.npmjs.com/package/@anas.abubakar/chargeguard-runner) | [chargeguard-workbench](https://github.com/Anasabubakar/chargeguard-workbench) | [demo](https://chargeguard-workbench-anasamasama.vercel.app) |
| UpgradeLab | Executable Soroban upgrade and migration rehearsal | [upgradelab-runner](https://github.com/Anasabubakar/upgradelab-runner) | [`upgradelab-runner`](https://crates.io/crates/upgradelab-runner) (crates.io) | [upgradelab-studio](https://github.com/Anasabubakar/upgradelab-studio) | [demo](https://upgradelab-studio-anasamasama.vercel.app) |

## Contents

- [HANDOFF.md](HANDOFF.md): repositories, pairings, verification record, evidence locations, limitations, owner-only items.
- [RELEASE-0.1.1.md](RELEASE-0.1.1.md): the coordinated patch release with commits, checksums and pairings.

Demos show recorded or synthetic data and run no user code. Core/app pairing is by committed tarball or vendored schema plus stamp, recorded in each app's `pairing.json` or `compat.json`.
