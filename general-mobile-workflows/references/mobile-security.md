# Mobile Security Guardrails

## Use This Reference For

- Threat modeling and release security sign-off.
- React Native/Expo/Swift/Kotlin mobile app hardening.
- Defining "do not cross" lines for client-side code.

## Baseline Security Workflow

1. Classify data handled by the app (public, internal, sensitive, regulated).
2. Map attack surfaces (network, local storage, deep links, auth/session, third-party SDKs, supply chain).
3. Apply platform controls before feature complete.
4. Run static/dependency checks and at least one dynamic test pass before release.
5. Track remediation deadlines by severity.

## Do-Not-Cross Lines

1. Do not store secrets, long-lived tokens, or private keys in plain-text files or standard preferences.
2. Do not hardcode backend credentials in mobile bundles.
3. Do not ship debug logging that leaks tokens, PII, or auth headers.
4. Do not grant broad permissions "just in case."
5. Do not bypass TLS validation in production builds.
6. Do not roll out OTA updates that change native contracts without runtime gating.

## Required Controls (Map to MASVS)

- Use secure local storage and key management.
- Enforce transport protection and certificate validation.
- Harden authentication/session handling and token lifecycle.
- Minimize attack surface (permissions, exported components, intent/deep-link validation).
- Protect build/release pipeline and dependency chain.
- Instrument security telemetry for abuse detection and incident response.

## Platform-Specific Checks

### React Native and Expo

- Keep JavaScript dependencies pinned and reviewed for known vulnerabilities.
- Store secrets in secure storage modules only.
- Separate dev/prod update channels and signing credentials.

### iOS

- Store sensitive values in Keychain.
- Use ATS-compliant networking and narrowly-scoped exceptions.
- Use App Attest/DeviceCheck when server-side trust needs stronger proof.

### Android

- Use Keystore-backed key material.
- Keep network security config strict for production.
- Use Play Integrity for high-risk flows.

## Verification Checklist Before Release

1. Complete dependency scan and remediate critical CVEs.
2. Confirm no secrets in source, logs, or bundled config.
3. Verify all auth/session edge cases (revocation, refresh, logout, device loss).
4. Validate deep-link handling and intent filters against malicious inputs.
5. Confirm observability hooks for security events and abuse anomalies.

## Primary Sources

- OWASP MASVS: <https://mas.owasp.org/MASVS/>
- OWASP MSTG: <https://mas.owasp.org/MSTG/>
- Android security best practices: <https://developer.android.com/privacy-and-security/security-best-practices>
- Android Keystore system: <https://developer.android.com/privacy-and-security/keystore>
- Play Integrity API overview: <https://developer.android.com/google/play/integrity/overview>
- Apple Security framework docs: <https://developer.apple.com/documentation/security>
- Apple Keychain Services: <https://developer.apple.com/documentation/security/keychain_services>
- Apple ATS configuration docs: <https://developer.apple.com/documentation/bundleresources/information_property_list/nsapptransportsecurity>
