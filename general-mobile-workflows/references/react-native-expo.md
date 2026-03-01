# React Native and Expo Workflows

## Use This Reference For

- New feature delivery in React Native or Expo.
- Expo managed vs prebuild vs bare decisions.
- Native module integration and OTA safety checks.

## Core Workflow

1. Start with the latest supported Expo SDK and React Native version.
2. Keep app config deterministic (`app.json` or `app.config.*` with environment controls).
3. Add dependencies in small batches and verify both iOS and Android each step.
4. Introduce native code only when Expo modules/config plugins cannot cover the need.
5. Lock CI toolchain versions and run release builds early, not only at the end.

## Architecture and Integration Guidance

- Put domain logic in shared TypeScript modules.
- Keep native bridges minimal; expose narrow interfaces and validate input/output types.
- Isolate third-party SDK code behind adapters to reduce vendor lock-in and simplify upgrades.
- For auth and payments, keep sensitive operations server-side; mobile client should hold scoped tokens only.

## Expo-Specific Guardrails

- Use EAS Build profiles per environment (`development`, `preview`, `production`).
- Use EAS Update channels/branches with explicit rollout strategy.
- Bump `runtimeVersion` when any native dependency, plugin behavior, or native interface changes.
- Regenerate native projects when plugin/native config drift appears:
  - `npx expo prebuild --clean`
- Use `references/expo-production-deploy.md` for production release flow.
- Use `references/gradle-build-pass-notes.md` when Android/EAS jobs fail in Gradle phases.
- Use `references/feed-ui-and-pagination.md` and `references/feed-video-playback-and-caching.md` for short-video feed feature delivery.

## Common Workarounds

1. Fix Metro and native cache corruption by cleaning derived/build caches and reinstalling dependencies.
2. Resolve Android Gradle mismatch by aligning Gradle, AGP, Kotlin, and JDK versions from official compatibility notes.
3. Resolve iOS native build failures by re-running CocoaPods install after dependency and config changes.
4. Avoid environment leakage by mapping each build profile to separate credentials, API base URLs, and update channels.

## Security Notes

- Prefer `expo-secure-store` or native secure storage for secrets; avoid AsyncStorage for secrets.
- Enable TLS-only transport and certificate pinning only when you own rotation processes.
- Avoid embedding long-lived API keys in client bundles.

## Primary Sources

- Expo docs root: <https://docs.expo.dev/>
- Expo EAS Build introduction: <https://docs.expo.dev/build/introduction/>
- Expo EAS Update introduction: <https://docs.expo.dev/eas-update/introduction/>
- Expo SecureStore SDK: <https://docs.expo.dev/versions/latest/sdk/securestore/>
- React Native docs root: <https://reactnative.dev/docs/getting-started>
- React Native architecture intro: <https://reactnative.dev/docs/the-new-architecture/landing-page>
- React Native upgrading: <https://reactnative.dev/docs/upgrading>
