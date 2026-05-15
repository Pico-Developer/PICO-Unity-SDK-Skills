# PICO Unity SDK Self-Contained Reference

This reference is a distilled, standalone knowledge base for PICO Unity SDK work. It is intended to travel with the skill package. Do not assume any external documentation is available to the developer.

## SDK positioning

PICO Unity SDK is used to build XR apps and spatial apps running on PICO OS. The SDK family supports three major development modes:

| Development mode | Best fit | Key caution |
| --- | --- | --- |
| PICO XR mode | High-performance immersive apps, games, complex 3D scenes, advanced rendering, PICO-specific features | Strongest PICO capability coverage, but less cross-platform by design |
| Unity OpenXR mode | Immersive apps that prioritize the OpenXR standard and cross-platform deployment while still using many PICO capabilities | Some PICO-specific features are unavailable |
| PICO Spatial mode | UI-centric spatial apps, simple 3D content, mobile-app spatialization, cross-app collaboration | Many immersive rendering, tracking, and MR features are unsupported or space-state limited |

## Capability matrix summary

Use this table for quick mode selection. Treat it as a practical guide rather than a full API reference.

| Area | Feature | PICO XR mode | Unity OpenXR mode | PICO Spatial mode |
| --- | --- | --- | --- | --- |
| Render | Splash Screen, Screen Fade | Supported | Supported | Not supported |
| Render | Eye Tracked Foveated Rendering (ETFR) | Supported | Supported | Not supported |
| Render | Fixed Foveated Rendering (FFR) | Supported | Supported | Not supported |
| Render | Display Refresh Rate | Supported | Supported | Not supported |
| Render | Composition Layer | Supported | Supported | Not supported |
| Render | Multiview Rendering | Supported | Supported | Not supported |
| Render | Anti-Aliasing | Supported | Supported | Not supported |
| Render | Focus Awareness | Supported | Supported | Not supported |
| Render | Application SpaceWarp (AppSW) | Supported | Supported | Not supported |
| Render | Late Latching | Supported | Supported | Not supported |
| Render | Buffer Discards Optimization | Supported | Supported | Not supported |
| Render | Render Viewport Scaling | Supported | Supported | Not supported |
| Render | Adaptive Resolution | Supported | Not supported | Not supported |
| Render | Super Resolution | Supported | Not supported | Not supported |
| Render | Sharpening | Supported | Not supported | Not supported |
| Interaction | XR Interaction Toolkit | Supported | Supported | Not supported |
| Interaction | System Keyboard | Supported | Supported | Full Space and Shared Space |
| Interaction | Haptic Feedback | Supported | Supported | Not supported |
| Interaction | Tracking Origin | Supported | Supported | Not supported |
| Tracking | Eye Tracking | Supported | Supported | Not supported |
| Tracking | Face Tracking | Supported | Not supported | Not supported |
| Tracking | Hand pose tracking | Supported | Supported | Full Space |
| Tracking | Body Tracking | Supported | Supported | Not supported |
| Tracking | Object Tracking | Supported | Not supported | Not supported |
| MR | Video Seethrough / VST | Supported | Supported | Not supported |
| MR | VST effects | Supported | Supported | Not supported |
| MR | Spatial Anchor | Supported | Supported | Not supported |
| MR | Shared Spatial Anchor | Supported | Not supported | Not supported |
| MR | Scene Capture | Supported | Supported | Not supported |
| MR | Spatial Mesh | Supported | Supported | Not supported |
| MR | Plane Detection | Supported | Not supported | Not supported |
| MR | SecureMR | Supported | Not supported | Not supported |
| MR | Environment Depth | Supported | Not supported | Not supported |
| MR | Light Estimation | Supported | Not supported | Not supported |
| AR Foundation | Session | Supported | Not supported | Full Space |
| AR Foundation | Device tracking | Supported | Supported | Not supported |
| AR Foundation | Camera | Supported | Not supported | Full Space |
| AR Foundation | Face / Body Tracking | Supported | Not supported | Not supported |
| AR Foundation | Anchor / Mesh | Supported | Not supported | Full Space |
| Services | Spatial Audio | Supported | Supported | Not supported |
| Services | Content Protection | Supported | Supported | Full Space and Shared Space |
| Services | Mixed Reality Capture | Supported | Supported | Not supported |
| Services | Platform Services | Supported | Supported | Full Space and Shared Space |
| Services | Enterprise Services | Supported | Supported | Full Space and Shared Space |
| Tools | PICO Portal | Supported | Supported | Full Space and Shared Space |
| Tools | Building Blocks | Supported | Not supported | Not supported |
| Tools | Project Validation | Supported | Supported | Full Space and Shared Space |
| Tools | PICO Debugger | Supported | Supported | Not supported |
| Tools | Live Preview | Supported | Not supported | Not supported |
| Tools | XR Profiling Toolkit | Supported | Supported | Not supported |
| Tools | RenderDoc | Supported | Supported | Not supported |

