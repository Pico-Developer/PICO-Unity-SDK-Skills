# Build, Release, and Troubleshooting Guide

This guide is self-contained. Use it for Android build setup, manifest issues, Project Validation, logs, release-mode failures, signing/copyright verification, entitlement-related release failures, and store-readiness checks.

## Android build baseline

- Build platform: Android.
- Scripting Backend: IL2CPP.
- Target Architecture: ARM64; avoid ARMv7-only builds.
- Minimum API Level: Android 10 / API Level 29 is a common current baseline in inspected setup docs.
- Target API Level: Automatic / highest installed is commonly recommended.
- Package name must be unique and should not remain the Unity default.
- Signing certificate/package name must remain consistent across app updates.
- Version code/version number should increase for release updates.

## XR / OpenXR baseline

- Enable the correct XR provider for the selected mode.
- For Unity OpenXR, enable OpenXR under Android settings and enable the relevant PICO feature groups.
- Add the appropriate controller interaction profile for target devices.
- Verify XR Origin and Main Camera setup.
- Ensure only one XR Origin and one MainCamera tag unless the app intentionally uses a more advanced camera stack.

## Project Validation workflow

Use Project Validation before every device build and release candidate:

1. Open `Edit > Project Settings > XR Plug-in Management > Project Validation`.
2. Show all items.
3. Fix Required issues first.
4. Fix Recommended issues when relevant to performance or stability.
5. Re-run after changing Unity version, SDK version, render pipeline, graphics API, or Android build settings.

Common validation categories:

- Android build target and architecture.
- IL2CPP / ARM64.
- Graphics API such as Vulkan/OpenGLES3.
- Multithreaded rendering.
- Stereo rendering mode / Multiview.
- MSAA recommendations.
- PICO/PXR manager existence.
- XR Origin and MainCamera uniqueness.
- URP HDR/Post Processing conflicts with Passthrough/VST.
- Missing composition layer package or OpenXR plugin compatibility requirements.

## Manifest and permissions

Common manifest needs vary by feature:

- Platform services: app ID / SDK metadata as required by SDK path.
- RTC: internet, microphone/audio, network state, and related Android permissions.
- External file access: app-specific storage or explicit permissions depending on Android version and use case.
- MR Safeguard: SDK may add metadata such as `enable_mr_safeguard` when the feature is enabled.
- SecureMR / camera / enterprise features: follow feature-specific privacy and permission requirements.

Use custom main manifest and Gradle templates only when necessary, then keep them synchronized with SDK upgrades.

## Logs and diagnostics

### adb logcat

Useful filters:

```bash
adb logcat | findstr /i "Unity PXR OpenXR PICO XR passthrough seethrough VST spatial anchor scene mesh plane SecureMR PlatformService entitlement"
```

For macOS/Linux:

```bash
adb logcat | grep -iE "Unity|PXR|OpenXR|PICO|passthrough|seethrough|VST|spatial|SecureMR|PlatformService|entitlement"
```

### Device log capture

- Enable device log recording where available.
- Reboot or restart app if required by the logging flow.
- Reproduce the issue.
- Pull device logs from the documented log folder or use adb.

### Performance logs

- Metrics HUD is fast for on-device live checks.
- PICO Developer Center can capture device performance logs.
- XR Profiling Toolkit is better for repeatable comparisons.

## Release-mode stuck on loading screen

Check:

- Missing PXR/PICO manager in loading scene or target scene.
- Platform Services initialization waiting forever without timeout/error UI.
- Entitlement Check blocking startup.
- Network unavailable but code assumes success.
- Release minification/ProGuard stripping required classes.
- Scene transition depends on debug-only code or editor-only assets.

Mitigations:

- Add explicit timeout and error UI for platform initialization.
- Log each startup step.
- Test Release build on device, not only Development Build.
- If using code shrinking/minification, add required keep rules or disable temporarily to isolate.

## Copyright Verification Failed / Illegal Signature

Common causes:

- Package name mismatch.
- Signing certificate mismatch compared with uploaded app.
- App ID mismatch.
- Default Unity package name.
- Wrong organization/app on Developer Platform.
- Entitlement/app ownership state differs from expectation.

Fix flow:

1. Confirm package name matches Developer Platform app.
2. Confirm signing certificate matches the uploaded/expected signing path.
3. Confirm App ID in Unity matches Developer Platform.
4. Confirm build uses IL2CPP + ARM64.
5. Confirm app is installed from the correct source for the test scenario.
6. Re-test entitlement and login state with a proper PICO account.

## Store/release readiness checklist

- Correct development mode selected.
- Project Validation Required items fixed.
- Android build settings correct: IL2CPP, ARM64, API levels, package name, signing.
- All required permissions declared.
- App ID and platform services configured.
- Entitlement Check integrated for paid apps and considered for free apps.
- Platform Services errors handled gracefully.
- Performance target met on each supported device.
- Long-duration thermal/power test completed.
- No editor-only paths or debug-only assumptions.
- Privacy-sensitive features clearly explained to users.
- Passthrough/camera/enterprise features follow platform privacy requirements.

## Common troubleshooting pattern

When diagnosing PICO issues, ask for:

- Device model and OS version.
- Unity version.
- SDK name and version.
- Development mode: PICO XR / Unity OpenXR / PICO Spatial.
- Render pipeline: Built-in / URP.
- Graphics API: Vulkan / OpenGLES3.
- Physical-device logs.
- Whether it fails in Development Build, Release Build, or both.
- Whether Project Validation has unresolved Required items.
