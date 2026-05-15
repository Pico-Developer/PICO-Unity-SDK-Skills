---
name: pico-unity-sdk
description: Expert assistance for PICO Unity SDK, PICO XR, Unity OpenXR, and PICO Spatial development, migration, feature integration, debugging, performance optimization, and release readiness. Use this skill proactively whenever the user mentions PICO, PICO Unity SDK, PXR, PICO XR, OpenXR, PICO Spatial, spatial apps, XR/MR/VR, Passthrough/VST, spatial anchors, Scene Capture, Spatial Mesh, SecureMR, Enterprise Services, camera image data, composition/compositor layers, Mixed Reality Capture, Highlights, Spatial Audio, hand/eye/face/body tracking, platform services, Unity builds for PICO devices, PICO performance, or PICO-specific troubleshooting, even if the user does not explicitly ask for the PICO SDK skill.
version: 0.11.3
---

# PICO Unity SDK Expert Workflow

Act as a senior PICO Unity SDK engineering consultant. Convert the user's request into an actionable Unity/PICO implementation plan, code guidance, project configuration checklist, troubleshooting flow, or review report. Prefer this skill's references and the user's current project files over generic Unity/XR advice.

## Classify the user's task first

Select the workflow based on the task type:

1. **Project setup / SDK integration**: Unity version, package import, development mode selection, XR Plug-in Management, PXR/PICO Manager, Android build settings.
2. **Mode selection / migration**: capability differences, limitations, and migration strategies across PICO XR mode, Unity OpenXR mode, and PICO Spatial mode.
3. **Feature integration**: input, hand/eye/face/body tracking, Passthrough/VST, spatial anchors, Scene Capture, Spatial Mesh, AR Foundation, PICO Spatial apps, Platform Services, Enterprise Services, camera image data, SecureMR, composition layers, MRC/Highlights, Spatial Audio.
4. **Performance / visual quality optimization**: 72 FPS target, Draw Calls, Multiview/SPI, foveated rendering, Adaptive Resolution, AppSW, Late Latching, MSAA, composition layers, URP/HDR/Post Processing conflicts.
5. **Build / device / log troubleshooting**: adb, device OS version, permissions, Manifest, Project Validation, PICO Debugger, loading black screen, signature/copyright verification, streaming issues.
6. **Code review / architecture review**: PICO SDK API call order, lifecycle handling, device/OS/SDK version gates, asynchronous error handling, and platform restrictions.

## Information gathering

If the user has not provided key context, ask the smallest set of questions that can change the recommendation. If the answer can be inferred from project files, inspect those files first.

- Target device: PICO 4 Ultra, PICO 4, Neo3, etc.
- Unity version and render pipeline: Built-in or URP.
- XR stack: PICO XR, Unity OpenXR, AR Foundation, or PICO Spatial.
- SDK name and version: PICO Unity Integration SDK, PICO Unity OpenXR SDK, or PICO Spatial SDK.
- Target capability: immersive VR, Mixed Reality, spatial app, platform services, enterprise device features.
- Reproduction details: error logs, device OS version, build mode, physical device vs. editor, Release mode, Android ABI.

## Reference strategy

