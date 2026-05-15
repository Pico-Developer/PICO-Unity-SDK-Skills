# Spatial Audio, Developer Tools, and Review Readiness Guide

This guide is self-contained. Use it when the user asks about PICO Spatial Audio, microphone/audio design, PICO Developer Center, PICO XR Portal, PICO Debugger, PICO Emulator, Live Preview, Play-to-PICO, PICO Haptic Editor, PICO Graphics Probe Tool, or app review readiness.

## Spatial Audio

PICO Spatial Audio Renderer spatializes sound from all directions and can simulate realistic changes such as distance attenuation, reflection, occlusion, absorption, scattering, and transmission.

Typical requirements:

- PICO Neo3, PICO 4, or PICO 4 Ultra series.
- PICO OS 5.11.0 or later.
- PICO Unity Integration SDK SpatialAudio package.

### Key components

| Component | Purpose |
| --- | --- |
| `PXR_Audio_Spatializer_Context` | Sets rendering backend and quality. Backend can be Unity or Wwise where supported. |
| `PXR_Audio_Spatializer_Audio Source` | Adds spatial source behavior: gain, reflection gain, source size, Doppler, attenuation, directivity. |
| `PXR_Audio_Spatializer_Audio Listener` | Outputs spatialized binaural audio, commonly through `OnAudioFilterRead` or Pico Audio Router. |
| `PXR_Audio_Spatializer_Scene Geometry` | Marks scene geometry for environmental acoustic simulation. |
| `PXR_Audio_Spatializer_Scene Material` | Configures absorption, scattering, and transmission. |
| `PXR_Audio_Spatializer_Ambisonic Source` | Handles Ambisonic content where appropriate. |

### Free-field setup

Use free field when the app only needs source direction and distance, not room acoustics.

1. Create a GameObject for audio context.
2. Add `PXR_Audio_Spatializer_Context`.
3. Create an audio source object.
4. Add `PXR_Audio_Spatializer_Audio Source`; keep Unity `Audio Source > Spatial Blend` at the recommended value for the plugin path.
5. Add `PXR_Audio_Spatializer_Audio Listener` to the object that has Unity `Audio Listener`, usually Main Camera.
6. Assign an `AudioClip`, enable `Play On Awake` / `Loop` for testing, and validate on device.

### Environmental acoustic simulation

Use this when reflections and occlusion matter:

1. Import or create environment geometry.
2. Add `PXR_Audio_Spatializer_SceneGeometry` to acoustic geometry.
3. Configure `Include Children`, editor mesh visualization, and static mesh baking.
4. Configure `PXR_Audio_Spatializer_SceneMaterial` using presets or custom absorption/scattering/transmission.
5. Profile CPU usage. Doppler, reflection, and environmental simulation increase audio-thread cost.

### Common audio pitfalls

- Min attenuation distance must not be greater than max attenuation distance.
- Doppler improves realism but increases audio CPU cost.
- Incorrect scene material can make reflections or occlusion sound unnatural.
- Microphone/voice features need clear permission timing and user-facing rationale.

## Tool selection guide

| Tool | Use when | Caveat |
| --- | --- | --- |
| Project Validation | Before any device build or when XR features fail. | Fix all PICO/OpenXR/Android recommendations before deeper debugging. |
| PICO Debugger | Device logs, runtime diagnostics, app troubleshooting. | Not a replacement for feature-specific logs. |
| Metrics HUD | Quick FPS/frame-time/thermal checks on device. | Use with repeatable scenes. |
| XR Profiling Toolkit | XR-focused performance analysis. | Pair with Unity Profiler for script/render-thread details. |
| RenderDoc for PICO | Frame capture, draw call, overdraw, shader/render-target inspection. | Use device-compatible graphics API/settings. |
| Snapdragon Profiler | CPU/GPU/system profiling. | Useful for hardware bottlenecks and thermal behavior. |
| PICO Graphics Probe Tool | Graphics diagnostics and GPU investigation. | Best used after reproducing a rendering symptom. |
| PICO Emulator | Early app flow validation. | Do not rely on it for tracking, camera, VST, MR, SecureMR, haptics, or performance truth. |
| Live Preview / Play-to-PICO | Fast iteration and scene preview on headset. | Connection/device support issues are common; physical APK builds remain necessary. |
| PICO Haptic Editor | Authoring and previewing haptic assets. | Validate haptics on actual controller hardware. |
| PICO XR Portal / Developer Center | SDK/app/service configuration, app ID, platform services, review, distribution. | Store-side configuration must match package/signing/App ID. |

## Review readiness checklist

Before release or store submission:

1. Run Project Validation and fix all blocking/recommended PICO items.
2. Confirm Android baseline: IL2CPP, ARM64, package name, signing, min/target SDK, permissions.
3. Verify manager components exist in loading and gameplay scenes.
4. Validate FPS target on physical devices; for Neo3-class devices target stable 72 FPS.
5. Verify privacy-sensitive capabilities: camera, microphone, recording, Highlights, MRC, Enterprise APIs, SecureMR, eye/face/body tracking.
6. Confirm Platform Services app ID, entitlement, products, test users, and release products.
7. Test Debug and Release builds separately.
8. Collect adb/PICO logs for first launch, entitlement, scene load, pause/resume, and shutdown.
9. Check metadata and user-facing descriptions match actual permissions and features.
10. For media/capture features, document recording behavior and user consent flows.

## Tool troubleshooting quick hits

- Emulator passes but device fails: check device-only features, OS version, permissions, and physical sensor requirements.
- Live Preview cannot connect: verify same network/USB mode, device authorization, supported device, SDK version, and firewall.
- PICO Debugger has no useful logs: increase log level, reproduce from cold start, and filter Unity/PXR/OpenXR/AndroidRuntime.
- Haptics feel wrong: validate amplitude/duration on hardware, not in editor.
- Store build fails entitlement/signature: compare App ID, package name, signing certificate, install source, and Developer Center configuration.
