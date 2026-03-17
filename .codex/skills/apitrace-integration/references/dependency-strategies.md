# Dependency Strategies

Use the smallest viable dependency strategy for the host project.

## iOS

Preferred order:

1. Git Swift package dependency from `git@github.com:ArjangConsulting/ios-network-recorder.git`
2. Local Swift package path when developing alongside the container repo (`ios/` submodule)
3. Vendored source only if the project cannot consume Swift packages cleanly

The products are:

- `APITraceCore`
- `APITraceDebug`
- `APITraceNoop`

## Android

Preferred order:

1. Published Maven artifact if available
2. Git submodule from `git@github.com:ArjangConsulting/android-network-recorder.git`
3. Vendored source as included Gradle modules
4. Direct file copy only if the host repo cannot use submodules or another shared-source approach

When integrating source directly, bring in these modules:

- `api-trace-core`
- `api-trace-debug`
- `api-trace-noop`

The host app's Gradle setup must already provide Android and Kotlin plugin management. This SDK repo does not include a reusable published plugin.

## Choose Based On Context

- If the host repo is a monorepo or adjacent local repo setup, prefer local path or submodule wiring.
- If multiple apps need the feature, prefer a published package/artifact instead of repeated source copies.
- If the user has not published this SDK yet, do not fabricate package coordinates. Use local or vendored integration.
