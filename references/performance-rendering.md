# Performance and Rendering Guide

This guide is self-contained. Use it for FPS, profiling, Draw Calls, overdraw, Multiview, foveated rendering, AppSW, Late Latching, Adaptive Resolution, Super Resolution, Sharpening, MSAA, and graphics-tool questions.

## Targets and metrics

- PICO Neo3 series apps should target at least 72 FPS.
- Default display refresh rate is commonly 72 Hz; higher rates such as 90/120 Hz increase performance and thermal pressure.
- Eye buffer resolution strongly affects GPU cost.
- Performance Score guidance from Metrics HUD: below 80 is healthy, 80-100 is risk, above 100 can cause frequent drops.

Monitor:

- FPS / refresh rate
- CPU utilization / GPU utilization
- Performance Score
- Eye Buffer width/height
- Foveation Level
- Singlepass / Multiview status
- CPU/GPU temperature, frequency, memory, battery, current

## Measurement tools

| Tool | Use |
| --- | --- |
| Unity Profiler | CPU, memory, renderer, audio, Unity-level performance. |
| Metrics HUD | On-device real-time FPS, utilization, eye buffer, foveation, temperature. Cannot export raw data. |
| PICO Developer Center / Performance Analyzer | PC-side device metrics and logs. |
| XR Profiling Toolkit | Automated graphics experiments, switch matrices, reports, regression comparisons. |
| Snapdragon Profiler | CPU/GPU timelines, frequency, thermals, memory, power. |
| RenderDoc for PICO | Frame capture, textures, meshes, pipeline/shader analysis. |
| PICO Graphics Probe Tool | GPU real-time data, render-stage trace, draw-call trace. |
| Unity Frame Debugger | Draw-call order and pass inspection. |
| Unity Scene Overdraw view | Transparent overdraw diagnosis. |

## Optimization sequence

1. Establish a physical-device baseline: FPS, CPU/GPU utilization, Perf Score, temperature, eye buffer, render mode.
2. Decide whether the bottleneck is CPU-bound, GPU fragment/fill-rate-bound, GPU geometry-bound, memory-bound, or thermal-bound.
3. Apply low-risk settings first: Multiview/SPI, VSync off, multithreaded rendering, appropriate MSAA, Project Validation fixes.
4. Reduce content cost: Draw Calls, materials, shader variants, transparent overdraw, UI Canvas rebuilds, particles, triangle count, realtime lights.
5. Apply PICO/Unity XR features only where supported: FFR/ETFR, AppSW, Late Latching, Adaptive Resolution, Super Resolution, Sharpening, Buffer Discards.
6. Re-measure with the same route/scene and compare before/after.
7. Run long-duration thermal validation, not only short profiling.

## CPU-bound checklist

- Enable Multiview / Single Pass Instanced.
- Reduce Draw Calls and renderer state changes.
- Share meshes, materials, textures, and shaders.
- Use GPU instancing for repeated objects.
- Reduce Canvas rebuilds; split static/dynamic UI.
- Use Frame Debugger to identify expensive draw-call groups.

## GPU/fill-rate-bound checklist

- Use Overdraw view to find transparent UI/particles/fullscreen overlays.
- Reduce transparent layers, masks, outlines, shadows, fullscreen blur, glass, and particle overdraw.
- Lower render viewport scale or eye buffer resolution carefully.
- Enable FFR/ETFR when supported.
- Reduce full-screen post-processing.
- Reduce MSAA only after evaluating visual quality; 4x is often a practical starting point, 2x can be used under pressure.

## Geometry-bound checklist

- Keep visible triangle counts controlled; roughly one million visible triangles is a useful warning line for Neo3-class targets.
- Use LODs, occlusion culling, and baked lighting.
- Reduce realtime lights and complex shadows.
- Avoid excessive double-sided transparent materials.

## Multiview / Single Pass Instanced

- Reduces duplicated stereo work and can reduce Draw Calls / culling cost.
- Especially useful for CPU-bound scenes.
- Unity OpenXR path: set OpenXR Android Render Mode to Single Pass Instanced / Multi-view.
- PICO XR path: set PICO Android Stereo Rendering Mode to Multiview.
- Heavy post-processing can reduce Multiview benefits.

## Foveated Rendering: FFR and ETFR

### FFR

- Fixed center high-resolution region; lower resolution in periphery.
- Supported on PICO Neo3, PICO 4, and PICO 4 Ultra families in relevant modes.

### ETFR

