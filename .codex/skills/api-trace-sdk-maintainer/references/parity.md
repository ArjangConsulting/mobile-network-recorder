# APITrace Parity Notes

## Module Map

| Concern | iOS | Android |
| --- | --- | --- |
| Public facade | `Sources/APITraceCore/APITrace.swift` | `api-trace-core/APITrace.kt` |
| Record model | `Sources/APITraceCore/APITraceRecord.swift` | `api-trace-core/APITraceRecord.kt` |
| Redaction | `Sources/APITraceCore/APITraceRedactor.swift` | `api-trace-core/APITraceRedactor.kt` |
| Debug bootstrap | `Sources/APITraceDebug/APITraceDebugBootstrap.swift` | `api-trace-debug/APITraceBootstrap.kt` |
| No-op bootstrap | `Sources/APITraceNoop/APITraceNoopBootstrap.swift` | `api-trace-noop/APITraceBootstrap.kt` |

Paths are relative to each submodule root (`ios/` for Swift, `android/` for Kotlin).

## Shared Expectations

- Both platforms expose three modules: core, debug, and noop.
- Request header and query capture is opt-in.
- `exact`/`EXACT` preserves configured values.
- `includes`/`INCLUDES` preserves presence semantics and stores the configured replacement value.
- Exported records should keep the same meaning for request payload, response payload, and failure state.

## Known Intentional Differences

- The behavioral differences (`startedAt` storage, redirect recording, non-debuggable builds, custom session configurations) are listed once, under Working Rules in the container `AGENTS.md`. Check that list before treating a platform difference as a parity bug.
- iOS export API is `exportJSON(prettyPrinted:)`.
- Android export API is `exportJson(pretty)`.

## Doc Update Checklist

- Root `README.md` for repo structure or positioning changes
- `ios/README.md` for Swift integration or API examples
- `android/README.md` for Kotlin integration or API examples
