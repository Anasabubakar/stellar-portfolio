# Submission text: EventParity

For the Drips Wave application form. Nothing here has been submitted. No demo video is included, by design.

## 1. Pre-submission checks

- [x] Not in the approved list: the live list at `drips.network/wave/stellar/repos` (824 repositories, loaded in full on 2026-10-08) contains neither repository nor the organization `Event-Parity`.
- [ ] Install the Drips GitHub app on the `Event-Parity` organization (required for approval).
- [ ] Check the live per-user and per-organization application limits before applying (not published in the documentation).
- [ ] Re-read the current Wave terms on the day of submission.

## 2. Links

| Item | Link |
|---|---|
| Core repository | https://github.com/Event-Parity/eventparity-engine |
| App repository | https://github.com/Event-Parity/eventparity-studio |
| Live app | https://eventparity-studio-anasamasama.vercel.app |
| Documentation (core) | https://stellar-developer-tools.gitbook.io/eventparity-engine/ |
| Documentation (app) | https://stellar-developer-tools.gitbook.io/eventparity-studio/ |
| Package | Go module `github.com/Event-Parity/eventparity-engine` (no registry package) |
| Latest release (core) | https://github.com/Event-Parity/eventparity-engine/releases/latest |
| Latest release (app) | https://github.com/Event-Parity/eventparity-studio/releases/latest |
| CI (core) | https://github.com/Event-Parity/eventparity-engine/actions |
| CI (app) | https://github.com/Event-Parity/eventparity-studio/actions |
| On-chain contracts | None. This project deploys no contract of its own; its evidence is recorded transactions and ledgers. |

## 3. Project description (form field)

**EventParity.** Teams moving payment ingestion from Horizon to Soroban RPC need to know whether the new pipeline lost or duplicated payments, and RPC keeps only a limited window of history. EventParity fetches classic payments for one declared ledger range from both sources, or reads a candidate stream, and compares them on exact fields: ledger, transaction, operation, accounts, asset with issuer, amount. Each side's coverage is tracked, so a ledger one source could not serve is reported as a coverage gap and never as a missing payment. The verdict is parity, differences or inconclusive, and inconclusive is explicitly not a pass. Built on: Horizon and Soroban RPC `getTransactions` with XDR decoding, Go 1.25, `go-stellar-sdk`, and a recorded testnet corpus of nine real transactions with independent ground truth.

No figure on the scale of the problem is cited, because none was verified for this submission.

## 4. How the two repositories connect

`eventparity-engine` is the Go comparison core and CLI. `eventparity-studio` is a static report explorer. It vendors the engine's report schema and three recorded reports, validates every report against exact coverage rules, and shows a pairing note when the engine version differs.

## 5. Neighboring approved work, stated plainly

`Soroban-Pulse/SorobanPulse` and `SoroScan/soroscan` are event indexers, and `StellarCanary/Protocol-Canary` checks protocol compatibility. EventParity compares two payment streams over a range and reports what each could and could not see.

## 6. What this does not claim

RPC does not reproduce every Horizon effect, balance or history record, and the tool does not claim it does. Only classic `payment` operations are compared one by one. Tested live on testnet only.

No user adoption, outside review, audit, funding or Wave approval is claimed. None of those processes has been started.

## 7. Planned issues

These are the open issues already filed, grouped by area. Each has a Summary, acceptance criteria as checkboxes, a Tech Stack line and a complexity label that was chosen to match the effort.

### eventparity-engine (10 open)

**Features**

- [#1](https://github.com/Event-Parity/eventparity-engine/issues/1) feat(adapters): add an adapter that reads CAP-67 events from RPC (high)
- [#3](https://github.com/Event-Parity/eventparity-engine/issues/3) feat(core): compare path payments as a first-class operation (high)
- [#5](https://github.com/Event-Parity/eventparity-engine/issues/5) feat(adapters): honor `Retry-After` in the RPC adapter and expose the retry settings (medium)
- [#6](https://github.com/Event-Parity/eventparity-engine/issues/6) feat(core): resume an interrupted fetch from the checkpoint file (medium)

**Tests and CI**

- [#2](https://github.com/Event-Parity/eventparity-engine/issues/2) test(tests): exercise one public mainnet provider (medium)
- [#8](https://github.com/Event-Parity/eventparity-engine/issues/8) test(tests): make HTML reports deterministic (medium)
- [#9](https://github.com/Event-Parity/eventparity-engine/issues/9) test(tests): fuzz the Horizon and RPC response decoders (medium)

**Documentation**

- [#4](https://github.com/Event-Parity/eventparity-engine/issues/4) docs: measure memory and time on a full-day range and document the limits (medium)
- [#7](https://github.com/Event-Parity/eventparity-engine/issues/7) docs: validate input streams against a published JSON Lines schema (medium)
- [#10](https://github.com/Event-Parity/eventparity-engine/issues/10) docs: write a migration guide: from Horizon ingestion to RPC (medium)

### eventparity-studio (10 open)

**Features**

- [#1](https://github.com/Event-Parity/eventparity-studio/issues/1) feat(ui): deep links for differences and filters (medium)
- [#2](https://github.com/Event-Parity/eventparity-studio/issues/2) feat(ui): compare two reports over time (medium)
- [#4](https://github.com/Event-Parity/eventparity-studio/issues/4) feat(ui): copy a difference as an issue-ready Markdown block (trivial)
- [#5](https://github.com/Event-Parity/eventparity-studio/issues/5) feat(ui): paginate and virtualize long difference lists (medium)
- [#8](https://github.com/Event-Parity/eventparity-studio/issues/8) feat(ui): handle report version upgrades gracefully (medium)
- [#9](https://github.com/Event-Parity/eventparity-studio/issues/9) feat(ui): print-friendly layout for reports (trivial)

**Security and hardening**

- [#6](https://github.com/Event-Parity/eventparity-studio/issues/6) feat(ui): verify stream hashes against supplied streams (medium)

**Tests and CI**

- [#10](https://github.com/Event-Parity/eventparity-studio/issues/10) ci: run a real-browser smoke test in CI (high)

**Accessibility**

- [#3](https://github.com/Event-Parity/eventparity-studio/issues/3) fix(a11y): make the coverage bars accessible (medium)

**Documentation**

- [#7](https://github.com/Event-Parity/eventparity-studio/issues/7) docs: explain coverage gap reasons from the engine (trivial)

