# Spatial Anchor and Shared Spatial Anchor Guide

This guide is self-contained. Use it when the user asks how to integrate, persist, query, locate, delete, troubleshoot, or share PICO spatial anchors.

## What spatial anchors do

Spatial anchors bind positions in the Unity virtual scene to positions in the user's real environment. After an anchor is created and persisted, the app can later query it and restore virtual content at the same real-world location when the user returns to that space.

Common use cases:

- Place and restore virtual objects in real rooms.
- Save room-specific props, characters, UI panels, or game objects.
- Blend gameplay or productivity content with real-world environmental positions.
- Share synchronized content among users in the same physical space using Shared Spatial Anchors.

## Core concepts

| Concept | Meaning | Practical implication |
| --- | --- | --- |
| UUID | A persistent unique identifier assigned when an anchor is created. | Store this in the app if you want to reload a specific anchor later. |
| Handle | A runtime reference that associates an in-memory anchor with a persisted anchor. | Handles are not permanent and may change after app restart. Use them for current-session operations. |
| Persisted anchor | An anchor saved to the device's local disk. | Can be queried later on the same device in the same space. |
| Shared spatial anchor | A local spatial anchor uploaded to PICO cloud and shared by UUID. | Requires login, platform services, networking/UUID exchange, and device support. |

## Mode and device support

### Spatial Anchor

- Supported in PICO XR mode.
- Supported in Unity OpenXR mode.
- Not supported in PICO Spatial mode according to the general development-mode matrix.
- Typical newer Integration SDK requirement: PICO 4 series / PICO 4 Ultra series with PICO OS 5.14.0 or later.
- Some OpenXR-path documents mention PICO 4 Ultra series / PICO Swan with OS 5.11.0 or later. When the user's SDK path is unclear, ask for SDK name/version and target OS; otherwise recommend using the newer stated requirement as the safer baseline.

### Shared Spatial Anchor

- Requires PICO 4 series / PICO 4 Ultra series.
- Requires PICO OS 5.15.0 or later.
- Requires users to be logged in on their PICO devices.
- Requires app ID configuration, Platform Services initialization, and a way to exchange anchor UUIDs between users.

## Unity setup checklist for Spatial Anchor

Use this checklist before writing code:

1. Confirm the app is using a mode that supports Spatial Anchor: PICO XR mode or Unity OpenXR mode.
2. Confirm the target device and OS meet the feature requirements.
3. Add `XR Origin` to the scene.
4. Add `PXR_Manager (Script)` to the `XR Origin` object when using the PXR/Integration SDK path.
5. Set up Passthrough / Video Seethrough first. Spatial anchors are normally used in MR flows where users need to observe the real environment.
6. Enable Spatial Anchor capability:
   - PXR_Manager path: in the Inspector, enable the `Spatial Anchor` checkbox on `PXR_Manager (Script)`.
   - Unity OpenXR path: open `Edit > Project Settings > XR Plug-in Management > OpenXR > OpenXR Feature Groups > All Features`, then enable `PICO Spatial Anchor`.
7. If AR Foundation v5.1.2+ is installed and the user wants to use PICO SDK APIs instead of AR Foundation's anchor subsystem, disable `Is Anchor Subsystem` in the `PICO Spatial Anchor` settings.
8. Run Project Validation and fix PICO/OpenXR/Android issues before testing on device.

## Spatial Anchor lifecycle

The standard lifecycle is:

1. Start the Spatial Anchor data provider.
2. Create an anchor at a world-space position and rotation.
3. Persist the anchor if it must survive app restart.
4. Store the returned UUID in the app's own save data if you need to query a specific anchor later.
5. Query anchors from memory or device local storage.
6. Locate anchors periodically to keep virtual objects aligned with the real world.
7. When deleting content, unpersist the anchor first, then destroy the runtime anchor handle.
8. Stop the data provider when all anchor operations are complete.

## API summary

The key API names and signatures commonly used by PICO spatial anchors are:

```csharp
// Start / stop the Spatial Anchor data provider.
async Task<PxrResult> StartSenseDataProvider(PxrSenseDataProviderType type);
PxrResult StopSenseDataProvider(PxrSenseDataProviderType type);

// Optional state check.
PxrResult GetSenseDataProviderState(PxrSenseDataProviderType type, out PxrSenseDataProviderState state);

// Create an anchor in app memory.
async Task<(PxrResult result, ulong anchorHandle, Guid uuid)> CreateSpatialAnchorAsync(Vector3 position, Quaternion rotation);

// Persist / unpersist from device local disk.
async Task<PxrResult> PersistSpatialAnchorAsync(ulong anchorHandle);
async Task<PxrResult> UnPersistSpatialAnchorAsync(ulong anchorHandle);

// Query anchors. Passing null loads all available anchors created by the current app.
async Task<(PxrResult result, List<ulong> anchorHandleList)> QuerySpatialAnchorAsync(Guid[] uuids = null);

// Get UUID and real-time pose.
PxrResult GetAnchorUuid(ulong anchorHandle, out Guid uuid);
PxrResult LocateAnchor(ulong anchorHandle, out Vector3 position, out Quaternion rotation);

// Destroy from app memory.
PxrResult DestroyAnchor(ulong anchorHandle);
```

