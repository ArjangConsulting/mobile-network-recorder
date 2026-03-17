# GEMINI.md

Use `AGENTS.md` as the source of truth for this repository.

Key repo constraints:

- This is a container repo with two Git submodules: `ios/` and `android/`.
- Each submodule is a standalone SDK repo with its own agent docs and skills.
- Shared behavior changes should be reviewed on both platforms.
- Keep public docs in sync with code changes.
- Make changes inside submodules first, then update the pointer in this container.
- The reliable local validation path is `cd ios && swift test`; Android verification requires a working local Gradle installation.

Repo-local skill: `.codex/skills/api-trace-sdk-maintainer/SKILL.md`.
