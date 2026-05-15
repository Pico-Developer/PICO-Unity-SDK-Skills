# Enterprise Services and Camera Image Data Guide

This guide is self-contained. Use it when the user asks about PICO Enterprise Services, enterprise devices, device management, large-space deployments, direct camera image data, `PXR_CameraImage`, `PXR_Enterprise`, TobService, seethrough camera management, or camera intrinsics/extrinsics.

## Privacy and capability boundary

Do not confuse these three capabilities:

| Capability | What the app gets | Typical use |
| --- | --- | --- |
| Passthrough / VST | System-composited real-world view. Normal apps do not directly receive camera frames. | MR background, projected passthrough, user orientation. |
| `PXR_CameraImage` user-device camera APIs | Enumerated camera devices, properties, intrinsics/extrinsics, and real-time image buffers where supported. | Computer vision, custom camera processing on supported devices. |
| Enterprise camera APIs | Enterprise-device camera stream and pose data through enterprise service APIs. | Enterprise CV, large-space, custom industrial workflows. |

If the user asks “can I access passthrough camera pixels?”, answer conservatively: ordinary Passthrough does not grant raw environment images. Direct camera APIs have separate device/OS/support/permission requirements.

## Enterprise Services overview

Enterprise Service APIs target PICO enterprise devices. Major categories include:

- **Device Info**: device specifications, serial/status information, battery, network, and runtime state.
- **Device Control**: connect to Wi-Fi, scheduled startup/shutdown, device operations.
- **System Setup**: boot/shutdown animations, system language, controller button status, and system customization.
- **System Switch**: enable or disable specified system functions.
- **App Management**: set launcher, auto-start apps after startup, keep apps active, install/manage apps.
- **Screencast**: cast headset screen through Miracast or PICO screencast capability.
- **Large Space**: allow multiple devices to share a map and coordinate system for multi-user large-space collaboration or battles.

Practical integration rules:

1. Confirm the target headset is an enterprise-capable model and that the deployed OS/firmware supports the requested API.
2. Add required Android permissions and any enterprise configuration before runtime calls.
3. Initialize and bind enterprise services before calling enterprise-only APIs.
4. Handle device-policy failures separately from code errors; enterprise APIs may fail because the device is not enrolled, not authorized, or not an enterprise SKU.
5. Treat camera/device-control APIs as privacy-sensitive; document why they are needed and avoid collecting unnecessary data.

## Enterprise service binding pattern

```csharp
using UnityEngine;
using Unity.XR.PXR;

public class PicoEnterpriseBootstrap : MonoBehaviour
{
    void Start()
    {
        PXR_Enterprise.InitEnterpriseService();
        PXR_Enterprise.BindEnterpriseService(success =>
        {
            Debug.Log($"BindEnterpriseService success={success}");
            if (!success)
            {
                // Check enterprise device, enrollment, OS version, permissions, and policy state.
            }
        });
    }
}
```

For coordinate-sensitive camera or large-space workflows, enable global pose where appropriate:

```csharp
PXR_Enterprise.UseGlobalPose(true);
```

## User-device camera image API: `PXR_CameraImage`

`PXR_CameraImage` is a static utility for supported PICO XR devices. It can:

- Enumerate available cameras.
- Query camera properties and capabilities: resolution, format, frame rate, camera model, facing, type, and position.
- Create and manage camera devices and capture sessions.
- Retrieve camera intrinsic and extrinsic parameters.
- Acquire and release camera image data in real time.

Typical requirements:

- PICO 4 Ultra with OS 5.15.0 or later, or Project Swan / PICO OS 6 class devices where supported.
- Android camera permission:

```xml
<uses-permission android:name="android.permission.CAMERA" />
```

Recommended workflow:

1. Request runtime camera permission.
2. `PXR_CameraImage.GetAvailableCameras(out XrCameraIdPICO[] cameraIds)`.
3. Query properties/capabilities such as facing, position, type, model, frame rate, and supported formats.
4. `CreateCameraDeviceAsync`.
5. `CreateCameraCaptureSessionAsync`.
6. `BeginCameraCapture`.
7. In a controlled loop, `AcquireCameraImage`.
8. Process the image.
9. Always `ReleaseCameraImage`.
10. `EndCameraCapture`.
11. Destroy capture session and camera device.

Example capability query:

```csharp
PxrResult result = PXR_CameraImage.GetAvailableCameras(out XrCameraIdPICO[] cameraIds);
if (result == PxrResult.SUCCESS)
{
    foreach (var cameraId in cameraIds)
    {
        Debug.Log($"Camera ID: {cameraId}");
    }
}
```

## Enterprise camera data on PICO 4 Ultra Enterprise

Enterprise camera data access is restricted to PICO 4 Ultra Enterprise. Use `PXR_Enterprise` / `PXRCapture` APIs only after permission, enterprise initialization, and service binding.

Setup:

1. Enable `Custom Main Manifest` in Unity Player settings.
2. Add `android.permission.CAMERA`.
3. Call `PXR_Enterprise.InitEnterpriseService()`.
4. Call `PXR_Enterprise.BindEnterpriseService(...)`.
5. Optionally call `PXR_Enterprise.UseGlobalPose(true)`.
6. Configure camera parameters with `Configurefor4U(...)`.
7. Open camera with `OpenCameraAsyncfor4U(...)`.

Key APIs and concepts:

```csharp
PXR_Enterprise.Configurefor4U(settings);
PXR_Enterprise.OpenCameraAsyncfor4U(success => { /* start image operations after success */ }, settings);
PXR_Enterprise.StartPreviewfor4U(surfacePtr, PXRCaptureRenderMode.PXRCapture_RenderMode_LEFT);
PXR_Enterprise.SetCameraFrameBufferfor4U(width, height, ref dataPtr, OnFrame);
PXR_Enterprise.StartGetImageDatafor4U(mode, width, height);
```

`PXRCaptureRenderMode` commonly distinguishes left camera, right camera, 3D merged output, and interlaced output.

Frame callback data typically includes:

- `width`, `height`
- `timestamp` in nanoseconds
- `datasize`
- `data` pointer
- `UnityEngine.Pose pose`
- `status` where `1` indicates good sensor status and `0` indicates bad sensor status

Coordinate caveat:

- Camera coordinate systems generally use a right-handed system; Unity uses a left-handed system.
- If unifying camera/hand/body pose into a global algorithm coordinate system, explicitly convert poses and verify tracking origin mode, commonly Floor.

## Troubleshooting

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Camera API returns unsupported | Wrong device/OS or wrong SKU. | Confirm PICO 4 Ultra / Enterprise requirements and OS version. |
| Permission dialog never appears | Manifest missing camera permission or runtime request path not reached. | Add `android.permission.CAMERA` and trigger runtime permission via the relevant open/create API. |
| Enterprise bind fails | Not an enterprise device, not enrolled, or policy/service unavailable. | Check device model, enterprise enrollment, service binding logs, and firmware. |
| Image data is distorted/unexpected | Raw vs processed output setting mismatch. | Check configuration keys such as raw-data output and image mode. |
| Pose alignment is wrong | Coordinate-system or tracking-origin mismatch. | Verify Floor tracking origin and left/right-handed conversion. |
| Frame memory grows | Images are acquired but not released. | Always release acquired image buffers and stop/destroy sessions on teardown. |

## Release and review cautions

- Camera access and enterprise device-control features are privacy-sensitive. Explain purpose and data handling clearly.
- Do not put secrets or enterprise credentials in client code.
- Separate consumer-device fallbacks from enterprise-only paths.
- Log `PxrResult` and enterprise bind state with enough detail to diagnose policy/device failures.
