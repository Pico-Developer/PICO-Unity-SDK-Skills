# PICO Unity SDK Playbooks

Use this file for quick triage. When the user's question needs implementation-level detail, open the matching bundled guide:

- `mr-environment-understanding.md` for Passthrough/VST, Scene Capture, Spatial Mesh, Plane Detection, Environment Depth, Light Estimation, MR Safeguard, and AR Foundation.
- `platform-services.md` for initialization, Entitlement Check, Accounts, IAP, Subscription, Leaderboard, Achievement, Room/Matchmaking, RTC, and Cloud Storage.
- `performance-rendering.md` for FPS/profiling, Multiview/SPI, FFR/ETFR, AppSW, Late Latching, Adaptive Resolution, Super Resolution, Sharpening, MSAA, and render debugging.
- `input-and-tracking.md` for controller input, XR Interaction Toolkit, hand/eye/face/body tracking, object tracking, and haptics.
- `build-release-troubleshooting.md` for Android build settings, Project Validation, Manifest/permissions, adb logs, release-mode loading issues, signing, Entitlement Check, and store readiness.
- `spatial-anchors.md` for Spatial Anchor and Shared Spatial Anchor setup, lifecycle APIs, code structure, and pitfalls.
- `pico-spatial-apps.md` for PICO Spatial mode, spatial apps, Shared Space / Full Space, Spatial Input, Spatial Camera, and spatial UI constraints.
- `enterprise-and-camera-data.md` for Enterprise Services, enterprise devices, direct camera image access, `PXR_CameraImage`, `PXR_Enterprise`, TobService, and Large Space.
- `securemr.md` for SecureMR tensors, operators, pipelines, QNN model integration, and SecureMR debugging.
- `composition-layers-and-media.md` for compositor/composition layers, crisp UI/video layers, MRC, Highlights, screenshots, recording, and media sharing.
- `spatial-audio-and-tools.md` for Spatial Audio, microphone/audio design, PICO tooling, preview tools, emulator limits, haptics tooling, and review readiness.

## A. New project integration checklist

1. Confirm the target experience: high-performance immersive app, OpenXR cross-platform app, or Spatial UI app.
2. Select the mode: PICO XR, Unity OpenXR, or PICO Spatial.
3. Create a Unity 3D project or a PICO Spatial template project.
4. Import the SDK package through Package Manager -> Add package from disk -> `package.json`.
5. Configure XR Plug-in Management and Android build settings.
6. Add XR Origin / PICO Manager / PXR Manager, and ensure manager components exist in every scene.
7. Run Project Validation and fix Android, XR, permission, and rendering-setting issues.
8. Build and run on a physical device. Validate with adb, PICO Debugger, and Metrics HUD.

If the project is PICO Spatial, split this checklist: use the PICO Spatial project path, choose Shared Space vs Full Space, use EnhancedTouch/SpatialInput instead of XR controller assumptions, and read `pico-spatial-apps.md`.

## B. Passthrough does not display

Read `mr-environment-understanding.md` when the user needs the full MR environment setup or cross-feature troubleshooting.

Investigate in this order:

1. Verify device support, device OS version, SDK version, and the OpenXR Passthrough Feature.
2. Disable HDR in URP and disable all Post Processing.
3. Main Camera: Clear Flags = Solid Color, Background = transparent black / `#00000000`.
4. Do not mix mutually exclusive Reconstruction Passthrough and Projected Passthrough paths.
5. If using `PassthroughFeature.EnableSeeThroughManual(true)`, re-enable it in `OnApplicationPause(false)`.
6. Check whether XR Origin has PICO Manager and whether the relevant Feature Group is enabled.

## C. Input is not responding or mapping is wrong

Read `input-and-tracking.md` when the user asks for exact controller mappings, XR Interaction Toolkit setup, tracking feature gates, or sample code patterns.