Use `PxrSenseDataProviderType.SpatialAnchor` when starting/stopping or querying provider state.

## Minimal API-based implementation skeleton

The exact namespace and class names can vary slightly by SDK version. Treat this as a structure to adapt to the user's installed SDK.

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using UnityEngine;
using Unity.XR.PXR;

public class PicoSpatialAnchorController : MonoBehaviour
{
    private readonly List<ulong> _runtimeAnchorHandles = new();
    private bool _providerStarted;

    public async Task<bool> StartSpatialAnchorAsync()
    {
        var result = await PXR_MixedReality.StartSenseDataProvider(PxrSenseDataProviderType.SpatialAnchor);
        _providerStarted = result == PxrResult.SUCCESS;
        Debug.Log($"Start SpatialAnchor provider: {result}");
        return _providerStarted;
    }

    public async Task<Guid?> CreateAndPersistAnchorAsync(Vector3 position, Quaternion rotation)
    {
        if (!_providerStarted)
        {
            Debug.LogWarning("SpatialAnchor provider is not started.");
            return null;
        }

        var create = await PXR_MixedReality.CreateSpatialAnchorAsync(position, rotation);
        if (create.result != PxrResult.SUCCESS)
        {
            Debug.LogError($"CreateSpatialAnchorAsync failed: {create.result}");
            return null;
        }

        var persist = await PXR_MixedReality.PersistSpatialAnchorAsync(create.anchorHandle);
        if (persist != PxrResult.SUCCESS)
        {
            Debug.LogError($"PersistSpatialAnchorAsync failed: {persist}");
            PXR_MixedReality.DestroyAnchor(create.anchorHandle);
            return null;
        }

        _runtimeAnchorHandles.Add(create.anchorHandle);
        Debug.Log($"Anchor created and persisted. uuid={create.uuid}, handle={create.anchorHandle}");
        return create.uuid;
    }

    public async Task<List<ulong>> QueryAnchorsAsync(Guid[] uuids = null)
    {
        var query = await PXR_MixedReality.QuerySpatialAnchorAsync(uuids);
        if (query.result != PxrResult.SUCCESS)
        {
            Debug.LogError($"QuerySpatialAnchorAsync failed: {query.result}");
            return new List<ulong>();
        }

        foreach (var handle in query.anchorHandleList)
        {
            if (!_runtimeAnchorHandles.Contains(handle))
                _runtimeAnchorHandles.Add(handle);
        }

        return query.anchorHandleList;
    }

    public bool TryLocateAnchor(ulong anchorHandle, out Vector3 position, out Quaternion rotation)
    {
        var result = PXR_MixedReality.LocateAnchor(anchorHandle, out position, out rotation);
        return result == PxrResult.SUCCESS;
    }

    public async Task DeleteAnchorAsync(ulong anchorHandle)
    {
        // Important: unpersist before DestroyAnchor, otherwise the runtime handle is lost
        // and the SDK may not be able to locate the persisted anchor for deletion.
        var unpersist = await PXR_MixedReality.UnPersistSpatialAnchorAsync(anchorHandle);
        Debug.Log($"UnPersistSpatialAnchorAsync: {unpersist}");

        var destroy = PXR_MixedReality.DestroyAnchor(anchorHandle);
        Debug.Log($"DestroyAnchor: {destroy}");

        _runtimeAnchorHandles.Remove(anchorHandle);
    }

    private void OnDestroy()
    {
        if (_providerStarted)
        {
            PXR_MixedReality.StopSenseDataProvider(PxrSenseDataProviderType.SpatialAnchor);
            _providerStarted = false;
        }
    }
}
```

## Component / prefab path

For SDK versions that provide `PXR_SpatialAnchor`:

- Add `PXR_Spatial Anchor (Script)` to a GameObject to let the SDK create an anchor based on that object's Transform and update the anchor pose.
- Wait until `anchor.Created` before using the anchor.
- Read `anchor.uuid` and `anchor.handle` after creation.
- Use `await anchor.PersistAsync()` and `await anchor.UnPersistAsync()` for persistence.
- Destroy the GameObject to destroy the anchor object in memory.
- Use `QuerySpatialAnchorObjectsAsync(Guid[] uuids = null, CancellationToken token = default)` to query GameObjects with `PXR_Spatial Anchor` components.

Example:

```csharp
IEnumerator CreateAnchorWithComponent()
{
    var anchorObject = new GameObject("SpatialAnchor");
    var anchor = anchorObject.AddComponent<PXR_SpatialAnchor>();

    yield return new WaitUntil(() => anchor.Created);

    Debug.Log($"uuid={anchor.uuid}, handle={anchor.handle}");
    _ = anchor.PersistAsync();
}
```

Some SDK versions also provide a `SpatialAnchor.prefab` under an Assets/Resources/Prefabs-style folder. It usually already includes the `PXR_SpatialAnchor` component. The developer can instantiate it and then use the component to persist, unpersist, or destroy the anchor.

## Query and locate behavior

- Only anchors created by the current app can be loaded.
- `QuerySpatialAnchorAsync` can only be called once at a time. Wait until the current query completes before starting the next one.
- If no UUIDs are passed, the query can return all available anchors for the current app.
- Use `GetAnchorUuid` to record UUIDs for later targeted loading.
- Use `LocateAnchor` to keep virtual content aligned with the anchor. A practical recommendation is about once per second; do not exceed once per frame.
- If `LocateAnchor` fails or an anchor cannot be found, guide the user back near the placement location and ask them to slowly look around the area.

## UX and environmental guidance

Good UX matters because anchor quality depends on user motion and environmental features:

- Prefer placing anchors within about 3 meters of the user's HMD.
- After placing an anchor, guide the user to look around and move around the anchor area slowly.
- The retrievable area depends on how much the user observed around placement. A practical upper radius is about 5 meters; anchors beyond that area may not be retrievable if the area was not mapped.
- Avoid relying on white walls, repetitive patterns, very dim light, very bright light, fast user motion, or highly dynamic scenes.
- Slow and steady movement improves tracking stability.
- If the user cannot retrieve a previous anchor, offer a flow to return to the placement location, recapture the space, or place the object again.

## Event for discovered anchors

Some SDK paths expose `OpenXRExtensions.SpatialAnchorDataUpdated`. Receiving the event means new spatial anchor data has been discovered. It does not necessarily mean old anchors have been removed when the user walks away.

```csharp
OpenXRExtensions.SpatialAnchorDataUpdated += OnSpatialAnchorDataUpdated;

