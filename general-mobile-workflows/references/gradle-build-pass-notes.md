# Gradle Build-Pass Notes (Android and Expo/RN)

## Use This Reference For

- Any Android Gradle build failure in native Android, React Native, or Expo prebuild/bare projects.
- EAS Android builds that fail in Gradle phases.
- Compatibility alignment (Gradle, AGP, Java, Kotlin) and reproducible build setup.

## Fast Failure Triage

1. Re-run with diagnostics:
   - `./gradlew assembleRelease --stacktrace --info`
   - Add `--scan` when sharing failures with teammates.
2. Confirm the first real failure in logs, not the last cascade error.
3. Check compatibility in this order:
   - Android Studio <-> AGP compatibility table.
   - Gradle <-> Java runtime compatibility matrix.
   - Kotlin plugin compatibility with AGP.
4. Build with Wrapper only (`./gradlew`), never system `gradle`.
5. Re-run after clean sync:
   - `./gradlew --stop`
   - `./gradlew clean`
   - `./gradlew assembleRelease`

## High-Probability Root Causes and Fix Paths

### 1) Version mismatch (most common)

- Symptoms:
  - "Minimum supported Gradle version is ..."
  - "This version of AGP requires Java ..."
- Fix:
  - Align `gradle-wrapper.properties`, AGP version, and JDK to official matrices.
  - Avoid dynamic plugin versions (`8.13.+` style).

### 2) Dependency conflict or duplicate classes

- Symptoms:
  - `Duplicate class` errors.
  - Resolution conflicts after adding new libraries.
- Fix:
  - Inspect dependency graph:
    - `./gradlew :app:dependencies`
    - `./gradlew :app:dependencyInsight --dependency <name>`
  - Constrain or exclude conflicting transitive dependencies.

### 3) Cache/corruption drift

- Symptoms:
  - Failure appears after partial upgrade or interrupted build.
- Fix:
  - Stop daemons, clean project, and rebuild.
  - If still failing, clear only relevant project caches before retry.

### 4) Out-of-memory or daemon crash

- Symptoms:
  - Daemon disappeared, OOM traces, abrupt process kill in CI.
- Fix:
  - Lower concurrency and tune memory for CI constraints.
  - Separate JS bundling diagnostics from native compile failures in Expo/RN pipelines.

## Performance Settings That Still Preserve Correctness

- Enable build cache when safe:
  - CLI: `--build-cache`
  - Persistent: `org.gradle.caching=true` in `gradle.properties`
- Use configuration cache only after plugin compatibility checks:
  - `--configuration-cache`
- Use `--parallel` only if modules/tasks are ready for parallel execution.

## Security and Supply-Chain Hardening

1. Commit Gradle Wrapper files to source control.
2. Verify wrapper distribution integrity with SHA-256 in `gradle-wrapper.properties`.
3. Treat wrapper updates as reviewed changes (same as dependency lock updates).

## Expo and React Native Specific Notes

1. If an EAS Android build fails, reproduce locally first:
   - `eas build --platform android --local`
2. If failure includes JS bundle phases (`bundleReleaseJsAndAssets`), verify JS bundle independently:
   - `npx expo export`
3. If native config drift is suspected in Expo prebuild projects:
   - `npx expo prebuild --clean`

## Primary Sources

- Gradle compatibility matrix: <https://docs.gradle.org/current/userguide/compatibility.html>
- Gradle wrapper guide: <https://docs.gradle.org/current/userguide/gradle_wrapper.html>
- Gradle CLI reference: <https://docs.gradle.org/current/userguide/command_line_interface.html>
- Gradle Build Scan basics: <https://docs.gradle.org/current/userguide/build_scans.html>
- Android Studio/AGP compatibility: <https://developer.android.com/build/releases/about-agp>
- Expo troubleshooting builds: <https://docs.expo.dev/build-reference/troubleshooting/>
- Expo local builds: <https://docs.expo.dev/build-reference/local-builds/>
