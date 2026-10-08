# Contract specification: ContractAtlas upgradeable fixture

Repository: `Contract-Atlas/contractatlas-core`, directory `fixtures/upgradeable-fixture/`. Status: shipped and deployed on testnet (see the `v0.1.1` release notes for the two deployed addresses). This is a **test fixture**. It is not audited and not for production.

## Purpose

The checker needs a real deployed contract whose executable can be upgraded, so the "match then drift" demo uses chain state and not a mock. The fixture does nothing else.

## Contracts

One contract, `UpgradeableFixture`. A single responsibility: hold an admin and allow that admin to replace the contract's executable.

There is no dependency graph. It calls no other contract.

## Build variants

The crate has one feature, `v2`. The default build reports version 1 and the `v2` build reports version 2. The two builds therefore have different WASM hashes, which is the whole point. Never add behavior to one build that the other lacks.

## Storage

| Type | Key | Value | Storage class |
|---|---|---|---|
| `enum DataKey` | `Admin` | `Address` | instance |

Instance storage is used because the admin is read on every `upgrade` call and lives and dies with the contract instance. No persistent or temporary storage is used. No TTL extension is performed, because the fixture is only read for the length of a demo.

## Public functions

| Function | Parameters | Returns | Auth | Behavior |
|---|---|---|---|---|
| `init` | `admin: Address` | nothing | none on the call itself | Stores `admin`. Panics with `"already initialised"` if an admin is already stored. |
| `upgrade` | `new_wasm_hash: BytesN<32>` | nothing | `admin.require_auth()` for the stored admin | Loads the stored admin (panics with `"not initialised"` if absent), requires its authorization, then calls `env.deployer().update_current_contract_wasm(new_wasm_hash)`. |
| `version` | none | `u32` | none | `2` when built with feature `v2`, otherwise `1`. |

Known limitation, deliberate: `init` has no `require_auth`. Whoever calls it first becomes admin. The fixture is deployed and initialized in one scripted step by its author. A production contract must not do this.

## Events

None emitted.

## Mapping to the product flow

| Step in the ContractAtlas demo | Function |
|---|---|
| Deploy fixture A and fixture B on v1 | `init` |
| Record the "match" report | `version` is not called; the checker reads the executable hash from the ledger |
| Upgrade fixture A to the v2 artifact | `upgrade` |
| Record the "drift" report | executable hash read again |

Every function maps to a step. There are no speculative functions.

## Tests (in the crate)

- `init_once_only`: a second `init` fails.
- `version_reports_build`: `version()` equals `2` under feature `v2`, otherwise `1`.

## Not covered, on purpose

- Authorization of `upgrade` against a wrong caller is exercised by the on-chain demo, not by a native test in this crate.
- No storage migration. This fixture changes code only.
