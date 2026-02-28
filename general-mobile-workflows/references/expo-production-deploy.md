# Expo Production Build and Deploy Runbook

## Use This Reference For

- Shipping Expo projects to production (Android and iOS).
- Passing EAS build jobs reliably and submitting binaries to stores.
- Running OTA updates safely after store release.

## Production Preflight

1. Verify SDK and dependency health:
   - `npx expo doctor`
2. Install dependency versions compatible with current Expo SDK:
   - `npx expo install --check`
3. Confirm app identifiers and versioning are correct:
   - iOS `bundleIdentifier`
   - Android `package`
4. Confirm `runtimeVersion` and update channel strategy before release.

## Minimum EAS Configuration

1. Initialize EAS in project:
   - `eas build:configure`
2. Keep an explicit production profile in `eas.json`:
   - Set `distribution: "store"`
   - Keep environment values explicit and deterministic.
3. Ensure credentials are valid and owned by your team:
   - `eas credentials`

## Build Commands (Production)

1. Android build:
   - `eas build --platform android --profile production`
2. iOS build:
   - `eas build --platform ios --profile production`
3. If CI-only failure appears, reproduce locally:
   - `eas build --platform android --profile production --local`

## Submit to Stores

1. Android submission:
   - `eas submit --platform android --latest`
2. iOS submission:
   - `eas submit --platform ios --latest`
3. If submission is split from build in CI, pass artifact path explicitly with `--path`.

## OTA Updates After Release

1. Publish production update:
   - `eas update --branch production --message "release note"`
2. Update only JS/assets unless native contracts are unchanged.
3. Bump `runtimeVersion` whenever native layer, native module, or config-plugin contract changes.

## Build-Pass Checklist for Expo Android Jobs

1. Confirm Expo SDK, React Native, and native packages are mutually compatible.
2. Resolve Gradle/AGP/JDK mismatches using official compatibility tables.
3. Regenerate native projects if prebuild drift exists:
   - `npx expo prebuild --clean`
4. Re-run with clear logs and identify first root-cause error.
5. Keep toolchain versions pinned in CI to avoid sudden breakage.

## Deployment Guardrails

1. Keep separate EAS channels/branches for preview and production.
2. Enforce approvals before production `eas update` commands.
3. Keep rollback plan ready:
   - Previous stable store binary
   - Previous stable OTA branch head
4. Never ship secrets in app config; use environment + server-side secret controls.

## Primary Sources

- EAS Build introduction: <https://docs.expo.dev/build/introduction/>
- EAS Build setup: <https://docs.expo.dev/build/setup/>
- EAS local builds: <https://docs.expo.dev/build-reference/local-builds/>
- EAS troubleshooting: <https://docs.expo.dev/build-reference/troubleshooting/>
- EAS Submit intro: <https://docs.expo.dev/submit/introduction/>
- EAS Submit to stores: <https://docs.expo.dev/submit/android/>
- EAS Update intro: <https://docs.expo.dev/eas-update/introduction/>
- Runtime versions: <https://docs.expo.dev/eas-update/runtime-versions/>
