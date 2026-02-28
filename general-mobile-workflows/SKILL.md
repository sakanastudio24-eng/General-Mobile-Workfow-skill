---
name: general-mobile-workflows
description: End-to-end mobile engineering workflow for React Native, Expo, Swift, Kotlin, and Kotlin Multiplatform projects. Use when planning or building mobile features, choosing stack boundaries, integrating native modules/services, handling CI/CD and app signing, troubleshooting build/runtime issues, upgrading SDK or framework versions, passing Android Gradle builds, shipping Expo production builds/deploys, or enforcing mobile security and release guardrails.
---

# General Mobile Workflows

Use this skill to deliver mobile work quickly with clear tradeoffs, safe defaults, and platform-correct execution.

## Workflow Decision Tree

1. Start in `references/examples-and-resources.md` to pick a known-good pattern and sample.
2. Use `references/react-native-expo.md` for React Native and Expo work, including EAS build/update and native module boundaries.
3. Use `references/expo-production-deploy.md` for production-grade Expo build and store delivery.
4. Use `references/gradle-build-pass-notes.md` when Android build or EAS Android job is failing.
5. Use `references/swift-ios.md` for Swift and iOS-native implementation details.
6. Use `references/kotlin-android-kmp.md` for Android-native Kotlin and Kotlin Multiplatform.
7. Apply `references/mobile-security.md` before merge and release.

## Execution Workflow

1. Define scope and platform split.
2. Choose architecture path.
3. Build the smallest vertical slice.
4. Integrate platform services.
5. Validate performance and reliability.
6. Run security and release gates.

### 1) Define Scope and Platform Split

- Capture platforms (`ios`, `android`) and release target (`prototype`, `beta`, `production`).
- Classify feature as `shared`, `platform-specific`, or `native-critical`.
- Decide whether you need native APIs immediately (camera, BLE, custom crypto, payment SDKs, attestation).

### 2) Choose Architecture Path

- Prefer Expo managed workflow for fastest shipping when required native integrations are supported by Expo modules/config plugins.
- Prefer Expo prebuild or bare React Native when you need custom native SDKs or deep native changes.
- Prefer fully native Swift/Kotlin when shared JS adds more complexity than value.
- Prefer Kotlin Multiplatform when business logic sharing is high and UI remains platform-native.

### 3) Build the Smallest Vertical Slice

- Implement one end-to-end flow: UI -> state -> network -> persistence -> error handling.
- Prove local run on both platforms before broad feature expansion.
- Keep integration seams explicit (interfaces/adapters) to reduce rewrite risk.

### 4) Integrate Platform Services

- Add push, auth, deep links, analytics, and secure storage incrementally.
- Keep secrets out of the client; store only scoped tokens and non-sensitive config.
- For Expo updates, isolate channels and runtime versions per environment.

### 5) Validate Performance and Reliability

- Measure startup time, memory, dropped frames, and crash-free sessions.
- Run on low-end Android and at least one older iOS device target if possible.
- Verify offline behavior, retry logic, and degraded network handling.

### 6) Run Security and Release Gates

- Enforce transport security, secure local storage, and least-privilege permissions.
- Verify integrity signals (Play Integrity, App Attest/DeviceCheck) for abuse-sensitive flows.
- Block release on critical findings from dependency and static checks.

## Common Workarounds and Integrations

1. Resolve Expo/RN native drift by regenerating native projects (`npx expo prebuild --clean`) and reapplying config plugin changes.
2. Avoid OTA breakage by bumping `runtimeVersion` whenever native contracts change.
3. Prevent credential lockouts by documenting ownership and rotation for keystores, certs, provisioning profiles, and API keys.
4. Reduce flaky mobile CI by pinning toolchain versions (Node, Java, Xcode, Android SDK/NDK, Gradle).
5. Avoid brittle deep-link handling by testing cold-start, warm-start, logged-in, and logged-out paths for every route.

## Codex-Specific Uses

Use this skill to make Codex outputs mobile-specific and production-oriented instead of generic:

1. Turn a product ask into platform-aware architecture choices with clear constraints.
2. Generate implementation plans that separate shared logic from native-critical work.
3. Build migration plans for web teams moving to Expo, React Native, Swift, Kotlin, or KMP.
4. Produce integration checklists for auth, push, deep links, analytics, secure storage, and CI/CD.
5. Diagnose build and release failures with likely root causes by platform and toolchain.
6. Run Gradle/Android build-fix playbooks with compatibility-aware checks.
7. Produce Expo production deployment runbooks (build, submit, OTA strategy, rollback guardrails).
8. Add release/security gates before merge and app store submission.

## Delivery Format

When using this skill in a task, return:

1. Recommended stack path with a 2-3 sentence tradeoff summary.
2. Ordered implementation plan with platform-specific checkpoints.
3. Integration checklist (auth, storage, push, deep links, analytics, CI/CD).
4. Build-pass checklist (especially Gradle/Android for Expo and RN projects).
5. Security checklist mapped to mobile controls.
6. Release checklist for App Store and Play Store.

## References

- React Native + Expo: [references/react-native-expo.md](references/react-native-expo.md)
- Expo production deploy: [references/expo-production-deploy.md](references/expo-production-deploy.md)
- Gradle build pass notes: [references/gradle-build-pass-notes.md](references/gradle-build-pass-notes.md)
- Swift + iOS: [references/swift-ios.md](references/swift-ios.md)
- Kotlin + Android + KMP: [references/kotlin-android-kmp.md](references/kotlin-android-kmp.md)
- Security guardrails: [references/mobile-security.md](references/mobile-security.md)
- Example projects and source links: [references/examples-and-resources.md](references/examples-and-resources.md)
