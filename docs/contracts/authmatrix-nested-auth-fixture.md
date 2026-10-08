# Contract specification: AuthMatrix nested-auth fixture

Repository: `Auth-Matrix/authmatrix-core`, directory `fixtures/nested-auth/`. Status: shipped and deployed on testnet (see the release notes). Test fixture. Not audited. The contracts hold no balances.

## Purpose

AuthMatrix interprets Soroban authorization entries, including a nested invocation tree. To test that, a signed entry needs two levels: an outer call that requires `from`'s authorization, and an inner call that requires it again. The two contracts exist to produce that shape and nothing else.

## Contracts and dependency graph

| Contract | Responsibility |
|---|---|
| `Inner` | A `transfer` with the SEP-41 argument shape that only requires authorization and returns the amount. Moves no funds. |
| `Outer` | Requires `from`'s authorization, then forwards to `Inner.transfer`. A second, identically shaped function exists so "function name" mutations have a target. |

`Outer` calls `Inner`. Build and deploy `Inner` first. `Outer` receives the `Inner` address as an argument on every call, so it has no stored dependency and no constructor.

## Storage

None. Neither contract stores anything. No TTL work exists.

## Public functions

`Inner`

| Function | Parameters | Returns | Auth | Behavior |
|---|---|---|---|---|
| `transfer` | `from: Address`, `_to: Address`, `amount: i128` | `i128` | `from.require_auth()` | Returns `amount`. Does not read or write storage. |

`Outer`

| Function | Parameters | Returns | Auth | Behavior |
|---|---|---|---|---|
| `relay` | `inner: Address`, `from: Address`, `to: Address`, `amount: i128` | `i128` | `from.require_auth()` | Invokes `inner.transfer(from, to, amount)` and returns its result. |
| `relay_alt` | `inner: Address`, `from: Address`, `to: Address`, `amount: i128` | `i128` | `from.require_auth()` | Identical to `relay`. Exists only so a mutation can change the function name and invalidate the signature. |

## Events

None emitted.

## Why two auth requirements matter

`relay` requires authorization for the outer call and `Inner.transfer` requires it again for the nested call. A signed entry for `from` therefore contains a root invocation and one sub-invocation. The tests assert that both are present, that changing the recipient, amount, network, nonce, expiry, function or contract id invalidates the signature, and that both SDK adapters decode the entry identically.

## Mapping to the product flow

| Step in the AuthMatrix demo | Function |
|---|---|
| Build an entry for `relay` and sign it | `Outer.relay`, then `Inner.transfer` as the nested call |
| Mutate the function name | `Outer.relay_alt` |
| Run the entry on the host and on testnet `simulateTransaction` | both functions, both contracts |

## Deliberately absent

No balances, no token logic, no contract-account signers, no custom `__check_auth`, no delegated signing. Those are tracked as issues in `authmatrix-core`.
