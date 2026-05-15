# PICO Spatial Apps and Spatial UI Guide

This guide is self-contained. Use it when the user asks about PICO Spatial mode, spatial apps, PICO OS 6 Shared Space / Full Space, spatial UI, Spatial Input, Spatial Camera, or PICO Spatial project setup.

## What PICO Spatial is

PICO Spatial is a spatial-app development path for PICO OS 6. It is intended for UI-centric applications, spatialized mobile-style apps, simple 3D elements, multi-window or panel-style experiences, and apps that should coexist with other applications in the user's environment.

Do not treat PICO Spatial as a replacement for an immersive VR/MR game stack. If the app needs high-performance immersive rendering, Video Seethrough, Spatial Anchor, Shared Spatial Anchor, SecureMR, Environment Depth, Light Estimation, Face/Object Tracking, XR Interaction Toolkit, haptics, compositor layers, or advanced PXR rendering features, prefer PICO XR mode or Unity OpenXR mode.

## Shared Space vs Full Space

| Mode | Meaning | Use when | Important limitation |
| --- | --- | --- | --- |
| Shared Space | Apps and containers are arranged in a system-managed 3D environment, similar to a spatial desktop. | Multitasking, panels, tool apps, content browsing, productivity, simple UI + 3D elements. | The app does not own the entire environment and has limited access to spatial perception. |
| Full Space | The app takes exclusive control of the whole space, similar to full-screen mode. | More immersive spatial UI, AR Foundation Full Space features, larger app-controlled scenes. | Still not equivalent to PICO XR mode; many immersive XR/MR features remain unsupported. |

## Project setup checklist

1. Use the PICO Spatial project template or create a Unity project configured for PICO Spatial SDK.
2. Confirm target device and OS: PICO Spatial targets PICO OS 6 spatial-app behavior.
3. Configure PICO Spatial settings before implementing feature code.
4. Decide the app's space behavior early: Shared Space by default, Full Space only when the app needs exclusive spatial control.
5. Use Unity UI and PICO Spatial UI components for app surfaces; do not assume XR Interaction Toolkit controller interaction is available.
6. Run Project Validation and build to a physical PICO device. Editor-only validation is insufficient for spatial input and spatial window behavior.

## Spatial Input

PICO Spatial mode uses Unity's New Input System and `EnhancedTouch`. The click and drag events are combined into Unity Touch events. Enable the new Input System:

`Edit > Project Settings > Player > Other Settings > Active Input Handling > Input System Package (New)`

Use `SpatialInputSupport.GetInputState(Touch)` to convert an active touch into a spatial input state.

```csharp
using UnityEngine;
using UnityEngine.InputSystem.EnhancedTouch;
using Touch = UnityEngine.InputSystem.EnhancedTouch.Touch;
using TouchPhase = UnityEngine.InputSystem.TouchPhase;
using MultiSpatial;

public class SpatialInputExample : MonoBehaviour
{
    void OnEnable()
    {
        EnhancedTouchSupport.Enable();
    }

    void Update()
    {
        foreach (var touch in Touch.activeTouches)
        {
            var inputState = SpatialInputSupport.GetInputState(touch);
            var target = inputState.targetObject;

            if (target != null && inputState.phase == TouchPhase.Moved)
            {
                target.transform.position = inputState.currentPosition;
                target.transform.rotation = inputState.deviceRotation;
            }
        }
    }
}
```

Practical rules:

- `targetObject` can be null if the target is deleted during interaction; always guard it.
- Design UI around touch-like spatial gestures instead of controller ray assumptions.
- Test click, drag, object deletion during drag, focus changes, and app switching on device.

## Unity UI in PICO Spatial

When using Unity UI / uGUI with PICO Spatial:

- Canvas Render Mode must be `World Space`.
- Add a collider to each interactive button.
- Hover transition is not supported; set button transition to `None`.
- UI Mask is not supported.
- Dynamic TextMesh Pro text is supported for font, color, line spacing, alignment, and size; TMP Font Style is not supported.
- Legacy Text is supported.
- Render order follows Unity sorting logic.

## AR Foundation in PICO Spatial

PICO Spatial can support selected AR Foundation behavior in Full Space, especially UI/spatial-app-oriented use cases. Do not generalize PICO XR / OpenXR MR capability support to PICO Spatial. If the user needs Spatial Anchor, Scene Capture, Spatial Mesh, Video Seethrough, Environment Depth, or Light Estimation, check the capability matrix first; most of these belong to PICO XR mode or Unity OpenXR mode, not PICO Spatial.

## Common pitfalls

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Controller/XRI code does not work | PICO Spatial does not use the same XR Interaction Toolkit path as immersive XR apps. | Use EnhancedTouch + SpatialInput patterns. |
| UI cannot be clicked | Canvas is not World Space or buttons lack colliders. | Set Canvas Render Mode to World Space and add colliders to interactive elements. |
| Hover visual states never trigger | Hover transition is unsupported. | Disable hover transition or implement a Spatial Input-driven visual state. |
| Masked UI appears wrong | UI Mask is unsupported. | Redesign clipping/masking using supported layout/mesh approaches. |
| Developer tries to add Spatial Anchor/VST/SecureMR | Wrong development mode. | Switch to PICO XR or Unity OpenXR depending on feature support. |

## How to answer PICO Spatial questions

1. First decide whether PICO Spatial is actually the right mode. If the app is a complex immersive game or MR environment-understanding app, recommend PICO XR/OpenXR instead.
2. If PICO Spatial is appropriate, ask whether the app should run in Shared Space or Full Space.
3. Ground the answer in spatial UI, EnhancedTouch/SpatialInput, World Space Canvas, and physical-device validation.
4. Explicitly call out unsupported immersive features to prevent wasted implementation time.
