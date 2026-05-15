# PICO Platform Services Guide

This guide is self-contained. Use it for Platform Services, initialization, entitlement, accounts, IAP, subscription, leaderboards, achievements, rooms/matchmaking, RTC, and cloud storage.

## Core rules

- Platform Services support PICO XR mode, Unity OpenXR mode, and PICO Spatial mode in Full Space / Shared Space.
- Platform Services require a 64-bit app. Use IL2CPP and ARM64; do not ship ARMv7-only builds.
- Configure App ID and services in the PICO Developer Platform before relying on runtime APIs.
- Do not embed App Secret in the Unity client. Keep secrets on your backend.
- Initialize Platform Services successfully before calling service APIs.
- For sensitive operations, prefer authoritative backend validation/fulfillment.
- Handle `IsError`, `Error.Code`, and `Error.Message` for every API call.

## Project setup checklist

1. Create app in PICO Developer Platform.
2. Configure app package name, signing, App ID, and required services.
3. Import PICO Unity SDK and choose development mode.
4. Use SDK Portal / Project Validation and fix required issues.
5. Android settings: IL2CPP, ARM64, suitable min/target API, correct package name/signing.
6. Configure service-specific backend entries: IAP SKUs, leaderboards, achievements, matchmaking pools, RTC enablement, cloud storage enablement, etc.

## Initialization

### Async initialization pattern

```csharp
CoreService.AsyncInitialize().OnComplete(m =>
{
    if (m.IsError)
    {
        Debug.Log($"Platform init failed: code={m.GetError().Code} message={m.GetError().Message}");
        return;
    }

    if (m.Data != PlatformInitializeResult.Success &&
        m.Data != PlatformInitializeResult.AlreadyInitialized)
    {
        Debug.Log($"Platform init result={m.Data}");
        return;
    }

    Debug.Log("Platform Services ready");
    // Safe to call platform APIs here.
});
```

### Game module initialization

Game-related services such as Room, Matchmaking, Leaderboard, Achievement, and Challenge can require game module initialization after global platform initialization:

```csharp
CoreService.GameInitialize(accessToken).OnComplete(msg =>
{
    if (msg.IsError)
    {
        Debug.Log($"GameInitialize failed: {msg.Error.Code} {msg.Error.Message}");
        return;
    }

    Debug.Log($"GameInitialize result={msg.Data}");
});
```

## Callback and async/await patterns

Most APIs use `OnComplete`:

```csharp
SomeService.SomeCall().OnComplete(msg =>
{
    if (msg.IsError)
    {
        Debug.Log($"Error: {msg.Error.Code} {msg.Error.Message}");
        return;
    }
    var data = msg.Data;
});
```

SDK 2.1.4+ supports async/await-style calls through `.Async()`:

```csharp
var userMessage = await UserService.GetLoggedInUser().Async();
if (userMessage.IsError)
{
    Debug.Log($"GetLoggedInUser failed: {userMessage.Error.Code} {userMessage.Error.Message}");
    return;
}
```

## Entitlement Check

Entitlement Check verifies whether the user legitimately owns or can access the app.

```csharp
UserService.EntitlementCheck(killApp).OnComplete(msg =>
{
    if (msg.IsError)
    {
        Debug.Log($"EntitlementCheck error: {msg.Error.Code} {msg.Error.Message}");
        return;
    }

    Debug.Log($"HasEntitlement={msg.Data.HasEntitlement}, status={msg.Data.StatusMessage}");
});
```

- `killApp=true`: system can show a failure popup and quit the app.
- `killApp=false`: app handles failure manually.
- Paid apps should enable entitlement checks; free apps should consider it too.
- Unpublished/test behavior can differ from published app behavior; do not treat local test success as release proof.
- User verification is not a replacement for entitlement checks.

## Accounts & Friends

Important concepts:

- OpenID: unique user identifier.
- Access Token: generated from PICO account and App ID.
- Organization ID: user ID scoped to apps from the same organization.
- ID Token: OIDC token for identity integrations.

Request permissions before accessing user/friend data:

```csharp
UserService.RequestUserPermissions(new[] { Permissions.UserInfo, Permissions.FriendRelation })
    .OnComplete(msg =>
    {
        if (msg.IsError) return;
        Debug.Log(string.Join(",", msg.Data.AuthorizedPermissions));
    });
```

Typical identity flow:

1. Initialize Platform Services.
2. Call `UserService.GetLoggedInUser()`.
3. Call `UserService.GetAccessToken()`.
4. Send user ID/OpenID + access token to your backend.
5. Backend verifies user with PICO server-side API.

