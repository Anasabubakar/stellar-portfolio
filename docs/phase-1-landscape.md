# Phase 1: ecosystem landscape (2026-10-08)

Everything here was fetched live on 2026-10-08. Sources are listed at the end. Counts that come from keyword matching on repository names are marked as rough, because a name does not always say what a repository does.

## What the Stellar stack offers now

Taken from the documentation and repository descriptions fetched for this review, not from memory:

- **Soroban smart contracts** on Protocol 29 testnet at the time of the work. Contract upgrade is `update_current_contract_wasm`. Authorization entries carry address-bound credentials under CAP-71.
- **Soroban RPC** for contract reads, simulation and `getTransactions`, with a limited retention window. **Horizon** still serves classic operations and history.
- **SEP standards** that these projects touch: SEP-24 (interactive deposit and withdrawal), SEP-10 (web authentication), SEP-41 (token interface).
- **Stellar Asset Contract** for classic assets inside Soroban, and the **MPP** and **x402** payment flows that other approved repositories already build on.

## What the Wave program lists

The approved list at `drips.network/wave/stellar/repos` showed **824 repositories**. Two program tags appear on the featured entries: the Stellar Agentic Hackathon and Build On Stellar Hackathon (IBW 2026). Several repositories carry 2x or 4x point multipliers.

Rough category counts from repository names (a repository can match more than one):

| Domain | Repositories (rough) | Reading |
|---|---:|---|
| Payments, remittance, wallets | 79 | Crowded |
| Developer tooling, SDKs, explorers, indexers | 93 | Large, but mostly application-side helpers and cost or lint tools |
| Escrow and trust | 42 | Crowded; Trustless Work and SafeTrust are the reference points |
| DeFi, lending, yield | 36 | Crowded |
| DAO, governance, streaming, payroll | 35 | Crowded |
| AI agents and x402/MPP | 26 | Growing |
| Education and learning | 23 | Moderate |
| Prediction markets | 23 | Moderate |
| Identity, credentials, compliance | 22 | Moderate |
| Crowdfunding, grants, bounties | 19 | Moderate |
| Real-world assets, carbon, agriculture | 18 | Moderate |
| Health and insurance | 18 | Moderate |
| NFT, gaming, social | 16 | Moderate |
| Anchors and SEP tooling | 5 | Thin |

## Where the seven projects sit

Descriptions below were read from each repository's GitHub description on the same day. "Overlap" means the approved repository addresses a neighboring problem, not the same one.

| Project | Closest approved repositories | What they do | What is left open |
|---|---|---|---|
| ContractAtlas | `SaboLabs/soroban-devkit` (release assurance, "inspect, verify, audit"), `Inferara/soroban-security-portal` | Release checks and a vulnerability knowledge base | A declared-versus-live comparison that treats a failed read as unavailable and never equates a hash match with audit coverage |
| AnchorTrace | `StellarCommons/Stellar-Explain` (explains a transaction hash in plain English), `ceejaylaboratory/AnchorPoint` (anchor dashboard) | Transaction explanation and anchor-side dashboards | Reconciling a SEP-24 record against chain evidence with explicit outcomes such as `ambiguous` and `insufficient_evidence` |
| EventParity | `Soroban-Pulse/SorobanPulse`, `SoroScan/soroscan` (event indexers), `StellarCanary/Protocol-Canary` | Indexing and protocol compatibility checks | Comparing two payment streams over one ledger range with retention gaps reported as gaps |
| RailLab | `Anchor-kit/anchor-kit`, `abore9769/SorobanAnchor`, `anchor-tools/stellar-toml-lint` | Building anchors, linting `stellar.toml` | Consumer-side incident simulation: delayed, repeated and reordered anchor responses against a wallet |
| AuthMatrix | `soroauth/soroauth-go` ("build, sign, and inspect Soroban authorization entries in Go", including CAP-71 V2 and delegated credentials), `dotandev/hintents`, `Toolbox-Lab/Prism` (transaction debuggers) | A Go library and transaction debuggers | Language-neutral reviewed vectors with independent adapters, plus a browser inspector with a signature mutation view. `soroauth-go` is the closest overlap and should be compared directly before any claim of novelty |
| ChargeGuard | `winsznx/routedock` (one `client.pay()` over x402 and MPP), `accensa/x402-facilitator-stellar` | Client and facilitator layers | Testing replay protection across two workers sharing one store |
| UpgradeLab | `ShippedLabs/soroban-upgrade-safeguard` (compares WASM builds statically), `benelabs/crucible` (test utilities), `Tollcraft/soroban-budget-assert` (cost assertions) | Static upgrade diffing, test helpers, cost checks | Executing an upgrade path with named invariants on compiled WASM and reporting execution categories separately |

## What the SDF funding pages say

- The SCF Build Award offers up to **$150K in XLM** per project, across an Open Track, an Integration Track and an RFP Track. SCF #46 closes on **8 November 2026**. Stated priorities are ecosystem infrastructure, DeFi applications and solutions for global needs, with no narrower list for 2026.
- A search for the foundation's 2026 plans returned a Soroban adoption fund and a 2026 protocol roadmap. Those results came from third-party news pages, so they are leads, not citations to rely on.

## Wave program rules that affect the repositories

From the Drips maintainer documentation:

- Issues carry a complexity level: **Trivial (100 points)**, **Medium (150)**, **High (200)**. Issues added through a GitHub label default to Trivial, and the level is raised in the Drips app.
- Good issues state the "why", give acceptance criteria, point at relevant files, and fit one Wave cycle. Low-effort issues posted only to have content are discouraged, as is inflating complexity.
- Repository applications are limited per user, per organization or both, with the numbers set per program and not published in the documentation. Rejected applications count toward the cycle.
- Approval requires installing the Drips GitHub app on the organization.

## Consequences for the seven repositories

1. **Do not call any of the seven new.** AuthMatrix and UpgradeLab have named neighbors that are active and approved. The decision records already compare them. The submission text should say what is different and stop there.
2. **The thinnest category is anchors and SEP tooling (about 5 repositories).** AnchorTrace and RailLab sit in it, and both are consumer-side, which the anchor-building repositories are not.
3. **Seven repositories from one owner may hit a per-user or per-organization cap.** The seven GitHub organizations help if the cap is per organization. Check the live limit before applying.
4. **Nothing here is a funding or approval prediction.** No Wave or SCF process has been started.

## Sources

- Approved list: https://www.drips.network/wave/stellar/repos (824 repositories, loaded in full in a browser)
- Maintainer documentation: https://docs.drips.network/wave/maintainers/participating-in-a-wave/ and https://docs.drips.network/wave/maintainers/repo-application-limits/ and https://docs.drips.network/wave/maintainers/faq/
- Issue guidance: https://www.drips.network/blog/posts/creating-meaningful-issues
- SCF awards: https://communityfund.stellar.org/awards
- Repository descriptions: GitHub API, fetched 2026-10-08
