# MR Environment Understanding Guide

This guide is self-contained. Use it for Passthrough/VST, Scene Capture, Spatial Mesh, Plane Detection, Environment Depth, Light Estimation, MR Safeguard, and AR Foundation questions.

## Feature selection

| User goal | Prefer | Key notes |
| --- | --- | --- |
| Show the real world behind virtual content | Passthrough / Video Seethrough | System processes camera imagery; normal apps cannot directly access surrounding images/videos. |
| Restore placed virtual content at real-world positions | Spatial Anchor | See `spatial-anchors.md`. |
| Scan a room and identify walls/floor/furniture | Scene Capture | Uses system Room Capture and scene anchors. |
| Get real-time mesh surfaces | Spatial Mesh | Good for collision/occlusion-like geometry and visualization; manage LOD/perf. |
| Detect horizontal/vertical/arbitrary planes | Plane Detection | Mode/device support is narrower than Scene Capture/Spatial Mesh. |
| Occlude virtual content using real-world depth | Environment Depth | Requires specific devices/OS; Vulkan/Multiview path in docs. |
| Match virtual lighting to the real environment | Light Estimation | Current docs only describe global lighting. |
| Safety reveal near HMD/controllers | MR Safeguard | Experimental/review-sensitive; depends on spatial mesh. |
| Use Unity AR Foundation abstractions | AR Foundation | Support varies by mode and Full Space requirements. |

## Mode support summary

- PICO XR mode supports VST, Spatial Anchor, Shared Spatial Anchor, Scene Capture, Spatial Mesh, Plane Detection, SecureMR, Environment Depth, and Light Estimation.
- Unity OpenXR mode supports VST, Spatial Anchor, Scene Capture, and Spatial Mesh, but does not support Plane Detection, SecureMR, Environment Depth, Light Estimation, or Shared Spatial Anchor in the general mode matrix.
- PICO Spatial mode does not support most immersive MR features, but AR Foundation Session/Camera/Anchor/Mesh can be available in Full Space.

## Passthrough / Video Seethrough essentials

### Requirements and setup

- Reconstruction Passthrough typically requires SDK 1.1.0+; Projected Passthrough/effects require SDK 1.2.0+.
- Common supported device families include PICO Neo3, PICO 4, and PICO 4 Ultra, but newer Video Seethrough docs narrow some paths to PICO 4 Ultra / newer OS. Ask for SDK version and device OS when exact gating matters.
- Main Camera: `Clear Flags = Solid Color`, background transparent black (`R=0,G=0,B=0,A=0`, `#00000000`).
- Disable Post Processing for Passthrough/VST.
- Disable HDR in URP; Video Seethrough with Vulkan + URP/Built-in also requires HDR off.
- Unity OpenXR path: enable `OpenXR Passthrough` in OpenXR Feature Groups.
- PXR path: add `XR Origin`, add `PXR_Manager`, enable `Video Seethrough`, then set `PXR_Manager.EnableVideoSeeThrough = true`.

### API patterns

```csharp
// OpenXR Passthrough path
PassthroughFeature.EnableSeeThroughManual(true);

// PXR Video Seethrough path
PXR_Manager.EnableVideoSeeThrough = true;
PXR_Manager.VstDisplayStatusChanged += status => Debug.Log(status);
```

### Common pitfalls

- Confusing normal Passthrough with direct camera access. Normal apps cannot access the user's surroundings imagery through Passthrough.
- Using opaque black camera background or forgetting alpha=0.
- Leaving HDR/Post Processing enabled.
- Mixing Reconstruction and Projected Passthrough APIs/components.
- Assuming enable calls are instant; listen for VST status changes where available.
- On some older OS paths, color-map effects may cause black screen; test on target OS.

## Scene Capture essentials

