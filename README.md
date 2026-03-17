# mobile-network-recorder

Container repository for cross-platform mobile network recording SDKs, extracted from `moqserver`.

## Layout

| Platform | Submodule | GitHub |
|----------|-----------|--------|
| iOS | `ios/` | [ios-network-recorder](https://github.com/ArjangConsulting/ios-network-recorder) |
| Android | `android/` | [android-network-recorder](https://github.com/ArjangConsulting/android-network-recorder) |

Each SDK lives in its own standalone repository and is included here as a Git submodule for cross-platform development.

## Purpose

These SDKs capture sanitized request/response traffic from mobile apps so the exported payload can later be ingested by `moqserver` or other tooling.

## Clone

```bash
git clone --recurse-submodules git@github.com:ArjangConsulting/mobile-network-recorder.git
```

If you already cloned without `--recurse-submodules`:

```bash
git submodule update --init --recursive
```

## Quick Start

### iOS

The Swift package is at `ios/`:

```bash
cd ios && swift test
```

See [ios/README.md](ios/README.md) for integration details.

### Android

The Gradle project is at `android/`:

```bash
cd android && gradle :api-trace-core:assemble :api-trace-debug:assemble :api-trace-noop:assemble
```

See [android/README.md](android/README.md) for integration details.

## Submodule Workflow

When making changes:

1. Work inside the submodule directory (`ios/` or `android/`).
2. Commit and push changes in the submodule first.
3. Return to the container repo root and commit the updated submodule pointer.

## Relationship To moqserver

`moqserver` remains the mock server and ingestion side of the workflow. This repository contains only the mobile capture SDKs.
