# Contract specification: UpgradeLab vault v1 and v2

Repository: `Upgrade-Lab/upgradelab-runner`, directory `fixtures/contracts/`. Status: shipped; compiled WASM is under `fixtures/wasm/`. Teaching fixture. Not audited. Not for production.

## Purpose

UpgradeLab rehearses a real upgrade path with named invariants. It needs a contract whose storage format changes between versions and whose migration can be broken in specific, documented ways, so each invariant has something real to catch.

## Contracts and dependency graph

| Contract | Responsibility |
|---|---|
| `VaultV1` | Balance vault in the original storage format. |
| `VaultV2` | Same entry points, a new per-account format, a batched `migrate`, and one build feature per deliberate defect. |

The graph is linear: v1 is deployed and seeded first, then `upgrade` swaps in the v2 WASM, then `migrate` runs. The contracts call nothing else.

## Storage

`VaultV1`

| Key | Value | Class |
|---|---|---|
| `Admin` | `Address` | instance |
| `Supply` | `i128` | persistent |
| `Holders` | `Vec<Address>` | persistent |
| `Balance(Address)` | `i128` | persistent |

`VaultV2` adds:

| Key | Value | Class |
|---|---|---|
| `BalanceV2(Address)` | `Account { amount: i128, deposits: u32 }` | persistent |
| `SchemaVersion` | `u32` | instance |

Reads fall back from `BalanceV2` to `Balance`, so state written by v1 and never touched after the upgrade coexists with state written by v2 ("mixed format"). Writes always use the new format and remove the legacy entry. No TTL extension is performed. Entries do not expire during a run, which the runner documents as a limitation.

## Errors (`#[contracterror]`, `u32`)

`AlreadyInitialized = 1`, `NotInitialized = 2`, `InsufficientBalance = 3`, `InvalidAmount = 4`.

## Public functions

Both versions

| Function | Parameters | Returns | Auth | Behavior |
|---|---|---|---|---|
| `initialize` | `admin: Address` | nothing | `admin.require_auth()` | Stores the admin, sets `Supply` to 0 and `Holders` to empty. A second call fails with `AlreadyInitialized`. |
| `deposit` | `from: Address`, `amount: i128` | nothing | `from.require_auth()` | `amount > 0` or `InvalidAmount`. Adds to the balance, to `Supply`, and records the holder once. |
| `withdraw` | `from: Address`, `amount: i128` | nothing | `from.require_auth()` | `amount > 0` or `InvalidAmount`; balance at least `amount` or `InsufficientBalance`. Subtracts from the balance and `Supply`. |
| `balance` | `who: Address` | `i128` | none | Effective balance. |
| `total_supply` | none | `i128` | none | `Supply`. |
| `admin` | none | `Address` | none | Stored admin or `NotInitialized`. |
| `holders` | none | `Vec<Address>` | none | Holder list. |
| `version` | none | `u32` | none | `1` in v1, `2` in v2. |
| `upgrade` | `new_wasm_hash: BytesN<32>` | nothing | stored admin's `require_auth()` | Calls `env.deployer().update_current_contract_wasm(new_wasm_hash)`. |

`VaultV2` only

| Function | Parameters | Returns | Auth | Behavior |
|---|---|---|---|---|
| `schema_version` | none | `u32` | none | `1` until every legacy entry is converted, then `2`. |
| `migrate` | `limit: u32` | `u32` | stored admin's `require_auth()` | Converts up to `limit` legacy balances to `BalanceV2` with `deposits: 0` and removes the legacy entry. Returns how many holders still have only a legacy entry. Sets `SchemaVersion` to 2 when none remain. Calling it again when nothing is left changes nothing. |

## Defect features (v2 only; enable at most one)

| Cargo feature | Defect | Invariants that fail in the recorded report |
|---|---|---|
| `broken-lose-balance` | The last holder's legacy entry is deleted without being written to the new format. | `seeded-balances-preserved-after-migration`, `supply-equals-sum-after-migration`, `migration-converts-every-entry` |
| `broken-double-balance` | Legacy entry left behind and reads sum both formats. | `partial-migration-preserves-balances`, `seeded-balances-preserved-after-migration`, `supply-equals-sum-after-migration`, `migration-converts-every-entry` |
| `broken-reinit` | `initialize` skips the already-initialized check. | `reinitialize-rejected`, `reinitialize-changes-nothing` |
| `broken-upgrade-auth` | `upgrade` never requires the admin's authorization. | `unauthorized-upgrade-rejected-no-auth` |
| `broken-not-idempotent` | After completion, each further `migrate` call increments every account's `deposits`. | `migration-idempotent` |

The invariant ids come from the recorded host reports in `evidence/host/`.

## Events

None emitted. The runner reads state through probes, not events.

## Mapping to the product flow

| Runner step | Function |
|---|---|
| Seed operations | `initialize`, `deposit` |
| Upgrade | `upgrade` |
| Migration | `migrate` (repeated, with a limit) |
| Probes at each checkpoint | `balance`, `total_supply`, `holders`, `schema_version`, `admin`, `version` |
