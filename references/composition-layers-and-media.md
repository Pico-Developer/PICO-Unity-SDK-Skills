# Composition Layers, Media, Capture, and Highlights Guide

This guide is self-contained. Use it when the user asks about compositor layers, composition layers, crisp UI/video layers, equirect/EAC/cubemap/panorama/HDR video layers, Mixed Reality Capture, Highlights, screenshots, recording, or media sharing.

## Composition / compositor layers

Compositor layers display focal content such as text, UI, video, images, or simple backgrounds by passing textures directly to the compositor / ATW path instead of rendering only into the eye buffer. They are useful for high-clarity UI and media because they avoid some eye-buffer sampling and post-processing quality loss.

Typical requirements:

- PICO Neo3 series, PICO 4 series, or PICO 4 Ultra series.
- PICO OS 5.7.0 or later for common compositor layer support.
- PICO XR mode or Unity OpenXR mode. Not PICO Spatial mode.

### Layer limits and comfort

- A scene can have at most 15 compositor layers; layers beyond that are not displayed.
- For performance, recommend no more than 4 compositor layers in one scene.
- Nearby objects should occlude distant ones; incorrect depth/occlusion can create shaking or discomfort.

### Layer types

| Concept | Options | Guidance |
| --- | --- | --- |
| Type | Overlay / Underlay | Overlay is in front of the eye buffer. Underlay is behind the eye buffer and relies on alpha holes in the eye buffer. |
| Shape | Quad, Cylinder, Equirect, Cubemap, Equi-angular Cubemap / EAC | Quad for text/HUD, Cylinder for curved UI, Equirect for 180/360 media, Cubemap/EAC for environment media. |
| Texture Type | Dynamic / Static | Use Dynamic for RenderTexture or per-frame updated media; Static for paintings, fixed images, static backgrounds. |
| Depth | Lower depth composites in front for overlays; underlay ordering is behind eye buffer. | Always set depth intentionally when more than one layer exists. |
| Texture Rects | Source Rects / Destination Rects | Use to crop a texture or map only part of a layer surface. |
| Layer Blend | source/destination color and alpha blending | Use for transparent/semitransparent layers. |
| Override Color Scale | color scale and offset | Use for global color adjustment. |

### Unity setup flow

1. Add `XR Origin (VR)` to the scene.
2. Add `PICO Manager` or the relevant PXR/PICO manager component to `XR Origin`.
3. Ensure the Main Camera under XR Origin has `Tag = MainCamera`.
4. Create a 3D object such as Quad or Cylinder.
5. Add the `CompositeLayerFeature` script to the object.
6. Set Type, Shape, Depth, Texture Type, and Texture.
7. Optionally configure Texture Rects, Layer Blend, and Override Color Scale.
8. Test on device, not just in editor.

Texture update API:

```csharp
// Set a static or dynamic texture on a compositor layer component.
compositeLayerFeature.SetTexture(texture, dynamic: true);
```

### Underlay alpha-hole rule

Underlay textures are behind the eye buffer. The eye buffer must contain transparent areas to reveal the underlay. Use the provided underlay-hole shader/material path or implement a shader that writes the required alpha hole. If the underlay is invisible, first check alpha, clear color, shader, and layer depth.

### Unity XR Composition Layers plugin

For Unity 2022.3 or later, PICO Unity OpenXR SDK 1.3.0+ supports Unity's XR Composition Layers plugin 1.0.0 provider path. Use this route when the project already standardizes on Unity OpenXR Composition Layers. Still validate runtime provider support on PICO hardware.

### Troubleshooting composition layers

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Layer invisible | Exceeded layer count, wrong depth/order, missing texture, camera too close to cylinder surface, unsupported mode/device. | Reduce layer count, verify texture assignment, adjust transform/depth, confirm PICO XR/OpenXR support. |
| Underlay invisible | Eye buffer has no alpha hole. | Use underlay-hole shader/material and transparent eye-buffer regions. |
| Text/video blurry | Content rendered through eye buffer instead of compositor, or texture resolution too low. | Use Quad/Dynamic layer with adequate texture resolution. |
| Layer jitters with Late Latching | Overlay/underlay interaction with late-latched content. | A/B test Late Latching and layer path; avoid mixing moving late-latched objects with sensitive overlays. |
| Super Resolution not affecting layer | Super Resolution applies to eye-buffer rendering, not compositor layers. | Increase layer texture resolution or use layer-specific image-quality features. |

## Mixed Reality Capture (MRC)

Mixed Reality Capture blends physical people with virtual scenes for recorded videos. It is not the same as Scene Capture and does not provide raw camera frames to normal app code.

Requirements and setup:

- PICO Neo3 series, PICO 4 series, or PICO 4 Ultra series.
- PICO OS 4.7.0 or later.
- Main XR camera tag must be `MainCamera`.
- Add `XR Origin` and `PXR_Manager`.
- Enable the `MRC` checkbox on `PXR_Manager`.
- Configure foreground and background layer masks.
- If using Vulkan, set Color Space to `Linear`; Vulkan + Gamma can significantly reduce frame rate.

Useful logs:

- Disabled: `PXR MRC Awake openMRC = False`
- Enabled path: `PXR MRC Awake openMRC = True`, `PXR MRC Init Succeed`, `PXR MRC Camera created`

Common MRC problems:

- First-person video: MRC not enabled, lifecycle blocked, abnormal calibration data, or MRC camera not created.
- Virtual scene scale wrong: third-person camera calibration position data is wrong.
- URP callbacks not executed: URP configuration file not set; enable detailed log level and verify pre/post render callbacks.

## Highlights service

Highlights is a Platform Service for recording and sharing users' moments as images or videos.

Important constraints:

- Available for apps submitted to the PICO Store in Chinese Mainland.
- Requires SDK 2.3.0 or later.
- Requires normal Platform Services setup and initialization.
- Enable Highlight in the PICO Developer Platform.
- In Unity, enable `PICO > Platform Settings > Use Highlight`; this writes manifest metadata such as `use_record_highlight_feature=true`.

Workflow:

1. Initialize Platform Services.
2. `UserService.RequestUserPermissions` for screen capture/record permissions.
3. `HighlightService.StartSession` and store the session ID.
4. Use `HighlightService.CaptureScreen`, `HighlightService.StartRecord`, and `HighlightService.StopRecord`.
5. Use `HighlightService.ListMedia` to retrieve images/videos for the session.
6. Provide a preview UI.
7. Use `HighlightService.SaveMedia` to save to local album or `HighlightService.ShareMedia` to share.
8. Register `HighlightService.SetOnRecordStopHandler` so unexpected stop events still return video path, job ID, and size.

Recording caveat: maximum recording duration is 15 minutes. If `StopRecord()` is not called, the system can end recording automatically.

## Capture/media answer pattern

When answering capture/media questions, first classify the request:

- Need room geometry? Use Scene Capture / Spatial Mesh / Plane Detection.
- Need high-quality UI or video display? Use Composition Layers.
- Need third-person MR videos? Use MRC.
- Need user screenshot/record/share moments? Use Highlights.
- Need raw camera frames? Use `PXR_CameraImage` or enterprise camera APIs only if device/OS/permission requirements are met.

This classification prevents mixing APIs with very different privacy and runtime models.