1. Use Unity XR `InputDevice.TryGetFeatureValue` and `CommonUsages` for controller buttons.
2. Distinguish Trigger/Grip bool button values from float axis values.
3. On Neo3, if `KeyCode.JoystickButton0` fails with the new Input System, set Active Input Handling to Both or Input Manager (Old).
4. XR Interaction Toolkit 2.1.1 or later is recommended.
5. Built-in controller models are under `Packages/PICO Integration/Assets/Resources/Prefabs`.

## D. Platform services integration

Read `platform-services.md` when the user asks for code patterns, service-specific setup, async/await usage, or release-readiness checks.

1. Verify the app is 64-bit.
2. Configure the app, service, and permissions in the PICO Developer Platform.
3. Initialize Platform Services globally. Game services such as Room, Leaderboard, Achievement, and Challenge require game module initialization.
4. Handle `IsError` for every API call and log `Error.Code` and `Error.Message`.
5. SDK 2.1.4+ can use `Task<T>.Async()` with async/await for clearer serial requests.
6. Add Entitlement Check before release to prevent unauthorized or incorrectly signed runs.

## E. Performance optimization loop

Read `performance-rendering.md` when the user needs a device-specific optimization plan or a feature tradeoff explanation.

1. Establish a baseline on device: FPS, CPU/GPU frame time, Draw Calls, triangle count, memory, and temperature.
2. Tools: Metrics HUD, XR Profiling Toolkit, Snapdragon Profiler, RenderDoc for PICO, and PICO Graphics Probe Tool.
3. Quick settings: disable VSync, enable multithreaded rendering, enable Multiview/SPI, use appropriate MSAA, and set a reasonable display refresh rate.
4. Rendering optimization: batching/instancing, fewer materials and shader variants, texture arrays, LOD, occlusion culling, and fewer transparent objects.
5. PICO capabilities: FFR/ETFR, Adaptive Resolution, AppSW, Late Latching, Buffer Discards, Super Resolution, and Sharpening depending on mode support.
6. For MR scenes, eliminate Passthrough configuration conflicts before applying general rendering optimizations.

## F. SecureMR troubleshooting

1. Device gate: PICO 4 Ultra series, OS 5.13.0+.
2. Enable SecureMR in PXR_Manager and configure VST first.
3. `INVALID PARAMETER` with resolution/shape mismatch: verify that operator output size matches tensor shape.
4. `HANDLE NOT INITIALIZED`: verify tensors are registered into the pipeline through `xrCreateSecureMrPipelineTensorPICO`, and check tensor IDs / pipeline IDs.
5. For QNN/model pipeline issues, use tensor debugging and adb commands to confirm every tensor/operator input and output.

## G. Build or release failure

Read `build-release-troubleshooting.md` when the user needs Android settings, Manifest, logcat filters, signing, release-mode, or store-submission guidance.

1. Check Android platform, 64-bit ABI, min/target SDK, package name, signing, and Manifest permissions.
2. Run Project Validation and fix Unity/PICO recommended settings.
3. Device logs: filter adb logcat for Unity, PXR, OpenXR, Secure MR, and Platform Service.
4. Release mode stuck on loading screen: check initialization order, entitlement/platform-service network callbacks, and missing PXR Manager in scenes.
5. Copyright Verification Failed / Illegal Signature: check signing, PICO Developer Center configuration, Entitlement Check, and install source.

## H. Spatial Anchor integration

Use this quick flow for “how do I integrate spatial anchors?” questions, then read `spatial-anchors.md` for details:

1. Confirm mode support: PICO XR mode or Unity OpenXR mode. Do not use PICO Spatial mode for this feature.
2. Confirm device and OS requirements. Use PICO 4 / PICO 4 Ultra class devices and check OS version against the user's SDK path.
3. Add XR Origin and the correct PICO/PXR manager component.
4. Configure Passthrough / Video Seethrough first.
5. Enable Spatial Anchor in PXR_Manager or the Unity OpenXR PICO Spatial Anchor feature.
6. Start `PxrSenseDataProviderType.SpatialAnchor`.
7. Create anchors with `CreateSpatialAnchorAsync`.
8. Persist anchors with `PersistSpatialAnchorAsync` and store UUIDs in app save data.
9. Query anchors with `QuerySpatialAnchorAsync`; do not run concurrent queries.
10. Locate anchors periodically with `LocateAnchor` and update virtual object transforms.
11. Delete anchors by calling `UnPersistSpatialAnchorAsync` before `DestroyAnchor`.

