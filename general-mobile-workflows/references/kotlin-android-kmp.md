# Kotlin, Android, and Kotlin Multiplatform Workflows

## Use This Reference For

- Android-native Kotlin delivery.
- Kotlin Multiplatform (KMP) shared business logic decisions.
- Android build, release, and performance stabilization.

## Core Android Workflow

1. Confirm `minSdk`, `targetSdk`, ABI support, and performance budgets.
2. Build feature slice with clear module boundaries.
3. Add instrumentation coverage for critical user paths.
4. Run release-mode testing on representative low/mid-tier hardware.

## Android Architecture Guidance

- Keep UI, domain, and data layers separate.
- Keep networking and persistence in tested modules.
- Use feature flags for staged rollouts and risky dependency migrations.
- Treat startup as a budget: defer optional SDK initialization.

## Kotlin Multiplatform Guidance

- Share business rules, API clients, and validation logic.
- Keep UI native (SwiftUI/UIKit on iOS, Compose/View on Android) unless explicit cross-platform UI framework choice is made.
- Define platform adapters for storage, logging, and secure secrets.
- Guard shared modules with strict semantic versioning to avoid multi-app breakage.

## Android Security Guardrails

- Use Android Keystore-backed storage for credentials and cryptographic keys.
- Enforce network security configuration and TLS-only endpoints.
- Verify app/device integrity for abuse-sensitive features with Play Integrity API.
- Keep exported activities/services/providers minimal and explicit.
- Validate deep links and intent handling to prevent hijacking.

## Release and Reliability Checklist

1. Align AGP, Gradle, Kotlin, and JDK versions with compatibility matrix.
2. Enable R8/proguard with tested keep rules.
3. Validate background behavior (push, workers, sync) with battery optimization constraints.
4. Verify Play Console requirements (target API level, data safety, privacy policy, signing).

## Primary Sources

- Android developer docs root: <https://developer.android.com/docs>
- Android app architecture: <https://developer.android.com/topic/architecture>
- Android app signing: <https://developer.android.com/studio/publish/app-signing>
- Android Keystore system: <https://developer.android.com/privacy-and-security/keystore>
- Play Integrity API: <https://developer.android.com/google/play/integrity/overview>
- JetBrains Kotlin docs: <https://kotlinlang.org/docs/home.html>
- Kotlin Multiplatform overview: <https://www.jetbrains.com/help/kotlin-multiplatform-dev/get-started.html>