## Mode-specific recommendations

### PICO XR mode

Recommend PICO XR mode when the app is primarily a PICO-targeted immersive experience or game and needs high performance, complex 3D content, advanced rendering, or maximum PICO feature coverage. It is the safest choice for PICO-specific features such as Adaptive Resolution, Super Resolution, Sharpening, Face/Object Tracking, Shared Spatial Anchor, SecureMR, Environment Depth, Light Estimation, Building Blocks, and Live Preview.

### Unity OpenXR mode

Recommend Unity OpenXR mode when the app is still immersive and performance-sensitive but needs a more standards-based path for possible cross-platform deployment. It supports many important PICO features such as ETFR/FFR, composition layers, Multiview, AppSW, Late Latching, XR Interaction Toolkit, eye/hand/body tracking, VST, Spatial Anchor, Scene Capture, Spatial Mesh, Platform Services, Enterprise Services, PICO Debugger, XR Profiling Toolkit, and RenderDoc. Do not promise unsupported PICO-specific capabilities in this mode.

### PICO Spatial mode

Recommend PICO Spatial mode for UI-centric spatial experiences, simple 3D elements, cross-app collaboration, and spatialized mobile-style apps. Do not recommend it for complex 3D games or immersive MR apps. Many capabilities are either unsupported or limited to Full Space / Shared Space.

For implementation details, use `pico-spatial-apps.md`. Key standalone facts:

- PICO Spatial targets PICO OS 6 spatial apps.
- Shared Space is system-managed multitasking/panel-style spatial desktop behavior.
- Full Space gives exclusive spatial control, but still does not equal PICO XR mode capability coverage.
- Spatial Input uses Unity New Input System `EnhancedTouch` and `SpatialInputSupport`, not normal XR Interaction Toolkit/controller assumptions.
- Unity UI requires World Space Canvas, colliders on buttons, no hover transition, no UI Mask, and TMP Font Style limitations.

## Project setup essentials

### SDK import

For PICO Unity OpenXR SDK, the typical import path is:

1. Create a Unity project.
2. Download and unzip the PICO Unity OpenXR SDK package.
3. In Unity, open `Window > Package Manager`.
4. Click `+ > Add package from disk`.
5. Select the SDK package's `package.json`.
6. Confirm Unity's prompt. Unity may enable native platform backends, disable old Input APIs, and restart.

### Scene structure

- Add XR Origin to XR scenes.
- Add PICO Manager / PXR Manager as required by the selected SDK path.
- PXR Manager is critical for PICO Integration SDK features and should be enabled in every scene, including loading scenes.
- Use Project Validation to catch missing XR Origin, multiple MainCamera tags, missing manager components, unsupported render settings, and Android build configuration issues.

### Android build basics

- Use the Android platform.
- Platform Services require a 64-bit app; IL2CPP + ARM64 is commonly required for release-ready builds.
- Verify package name, signing, Manifest permissions, min/target SDK, Graphics API, and XR provider settings.

## Passthrough / VST essentials

Passthrough allows the real environment to appear behind or within virtual content. PICO processes Passthrough images at the system level. A normal app cannot directly access images or videos of the user's surroundings.

### Typical requirements

- Reconstruction Passthrough: SDK 1.1.0 or later.
- Projected Passthrough and Passthrough effects: SDK 1.2.0 or later.
- Common supported device families include PICO Neo3, PICO 4, and PICO 4 Ultra.
- A common OS baseline is 5.7.0 or later, but newer device-specific features may require newer OS versions.

### Required render setup

- Disable all Post Processing when using Passthrough.
- If using URP, disable HDR; otherwise Passthrough may not work.
- Set the Main Camera to `Clear Flags = Solid Color`.
- Set the Main Camera background to transparent black: `R=0, G=0, B=0, A=0`, equivalent to `#00000000`.
- Enable the relevant OpenXR Passthrough Feature / Feature Group when using Unity OpenXR.

### Reconstruction vs Projected Passthrough

- Reconstruction Passthrough makes the whole background appear as Passthrough. Typical call: `PassthroughFeature.EnableSeeThroughManual(true)`.
- Projected Passthrough shows Passthrough only inside specified geometry or mesh regions. It may require a Passthrough layer component, triangle mesh setup, and an UnderlayHole-style material.
- Do not mix mutually exclusive Reconstruction and Projected Passthrough APIs/components in the same path.
- App pause can disable Passthrough; re-enable it when the app resumes.

