# Coordinated 0.1.1 patch release (2026-10-08)

Follows the external audit. v0.1.0 tags are preserved. Every 0.1.1 tag was cut from a commit with green CI; npm tarballs and the crate were verified against registry checksums (npm sha1 shasum, crates.io sha256) and clean-installed.

Pairings: anchortrace-studio vendors the exact published sdk tarball (sha256 in `pairing.json`, sdk tag v0.1.1 at the pinned commit). raillab-workbench and authmatrix-inspector vendor the published engine/core tarballs. contractatlas-studio, upgradelab-studio and chargeguard-workbench vendor the 0.1.1 core output; real recorded samples (ContractAtlas runs, UpgradeLab testnet runs) keep the tool version that recorded them, listed in `sampleReportsRecordedWith`.

Note: the upgradelab-studio v0.1.1 release was deleted and recreated once (minutes after creation, before use) to include a sample-label fix.

| Repo | v0.1.1 commit | Artifact sha256 |
|---|---|---|
| contractatlas-core | `a6d5bc6b88db` | `d34cc306f4d8e48f99da48745545577145cc529fa2d5925cc4b00e6e100290a2` |
| anchortrace-sdk | `e480415795b9` | `ebe3b7702cfb51bbfc63a0521deb4783d0795a077e6704a6688f7d0912c418e4` |
| raillab-engine | `9fefb742d345` | `41138a9343c829d28223e8aa290f38f1f57014acd24393415ee4b29086b85255` |
| authmatrix-core | `ed19e039f90f` | `c888ccbd5b7e89db7574130734f306b676468e3a687306a1c445f4ec563313ae` |
| chargeguard-runner | `957d8f222de3` | `929184853d6a86aca1e28069fa7fc4925748bbd8873ee05c34063b00360965ac` |
| upgradelab-runner | `a7f38ac6199b` | `c6fdbf78…59de (crate)` |
| eventparity-engine | `0f05a26856df` | `none` |
| anchortrace-studio | `9a0d9fbb03ab` | `none` |
| contractatlas-studio | `10e82b1ff98a` | `none` |
| upgradelab-studio | `4d9d80d118c9` | `none` |
| chargeguard-workbench | `7a82e4b99970` | `none` |
| raillab-workbench | `44f8a771e402` | `none` |
| authmatrix-inspector | `6dcd3b32f8e6` | `none` |

Production verification (real browser, 375 px): all seven demos loaded and showed no horizontal overflow; sample loading, malformed-input rejection and tamper rejection were exercised on ContractAtlas, EventParity, AuthMatrix, UpgradeLab and RailLab; the 0.1.1 pairing line was read on ContractAtlas, ChargeGuard and AuthMatrix. Known cosmetic: ContractAtlas logs a console notice that frame-ancestors is ignored in a meta CSP (the real header is set in vercel.json). 
