# Copilot Instructions

Use `AGENTS.md` as the full repository guide. The essentials are:

- This is a container repo with two Git submodules: `ios/` and `android/`.
- Each submodule is a standalone SDK repo ([ios-network-recorder](https://github.com/ArjangConsulting/ios-network-recorder), [android-network-recorder](https://github.com/ArjangConsulting/android-network-recorder)).
- If a change affects capture semantics, redaction, exported data, or install/bootstrap behavior, inspect both platforms.
- Keep semantic parity while preserving current intentional differences, including iOS `startedAt` versus Android `startedAtEpochMs`.
- Make changes inside submodules first, commit and push there, then update the submodule pointer in this container.
- Run `cd ios && swift test` after Swift changes.
- Android has no checked-in Gradle wrapper; use installed Gradle or Android Studio, and report environment blockers explicitly.