```csharp
using UnityEngine;
using Unity.XR.OpenXR.Features.PICOSupport;

public class PicoPassthroughBootstrap : MonoBehaviour
{
    void Awake()
    {
        PassthroughFeature.EnableSeeThroughManual(true);
    }

    void OnApplicationPause(bool pause)
    {
        PassthroughFeature.EnableSeeThroughManual(!pause);
    }
}
```

## Input essentials

Use Unity XR input APIs for controller buttons and axes where possible:

```csharp
using UnityEngine;
using UnityEngine.XR;

public class PicoControllerInputExample : MonoBehaviour
{
    void Update()
    {
        var rightHand = InputDevices.GetDeviceAtXRNode(XRNode.RightHand);
        if (rightHand.TryGetFeatureValue(CommonUsages.triggerButton, out bool triggerPressed) && triggerPressed)
        {
            Debug.Log("Trigger pressed");
        }

        if (rightHand.TryGetFeatureValue(CommonUsages.primary2DAxis, out Vector2 axis))
        {
            Debug.Log($"Thumbstick: {axis}");
        }
    }
}
```

Common mappings:

- Menu: `CommonUsages.menuButton`
- Trigger button: `CommonUsages.triggerButton`
- Trigger analog value: `CommonUsages.trigger`
- Grip button: `CommonUsages.gripButton`
- Grip analog value: `CommonUsages.grip`
- Thumbstick click: `CommonUsages.primary2DAxisClick`
- Thumbstick axis: `CommonUsages.primary2DAxis`
- X/A: `CommonUsages.primaryButton`
- Y/B: `CommonUsages.secondaryButton`

Neo3 HMD Confirm may require old input handling if using `KeyCode.JoystickButton0`; set Active Input Handling to Both or Input Manager (Old) when necessary.

## Platform Services essentials

Platform Services are used for account, entitlement, revenue, social interaction, engagement, communication, and persistence features.

Common services include:

- Accounts & Friends
- Account linking
- Entitlement Check
- RTC
- Speech-to-text
- Room & Matchmaking
- Leaderboard
- Achievement
- Challenge
- Highlights
- In-app purchase (IAP)
- DLC / Subscription
- Exercise data authorization
- Cloud storage
- Profanity detection

Important rules:

- Platform Services only support 64-bit apps.
- Configure the app and services in the PICO Developer Platform before relying on runtime APIs.
- Initialize Platform Services before calling service APIs.
- Game-related services such as Room, Matchmaking, Leaderboard, Achievement, and Challenge require game module initialization in addition to global platform initialization.
- Handle `IsError`, `Error.Code`, and `Error.Message` for every service call.
- SDK 2.1.4+ supports async/await-style calls via `Task<T>.Async()`.

Callback-style example:

```csharp
UserService.GetLoggedInUser().OnComplete(m =>
{
    if (m.IsError)
    {
        Debug.Log($"GetLoggedInUser failed: code={m.Error.Code} message={m.Error.Message}");
        return;
    }

    Debug.Log($"DisplayName={m.Data.DisplayName} UserId={m.Data.ID}");
});
```

Async-style example:

```csharp
var userMessage = await UserService.GetLoggedInUser().Async();
if (userMessage.IsError)
{
    Debug.Log($"GetLoggedInUser failed: code={userMessage.Error.Code} message={userMessage.Error.Message}");
    return;
}

Debug.Log($"DisplayName={userMessage.Data.DisplayName} UserId={userMessage.Data.ID}");
```

## Performance essentials

### Targets

- On PICO Neo3 series devices, the app should target at least 72 FPS.
- High Draw Calls can be caused by frequent pipeline state changes, unique materials/shaders/textures/meshes, UI Canvas rebuilds, and insufficient instancing or batching.
- Keep visible triangle counts controlled; around one million visible triangles is a useful practical warning line for Neo3-class targets.

### First checks

- Disable VSync so the app can control its own frame pacing.
- Enable multithreaded rendering.
- Use Multiview / Single Pass Instanced where supported.
- Use a sensible MSAA level; 4x is often a practical starting point.
- Use FFR or ETFR where device and mode support it.
- Consider Late Latching for reducing HMD/controller pose latency.
- Use Adaptive Resolution, Super Resolution, Sharpening, AppSW, or Buffer Discards only where the selected mode and device support them.

### Optimization focus

