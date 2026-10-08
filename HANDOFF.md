# Stellar portfolio: final handoff

See also RELEASE-0.1.1.md for the coordinated patch release record.

Generated 2026-10-08 from the repositories on disk and GitHub. Owner: GitHub `Anasabubakar`. All repositories are public, MIT licensed, on branch `main`, tagged `v0.1.0` and `v0.1.1` with GitHub releases, with branch protection (no force-push or deletion; required CI status checks; no required reviewers because this is a solo project) and topics set.

## Repositories

| Project | Repo | Role | Commits | Tests (re-run by me unless noted) | Demo | Package |
|---|---|---|---|---|---|---|
| ContractAtlas | [contractatlas-core](https://github.com/Anasabubakar/contractatlas-core) | core | 59 | 50 + 2 live |  | @anas.abubakar/contractatlas-core (npm) |
| ContractAtlas | [contractatlas-studio](https://github.com/Anasabubakar/contractatlas-studio) | app | 41 | 27 | https://contractatlas-studio-anasamasama.vercel.app |  |
| AnchorTrace | [anchortrace-sdk](https://github.com/Anasabubakar/anchortrace-sdk) | core | 62 | 150 + 3 live |  | @anas.abubakar/anchortrace-sdk (npm) |
| AnchorTrace | [anchortrace-studio](https://github.com/Anasabubakar/anchortrace-studio) | app | 49 | 20 unit + 58 Playwright | https://anchortrace-studio-anasamasama.vercel.app |  |
| EventParity | [eventparity-engine](https://github.com/Anasabubakar/eventparity-engine) | core | 56 | 75 + 1 live |  | Go module github.com/Anasabubakar/eventparity-engine (no registry) |
| EventParity | [eventparity-studio](https://github.com/Anasabubakar/eventparity-studio) | app | 43 | 30 | https://eventparity-studio-anasamasama.vercel.app |  |
| RailLab | [raillab-engine](https://github.com/Anasabubakar/raillab-engine) | core | 55 | 160 |  | @anas.abubakar/raillab-engine (npm) |
| RailLab | [raillab-workbench](https://github.com/Anasabubakar/raillab-workbench) | app | 34 | 21 | https://raillab-workbench-anasamasama.vercel.app |  |
| AuthMatrix | [authmatrix-core](https://github.com/Anasabubakar/authmatrix-core) | core | 50 | 113 vitest + 4 Rust adapter + 1 real-host fixture; conformance 372/372, 74/74 |  | @anas.abubakar/authmatrix-core (npm) |
| AuthMatrix | [authmatrix-inspector](https://github.com/Anasabubakar/authmatrix-inspector) | app | 31 | 83 | https://authmatrix-inspector-anasamasama.vercel.app |  |
| ChargeGuard | [chargeguard-runner](https://github.com/Anasabubakar/chargeguard-runner) | core | 70 | 67 |  | @anas.abubakar/chargeguard-runner (npm) |
| ChargeGuard | [chargeguard-workbench](https://github.com/Anasabubakar/chargeguard-workbench) | app | 21 | 32 | https://chargeguard-workbench-anasamasama.vercel.app |  |
| UpgradeLab | [upgradelab-runner](https://github.com/Anasabubakar/upgradelab-runner) | core | 47 | 68 runner + 7 fixture |  | upgradelab-runner (crates.io) |
| UpgradeLab | [upgradelab-studio](https://github.com/Anasabubakar/upgradelab-studio) | app | 19 | 36 | https://upgradelab-studio-anasamasama.vercel.app |  |

Total commits across the 14 repositories: **637** (all authored as Anas Abubakar; no Claude/AI trailers).

Local paths: `/home/gamp/Desktop/Projects/Stellar/<project>/<repo>/`. Planning, status, blockers and the local issue backlog: `/home/gamp/Desktop/Projects/Stellar/_portfolio/`.

## Core and app pairings (tested versions, 0.1.1)

| App | Pairs with | Mechanism |
|---|---|---|
| contractatlas-studio 0.1.1 | contractatlas-core 0.1.1 (report v1) | vendored schema + sample reports, stamped commit, `compat.json` |
| anchortrace-studio 0.1.1 | anchortrace-sdk 0.1.1 | committed tarball, `pairing.json`, runtime and build-time check |
| eventparity-studio 0.1.1 | eventparity-engine 0.1.1 (report v1) | vendored schema, golden reports and text renderings, `compat.json` |
| raillab-workbench 0.1.1 | raillab-engine 0.1.1 (session/scenario v1) | committed tarball with stamped SHA-256 |
| authmatrix-inspector 0.1.1 | authmatrix-core 0.1.1 | committed tarball, `pairing.json`, `compat.json` |
| chargeguard-workbench 0.1.1 | chargeguard-runner 0.1.1 | vendored schemas and suites with SHA-256 stamp |
| upgradelab-studio 0.1.1 | upgradelab-runner 0.1.1 (report v1) | vendored schema and recorded reports with stamp |

## Supported networks and versions

Everything was exercised on **Stellar testnet** (protocol 29 at the time) or locally. Mainnet is never written to; it is only accepted by some schemas and not exercised. Node 22+ (developed on 24.19); Go 1.25 (EventParity); Rust 1.96 with soroban-sdk 28.0.0 and stellar-cli 28.1.0 for fixtures; `@stellar/stellar-sdk` 17.2.1 (ChargeGuard pins 15.1.0 because the published `@stellar/mpp` requires it).

## Verification record (2026-10-08)

- **GitHub CI:** green on all 14 repositories (re-checked on every 0.1.1 release commit) after fixing two failures (authmatrix-core CLI install step, upgradelab-runner clippy lint).
- **Clean-clone installs and builds:** done for every repo before the push (or by the agent that built it, then confirmed by CI).
- **Re-run by me today:** ChargeGuard runner 67/67; UpgradeLab runner 68 + fixtures 7 and all six scenarios give the expected verdicts and exit codes; AuthMatrix 113 + 4 Rust adapter + 1 real-host fixture, conformance 372/372 and 74/74 adapter agreement; AnchorTrace studio 58 Playwright tests; plus the unit suites listed above.
- **Real testnet re-runs today:** ContractAtlas live test (2 pass); EventParity live test (passes; the RPC retention window had moved so it asserted the honest gap path); AnchorTrace live tests (3 pass); AuthMatrix testnet simulate(enforce): 28 results, none contradict expectations (re-recorded under `evidence/testnet`); ChargeGuard real testnet settlement suite: 9 runs, all matched expectation (`docs/evidence/suite-testnet.rerun-2026-10-08.*`); UpgradeLab fresh testnet upgrade: 14/14 invariants, 12/12 transactions SUCCESS re-checked on public RPC (`evidence/testnet/rerun-2026-10-08.*`).
- **Real-browser checks (earlier, by me or the building agent):** every app at desktop and 375 px with `main.scrollWidth` vs `clientWidth`; a CSP bug and two narrow-screen overflows were found and fixed this way.

## Evidence locations

- ContractAtlas: `contractatlas-core/fixtures/testnet/` (manifest, DEPLOYMENT.md, before/after-upgrade reports).
- AnchorTrace: `anchortrace-sdk/fixtures/testnet/` (11 real transactions), `docs/evidence/`.
- EventParity: `eventparity-engine/corpus/` (ground truth, recorded Horizon/RPC exchanges, golden reports).
- RailLab: tests plus `raillab-workbench/docs/evidence/` screenshots.
- AuthMatrix: `authmatrix-core/evidence/{native-host,testnet}` and `docs/host-verification.md`.
- ChargeGuard: `chargeguard-runner/docs/evidence/` (stub and testnet suites, reruns).
- UpgradeLab: `upgradelab-runner/evidence/{host,native,testnet}`.

## Known limitations (see each repository's README for the full list)

- Classic payments only (AnchorTrace, EventParity); SEP-24 withdrawal subset with a simulated anchor (RailLab); charge mode, unsponsored, testnet (ChargeGuard); single-key classic-account signers (AuthMatrix, UpgradeLab auth).
- UpgradeLab uses the in-process Soroban host (protocol 28), not a local network, because Docker was unusable on the build machine. State archival is not modelled.
- Testnet runs are single observations of a shared network on one day; recorded corpora have retention windows (testnet RPC keeps about a week).
- Hosted demos show recorded or synthetic data and run no user code or network requests.

## Not claimed

User validation, maintainer or external review, professional audit, security certification, novelty, endorsement by SDF or Drips, and Drips Wave or SCF admission or funding. None of those processes has been started. No upstream issues, PRs, messages or applications were made.

## Local backlog

`_portfolio/backlog/<repo>.md`: 65 draft items (not published as issues), each tied to a documented limitation.

## Only the owner can do (or must decide)

1. Revoke the npm token and the crates.io token that were pasted into chat; create replacements if you want future publishes.
2. Choose whether and when to contact reviewers or maintainers, file any backlog items as issues, and apply to Drips Wave or SCF (each repository application is a separate decision; check current rules and limits first).
3. Optionally add custom domains for the Vercel demos and decide on paid resources (none were created).
4. Optionally add a required-reviewer rule if collaborators join (it was deliberately not enforced for a solo project).
5. Free disk space if you want to keep building (the machine was at about 98% full; cargo's shared target is about 4.5 GB and `~/.npm` is several GB).
6. Review the throwaway testnet keys left in `~/.config/stellar` (they hold only test XLM) and delete them if you do not need them.
