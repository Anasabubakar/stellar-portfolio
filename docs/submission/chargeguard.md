# Submission text: ChargeGuard

For the Drips Wave application form. Nothing here has been submitted. No demo video is included, by design.

## 1. Pre-submission checks

- [x] Not in the approved list: the live list at `drips.network/wave/stellar/repos` (824 repositories, loaded in full on 2026-10-08) contains neither repository nor the organization `Charge-Guard`.
- [ ] Install the Drips GitHub app on the `Charge-Guard` organization (required for approval).
- [ ] Check the live per-user and per-organization application limits before applying (not published in the documentation).
- [ ] Re-read the current Wave terms on the day of submission.

## 2. Links

| Item | Link |
|---|---|
| Core repository | https://github.com/Charge-Guard/chargeguard-runner |
| App repository | https://github.com/Charge-Guard/chargeguard-workbench |
| Live app | https://chargeguard-workbench-anasamasama.vercel.app |
| Documentation (core) | https://stellar-developer-tools.gitbook.io/chargeguard-runner/ |
| Documentation (app) | https://stellar-developer-tools.gitbook.io/chargeguard-workbench/ |
| Package | [`@anas.abubakar/chargeguard-runner`](https://www.npmjs.com/package/@anas.abubakar/chargeguard-runner) |
| Latest release (core) | https://github.com/Charge-Guard/chargeguard-runner/releases/latest |
| Latest release (app) | https://github.com/Charge-Guard/chargeguard-workbench/releases/latest |
| CI (core) | https://github.com/Charge-Guard/chargeguard-runner/actions |
| CI (app) | https://github.com/Charge-Guard/chargeguard-workbench/actions |
| On-chain contracts | None. This project deploys no contract of its own; its evidence is recorded transactions and ledgers. |

## 3. Project description (form field)

**ChargeGuard.** A paid API that accepts Stellar MPP charges must reject a credential that has already been used, even when two workers serve requests and one restarts. With in-memory state per worker, a replayed credential can pass. ChargeGuard runs the official MPP charge integration in two workers and exercises challenge consumption, restart persistence, storage unavailability and ambiguous settlement. It reports four distinct levels for each payment: accepted credential, submitted transaction, confirmation and fulfillment. In the recorded suite, isolated memory stores fail the repeated-credential scenario and a shared atomic SQLite store passes it. Built on: `@stellar/mpp` 0.7.1, `mppx` 0.6.31, Stellar testnet settlement, SQLite as the shared store.

No figure on the scale of the problem is cited, because none was verified for this submission.

## 4. How the two repositories connect

`chargeguard-runner` is the harness, reference server, scenarios and reports. `chargeguard-workbench` is a static viewer of recorded run and suite reports, with the isolated-versus-shared comparison, per-worker lanes and the four levels. It vendors the runner's schemas and recorded suites with a checksum stamp.

## 5. Neighboring approved work, stated plainly

`winsznx/routedock` is a client-side payment layer over x402 and MPP, and `accensa/x402-facilitator-stellar` is a facilitator. ChargeGuard tests the server side's replay protection across workers.

## 6. What this does not claim

Charge mode, unsponsored, on testnet only, against the runner's own reference server. It does not claim linearizability or exactly-once business delivery, and a finite number of runs is evidence and not proof.

No user adoption, outside review, audit, funding or Wave approval is claimed. None of those processes has been started.

## 7. Planned issues

These are the open issues already filed, grouped by area. Each has a Summary, acceptance criteria as checkboxes, a Tech Stack line and a complexity label that was chosen to match the effort.

### chargeguard-runner (10 open)

**Features**

- [#1](https://github.com/Charge-Guard/chargeguard-runner/issues/1) feat(core): run the scenarios against a user-supplied server (high)
- [#3](https://github.com/Charge-Guard/chargeguard-runner/issues/3) feat(core): cover the sponsored (`feePayer`) charge path (high)
- [#5](https://github.com/Charge-Guard/chargeguard-runner/issues/5) feat(core): add a scenario for ambiguous settlement after a timeout (medium)
- [#6](https://github.com/Charge-Guard/chargeguard-runner/issues/6) feat(core): repeat each scenario N times and report how stable the result is (medium)
- [#7](https://github.com/Charge-Guard/chargeguard-runner/issues/7) feat(core): time-box testnet runs and fail clearly when the network is slow (medium)
- [#10](https://github.com/Charge-Guard/chargeguard-runner/issues/10) feat(cli): add JUnit output for CI dashboards (medium)

**Tests and CI**

- [#2](https://github.com/Charge-Guard/chargeguard-runner/issues/2) test(tests): test the Redis and PostgreSQL store adapters over a network (high)
- [#4](https://github.com/Charge-Guard/chargeguard-runner/issues/4) ci: re-validate against newer `@stellar/mpp` and `mppx` releases (medium)
- [#9](https://github.com/Charge-Guard/chargeguard-runner/issues/9) test(tests): report worker restarts and what survived them (medium)

**Documentation**

- [#8](https://github.com/Charge-Guard/chargeguard-runner/issues/8) docs: document how to add a store adapter (trivial)

### chargeguard-workbench (10 open)

**Features**

- [#1](https://github.com/Charge-Guard/chargeguard-workbench/issues/1) feat(ui): download a run as a shareable evidence bundle (medium)
- [#2](https://github.com/Charge-Guard/chargeguard-workbench/issues/2) feat(ui): compare two runs side by side (medium)
- [#5](https://github.com/Charge-Guard/chargeguard-workbench/issues/5) feat(ui): show restarts on the worker lanes (medium)

**Tests and CI**

- [#6](https://github.com/Charge-Guard/chargeguard-workbench/issues/6) test(tests): validate and explain suite totals (medium)
- [#10](https://github.com/Charge-Guard/chargeguard-workbench/issues/10) ci: run a real-browser smoke test in CI (high)

**Accessibility**

- [#3](https://github.com/Charge-Guard/chargeguard-workbench/issues/3) fix(a11y): make PASS and FAIL accessible without color (medium)
- [#9](https://github.com/Charge-Guard/chargeguard-workbench/issues/9) feat(a11y): add a compact view for narrow screens (medium)

**Documentation**

- [#4](https://github.com/Charge-Guard/chargeguard-workbench/issues/4) docs: explain the four levels with a worked example (medium)
- [#7](https://github.com/Charge-Guard/chargeguard-workbench/issues/7) docs: link failing checks to runner docs (trivial)
- [#8](https://github.com/Charge-Guard/chargeguard-workbench/issues/8) docs: persist the last file opened only in memory and say so (medium)

