# Submission text: ContractAtlas

For the Drips Wave application form. Nothing here has been submitted. No demo video is included, by design.

## 1. Pre-submission checks

- [x] Not in the approved list: the live list at `drips.network/wave/stellar/repos` (824 repositories, loaded in full on 2026-10-08) contains neither repository nor the organization `Contract-Atlas`.
- [ ] Install the Drips GitHub app on the `Contract-Atlas` organization (required for approval).
- [ ] Check the live per-user and per-organization application limits before applying (not published in the documentation).
- [ ] Re-read the current Wave terms on the day of submission.

## 2. Links

| Item | Link |
|---|---|
| Core repository | https://github.com/Contract-Atlas/contractatlas-core |
| App repository | https://github.com/Contract-Atlas/contractatlas-studio |
| Live app | https://contractatlas-studio-anasamasama.vercel.app |
| Documentation (core) | https://stellar-developer-tools.gitbook.io/contractatlas-core/ |
| Documentation (app) | https://stellar-developer-tools.gitbook.io/contractatlas-studio/ |
| Package | [`@anas.abubakar/contractatlas-core`](https://www.npmjs.com/package/@anas.abubakar/contractatlas-core) |
| Latest release (core) | https://github.com/Contract-Atlas/contractatlas-core/releases/latest |
| Latest release (app) | https://github.com/Contract-Atlas/contractatlas-studio/releases/latest |
| CI (core) | https://github.com/Contract-Atlas/contractatlas-core/actions |
| CI (app) | https://github.com/Contract-Atlas/contractatlas-studio/actions |
| Testnet contracts | [`CADRVGSP...EPIQ3BD`](https://stellar.expert/explorer/testnet/contract/CADRVGSPFVDYWRABKTEVETRVCKIADNF4XCQC73OIJPJQZOHG7EPIQ3BD) fixture A, upgraded from v1 to v2; [`CD2FBDVY...7J2EIZH`](https://stellar.expert/explorer/testnet/contract/CD2FBDVYS6TBDZNJPRUBVEY7TNCFJX36QJ6KQCUHXWG4IFFSR7J2EIZH) fixture B |

## 3. Project description (form field)

**ContractAtlas.** A protocol publishes an audit and a contract ID. Months later the contract may run different code, and the audit page says nothing about that. The protocol writes a manifest: for each contract, the WASM hash it expects, and which audits list that hash as reviewed. ContractAtlas reads the live executable hash from the ledger and reports one of four states per contract: match, drift, incomplete, unavailable. A failed read is never reported as drift, and a missing mapping from audit to artifact is never reported as audited. The same report appears in a terminal, in CI and on a public page. Built on: Soroban RPC `getLedgerEntries`, `@stellar/stellar-sdk` 17.2.1, TypeScript.

No figure on the scale of the problem is cited, because none was verified for this submission.

## 4. How the two repositories connect

`contractatlas-core` produces the report: the manifest schema, the checker, the CLI and the fixture contracts. `contractatlas-studio` is a static page that validates and displays that report. The page vendors the core's report schema and two recorded reports from a real testnet upgrade, stamped with the core's version and commit, and refuses a report that contradicts itself.

## 5. Neighboring approved work, stated plainly

`SaboLabs/soroban-devkit` covers release assurance more broadly; `Inferara/soroban-security-portal` is a vulnerability knowledge base. Neither compares a published manifest with the live ledger and reports unavailable separately from drift. ContractAtlas does not replace either.

## 6. What this does not claim

No safety score, no "audited" label, no inference of privileged roles, no source rebuild. A match means the live hash equals a hash an audit lists as reviewed, not that the audit covered dependencies or configuration.

No user adoption, outside review, audit, funding or Wave approval is claimed. None of those processes has been started.

## 7. Planned issues

These are the open issues already filed, grouped by area. Each has a Summary, acceptance criteria as checkboxes, a Tech Stack line and a complexity label that was chosen to match the effort.

### contractatlas-core (10 open)

**Features**

- [#1](https://github.com/Contract-Atlas/contractatlas-core/issues/1) feat(core): tell an archived contract instance apart from one that was never deployed (medium)
- [#2](https://github.com/Contract-Atlas/contractatlas-core/issues/2) feat(cli): add `contractatlas init` to scaffold a manifest from live contract IDs (medium)
- [#3](https://github.com/Contract-Atlas/contractatlas-core/issues/3) feat(cli): emit GitHub annotations and SARIF from `check` (medium)
- [#6](https://github.com/Contract-Atlas/contractatlas-core/issues/6) feat(adapters): separate transport failures from RPC answers in `unavailable` findings (medium)
- [#7](https://github.com/Contract-Atlas/contractatlas-core/issues/7) feat(cli): add `contractatlas diff` to compare two saved reports (medium)

**Security and hardening**

- [#5](https://github.com/Contract-Atlas/contractatlas-core/issues/5) feat(core): optionally fetch contract code to confirm hash-to-bytes integrity (medium)

**Tests and CI**

- [#4](https://github.com/Contract-Atlas/contractatlas-core/issues/4) feat(core): exercise one documented mainnet contract, read-only (medium)
- [#9](https://github.com/Contract-Atlas/contractatlas-core/issues/9) test(tests): fuzz and bound the manifest parser (medium)

**Documentation**

- [#8](https://github.com/Contract-Atlas/contractatlas-core/issues/8) docs: publish the manifest JSON Schema for editor validation (trivial)
- [#10](https://github.com/Contract-Atlas/contractatlas-core/issues/10) docs: write a nightly drift-check recipe for GitHub Actions (trivial)

### contractatlas-studio (10 open)

**Features**

- [#2](https://github.com/Contract-Atlas/contractatlas-studio/issues/2) feat(ui): make a comparison linkable (medium)
- [#3](https://github.com/Contract-Atlas/contractatlas-studio/issues/3) feat(ui): provide a print and PDF layout (trivial)
- [#4](https://github.com/Contract-Atlas/contractatlas-studio/issues/4) feat(ui): show a hash diff for drifting contracts (medium)
- [#6](https://github.com/Contract-Atlas/contractatlas-studio/issues/6) feat(ui): warn when a loaded report is older than the manifest it describes (medium)
- [#8](https://github.com/Contract-Atlas/contractatlas-studio/issues/8) feat(ui): localize dates and numbers without changing hashes or ledger values (trivial)
- [#9](https://github.com/Contract-Atlas/contractatlas-studio/issues/9) docs: explain every finding code in the page (trivial)

**Security and hardening**

- [#5](https://github.com/Contract-Atlas/contractatlas-studio/issues/5) feat(ui): open a report from a URL with explicit consent (medium)

**Tests and CI**

- [#7](https://github.com/Contract-Atlas/contractatlas-studio/issues/7) ci: add a bundle size and dependency budget (medium)
- [#10](https://github.com/Contract-Atlas/contractatlas-studio/issues/10) ci: run a real-browser smoke test in CI (high)

**Accessibility**

- [#1](https://github.com/Contract-Atlas/contractatlas-studio/issues/1) fix(a11y): audit the report page with a screen reader and the keyboard (medium)

