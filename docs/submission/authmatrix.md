# Submission text: AuthMatrix

For the Drips Wave application form. Nothing here has been submitted. No demo video is included, by design.

## 1. Pre-submission checks

- [x] Not in the approved list: the live list at `drips.network/wave/stellar/repos` (824 repositories, loaded in full on 2026-10-08) contains neither repository nor the organization `Auth-Matrix`.
- [ ] Install the Drips GitHub app on the `Auth-Matrix` organization (required for approval).
- [ ] Check the live per-user and per-organization application limits before applying (not published in the documentation).
- [ ] Re-read the current Wave terms on the day of submission.

## 2. Links

| Item | Link |
|---|---|
| Core repository | https://github.com/Auth-Matrix/authmatrix-core |
| App repository | https://github.com/Auth-Matrix/authmatrix-inspector |
| Live app | https://authmatrix-inspector-anasamasama.vercel.app |
| Documentation (core) | https://stellar-developer-tools.gitbook.io/authmatrix-core/ |
| Documentation (app) | https://stellar-developer-tools.gitbook.io/authmatrix-inspector/ |
| Package | [`@anas.abubakar/authmatrix-core`](https://www.npmjs.com/package/@anas.abubakar/authmatrix-core) |
| Latest release (core) | https://github.com/Auth-Matrix/authmatrix-core/releases/latest |
| Latest release (app) | https://github.com/Auth-Matrix/authmatrix-inspector/releases/latest |
| CI (core) | https://github.com/Auth-Matrix/authmatrix-core/actions |
| CI (app) | https://github.com/Auth-Matrix/authmatrix-inspector/actions |
| Testnet contracts | [`CCYEZ3EX...SOHF`](https://stellar.expert/explorer/testnet/contract/CCYEZ3EXL7OZAPMN2ARFZT23ODFOOT6QCPHWY3WBM7GGBFCDVYQ2SOHF) inner; [`CBHPE4LN...MFQK`](https://stellar.expert/explorer/testnet/contract/CBHPE4LNYOWPO3G6WAP64MDKENGX7LUR34KQUTWGAZED5MXTA7CAMFQK) outer; [`CASRT7GY...GS3MR`](https://stellar.expert/explorer/testnet/contract/CASRT7GY4N7FXHVW2FHUSPHJ3BO6WAYFVTA2BUMFOKTGE3XJKJMGS3MR) outer, second instance |

## 3. Project description (form field)

**AuthMatrix.** Soroban authorization entries are signed over a payload that includes the network, nonce, expiry and the whole invocation tree, and SDKs differ in how they build and read them. A wallet or developer cannot easily check what an entry actually authorizes. AuthMatrix ships language-neutral reviewed vectors, two independent adapters (TypeScript and Rust) that must produce identical canonical bytes, and a verifier against the real Soroban host and against testnet `simulateTransaction` in enforce mode. It decodes the authorizing address, network, credential type (including CAP-71 address-bound credentials), nonce, expiry and nested calls, decodes known SEP-41 arguments, and keeps unknown data raw. A mutation view shows that changing the recipient, amount, network, nonce, expiry, function or contract id invalidates the original signature. Built on: Soroban authorization (CAP-71), `@stellar/stellar-sdk`, Rust `stellar-xdr` and `ed25519-dalek`, the native Soroban host, testnet RPC.

No figure on the scale of the problem is cited, because none was verified for this submission.

## 4. How the two repositories connect

`authmatrix-core` holds the vectors, the two adapters, the conformance runner, the evidence and the nested-call fixture contracts. `authmatrix-inspector` is a static browser app that imports the core's tarball, verifies signatures locally and labels recorded host results as recorded.

## 5. Neighboring approved work, stated plainly

`soroauth/soroauth-go` builds, signs and inspects authorization entries in Go, including CAP-71 V2 and delegated credentials. It is the closest overlap and was not tested against. `dotandev/hintents` and `Toolbox-Lab/Prism` are transaction debuggers. AuthMatrix differs in shipping reviewed vectors with independent adapters and host evidence, and in the browser mutation view.

## 6. What this does not claim

Only classic ed25519 account signers are host-verified. Contract-account signers, custom `__check_auth` and delegated signing are decoded only. A decoded authorization is not a statement about what a contract does with it, and nothing here is audited.

No user adoption, outside review, audit, funding or Wave approval is claimed. None of those processes has been started.

## 7. Planned issues

These are the open issues already filed, grouped by area. Each has a Summary, acceptance criteria as checkboxes, a Tech Stack line and a complexity label that was chosen to match the effort.

### authmatrix-core (10 open)

**Features**

- [#1](https://github.com/Auth-Matrix/authmatrix-core/issues/1) feat(core): add contract-account signer vectors with a custom `__check_auth` (high)
- [#2](https://github.com/Auth-Matrix/authmatrix-core/issues/2) feat(core): verify delegated signing (`ADDRESS_WITH_DELEGATES`) on the host (high)
- [#4](https://github.com/Auth-Matrix/authmatrix-core/issues/4) feat(cli): add a third adapter in a different codebase (high)
- [#6](https://github.com/Auth-Matrix/authmatrix-core/issues/6) feat(core): extract authorization entries from a transaction or simulation response (medium)
- [#10](https://github.com/Auth-Matrix/authmatrix-core/issues/10) docs: expose the mutation engine as a library API with examples (medium)

**Tests and CI**

- [#3](https://github.com/Auth-Matrix/authmatrix-core/issues/3) test(tests): cover ed25519 edge-case encodings where adapters may differ (medium)
- [#8](https://github.com/Auth-Matrix/authmatrix-core/issues/8) test(tests): record negative host evidence for malformed entries (medium)

**Documentation**

- [#5](https://github.com/Auth-Matrix/authmatrix-core/issues/5) docs: give the public-network vector provenance (medium)
- [#7](https://github.com/Auth-Matrix/authmatrix-core/issues/7) docs: publish the vector and evidence schemas with stable ids (trivial)
- [#9](https://github.com/Auth-Matrix/authmatrix-core/issues/9) docs: document the key-derivation phrases and keep them out of real use (trivial)

### authmatrix-inspector (10 open)

**Features**

- [#1](https://github.com/Auth-Matrix/authmatrix-inspector/issues/1) feat(ui): decode delegated and contract-account credentials (high)
- [#2](https://github.com/Auth-Matrix/authmatrix-inspector/issues/2) feat(ui): import an entry from a transaction XDR or a simulation response (medium)
- [#3](https://github.com/Auth-Matrix/authmatrix-inspector/issues/3) feat(ui): add a wallet-style summary view (medium)
- [#5](https://github.com/Auth-Matrix/authmatrix-inspector/issues/5) feat(ui): explain network id and passphrase mismatches (trivial)
- [#6](https://github.com/Auth-Matrix/authmatrix-inspector/issues/6) feat(ui): copy canonical bytes and payload hash for adapter debugging (trivial)

**Tests and CI**

- [#7](https://github.com/Auth-Matrix/authmatrix-inspector/issues/7) test(tests): handle very large entries safely (medium)
- [#9](https://github.com/Auth-Matrix/authmatrix-inspector/issues/9) ci: update the pairing check when the core ships new vectors (medium)
- [#10](https://github.com/Auth-Matrix/authmatrix-inspector/issues/10) ci: run a real-browser smoke test in CI (high)

**Accessibility**

- [#4](https://github.com/Auth-Matrix/authmatrix-inspector/issues/4) fix(a11y): accessible mutation chips and diff view (medium)

**Documentation**

- [#8](https://github.com/Auth-Matrix/authmatrix-inspector/issues/8) docs: link recorded host results to the vector's evidence file (trivial)