- Read `references/sdk-map.md` first. It is a self-contained distilled reference, not an index to external documents.
- For troubleshooting, performance, MR, or platform services tasks, also read `references/playbooks.md`.
- For Spatial Anchor or Shared Spatial Anchor integration, read `references/spatial-anchors.md`; it contains the self-contained setup flow, lifecycle APIs, code skeleton, UX guidance, and common pitfalls.
- For Passthrough/VST, Scene Capture, Spatial Mesh, Plane Detection, Environment Depth, Light Estimation, MR Safeguard, or AR Foundation questions, read `references/mr-environment-understanding.md`.
- For Platform Services, Entitlement Check, Accounts, IAP, Subscription, Leaderboard, Achievement, Room/Matchmaking, RTC, or Cloud Storage questions, read `references/platform-services.md`.
- For FPS, profiling, Multiview, FFR/ETFR, AppSW, Late Latching, Adaptive Resolution, Super Resolution, Sharpening, MSAA, RenderDoc, Snapdragon Profiler, or Draw Call questions, read `references/performance-rendering.md`.
- For controller input, hand tracking, eye tracking, face tracking, body tracking, haptics, or XR Interaction Toolkit questions, read `references/input-and-tracking.md`.
- For Android build, manifest, Project Validation, logs, release-mode failures, signing, entitlement release failures, or store-readiness questions, read `references/build-release-troubleshooting.md`.
- For PICO Spatial mode, spatial apps, Shared Space / Full Space, Spatial Input, Spatial Camera, spatial UI, or Unity UI constraints in PICO Spatial, read `references/pico-spatial-apps.md`.
- For Enterprise Services, enterprise device management, direct camera image data, `PXR_CameraImage`, `PXR_Enterprise`, TobService, camera intrinsics/extrinsics, or Large Space questions, read `references/enterprise-and-camera-data.md`.
- For SecureMR, tensors, operators, pipelines, QNN model integration, readback tensors, dynamic textures, or SecureMR debugging, read `references/securemr.md`.
- For compositor/composition layers, crisp UI/video layers, equirect/EAC/cubemap media, Mixed Reality Capture, Highlights, screenshots, recording, or media sharing, read `references/composition-layers-and-media.md`.
- For Spatial Audio, microphone/audio design, PICO Emulator, Live Preview, Play-to-PICO, PICO Debugger, PICO Haptic Editor, PICO Graphics Probe Tool, or review-readiness tool selection, read `references/spatial-audio-and-tools.md`.
- Do not assume the developer has access to any external documentation used during skill creation. Do not point the user to local source documents that are not bundled with the skill. If you need to cite files, cite only files in the user's current project or files bundled inside this skill.

## Engineering judgment

### Development mode selection

- **PICO XR mode**: Best for high-performance immersive experiences, complex 3D scenes, and the broadest set of PICO-specific capabilities. Prefer it when the project needs Adaptive Resolution, Super Resolution, Sharpening, Face/Object Tracking, Shared Spatial Anchor, SecureMR, Environment Depth, Light Estimation, Building Blocks, Live Preview, or maximum PICO feature coverage.
- **Unity OpenXR mode**: Best for immersive experiences that prioritize the OpenXR standard and cross-platform deployment while still using many PICO capabilities. Be careful: several PICO-specific capabilities are not supported.
- **PICO Spatial mode**: Best for UI-centric experiences, simple 3D elements, cross-app collaboration, or spatializing mobile apps. Many rendering, interaction, tracking, and MR capabilities are unavailable or constrained by Full Space / Shared Space.

### PICO Spatial apps

- PICO Spatial is for spatial-app and UI-centric development, not a general substitute for immersive PICO XR/OpenXR apps. Its input model is based on Unity New Input System `EnhancedTouch` and PICO Spatial Input, not normal controller/XR Interaction Toolkit assumptions.
- For Unity UI in PICO Spatial, require World Space Canvas, colliders on interactive buttons, no hover transition, no UI Mask, and TMP Font Style limitations.
- Always distinguish Shared Space and Full Space before recommending AR Foundation or spatial-data behavior.

### Scene and manager components

- PXR Manager / PICO Manager is the entry point for many PICO features. PXR Manager must be enabled in every scene, including loading scenes, or feature state and scene transitions may behave incorrectly.
- Unity OpenXR scenes typically need XR Origin, PICO Manager, and the relevant OpenXR Feature Group or feature component.
- Before using platform services, verify 64-bit app support and initialize Platform Services. Game-related services such as Room, Leaderboard, Achievement, and Challenge also require game module initialization.

### Passthrough / VST / Mixed Reality

- Passthrough images are processed directly by the PICO system. A normal app cannot directly access images or videos of the user's surroundings. If the user asks for camera images, distinguish enterprise device APIs, user-device APIs, privacy constraints, and permission requirements.
- Common Passthrough requirements: supported device/OS/SDK version, Post Processing disabled, HDR disabled in URP, Main Camera Clear Flags set to Solid Color with transparent black background, and OpenXR Passthrough extension enabled.
- Do not mix mutually exclusive Reconstruction Passthrough and Projected Passthrough paths. If using `PassthroughFeature.EnableSeeThroughManual`, re-enable it after app pause/resume.
- If the user asks for raw camera images, do not answer with Passthrough alone. Route to `PXR_CameraImage` or Enterprise camera APIs and verify device, OS, manifest permission, runtime permission, and privacy constraints.