Scene Capture uses a system Room Capture app to scan real-world structure and semantic information. It can identify floors, ceilings, walls, doors, windows, openings, tables, sofas, chairs, and in newer docs additional categories such as curtains, cabinets, beds, plants, screens, appliances, lamps, and wall art.

### Setup

- Add `XR Origin` and `PXR_Manager`.
- Set XR Origin and Camera Offset position/rotation to `(0,0,0)` when required by the SDK path.
- Configure Video Seethrough first.
- Enable Scene Capture either in OpenXR Feature Groups (`PICO Scene Capture`) or on `PXR_Manager` (`Scene Capture`) depending on SDK path.

### API flow

```csharp
await PXR_MixedReality.StartSenseDataProvider(PxrSenseDataProviderType.SceneCapture);
var captureResult = await PXR_MixedReality.StartSceneCaptureAsync();
var query = await PXR_MixedReality.QuerySceneAnchorAsync();
// For each scene anchor:
PXR_MixedReality.GetSceneAnchorComponentTypes(anchorHandle, out var componentTypes);
PXR_MixedReality.GetSceneSemanticLabel(anchorHandle, out var label);
PXR_MixedReality.GetSceneBox3DData(anchorHandle, out var box3D);
PXR_MixedReality.GetSceneBox2DData(anchorHandle, out var box2D);
PXR_MixedReality.GetScenePolygonData(anchorHandle, out var polygon);
PXR_MixedReality.LocateAnchor(anchorHandle, out var position, out var rotation);
PXR_MixedReality.StopSenseDataProvider(PxrSenseDataProviderType.SceneCapture);
```

### Notes

- Apps can read/access scene anchors with user permission but cannot modify system scene anchors.
- If no scene anchor data exists, launch Room Capture.
- `LocateAnchor` pose data for scene anchors may only refresh after `QuerySceneAnchorAsync`.
- Scene anchor update events indicate newly discovered data; old anchors may not be removed automatically when the user walks away.

## Spatial Mesh essentials

Spatial Mesh scans real-world surfaces into mesh data with vertices, indices, labels, and change states.

### Setup

- Enable `PICO Spatial Mesh` in OpenXR Feature Groups or `Spatial Mesh` in `PXR_Manager`.
- Add `PXR_Spatial Mesh Manager` where appropriate.
- Mesh prefab must include `Mesh Filter`; add `Mesh Renderer` and material if visualization is needed.
- Choose LOD based on performance:
  - High: about 250 triangle meshes per square meter.
  - Medium: about 125 triangle meshes per square meter.
  - Low: about 80 triangle meshes per square meter.

### API/events

- Start/stop the XR mesh subsystem.
- Listen for `MeshAdded`, `MeshUpdated`, `MeshRemoved`, or `SpatialMeshDataUpdated` events.
- Data includes UUID, state, position, rotation, indices, vertices, and labels.

### Performance notes

- Only mesh data around roughly a 5-meter HMD-centered area is loaded in real time.
- If the app needs larger-area data, store it explicitly.
- Stop real-time mesh updates after capturing/storing data if the app does not need continuous updates.
- Lower LOD to reduce mesh count and CPU/GPU cost.

## Plane Detection essentials

Plane Detection identifies horizontal, vertical, or arbitrary planes such as floors, walls, tables, or sloped surfaces.

### Support cautions

- General mode matrix: supported in PICO XR mode, not Unity OpenXR mode, not PICO Spatial mode.
- Some docs list Project Swan / PICO OS 6 requirements. Ask for target device and SDK path before promising support.

### API flow

```csharp
await PXR_MixedReality.StartSenseDataProvider(PxrSenseDataProviderType.PlaneDetection);
PXR_Manager.PlaneDetectionDataUpdated += OnPlaneDetectionDataUpdated;
// Data: uuid, position, rotation, label, box2D, indices, vertices, state, orientationMode.
PXR_MixedReality.StopSenseDataProvider(PxrSenseDataProviderType.PlaneDetection);
```

