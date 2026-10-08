# Submission text: AnchorTrace

For the Drips Wave application form. Nothing here has been submitted. No demo video is included, by design.

## 1. Pre-submission checks

- [x] Not in the approved list: the live list at `drips.network/wave/stellar/repos` (824 repositories, loaded in full on 2026-10-08) contains neither repository nor the organization `Anchor-Trace`.
- [ ] Install the Drips GitHub app on the `Anchor-Trace` organization (required for approval).
- [ ] Check the live per-user and per-organization application limits before applying (not published in the documentation).
- [ ] Re-read the current Wave terms on the day of submission.

## 2. Links

| Item | Link |
|---|---|
| Core repository | https://github.com/Anchor-Trace/anchortrace-sdk |
| App repository | https://github.com/Anchor-Trace/anchortrace-studio |
| Live app | https://anchortrace-studio-anasamasama.vercel.app |
| Documentation (core) | https://stellar-developer-tools.gitbook.io/anchortrace-sdk/ |
| Documentation (app) | https://stellar-developer-tools.gitbook.io/anchortrace-studio/ |
| Package | [`@anas.abubakar/anchortrace-sdk`](https://www.npmjs.com/package/@anas.abubakar/anchortrace-sdk) |
| Latest release (core) | https://github.com/Anchor-Trace/anchortrace-sdk/releases/latest |
| Latest release (app) | https://github.com/Anchor-Trace/anchortrace-studio/releases/latest |
| CI (core) | https://github.com/Anchor-Trace/anchortrace-sdk/actions |
| CI (app) | https://github.com/Anchor-Trace/anchortrace-studio/actions |
| On-chain contracts | None. This project deploys no contract of its own; its evidence is recorded transactions and ledgers. |

## 3. Project description (form field)

**AnchorTrace.** When a customer says a withdrawal or deposit went wrong, a support team has to line up an anchor's SEP-24 record with what happened on chain. Doing it by hand is slow, and the usual shortcut ("the payment is on chain, so it is done") is wrong, because the bank or mobile-money leg is never visible there. AnchorTrace reads a SEP-24 transaction record and Horizon evidence and returns one of six outcomes: matched, pending, discrepant, ambiguous, unsupported, insufficient evidence. It compares destination, memo, issuer-aware asset and exact amount under an explicit fee policy, preserves transaction and operation identity, and says what would change each verdict. A failed read is insufficient evidence, never a mismatch, and a match never implies a bank payout. Built on: SEP-24, Horizon (read-only), TypeScript, decimal-safe arithmetic on stroops.

No figure on the scale of the problem is cited, because none was verified for this submission.

## 4. How the two repositories connect

`anchortrace-sdk` is the engine and CLI. `anchortrace-studio` is a browser investigation UI that runs the same engine locally on pasted records and evidence. The studio bundles a committed tarball of the SDK, with its SHA-256 and the SDK's git tag and commit recorded, and a build-time check fails if they drift.

## 5. Neighboring approved work, stated plainly

`StellarCommons/Stellar-Explain` explains a transaction hash in plain language and `ceejaylaboratory/AnchorPoint` is an anchor-side dashboard. AnchorTrace starts from an anchor's own record and asks whether chain evidence supports it.

## 6. What this does not claim

Classic payment operations only. Path payments, claimable balances and Soroban transfers are reported unsupported so a person decides. The shipped records are synthetic, and no anchor or support team has used the tool.

No user adoption, outside review, audit, funding or Wave approval is claimed. None of those processes has been started.

## 7. Planned issues

These are the open issues already filed, grouped by area. Each has a Summary, acceptance criteria as checkboxes, a Tech Stack line and a complexity label that was chosen to match the effort.

### anchortrace-sdk (10 open)

**Features**

- [#1](https://github.com/Anchor-Trace/anchortrace-sdk/issues/1) feat(cli): support path payments behind an explicit flag (high)
- [#2](https://github.com/Anchor-Trace/anchortrace-sdk/issues/2) feat(core): check converted amounts when the record names two assets (high)
- [#4](https://github.com/Anchor-Trace/anchortrace-sdk/issues/4) feat(core): scan an account's history to find a deposit without a transaction hash (high)
- [#6](https://github.com/Anchor-Trace/anchortrace-sdk/issues/6) feat(core): suggest the matching fee policy when an amount is off by exactly the fee (medium)

**Security and hardening**

- [#3](https://github.com/Anchor-Trace/anchortrace-sdk/issues/3) feat(adapters): corroborate a live read across more than one Horizon instance (high)
- [#5](https://github.com/Anchor-Trace/anchortrace-sdk/issues/5) feat(core): harden the redactor against free-text identifiers (medium)

**Tests and CI**

- [#7](https://github.com/Anchor-Trace/anchortrace-sdk/issues/7) test(tests): test memo handling across `text`, `id` and `hash` types (medium)
- [#8](https://github.com/Anchor-Trace/anchortrace-sdk/issues/8) test(tests): property-test decimal handling at stroop precision (medium)
- [#9](https://github.com/Anchor-Trace/anchortrace-sdk/issues/9) test(tests): prove status updates are order-independent with generated permutations (medium)
- [#10](https://github.com/Anchor-Trace/anchortrace-sdk/issues/10) ci: fail CI if the browser-safe entry point imports Node built-ins (trivial)

### anchortrace-studio (10 open)

**Features**

- [#1](https://github.com/Anchor-Trace/anchortrace-studio/issues/1) feat(ui): move reconciliation to a Web Worker for large evidence (high)
- [#4](https://github.com/Anchor-Trace/anchortrace-studio/issues/4) feat(ui): export a case bundle: record, evidence and report in one file (medium)
- [#6](https://github.com/Anchor-Trace/anchortrace-studio/issues/6) feat(ui): show the effect of each verdict option before running (medium)

**Security and hardening**

- [#3](https://github.com/Anchor-Trace/anchortrace-studio/issues/3) feat(ui): import evidence from a Horizon URL with explicit consent (medium)

**Tests and CI**

- [#10](https://github.com/Anchor-Trace/anchortrace-studio/issues/10) test(tests): track bundled sample drift against the SDK (medium)

**Accessibility**

- [#2](https://github.com/Anchor-Trace/anchortrace-studio/issues/2) test(tests): verify cross-browser and screen-reader behavior (medium)
- [#5](https://github.com/Anchor-Trace/anchortrace-studio/issues/5) fix(a11y): manage focus and announce results after Reconcile (trivial)
- [#8](https://github.com/Anchor-Trace/anchortrace-studio/issues/8) feat(a11y): add a dark theme that preserves status contrast (medium)

**Documentation**

- [#7](https://github.com/Anchor-Trace/anchortrace-studio/issues/7) docs: persist nothing by default, and say so on the page (medium)
- [#9](https://github.com/Anchor-Trace/anchortrace-studio/issues/9) docs: add example sets for the "explain what would change it" text (medium)