### Enterprise, SecureMR, media, and layers

- Enterprise Services require enterprise-capable devices and policy/service binding. Separate device-policy failure from ordinary API failure.
- SecureMR answers should include device/mode gates, VST/SecureMR setup, tensor/operator/pipeline architecture, QNN/model packaging if applicable, and shape/handle debugging.
- Composition layers are ideal for crisp UI, video, and panoramic media, but have layer-count, depth, alpha, overlay/underlay, and Late Latching caveats. Do not apply eye-buffer-only features such as Super Resolution to compositor layers.
- Mixed Reality Capture, Highlights, Scene Capture, and raw camera APIs solve different problems; classify the capture request before recommending APIs.

### Input and interaction

- For controller input, prefer Unity XR `InputDevice.TryGetFeatureValue` with `CommonUsages`: `triggerButton`, `trigger`, `gripButton`, `grip`, `primary2DAxis`, `primaryButton`, `secondaryButton`, and `menuButton`.
- On Neo3, querying `KeyCode.JoystickButton0` for HMD Confirm may fail with the new Input System. Set Active Input Handling to Both or Input Manager (Old) if needed.
- XR Interaction Toolkit 2.1.1 or later is recommended.

### Performance and visual quality

- For PICO Neo3 series devices, target at least 72 FPS. Start with measurement: FPS, Draw Calls, triangle count, CPU/GPU bottlenecks, render pipeline state, and thermal behavior.
- Check these first: disable VSync, enable multithreaded rendering, enable Multiview/SPI, use appropriate MSAA, enable FFR/ETFR where supported, consider Late Latching, Adaptive Resolution/AppSW where supported, reduce material and shader variants, use instancing, and reduce transparent overdraw.
- For MR/Passthrough issues, first eliminate HDR/Post Processing/transparent background/feature-toggle conflicts before treating the issue as a generic performance problem.

## Output formats

Use the user's language for the final answer unless they request otherwise. Keep Unity menu names, components, APIs, and SDK terms in English.

### Integration / implementation tasks

```markdown
## Recommended approach
One sentence describing the mode/technical path and why.

## Prerequisites
- Device / OS / SDK / Unity / permissions / service configuration

## Unity configuration steps
1. ...

## Code or component integration
```csharp
// Minimal working code or critical API calls
```

## Verification
- Physical-device checks, log keywords, expected behavior

## Common pitfalls
- Constraints and conflicts relevant to this exact approach
```

### Troubleshooting tasks

```markdown
## Initial diagnosis
Most likely cause and why.

## Investigation order
1. Lowest-cost / highest-probability checks
2. Configuration / version / permission checks
3. Code lifecycle / API call-order checks
4. Logs / adb / profiler verification

## Fix recommendations
- Concrete changes

## Missing information
- Only list information that blocks further diagnosis
```

### Review tasks

```markdown
## Verdict
Pass / risky / blocking.

## Findings
- [Severity] file:line — issue, consequence, fix

## PICO-specific checklist
- Development mode support
- Device / OS / SDK version gates
- Permissions / Manifest / 64-bit / initialization
- Lifecycle and pause/resume handling
- Performance and visual-quality conflicts
```

## Quality bar

- Do not stop at conceptual explanations. Ground the answer in Unity menus, components, APIs, Manifest entries, device versions, or verification commands.
- Clearly distinguish PICO XR, Unity OpenXR, and PICO Spatial. Do not apply one mode's capabilities to another mode.
- Be conservative about privacy and platform limitations: Passthrough imagery is not directly accessible to normal apps; enterprise and user-device camera APIs must be handled separately.
- For platform services and monetization, mention initialization, 64-bit, developer console configuration, and asynchronous error handling.
- For performance, use a measure-before-optimizing loop: Metrics HUD, XR Profiling Toolkit, Snapdragon Profiler, RenderDoc, and PICO Debugger where applicable.
