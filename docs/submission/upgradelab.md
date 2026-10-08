# Submission text: UpgradeLab

For the Drips Wave application form. Nothing here has been submitted. No demo video is included, by design.

## 1. Pre-submission checks

- [x] Not in the approved list: the live list at `drips.network/wave/stellar/repos` (824 repositories, loaded in full on 2026-10-08) contains neither repository nor the organization `Upgrade-Lab`.
- [ ] Install the Drips GitHub app on the `Upgrade-Lab` organization (required for approval).
- [ ] Check the live per-user and per-organization application limits before applying (not published in the documentation).
- [ ] Re-read the current Wave terms on the day of submission.

## 2. Links

| Item | Link |
|---|---|
| Core repository | https://github.com/Upgrade-Lab/upgradelab-runner |
| App repository | https://github.com/Upgrade-Lab/upgradelab-studio |
| Live app | https://upgradelab-studio-anasamasama.vercel.app |
| Documentation (core) | https://stellar-developer-tools.gitbook.io/upgradelab-runner/ |
| Documentation (app) | https://stellar-developer-tools.gitbook.io/upgradelab-studio/ |
| Package | [`upgradelab-runner`](https://crates.io/crates/upgradelab-runner) on crates.io |
| Latest release (core) | https://github.com/Upgrade-Lab/upgradelab-runner/releases/latest |
| Latest release (app) | https://github.com/Upgrade-Lab/upgradelab-studio/releases/latest |
| CI (core) | https://github.com/Upgrade-Lab/upgradelab-runner/actions |
| CI (app) | https://github.com/Upgrade-Lab/upgradelab-studio/actions |
| Testnet contracts | [`CC6TBNXU...JMLM4`](https://stellar.expert/explorer/testnet/contract/CC6TBNXUS5NFBKDPEULVFXB4ORDYRYN6JRFYQWEC6YLG6EJ5JNHJMLM4) vault, recorded run 1; [`CAKHVPXU...77AQMB`](https://stellar.expert/explorer/testnet/contract/CAKHVPXUGQ33VMZYOTYHEY5MGMOQ4OWRQR3QSWSGQ4SUTXZXMM77AQMB) vault, recorded run 2 |

## 3. Project description (form field)

**UpgradeLab.** A Soroban upgrade can compile, pass its own unit tests and still lose a balance, double one, let anyone call `initialize` again, or leave the upgrade function unauthorized. Those failures show up in the state that survives the upgrade. UpgradeLab runs the compiled old and new WASM in the Soroban host, applies the application's seed operations, performs the upgrade, runs the migration, and evaluates named invariants, including repeated migration and an authorization check on `upgrade`. A report names each invariant, the values compared, the operation timeline and the execution category (compiled WASM in-process, testnet RPC, or native SDK tests) so they are never merged. Reports replay byte for byte. Built on: Rust 1.96, `soroban-sdk` 28.0.0, the in-process Soroban host, and a real testnet run of the corrected path.

No figure on the scale of the problem is cited, because none was verified for this submission.

## 4. How the two repositories connect

`upgradelab-runner` is the Rust runner and fixture vault (a correct migration and five deliberately broken ones). `upgradelab-studio` is a static viewer for the reports: broken next to corrected, invariants with evidence, the timeline and checkpoints. It vendors the runner's report schema and recorded reports and flags a report from a different runner version.

## 5. Neighboring approved work, stated plainly

`ShippedLabs/soroban-upgrade-safeguard` compares WASM builds statically, `benelabs/crucible` provides test utilities and `Tollcraft/soroban-budget-assert` checks costs. UpgradeLab executes an upgrade path with invariants and reports what it observed.

## 6. What this does not claim

No cloning of live state, no fees, resource limits or state archival, and the host protocol (28) can differ from the live network. A pass means the named invariants held in that scenario in that host. The vault is a teaching fixture and no contract-security expert has reviewed the invariants.

No user adoption, outside review, audit, funding or Wave approval is claimed. None of those processes has been started.

## 7. Planned issues

These are the open issues already filed, grouped by area. Each has a Summary, acceptance criteria as checkboxes, a Tech Stack line and a complexity label that was chosen to match the effort.

### upgradelab-runner (10 open)

**Features**

- [#1](https://github.com/Upgrade-Lab/upgradelab-runner/issues/1) feat(core): check multi-signature and threshold accounts for the upgrade path (high)
- [#2](https://github.com/Upgrade-Lab/upgradelab-runner/issues/2) feat(core): rehearse state archival and restore (high)
- [#3](https://github.com/Upgrade-Lab/upgradelab-runner/issues/3) feat(core): offer a container-based local network backend (high)
- [#4](https://github.com/Upgrade-Lab/upgradelab-runner/issues/4) feat(core): seed state from a recorded set of storage keys you supply (medium)
- [#6](https://github.com/Upgrade-Lab/upgradelab-runner/issues/6) feat(cli): extend `validate` to cross-check signers, probes and WASM paths (medium)
- [#7](https://github.com/Upgrade-Lab/upgradelab-runner/issues/7) feat(core): scaffold a scenario from a pair of WASM files (medium)
- [#9](https://github.com/Upgrade-Lab/upgradelab-runner/issues/9) feat(core): time and resource budgets in reports (medium)

**Tests and CI**

- [#10](https://github.com/Upgrade-Lab/upgradelab-runner/issues/10) ci: run the fixture tests on a second host platform in CI (medium)

**Documentation**

- [#5](https://github.com/Upgrade-Lab/upgradelab-runner/issues/5) docs: write a guide for authoring invariants (medium)
- [#8](https://github.com/Upgrade-Lab/upgradelab-runner/issues/8) docs: publish the report schema and a changelog policy (trivial)

### upgradelab-studio (10 open)

**Features**

- [#1](https://github.com/Upgrade-Lab/upgradelab-studio/issues/1) feat(ui): compare any two reports and show state diffs (medium)
- [#3](https://github.com/Upgrade-Lab/upgradelab-studio/issues/3) feat(ui): download a comparison as Markdown (medium)
- [#4](https://github.com/Upgrade-Lab/upgradelab-studio/issues/4) feat(ui): show the WASM hashes of both reports prominently (medium)
- [#7](https://github.com/Upgrade-Lab/upgradelab-studio/issues/7) feat(ui): show runner version differences clearly (medium)
- [#9](https://github.com/Upgrade-Lab/upgradelab-studio/issues/9) feat(ui): provide a deep link to an invariant (trivial)

**Security and hardening**

- [#8](https://github.com/Upgrade-Lab/upgradelab-studio/issues/8) feat(ui): verify a report's recorded hashes against supplied files (medium)

**Tests and CI**

- [#10](https://github.com/Upgrade-Lab/upgradelab-studio/issues/10) ci: run a real-browser smoke test in CI (high)

**Accessibility**

- [#2](https://github.com/Upgrade-Lab/upgradelab-studio/issues/2) fix(a11y): accessibility pass on the timeline and tables (medium)
- [#6](https://github.com/Upgrade-Lab/upgradelab-studio/issues/6) test(tests): render long probe values without breaking layout (medium)

**Documentation**

- [#5](https://github.com/Upgrade-Lab/upgradelab-studio/issues/5) docs: explain invariant ids (trivial)

