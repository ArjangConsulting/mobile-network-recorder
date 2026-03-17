# AGENTS.md

This repository is a container for two SDK submodules that implement the same API tracing concept:

- `ios/`: Swift Package Manager package ([ios-network-recorder](https://github.com/ArjangConsulting/ios-network-recorder))
- `android/`: Gradle multi-module Android library ([android-network-recorder](https://github.com/ArjangConsulting/android-network-recorder))

Both are Git submodules. Each SDK has its own standalone repo with self-contained agent docs.

This file is the canonical agent guide for the container repo. It focuses on cross-platform orchestration.

## Scope

- Cross-platform parity, shared architecture, and submodule coordination.
- For iOS-specific work, see `ios/AGENTS.md` in the submodule.
- For Android-specific work, see `android/AGENTS.md` in the submodule.

## Repo Map

- `ios/Package.swift`: Swift package definition
- `ios/Sources/APITraceCore`: shared Swift public API and models
- `ios/Sources/APITraceDebug`: Swift debug capture backend
- `ios/Sources/APITraceNoop`: Swift release-safe no-op bootstrap
- `ios/Tests/APITraceCoreTests`: current Swift test coverage
- `android/settings.gradle.kts`: Android module graph
- `android/api-trace-core`: Kotlin public API and models
- `android/api-trace-debug`: Kotlin OkHttp capture backend
- `android/api-trace-noop`: Kotlin release-safe no-op bootstrap

## Working Rules

- Treat capture behavior as a cross-platform contract. If a change affects redaction, capture lifecycle, exported records, or bootstrap/install behavior, inspect both the Swift and Kotlin implementations.
- Keep semantic parity, not forced textual parity. Current intentional difference: iOS exports `startedAt` as ISO 8601, while Android exports `startedAtEpochMs` as epoch milliseconds.
- Keep the module mapping aligned:
  - `APITraceCore` <-> `api-trace-core`
  - `APITraceDebug` <-> `api-trace-debug`
  - `APITraceNoop` <-> `api-trace-noop`
- Prefer additive public API changes. Do not rename public symbols or JSON keys casually.
- If you intentionally introduce a platform-specific difference, document it in the relevant platform README and mention it in the final summary.
- When public behavior or integration changes, update `README.md` and the platform README files that are affected.
- This repo ships SDKs, not sample apps. Avoid app-specific assumptions in code or docs.

## Submodule Workflow

- Each submodule is a standalone repo. Make changes, commit, and push inside the submodule first.
- Then return to the container root and commit the updated submodule pointer.
- Do not make source code changes at the container level — all code lives in the submodules.

## Validation

- Preferred iOS check:
  - `cd ios && swift test`
- Preferred Android check when Gradle is available:
  - `cd android && gradle :api-trace-core:assemble :api-trace-debug:assemble :api-trace-noop:assemble`
- Current repo state:
  - Swift tests run successfully on this machine.
  - No Gradle wrapper is committed in the Android submodule.
  - If Android validation is blocked, report that explicitly instead of pretending the check passed.

## Testing Expectations

- Keep or expand Swift tests when changing core redaction or record modeling behavior.
- Android currently has no committed tests. If you add non-trivial Kotlin logic, prefer adding tests instead of relying only on manual review.

## Skills

- Use the repo-local skill at `.codex/skills/api-trace-sdk-maintainer/SKILL.md` for cross-platform SDK work in this repository.
- Use the repo-local skill at `.codex/skills/apitrace-integration/SKILL.md` when the task is to add this SDK into another app repository.
- Each submodule also carries its own `apitrace-integration` skill for platform-specific integration tasks.