Friend list caveat: users and friends may need to have used the same app and authorized friend-list access.

## IAP and Subscription

### IAP concepts

- SKU: unique add-on identifier.
- Durable add-on: permanent after purchase.
- Consumable: must be fulfilled and consumed before repurchase.
- Consume: records that a consumable was fulfilled.

### IAP flow

1. Enable/configure IAP and add-ons in Developer Platform.
2. Initialize Platform Services.
3. Query products:
   ```csharp
   IAPService.GetProductsBySKU(skus);
   ```
4. Launch checkout:
   ```csharp
   IAPService.LaunchCheckoutFlow2(product);
   ```
5. Query owned purchases:
   ```csharp
   IAPService.GetViewerPurchases();
   ```
6. Fulfill on backend/account system.
7. For consumables, call:
   ```csharp
   IAPService.ConsumePurchase(sku);
   ```

### IAP pitfalls

- Do not hardcode currency; PICO can localize prices based on region.
- Real payment methods may be required for testing.
- Developer accounts and normal accounts can have different add-on testing rules depending on add-on review state.
- For Mainland China games, IAP availability can depend on license eligibility.
- Put fulfillment logic on backend for paid currency/items where possible.

### Subscription notes

- Subscriptions are part of IAP and use SKU/OuterID concepts.
- Common periods include 1 month, 3 months, and 1 year.
- Query subscription products with `GetProductsBySKU`, launch purchase with `LaunchCheckoutFlow2`, and query purchases/status with `GetViewerPurchases` / subscription status APIs.
- Subscription add-on edit/removal rules can be strict after review/approval.

## Leaderboard

Setup:

1. Create leaderboard in Developer Platform.
2. Configure API name, sorting order, sorting field, write permission, friend leaderboard, and notifications.
3. Enable related matchmaking/service requirements where applicable.
4. Initialize Platform Services and game module.

Client APIs commonly include:

- `LeaderboardService.Get`
- `LeaderboardService.GetEntries`
- `LeaderboardService.GetEntriesAfterRank`
- `LeaderboardService.GetEntriesByIds`
- `LeaderboardService.WriteEntry`
- `LeaderboardService.WriteEntryWithSupplementaryMetric`

Pitfalls:

- Leaderboard may not be testable in Unity Editor.
- Decide early whether writes are client-authoritative or server-authoritative.
- API names in code must match Developer Platform configuration.
- Region can affect leaderboard lookup and server domain choice.

## Achievement

Setup:

1. Create achievements in Developer Platform.
2. Configure display names, descriptions, unlocked descriptions, API names, type, write permission, secret/hidden status, notifications, icons, and localization.
3. Initialize Platform Services and, where required, game module.

Achievement types:

- Simple
- Count
- Bitfield

Common APIs:

- `AchievementsService.GetDefinitionsByName`
- `AchievementsService.GetAllDefinitions`
- `AchievementsService.GetProgressByName`
- `AchievementsService.GetAllProgress`
- `AchievementsService.AddCount`
- `AchievementsService.AddFields`
- `AchievementsService.Unlock`

Pitfalls:

- Achievement may not be testable in Unity Editor.
- Decide client-authoritative vs server-authoritative progress updates early.

## Room & Matchmaking

Room & Matchmaking supports room management, matchmaking, networking, and messaging.

Concepts:

- Matchmaking Pool
- Room
- Room Lock
- Private room
- Named room
- Moderated room
- Matchmaking room

Setup:

1. Enable Matchmaking service in Developer Platform.
2. Create matchmaking pool.
3. Configure min/recommended/max users, room creation rules, unmatched users, reservations, cooldowns, custom data, and queries.
4. Initialize Platform Services and game module.
5. Register network callbacks.

Network event handling:

```csharp
NetworkService.SetNotification_Game_ConnectionEventCallback(OnGameConnectionEvent);
```

Handle events such as `Connected`, `Closed`, `GameLogicError`, `Lost`, `Resumed`, `KickedByRelogin`, and `KickedByGameServer`.

Pitfalls:

- On `Lost`, stop sending game requests.
- On `Resumed`, notify user and refresh state.
- Backgrounding can stop message polling and cause missed heartbeats or lost messages.

## RTC

RTC provides real-time voice chat.

Setup essentials:

