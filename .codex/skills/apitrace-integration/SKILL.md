---
name: apitrace-integration
description: Integrate the APITrace mobile network recorder into iOS and Android apps using this repository's SDK. Use when asked to add sanitized request/response capture, debug-only tracing, or trace export/share flows in a host project.
---

# APITrace Integration Skill

Use this skill when an app team wants to add this repository's network recording feature into their own project.

This skill is for host app integration. It is not the SDK maintenance guide.

## Use when

- adding API trace capture to an iOS app
- adding API trace capture to an Android app
- wiring a debug-only export/share flow for captured traffic
- integrating with moqserver ingestion or any other tool that consumes exported traces

## Resolve Up Front

- target platform: iOS, Android, or both
- dependency strategy: local path, vendored source, or published package/artifact
- real network stack in the app: `URLSession`, OkHttp, Retrofit, or wrappers around them
- developer surface for export: debug screen, share sheet, hidden action, file export, or upload flow

## Workflow

1. Inspect where the host app creates its main network clients or sessions.
2. Choose how the SDK will be added. Read `references/dependency-strategies.md` if needed.
3. Add `core` plus `debug`/`noop` modules so release behavior stays safe.
4. Install the bootstrap before the app's main network clients are created.
5. Start capture during app startup.
6. Configure an explicit redaction allowlist. Request capture is opt-in by design.
7. Add a developer-only export surface using the platform export API.
8. Run one real request and inspect the exported payload for redaction correctness.
9. Update the host project's docs or debug menu labeling if the feature is discoverable by developers.

## Platform References

- iOS integration: `references/ios.md`
- Android integration: `references/android.md`
- Rollout checklist: `references/host-checklist.md`
- Dependency choices: `references/dependency-strategies.md`

## Guardrails

- Keep release builds on the no-op path unless the user explicitly wants production capture.
- Do not capture all request headers or query items by default.
- Instrument the app's real network path, not a new unused client.
- Preserve existing auth, retries, caching, logging, and certificate pinning behavior.
- If the app already has a debug menu or diagnostics screen, extend it instead of adding a second developer surface.
- Do not invent a backend upload protocol. Export JSON and connect it to the app's existing share or upload flow.

## Completion Output

When finishing the task in a host repo, report:

- where bootstrap/install happens
- which client/session path is actually instrumented
- which headers and query items are allowlisted
- how a developer exports traces
- what was validated and what is still manual