- Uses eye tracking to move the high-resolution region with gaze.
- Requires eye-tracking hardware such as Neo3 Pro Eye / PICO 4 Pro / PICO 4 Enterprise-class devices.
- ETFR and FFR are mutually exclusive; enable only one.

### Caveats

- OpenXR FFR/ETFR graphics API support can vary. Some docs state ETFR only supports OpenGL in certain OpenXR paths.
- URP intermediate textures or post-processing can make FFR ineffective because FFR is tied to the eye buffer.
- Super Resolution / Sharpening may conflict with subsampling paths.

## AppSW

Application SpaceWarp lets the app render at half the display frame rate while the system synthesizes intermediate frames using eye buffer, motion vectors, and depth.

Typical requirements:

- PICO 4 / PICO 4 Ultra class devices.
- PICO OS 5.11.0+ in inspected docs.
- Unity 2021 LTS+.
- Unity OpenXR Plugin 1.9.1+.
- Vulkan.
- Multiview.
- Motion vectors and depth buffer.

Use AppSW for heavy scenes only after baseline optimization. Verify status with metrics/logs such as app FPS vs display FPS and AppSW on/off. Do not combine blindly with Content Protection because docs mention jitter/ghosting issues in that combination.

## Late Latching

- Reduces motion-to-photon latency and can remove one frame of HMD/controller pose latency.
- Common requirements include Vulkan and Multiview; OpenXR paths can require URP and Unity OpenXR 1.9.1+.
- Debug mode may require Development Build.
- Late Latching with compositor overlay/underlay layers can cause layer jitter in inspected docs.

## Adaptive Resolution, Eye Buffer, Render Viewport Scale

- Adaptive Resolution changes resolution based on GPU load and is supported in PICO XR mode, not Unity OpenXR mode in the general matrix.
- `XRSettings.eyeTextureResolutionScale` reallocates eye textures and is expensive to change frequently; practical range may be 0.8-2.0, but values over 1.5 are not recommended.
- `XRSettings.renderViewportScale` changes the rendered viewport inside the allocated texture and is better for runtime adjustment.
- URP pipeline asset render scale can override adaptive-resolution max scale.

## Super Resolution and Sharpening

### Super Resolution

- Improves clarity with relatively fixed GPU cost.
- Useful when GPU load prevents raising eye buffer resolution directly.
- Avoid if render resolution is already far below default eye buffer resolution because noise can become more visible.
- Does not apply to compositor layers in inspected docs.

### Sharpening

- Enhances high-frequency edges and contours.
- Modes can include Normal and Quality; Quality costs more.
- Can amplify noise or moire.

### Conflicts

- Super Resolution and Sharpening cannot effectively be enabled on the same eye buffer simultaneously; Super Resolution takes priority in inspected docs.
- Both can conflict with subsampling paths.

## Anti-Aliasing / MSAA

- 4x MSAA is a common quality/performance starting point.
- Under CPU/GPU pressure, test 2x.
- 8x can be expensive.
- URP/MSAA combinations may have known performance issues in some Unity versions; test on target device.

## Buffer Discards Optimization

- Vulkan-specific optimization.
- Discards depth buffer contents after rendering instead of resolving/storing unnecessary data.
- Useful on PICO Neo3 / PICO 4 / PICO 4 Ultra class devices with supported OS.

## Semi-transparent objects

- Avoid stacking many transparent layers; PICO docs warn that multi-layer translucent rendering can be problematic.
- For transparent/non-transparent intersections, adjust render queue manually.
- For double-sided transparency, consider `ZWrite Off` and separate front/back passes.
- Premultiplied alpha can improve consistency for transparent UI/particles:
  ```csharp
  PXR_Plugin.Render.UPxr_EnablePremultipliedAlpha(true);
  ```

## Quick recommendations by symptom

| Symptom | First actions |
| --- | --- |
| FPS low, CPU high | Enable Multiview, reduce Draw Calls, use instancing, inspect Frame Debugger. |
| FPS low, GPU high | Reduce overdraw/post-processing, lower viewport scale, enable FFR/ETFR, reduce MSAA. |
| Text blurry | Use TextMeshPro; check eye buffer and MSAA. |
| Aliasing | Start with 4x MSAA, test 2x if under pressure. |
| Thermal throttling | Lower refresh rate/resolution, reduce GPU effects, test long runs. |
| FFR has no effect | Check URP intermediate textures, post-processing, and whether rendering actually targets eye buffer. |
| AppSW not active | Check Vulkan, Multiview, motion vectors, depth, SDK/plugin/device requirements. |
| Layer jitter | Check Late Latching plus compositor overlay/underlay interaction. |