Unsubscribe events in `OnDisable` to avoid leaks.

## Environment Depth essentials

Environment Depth provides real-time depth maps for occluding virtual objects behind real-world surfaces.

### Setup and limitations

- General mode matrix: PICO XR mode only.
- Some docs list Project Swan / PICO OS 6 requirements.
- Add `PXR_Environment Depth Manager` to XR Origin.
- Enable `Environment Depth` in PXR_Manager.
- Use Multiview and Vulkan.
- Apply an environment-depth occlusion shader/material, for example a `PICO/EnvironmentDepth/.../OcclusionUnlit` style shader where available.

### APIs

```csharp
await PXR_MixedReality.StartSenseDataProvider(PxrSenseDataProviderType.EnvironmentDepth);
PXR_MixedReality.GetEnvironmentDepthTextureId(ref textureId);
PXR_MixedReality.UPxr_GetEnvironmentDepthFrameDesc(ref desc, eye);
PXR_MixedReality.StopSenseDataProvider(PxrSenseDataProviderType.EnvironmentDepth);
```

## Light Estimation essentials

Light Estimation captures global environmental lighting so virtual objects can better match real-world illumination.

- General mode matrix: PICO XR mode only.
- Some docs list Project Swan / PICO OS 6 requirements.
- Only global lighting is described in current docs.
- Add `PXR_Light Estimation Manager` to XR Origin.
- Enable `Light Estimation` in PXR_Manager.
- Select cubemap/texture resolution.
- Metallic/opaque materials are useful for validating reflections.

```csharp
await PXR_MixedReality.StartSenseDataProvider(PxrSenseDataProviderType.LightEstimation);
PXR_MixedReality.StopSenseDataProvider(PxrSenseDataProviderType.LightEstimation);
```

## MR Safeguard essentials

MR Safeguard reveals the real world when virtual objects come near the HMD/controllers for safety.

- Experimental/review-sensitive feature; final permission can depend on app review.
- HMD detection ball radius is about 20 cm; controller detection ball radius is about 10 cm.
- Requires XR Origin, PXR_Manager, and Spatial Mesh setup.
- Enable `MR Safeguard` in PXR_Manager or OpenXR/PICO Support settings depending on SDK path.
- The SDK can add Android manifest metadata such as `enable_mr_safeguard=1`.
- Best fit: MR apps where users can see surroundings and are not doing fast/intense movement.

## AR Foundation on PICO

### PICO Spatial mode

- Full Space is required for AR Foundation spatial features.
- Common supported features include Session, Anchors, and Meshing; Camera/Anchor/Mesh may be available in Full Space depending on mode matrix.

### PICO Integration path

- AR Foundation support can include Session, Device Tracking, Camera, Face Tracking, Body Tracking, Anchors, and Meshing.
- SDK 3.0.0/3.0.5 paths mention Unity 2022.3 + AR Foundation 5.1.
- SDK 3.1.0 path mentions Unity 6 + AR Foundation 6.0.
- Image tracking is not supported in the inspected docs.
- Enable AR Foundation under `XR Plug-in Management > PICO > Android Settings`, then enable permissions/features as needed.
- Camera setup may automatically set transparent background and add a PXR AR camera effect manager.

## Cross-feature troubleshooting checklist

- Confirm development mode supports the requested MR feature.
- Confirm target device, OS, Unity, SDK, and render pipeline.
- Confirm XR Origin and correct PICO/PXR manager component exist.
- Confirm Passthrough/VST is configured before MR features that depend on environmental observation.
- Confirm HDR/Post Processing settings do not break Passthrough.
- Confirm `StartSenseDataProvider` was called for the correct provider type.
- Confirm the app waits for asynchronous operations and checks `PxrResult`.
- Confirm events are subscribed/unsubscribed correctly.
- For mesh/scene/plane data, guide the user to scan slowly under good lighting and avoid blank/repetitive environments.
