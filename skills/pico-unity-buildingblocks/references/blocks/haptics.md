# Controller haptics

## Tool

`pico_xr_haptics` — actions: `attach` / `upsert_effect` / `remove_effect` /
`remove` / `status`

## Scope

This block attaches one `PXR_MCP_HapticsManager` to the existing agent XR
Origin and manages reusable named effects. It does not decide when vibration happens.
Gameplay code or any compatible UnityEvent owns that decision.
The supported source family is AudioClip/PCM/PHF plus impulse.

The manager uses only current PICO-native APIs:

```csharp
PXR_Input.SendHapticImpulse(...);
PXR_Input.SendHapticBuffer(...); // AudioClip, PCM, or PHF overload
PXR_Input.StartHapticBuffer(sourceId);
PXR_Input.PauseHapticBuffer(sourceId);
PXR_Input.ResumeHapticBuffer(sourceId);
PXR_Input.UpdateHapticBuffer(sourceId, vibrateType, channelFlip, amplitudeScale);
PXR_Input.StopHapticBuffer(sourceId, clearCache);
```

Do not substitute deprecated `StartVibrateBy*` methods, old Haptic Stream APIs,
`PXR_Plugin` internals, or Unity XR/OpenXR haptics. The separate
`PXR_HapticParametric` API is not part of this basic haptics block.

## Architecture

- One manager is attached directly to `[PICO_MCP] XR Origin (XR Rig)`.
- Haptics does not create an XR Origin. If no agent XR Origin exists, stop and
  ask the user to create/enable one through the normal building-block flow.
- Controller GameObjects are not required. PICO's `VibrateType` selects the
  physical left/right controller directly.
- One manager contains multiple named effects. Do not create one component per
  effect or per controller.
- A named effect has one effect type and may target `left`, `right`, or `both`.
  `both` has independent left/right settings, assets, and runtime source IDs.
- If the two hands require different effect types, create two named effects.

## Parameters

Common parameters:

| Parameter    | Values                                       | Default                         |
| ------------ | -------------------------------------------- | ------------------------------- |
| `effectName` | non-empty string                             | `Default`                       |
| `effectType` | `impulse`, `audio_clip_buffer`, `phf_buffer` | `impulse`                       |
| `controller` | `left`, `right`, `both`                      | `both`                          |
| `setDefault` | boolean                                      | attach: `true`; upsert: `false` |

Impulse parameters:

| Parameter     | Range         | Default |
| ------------- | ------------- | ------- |
| `amplitude`   | `0..1`        | `0.5`   |
| `durationMs`  | `0..65535` ms | `100`   |
| `frequencyHz` | `50..500` Hz  | `150`   |

Use `leftAmplitude` / `rightAmplitude`, `leftDurationMs` / `rightDurationMs`,
and `leftFrequencyHz` / `rightFrequencyHz` to override the shared fallback per
hand.

Buffer parameters:

| Parameter        | Values / range                                        | Default                |
| ---------------- | ----------------------------------------------------- | ---------------------- |
| `audioClipPath`  | Unity project path to an `AudioClip`                  | required for AudioClip |
| `phfTextPath`    | Unity project path to a PHF JSON `TextAsset`          | required for PHF       |
| `channelFlip`    | `no`, `yes`                                           | `no`                   |
| `cacheType`      | `dont_cache`, `cache_and_vibrate`, `cache_no_vibrate` | `dont_cache`           |
| `amplitudeScale` | `0..2`                                                | `1`                    |

Every shared buffer field also has a `left*` and `right*` override. PHF uses
`amplitudeScale` when it is sent. AudioClip uses `UpdateHapticBuffer` after
source creation when scale is not `1`. Invalid values and missing/wrong asset
paths are errors; never silently clamp or guess paths.

PCM is intentionally code-only because raw `float[]` PCM is unsuitable for the
Inspector/MCP JSON contract. Business code calls `SendPcm(...)`; the manager
then owns its source IDs under the supplied runtime effect name.

## Actions

### Attach

```text
pico_xr_haptics(action=attach, effectName=Hit, effectType=impulse,
                controller=both, leftAmplitude=0.4, rightAmplitude=0.8,
                durationMs=80, frequencyHz=180)
```

Creates the manager on the existing agent XR Origin and upserts the first named
effect. Repeating the same call is idempotent. It does not bind a business event.

### Upsert effect

```text
pico_xr_haptics(action=upsert_effect, effectName=Engine,
                effectType=audio_clip_buffer, controller=both,
                leftAudioClipPath=Assets/Haptics/left.wav,
                rightAudioClipPath=Assets/Haptics/right.wav,
                cacheType=cache_no_vibrate, amplitudeScale=1.2)
```

Adds or replaces one named effect while retaining the other effects and their
Inspector callbacks. The manager must already exist.

### Remove effect / remove / status

- `remove_effect` removes only the named effect.
- `remove` removes only an MCP-managed manager and leaves the XR Origin intact.
- `status` reports the manager path, ownership, default effect, and all serialized
  effect settings. It is configuration evidence, not proof of device vibration.

Cleanup remains available if the project has since switched runtime.

## Runtime entry points and callbacks

UnityEvent-friendly public methods include:

```csharp
manager.Send();                         // default effect
manager.Send("Hit");                  // named effect
manager.SendImpulse(0.8f);              // default impulse with amplitude override
manager.StartEffect();                  // cached default effect
manager.StartEffect("Engine");
manager.Pause("Engine");
manager.Resume("Engine");
manager.UpdateEffect("Engine");
manager.UpdateAmplitude(1.5f);          // default buffered effect
manager.Stop("Engine");
manager.StopAndClear("Engine");
manager.StopAll();
```

The parameterless cached-start method is named `StartEffect()` rather than
`Start()` so Unity does not invoke it automatically as a MonoBehaviour lifecycle
message. Likewise, use `UpdateEffect()` for the default effect; the overloads
with a string argument target a named effect.

Business code that needs a success value uses `TrySend`, `TrySendImpulse`,
`TryStart`, `TryPause`, `TryResume`, `TryUpdate`, `TryUpdateAmplitude`,
`TryStop`, or `TryStopAll`.

The Inspector exposes serialized callbacks with `(effectName, targetOrDetail)`:

- `OnRequested`, `OnSent`, `OnSourceCreated`, `OnStarted`
- `OnPaused`, `OnResumed`, `OnUpdated`, `OnStopped`, `OnFailed`

The SDK exposes no reliable playback-completion callback, so do not claim or
synthesize `OnCompleted`. Shooting, collision, damage, UI, animation, timeline,
and custom events are valid callers but are examples, never a trigger allowlist.
Wire a trigger only when the user names the business behavior.

## Workflow

```text
pico_xr_status()
  -> runtime must be native
  -> agent XR Origin must already exist
pico_xr_haptics(action=attach/upsert_effect, ...)
pico_xr_haptics(action=status)
Save Scene when the manager or effects changed
Report that physical behavior still requires a connected PICO-device test
```

No package import and no domain-reload settle loop are expected.