- Reduce Draw Calls through shared materials, shader simplification, batching, and GPU instancing.
- Reduce shader variants and avoid excessive keyword combinations.
- Reduce transparent overdraw from UI, particles, glass effects, outlines, masks, and fullscreen overlays.
- Split static and dynamic UI Canvases to avoid expensive full-Canvas rebuilds.
- Disable raycast targets for non-interactive UI graphics.
- Use LOD, occlusion culling, baked lighting, fewer realtime lights, and simplified shadows.

### Tools

- Metrics HUD: on-device FPS, CPU/GPU utilization, temperature, eye buffer, foveation level, and rendering mode.
- XR Profiling Toolkit: compare rendering switches such as Multiview, MSAA, FFR, and resolution.
- Snapdragon Profiler: CPU/GPU timelines, frequency, thermals, and power.
- RenderDoc for PICO: inspect expensive frames, passes, textures, and draw calls.
- PICO Debugger / PICO Graphics Probe Tool: device-side debugging and graphics state inspection.

## Composition layers and media essentials

Read `composition-layers-and-media.md` for compositor layers, Mixed Reality Capture, Highlights, screenshots, recording, and media-sharing questions.

- Composition layers are useful for crisp text, high-quality UI, video, panoramic media, and simple focal surfaces.
- Supported common layer concepts include Overlay, Underlay, Quad, Cylinder, Equirect, Cubemap, EAC, Dynamic Texture, Static Texture, depth ordering, texture rects, blend, and color scale.
- Do not add more than 15 compositor layers; recommend no more than 4 for performance.
- Underlay requires alpha holes in the eye buffer.
- Super Resolution and many eye-buffer image-quality operations do not automatically improve compositor layers.
- Mixed Reality Capture requires MainCamera tag, XR Origin, PXR_Manager MRC enablement, layer masks, and logs such as `PXR MRC Init Succeed`.
- Highlights is a Platform Service for screenshot/record/share workflows and has store/region/service-enable requirements.

## Enterprise and camera data essentials

Read `enterprise-and-camera-data.md` for Enterprise Services, direct camera image data, enterprise camera data, Large Space, and TobService questions.

- Ordinary Passthrough/VST does not give normal apps raw camera frames.
- `PXR_CameraImage` can enumerate supported cameras, query properties/capabilities, create device/session, begin capture, acquire/release images, and access camera intrinsics/extrinsics where supported.
- User-device camera image APIs require device/OS support and `android.permission.CAMERA`.
- Enterprise camera APIs are restricted to enterprise-capable devices such as PICO 4 Ultra Enterprise and require enterprise service initialization/binding.
- Enterprise Services include Device Info, Device Control, System Setup, System Switch, App Management, Screencast, and Large Space.

## SecureMR essentials

- SecureMR requires PICO 4 Ultra series devices and OS 5.13.0 or later.
- Enable SecureMR in PXR_Manager.
- Configure VST before implementing SecureMR experiences.
- SecureMR development centers on tensors, operators, and pipelines; read `securemr.md` for integration details.
- Tensor shape, channel, data type, and usage must exactly match operator/model expectations.
- Pipelines should be submitted at a controlled rate to avoid queue buildup.
- Common `INVALID PARAMETER` errors can come from operator output shape / resolution mismatches against tensor configuration.
- Common `HANDLE NOT INITIALIZED` errors can come from tensors not registered into the pipeline, incorrect tensor IDs, or incorrect pipeline IDs.
- Verify tensor, operator, and pipeline wiring before assuming model inference failure.

## Spatial Audio and tool essentials

Read `spatial-audio-and-tools.md` for Spatial Audio, microphone/audio design, PICO Emulator, Live Preview, PICO Debugger, PICO Haptic Editor, Graphics Probe, and review-readiness questions.

- Spatial Audio commonly uses `PXR_Audio_Spatializer_Context`, `PXR_Audio_Spatializer_Audio Source`, `PXR_Audio_Spatializer_Audio Listener`, `PXR_Audio_Spatializer_Scene Geometry`, and `PXR_Audio_Spatializer_Scene Material`.
- Free-field audio is simpler; environmental acoustic simulation adds reflections, occlusion, absorption, scattering, and transmission.
- PICO Emulator and Live Preview are useful for iteration but do not replace physical-device validation for tracking, haptics, camera, VST, SecureMR, or performance.

## Common release and troubleshooting reminders

- Use Project Validation before device builds and before release submission.
- For device logs, filter for Unity, PXR, OpenXR, Passthrough, VST, composition, Secure MR, and Platform Service keywords.
- If Release mode gets stuck on loading, check service initialization order, entitlement/network callbacks, and whether every scene has the required PXR/PICO manager component.
- For copyright verification or illegal signature errors, check signing, developer console configuration, entitlement setup, and install source.
