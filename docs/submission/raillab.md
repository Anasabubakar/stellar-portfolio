# Submission text: RailLab

For the Drips Wave application form. Nothing here has been submitted. No demo video is included, by design.

## 1. Pre-submission checks

- [x] Not in the approved list: the live list at `drips.network/wave/stellar/repos` (824 repositories, loaded in full on 2026-10-08) contains neither repository nor the organization `Rail-L-b`.
- [ ] Install the Drips GitHub app on the `Rail-L-b` organization (required for approval).
- [ ] Check the live per-user and per-organization application limits before applying (not published in the documentation).
- [ ] Re-read the current Wave terms on the day of submission.

## 2. Links

| Item | Link |
|---|---|
| Core repository | https://github.com/Rail-L-b/raillab-engine |
| App repository | https://github.com/Rail-L-b/raillab-workbench |
| Live app | https://raillab-workbench-anasamasama.vercel.app |
| Documentation (core) | https://stellar-developer-tools.gitbook.io/raillab-engine/ |
| Documentation (app) | https://stellar-developer-tools.gitbook.io/raillab-workbench/ |
| Package | [`@anas.abubakar/raillab-engine`](https://www.npmjs.com/package/@anas.abubakar/raillab-engine) |
| Latest release (core) | https://github.com/Rail-L-b/raillab-engine/releases/latest |
| Latest release (app) | https://github.com/Rail-L-b/raillab-workbench/releases/latest |
| CI (core) | https://github.com/Rail-L-b/raillab-engine/actions |
| CI (app) | https://github.com/Rail-L-b/raillab-workbench/actions |
| On-chain contracts | None. This project deploys no contract of its own; its evidence is recorded transactions and ledgers. |

## 3. Project description (form field)

**RailLab.** Wallets that talk to a SEP-24 anchor break in the same few ways: they tell the user a withdrawal is complete while the anchor still says pending, they apply a repeated or reordered status twice, or they give up after one outage. These incidents are hard to reproduce against a real anchor. RailLab is a scenario server with a virtual clock, a seeded fault schedule and assertions. It serves a documented subset of SEP-24 withdrawal polling with delayed, repeated, reordered and failing responses, stale authentication and mismatched references. The same scenario and seed give an identical timeline. Rules are labelled as a SEP-24 requirement or an application policy, with evidence. Any consumer in any language can be tested through a command contract. Built on: SEP-24, TypeScript, a deterministic virtual clock and a seeded PRNG.

No figure on the scale of the problem is cited, because none was verified for this submission.

## 4. How the two repositories connect

`raillab-engine` is the scenario server, CLI, rules and reference clients. `raillab-workbench` runs the real engine in the browser: a defective and a corrected client side by side, per-rule mutants, a swimlane and a full timeline. It consumes a committed engine tarball with a stamped SHA-256 and verifies saved sessions by recomputing their results.

## 5. Neighboring approved work, stated plainly

`Anchor-kit/anchor-kit` and `abore9769/SorobanAnchor` help build anchors, and `anchor-tools/stellar-toml-lint` lints `stellar.toml`. RailLab is on the other side: it is for the wallet that consumes an anchor.

## 6. What this does not claim

Simulated anchor and simulated banking only. Not a conformance test for anchors and no claim of parity with a production anchor. `POST /auth` simulates the outcome of SEP-10 and does not implement challenge signing.

No user adoption, outside review, audit, funding or Wave approval is claimed. None of those processes has been started.

## 7. Planned issues

These are the open issues already filed, grouped by area. Each has a Summary, acceptance criteria as checkboxes, a Tech Stack line and a complexity label that was chosen to match the effort.

### raillab-engine (10 open)

**Features**

- [#1](https://github.com/Rail-L-b/raillab-engine/issues/1) feat(core): add deposit flow scenarios (high)
- [#2](https://github.com/Rail-L-b/raillab-engine/issues/2) feat(core): offer a real SEP-10 challenge flow as an option (high)
- [#3](https://github.com/Rail-L-b/raillab-engine/issues/3) feat(core): model webhook and callback faults (high)
- [#5](https://github.com/Rail-L-b/raillab-engine/issues/5) feat(core): report which rules a scenario actually exercised (medium)
- [#8](https://github.com/Rail-L-b/raillab-engine/issues/8) feat(core): windows support for the external consumer runner (high)
- [#9](https://github.com/Rail-L-b/raillab-engine/issues/9) feat(core): record and replay a real anchor's responses as a scenario (medium)

**Tests and CI**

- [#7](https://github.com/Rail-L-b/raillab-engine/issues/7) test(tests): make server shutdown and port handling robust in tests (medium)

**Documentation**

- [#4](https://github.com/Rail-L-b/raillab-engine/issues/4) docs: ship consumer examples in other languages (medium)
- [#6](https://github.com/Rail-L-b/raillab-engine/issues/6) docs: write a scenario authoring guide with annotated examples (medium)
- [#10](https://github.com/Rail-L-b/raillab-engine/issues/10) docs: expose the virtual clock to consumers (trivial)

### raillab-workbench (10 open)

**Features**

- [#1](https://github.com/Rail-L-b/raillab-workbench/issues/1) feat(ui): edit faults visually instead of raw JSON (medium)
- [#2](https://github.com/Rail-L-b/raillab-workbench/issues/2) feat(ui): share a scenario and seed by URL (medium)
- [#4](https://github.com/Rail-L-b/raillab-workbench/issues/4) feat(ui): explain a rule failure in context on the timeline (medium)
- [#5](https://github.com/Rail-L-b/raillab-workbench/issues/5) feat(ui): compare two sessions (medium)
- [#6](https://github.com/Rail-L-b/raillab-workbench/issues/6) feat(ui): warn before opening a session saved by a different engine version (medium)
- [#7](https://github.com/Rail-L-b/raillab-workbench/issues/7) feat(ui): add a seed explorer (medium)
- [#9](https://github.com/Rail-L-b/raillab-workbench/issues/9) feat(ui): persist the last run locally with a visible clear control (medium)

**Tests and CI**

- [#10](https://github.com/Rail-L-b/raillab-workbench/issues/10) ci: run a real-browser smoke test in CI (high)

**Accessibility**

- [#3](https://github.com/Rail-L-b/raillab-workbench/issues/3) fix(a11y): make the swimlane diagram accessible (medium)
- [#8](https://github.com/Rail-L-b/raillab-workbench/issues/8) docs: show what the user was told in plain language (medium)