- Enable RTC in Developer Platform.
- Add Android permissions such as `INTERNET`, `RECORD_AUDIO`, `MODIFY_AUDIO_SETTINGS`, `ACCESS_NETWORK_STATE`, and other required permissions depending on SDK path.
- Initialize Platform Services first, then initialize RTC engine.

```csharp
var res = RtcService.InitRtcEngine();
if (res != RtcEngineInitResult.Success)
{
    throw new UnityException($"Init RTC Engine Failed: {res}");
}
RtcService.EnableAudioPropertiesReport(2000);
```

Join flow:

1. Validate room ID and user ID.
2. Call `RtcService.GetToken(roomId, userId, ttl, privilege)`.
3. Call `RtcService.JoinRoom(...)`.
4. Register join/leave/publish/unpublish callbacks.
5. Publish/subscribe audio streams.

Pitfalls:

- Token expiration must be handled and renewed.
- A user can publish local audio to only one room at a time.
- Clean up rooms/resources when users leave.
- Custom messages and stream sync info have size limits.

## Cloud Storage

Cloud Storage backs up simple app data such as identities, settings, preferences, and progress.

Behavior:

- Recovery can occur when using a new device, resetting a device, or reinstalling an app.
- Recovery is asynchronous at app launch.
- Users may see recovery progress popups.

Backup paths commonly include app files, databases, shared preferences, and app external files under Android app-specific directories.

Backup modes:

- Active backup with `CloudStorageService.StartNewBackup()`.
- Passive backup after conditions such as elapsed time, changed data, and app exit.

Pitfalls:

- Backup size limit is about 100 MiB per app per user.
- Only the latest cloud backup is stored.
- Multiple devices can overwrite each other's latest backup.
- Do not back up DLC or large generated assets.
- Network is required for backup/recovery.

## Account Linking / SSO

Account Linking connects a user's PICO account to the developer's own account system. Use it when the app has its own backend identity and wants PICO login as an authorization source.

Core concepts:

- SSO redirect domain: the developer-owned HTTPS domain registered in the PICO Developer Platform.
- Authorization code: returned to the redirect URI after the user authorizes through the PICO login page.
- Access Token: used to retrieve PICO account information; treat as sensitive and time-limited.
- Refresh Token: used to refresh expired access tokens; treat as sensitive and keep server-side.

Recommended architecture:

1. Register region-specific SSO redirect domains in the Developer Platform.
2. In the app or web UI, direct the user to the PICO authorization URL with `client_key` and `redirect_uri`.
3. Receive the authorization code on the developer backend via HTTPS redirect.
4. Exchange the authorization code for access/refresh tokens on the backend, not inside the Unity client.
5. Call the userinfo endpoint from the backend to retrieve nickname, user ID, and avatar.
6. Link the PICO identity to the developer account and return an app session token to Unity.

Security rule: never ship the app secret or long-lived refresh token in the Unity client.

## Challenges, Highlights, Exercise, and Profanity Detection

These services are less common than Entitlement/IAP/Leaderboard, but the skill should recognize them.

### Challenges

- Challenges are competition activities tied to leaderboard-style scores.
- Common operations include get challenge, list challenges, join, leave, invite friends, and query challenge entries.
- Confirm visibility/public-private behavior, leaderboard relationship, and test-user setup before debugging code.

### Highlights

- Highlights records and shares screenshots or videos of important user moments.
- It requires Platform Services initialization, user permission request, service enablement in Developer Platform, and Unity Platform Settings enablement.
- Typical APIs: `HighlightService.StartSession`, `CaptureScreen`, `StartRecord`, `StopRecord`, `ListMedia`, `SaveMedia`, `ShareMedia`, and `SetOnRecordStopHandler`.
- It has store/region/service constraints; for detailed capture workflow use `composition-layers-and-media.md`.

### Exercise data authorization

- Use when the app needs authorized user sport/exercise data.
- Typical service family: `SportService`, with calls such as user info, summary, and daily summary queries.
- Treat exercise data as sensitive user data and require explicit authorization.

### Profanity detection

- Use for moderation/compliance workflows where available.
- It can involve `ComplianceService` and/or server-side sensitive-word detection.
- Check regional availability; do not assume it is globally available.

## Cross-service release checklist

- IL2CPP + ARM64.
- Correct package name and signing.
- App ID matches Developer Platform.
- Do not ship App Secret in client.
- Initialize before API calls.
- Handle all errors and network failures.
- Paid apps use Entitlement Check.
- Backend validates purchases and user identity where needed.
- Test with real PICO accounts and device builds, not only Unity Editor.
