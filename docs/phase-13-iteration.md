# Phase 13: how to handle changes after a Wave approval

This is the working procedure for any new gap found once a repository is approved: a missing feature, an unsupported asset type, an edge case. It applies to all fourteen repositories. Nothing here has been used yet, because nothing has been approved.

## 1. Scope it before writing it

Decide which of three sizes it is, and say so in the issue before anyone builds:

| Size | Test | Complexity label |
|---|---|---|
| Quick addition | One module, no schema or report change, no change to the paired repository | trivial or medium |
| Core change | Touches the report schema, a verdict rule, or a pinned dependency | medium or high |
| Spans both repositories | The core changes what the app reads | high, as two linked issues |

If it changes a report schema or a verdict meaning, it is never a quick addition.

## 2. Spans both repositories: two issues, linked both ways

Every project is a core repository plus an app repository, and the app vendors a tarball or schema from the core. So:

1. Open the **core** issue first. Its acceptance criteria include a release (a tag, and a published package where one exists).
2. Open the **app** issue with `Depends on: <link to the core issue>` in the body and in the "Where this lives" section of the template.
3. Add the reverse link to the core issue ("Unblocks: ...").
4. The app issue stays blocked until the core release exists and its checksum is known. The app then re-vendors, updates its pairing record and `compat.json`, and ships.

Never merge an app change that reads a field the released core does not yet produce. That sequencing mistake looks like a regression and is not one.

## 3. Write the issue with the original rigor

Use the **Scoped work** issue template that now exists in every repository. It requires:

- **Summary** and **Why it matters**: what changes and who it affects.
- **Where this lives** with a `Depends on` field.
- **Scoped options**, only where there is a real design decision, with a recommendation.
- **Acceptance Criteria** as checkboxes, always including tests, CI, and docs or changelog.
- **Tech Stack**.
- **Complexity**, matched honestly to effort. Do not inflate it. The Drips guidance says inflated or underpriced points erode trust.

An issue must fit one Wave cycle. If it does not, split it. Do not publish low-effort issues only to have content available.

## 4. Confirm before building

Before any code, write down in the issue:

1. Which repository and which module the change belongs to.
2. Which existing decision record (`docs/adr/`) it depends on or would contradict. If it contradicts one, write a new decision record first.
3. Whether the paired repository needs a release first.

## 5. After the change

- Core: bump the version, update `CHANGELOG.md`, tag, release with checksums, and publish the package if the repository has one.
- App: re-vendor, run the pairing check, update `compat.json`, and let CI deploy.
- Documentation: the GitBook source is the `gitbook/` folder, so the same pull request updates the docs. The published site syncs from `main`.
- Record the pairing in the portfolio repository's release record.

## Complexity map for the examples already open

The open issues already follow this. For example, the CAP-67 events adapter in `eventparity-engine` is **high** and needs a matching display change in `eventparity-studio` afterward; a new finding code in `contractatlas-core` is **medium** and needs the studio to learn it (an open issue in the studio proposes a test that fails when the core adds a code the studio does not explain).
