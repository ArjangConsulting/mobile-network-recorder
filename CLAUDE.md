# CLAUDE.md

Start with `AGENTS.md`. It is the canonical repo guide.

The short version:

- This is a container repo with two Git submodules: `ios/` (SwiftPM) and `android/` (Kotlin/Gradle).
- Each submodule is a standalone SDK repo with its own agent docs.
- Keep public capture behavior semantically aligned across platforms.
- Preserve known intentional differences such as iOS `startedAt` versus Android `startedAtEpochMs`.
- Make changes inside submodules first, then update the pointer in this container.
- Validate with `cd ios && swift test`. Android validation depends on installed Gradle because no wrapper is committed.

For repo-specific workflow details, use `.codex/skills/api-trace-sdk-maintainer/SKILL.md`.
