# Swift and iOS Workflows

## Use This Reference For

- iOS-native feature delivery in Swift.
- React Native/Expo projects that require custom iOS modules or SDK integrations.
- App Store release hardening and runtime security checks.

## Core Workflow

1. Define iOS minimum deployment target and required Apple frameworks first.
2. Implement feature vertically (UI -> domain -> network/storage -> telemetry).
3. Add unit tests for domain logic and one UI/integration smoke path.
4. Validate on at least one real device before release candidate.

## Integration Patterns

- Keep networking in one client layer with strict request/response modeling.
- Prefer Swift Package Manager for internal and external dependencies when available.
- For hybrid stacks (RN/Expo + native), keep bridge APIs stable and versioned.
- Separate crash-critical startup code from optional SDK initialization.

## iOS Security Guardrails

- Store secrets/tokens in Keychain, not `UserDefaults`.
- Require HTTPS endpoints and maintain App Transport Security exceptions only when strictly required.
- Use App Attest or DeviceCheck where abuse resistance matters.
- Minimize entitlement and permission scope; request only what feature paths need.
- Validate universal links and URL scheme handling against spoofing and open redirect paths.

## Release and Reliability Checklist

1. Verify code signing and provisioning profile ownership.
2. Check background modes and push notification behavior under low-power and low-connectivity states.
3. Confirm privacy manifest and permission rationale strings are current.
4. Review crash analytics and startup performance before App Store submission.

## Primary Sources

- Apple Developer documentation root: <https://developer.apple.com/documentation/>
- Xcode guide: <https://developer.apple.com/xcode/>
- Swift.org docs: <https://www.swift.org/documentation/>
- Keychain Services: <https://developer.apple.com/documentation/security/keychain_services>
- App Transport Security overview: <https://developer.apple.com/documentation/bundleresources/information_property_list/nsapptransportsecurity>
- App Attest: <https://developer.apple.com/documentation/devicecheck/validating_apps_that_connect_to_your_server>
- DeviceCheck: <https://developer.apple.com/documentation/devicecheck>