## I. MR environment understanding feature integration

Use this quick flow for Scene Capture, Spatial Mesh, Plane Detection, Environment Depth, Light Estimation, MR Safeguard, or AR Foundation questions, then read `mr-environment-understanding.md` for details:

1. Confirm the user's development path: PICO XR mode, Unity OpenXR mode, AR Foundation, or PICO Spatial.
2. Verify device, OS, SDK version, and feature availability before giving code.
3. Configure Passthrough/VST first for MR user orientation unless the feature is purely immersive.
4. Enable the relevant PXR Manager checkbox or OpenXR feature group.
5. Start the feature-specific provider or subsystem before querying scene data.
6. Treat scanned scene data as asynchronous and stateful; handle permission, capture, and recapture flows explicitly.
7. For occlusion/depth/lighting issues, check render pipeline, camera settings, feature order, and visual-debug overlays before changing gameplay code.

## J. Platform services feature integration

Use this quick flow for Entitlement Check, Accounts, IAP, Subscription, Leaderboard, Achievement, Room/Matchmaking, RTC, or Cloud Storage questions, then read `platform-services.md` for details:

1. Confirm App ID, package name, signing, 64-bit ABI, developer-console service configuration, and test-user setup.
2. Initialize Platform Services once during app startup before calling service APIs.
3. For game services, initialize the game module where required.
4. Choose one async style consistently: callback `.OnComplete(...)` or SDK 2.1.4+ `await SomeServiceCall().Async()`.
5. Check `IsError` on every message and log the error code/message.
6. Add Entitlement Check and account/login flow before release.
7. Separate sandbox/test products, release products, and store-side configuration when diagnosing IAP/subscription failures.

## K. Input and tracking feature integration

Use this quick flow for controller, hand, eye, face, body, object tracking, haptics, or interaction questions, then read `input-and-tracking.md` for details:

1. Pick the input layer first: Unity XR InputDevice/CommonUsages, XR Interaction Toolkit, Input System, or PICO-specific tracking APIs.
2. For controllers, read bool buttons and analog axes separately; do not infer trigger/grip float values from button booleans.
3. For hand/eye/face/body/object tracking, confirm device support, OS version, SDK package, runtime permission, and user privacy requirements.
4. Enable the relevant capability in PXR/PICO Manager or OpenXR Feature Groups.
5. Handle tracking confidence/lost-tracking states in gameplay and UI.
6. Test on physical devices; editor behavior is not a substitute for tracking validation.

## L. Build, release, and device-log troubleshooting

Use this quick flow for build failures, black screens, device install/runtime issues, signing errors, release-mode loading issues, or store submission questions, then read `build-release-troubleshooting.md` for details:

1. Verify Android baseline: IL2CPP, ARM64, package name, min/target SDK, internet/network permissions if needed, and signing.
2. Run Project Validation and fix every PICO/OpenXR/Android issue before chasing runtime symptoms.
3. Confirm manager components exist in loading scenes as well as gameplay scenes.
4. Reproduce on a physical device and collect adb logcat filtered by Unity, PXR, OpenXR, AndroidRuntime, and Platform Service keywords.
5. For release-only failures, compare Debug vs Release initialization order, stripping, signing, entitlement, network callbacks, and store/developer-console configuration.
6. For store readiness, validate copyright/signature, entitlement, permissions, device compatibility, performance, and privacy-sensitive feature declarations.

## M. PICO Spatial app integration

Use this quick flow for PICO Spatial mode, spatial apps, Shared Space / Full Space, Spatial Input, or spatial UI questions, then read `pico-spatial-apps.md` for details:

1. Confirm the target is truly a spatial app rather than an immersive VR/MR app.
2. Choose Shared Space for multitasking/panel apps; choose Full Space only when the app needs exclusive spatial control.
3. Use PICO Spatial project/template settings and Project Validation.
4. Enable Unity New Input System and use EnhancedTouch + `SpatialInputSupport.GetInputState`.
5. Use World Space Canvas, colliders on UI buttons, no hover transition, and avoid unsupported UI Mask behavior.
6. Do not promise unsupported immersive features such as VST, Spatial Anchor, SecureMR, haptics, or XR Interaction Toolkit.

## N. Enterprise services and camera image data

Use this quick flow for enterprise APIs, device management, direct camera frames, `PXR_CameraImage`, `PXR_Enterprise`, or Large Space questions, then read `enterprise-and-camera-data.md` for details:

1. Distinguish Passthrough display from raw camera image access.
2. Verify device SKU, OS version, enterprise enrollment/policy state, and whether the API is user-device or enterprise-only.
3. Add `android.permission.CAMERA` and request runtime permission where camera data is used.
4. For enterprise APIs, call `PXR_Enterprise.InitEnterpriseService` and `BindEnterpriseService` before feature calls.
5. For `PXR_CameraImage`, enumerate cameras, query capabilities, create device/session, begin capture, acquire/release images, and clean up.
6. For pose/camera alignment, verify intrinsics/extrinsics, tracking origin, and coordinate-system conversion.

## O. SecureMR integration and debugging

Use this quick flow for SecureMR, tensors/operators/pipelines, or QNN model questions, then read `securemr.md` for details:

1. Confirm PICO XR mode, supported PICO 4 Ultra-class device, OS version, and SecureMR capability enabled.
2. Configure VST first if the pipeline consumes camera-derived input.
3. Design tensors with explicit shape, channel, data type, and usage.
4. Create operators, set operands/results, and assemble pipelines in execution order.
5. Convert/package/profile QNN models if model inference is involved.
6. Submit pipelines at a controlled rate and use wait-for/condition/global tensors deliberately.
7. Debug `INVALID PARAMETER` with tensor shapes and `HANDLE NOT INITIALIZED` with lifecycle/ID checks.

## P. Composition layers and media/capture

Use this quick flow for compositor layers, crisp text/video, 180/360 media, MRC, Highlights, screenshots, recording, or sharing questions, then read `composition-layers-and-media.md` for details:

1. Classify the request: high-quality display layer, third-person MRC, user highlight recording/sharing, scene geometry capture, or raw camera frames.
2. For composition layers, verify PICO XR/OpenXR support, layer count, Overlay vs Underlay, shape, depth, texture type, and alpha-hole rules.
3. For MRC, verify MainCamera tag, XR Origin, PXR_Manager MRC checkbox, layer masks, Linear color space with Vulkan, and MRC logs.
4. For Highlights, initialize Platform Services, request user permissions, start a session, capture/record/list/save/share media, and respect regional/store constraints.
5. Do not mix Scene Capture, MRC, Highlights, and raw camera APIs; they solve different problems.

## Q. Spatial Audio and PICO tools

Use this quick flow for Spatial Audio, PICO tooling, preview, emulator, haptics, or review-readiness questions, then read `spatial-audio-and-tools.md` for details:

1. For Spatial Audio, add Context, Audio Source, Audio Listener, and optional Scene Geometry/Material components.
2. Choose free-field audio for simple spatialized sources; use environmental acoustic simulation for reflection/occlusion.
3. Profile audio CPU cost when enabling Doppler/reflections/environment simulation.
4. Pick tools by symptom: Project Validation for setup, Metrics HUD for quick FPS, RenderDoc/Graphics Probe for graphics, PICO Debugger/logcat for runtime, Emulator/Live Preview only for limited iteration.
5. For release, validate privacy-sensitive features, signing/entitlement, Debug vs Release behavior, and store metadata.
