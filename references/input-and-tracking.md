# Input and Tracking Guide

This guide is self-contained. Use it for controller/HMD input, hand tracking, XR Hands, XR Interaction Toolkit, eye tracking, face tracking, body tracking, object tracking, and haptics.

## Controller and HMD input

Prefer Unity XR input APIs for controller buttons and axes:

```csharp
using UnityEngine;
using UnityEngine.XR;

public class PicoInputExample : MonoBehaviour
{
    void Update()
    {
        var rightHand = InputDevices.GetDeviceAtXRNode(XRNode.RightHand);

        if (rightHand.TryGetFeatureValue(CommonUsages.triggerButton, out bool triggerPressed) && triggerPressed)
            Debug.Log("Trigger pressed");

        if (rightHand.TryGetFeatureValue(CommonUsages.trigger, out float triggerValue))
            Debug.Log($"Trigger value={triggerValue}");

        if (rightHand.TryGetFeatureValue(CommonUsages.primary2DAxis, out Vector2 axis))
            Debug.Log($"Thumbstick={axis}");
    }
}
```

Common mappings:

- Menu: `CommonUsages.menuButton`
- Trigger button: `CommonUsages.triggerButton`
- Trigger analog: `CommonUsages.trigger`
- Grip button: `CommonUsages.gripButton`
- Grip analog: `CommonUsages.grip`
- Thumbstick click: `CommonUsages.primary2DAxisClick`
- Thumbstick axis: `CommonUsages.primary2DAxis`
- X/A: `CommonUsages.primaryButton`
- Y/B: `CommonUsages.secondaryButton`

Neo3 HMD Confirm can require old input handling when using `KeyCode.JoystickButton0`. Set Active Input Handling to Both or Input Manager (Old) if needed.

## XR Interaction Toolkit

- XR Interaction Toolkit 2.1.1+ is recommended.
- Use XRI Starter Assets and action-based controllers for maintainable bindings.
- Avoid hardcoding PICO-specific button names in gameplay systems; wrap input into an app-level service such as `IXRInputService`.
- When UI rays or hand/controller interactions fail, check EventSystem, XR UI Input Module, Canvas world camera, interaction layers, action maps, and controller/hand profiles.

## Hand Tracking / XR Hands

Typical setup:

1. Confirm device and SDK support hand tracking.
2. Enable Hand Tracking in the PICO/PXR/OpenXR feature settings for the selected SDK path.
3. Install/enable Unity XR Hands if using the XR Hands route.
4. Choose Controller+Hands or Hands Only behavior based on UX.
5. Configure XRI hand interactors, hand visualizers, and action bindings.
6. Test pinch/select, poke, ray, and grab interactions on device.

Common pitfalls:

- Hand tracking is enabled in project settings but not at runtime/device settings.
- XRI action maps are not assigned or not enabled.
- Interaction layers do not match interactables.
- UI Canvas is not configured for XR interaction.
- Pinch gestures fail because the wrong hand profile or binding set is active.
- High-frequency tracking paths can require Android manifest metadata or SDK-specific toggles.

## Hand pose authoring

For custom hand poses:

- Capture or define reference hand pose data.
- Associate poses with interactables or grab states.
- Keep pose logic tolerant of imperfect tracking.
- Provide controller fallback when hand tracking quality is poor.

## Eye Tracking

Use eye tracking for gaze input, analytics, and ETFR where supported.

Checklist:

1. Confirm device has eye-tracking hardware.
2. Enable eye tracking in PXR/PICO settings.
3. Request permissions/calibration where required by SDK/device path.
4. Check support/state before reading data.
5. Start tracking, poll gaze data, and stop tracking when not needed.
6. Provide fallback for devices without eye tracking.

ETFR caveats:

- ETFR and FFR are mutually exclusive.
- ETFR requires eye-tracking hardware.
- Graphics API support varies by SDK path; validate on target device.

## Face Tracking

Use face tracking for avatar expressions and social presence.

Checklist:

1. Confirm target device supports face tracking.
2. Enable face tracking in PXR/PICO settings.
3. Request permissions and check support/state.
4. Start tracking and map blendshape/viseme values to the avatar rig.
5. Stop tracking when not needed to save resources.

Pitfalls:

- Face tracking is not supported in Unity OpenXR mode according to the general matrix.
- Some modes/devices can trade CPU cost for richer tracking data. Provide quality/performance options.
- Always handle unsupported devices gracefully.

## Body Tracking

Body Tracking can provide body pose/joint data for avatars and fitness/social apps.

Checklist:

1. Confirm body tracking support for target device and accessory path.
2. Check support with the SDK support query where available.
3. Start body tracking.
4. Calibrate trackers when required.
5. Poll body joint data and state.
6. Stop tracking when done.

Common API names in docs include support query, start/stop body tracking, body data retrieval, tracking state retrieval, and motion tracker calibration app launch. Exact signatures can vary by SDK version.

## Object Tracking

- Object Tracking is supported in PICO XR mode but not Unity OpenXR mode or PICO Spatial mode in the general matrix.
- Confirm device, SDK, and object model requirements before promising integration.

## Haptics

Use haptics for controller feedback:

- Confirm selected SDK mode supports Haptic Feedback.
- Trigger haptic impulses through Unity XR or PICO-specific APIs depending on SDK path.
- Keep duration/amplitude reasonable to avoid discomfort.
- Provide fallback when controllers are not active or when using hands-only UX.

## Troubleshooting checklist

- Confirm the selected development mode supports the tracking/input feature.
- Confirm target hardware contains the required sensors.
- Confirm device OS and SDK version.
- Confirm feature toggles and permissions.
- Confirm runtime support/state before polling.
- Confirm action maps, bindings, interaction layers, and EventSystem setup.
- Test on a physical device; many tracking features cannot be validated in Unity Editor.