private void OnSpatialAnchorDataUpdated()
{
    // Query, locate, persist, destroy, or update UI as needed.
}
```

## Shared Spatial Anchor flow

Use Shared Spatial Anchor only when multiple users need to align content in the same physical space.

### Requirements

- PICO 4 series or PICO 4 Ultra series.
- PICO OS 5.15.0 or later.
- Users must log in to their PICO devices.
- `XR Origin` and `PXR_Manager` are present.
- Video Seethrough is configured.
- App ID is configured.
- Platform Services are initialized.
- The app calls `GetLoggedInUser` or `GetAccessToken` to retrieve account information and trigger login if necessary.
- The app has a networking path to exchange UUIDs, such as PICO Room/Matchmaking/Networking services or a third-party networking framework.

### Flow

1. Enable `Shared Spatial Anchor` on `PXR_Manager`.
2. Create a local spatial anchor with `CreateSpatialAnchorAsync`.
3. Persist it locally with `PersistSpatialAnchorAsync`.
4. Upload it to PICO cloud with `UploadSpatialAnchorAsync(anchorHandle)` or `UploadSpatialAnchorWithProgressAsync(anchorHandle, progressUpdated)`.
5. Share the returned UUID through Room/Matchmaking/Networking or another multiplayer channel.
6. Other users download it with `DownloadSharedSpatialAnchorAsync(uuid)` or `DownloadSharedSpatialAnchorWithProgressAsync(uuid, progressUpdated)`.
7. Other users load it in the scene with `QuerySpatialAnchorAsync(new[] { uuid })`.
8. Locate it with `LocateAnchor` and align shared content to its pose.

### Shared anchor API summary

```csharp
async Task<(PxrResult result, Guid uuid)> UploadSpatialAnchorAsync(ulong anchorHandle);
public static async Task<(PxrResult result, Guid uuid)> UploadSpatialAnchorWithProgressAsync(
    ulong anchorHandle,
    Action<int> progressUpdated,
    CancellationToken token = default);

async Task<PxrResult> DownloadSharedSpatialAnchorAsync(Guid uuid);
public static async Task<PxrResult> DownloadSharedSpatialAnchorWithProgressAsync(
    Guid uuid,
    Action<int> progressUpdated,
    CancellationToken token = default);
```

### Shared anchor limitations

- After a shared anchor is downloaded, the receiving app can obtain pose data but cannot persist or unpersist that shared anchor.
- After a user uploads an anchor to PICO cloud, the user cannot actively unpersist the cloud copy.
- PICO automatically unpersists shared anchors that have been inactive for 7 days from the last active time.
- Unpersisting or deleting the local anchor after upload does not necessarily make existing cloud-shared anchors unusable for other users.

## Common pitfalls

- Trying to use Spatial Anchor in PICO Spatial mode for immersive MR behavior.
- Forgetting to configure Passthrough / Video Seethrough before anchor workflows.
- Creating anchors but not persisting them, then expecting them to survive app exit.
- Destroying an anchor before unpersisting it. Delete order should be `UnPersistSpatialAnchorAsync` first, then `DestroyAnchor`.
- Not storing UUIDs in app save data, making targeted reload difficult.
- Calling `QuerySpatialAnchorAsync` or `UnPersistSpatialAnchorAsync` concurrently.
- Calling `LocateAnchor` too rarely and letting visual objects drift, or too frequently without need.
- Testing in poor environments: blank walls, repetitive textures, poor lighting, dynamic objects, or fast motion.
- For shared anchors, forgetting login, App ID, Platform Services initialization, or UUID exchange between users.
