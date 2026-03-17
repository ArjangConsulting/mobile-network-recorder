---
name: api-trace-sdk-maintainer
description: Maintain the APITrace Swift and Kotlin SDKs with cross-platform parity, stable export behavior, and synchronized docs. Use when a task touches public API, redaction, capture flow, JSON export, or integration guidance in this repo.
---

# APITrace SDK Maintainer

Use this skill when work touches:

- both platforms
- one platform's public API or exported record format
- bootstrap/install behavior
- README examples or integration guidance

## Workflow

1. Classify the change.
   - Swift-only work stays in `ios/` (submodule).
   - Kotlin-only work stays in `android/` (submodule).
   - Shared-contract work requires checking both implementations.
2. Map the equivalent modules before editing.
   - `APITraceCore` <-> `api-trace-core`
   - `APITraceDebug` <-> `api-trace-debug`
   - `APITraceNoop` <-> `api-trace-noop`
3. Preserve semantic parity.
   - Keep capture lifecycle, redaction rules, and request/response modeling aligned.
   - Respect existing intentional divergence: iOS serializes `startedAt` as ISO 8601, Android serializes `startedAtEpochMs` as epoch milliseconds.
4. Commit in submodules first.
   - Make changes inside the `ios/` or `android/` submodule directory.
   - Commit and push in the submodule.
   - Then update the submodule pointer in this container repo.
5. Validate.
   - Run `swift test` in `ios/`.
   - If Android changed, try Gradle from `android/`. If the environment blocks it, report the exact blocker.
6. Update docs.
   - Adjust `README.md` and the affected platform README files for public-facing changes.

## Read When Needed

- For the current parity map and doc checklist, read `references/parity.md`.

## Avoid

- Renaming public symbols casually.
- Changing JSON keys or redaction semantics on only one platform without documenting the reason.
- Writing guidance that assumes this repo contains a host app.
