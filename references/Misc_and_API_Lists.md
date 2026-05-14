# Miscellaneous and API Lists

## Table of Contents
- About the PXR Manager
- Account linking
- Accounts & Friends
- API list(2)
- API list(3)
- API list
- AR Foundation
- Build review-related FAQs
- Camera image data (for enterprise device)
- Camera image data (user device)
- Capture, record, and cast screen
- Challenges
- Cloud storage
- Compatibility & porting guide for MR features
- Content Protection
- Convert and profile models for SecureMR
- Create a QNN model to run algorithms
- Create example hand poses
- Create immersive scenes
- Demo(2)
- Demo(3)
- Demo
- DLC
- Does the PICO Unity Integration SDK support desktop app development_
- Download development resources
- Download the streaming service
- Enhance image quality
- Enterprise services
- Entitlement check
- Ergonomics & device limitations
- Exercise data authorization
- Highlights
- How can I test my apps on PICO Neo 3 for PICO Neo 3 Link_
- Implement the Leaderboard service
- Implement the social intraction experience
- Improve microphone-related designs
- In-app purchase (IAP)
- Integrate the Achievement service
- Manage files
- Metadata review-related FAQs
- Modify the eye buffer resolution
- Motion tracking API compatibility information
- Object Tracking
- Parameter details
- Performance metrics
- PICO Building Blocks
- PICO XR Portal
- Pipeline synchronization
- Plane detection
- Play HDR videos
- Preview scenes in real time
- Profanity detection
- Push URLs to a PICO device
- Room & Matchmaking
- RTC
- Scene Capture
- Screen Fade
- SecureMR Privacy Notice
- SecureMR samples
- SecureMR use cases
- Service design(2)
- Service design
- Set up a camera for each eye and display content in two cameras separately
- Settlement-related questions
- Spatial data permission control
- SpatialMLCapture Terms of Service
- SpatialMLCapture
- Speech-to-text
- Splash Screen
- Subscription
- Support for the Unity OpenXR Plugin
- System Keyboard
- The number of APK files associated with a key exceeds the limit
- The SpatialMP4 Whitepaper
- Tips on dealing with semitransparent objects
- Tracking Origin
- Use cases & code samples(2)
- Use cases & code samples(3)
- Use cases & code samples
- Use different operators
- Use the dynamic texture
- Use the hand interactables of the XR Interaction toolkit
- Use the Readback tensor
- Where can I download an older version of the SDK_
- Where can I get the SDK demo_

---



# --- BEGIN: About the PXR Manager.md ---

PXR Manager is a crucial part of the PICO Unity Integration SDK. You must have it on and enabled in every scene, including the loading screen.
## UI
Below is the UI of the PXR_Manager script.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71d06ff231454df080cdf392f2b16d0e~tplv-goo7wpa0wc-image.image)
## What you can do with it
You can use the PXR_Manager script to manage many SDK features.
| **Feature** | **Description** |
| --- | --- |
| [Home button recentering](/en_app-recenter-failure) | Long press the Home button to recenter. |
| [Screen fade](/en_screen-fade) | After checking the **Open Screen Fade** checkbox, the PXR Manager will add the PXR_ScreenFade script to the GameObject to help realize the fade-in and fade-out effect during scene transitions. |
| [Eye tracked foveated rendering](/en_eye-tracked-foveated-rendering) | Eye tracked foveated rendering (ETFR) renders the image at full resolution in the area of the eye's gaze point, while rendering the peripheral area at a lower resolution.  |
| [Fixed foveated rendering](/en_fixed-foveated-rendering) | Fixed foveated rendering (FFR) fixes the gaze point in the center of view, and the resolution decreases from the center to the peripheral area. |
| [Eye tracking](/en_eye-tracking) | Eye tracking converts users' eye movements into input data. |
| [Face tracking](/en_face-tracking) | Face tracking **** enables users' facial expressions as input data. |
| [Hand tracking](/en_hand-tracking-overview) | Hand tracking **** converts users' hand poses into input data. |
| [Body tracking](/en_body-tracking) | Body tracking collects users' body position information and converts it into reproducible pose data. |
| [Content protection](/en_content-protection) | After checking the **Use Content Protect** checkbox, the screen becomes black when users are trying to make screenshots or record videos in your app |
| [Mixed reality capture](/en_mixed-reality-capture) | Enable **MRC** to empower the creation of mixed reality videos. |
| [Late latching](/en_late-latching) | Late latching reduces 1 frame of latency in HMD and controller poses. |
| [Anti-aliasing](/en_anti-aliasing) | Check the **Use Recommended MSAA** checkbox to enable the default MSAA level which is "4x" for the scene. |
| [Adaptive resolution](/en_adaptive-resolution) | Adaptive resolution automatically adjusts the screen resolution based on GPU workload.  |
| [Video seethrough](/en_seethrough) | Video seethough enables the physical environment to become a scene's background image upon which the virtual objects are overlayed. |
| [Spatial anchors](/en_spatial-anchors) | Spatial anchors enable the alignment of positions between a virtual environment and the real world. It is used to anchor virtual objects to locations or objects in the physical world. |


# --- END: About the PXR Manager.md ---



# --- BEGIN: Account linking.md ---

Account linking links users' PICO accounts to your self-established account system. You can retrieve users' PICO account information such as the nickname, user ID, and profile photo, allowing them to log in to your app using their PICO accounts.
## Basic concepts
| **Name** | **Description** |
| --- | --- |
| SSO | Single Sign-On (SSO) is an identity authentication solution that allows users to log in to multiple apps using a single set of credentials, such as a username and password, without the need to enter the credentials separately for each app. |
| SSO redirect domain name | You own login service. |
| Access Token | Access tokens are used to retrieve users' PICO account information and are valid for 15 days. |
| Refresh Token | Refresh tokens are used to update expired access tokens and are valid for 30 days. |
## Procedure
### Step 1: Create an SSO redirect domain name
You can create a Chinese Mainland domain name and an Outside Chinese Mainland domain name for an app, and these two domain names are mutually independent. You can create one or two SSO redirect domain names based on the region where your app is available.

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/).
2. Click the card of an app to enter its overview screen.
3. From the left navigation panel, select **Platform Services** > **SSO**.
   This directs you to the **SSO** screen.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90db3dc7319f4b1594e3ce405c6ed652~tplv-goo7wpa0wc-image.image)
4. Select **Chinese Mainland** and/or **Outside Chinese Mainland** according to the region where your app is available.
5. Click the **Edit** button.
6. Fill in the SSO redirect domain name.
   * The URL should start with https://.
   * The length of the domain name should not exceed 500 characters.
   * When entering a complete URL, only the domain name will be saved.

   Below are two examples:
   ```Plain Text
   https://platform-cn.picovr.com
   https://platform-cn.picovr.com/open/v1/authorize/login
   ```

7. Click the **Save** button.

### Step 2: Create a UI that redirects users to PICO
You need to provide a button or link that redirects users to PICO's login authorization screen.
Below is the format of the URL of the authorization screen:
```Plain Text
https://$pico_auth_domain/oauth/authorize?client_key=$app_id&redirect_uri=$developer_code_receive_url
```

The URL consists of three parameters. Below are descriptions: 
| **Parameter** | **Description** |
| --- | --- |
| pico_auth_domain | PICO-provided domain names for third-party authorization screens: <br>  <br> * Chinese Mainland: openid.picovr.com <br> * Outside Chinese Mainland: open-global.picoxr.com |
| client_key | The app's ID, which is provided on the PICO Developer Platform. For how to view an app's ID, refer to [this article](/document/distribute/create-an-app/). |
| redirect_uri | After users authorize their PICO accounts for you, you need to redirect users to your own login service. The redirection carries an authorization code of PICO account. The redirection address must support https, and its domain name must be the same as the SSO redirect domain name you create on the PICO Developer Platform. |
Below is an example URL:
```Plain Text
https://openid.picovr.com/oauth/authorize?client_key=xxxxf0c4aafa504fc1ae8386113c8421&redirect_uri=https://platform-cn.picovr.com/open/v1/authorize/login
```

Below is the PICO login authorization screen:
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa0620b02e9a425581812b622bb025fd~tplv-goo7wpa0wc-image.image)
### Step 3: Retrieve the authorization code of PICO account
After a user logs in to the PICO login authorization screen, the user will be redirected to the address specified in the `redirect_uri` parameter through HTTP 302, and the redirection carries an authorization code of PICO account. You need to retrieve the authorization code, which you can later use to retrieve the access token for accessing the information of the user's PICO account.
Below is an example redirection URL:
```Plain Text
https://platform-cn.picovr.com/open/v1/authorize/login?code=xxxx4530340d3292bccctu0Mu5NGYWmXcyux&scopes=user_info
```

### Step 4: Retrieve the access token for accessing a user's PICO account info
After retrieving the authorization code, you can use it to retrieve the access token from PICO's server. 
Below are the details of the API:
|  | **Format** | **Description** |
| --- | --- | --- |
| **API Address** | https://$pico_auth_domain/passport/open/access_token/ <br>  | PICO-provided domain names for third-party authorization screens: <br>  <br> * Chinese Mainland: openid.picovr.com <br> * Outside Chinese Mainland: open-global.picoxr.com |
| **Method** | POST | - |
| **Content-Type** | application/x-www-form-urlencoded | - |
| **Body** <br>  | client_key=$app_id&client_secret=$app_secret&code=$code&grant_type=authorization_code | * `client_key`: The app's ID, which is provided on the PICO Developer Platform. <br> * `client_secret`: The app's secret, which is provided on the PICO Developer Platform. <br> * `code`: The authorization code, which is returned in step 3. <br>  <br> ***Note***: For how to view an app's ID and secret, refer to [this article](/document/distribute/create-an-app/). |
Example request:
```JSON
curl -X POST "https://openid.picovr.com/passport/open/access_token/" -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" -d "client_key=xxxxf0c4aafa504fc1ae8386113c8421&client_secret=ec850766400cc0a383332f85faac01d4&code=xxxx4530340d3292bccctu0Mu5NGYWmXcyux&grant_type=authorization_code" -v
```

Example response:
```JSON
{
    "data":{
        "access_token":"act.xxxx2fa0b41f9b0f49cfdf0e1a5a4e08UQe5FTYFgGEcAeMdlCzEhzp26Udf",
        "captcha":"",
        "desc_url":"",
        "description":"",
        "error_code":0,
        "expires_in":5184000,
        "log_id":"xxxx08251052489473587D0F4BF26D3378",
        "open_id":"xxxx842695713621048",
        "refresh_expires_in":15552000,
        "refresh_token":"rft.xxxxf2d0570e3b1762248d6c41a6300fUVTiu8GCnZkVMUSvIRQB4uNjedKt",
        "scope":"user_info"
    },
    "message":"success"
}
```

### Step 5: Retrieve a user's PICO account info using the access token
After getting the access token, you can use it to retrieve a user's PICO account information.
Below are the details of the API:
|  | **Format** | **Description** |
| --- | --- | --- |
| **API Address** | https://$pico_auth_domain/passport/open/userinfo/ <br>  | PICO-provided domain names for third-party authorization screens: <br>  <br> * Chinese Mainland: openid.picovr.com <br> * Outside Chinese Mainland: open-global.picoxr.com |
| **Method** | POST | - |
| **Content-Type** | application/x-www-form-urlencoded | - |
| **Body** <br>  | open_id=$open_id&access_token=$access_token | * `open_id`: The user ID returned in step 4. <br> * `access_token`: The access token returned in step 4. |
Example request:
```JSON
curl -X POST "https://openid.picovr.com/passport/open/userinfo/" -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" -d "open_id=7241842695713621048&access_token=act.e5612fa0b41f9b0f49cfdf0e1a5a4e08UQe5FTYFgGEcAeMdlCzEhzp26Udf" -v
```

Example response:
```JSON
{
    "data":{
        "avatar":"https://p26-passport.byteacctimg.com/img/user-avatar/80f4ec6a25460f15d906392a7a9d1e05~300x300.image",
        "captcha":"",
        "client_key":"xxxxf0c4aafa504fc1ae8386113c8421",
        "desc_url":"",
        "description":"",
        "error_code":0,
        "log_id":"xxxx08251054456497265C287F8671A9F1",
        "nickname":"PICO",
        "open_id":"xxxx842695713621048"
    },
    "message":"success"
}
```

### Step 6: Use the refresh token to update the access token
Once the access token expires, you can use the refresh token to update it.
Below are the details of the API:
|  | **Format** | **Description** |
| --- | --- | --- |
| **API Address** | https://$pico_auth_domain/passport/open/refresh_token/ <br>  | PICO-provided domain names for third-party authorization screens: <br>  <br> * Chinese Mainland: openid.picovr.com <br> * Outside Chinese Mainland: open-global.picoxr.com |
| **Method** | POST | - |
| **Content-Type** | application/x-www-form-urlencoded | - |
| **Body** <br>  | client_key=$app_id&grant_type=refresh_token&refresh_token=$refresh_token | * `client_key`: The app's ID, which is provided on the PICO Developer Platform. For how to view an app's ID, refer to [this article](/document/distribute/create-an-app/). <br> * `refresh_token`: The refresh token returned in step 4. |
Example request:
```JSON
curl -X POST "https://openid.picovr.com/passport/open/refresh_token/" -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" -d "client_key=xxxxf0c4aafa504fc1ae8386113c8421&grant_type=refresh_token&refresh_token=rft.xxxxf2d0570e3b1762248d6c41a6300fUVTiu8GCnZkVMUSvIRQB4uNjedKt" -v
```

Example response:
```JSON
{
    "data":{
        "access_token":"act.xxxx2fa0b41f9b0f49cfdf0e1a5a4e08UQe5FTYFgGEcAeMdlCzEhzp26Udf",
        "captcha":"",
        "desc_url":"",
        "description":"",
        "error_code":0,
        "expires_in":5184000,
        "log_id":"xxxx08251056423F8EBE0681AEC16184C9",
        "open_id":"xxxx842695713621048",
        "refresh_expires_in":15551766,
        "refresh_token":"rft.xxxxf2d0570e3b1762248d6c41a6300fUVTiu8GCnZkVMUSvIRQB4uNjedKt",
        "scope":"user_info"
    },
    "message":"success"
}
```


# --- END: Account linking.md ---



# --- BEGIN: Accounts & Friends.md ---

"Account & Friend" service enables you to access the information of a specified user, get the friends list of the currently logged-in users, and enables your app's users to enjoy a social experience, such as sending friend requests.
## Basic concepts
| **Name** | **Description** |
| --- | --- |
| PICO account | An account that you can use for logging in to the [PICO official website](https://www.picoxr.com/uk/?utm_source=Search&utm_channel=Google&utm_campaign=brand&gclid=CjwKCAjw-IWkBhBTEiwA2exyO5fqxYRUYXml0IlXwBnYek5BzxYCELbbtNuzi84PmdorYsujxMXD8BoCpmoQAvD_BwE), PICO VR headsets, and the PICO VR app.  |
| OpenID | A user's unique identifier that is generated from their PICO accounts. The OpenID of each user is unique and fixed within different apps |
| Access Token | A token generated from the PICO account and app ID. Users with verified tokens can access PICO's platform services. |
| ID Token | A user's identity credentials for login with OIDC. |
| Organization ID | A user has one unique ID within the apps created by one organization. |
## Use the "Account & Friend" service
### Step 1: Complete general setups
Refer to the "[Platform services overview](/en_platform-services-overview#712343ad)" article to complete general setups, including registering on the PICO Developer Platform, importing the SDK, completing project settings in the Unity Editor, initializing platform services, and more.
### Step 2: Call UserService APIs
Call [UserService APIs](/reference/unity/latest/UserService/) to integrate the "Account & Friend" service into your app. Refer to the "Use cases" section for detailed introductions and code samples.
## Use cases
### Request user permissions
**Account login**
Users can log in to your app using their PICO accounts, so you don't need to customize signup and signin logics for your app. If a user is not logged into their PICO account, they will be prompted to do so when they first open the app. An app can be authorized with account login permission only after you [upload builds](/en_upload-a-build) for it on the PICO Developer Platform.
The system verifies your signature while performing account authorization. You must keep your signature safe and all updates to your app must be signed using the same certificate. You can refer to [this article](/en_sign-your-app) to learn more about app signing.
**User information**
Certain platform service APIs require user authorization before they can be executed. For instance, in order to retrieve a user's personal information using `UserService.GetLoggedInUser()`, the user must first authorize the app to access their profile information. Similarly, in order to obtain a user's friend list using `UserService.GetFriends()`, the user must first grant the app access to their friend information. Once the user has completed the authorization process, subsequent calls to the same API will no longer trigger an authorization pop-up. 
To improve user experience, it is advisable to avoid frequent pop-ups when the user is using your app. As such, the SDK offers the `UserService.RequestUserPermissions()` API, which allows you to apply for permissions from the user in a batch. It is recommended to apply for all the permissions you require after app initialization and proceed with further operations only after all the necessary permissions have been granted.
| **Permission Type** | **Description** |
| --- | --- |
| UserInfo | The permission to get the user's registration information, including the user's nickname, gender, profile photo, and more. |
| FriendRelation | The permission to get users' friend relations. |
| SportsUserInfo | The permission to get the user's information, including the user's gender, birthday, stature, weight, and more, on the PICO Fitness app. |
| SportsSummaryData | The permission to get users' exercise data from the PICO Fitness app. |
| RecordHighlight | The permission to capture or record the screen, which is required when using the highlight service. |
```C#
UserService.RequestUserPermissions(new[] {Permissions.UserInfo, Permissions.FriendRelation}).OnComplete(m => 
{ 
    if (m.IsError) 
    { 
        Log($"Permission failed code={m.Error.Code} message={m.Error.Message}"); 
        return; 
    } 
    // View the authorized permissions here 
    Log($"RequestUserPermissions successfully:{String.Join(",", m.Data.AuthorizedPermissions)}"); 
    getUser(); 
}); 
```

### Verify a user
You can verify a user's identity by checking the user's openID and access token, thereby ensuring that the current user is allowed to access your app using the PICO account provided by the client.
User verification cannot replace user entitlement check.

Below is the flow of user verification:

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI4NDVweCIgaGVpZ2h0PSI0MDdweCIgdmlld0JveD0iLTAuNSAtMC41IDg0NSA0MDciPjxkZWZzLz48Zz48cmVjdCB4PSIyMzIiIHk9IjIiIHdpZHRoPSIxNjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMzMzM2ZmIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDIzM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5QSUNPIFBsYXRmb3JtIFNlcnZpY2VzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NDIiIHk9IjIiIHdpZHRoPSIxMDAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMzMzM2ZmIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogNzQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBJQ08gU2VydmVyPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzMzMzNmZiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q2xpZW50IGFwcDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDcyIiB5PSIyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzMzMzNmZiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDQ3M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Zb3VyIFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1MS41IDQwMiBMIDUxLjUgNjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzgwODA4MCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDMxMS41IDQwMyBMIDMxMS41IDYyIiBmaWxsPSJub25lIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1MjIgNDAyIEwgNTIxLjUgNjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzgwODA4MCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc5MS41IDQwMiBMIDc5MSA2MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjODA4MDgwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTIgMTIyIEwgMzA1LjYzIDEyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjODA4MDgwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDMxMC44OCAxMjIgTCAzMDMuODggMTI1LjUgTCAzMDUuNjMgMTIyIEwgMzAzLjg4IDExOC41IFoiIGZpbGw9IiM4MDgwODAiIHN0cm9rZT0iIzgwODA4MCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAzMTIgMTcyIEwgNTguMzcgMTcyIiBmaWxsPSJub25lIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTMuMTIgMTcyIEwgNjAuMTIgMTY4LjUgTCA1OC4zNyAxNzIgTCA2MC4xMiAxNzUuNSBaIiBmaWxsPSIjODA4MDgwIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTIgMjIyIEwgNTE1LjYzIDIyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjODA4MDgwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDUyMC44OCAyMjIgTCA1MTMuODggMjI1LjUgTCA1MTUuNjMgMjIyIEwgNTEzLjg4IDIxOC41IFoiIGZpbGw9IiM4MDgwODAiIHN0cm9rZT0iIzgwODA4MCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA1MjIgMzcyIEwgNTguMzcgMzcyIiBmaWxsPSJub25lIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTMuMTIgMzcyIEwgNjAuMTIgMzY4LjUgTCA1OC4zNyAzNzIgTCA2MC4xMiAzNzUuNSBaIiBmaWxsPSIjODA4MDgwIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjYwLjc1IiB5PSIxNTIiIHdpZHRoPSIyNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE2MnB4OyBtYXJnaW4tbGVmdDogNjJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4+UmV0dXJuIHRoZSB1c2VyJ3Mgb3BlbklEIGFuZCBhY2Nlc3MgdG9rZW48L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxNTIiIHk9IjIwMiIgd2lkdGg9IjMyMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjEycHg7IG1hcmdpbi1sZWZ0OiAxNTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4+UGFzcyB0aGUgdXNlcidzwqAgb3BlbklEIGFuZCBhY2Nlc3MgdG9rZW4gdG8geW91ciBzZXJ2ZXI8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxODcuNjMiIHk9IjM1MiIgd2lkdGg9IjI0OC43NSIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjQ3cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzYycHg7IG1hcmdpbi1sZWZ0OiAxODlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4+UGFzcyB0aGUgdmVyaWZpY2F0aW9uIHJlc3VsdCB0byB0aGUgY2xpZW50IGFwcDwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTIyIDI3MiBMIDc4NS42MyAyNzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzgwODA4MCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3OTAuODggMjcyIEwgNzgzLjg4IDI3NS41IEwgNzg1LjYzIDI3MiBMIDc4My44OCAyNjguNSBaIiBmaWxsPSIjODA4MDgwIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNzkyIDMyMiBMIDUyOC4zNyAzMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzgwODA4MCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1MjMuMTIgMzIyIEwgNTMwLjEyIDMxOC41IEwgNTI4LjM3IDMyMiBMIDUzMC4xMiAzMjUuNSBaIiBmaWxsPSIjODA4MDgwIiBzdHJva2U9IiM4MDgwODAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjUyMiIgeT0iMjUyIiB3aWR0aD0iMjYwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyNThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNjJweDsgbWFyZ2luLWxlZnQ6IDUyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48c3Bhbj5TZW5kIGFuIFMyUyBQT1NUIHJlcXVlc3QgdG8gdmVyaWZ5IHRoZSB1c2VyPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTY5LjUiIHk9IjMwMiIgd2lkdGg9IjE2NSIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTYzcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzEycHg7IG1hcmdpbi1sZWZ0OiA1NzFweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4+UmV0dXJuIHRoZSB2ZXJpZmljYXRpb24gcmVzdWx0PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNzIiIHk9IjkyIiB3aWR0aD0iMjE3LjUiIGhlaWdodD0iMzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxNnB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwN3B4OyBtYXJnaW4tbGVmdDogNzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4+Q2FsbCBVc2VyU2VydmljZS48L3NwYW4+R2V0TG9nZ2VkSW5Vc2VyPHNwYW4+KCkgYW5kIFVzZXJTZXJ2aWNlLjwvc3Bhbj5HZXRBY2Nlc3NUb2tlbjxzcGFuPigpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxCellList&quot;:[&quot;Xfazc13W&quot;,&quot;Pect1uf9&quot;,&quot;fkTlT7Qu&quot;,&quot;Z539nP1d&quot;,&quot;cXs6FUi4&quot;,&quot;RoNrnoMR&quot;,&quot;M8zaEDlA&quot;,&quot;4oxEyOF4&quot;,&quot;3FhSaSvf&quot;,&quot;BaK1zykg&quot;,&quot;pM7frAmN&quot;,&quot;Fu18QyUR&quot;,&quot;UzVBmucS&quot;,&quot;GGWqxH6L&quot;,&quot;Y3W4vaID&quot;,&quot;bCeq8Y90&quot;,&quot;G4YXVlas&quot;,&quot;1b1jS6t3&quot;,&quot;RoCLheCQ&quot;,&quot;rxOxCEeU&quot;,&quot;El2aViLr&quot;,&quot;BABJ8NvO&quot;],&quot;mxGraphModel&quot;:{&quot;arrows&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;dx&quot;:&quot;782&quot;,&quot;dy&quot;:&quot;472&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageHeight&quot;:&quot;1169&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;tooltips&quot;:&quot;1&quot;},&quot;mxCellMap&quot;:{&quot;1b1jS6t3&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;590&quot;,&quot;y&quot;:&quot;310&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;860&quot;,&quot;y&quot;:&quot;310&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;1b1jS6t3&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;strokeColor=#808080;&quot;,&quot;value&quot;:&quot;&quot;},&quot;3FhSaSvf&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;590&quot;,&quot;y&quot;:&quot;440&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;589.5&quot;,&quot;y&quot;:&quot;100&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;dashed&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;3FhSaSvf&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=none;dashed=1;html=1;strokeColor=#808080;&quot;,&quot;value&quot;:&quot;&quot;},&quot;4oxEyOF4&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;379.5&quot;,&quot;y&quot;:&quot;441&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;379.5&quot;,&quot;y&quot;:&quot;100&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;dashed&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;4oxEyOF4&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=none;dashed=1;html=1;strokeColor=#808080;entryX=0.5;entryY=1;entryDx=0;entryDy=0;&quot;,&quot;value&quot;:&quot;&quot;},&quot;BABJ8NvO&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;30&quot;,&quot;width&quot;:&quot;217.5&quot;,&quot;x&quot;:&quot;140&quot;,&quot;y&quot;:&quot;130&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;id&quot;:&quot;BABJ8NvO&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;&quot;,&quot;value&quot;:&quot;Call UserService.GetLoggedInUser() and UserService.GetAccessToken()&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;BaK1zykg&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;859.5&quot;,&quot;y&quot;:&quot;440&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;859&quot;,&quot;y&quot;:&quot;100&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;dashed&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;BaK1zykg&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=none;dashed=1;html=1;strokeColor=#808080;&quot;,&quot;value&quot;:&quot;&quot;},&quot;El2aViLr&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;165&quot;,&quot;x&quot;:&quot;637.5&quot;,&quot;y&quot;:&quot;340&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;id&quot;:&quot;El2aViLr&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;&quot;,&quot;value&quot;:&quot;Return the verification result&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;Fu18QyUR&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;380&quot;,&quot;y&quot;:&quot;210&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;210&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;Fu18QyUR&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;strokeColor=#808080;&quot;,&quot;value&quot;:&quot;&quot;},&quot;G4YXVlas&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;248.75&quot;,&quot;x&quot;:&quot;255.63&quot;,&quot;y&quot;:&quot;390&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;id&quot;:&quot;G4YXVlas&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;&quot;,&quot;value&quot;:&quot;Pass the verification result to the client app&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;GGWqxH6L&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;590&quot;,&quot;y&quot;:&quot;410&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;410&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;GGWqxH6L&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;strokeColor=#808080;&quot;,&quot;value&quot;:&quot;&quot;},&quot;M8zaEDlA&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;119.5&quot;,&quot;y&quot;:&quot;440&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;119.5&quot;,&quot;y&quot;:&quot;100&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;dashed&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;M8zaEDlA&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=none;dashed=1;html=1;strokeColor=#808080;&quot;,&quot;value&quot;:&quot;&quot;},&quot;Pect1uf9&quot;:{&quot;id&quot;:&quot;Pect1uf9&quot;,&quot;parent&quot;:&quot;Xfazc13W&quot;},&quot;RoCLheCQ&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;860&quot;,&quot;y&quot;:&quot;360&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;590&quot;,&quot;y&quot;:&quot;360&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;RoCLheCQ&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;strokeColor=#808080;&quot;,&quot;value&quot;:&quot;&quot;},&quot;RoNrnoMR&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;100&quot;,&quot;x&quot;:&quot;540&quot;,&quot;y&quot;:&quot;40&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;id&quot;:&quot;RoNrnoMR&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;strokeColor=#3333FF;&quot;,&quot;value&quot;:&quot;Your Server&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;UzVBmucS&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;260&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;590&quot;,&quot;y&quot;:&quot;260&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;UzVBmucS&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;strokeColor=#808080;&quot;,&quot;value&quot;:&quot;&quot;},&quot;Xfazc13W&quot;:{&quot;id&quot;:&quot;Xfazc13W&quot;},&quot;Y3W4vaID&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;240&quot;,&quot;x&quot;:&quot;128.75&quot;,&quot;y&quot;:&quot;190&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;id&quot;:&quot;Y3W4vaID&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;&quot;,&quot;value&quot;:&quot;Return the user's openID and access token&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;Z539nP1d&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;100&quot;,&quot;x&quot;:&quot;810&quot;,&quot;y&quot;:&quot;40&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;id&quot;:&quot;Z539nP1d&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;strokeColor=#3333FF;&quot;,&quot;value&quot;:&quot;PICO Server&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;bCeq8Y90&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;320&quot;,&quot;x&quot;:&quot;220&quot;,&quot;y&quot;:&quot;240&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;id&quot;:&quot;bCeq8Y90&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;&quot;,&quot;value&quot;:&quot;Pass the user's  openID and access token to your server&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;cXs6FUi4&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;100&quot;,&quot;x&quot;:&quot;70&quot;,&quot;y&quot;:&quot;40&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;id&quot;:&quot;cXs6FUi4&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;strokeColor=#3333FF;&quot;,&quot;value&quot;:&quot;Client app&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;fkTlT7Qu&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;160&quot;,&quot;x&quot;:&quot;300&quot;,&quot;y&quot;:&quot;40&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;id&quot;:&quot;fkTlT7Qu&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;strokeColor=#3333FF;&quot;,&quot;value&quot;:&quot;PICO Platform Services&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;pM7frAmN&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;160&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;380&quot;,&quot;y&quot;:&quot;160&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;pM7frAmN&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;strokeColor=#808080;&quot;,&quot;value&quot;:&quot;&quot;},&quot;rxOxCEeU&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;260&quot;,&quot;x&quot;:&quot;590&quot;,&quot;y&quot;:&quot;290&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;id&quot;:&quot;rxOxCEeU&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;&quot;,&quot;value&quot;:&quot;Send an S2S POST request to verify the user&quot;,&quot;vertex&quot;:&quot;1&quot;}}},&quot;diagramType&quot;:&quot;flowchart&quot;,&quot;lastEditTime&quot;:0}" />

1. Launch the CoreService from within the Unity.
2. Call `UserService.GetLoggedInUser()` and `UserService.GetAccessToken()` to retrieve the user's openID and access token.
   To get the user's account information, including the openID:
   ```C#
   UserService.GetLoggedInUser().OnComplete(msg =>
   {
       if (msg.IsError)
       {
           Log($"GetLoggedInUser failed: code={msg.Error.Code} message={msg.Error.Message}");
           return;
       }
   
       User user = msg.Data;
       Log($"GetLoggedInUser success: {User2String(user)}");
   });
   ```

   To get the user's access token:
   ```C#
   UserService.GetAccessToken().OnComplete(msg =>
   {
       if (msg.IsError)
       {
           Log($"Got access token error:code={msg.Error.Code} {msg.Error.Message} ");
           return;
       }
   
       string accessToken = msg.Data;
       Log($"Got accessToken {accessToken}");
   });
   ```

3. Pass the access token and userID to your own server. This server will then send an S2S POST request to the PICO server for user verification. Therefore, you need to use the "[Verify a user](/reference/unity-server/latest/verify-a-user/)" S2S API to verify the user.

### Send friend requests
Below is the code sample that demonstrates the process of sending a friend request to a user, during which a system-level panel will pop up for the sender to fill in remarks. The API request returns the `LaunchFriendResult` structure. `LaunchFriendResult.DidCancel` indicates whether the sender has canceled the friend request, and `LaunchFriendResult.DidSendRequest` indicates whether the friend request has been successfully sent. If the two users are already friends or if the friend request fails because one of them has added the another person to the blocklist, `msg.Error.Code` and `msg.Error.Message` returns the error information, and you can refer to the "[Error codes](/reference/unity-server/latest/error-codes/)" article (from error code 10101 to 10108) for details.
```C#
// Send a friend request to a user
UserService.LaunchFriendRequestFlow(targetUserId).OnComplete(msg =>
{
    if (msg.IsError)
    {
        Log($"Launch friend request failed {msg.Error}");
        return;
    }

    var launchResult = msg.Data;
    Log($"Launch friend request ok:DidCancel={launchResult.DidCancel},DidSend={launchResult.DidSendRequest}");
});
```

Get the current user's friend list:
```C#
// Get the current user's friend list
UserService.GetFriends().OnComplete(msg =>
{
    if (msg.IsError)
    {
        Log($"Get Friends error {msg.Error}");
        return;
    }

    var userList = msg.Data;
    Log($"Your friends count:{userList.Count}");
});
```

### Retrieve a user's organization ID
An organization is allowed to create multiple apps on the PICO Developer Platform. If a user purchases multiple apps created by the same organization, the user will have a unique organization ID for all the apps purchased. You can pass the user's openID in `UserService.GetOrgScopedID` to retrieve the user's organization ID.
The following code sample demonstrates how to get the user's organization ID through async/await API calls:
```C#
async void GetLoggedInUserOrgId()
{
    // Get the user's openID first
    var userMsg = await UserService.GetLoggedInUser().Async();
    if (userMsg.IsError)
    {
        Debug.LogError($"GetLoggedInUser failed {userMsg.Error}");
        return;
    }

    var myId = userMsg.Data.ID;
    // Get the user's organization ID
    var orgMsg = await UserService.GetOrgScopedID(myId).Async();
    if (orgMsg.IsError)
    {
        Debug.LogError($"GetOrgScopeID failed {orgMsg.Error}");
        return;
    }

    Debug.Log($"My orgId is {orgMsg.Data.ID}");
}
```

### Check entitlements
User entitlement checks are used to verify if users are entitled to access your app. Refer to the "User entitlement check" article for detailed instructions and code samples.
### Sign in users with OIDC
OpenID Connect (OIDC) is an OAuth2-based authentication mechanism. You can use OIDC to enable users to log in to third-party platforms, such as the Unity Gaming Service, using their PICO accounts.
**Step 1: Complete preparatory tasks**
Refer to [Unity's official instructions](https://docs.unity.com/authentication/en-us/manual/get-started) to complete the following tasks:

1. Sign up for the Unity Gaming Service (UGS).
2. Link your project to a cloud project in the Unity Editor.
3. Install Unity's Authentication package for your project.

**Step 2: Add the identity provider offered by PICO**

1. Open an existing scene or create a new scene in the Unity Editor.
2. Go to **Edit** > **Project Settings** > **Services** > **Authentication**.
3. Select **OpenID Connect** from the **Identity Provides** list and click the **Add** button.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/772e6949fc7640abb892e22f4a123cd8~tplv-goo7wpa0wc-image.image)
4. Add and save identity provider information according to your app's distribution country/region. If your app is distributed to both Mainland China and Non-Mainland China countries/regions, you need to add two identity providers.
   | **Mainland China apps** | **Non-Mainland China apps** |
   | --- | --- |
   | Add and save the following identity provider information: <br>  <br> * Client ID: your app's ID <br> * Oidc Name: oidc-pico-cn <br> * Issuer(URL): https://platform-cn.picovr.com | Add and save the following identity provider information: <br>  <br> * Client ID: your app's ID <br> * Oidc Name: oidc-pico-global <br> * Issuer(URL): https://platform-us.picovr.com |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6624eb4452041949334e1fabf3dd038~tplv-goo7wpa0wc-image.image)

**Step 3: Sign in users to the Unity Gaming Service through OIDC**
The following code sample demonstrates how to sign in users to the Unity Gaming Service through OIDC. You first need to select the proper identity provider according to the country/region information of the user's device, then get the user's ID token, and finally call the `SignInWithPICO` and `LinkWithPICO` functions.
```C++
using System;
using Pico.Platform;
using Unity.Services.Authentication;
using Unity.Services.Core;
using UnityEngine;
using Task = System.Threading.Tasks.Task;

public static class PICOAuth
{
    private static async System.Threading.Tasks.Task<(string, string)> GetProviderNameAndIDToken()
    {
        string providerName, idToken;
        {
            // Get the device's country/region info
            var systemInfo = ApplicationService.GetSystemInfo();
            // Select the proper identity provider according to the device's country/region info
            providerName = systemInfo.IsCnDevice ? "oidc-pico-cn" : "oidc-pico-global";
        }
        {
            // Get the user's ID token
            var message = await UserService.GetIdToken().Async();
            if (message.IsError)
            {
                Debug.LogError(message.Error);
                throw new Exception("Failed to get id token");
            }

            idToken = message.Data;
        }
        return (providerName, idToken);
    }

    public static async Task SignInWithPICO()
    {
        var (provider, idToken) = await GetProviderNameAndIDToken();
        try
        {
            await AuthenticationService.Instance.SignInWithOpenIdConnectAsync(provider, idToken);
            Debug.Log($"SignIn is successful. {AuthenticationService.Instance.PlayerId}");
        }
        catch (Exception ex)
        {
            Debug.LogException(ex);
        }
    }

    public static async Task LinkWithPICO()
    {
        var (provider, idToken) = await GetProviderNameAndIDToken();
        try
        {
            await AuthenticationService.Instance.LinkWithOpenIdConnectAsync(provider, idToken);
            Debug.Log($"Link is successful. {AuthenticationService.Instance.PlayerId}");
        }
        catch (AuthenticationException ex) when (ex.ErrorCode == AuthenticationErrorCodes.AccountAlreadyLinked)
        {
            // Prompt the user with an error message
            Debug.LogError("This user is already linked with another account. Log in instead.");
        }
        catch (AuthenticationException ex)
        {
            // Compare the error code to AuthenticationErrorCodes
            // Prompt the user with the proper error message
            Debug.LogException(ex);
        }
        catch (RequestFailedException ex)
        {
            // Compare the error code to CommonErrorCodes
            // Prompt the user with the proper error message
            Debug.LogException(ex);
        }
    }
}
```

## API reference
### Client APIs
The following table lists the functions packaged in the `UserService` class. To learn more information about these functions, refer to the [API reference](/reference/unity/client-api/UserService/).
| **Function** | **Description** |
| --- | --- |
| `UserService.GetAccessToken` | Get the current user's access token. |
| `UserService.GetLoggedInUser` | Get the information about the current logged-in user. |
| `UserService.Get` | Get the information about a specified user. Return the same fields as `UserService.GetLoggedInUser`. |
| `UserService.LaunchFriendRequestFlow` | Send a friend request to someone else. |
| `UserService.GetFriends` | Get the friend list of the current user. <br> ***Note***: The friend list is retrievable only if the current user and the user's friends have all used the same app and authorized the app to access their friend lists. |
| `UserService.GetNextUserListPage` | Get the next page of user list. |
| `UserService.RequestUserPermissions` | Request the permission to view a user's information, exercise data, etc. |
| `UserService.GetAuthorizedPermissions` | Get the permissions the user has granted to your app. |
| `UserService.EntitlementCheck` <br>  | Verify if users are entitled to use your app, that is, whether they have purchased the app or obtained the right to use it through other legitimate means. This can be used to protect your app's copyright. |
| `UserService.GetIdToken` | Get the user's ID token for login with OIDC. |
| `UserService.GetOrgScopedID` | Get the user's unique ID in all the apps created by your organization. |
### Server APIs

* [Verify a user](/reference/unity-server/latest/verify-a-user/)
* [Retrieve a user's social relationship](/reference/unity-server/latest/query-social-relationships/)
* [Retrieve a user's friend list](/reference/unity-server/latest/get-friend-list/)
* [Get a user's organization ID](/reference/unity-server/latest/get-organization-id/)

## Demo 
### UserDemo
You can use the UserDemo to debug Account & Friends service on PICO VR headset. For more information, refer to the "[User demo](/en_user-demo)" article.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29005d521ff14217a63f760887c161f3~tplv-goo7wpa0wc-image.image" width="700px" />

### SimpleDemo
SimpleDemo shows how to initialize platform services, request user permission, and get the information of the currently logged-in user. For more information on the demo, refer to the "[Simple demo for platform services](/en_simple-demo)" article.


# --- END: Accounts & Friends.md ---



# --- BEGIN: API list(2).md ---

This article lists the client APIs and server APIs that you can use to integrate the leaderboard service into your app.
## Client APIs
The following table lists the functions packaged in the `LeaderboardService` class. To learn more information about these functions, refer to the [API reference](/reference/unity/client-api/LeaderboardService/).
| **Function** | **Description** |
| --- | --- |
| LeaderboardService.Get | Get the information about a specified leaderboard. |
| LeaderboardService.GetEntries | Get leaderboard entries, including the total number of entries, entry ID, score, extra information, rank, and more. |
| LeaderboardService.GetEntriesAfterRank | Get the entries after a specified rank. |
| LeaderboardService.GetEntriesByIds | Get the entries for specified users on a specific leaderboard. |
| LeaderboardService.WriteEntry | Write an entry to a leaderboard. |
| LeaderboardService.WriteEntryWithSupplementaryMetric | Write an entry to a leaderboard. The entry can contain supplementary metrics for the tiebreaker. |
## Server APIs

* [Create or modify a leaderboard](/reference/unity-server/latest/create-or-modify-leaderboard/)
* [Get leaderboard details](/reference/unity-server/latest/get-leaderboard-info/)
* [Get all the leaderboards in an app](/reference/unity-server/latest/get-all-leaderboard-ids/)
* [Delete a specific leaderboard](/reference/unity-server/latest/delete-a-leaderboard/)
* [Create or modify a leaderboard entry](/reference/unity-server/latest/create-or-modify-leaderboard-entries/)
* [Get leaderboard entries](/reference/unity-server/latest/get-leaderboard-entries/)
* [Delete a specified entry for a leaderboard](/reference/unity-server/latest/delete-a-specified-leaderboard-entry/)
* [Delete all entries for a leaderboard](/reference/unity-server/latest/delete-all-entries/)


# --- END: API list(2).md ---



# --- BEGIN: API list(3).md ---

This article lists the client APIs and server APIs that you can use to integrate the achievement service into your app.
## Client APIs
The following table lists the functions packaged in the `AchievementsService` class. To learn more information about these functions, refer to the [API reference](/reference/unity/client-api/AchievementsService/).
| **Function** | **Description** |
| --- | --- |
| AchievementsService.GetDefinitionsByName | Get the information of a specified achievement. The information includes the achievement's API name, description, and whether it is unlocked. |
| AchievementsService.GetAllDefinitions | Get the information of all achievements. |
| AchievementsService.GetProgressByName | Get the progress the user has made for unlocking a specified achievement. |
| AchievementsService.GetAllProgress | Get the progress the user has made for unlocking all achievements. |
| AchievementsService.AddCount | Add a count to a specified count achievement. |
| AchievementsService.AddFields | Unlock the bit(s) of a specified bitfield achievement. |
| AchievementsService.Unlock | Unlock a specified achievement of any type even if the target for unlocking this achievement is not reached. |
## Server APIs

* [Create or update an achievement](/reference/unity-server/latest/create-or-update-achievement/)
* [Get the basic information of achievements](/reference/unity-server/latest/get-basic-achievement-info/)
* [Update a user's achievement progress](/reference/unity-server/latest/update-user-achievement-progress/)
* [Get a user's achievement progress](/reference/unity-server/latest/get-user-achievement-progress/)
* [Delete a user's achievement progress](/reference/unity-server/latest/delete-user-achievement-progress/)


# --- END: API list(3).md ---



# --- BEGIN: API list.md ---

This article lists the APIs that you can use to implement the Social Interaction service. Each API is given a description explaining what it can do. For detailed descriptions of each API's input parameters and returns, check out the [API reference](/reference/unity/client-api/PresenceService/).
## Invite friends
| **API** | **Description** | **Remark** |
| --- | --- | --- |
| PresenceService.Set | Sets all presence information for a user, including the destination, joinability, lobby session ID, match session ID, and extra information. | - |
| PresenceService.Clear | Clears a user's presence information. | - |
| PresenceService.GetInvitableUsers | Gets invitable friends. | - |
| PresenceService.LaunchInvitePanel | Invites friends to a destination. | The system default Invite UI provided by the PICO Friends app will be launched if using the three APIs. |
| RoomService.LaunchInvitableUserFlow | Invites friends to a private room. |  |
| ChallengesService.LaunchInvitableUserFlow | Invites friends to a challenge. |  |
| PresenceService.SendInvites | Invites friends to a destination. | You need to customize the Invite UI if using the three APIs. |
| RoomService.InviteUser | Invites friends to a private room. |  |
| ChallengesService.Invite | Invites friends to a challenge. |  |
| PresenceService.GetSentInvites | Gets the sent invitations. | - |
## Get destinations
| **API** | **Description** |
| --- | --- |
| PresenceService.GetDestinations | Gets all the destinations you created on the PICO Developer Platform. |
| PresenceService.GetNextDestinationListPage | Gets the next page of destinations. |
## Jump between apps
| **API** | **Description** |
| --- | --- |
| ApplicationService.LaunchApp | Directs the user to another app by specifying the app package name. |
| ApplicationService.LaunchAppByAppId | Directs the user to another app by specifying the app ID. |
| ApplicationService.LaunchStore | Directs the user to the current app's details page on the PICO Store. |
| ApplicationService.GetLaunchDetails | Gets app launch details. |
| ApplicationService.SetLaunchIntentChangedCallback | When the launch intent has changed, you will receive this notification. Then you can call ApplicationService.GetLaunchDetails to retrieve the launch details. |
## Share content
| **API** | **Description** |
| --- | --- |
| PresenceService.ShareVideo | Shares videos attached with thumbnails on the Douyin app. |
| PresenceService.ShareVideoByImages | Shares screenshots on the Douyin app. |


# --- END: API list.md ---



# --- BEGIN: AR Foundation.md ---

This article introduces how to use the AR Foundation-based features that the PICO Unity Integration SDK provides. You can set up these features from scratch, or configure relevant AR Foundation samples to make them compatible with the PICO Unity Integration SDK.
## Feature support
PICO Unity Integration SDK supports the following features provided by AR Foundation:
| **Feature** | **Description** |
| --- | --- |
| Session | Enable, disable, and configure AR on the target platform. |
| Device Tracking | Track the device's position and rotation in a physical space. |
| Camera | Render images from the device's cameras. |
| Face Tracking | Detect and track human faces. |
| Body Tracking | Detect and track human bodies. |
| Anchors | Track arbitrary points in space. |
| Meshing | Generate meshes of the environment. |
## Overall system requirements
Below are the overall development environment requirements, and each feature has its own extra requirements.
|  | **SDK 3.0.0 & 3.0.5** | **SDK 3.1.0** |
| --- | --- | --- |
| **Unity** | 2022.3 | Unity 6 |
| **AR Foundation** | 5.1 | 6.0 |
## Limitations
Image tracking is currently not supported.
## Unity's AR Foundation samples
If you want to use Unity's AR Foundation samples, visit the Unity-Technologies GitHub and pull the branch you want.

* [For Unity 2022.3 and AR Foundation 5.1](https://github.com/Unity-Technologies/arfoundation-samples/tree/5.1).
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8e839313fb8489fa68a27a081350d86~tplv-goo7wpa0wc-image.image)
* [For Unity 6 and AR Foundation 6.0](https://github.com/Unity-Technologies/arfoundation-samples/?tab=readme-ov-file).
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dad5d18c1d2c422f8319ee653feed2ca~tplv-goo7wpa0wc-image.image)

## PICO's AR Foundation samples
PICO's AR Foundation samples are provided at repository [PICOARFoundationSamples-Unity](https://github.com/Pico-Developer/PICOARFoundationSamples-Unity). After pulling this repository, you can go to \PICOARFoundationSamples-Unity\Assets\Scenes\PICO to access the samples. These samples have been made compatible with the PICO Unity Integration SDK. You can directly compile them and run them on your PICO device.
If there are already official AR Foundation samples in your project, you can import the PICO folder into your project and then refer to PICO's samples to make official AR Foundation samples compatible with the PICO Unity Integration SDK.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0d82c38361042ec8f7dc99213b1c8dd~tplv-goo7wpa0wc-image.image" width="1684px" />

## Enable AR Foundation
Before using AR Foundation-based features, go to  **Edit** > **Project Settings** > **XR Plug-in Management** > **PICO** > **Android Settings**, and check the **AR Foundation** checkbox to enable AR Foundation. If you want to use a specific feature, check the corresponding checkbox to enable its permission.

* **Body Tracking**: for enabling Body Tracking permission
* **Face Tracking**: for enabling Face Tracking permission
* **Anchor**: for enabling Anchor permission
* **Meshing**: for enabling Meshing permission

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f9e4c0c58344c3693ec7aaf1979ee77~tplv-goo7wpa0wc-image.image" width="700px" />

## Camera
This section introduces how to use the camera.
### Extra requirements

* PICO device models: PICO 4 series and PICO 4 Ultra series
* PICO device's system version: 5.11.0 or later

### Basic usage
You can use the camera after adding the XR Origin (XR Rig) object to the scene.

1. Open your project in the Unity Editor.
2. In the **Hierarchy** window, click **+** > **XR** > **XR Origin (AR)** to add the **XR Origin (XR Rig)** object to the scene.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/593a0ce8ef204f7ea22c1afd94a72cba~tplv-goo7wpa0wc-image.image" width="1834px" />   

### Advanced usage
This section introduces how to set up camera effects provided by PICO.
After adding the XR Origin (XR Rig) object, go to **Edit** > **Project Settings** > **XR Plug-in Management** > **PICO** > **Android Settings** and check the **AR Foundation** checkbox to enable AR Foundation for your project.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/291959a78dc44f8bb01c826ce09cd9f9~tplv-goo7wpa0wc-image.image" width="700px" />

Once enabled, AR Foundation automatically sets up the camera as follows:

* Set camera.backgroundColor to new Color(0, 0, 0, 0);
* Add the **PXR_AR Camera Effect Manager (Script)** component to the **Main Camera** object which is under the **XR Origin (XR Rig)** directory.

You can then check the **Camera Offset** checkbox on the  **PXR_AR Camera Effect Manager (Script)** pane and do the following setting as needed:

* Set video seethrough-related parameters, including color temperature, brightness, saturation, and contrast.
* Set the LUT texture.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/615e4da98be94ee5a7c221d3f7129b63~tplv-goo7wpa0wc-image.image" width="2560px" />

## Body Tracking
This section introduces how to use the Body Tracking feature. You can set up the Body Tracking feature from scratch or configure the relevant official AR Foundation sample to make it compatible with the PICO Unity Integration SDK.
### Extra requirements

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series
* PICO device's system version: 5.11.0 or later
* PICO Motion Tracker (Official)

### Important notes

* The SDK only supports tracking 24 body joints. The avatar model may consist of more than 24 body joints, so you need to manually select the joints for matching.
* The names of `BodyTrackerRole` enumeration values in the PXR_Bone Controller (Script) component must match the joint names of the avatar model. If the joint names of the avatar model change, you need to make an update accordingly.

### Basic usage
This section introduces how to use the default human skeleton provided by AR Foundation to implement body tracking effects.

1. Open your project in the Unity Editor.
2. Refer to the "Enable AR Foundation" section to enable AR Foundation and body tracking permission for your project.
3. In the **Hierarchy** window:
   1. Click **+** > **XR** > **XR Origin (AR)** to add the **XR Origin (XR Rig)** object to the scene;
   2. Click **+** > **XR** > **AR Session** to add the **AR Session** object to the scene.
4. Go to the **Project** window and add the **BodyTracking** prefab to the scene.
   <a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f92fc070b9046eb8751249b116de851~tplv-goo7wpa0wc-image.image" filename="BodyTracking.prefab" download>BodyTracking.prefab</a>
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa6d0f97f8f949cc928be2a5946c5ed2~tplv-goo7wpa0wc-image.image" width="2560px" />   

   The BodyTracking prefab includes 24 body joints supported by the SDK. 
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96c3b28cbc8e407eb67665326a6e2e33~tplv-goo7wpa0wc-image.image)
5. Select the **XR Origin (XR Rig)** object and go to the **Inspector** window to complete the following for it:
   1. Add the **AR Human Body Manager (Script)** and **PXR_Human Body Tracker (Script)** components;
   2. On the **AR Human Body Manager (Script)** panel, uncheck the **Pose 2D** checkbox;
   3. On the **PXR_Human Body Tracker (Script)** panel, set **Skeleton Prefab** as the previously added BodyTracking prefab, then set **Human Body Manager** as the **AR Human Body Manager (Script)** component added to the **XR Origin (XR Rig)** object.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67e02ff2860c41a0973483a4fc959020~tplv-goo7wpa0wc-image.image" width="2560px" />   

6. Build your project and run it on a PICO device to see if body tracking works.

### Advanced usage
This section explains how to animate a custom avatar model using the 24 body joints from the BodyTracking prefab.

1. Import your avatar model into the scene and identify the body joints that need to be animated.
2. Under the BodyTracking prefab, locate the corresponding body joints you want to animate. Create child nodes under these body joints (for example, if the parent node is `RIGHT_ANKLE`, create a child node named `Right Ankle Target`). These child nodes are used to capture and reflect body movement data.
3. Use the child nodes included in the BodyTracking prefab as animating signals to control the movements or poses of your avatar model, as illustrated below:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ae11bb964e14e8b9e158acd47d1cb09~tplv-goo7wpa0wc-image.image)
4. If the coordinate system of the body joint data differs from that of the avatar model's joints, you need to transform the coordinate system of the child nodes in the BodyTracking prefab, as illustrated below:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d392f779ebc14ef89f34a0ac7408c0ac~tplv-goo7wpa0wc-image.image)
   The 24 body joints in the BodyTracking prefab are currently displayed using cubes. When using the prefab, you can delete the Cube (Mesh Filter) and Mesh Renderer components to remove the visual representation.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0d034eca65a4ba0a72c5581984567c4~tplv-goo7wpa0wc-image.image" width="2521px" />   

### Directly configure Unity's AR Foundation sample
This section explains how to configure the HumanBodyTracking3D scene provided in arfoundation-samples, making it compatible with the PICO Unity Integration SDK.

1. Copy the **HumanBodyTracking3D** scene and rename it as **PICOHumanBodyTracking3D**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb8d373b85ef4bd2ae3ce97e6fb5e308~tplv-goo7wpa0wc-image.image)
2. Place the **ControlledRobot** prefab into the scene, delete the **Bone Controller (Script)** component originally added to the prefab, and add the **PXR_Bone Controller (Script)** component to it.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4b92e1b1258477e8348c7e64d817ac0~tplv-goo7wpa0wc-image.image)
3. Change the component added to the **Human Body Tracking** object to **PXR_Human Body Tracker (Script)**, and configure it as shown below:
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e39e61e9a7414f6280593310f9b44d44~tplv-goo7wpa0wc-image.image" width="2024px" />   

   At this point, the basic setup for the HumanBodyTracking3D scene is complete. If you need to further optimize it, please continue with the steps below.
4. In the scene, add a mirror to display the avatar from the front.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7dcbb0ad37aa4a81959bc0dc7fb276d1~tplv-goo7wpa0wc-image.image" width="2024px" />   

5. Activate the Back button in the scene.
   Once activated, if you navigate from the PICOMenu scene to this scene, you can click the Back button to return to the PICOMenu scene.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f3d71e210f74d7f9b9c7727dffede89~tplv-goo7wpa0wc-image.image" width="2018px" />   

### BodyTrackerRole enumeration
Below are the values of the `BodyTrackerRole` enumeration:
```C#
public enum BodyTrackerRole
    {
        Root = 0,
        LeftUpLeg = 1,
        RightUpLeg = 2, 
        Spine3 = 3, 
        LeftLeg = 4, 
        RightLeg = 5, 
        Spine6 = 6,  
        LeftFoot = 7, 
        RightFoot = 8, 
        Spine7 = 9, 
        LeftToes = 10, 
        RightToes = 11,
        Neck1 = 12,  
        LeftShoulder1 = 13, 
        RightShoulder1 = 14, 
        Neck4 = 15, 
        LeftArm = 16,  
        RightArm = 17,  
        LeftForearm = 18, 
        RightForearm = 19, 
        LeftHand = 20, 
        RightHand = 21, 
        LeftHandMid1 = 22, 
        RightHandMid1 = 23, 
    }
```

### Body joint reference
The following illustration shows the 24 body joints that the SDK supports tracking.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f52d92fad814aef8191806fe5d5bab5~tplv-goo7wpa0wc-image.image" width="650px" />

### PICO's sample scripts
After importing PICO's sample scenes into your project, you can refer to the codes in XR_BoneController.cs and PXR_HumanBodyTracker.cs scripts to configure Unity's official AR Foundation scenes.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06bb46d4ae694de08dad1dd98006aabd~tplv-goo7wpa0wc-image.image" width="1836px" />

## Face Tracking
This section explains how to use the Face Tracking feature. You can set up the Face Tracking feature from scratch or configure the relevant official AR Foundation sample to make it compatible with the PICO Unity Integration SDK.
### Extra requirements

* PICO device model: PICO 4 Enterprise, which is equipped with the face tracking camera
* PICO device's system version: 5.11.0 or later

### Integrate the Face Tracking feature

1. Open your project in the Unity Editor.
2. Refer to the "Enable AR Foundation" section to enable AR Foundation and face tracking permission for your project.
3. In the **Hierarchy** window, click **+** > **XR** > **XR Origin (AR)** to add the **XR Origin (XR Rig)** object to the scene.
4. Select the **XR Origin (XR Rig)** object and add the **AR Face Manager (Script)** and **AR Session (Script)** components to it in the **Inspector** window.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5460ab34a104727a352b4182a0c57bf~tplv-goo7wpa0wc-image.image" width="2063px" />   

5. Add a face model to the scene, then add the **PXR_Blend Shape Visualizer (Script)** component to it and set the **Skinned Mesh Renderer** parameter.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1217b3d7b1b64c0b9eee33e51f8f0eaa~tplv-goo7wpa0wc-image.image" width="2783px" />   

6. Modify the name of blend shapes in the PXR_BlendShapeVisualizer.cs file if necessary.
   **Note**
   The PXR_BlendShapeVisualizer.cs file contains code for parsing the face model. When using it, ensure that the blend shapes of the face model correctly correspond to the 52 blend shapes provided by the SDK. If they do not match, you will need to modify the blend shape names in the code to align with those of your face model.  The "Example blend shapes setup" section is for your reference.

   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a963a5e0bd8949a887839de6aa80217d~tplv-goo7wpa0wc-image.image" width="2791px" />   

### Directly configure Unity's AR Foundation sample
This section explains how to configure the ARKitFaceBlendShapes scene provided in arfoundation-samples, making it compatible with the PICO Unity Integration SDK.

1. Copy the **ARKitFaceBlendShapes** scene and rename it as **PICOFaceBlendShapes**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be779138210842f797601f680675132e~tplv-goo7wpa0wc-image.image)
2. In the scene, place the facial model **SlothHead**, replace the originally added **AR Kit Blend Shape Visualizer (Script)** component with the **PXR_Blend Shape Visualizer (Script)** component, and configure the **Skinned Mesh Renderer**.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d17c456726dc4efc88a04a414cd92e28~tplv-goo7wpa0wc-image.image" width="2027px" />   

3. Modify the name of blend shapes in the PXR_BlendShapeVisualizer.cs file if necessary.
   **Note**
   The PXR_BlendShapeVisualizer.cs file contains code for parsing the face model. When using it, ensure that the blend shapes of the face model correctly correspond to the 52 blend shapes provided by the SDK. If they do not match, you will need to modify the blend shape names in the code to align with those of your face model.  The "Example blend shapes setup" section is for your reference.

   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b88649117dff43e09c9790a910419dc4~tplv-goo7wpa0wc-image.image" width="2791px" />   

### Example blend shapes setup
In the following code, the bold codes should be the blend shape names of the face model.
```C#
void CreateFeatureBlendMapping()
        {
            if (skinnedMeshRenderer == null || skinnedMeshRenderer.sharedMesh == null)
            {
                return;
            }

            const string strPrefix = "blendShape2.";
            m_FaceBlendShapeIndexMap = new Dictionary<BlendShapeIndex, int>();

            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeLookDown_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeLookDown_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.NoseSneer_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "noseSneer_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeLookIn_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeLookIn_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.BrowInnerUp] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "browInnerUp");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.BrowDown_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "browDown_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthClose] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthClose");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthLowerDown_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthLowerDown_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.JawOpen] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "jawOpen");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthUpperUp_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthUpperUp_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthShrugUpper] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthShrugUpper");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthFunnel] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthFunnel");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeLookIn_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeLookIn_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeLookDown_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeLookDown_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.NoseSneer_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "noseSneer_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthRollUpper] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthRollUpper");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.JawRight] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "jawRight");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.BrowDown_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "browDown_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthShrugLower] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthShrugLower");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthRollLower] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthRollLower");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthSmile_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthSmile_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthPress_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthPress_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthSmile_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthSmile_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthPress_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthPress_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthDimple_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthDimple_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthLeft] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthLeft");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.JawForward] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "jawForward");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeSquint_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeSquint_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthFrown_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthFrown_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeBlink_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeBlink_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.CheekSquint_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "cheekSquint_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.BrowOuterUp_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "browOuterUp_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeLookUp_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeLookUp_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.JawLeft] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "jawLeft");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthStretch_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthStretch_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthPucker] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthPucker");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeLookUp_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeLookUp_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.BrowOuterUp_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "browOuterUp_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.CheekSquint_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "cheekSquint_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeBlink_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeBlink_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthUpperUp_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthUpperUp_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthFrown_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthFrown_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeSquint_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeSquint_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthStretch_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthStretch_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.CheekPuff] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "cheekPuff");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeLookOut_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeLookOut_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeLookOut_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeLookOut_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeWide_R] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeWide_R");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.EyeWide_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "eyeWide_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthDimple_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthDimple_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthLowerDown_L] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthLowerDown_L");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.MouthRight] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "mouthRight");
            m_FaceBlendShapeIndexMap[BlendShapeIndex.TongueOut] = skinnedMeshRenderer.sharedMesh.GetBlendShapeIndex(strPrefix + "tongueOut");
        }
```

## Anchors
The AR Anchor Manager component provided by Unity can create a GameObject for each anchor. 
### Extra requirements

* PICO device model: PICO 4 series
* PICO device's system version: 5.11.0 or later

### Use anchors
Before using it, open your project in the Unity Editor and refer to the "Enable AR Foundation" section to enable AR Foundation and anchor permission for your project.  For detailed instructions on using the Anchor feature, refer to [Unity's documentation](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@5.1/manual/features/anchors.html).
## Meshing
The AR Mesh Manager component provided by Unity can dynamically scan real-world scenes in real time and convert the content of those scenes into meshes.
### Extra requirements

* PICO device model: PICO 4 Ultra series
* PICO device's system version: 5.11.0 or later

### Use meshing
Below are brief instructions on using the AR Mesh Manager component. For detailed instructions, refer to [Unity's documentation](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@5.1/manual/features/meshing.html). 

1. Open your project in the Unity Editor and refer to the "Enable AR Foundation" section to enable AR Foundation for your app.
2. Add the **AR Mesh Manager (Script)** component to a child GameObject of the **XR Origin (XR Rig)** object. 
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9b43aff1ba243d6bcfbcb5cc3febac5~tplv-goo7wpa0wc-image.image" width="2560px" />   

3. Set the MeshPrefab to the prefab that will be instantiated for each scanned mesh. The MeshPrefab must contain at least one **Mesh Filter** component. If you want to render the scanned mesh, you also need to add a **Mesh Renderer** component and a **Material** component to the GameObject of the MeshPrefab.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ea89491644c45a5b1b911fb49e98e50~tplv-goo7wpa0wc-image.image)

### Code sample
Code sample can be found in the following ARMeshManager.cs file.
<a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/135eb742392345b9a61d743d22600d99~tplv-goo7wpa0wc-image.image" filename="ARMeshManager.cs" download>ARMeshManager.cs</a>


# --- END: AR Foundation.md ---



# --- BEGIN: Build review-related FAQs.md ---

Refer to [this article](/document/distribute/app-functionality-review-faqs/).


# --- END: Build review-related FAQs.md ---



# --- BEGIN: Camera image data (for enterprise device).md ---

This article introduces how to obtain camera data from PICO devices.
## Usage restrictions
This feature can only be used on PICO 4 Ultra Enterprise.
## Request permissions
To obtain camera data, camera permission must be requested. The steps are as follows:

1. In the Unity Editor, go to **Edit** > **Project Settings** > **Player** > **Build**, and check the **Custom Main Manifest** checkbox.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/312ebe591e83461396dfa9f985c3345d~tplv-goo7wpa0wc-image.image)
2. In the AndroidManifest.xml file, add the following content.
   ```XML
   <uses-permission android:name="android.permission.CAMERA" /> 
   ```

   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62e3bd849ae440f69a102695c137df4b~tplv-goo7wpa0wc-image.image)
   A dynamic permission request occurs when the `OpenCameraAsync` API is called, and you must click confirm before camera data can be accessed.

## Bind TobService
```C#
PXR_Enterprise.InitEnterpriseService();
PXR_Enterprise.BindEnterpriseService(b =>
{
    Debug.Log($"{tag}  Bind enterprise service success={b}");
} );
```

## Configure and enable Global data
```C#
PXR_Enterprise.UseGlobalPose(true);
```

## Set parameters
```C#
void Configurefor4U(Dictionary<string, string> setting=null)
```

If no map value is provided, the default configuration is used.
`KEY_OUTPUT_CAMERA_RAW_DATA = "output-camera-raw-data";//` can be used to obtain images with distortion.
Code example:
```C#
Dictionary<string, string> cameraParams1 = new Dictionary<string, string>();
// When set to true, outputs the camera's native image
cameraParams1.Add(PXRCapture.KEY_OUTPUT_CAMERA_RAW_DATA, PXRCapture.VALUE_TRUE);
PXR_Enterprise.Configurefor4U(cameraParams1);
```

`void Configurefor4U(bool enableMvHevc, int videoFps)`

* `enableMvHevc`: Recording mvhevc is currently not supported; set to `false`.
* `videoFps`: Takes effect when the value is greater than `0`. If the value is less than or equal to `0`, use the default frame rate. Recommended value range: 5–60 fps, default value is 60 fps.

## Enable camera functionality
```C#
void OpenCameraAsyncfor4U(Action<bool> callback)
public static void OpenCameraAsyncfor4U(Action<bool> callback,Dictionary<string, string> setting=null)
```

Asynchronously returns whether the camera has been enabled successfully. After successful activation, execute the interfaces used for obtaining camera data and other operations.
Code example:
```TypeScript
Dictionary<string, string> cameraParams = new Dictionary<string, string>();
cameraParams.Add(PXRCapture.KEY_MCTF, PXRCapture.VALUE_TRUE);
cameraParams.Add(PXRCapture.KEY_EIS, PXRCapture.VALUE_FALSE);
cameraParams.Add(PXRCapture.KEY_MFNR, PXRCapture.VALUE_TRUE);

PXR_Enterprise.OpenCameraAsyncfor4U(ret =>
{
    Debug.Log($"{tag}  OpenCameraAsync ret=  {ret}");
},cameraParams);
```

## Image mode
```C#
public enum  PXRCaptureRenderMode{
    PXRCapture_RenderMode_LEFT, // Data from the left camera
    PXRCapture_RenderMode_RIGHT,// Data of the right camera
    PXRCapture_RenderMode_3D,// Merge the data from the left and right cameras into a single image
    PXRCapture_RenderMode_Interlace, // Alternating output between left and right eyes, the difference between timestamp intervals is 1
}
```

## Render camera image data to the specified Android Surface
```C#
bool StartPreviewfor4U(IntPtr surfaceObj, PXRCaptureRenderMode mode)
```

Once enabled, the content will be rendered onto the specified Android Surface based on the image mode.
## Obtain camera image data
The steps are as follows:

1. Set buffer and callback.
   ```C#
   // Set buffer parameters and callback information for data retrieval
   bool SetCameraFrameBufferfor4U(int width, int height, ref IntPtr data, Action<Frame> imageAvailable)
   
   public struct Frame
   {
       public UInt32 width;          // width
       public UInt32 height;         // height
       public UInt64 timestamp;      // start of exposure time:ns (BOOTTIME)
       public UInt32 datasize;       // datasize
       public IntPtr data;           // image data
       public UnityEngine.Pose pose; // The head Pose at the time of image production.（Right-handed coordinate system: X right, Y up, Z in）
       public int status;            // sensor status(1:good 0:bad)
   }
   ```

   Usage example:
   ```C#
   byte[] imgByte = new byte[width*height*4];
   IntPtr data=Marshal.UnsafeAddrOfPinnedArrayElement(imgByte,0);
   PXR_Enterprise.SetCameraFrameBufferfor4U(width,height,ref data, (Frame frame) =>
   {
       texture.LoadRawTextureData(imgByte);
       texture.Apply();
       Debug.Log("onImageAvailable cameraFramePredictedDisplayTime = "+frame.timestamp);
       Debug.Log("onImageAvailable size = "+frame.datasize);
   });
   ```

2. Enable the functionality for obtaining image data based on image mode.
   ```C#
   bool StartGetImageDatafor4U(PXRCaptureRenderMode mode, int width, int height) 
   ```

## Local and global coordinate systems in the conversion engine under floorlevel mode
```C#
public enum ConvertCoordinateType{
    kLocal2Global = 0,
    kGlobal2Local = 1,
}
/**
*  Convert pose coordinates
 *  type: conversion type
 *  srcPose:original pose
 *  destPose: pose after original conversion
 * \return: 0 indicates success; any other value indicates failure
 */
int ConvertPoseCoordinate(PXR_EnterprisePlugin.ConvertCoordinateType type,UnityEngine.Pose srcPose,ref UnityEngine.Pose destPose)
```

After conversion, the pose is still in the left-handed coordinate system.
Camera coordinate systems generally use the right-handed system, while Unity uses a left-handed system. Therefore, when unifying to the algorithm's global coordinate system (global), conversion between left-handed and right-handed coordinate systems must be performed.

Usage example:
Set XR Origin's **Tracking Origin Mode** to **Floor**.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/819bcf9598e3477ab1ccb3bed430e35f~tplv-goo7wpa0wc-image.image)
For example, using hand pose data:
```C#
if (PXR_HandTracking.GetJointLocations(handType, ref handJointLocations))
{

    for (int i = 0; i < handJoints.Count; ++i)
    {
    
        Pose srcPose = new Pose();
        Pose detPose = new Pose();
        srcPose.position = handJointLocations.jointLocations[i].pose.Position.ToFloat3();
        srcPose.rotation = handJointLocations.jointLocations[i].pose.Orientation.ToFloat4();
        PXR_Enterprise.ConvertPoseCoordinate(PXR_EnterprisePlugin.ConvertCoordinateType.kLocal2Global,srcPose, ref detPose);
    
        handJointLocations.jointLocations[i].pose.Position.x=detPose.position.x;
        handJointLocations.jointLocations[i].pose.Position.y=detPose.position.y;
        handJointLocations.jointLocations[i].pose.Position.z=detPose.position.z;
    
        handJointLocations.jointLocations[i].pose.Orientation.x=detPose.rotation.x;
        handJointLocations.jointLocations[i].pose.Orientation.y=detPose.rotation.y;
        handJointLocations.jointLocations[i].pose.Orientation.z=detPose.rotation.z;
        handJointLocations.jointLocations[i].pose.Orientation.w=detPose.rotation.w;
    }
}
```

## Close and release cameras
```C#
bool CloseCamerafor4U()
```

## Obtain intrinsic and extrinsic parameters

1. Use the default FOV of the PICO 4 Ultra device to obtain external and internal parameter data.
   ```C#
   public static RGBCameraParamsNew GetCameraParametersNewfor4U(int width, int height)
   
   public struct RGBCameraParamsNew
   {
       // Internal reference data
       public double fx;
       public double fy;
       public double cx;
       public double cy;
   
       // External parameter data of the left eye
       public Vector3 l_pos;
       public Quaternion l_rot;
       // External parameter data of the right eye
       public Vector3 r_pos;
       public Quaternion r_rot;
   }
   ```

2. Calculate based on the configured width, height, and FOV. Only obtain intrinsic parameter data, corresponding to the `RGBCameraParamsNew` structure's `cx`, `cy`, `fx`, and `fy` parameters.

```C#
 double[] GetCameraIntrinsicsfor4U(int width, int height, double h_fov, double v_fov)
```

3. Obtain the original matrix of external parameters.
   * `left`: Returns the external parameter data (matrix) of the left eye
   * `right`: Returns the external parameter data (matrix) of the right eye

```C#
public static bool GetCameraExtrinsicsfor4U(out Matrix4x4 left, out Matrix4x4 right)
```

## Obtain HeadPose data
When calling the `UseGlobalPose` API, the second parameter can be set to `true` or omitted (by default, global data is returned). If `UseGlobalPose` is called and the second parameter is set to `false`, local data will be returned.
```C#
PXR_Enterprise.GetPredictedMainSensorState(time, false);
```

## Handle screen on and off states
After the screen is turned off, the camera will keep updating data because it is not controlled by the Unity lifecycle. The camera will only be forcibly powered off after entering sleep mode. It is recommended to handle the screen-on and screen-off states properly.
```C#
private bool isRunning=false; // After calling StartGetImageData, set the status to true
static bool  reopen = false;

private void Update()
{
    if (reopen)
    {
        // Execute the reopen functionality in the main thread
        reopen = false;
        PXR_Enterprise.StartGetImageDatafor4U(Mode, (int)frame.width, (int)frame.height);  
    }
}

private void OnApplicationPause(bool pauseStatus)
{
    if (isRunning)
    {
        // After the data acquisition function has been started
        if (pauseStatus)
        {
            // If the screen turns off, execute the close function and release the camera
            PXR_Enterprise.CloseCamerafor4U();
        }
        else
        {
            // Turn off the screen again or turn on the screen, then reopen the camera
            PXR_Enterprise.OpenCameraAsyncfor4U(ret =>
            {
                Debug.Log($"{tag}  OpenCameraAsync ret=  {ret}");
                // Modify the flag indicating reopening
                reopen = ret;
            });
        }
    }
    
}
```


# --- END: Camera image data (for enterprise device).md ---



# --- BEGIN: Camera image data (user device).md ---

This article describes how to use the APIs provided by the `PXR_CameraImage` class to manage camera image
 data on PICO XR devices.
## About PXR_CameraImage
`PXR_CameraImage` is a static utility class that encapsulates camera-related capabilities for PICO XR devices, mainly including:

* Enumerating available cameras on the device
* Querying camera properties and capabilities (resolution, format, frame rate, model, and more)
* Creating and managing camera devices and capture sessions
* Retrieving camera intrinsic and extrinsic parameters
* Acquiring and releasing camera image data in real time

The underlying implementation of `PXR_CameraImage` is based on the OpenXR extension `XR_PICO_camera_image`, and relies on the asynchronous capabilities provided by `XR_EXT_future`.
## System requirements

* Device model: PICO 4 Ultra, Project Swan
* Device's system version:
   * PICO 4 Ultra: 5.15.0 or later
   * Project Swan: PICO OS 6

## Prerequisites
Declare camera permissions in AndroidManifest.xml.
```XML
<uses-permission android:name="android.permission.CAMERA" />
```

## Overall workflow

1. Request camera permissions.
2. Call `GetAvailableCameras` to obtain available cameras.
3. Query camera capabilities (resolution, format, and more).
4. Call `CreateCameraDeviceAsync` to create a camera device.
5. Call `CreateCameraCaptureSessionAsync` to create a capture session.
6. Call `BeginCameraCapture` to start capturing images.
7. Use `AcquireCameraImage` in a loop to acquire images.
8. Process the acquired images.
9. Call `ReleaseCameraImage` to release image resources.
10. Call `EndCameraCapture` to end capturing.
11. Call `DestroyCameraCaptureSession` and `DestroyCameraDevice` to clean up resources.

![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e549f6f68bd435c8a69c6817ea04784~tplv-goo7wpa0wc-image.image)
## Code samples
### Get available cameras
Get the list of available camera IDs on the device.
```C#
public void GetAvailableCameras()
{
    PxrResult ret = PXR_CameraImage.GetAvailableCameras(out XrCameraIdPICO[] cameraIds);
    if (ret == PxrResult.SUCCESS)
    {
        foreach (var cameraId in cameraIds)
        {
            Debug.Log("CameraAPITest GetAvailableCameras cameraId:" + cameraId);
        }
    }
}
```

### Get supported property types of the camera
Get the list of supported property types for the specified camera.
```C#
public void GetCameraPropertyTypesAvailable()
{
    PxrResult ret = PXR_CameraImage.GetCameraPropertyTypesAvailable(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO,
        out XrCameraPropertyTypePICO[] types);
    if (ret == PxrResult.SUCCESS)
    {
        foreach (var type in types)
        {
            Debug.Log("CameraAPITest GetCameraPropertyTypesAvailable type:" + type);
        }
    }
}
```

### Get the camera's orientation
Get the camera orientation.
```C#
public void GetCameraFacingProperties()
{
    var ret = PXR_CameraImage.GetCameraFacingProperties(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO,
        out XrCameraFacingPICO facing);
    Debug.Log("CameraAPITest GetCameraFacingProperties ret:" + ret + " facing:" + facing);
}
```

### Get the camera's position
Get the camera position.
```C#
public void GetCameraPositionProperties()
{
    var ret = PXR_CameraImage.GetCameraPositionProperties(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO,
        out XrCameraPositionPICO position);
    Debug.Log("CameraAPITest GetCameraPositionProperties ret:" + ret + " position:" + position);
}
```

### Get the camera's type
Get the camera type (such as color perspective camera).
```C#
public void GetCameraCameraTypeProperties()
{
    var ret = PXR_CameraImage.GetCameraCameraTypeProperties(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO,
        out XrCameraTypePICO cameraTypePico);
    Debug.Log("CameraAPITest GetCameraCameraTypeProperties ret:" + ret + " cameraTypePico:" + cameraTypePico);
}
```

### Get supported capability types of the camera
Get the list of supported capability types for the specified camera.
```C#
public void GetCameraCapabilityAvailable()
{
    var ret = PXR_CameraImage.GetCameraCapabilityAvailable(XrCameraIdPICO.XR_CAMERA_ID_RGB_RIGHT_PICO,
        out XrCameraCapabilityTypePICO[] capabilities);
    if (ret == PxrResult.SUCCESS)
    {
        foreach (var capability in capabilities)
        {
            Debug.Log("CameraAPITest GetCameraCapabilityAvailable capability:" + capability);
        }
    }
}
```

### Get supported image frame rates of the camera
Get the list of supported image frame rates for the camera.
```C#
public void GetCameraImageFpsCapability()
{
    PxrResult ret = PXR_CameraImage.GetCameraImageFpsCapability(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO,
        out XrCameraImageFpsPICO[] imageFps);
    if (ret == PxrResult.SUCCESS)
    {
        foreach (var fps in imageFps)
        {
            Debug.Log("CameraAPITest GetCameraImageFpsCapability fps:" + fps);
        }
    }
}
```

### Get supported camera models of the camera
Get the list of supported camera models for the camera.
```C#
public void GetCameraCameraModelCapability()
{
    PxrResult ret = PXR_CameraImage.GetCameraCameraModelCapability(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO,
        out XrCameraModelPICO[] cameraModels);
    if (ret == PxrResult.SUCCESS)
    {
        foreach (var cameraModel in cameraModels)
        {
            Debug.Log("CameraAPITest GetCameraCameraModelCapability cameraModel:" + cameraModel);
        }
    }
}
```

### Get supported data transmission types of the camera
Get the list of supported data transmission types for the camera.
```C#
public void GetCameraDataTransferTypeCapability()
{
    PxrResult ret = PXR_CameraImage.GetCameraDataTransferTypeCapability(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO,
        out XrCameraDataTransferTypePICO[] dataTransferTypes);
    if (ret == PxrResult.SUCCESS)
    {
        foreach (var dataTransferType in dataTransferTypes)
        {
            Debug.Log("CameraAPITest GetCameraDataTransferTypeCapability dataTransferType:" + dataTransferType);
        }
    }
}
```

### Get supported image formats of the camera
Get the list of supported image formats for the camera.
```C#
public void GetCameraImageFormatCapability()
{
    PxrResult ret = PXR_CameraImage.GetCameraImageFormatCapability(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO,
        out XrCameraImageFormatPICO[] formats);
    if (ret == PxrResult.SUCCESS)
    {
        foreach (var format in formats)
        {
            Debug.Log("CameraAPITest GetCameraImageFormatCapability format:" + format);
        }
    }
}
```

### Get supported image resolutions of the camera
Get the list of supported image resolutions for the camera.
```C#
public void GetCameraImageResolutionCapability()
{
    PxrResult ret = PXR_CameraImage.GetCameraImageResolutionCapability(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO,
        out PxrExtent2Di[] resolutions);
    if (ret == PxrResult.SUCCESS)
    {
        foreach (var resolution in resolutions)
        {
            Debug.Log($"CameraAPITest GetCameraImageResolutionCapability resolution:{resolution.width}x{resolution.height}");
        }
    }
}
```

### Asynchronously create camera device
Asynchronously create a camera device with the specified ID.
```C#
public async void CreateCameraDeviceAsync()
{
    var result0 = await PXR_CameraImage.CreateCameraDeviceAsync(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO);
    Debug.Log("CameraAPITest CreateCameraDeviceAsync result:" + result0);
}
```

### Asynchronously create camera capture session
Asynchronously create a camera capture session and configure capture parameters.
```C#
public async void CreateCameraCaptureSessionAsync()
{
    var result0 = await PXR_CameraImage.CreateCameraCaptureSessionAsync(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO,width, height, fps, format, transferType, model);
    Debug.Log("CameraAPITest CreateCameraCaptureSessionAsync result:" + result0);
}
```

### Destroy camera device
Destroy the camera device with the specified ID.
```C#
public void DestroyCameraDevice()
{
    PxrResult ret = PXR_CameraImage.DestroyCameraDevice(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO);
    Debug.Log("CameraAPITest DestroyCameraDevice result:" + ret);
}
```

### Destroy camera capture session
Destroy the capture session for the specified camera ID.
```C#
public void DestroyCameraCaptureSession()
{
    PxrResult ret = PXR_CameraImage.DestroyCameraCaptureSession(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO);
    Debug.Log("CameraAPITest DestroyCameraCaptureSession result:" + ret);
}
```

### Get camera intrinsic parameters
Get the camera's intrinsic parameter information.
```C#
public void GetCameraIntrinsics()
{
    PxrResult ret = PXR_CameraImage.GetCameraIntrinsics(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO, out XrCameraIntrinsics intrinsics);
    if (ret==PxrResult.SUCCESS)
    {
        Debug.Log($"CameraAPITest GetCameraIntrinsics intrinsics.focalLength:{intrinsics.focalLength.X},{intrinsics.focalLength.Y}");
        Debug.Log($"CameraAPITest GetCameraIntrinsics intrinsics.principalPoint:{intrinsics.principalPoint.X},{intrinsics.principalPoint.Y}");
        Debug.Log($"CameraAPITest GetCameraIntrinsics intrinsics.fov:{intrinsics.fov.X},{intrinsics.fov.Y}");
    }
}
```

### Get camera extrinsic parameters
Get the camera's extrinsic parameter information (position and orientation relative to the device).
```C#
public void GetCameraExtrinsics()
{
    PxrResult ret = PXR_CameraImage.GetCameraExtrinsics(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO, out XrCameraExtrinsics extrinsics);
    if (ret==PxrResult.SUCCESS)
    {
        Debug.Log($"CameraAPITest GetCameraExtrinsics extrinsics.pose.Position:{extrinsics.pose.Position.X},{extrinsics.pose.Position.Y},{extrinsics.pose.Position.Z}");
        Debug.Log($"CameraAPITest GetCameraExtrinsics extrinsics.pose.Orientation:{extrinsics.pose.Orientation.X},{extrinsics.pose.Orientation.Y},{extrinsics.pose.Orientation.Z},{extrinsics.pose.Orientation.W}");
    }
}
```

### Start image capture for the specified camera
Start capturing images with the specified camera.
```C#
public void BeginCameraCapture()
{
    var result0 =PXR_CameraImage.BeginCameraCapture(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO);
    Debug.Log("CameraAPITest BeginCameraCapture result:" + result0);
    isBeginCameraCapture = (result0==PxrResult.SUCCESS);
}
```

### End image capture for the specified camera
End image capture with the specified camera.
```C#
public void EndCameraCapture()
{
    var result0 =PXR_CameraImage.EndCameraCapture(XrCameraIdPICO.XR_CAMERA_ID_RGB_LEFT_PICO);
    Debug.Log("CameraAPITest EndCameraCapture result:" + result0);
    isBeginCameraCapture = !(result0==PxrResult.SUCCESS);
}
```

### Camera image acquisition and resource release

* Acquire a camera image and return the latest image ID.
* Release previously acquired camera image resources.
* Obtain the raw data of the camera image.

The following is the combined call flow for each frame:
```C#
private IEnumerator ProcessCameraImageAsync()
{
    // Acquire camera image
    ulong imageId;
    PxrResult acquireResult = PXR_CameraImage.AcquireCameraImage(targetCamera, lastCaptureTime, out imageId,out Int64 captureTime);
    
    if (acquireResult == PxrResult.SUCCESS && imageId > 0)
    {
        // Obtain the raw data of the image
        XrCameraImageDataRawBuffer imageData;
        if (PXR_CameraImage.GetCameraImageData(targetCamera, imageId, out imageData) == PxrResult.SUCCESS)
        {
            // Render the raw image data to Texture2D
          
        }
        
        // Release image resources
        PXR_CameraImage.ReleaseCameraImage(targetCamera, imageId);
    }
    else if (acquireResult != PxrResult.SUCCESS)
    {
        UpdateStatus($"获取图像失败: {acquireResult}");
    }
    
    yield return null;
}
```

## API reference
To get more information about camera image data-related APIs, refer to the API reference.


# --- END: Camera image data (user device).md ---



# --- BEGIN: Capture, record, and cast screen.md ---

The PDC tool provides a variety of quick tools that you can use to capture, record, and cast your PICO device's screen.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d153667918ea4e2ea10815da0a6cd42d~tplv-goo7wpa0wc-image.image" width="700px" />

## Before you begin
Refer to the "[PICO Developer Center overview](/13136/en_pdc-basic-info#f5a5a632)" article to complete general setups, including installing the PDC tool, enabling the "Developer" mode for your PICO device, and connecting your PICO device to the PC.
## Capture screen
Click **Run** in the **Screenshot** field to capture the current in-app screen. Once finished, click **End** to stop recording. The PDC tool displays the screenshot on a pop-up window. You can:

* Click **Abandon** to abandon the screenshot.
* Click **Save** to save the screenshot on your PC.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8788337e6b044e8903954dc8590f4c5~tplv-goo7wpa0wc-image.image" width="546px" />

## Record screen
Click **Run** in the **Record Screen** field to record the in-app screen. The PDC tool displays the video on a pop-up window. You can:

* Click the **Play** button to play the video.
* Click **Abandon** to abandon the video.
* Click **Save** to save the video on your PC.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1375dd4a98b434f85caef79590fa58e~tplv-goo7wpa0wc-image.image" width="546px" />

## Cast screen
You can cast your PICO screen to your PC by using the PDC tool.
### Prerequsite
Your PICO device has been connected to the same LAN as your PC.
### Procedure

1. Click **Run** in the Cast Device field. 
   The screencast window opens and you can see your PICO device's model on it.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86ff305ee0374fcdba35303adf81bd78~tplv-goo7wpa0wc-image.image)
2. On the screencast page, click **Create screencast connection**. 
   The **Screencast to External Devices** window appears on the HMD.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d8f977ec69544bd85f3c0f6059f72f8~tplv-goo7wpa0wc-image.image)
3. Click **Allow**. 
   The in-app screen appears on the screencast window.
4. On the screencast window, you can:
   * Click the **Volume** button to turn on the volume on your PC.
   * Click **Screenshot **to capture the current screen. 
   * Click **Record Screen** to record the current screen.
   * Click **16:9** to switch the aspect ratio.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3000e4c035641fd99c6cc41bcebae6a~tplv-goo7wpa0wc-image.image)
5. After casting, click **End** at the bottom-left corner of the screencast page. 
   The **End **window appears on the HMD.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8ba2658a9ae45b8804bd09860fb214a~tplv-goo7wpa0wc-image.image)
6. Click **Yes**.


# --- END: Capture, record, and cast screen.md ---



# --- BEGIN: Challenges.md ---

Challenges create fun-to-join competitions among users, which can therefore provide users with more opportunities to interact with others. Challenges are asynchronous events, so users do not have to be online and do challenges at the same time.
Both you and your app's users are able to create challenges, configure challenge settings (including name, visibility, start time, and end time), and invite friends to join challenges to have fun together. Users can also join the challenges created by PICO.
## Key features
### Get challenge info
You can set visibility for challenges. If a challenge is publicly visible, it will then be displayed in your app. Users can view the challenge list and click on a challenge to view its detailed information.
### Proactively join/leave a challenge
Users can view publicly visible challenges and select which to join. Users can also leave challenges if desired.
### Invite friends to challenges
Users can invite their friends to join challenges, including in-progress and unstarted challenges. Invitees will receive a notification in PICO IM and can decide whether to accept the invitation. After an invitee accepts an invitation:

* If the leaderboard for that challenge is associated with a destination, the app will be launched, and the user will be directed to the destination.
* If the leaderboard for that challenge is not associated with any destination, the app will be launched, and the user will be directed to the Home page.

You can design the Inivite UI by yourself or call the relevant API to implement the system default Invite UI (as shown below) provided by the PICO Friends app.
This API launches the system default invite-friend pane (as shown below) where all of the user's friends are displayed. If an invited friend has not installed the app, the friend will be directed to the app's details page in the PICO Store after clicking the invitation card.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a90d4e8a42224b85b3b57c78fea3b983~tplv-goo7wpa0wc-image.image" width="340px" />

### Manage challenge entries
Challenges belong to leaderboards. Each challenge will use the sorting method and score type of the leaderboard it belongs to. If a user leaves the challenge, the user's entry will be deleted. Challenge and leaderboard entries are separately stored and updated case by case:

* **Update challenge entries only**
   If the latest challenge score is equal to or better than the current challenge score but is worse than the current leaderboard score, the latest score will be written to the challenge entry only.
* **Update both challenge and leaderboard entries**
   If the latest score is equal to or better than both the current challenge and leaderboard scores, the latest score will be written to both challenge and leaderboard entries..

## Overall workflow
Challenges belong to leaderboards, which means that you and your app's users can only create challenges for existing leaderboards. You are also able to manage challenge-related data such as challenge entries. Below is the overall workflow:

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1NjVweCIgaGVpZ2h0PSI3MzVweCIgdmlld0JveD0iLTAuNSAtMC41IDU2NSA3MzUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDIgMjUgTCAyIDIgTCAyODIgMiBMIDI4MiAyNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDIgMjUgTCAyIDczMiBMIDI4MiA3MzIgTCAyODIgMjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMiAyNSBMIDI4MiAyNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTJweCI+PHRleHQgeD0iMTQxLjUiIHk9IjE4Ij5EZXZlbG9wZXI8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMTQyIDExMiBMIDE0MiAxNTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTQyIDE2MC44OCBMIDEzOC41IDE1My44OCBMIDE0MiAxNTUuNjMgTCAxNDUuNSAxNTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iNDIiIHk9IjUyIiB3aWR0aD0iMjAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODJweDsgbWFyZ2luLWxlZnQ6IDQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBub25lOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DcmVhdGUgYSBsZWFkZXJib2FyZCBhbmQgY29tcGxldGUgbGVhZGVyYm9hcmQgc2V0dGluZ3Mgb24gdGhlIFBJQ08gRGV2ZWxvcGVyIFBsYXRmb3JtPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDE0MiAyMjIgTCAxNDIgMjg5LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE0MiAyOTQuODggTCAxMzguNSAyODcuODggTCAxNDIgMjg5LjYzIEwgMTQ1LjUgMjg3Ljg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxyZWN0IHg9IjQyIiB5PSIxNjIiIHdpZHRoPSIyMDAiIGhlaWdodD0iNjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTJweDsgbWFyZ2luLWxlZnQ6IDQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBub25lOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DcmVhdGUgY2hhbGxlbmdlKHMpIGZvciB0aGUgbGVhZGVyYm9hcmQgYW5kIGNvbXBsZXRlIGNoYWxsZW5nZSBzZXR0aW5ncyBvbiB0aGUgUElDTyBEZXZlbG9wZXIgUGxhdGZvcm08L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQyIiB5PSIyOTYiIHdpZHRoPSIyMDAiIGhlaWdodD0iNjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMjZweDsgbWFyZ2luLWxlZnQ6IDQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBub25lOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EaXNwbGF5IGNoYWxsZW5nZShzKSBpbiB0aGUgYXBwPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0MiIgeT0iNTE2IiB3aWR0aD0iMjAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTQ2cHg7IG1hcmdpbi1sZWZ0OiA0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogbm9uZTsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+V3JpdGUgdGhlIHVzZXIncyBzY29yZSB0byBhIGNoYWxsZW5nZSBlbnRyeTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyODIgMjUgTCAyODIgMiBMIDU2MiAyIEwgNTYyIDI1IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI4MiAyNSBMIDI4MiA3MzIgTCA1NjIgNzMyIEwgNTYyIDI1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI4MiAyNSBMIDU2MiAyNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTJweCI+PHRleHQgeD0iNDIxLjUiIHk9IjE4Ij5Vc2VyPC90ZXh0PjwvZz48cmVjdCB4PSIzMjIiIHk9IjQyMiIgd2lkdGg9IjIwMCIgaGVpZ2h0PSI2MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQ1MnB4OyBtYXJnaW4tbGVmdDogMzIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBub25lOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5UaGUgdXNlciBjb21wbGV0ZXMgYSBjaGFsbGVuZ2UgPGJyIC8+T1I8YnIgLz5UaGUgdXNlciBhY2NlcHRzIGFuIGludml0YXRpb24gYW5kIGNvbXBsZXRlcyBhIGNoYWxsZW5nZcKgPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMjIiIHk9IjY0MiIgd2lkdGg9IjIwMCIgaGVpZ2h0PSI2MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDY3MnB4OyBtYXJnaW4tbGVmdDogMzIzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBub25lOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5WaWV3IHRoZSBsYXRlc3Qgc2NvcmUgYW5kIHJhbmtpbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjMyMiIgeT0iMTUyIiB3aWR0aD0iMjAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTgycHg7IG1hcmdpbi1sZWZ0OiAzMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IG5vbmU7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNyZWF0ZSBjaGFsbGVuZ2UocykgZm9yIHRoZSBsZWFkZXJib2FyZCBhbmQgY29tcGxldGUgY2hhbGxlbmdlIHNldHRpbmdzIGluIHRoZSBhcHA8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTQyIDM1NiBMIDE0MiA0NTIgTCAzMTUuNjMgNDUyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDMyMC44OCA0NTIgTCAzMTMuODggNDU1LjUgTCAzMTUuNjMgNDUyIEwgMzEzLjg4IDQ0OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDIyIDIxMiBMIDQyMiAzMjYgTCAyNDguMzcgMzI2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI0My4xMiAzMjYgTCAyNTAuMTIgMzIyLjUgTCAyNDguMzcgMzI2IEwgMjUwLjEyIDMyOS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjQyIDgyIEwgNDIyIDgyIEwgNDIyIDE0NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0MjIgMTUwLjg4IEwgNDE4LjUgMTQzLjg4IEwgNDIyIDE0NS42MyBMIDQyNS41IDE0My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQyMiA0ODIgTCA0MjIgNTQ2IEwgMjQ4LjM3IDU0NiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNDMuMTIgNTQ2IEwgMjUwLjEyIDU0Mi41IEwgMjQ4LjM3IDU0NiBMIDI1MC4xMiA1NDkuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE0MiA1NzYgTCAxNDIgNjA5IEwgNDIyIDYwOSBMIDQyMiA2MzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDIyIDY0MC44OCBMIDQxOC41IDYzMy44OCBMIDQyMiA2MzUuNjMgTCA0MjUuNSA2MzMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PC9nPjwvc3ZnPg==" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxCellList&quot;:[&quot;Xfazc13W&quot;,&quot;Pect1uf9&quot;,&quot;a2P22wOT&quot;,&quot;1FQKxFGb&quot;,&quot;MJsr5DBs&quot;,&quot;e9WFqloL&quot;,&quot;KWhYEc3i&quot;,&quot;u90o8LQQ&quot;,&quot;djVZYdNV&quot;,&quot;XR0z6YES&quot;,&quot;tcIGuMZR&quot;,&quot;QMPqJDRL&quot;,&quot;5QOILM5r&quot;,&quot;pU3FxO3i&quot;,&quot;vEDg40Ny&quot;,&quot;2rA3Aamp&quot;,&quot;oOlJhYnK&quot;,&quot;zV6m5RJz&quot;],&quot;mxGraphModel&quot;:{&quot;arrows&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;dx&quot;:&quot;782&quot;,&quot;dy&quot;:&quot;472&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageHeight&quot;:&quot;1169&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;tooltips&quot;:&quot;1&quot;},&quot;mxCellMap&quot;:{&quot;1FQKxFGb&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;1FQKxFGb&quot;,&quot;parent&quot;:&quot;a2P22wOT&quot;,&quot;source&quot;:&quot;MJsr5DBs&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;KWhYEc3i&quot;},&quot;2rA3Aamp&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;2rA3Aamp&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;MJsr5DBs&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;5QOILM5r&quot;},&quot;5QOILM5r&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;200&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;150&quot;},&quot;id&quot;:&quot;5QOILM5r&quot;,&quot;parent&quot;:&quot;XR0z6YES&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fillColor=none;fontStyle=0&quot;,&quot;value&quot;:&quot;Create challenge(s) for the leaderboard and complete challenge settings in the app&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;KWhYEc3i&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;200&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;160&quot;},&quot;id&quot;:&quot;KWhYEc3i&quot;,&quot;parent&quot;:&quot;a2P22wOT&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fillColor=none;fontStyle=0&quot;,&quot;value&quot;:&quot;Create challenge(s) for the leaderboard and complete challenge settings on the PICO Developer Platform&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;MJsr5DBs&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;200&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;50&quot;},&quot;id&quot;:&quot;MJsr5DBs&quot;,&quot;parent&quot;:&quot;a2P22wOT&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fillColor=none;fontStyle=0&quot;,&quot;value&quot;:&quot;Create a leaderboard and complete leaderboard settings on the PICO Developer Platform&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;Pect1uf9&quot;:{&quot;id&quot;:&quot;Pect1uf9&quot;,&quot;parent&quot;:&quot;Xfazc13W&quot;},&quot;QMPqJDRL&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;200&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;640&quot;},&quot;id&quot;:&quot;QMPqJDRL&quot;,&quot;parent&quot;:&quot;XR0z6YES&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fillColor=none;fontStyle=0&quot;,&quot;value&quot;:&quot;View the latest score and ranking&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;XR0z6YES&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;730&quot;,&quot;width&quot;:&quot;280&quot;,&quot;x&quot;:&quot;400&quot;,&quot;y&quot;:&quot;160&quot;},&quot;id&quot;:&quot;XR0z6YES&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;swimlane;&quot;,&quot;value&quot;:&quot;User&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;Xfazc13W&quot;:{&quot;id&quot;:&quot;Xfazc13W&quot;},&quot;a2P22wOT&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;730&quot;,&quot;width&quot;:&quot;280&quot;,&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;160&quot;},&quot;id&quot;:&quot;a2P22wOT&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;swimlane;&quot;,&quot;value&quot;:&quot;Developer&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;djVZYdNV&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;200&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;514&quot;},&quot;id&quot;:&quot;djVZYdNV&quot;,&quot;parent&quot;:&quot;a2P22wOT&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fillColor=none;fontStyle=0&quot;,&quot;value&quot;:&quot;Write the user's score to a challenge entry&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;e9WFqloL&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;e9WFqloL&quot;,&quot;parent&quot;:&quot;a2P22wOT&quot;,&quot;source&quot;:&quot;KWhYEc3i&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;target&quot;:&quot;u90o8LQQ&quot;},&quot;oOlJhYnK&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;oOlJhYnK&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;tcIGuMZR&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=1;entryY=0.5;entryDx=0;entryDy=0;exitX=0.5;exitY=1;exitDx=0;exitDy=0;&quot;,&quot;target&quot;:&quot;djVZYdNV&quot;},&quot;pU3FxO3i&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;pU3FxO3i&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;u90o8LQQ&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0;entryY=0.5;entryDx=0;entryDy=0;exitX=0.5;exitY=1;exitDx=0;exitDy=0;&quot;,&quot;target&quot;:&quot;tcIGuMZR&quot;},&quot;tcIGuMZR&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;200&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;420&quot;},&quot;id&quot;:&quot;tcIGuMZR&quot;,&quot;parent&quot;:&quot;XR0z6YES&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fillColor=none;fontStyle=0&quot;,&quot;value&quot;:&quot;The user completes a challenge <br />OR<br />The user accepts an invitation and completes a challenge &quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;u90o8LQQ&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;200&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;294&quot;},&quot;id&quot;:&quot;u90o8LQQ&quot;,&quot;parent&quot;:&quot;a2P22wOT&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fillColor=none;fontStyle=0&quot;,&quot;value&quot;:&quot;Display challenge(s) in the app&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;vEDg40Ny&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;vEDg40Ny&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;5QOILM5r&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=1;entryY=0.5;entryDx=0;entryDy=0;exitX=0.5;exitY=1;exitDx=0;exitDy=0;&quot;,&quot;target&quot;:&quot;u90o8LQQ&quot;},&quot;zV6m5RJz&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;zV6m5RJz&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;djVZYdNV&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;&quot;,&quot;target&quot;:&quot;QMPqJDRL&quot;}}},&quot;diagramType&quot;:&quot;flowchart&quot;,&quot;lastEditTime&quot;:0}" />

## Integrate the Challenge service
### Step 1: Import the SDK and complete project settings
Import the PICO Unity Integration SDK into your project and complete required project settings. Refer to the following articles for detailed instructions:

* [Import the SDK](/en_import-the-sdk)
* [Complete project settings](/en_complete-project-settings)

### Step 2: Create a leaderboard
Challenges belong to leaderboards. Therefore, a leaderboard's settings, such as the sorting method, score type, and whether to display friends' leaderboard data, will also be applied to the challenges it associates with. For detailed instructions on creating a leaderboard, see [this article](/en_leaderboard#create-a-leaderboard).
### Step 3: Create a challenge
**Method 1:**
You can call the [S2S API](/reference/unity-server/latest/create-a-challenge/) to create a challenge for a specified leaderboard. In addition, users can create challenges in your app.
**Method 2:**
You can use the following steps to create a challenge for a specific leaderboard on the PICO Developer Platform.

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/organization/).
2. From the left navigation pane, select **My Apps**.
   This directs you to the **My Apps** screen.
3. Click on the target app.
   This directs you to the app's **Overview** screen.
4. From the left navigation pane, select **Platform Services** > **Leaderboard**.
   This directs you to the **Leaderboard** screen.
5. Find the target learboard in the list and click the number in the **My challenges** column.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/59e31ec74d12472f97619cb5bbc5bafb~tplv-em5hxbkur4-noop.image?width=2109&height=731)
   This directs you to the following screen:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/ac4efb20a5fb402a8b4aa642b4947898~tplv-em5hxbkur4-noop.image?width=2083&height=726)
6. Click **+ Create Challenge**.
7. On the **New Challenge** screen, follow the on-screen instructions to configure the challenge.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/b1ac6cfc447743bc870936c87f67d535~tplv-em5hxbkur4-noop.image?width=2116&height=1094)
8. Click **Save**.
9. Refer to the figure and table below for more operations:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/a19b8b32e11e498db79a0b756be5e56b~tplv-em5hxbkur4-noop.image?width=2106&height=740)
   | **No.** | **Description** |
   | --- | --- |
   | 1 | Click **My challenges** to view all the challenges you have created. |
   | 2 | Click **User Challenges** to view all the challenges users have created in your app. |
   | 3 | In the **Actions** column, you can: <br>  <br>    * Click **View Entries** to view the challenge's entries. <br>    * Click **Edit** to edit the challenge. <br>    * Click **Delete** to delete the challenge. |

### Step 4: Initialize platform services globally and the game module

* Initialize platform services globally. You can call `CoreService.Initialize()` for synchronous initialization or call `CoreService.AsyncInitialize()` for asynchronous initialization.
* Call `CoreService.GameInitialize` to initialize the game module.

For detailed instructions and code samples, refer to the "[Initialization](/en_initialization)" article.
### Step 5: Implement the Challenge service
Call APIs to implement the Challenge service in your app. Below are example implementations for different scenarios.
**Get challenge info**
Below are relevant APIs:
| **API** | **Description** |
| --- | --- |
| `ChallengesService.Get` | Gets the information about a specified challenge. In addition to basic challenge information, you can also get those who have been invited and joined. |
| `ChallengesService.GetList` | Gets a list of challenges. The challenge list is divided into different pages, so you need to specify which page to return and the number of challenges given on each page. You can also filter challenges by setting `ChallengeOptions`, including the start and end dates of challenges, the leaderboards that the challenges belong to, visibility types, etc. |
Below is an example implementation:
```C#
// Click on the button for getting challenges
void OnGetListBtnClick()
{
    ChallengeOptions options = new ChallengeOptions();
    options.SetTitle("your challenge title");
    options.SetVisibility(ChallengeVisibility.Public);
    options.SetLeaderboardName("your leaderboard name");
    options.SetViewerFilter(ChallengeViewerFilter.AllVisible);
    options.SetIncludeActiveChallenges(true);
    options.SetIncludeFutureChallenges(true);
    options.SetIncludePastChallenges(true);
    
    var task = ChallengesService.GetList(options, 0, 5);
    // Add the `OnComplete` function
    task.OnComplete(OnGetListComplete);
}

void OnGetListComplete(Message<ChallengeList> msg)
{
    if (msg.IsError)
    {
        Debug.Log($"OnGetListComplete error: {msg.GetError().Code}, {msg.GetError().Message}");
        return;
    }
    // Process the returned data (ChallengeList)
}
```

**Proactively join/leave a challenge**
Below are relevant APIs:
| **API** | **Description** |
| --- | --- |
| `ChallengesService.Join` | Allows users to proactively join challenges. Once a user joins a challenge, the user will appear on the list of challenge participants. Once the user leaves the challenge, the user will be removed from the participant list. |
| `ChallengesService.Leave` | Allows users to proactively leave challenges. Once a user leaves a challenge, the user's entry will be deleted. |
Below are example implementations:

* `ChallengesService.Join`
   ```C#
   ChallengesService.Join(challengeID).OnComplete(OnJoinComplete);
   ```

* `ChallengesService.Leave`
   ```C#
   ChallengesService.Leave(challengeID).OnComplete(OnLeaveComplete); 
   ```

`ChallengesService.Join` and `ChallengesService.Leave` have similar `OnComplete`, and the message returned by both requests is `Message<Challenge>`.
```C#
void OnJoinComplete(Message<Challenge> msg)
{
    if (!isError)
    {
        Debug.Log("OnJoinComplete success");
        var data = msg.Data;
        // Process returned data (Challenge)
    }
    else
    {
        Debug.Log("OnJoinComplete failed");
    }
}
```

**Invite friends to challenges**
Below are the APIs that you can use:
| **API** | **Description** |
| --- | --- |
| `ChallengesService.Invite` (without the system default invite-friend pane) | Invite friends to join a challenge. The challenge ID will be sent to the invited friends. <br> ***Note***: You need to design the invite-friends pane by yourself if you use this API. |
| `ChallengesService.LaunchInvitableUserFlow` (with the system default invite-friend pane) | Invite friends to join a challenge. The challenge ID will be sent to the invited friends. This API launches the system default invite-friend pane (as shown below) where all of the user's friends are displayed. If an invited friend has not installed the app, the friend will be directed to the app's details page in the PICO Store after clicking the invitation card. |
Below are example implementations:
```C#
// ChallengesService.Invite
string[] userIds = new string[]{"userid1", "userid2"};
ChallengesService.Invite(challengeID, userIds).OnComplete(OnInviteComplete);
```

```C#
// ChallengesService.LaunchInvitableUserFlow
var task = ChallengesService.LaunchInvitableUserFlow(challengeID).OnComplete((Message message) =>
{
    if (!message.IsError)
    {
        Debug.Log($"OnLaunchInvitableUserFlowComplete no error");
    }
    else
    {
        var error = message.GetError();
        Debug.Log($"OnLaunchInvitableUserFlowComplete error: {error.Message}");
    }
});
```

**Manage challenge entries**
Below are relevant APIs:
| **API** | **Description** |
| --- | --- |
| `LeaderboardService.WriteEntry` | Writes a user's score to a challenge entry on the leaderboard. |
| `ChallengesService.GetEntries` | Gets challenge entries.You can set the `filter` parameter to restrict the scope of entries to return: <br>  <br> * `None`: do not filter, therefore returns all entries. <br> * `Unknown` & `UserIds`: invalid type, returns no entry. <br> * `Friends`: return both your and your friends' entries. <br>  <br> ***Note*** : If you want to filter entries by user ID, you can also call `ChallengesService.GetEntriesByIds`. |
| `ChallengesService.GetEntriesAfterRank` | Gets challenges entries after a specified ranking. |
| `ChallengesService.GetEntriesByIds` | Gets the challenge entry for a specified user. |
Below are example implementations:

* `ChallengesService.GetEntries`
   ```C#
   var task = ChallengesService.GetEntries(challengeID, 
       LeaderboardFilterType.None,
       LeaderboardStartAt.Top, 
       0,
       5).OnComplete(OnGetEntriesComplete);
   ```

* `ChallengesService.GetEntriesByIds`
   ```C#
   string[] userIds = new string[]{"your userid1", "your id2"};
   var task = ChallengesService.GetEntriesByIds(challengeID, 
       LeaderboardStartAt.Top, 
       userIds, 
       0,
       5).OnComplete(OnGetEntriesComplete);
   ```

* `ChallengesService.GetEntriesAfterRank`
   ```C#
   var task = ChallengesService.GetEntriesAfterRank(challengeID,
       5,
       0,
       5);
   task.OnComplete(OnGetEntriesComplete);
   ```

The three methods have the similar `OnComplete`. The message returned by the above three requests is `Message<ChallengeEntryList>`.
```C#
void OnGetEntriesComplete(Message<ChallengeEntryList> msg)
{
    if (msg.IsError)
    {
        Debug.Log($"OnGetEntriesComplete error: {msg.GetError().Code}, {msg.GetError().Message}");
        return;
    }
    // Process returned data (ChallengeEntryList)
}
```

## Best practice
Destinations are locations that users are directed to via deeplinks. You can create destinations and link them to leaderboards so that users can be directed to specific levels, lobbies, or other types of locations after accepting challenge invitations. For detailed instructions on creating a destination, see [this article](/en_interaction#create-a-destination).
## Demo
You can use the ChallengesDemo to debug Challenge service. For more information, refer to the "[Challenges demo](/en_challenge-demo)" article.
## API reference
To learn more about Challenge service-related APIs, refer to the [API reference](/reference/unity/client-api/ChallengesService/).


# --- END: Challenges.md ---



# --- BEGIN: Cloud storage.md ---

Cloud storage is used to back up and restore users' app data, such as identities, custom settings, preference settings, and game progress, on specific devices. You can enable/disable Cloud Storage service for your app on the PICO Developer Platform.
## Requirements

* SDK version: 2.0.5 or later
* Device model: PICO Neo3 and PICO 4 series
* Device's system version:
   | **Mainland China** | **Non-Mainland China** |
   | --- | --- |
   | 4.7.4 or later. | 4.7.1.7 or later. |

## Important notes

* Cloud Storage is only used for simple file backup and recovery, and does not involve data retrieval logic.
* Data recovery only occurs when users use new devices, reset their devices, or reinstall their apps. 

## Data backup workflows
A user can use the same PICO account on multiple PICO VR headsets. Therefore, the data backup workflows and results vary with the number of devices where the PICO account and app are used and run.
### **For a single device**
If a PICO account is used on a single device only, the data backup workflow and result are as follows:

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3MjNweCIgaGVpZ2h0PSI0OTBweCIgdmlld0JveD0iLTAuNSAtMC41IDcyMyA0OTAiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEyMiAzMiBMIDE5NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIwMC44OCAzMiBMIDE5My44OCAzNS41IEwgMTk1LjYzIDMyIEwgMTkzLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5UaGUgdXNlciBkb3dubG9hZHMgeW91ciBhcHAgZm9yIHRoZSBmaXJzdCB0aW1lPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDUyMCAzMiBMIDU0MiAzMiBMIDU4NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU5MC44OCAzMiBMIDU4My44OCAzNS41IEwgNTg1LjYzIDMyIEwgNTgzLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAyMDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIHVzZXIgdXNlcyB5b3VyIGFwcDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTkyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogNTkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRhdGEgYmFja3VwIG9uIHRoZSBjbG91ZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTMyIiB5PSIxMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjJweDsgbWFyZ2luLWxlZnQ6IDU1MnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPlllczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA0NjAgNjIgTCA0NjAgODIgTCAyNjIgODIgTCAyNjIgNjguMzciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNjIgNjMuMTIgTCAyNjUuNSA3MC4xMiBMIDI2MiA2OC4zNyBMIDI1OC41IDcwLjEyIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA0NjAgMiBMIDUyMCAzMiBMIDQ2MCA2MiBMIDQwMCAzMiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiA0MDFweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+TWVldCB0aGUgY2xvdWQgc3RvcmFnZSByZXF1aXJlbWVudHM/PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDMyMiAzMiBMIDM5My42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM5OC44OCAzMiBMIDM5MS44OCAzNS41IEwgMzkzLjYzIDMyIEwgMzkxLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzNDIiIHk9Ijg4IiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA5OHB4OyBtYXJnaW4tbGVmdDogMzYycHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+Tm88L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTIyIDIwMiBMIDE5NS42MyAyMDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMDAuODggMjAyIEwgMTkzLjg4IDIwNS41IEwgMTk1LjYzIDIwMiBMIDE5My44OCAxOTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjE3MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjAycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlRoZSB1c2VyIHVuaW5zdGFsbHMgeW91ciBhcHA8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIwMiIgeT0iMTcyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMDJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EZWxldGUgdGhlIGxvY2FsIGRhdGEgd2hpbGUgcmV0YWluaW5nIHRoZSBjbG91ZCBiYWNrdXAgZGF0YTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMjIgMzcyIEwgMTk1LjYzIDM3MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIwMC44OCAzNzIgTCAxOTMuODggMzc1LjUgTCAxOTUuNjMgMzcyIEwgMTkzLjg4IDM2OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMzQyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIHVzZXIgcmVpbnN0YWxscyB5b3VyIGFwcDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyNjIgNDAyIEwgMjYyIDQ1NyBMIDU5My42MyA0NTciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1OTguODggNDU3IEwgNTkxLjg4IDQ2MC41IEwgNTkzLjYzIDQ1NyBMIDU5MS44OCA0NTMuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYyIDM0MiBMIDMyMiAzNzIgTCAyNjIgNDAyIEwgMjAyIDM3MiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM3MnB4OyBtYXJnaW4tbGVmdDogMjAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk1lZXQgdGhlIGNsb3VkIHN0b3JhZ2UgcmVxdWlyZW1lbnRzPzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMzcyIEwgMzkzLjYzIDM3MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM5OC44OCAzNzIgTCAzOTEuODggMzc1LjUgTCAzOTMuNjMgMzcyIEwgMzkxLjg4IDM2OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA1MjAgMzcyIEwgNTkzLjYzIDM3MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU5OC44OCAzNzIgTCA1OTEuODggMzc1LjUgTCA1OTMuNjMgMzcyIEwgNTkxLjg4IDM2OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNDAwIiB5PSIzNDIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM3MnB4OyBtYXJnaW4tbGVmdDogNDAxcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlJlc3RvcmUgdGhlIGRhdGEgb24gdGhlIHVzZXIncyBkZXZpY2U8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjYwMCIgeT0iMzQyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNzJweDsgbWFyZ2luLWxlZnQ6IDYwMXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5UaGUgdXNlciBjYW4gY29udGludWUgZnJvbSB0aGUgZm9ybWVyIHByb2dyZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MDAiIHk9IjQyNyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDU3cHg7IG1hcmdpbi1sZWZ0OiA2MDFweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIHVzZXIgaGFzIHRvIHVzZSB0aGUgYXBwIGZyb20gc2NyYXRjaDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjUyIiB5PSI0MTciIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQyN3B4OyBtYXJnaW4tbGVmdDogMjcycHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+Tm88L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjM0MCIgeT0iMzUyIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNjJweDsgbWFyZ2luLWxlZnQ6IDM2MHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPlllczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxCellList&quot;:[&quot;Xfazc13W&quot;,&quot;Pect1uf9&quot;,&quot;P0Bvo38e&quot;,&quot;DDZvBtwb&quot;,&quot;YQXFDWCa&quot;,&quot;RF0KinJt&quot;,&quot;262uqCuq&quot;,&quot;q5VtsZ8k&quot;,&quot;JlzilwB4&quot;,&quot;ZxCvrGZg&quot;,&quot;P4ZTfgHS&quot;,&quot;LfJXenDW&quot;,&quot;o674vDEO&quot;,&quot;ose7jbE0&quot;,&quot;pkktcdNB&quot;,&quot;nWtSzh2o&quot;,&quot;NJyEUmuV&quot;,&quot;ahuuHps5&quot;,&quot;yiHdSYsJ&quot;,&quot;Kqg0b67P&quot;,&quot;SETVuuZF&quot;,&quot;RXyGEXDz&quot;,&quot;JOZje1Jd&quot;,&quot;EwYp4Z14&quot;,&quot;mb9fvfbw&quot;,&quot;9pcShJ2H&quot;],&quot;mxGraphModel&quot;:{&quot;arrows&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;dx&quot;:&quot;782&quot;,&quot;dy&quot;:&quot;472&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageHeight&quot;:&quot;1169&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;tooltips&quot;:&quot;1&quot;},&quot;mxCellMap&quot;:{&quot;262uqCuq&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;740&quot;,&quot;y&quot;:&quot;190&quot;},&quot;id&quot;:&quot;262uqCuq&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;Data backup on the cloud&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;9pcShJ2H&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;488&quot;,&quot;y&quot;:&quot;540&quot;},&quot;id&quot;:&quot;9pcShJ2H&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;Yes&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;DDZvBtwb&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;150&quot;,&quot;y&quot;:&quot;190&quot;},&quot;id&quot;:&quot;DDZvBtwb&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user downloads your app for the first time&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;EwYp4Z14&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;748&quot;,&quot;y&quot;:&quot;615&quot;},&quot;id&quot;:&quot;EwYp4Z14&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user has to use the app from scratch&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;JOZje1Jd&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;748&quot;,&quot;y&quot;:&quot;530&quot;},&quot;id&quot;:&quot;JOZje1Jd&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;The user can continue from the former progress&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;JlzilwB4&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;JlzilwB4&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;ZxCvrGZg&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;&quot;,&quot;target&quot;:&quot;RF0KinJt&quot;},&quot;Kqg0b67P&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;468&quot;,&quot;y&quot;:&quot;560&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;Kqg0b67P&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;yiHdSYsJ&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;&quot;,&quot;target&quot;:&quot;RXyGEXDz&quot;,&quot;value&quot;:&quot;&quot;},&quot;LfJXenDW&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;490&quot;,&quot;y&quot;:&quot;276&quot;},&quot;id&quot;:&quot;LfJXenDW&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;No&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;NJyEUmuV&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;150&quot;,&quot;y&quot;:&quot;530&quot;},&quot;id&quot;:&quot;NJyEUmuV&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user reinstalls your app&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;P0Bvo38e&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;P0Bvo38e&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;DDZvBtwb&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;RF0KinJt&quot;,&quot;value&quot;:&quot;&quot;},&quot;P4ZTfgHS&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;470&quot;,&quot;y&quot;:&quot;220&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;740&quot;,&quot;y&quot;:&quot;220&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;P4ZTfgHS&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;RF0KinJt&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;ZxCvrGZg&quot;,&quot;value&quot;:&quot;&quot;},&quot;Pect1uf9&quot;:{&quot;id&quot;:&quot;Pect1uf9&quot;,&quot;parent&quot;:&quot;Xfazc13W&quot;},&quot;RF0KinJt&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;350&quot;,&quot;y&quot;:&quot;190&quot;},&quot;id&quot;:&quot;RF0KinJt&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user uses your app&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;RXyGEXDz&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;548&quot;,&quot;y&quot;:&quot;530&quot;},&quot;id&quot;:&quot;RXyGEXDz&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;Restore the data on the user's device&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;SETVuuZF&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;SETVuuZF&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;RXyGEXDz&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;JOZje1Jd&quot;,&quot;value&quot;:&quot;&quot;},&quot;Xfazc13W&quot;:{&quot;id&quot;:&quot;Xfazc13W&quot;},&quot;YQXFDWCa&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;610&quot;,&quot;y&quot;:&quot;120&quot;},&quot;-1-Array&quot;:{&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;690&quot;,&quot;y&quot;:&quot;220&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;690&quot;,&quot;y&quot;:&quot;220&quot;},&quot;as&quot;:&quot;points&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;YQXFDWCa&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;ZxCvrGZg&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0;entryY=0.5;entryDx=0;entryDy=0;exitX=1;exitY=0.5;exitDx=0;exitDy=0;&quot;,&quot;target&quot;:&quot;262uqCuq&quot;,&quot;value&quot;:&quot;&quot;},&quot;ZxCvrGZg&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;548&quot;,&quot;y&quot;:&quot;190&quot;},&quot;id&quot;:&quot;ZxCvrGZg&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rhombus;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;Meet the cloud storage requirements?&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;ahuuHps5&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;ahuuHps5&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;yiHdSYsJ&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;&quot;,&quot;target&quot;:&quot;EwYp4Z14&quot;},&quot;mb9fvfbw&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;400&quot;,&quot;y&quot;:&quot;605&quot;},&quot;id&quot;:&quot;mb9fvfbw&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;No&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;nWtSzh2o&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;nWtSzh2o&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;NJyEUmuV&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;yiHdSYsJ&quot;,&quot;value&quot;:&quot;&quot;},&quot;o674vDEO&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;350&quot;,&quot;y&quot;:&quot;390&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;o674vDEO&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;ose7jbE0&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;value&quot;:&quot;&quot;},&quot;ose7jbE0&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;150&quot;,&quot;y&quot;:&quot;360&quot;},&quot;id&quot;:&quot;ose7jbE0&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user uninstalls your app&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;pkktcdNB&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;350&quot;,&quot;y&quot;:&quot;360&quot;},&quot;id&quot;:&quot;pkktcdNB&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;Delete the local data while retaining the cloud backup data&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;q5VtsZ8k&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;680&quot;,&quot;y&quot;:&quot;200&quot;},&quot;id&quot;:&quot;q5VtsZ8k&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;Yes&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;yiHdSYsJ&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;350&quot;,&quot;y&quot;:&quot;530&quot;},&quot;id&quot;:&quot;yiHdSYsJ&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rhombus;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;Meet the cloud storage requirements?&quot;,&quot;vertex&quot;:&quot;1&quot;}}},&quot;diagramType&quot;:&quot;flowchart&quot;,&quot;lastEditTime&quot;:0}" />

### **For multiple devices**
If a PICO account is used on multiple devices, the data backup workflows and results on each device are as follows:

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3MjVweCIgaGVpZ2h0PSI2MjdweCIgdmlld0JveD0iLTAuNSAtMC41IDcyNSA2MjciPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEyMiA2MiBMIDE5NS42MyA2MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIwMC44OCA2MiBMIDE5My44OCA2NS41IEwgMTk1LjYzIDYyIEwgMTkzLjg4IDU4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIzMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNjJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIHVzZXIgZG93bmxvYWRzIHlvdXIgYXBwIGZvciB0aGUgZmlyc3QgdGltZSBvbiBkZXZpY2UgQTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1MTIgNjIgTCA1NDIgNjIgTCA1ODUuNjMgNjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1OTAuODggNjIgTCA1ODMuODggNjUuNSBMIDU4NS42MyA2MiBMIDU4My44OCA1OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjAyIiB5PSIzMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNjJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5UaGUgdXNlciB1c2VzIHlvdXIgYXBwPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1OTIiIHk9IjMyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA2MnB4OyBtYXJnaW4tbGVmdDogNTkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRhdGEgYmFja3VwIG9uIHRoZSBjbG91ZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTMyIiB5PSI0MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTJweDsgbWFyZ2luLWxlZnQ6IDU1MnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPlllczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA0NDcgOTIgTCA0NDcgMTEyIEwgMjYyIDExMiBMIDI2MiA5OC4zNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI2MiA5My4xMiBMIDI2NS41IDEwMC4xMiBMIDI2MiA5OC4zNyBMIDI1OC41IDEwMC4xMiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDQ3IDMyIEwgNTEyIDYyIEwgNDQ3IDkyIEwgMzgyIDYyIFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTI4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNjJweDsgbWFyZ2luLWxlZnQ6IDM4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5XaGV0aGVyIGNsb3VkIHN0b3JhZ2UgcmVxdWlyZW1lbnRzIGFyZSBtZXQ/PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDMyMiA2MiBMIDM3NS42MyA2MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM4MC44OCA2MiBMIDM3My44OCA2NS41IEwgMzc1LjYzIDYyIEwgMzczLjg4IDU4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzNDEiIHk9IjExMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiAzNjFweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5ObzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMjIgNTk0IEwgMTk1LjYzIDU5NCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIwMC44OCA1OTQgTCAxOTMuODggNTk3LjUgTCAxOTUuNjMgNTk0IEwgMTkzLjg4IDU5MC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iNTY0IiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1OTRweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIHVzZXIgdW5pbnN0YWxscyB5b3VyIGFwcCBvbiBkZXZpY2UgQTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjAyIiB5PSI1NjQiIHdpZHRoPSIyNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU5NHB4OyBtYXJnaW4tbGVmdDogMjAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkZvciBkZXZpY2UgQSwgdGhlIGxvY2FsIGRhdGEgd2lsbCBiZSBkZWxldGVkLiBGb3IgZGV2aWNlIEIsIGJvdGggdGhlIGxvY2FsIGRhdGEgYW5kIGNsb3VkIGJhY2t1cCBkYXRhIHdpbGwgYmUgcmV0YWluZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjEyIiB5PSIyIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMnB4OyBtYXJnaW4tbGVmdDogMzJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjE2cHgiPjxiPkRldmljZSBBOjwvYj48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMiIgeT0iMTYyIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNzJweDsgbWFyZ2luLWxlZnQ6IDMycHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PGZvbnQgc3R5bGU9ImZvbnQtc2l6ZToxNnB4Ij48Yj5EZXZpY2UgQjo8L2I+PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMjIgMjIyIEwgMTk1LjYzIDIyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIwMC44OCAyMjIgTCAxOTMuODggMjI1LjUgTCAxOTUuNjMgMjIyIEwgMTkzLjg4IDIxOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMTkyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMjJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIHVzZXIgZG93bmxvYWRzIHlvdXIgYXBwIG9uIGRldmljZSBCIGFuZCBsb2cgaW4gd2l0aCB0aGUgc2FtZSBQSUNPIGFjY291bnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzIyIDIyMiBMIDM5NS42MyAyMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDAuODggMjIyIEwgMzkzLjg4IDIyNS41IEwgMzk1LjYzIDIyMiBMIDM5My44OCAyMTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYyIDI1MiBMIDI2MiAzMDcgTCA1OTUuNjMgMzA3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjAwLjg4IDMwNyBMIDU5My44OCAzMTAuNSBMIDU5NS42MyAzMDcgTCA1OTMuODggMzAzLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDI2MiAxOTIgTCAzMjIgMjIyIEwgMjYyIDI1MiBMIDIwMiAyMjIgWiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMjJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5XaGV0aGVyIHRoZXJlIGlzIGNsb3VkIGJhY2t1cCBkYXRhPzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1MjIgMjIyIEwgNTk1LjYzIDIyMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDYwMC44OCAyMjIgTCA1OTMuODggMjI1LjUgTCA1OTUuNjMgMjIyIEwgNTkzLjg4IDIxOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNDAyIiB5PSIxOTIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyMnB4OyBtYXJnaW4tbGVmdDogNDAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlJlc3RvcmUgdGhlIGJhY2t1cCBkYXRhIG9uIGRldmljZSBCPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MDIiIHk9IjE5MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjIycHg7IG1hcmdpbi1sZWZ0OiA2MDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIHVzZXIgY2FuIGNvbnRpbnVlIGZyb20gdGhlIGZvcm1lciBwcm9ncmVzczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNjAyIiB5PSIyNzciIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMwN3B4OyBtYXJnaW4tbGVmdDogNjAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlRoZSB1c2VyIGhhcyB0byB1c2UgdGhlIGFwcCBmcm9tIHNjcmF0Y2g8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI1MiIgeT0iMjcyIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyODJweDsgbWFyZ2luLWxlZnQ6IDI3MnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPk5vPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzNDEiIHk9IjIwMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjEycHg7IG1hcmdpbi1sZWZ0OiAzNjFweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5ZZXM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjEyIiB5PSI1MzIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU0MnB4OyBtYXJnaW4tbGVmdDogMzJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjE2cHgiPjxiPkRldmljZSBBOjwvYj48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDMyMiA0MzIgTCAzNDIgNDMyIEwgMzgyIDQzMiBMIDM4MiA0MzAuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzODIgNDM1Ljg4IEwgMzc4LjUgNDI4Ljg4IEwgMzgyIDQzMC42MyBMIDM4NS41IDQyOC44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjQwMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDMycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlRoZSB1c2VyIHVzZXMgeW91ciBhcHAgb24gZGV2aWNlIEI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjM4MiIgeT0iMzkyIiB3aWR0aD0iMzQwIiBoZWlnaHQ9IjkwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0MzdweDsgbWFyZ2luLWxlZnQ6IDM4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EYXRhIGJhY2t1cCBvbiB0aGUgY2xvdWQ8YnIgLz48aT48Yj5Ob3RlPC9iPjwvaT46IFRoaXMgd2lsbCBvdmVyd3JpdGUgdGhlIGRhdGEgYmFja2VkIHVwIGZyb20gZGV2aWNlIEEuIEFmdGVyd2FyZHMsIGlmIHRoZSB1c2VyIHVzZXMgeW91ciBhcHAgYWdhaW4gb24gZGV2aWNlIEEgYW5kIGNsb3VkIGRhdGEgYmFja3VwIHJlcXVpcmVtZW50cyBhcmUgbWV0LCB0aGUgZGF0YSBiYWNrZWQgdXAgZnJvbSBkZXZpY2UgQSB3aWxsIG92ZXJ3cml0ZSB0aGUgZGF0YSBiYWNrZWQgdXAgZnJvbSBoZXJlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMzIiIHk9IjQxMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDIycHg7IG1hcmdpbi1sZWZ0OiAzNTJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5ZZXM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjU3IDQ2MiBMIDI1NyA0ODIgTCA2MiA0ODIgTCA2MiA0NjguMzciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2MiA0NjMuMTIgTCA2NS41IDQ3MC4xMiBMIDYyIDQ2OC4zNyBMIDU4LjUgNDcwLjEyIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyNTcgNDAyIEwgMzIyIDQzMiBMIDI1NyA0NjIgTCAxOTIgNDMyIFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTI4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDMycHg7IG1hcmdpbi1sZWZ0OiAxOTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+V2hldGhlciBjbG91ZCBzdG9yYWdlIHJlcXVpcmVtZW50cyBhcmUgbWV0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDEyMiA0MzIgTCAxODUuNjMgNDMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTkwLjg4IDQzMiBMIDE4My44OCA0MzUuNSBMIDE4NS42MyA0MzIgTCAxODMuODggNDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxNDIiIHk9IjQ4MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDkycHg7IG1hcmdpbi1sZWZ0OiAxNjJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5ObzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTIiIHk9IjM3MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzgycHg7IG1hcmdpbi1sZWZ0OiAzMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTZweCI+RGV2aWNlIEI6PC9mb250PjwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxCellList&quot;:[&quot;Xfazc13W&quot;,&quot;Pect1uf9&quot;,&quot;DtSidctE&quot;,&quot;NxSWLE9v&quot;,&quot;xlEKDaXv&quot;,&quot;nkfjkdPx&quot;,&quot;JSKrVLBb&quot;,&quot;4VJWwI4m&quot;,&quot;3TLUTdPW&quot;,&quot;uX6A3NzY&quot;,&quot;qpkDKwpw&quot;,&quot;CcKN9Koh&quot;,&quot;MjncI2hq&quot;,&quot;dffoIFZT&quot;,&quot;6gYi2w8d&quot;,&quot;KVuXsL8Q&quot;,&quot;EGWRAtqt&quot;,&quot;wXY3aK05&quot;,&quot;9eJXZ5xx&quot;,&quot;lYeMHHo5&quot;,&quot;ONmVK2o3&quot;,&quot;SX01mPPb&quot;,&quot;w4jbxgsC&quot;,&quot;payS4Zux&quot;,&quot;zS81qYRI&quot;,&quot;Ch804Tdf&quot;,&quot;Ux9YgJWP&quot;,&quot;eh81cT4c&quot;,&quot;NAGIiLr3&quot;,&quot;CQZ2gvxU&quot;,&quot;OSSaJDXv&quot;,&quot;hOCVGVho&quot;,&quot;X3RzBLrU&quot;,&quot;zf50xwY7&quot;,&quot;wqWIHwtf&quot;,&quot;4cN3qESf&quot;,&quot;4D1IBlob&quot;,&quot;PthRTVjR&quot;],&quot;mxGraphModel&quot;:{&quot;arrows&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;dx&quot;:&quot;782&quot;,&quot;dy&quot;:&quot;472&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageHeight&quot;:&quot;1169&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;tooltips&quot;:&quot;1&quot;},&quot;mxCellMap&quot;:{&quot;3TLUTdPW&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;3TLUTdPW&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;uX6A3NzY&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;&quot;,&quot;target&quot;:&quot;nkfjkdPx&quot;},&quot;4D1IBlob&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;180&quot;,&quot;y&quot;:&quot;630&quot;},&quot;id&quot;:&quot;4D1IBlob&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;No&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;4VJWwI4m&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;570&quot;,&quot;y&quot;:&quot;190&quot;},&quot;id&quot;:&quot;4VJWwI4m&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;Yes&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;4cN3qESf&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;160&quot;,&quot;y&quot;:&quot;580&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;430&quot;,&quot;y&quot;:&quot;580&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;4cN3qESf&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;OSSaJDXv&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;wqWIHwtf&quot;,&quot;value&quot;:&quot;&quot;},&quot;6gYi2w8d&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;240&quot;,&quot;x&quot;:&quot;240&quot;,&quot;y&quot;:&quot;712&quot;},&quot;id&quot;:&quot;6gYi2w8d&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;For device A, the local data will be deleted. For device B, both the local data and cloud backup data will be retained&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;9eJXZ5xx&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;340&quot;},&quot;id&quot;:&quot;9eJXZ5xx&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user downloads your app on device B and log in with the same PICO account&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;CQZ2gvxU&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;300&quot;,&quot;y&quot;:&quot;480&quot;},&quot;-1-Array&quot;:{&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;380&quot;,&quot;y&quot;:&quot;580&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;380&quot;,&quot;y&quot;:&quot;580&quot;},&quot;as&quot;:&quot;points&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;CQZ2gvxU&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;wqWIHwtf&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0;entryY=0.5;entryDx=0;entryDy=0;exitX=1;exitY=0.5;exitDx=0;exitDy=0;&quot;,&quot;target&quot;:&quot;hOCVGVho&quot;,&quot;value&quot;:&quot;&quot;},&quot;CcKN9Koh&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;379&quot;,&quot;y&quot;:&quot;260&quot;},&quot;id&quot;:&quot;CcKN9Koh&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;No&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;Ch804Tdf&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;640&quot;,&quot;y&quot;:&quot;425&quot;},&quot;id&quot;:&quot;Ch804Tdf&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user has to use the app from scratch&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;DtSidctE&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;DtSidctE&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;NxSWLE9v&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;nkfjkdPx&quot;,&quot;value&quot;:&quot;&quot;},&quot;EGWRAtqt&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;50&quot;,&quot;y&quot;:&quot;310&quot;},&quot;id&quot;:&quot;EGWRAtqt&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;<font style=\&quot;font-size: 16px;\&quot;><b>Device B:</b></font>&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;JSKrVLBb&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;630&quot;,&quot;y&quot;:&quot;180&quot;},&quot;id&quot;:&quot;JSKrVLBb&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;Data backup on the cloud&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;KVuXsL8Q&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;50&quot;,&quot;y&quot;:&quot;150&quot;},&quot;id&quot;:&quot;KVuXsL8Q&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;<font style=\&quot;font-size: 16px;\&quot;><b>Device A:</b></font>&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;MjncI2hq&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;240&quot;,&quot;y&quot;:&quot;742&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;MjncI2hq&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;dffoIFZT&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;value&quot;:&quot;&quot;},&quot;NAGIiLr3&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;50&quot;,&quot;y&quot;:&quot;680&quot;},&quot;id&quot;:&quot;NAGIiLr3&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;<font style=\&quot;font-size: 16px;\&quot;><b>Device A:</b></font>&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;NxSWLE9v&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;180&quot;},&quot;id&quot;:&quot;NxSWLE9v&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user downloads your app for the first time on device A&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;ONmVK2o3&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;ONmVK2o3&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;SX01mPPb&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;&quot;,&quot;target&quot;:&quot;Ch804Tdf&quot;},&quot;OSSaJDXv&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;550&quot;},&quot;id&quot;:&quot;OSSaJDXv&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user uses your app on device B&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;Pect1uf9&quot;:{&quot;id&quot;:&quot;Pect1uf9&quot;,&quot;parent&quot;:&quot;Xfazc13W&quot;},&quot;PthRTVjR&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;50&quot;,&quot;y&quot;:&quot;520&quot;},&quot;id&quot;:&quot;PthRTVjR&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;<b><font style=\&quot;font-size: 16px;\&quot;>Device B:</font></b>&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;SX01mPPb&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;240&quot;,&quot;y&quot;:&quot;340&quot;},&quot;id&quot;:&quot;SX01mPPb&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rhombus;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;Whether there is cloud backup data?&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;Ux9YgJWP&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;290&quot;,&quot;y&quot;:&quot;420&quot;},&quot;id&quot;:&quot;Ux9YgJWP&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;No&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;X3RzBLrU&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;370&quot;,&quot;y&quot;:&quot;560&quot;},&quot;id&quot;:&quot;X3RzBLrU&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;Yes&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;Xfazc13W&quot;:{&quot;id&quot;:&quot;Xfazc13W&quot;},&quot;dffoIFZT&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;712&quot;},&quot;id&quot;:&quot;dffoIFZT&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user uninstalls your app on device A&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;eh81cT4c&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;379&quot;,&quot;y&quot;:&quot;350&quot;},&quot;id&quot;:&quot;eh81cT4c&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;Yes&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;hOCVGVho&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;90&quot;,&quot;width&quot;:&quot;340&quot;,&quot;x&quot;:&quot;420&quot;,&quot;y&quot;:&quot;540&quot;},&quot;id&quot;:&quot;hOCVGVho&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;Data backup on the cloud<br /><i><b>Note</b></i>: This will overwrite the data backed up from device A. Afterwards, if the user uses your app again on device A and cloud data backup requirements are met, the data backed up from device A will overwrite the data backed up from here&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;lYeMHHo5&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;440&quot;,&quot;y&quot;:&quot;370&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;lYeMHHo5&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;SX01mPPb&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0;entryY=0.5;entryDx=0;entryDy=0;&quot;,&quot;target&quot;:&quot;payS4Zux&quot;,&quot;value&quot;:&quot;&quot;},&quot;nkfjkdPx&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;240&quot;,&quot;y&quot;:&quot;180&quot;},&quot;id&quot;:&quot;nkfjkdPx&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user uses your app&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;payS4Zux&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;440&quot;,&quot;y&quot;:&quot;340&quot;},&quot;id&quot;:&quot;payS4Zux&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;Restore the backup data on device B&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;qpkDKwpw&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;360&quot;,&quot;y&quot;:&quot;210&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;630&quot;,&quot;y&quot;:&quot;210&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;qpkDKwpw&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;nkfjkdPx&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;uX6A3NzY&quot;,&quot;value&quot;:&quot;&quot;},&quot;uX6A3NzY&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;130&quot;,&quot;x&quot;:&quot;420&quot;,&quot;y&quot;:&quot;180&quot;},&quot;id&quot;:&quot;uX6A3NzY&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rhombus;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;Whether cloud storage requirements are met?&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;w4jbxgsC&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;w4jbxgsC&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;payS4Zux&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;zS81qYRI&quot;,&quot;value&quot;:&quot;&quot;},&quot;wXY3aK05&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;wXY3aK05&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;9eJXZ5xx&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;SX01mPPb&quot;,&quot;value&quot;:&quot;&quot;},&quot;wqWIHwtf&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;130&quot;,&quot;x&quot;:&quot;230&quot;,&quot;y&quot;:&quot;550&quot;},&quot;id&quot;:&quot;wqWIHwtf&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rhombus;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;Whether cloud storage requirements are met&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;xlEKDaXv&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;500&quot;,&quot;y&quot;:&quot;110&quot;},&quot;-1-Array&quot;:{&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;580&quot;,&quot;y&quot;:&quot;210&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;580&quot;,&quot;y&quot;:&quot;210&quot;},&quot;as&quot;:&quot;points&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;xlEKDaXv&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;uX6A3NzY&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0;entryY=0.5;entryDx=0;entryDy=0;exitX=1;exitY=0.5;exitDx=0;exitDy=0;&quot;,&quot;target&quot;:&quot;JSKrVLBb&quot;,&quot;value&quot;:&quot;&quot;},&quot;zS81qYRI&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;640&quot;,&quot;y&quot;:&quot;340&quot;},&quot;id&quot;:&quot;zS81qYRI&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;fontFamily=Helvetica;fontSize=12;fontColor=#000000;align=center;strokeColor=#000000;fillColor=#ffffff;&quot;,&quot;value&quot;:&quot;The user can continue from the former progress&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;zf50xwY7&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;zf50xwY7&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;wqWIHwtf&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;&quot;,&quot;target&quot;:&quot;OSSaJDXv&quot;}}},&quot;diagramType&quot;:&quot;flowchart&quot;,&quot;lastEditTime&quot;:0}" />

## Expected effect
This section compares the data storage and recovery scenarios between the disabled and enabled states of the "Cloud Storage" feature.

* The name of the file is "ABCD".
* The name of the app package is "com.bytedance.newonline".
* The storage location of the file is "/data/data/com.bytedance.newonline/shared_prefs".

|  | **Cloud Storage Disabled** | **Cloud Storage Enabled** |
| --- | --- | --- |
| **Save Data** | The "ABCD" file appears under the directory after saving it. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/885051393cdd4382967de5dfaca68b86~tplv-goo7wpa0wc-image.image) | The "ABCD" file appears under the directory after saving it. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abd9b809f77a49fcba7a70636b1f5917~tplv-goo7wpa0wc-image.image) |
| **Restore Data** <br>  | After reinstalling the app, the "ABCD" file is no longer present in the directory.  <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf7a4f14298c4bceaee6369141d55181~tplv-goo7wpa0wc-image.image) | After reinstalling the app, when the user opens the app for the first time, a pop-up window will appear asking if the user wants to restore the app's data from the cloud. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca271520bb1849209e92524fd2425b18~tplv-goo7wpa0wc-image.image) <br> If the user chooses to restore the data, the prompt information you set in the code will appear. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cf7f8c86b924fbfa696bfb1d1a77d90~tplv-goo7wpa0wc-image.image) <br> Meanwhile, the corresponding file will be added to the directory. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e42938015aaf45b6a08abd24cf0d5a4f~tplv-goo7wpa0wc-image.image) |
## Key features
### Active data backup
PICO SDK of version 2.4.0 and later versions provide the `StartNewBackup` API for you to actively trigger data backups. When users achieve key progress (e.g., clearing a level) in your app, call this API to save the progress in time.
### Passive data backup
For devices and apps that meet the data backup requirements, an app's data on a specific device can then be backed up to the cloud. Keep your VR headset connected to the network during data backup; otherwise, the backup will fail. Once failed, no retry will take place until the next data backup is triggered.
**Trigger conditions & limitations**
Data backup will be triggered in certain circumstances. There are also some limitations that data backup has to satisfy. Below are detailed descriptions:
| **Trigger Conditions** | **Limitations** |
| --- | --- |
| Data backup will be triggered when the following conditions are met at the same time:  <br>  <br> * Cloud Storage service is enabled for an app on the PICO Developer Platform and users' VR headsets. <br> * The interval between one data backup and the next has exceeded 24 hours. <br> * The data in the files under the specified or custom data backup directories has changed. <br> * The app has exited. | There are two main limitations: <br>  <br> * A user can back up **no more than** 100 MiB data for each app. Backup will fail if the data size exceeds the limit. <br> * Data backups are associated with users' PICO accounts. One user can only have one data backup for each app. |
**Directories for data backup**
The system will back up data from the following directories.
Any file type is accepted but with a 100MB size limit.

| **Directory** | **Relevant API** |
| --- | --- |
| /data/data/{packagename}/files | [android.content.Context#getFilesDir](https://developer.android.com/reference/android/content/Context#getFilesDir()) |
| /data/data/{packagename}/databases | [android.content.Context#getDatabasePath](https://developer.android.com/reference/android/content/Context#getDatabasePath(java.lang.String)) |
| /data/data/{packagename}/shared_prefs | [android.content.Context#getDataDir](https://developer.android.com/reference/android/content/Context#getDataDir()) |
| /storage/emulated/0/Android/data/{packagename}/files | [android.content.Context#getExternalFilesDir](https://developer.android.com/reference/android/content/Context#getExternalFilesDir(java.lang.String)) |
If you would like to back up data from **custom directories** , pay attention to the following:

* You can create sub-directories under the above-mentioned specified directories to back up data from. The system will ONLY back up data from the specified directories or the custom directories under them.
* Due to data size limitations, it is recommended NOT to place DLC files under the directories for data backup, to avoid potential backup failures caused by oversized data and unnecessary backups and restores.

**Update data backups**
Data backups can be updated. Below are relevant notes:

* The cloud only stores the latest backup. Once a new backup is uploaded, the older one will be deleted.
* For a single app, if a PICO account has generated app data on multiple devices, the cloud only stores the data from the last device that performs data backup.
* Backups will be uploaded and updated only when apps' data has changed.

### Data recovery
For an app with data backups, data recovery will be triggered when one of the following conditions is met:

* The user re-installs the same app and launches it for the first time on the same device.
* The user installs and launches the same app for the first time on another device.

Pay attention to the following:

* If you or any of your users disable Cloud Storage service, your app's data is then unable to be restored from backups.
* Data recovery takes place **asynchronously** when an app launches, which essentially will not affect app operation.
* Users will get notified of the recovery progress by a popup. The popup disappears once data recovery is complete. If data recovery fails, users will also get notified by another popup.
* Users should keep their VR headsets connected to the network during data recovery; otherwise, the recovery will fail.
* If data recovery fails, users can click on the popup for a retry, or they can click to cancel data recovery and re-launch the app.

### Data deletion
When a user closes their account, all of their cloud data backups will be automatically deleted by the server.
### Security measures
To secure data backups, all data will be encrypted and go through a data digest check. Therefore, when backing up data to the cloud, the system will encrypt data and calculate a digest. When restoring data backup to a device, the system first pulls the data backup from the cloud, decrypts it, and then checks the digest. Once the data backup is successfully decrypted and passes the digest check, it can be restored.
## Procedure
### Step 1: Enable the Cloud Storage service
You can go to the PICO Developer Platform to enable Cloud Storage service for your app. Below are the steps to follow:

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/organization/).
2. From the left navigation pane, select **My Apps**.
   This directs you to the **My Apps** screen.
3. Click on the target app.
   This directs you to the app's **Overview** screen.
4. From the left navigation pane, select **Platform Services** > **Cloud Storage**.
5. Click **Enable**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/77d041a2cb144f688bf3fd010f38737d~tplv-em5hxbkur4-noop.image?width=1971&height=998)

### Step 2: Implement the Cloud Storage service
Call Cloud Storage APIs to implement this service in your app. For the API list and API details, refer to the [API reference](/reference/unity/latest/CloudStorageService/).
Below is the code sample:
```C#
using System;
using UnityEngine;
using UnityEngine.UI;

namespace Pico.Platform.Samples.Game
{
    public class CloudStorageSample : MonoBehaviour
    {
        public Text showText; // Text component used to display information to the user
        public Text debugText; // Text component used to display debug information
        // This method is called when the user wants to start a new backup
        public void StartNewBackup()
        {
            string debugMsg= "";
            debugMsg += "\nStartNewBackup Start";

            CloudStorageService.StartNewBackup().OnComplete(msg =>
            {
                if (msg.IsError)
                {
                    debugMsg += "\nStartNewBackup IsError, ErrorMessage:" + msg.Error.Message + " ErrorCode:" + msg.Error.Code;
                }
                else
                {
                    debugMsg = "\nStartNewBackup Successfully";
                }

                Debug.Log(debugMsg);
                debugText.text = debugMsg;
            });

            Debug.Log(debugMsg);
            debugText.text = debugMsg;
        }
        // This method is used to store a string value in the PlayerPrefs
        public void SetString(string KeyName, string Value)
        {
            PlayerPrefs.SetString(KeyName, Value);
        }

        // This method is used to retrieve a string value from the PlayerPrefs
        public string GetString(string KeyName)
        {
            return PlayerPrefs.GetString(KeyName);
        }
        // This method is called to save data (test value) to the PlayerPrefs
        public void savedata()
        {
            SetString("test", "ABCD");
        }

        private void Update()
        {
            // Retrieve the saved string value from the PlayerPrefs
            string showMsg = GetString("test");
            // Update the showText UI element with the retrieved string value or a default message if no value is found
            // Note: You can edit the text given below
            showText.text = "Retrieved the following data："+ (string.IsNullOrEmpty(showMsg) ? "No data" : showMsg);
        }
    }
}
```


# --- END: Cloud storage.md ---



# --- BEGIN: Compatibility & porting guide for MR features.md ---

This article introduces the compatibility of mixed reality features of different SDK versions on PICO 4 and PICO 4 Ultra devices. You can follow the porting guide to upgrade mixed reality APIs from 2.5.0 or earlier versions to 3.0.0 for your app.
## Important note
SDK version 3.0.0 does not involve the refactoring of video seethrough, so it is not mentioned in this article.
## Compatibility notice
The following outlines the support for the MR (Mixed Reality) APIs in SDK version 2.5.0 or earlier, and version 3.0.0, for the PICO 4 and PICO 4 Ultra devices.
| **SDK Version** | **PICO 4** | **PICO 4 Ultra** |
| --- | --- | --- |
| 2.5.0 or earlier | Support all | Not support |
| 3.0.0 | Only support Spatial Anchor (excluding Shared Spatial Anchor) and Scene Capture APIs | Support all |
## Port the Spatial Anchor feature
Below is the porting guide for the Spatial Anchor feature. For more instructions on how to implement this feature in your app, refer to the following articles:

* 2.5.0 or earlier versions: [Spatial Anchor guide](/document/unity/spatial-anchors/?v=2.5.0), [API reference](/reference/unity/client-api/PXR_MixedReality/?v=2.5.0).
* 3.0.0: [Saptial Anchor guide](/document/unity/spatial-anchors/?v=3.0.0), [API reference](/reference/unity/client-api/PXR_MixedReality/?v=3.0.0).

### Enable the feature
| **2.5.0 or earlier versions** | **3.0.0** |
| --- | --- |
| On the **PXR_Manager (Script)** panel, check the **Anchor** checkbox. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a4df793e6e2442d830dea28aaff13ab~tplv-goo7wpa0wc-image.image) | On the **PXR_Manager (Script)** panel, check the **Spatial Anchor** checkbox. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f7fffdb4dbe461a9adf09b4827e5ef0~tplv-goo7wpa0wc-image.image) |
### API list
| **Operation** | **2.5.0 or earlier versions** | **3.0.0** |
| --- | --- | --- |
| Start/stop the Spatial Anchor feature | None <br>  | Before calling other APIs, call `StartSenseDataProvider` to start the Spatial Anchor feature. When everything is done, call `StopSenseDataProvider` to stop the Spatial Anchor feature. |
| Create a spatial anchor | 1. Call ` CreateAnchorEntity`. <br> 2. Listen for the `AnchorEntityCreated` event. | `CreateSpatialAnchorAsync` <br>  |
| Destroy a spatial anchor in the app's memory | `DestroyAnchorEntity` | `DestroyAnchor` |
| Save a spatial anchor to the device's local storage | 1. Call `PersistAnchorEntity`。 <br> 2. Listen for the `AnchorEntityPersisted` event. | `PersistSpatialAnchorAsync` |
| Delete a spatial anchor in the device's local storage | 1. Call `UnPersistAnchorEntity`. <br> 2. Listen for the `AnchorEntityUnPersisted` event. | `UnPersistSpatialAnchorAsync` |
| Load spatial anchors | 1. Call `LoadAnchorEntityByUuidFilter`. <br> 2. Listen for the `AnchorEntityLoaded` event. <br> 3. Call `GetAnchorEntityLoadResults`. | `QuerySpatialAnchorAsync` |
| Get the UUID of a spatial anchor | `GetAnchorEntityUuid` | `GetAnchorUuid` |
| Get the pose of a spatial anchor | `GetAnchorPose` | `LocateAnchor` |
## Port the Scene Capture feature
Below is the porting guide for the Scene Capture feature. For more instructions on how to implement this feature in your app, refer to the following articles:

* 2.5.0 or earlier versions: [Scene Capture guide](/document/unity/space-calibration/?v=2.5.0), [API reference](/reference/unity/client-api/PXR_MixedReality/?v=2.5.0).
* 3.0.0: [Scene Capture guide](/document/unity/scene-capture/?v=3.0.0), [API reference](/reference/unity/client-api/PXR_MixedReality/?v=3.0.0).

### Enable the feature
| **2.5.0 or earlier versions** | **3.0.0** |
| --- | --- |
| None | On the **PXR_Manager (Script)** panel, check the **Scene Capture** checkbox. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c528712a214b4d5188b75fbed8690b6c~tplv-goo7wpa0wc-image.image) |
### API list
| **Operation** | **2.5.0 or earlier versions** | **3.0.0** |
| --- | --- | --- |
| Start/stop the Scene Capture feature | None | Before calling other APIs, call `StartSenseDataProvider` to start the Scene Capture feature. <br> When everything is done, call `StopSenseDataProvider` to stop the Scene Capture feature. |
| Launch the Room Capture app | 1. Call `StartSpatialSceneCapture`. <br> 2. Listen for the `SpatialSceneCaptured` event. | `StartSceneCaptureAsync` |
| Load scene anchors | 1. Call `LoadAnchorEntityBySceneFilter`. <br> 2. Listen for the `AnchorEntityLoaded` event. <br> 3. Call `GetAnchorEntityLoadResults`. | `QuerySceneAnchorAsync` <br>  |
| Get the semantic label of a scene anchor | `GetAnchorSceneLabel` | `GetSceneSemanticLabel` |
| Get the component of a scene anchor | `GetAnchorComponentFlags` | `GetSceneAnchorComponentTypes` |
| Get the Box3D data of a scene anchor | `GetAnchorVolumeInfo` | `GetSceneBox3DData` |
| Get the Box2D data of a scene anchor | `GetAnchorPlaneBoundaryInfo` | `GetSceneBox2DData` |
| Get the polygon data of a scene anchor | `GetAnchorPlanePolygonInfo` | `GetScenePolygonData` |
| Get the UUID of a scene anchor | `GetAnchorEntityUuid` | `GetAnchorUuid` |
| Get the pose of a scene anchor | `GetAnchorPose` | `LocateAnchor` |


# --- END: Compatibility & porting guide for MR features.md ---



# --- BEGIN: Content Protection.md ---

After enabling content protection for your app, the screen color becomes black when users are trying to make screenshots or record videos in your app.
## Enable content protection

1. In the Unity Editor, open an existing scene or create a new one.
2. Add **XR Origin** to the scene. If there is already one, skip this step.
   If you have not upgraded the XR Interaction Toolkit to the latest version, the object name will be XR Rig. Refer to the [Quickstart](/13136/en_create-an-xr-scene#782faf9d) guide for how to upgrade the XR Interaction Toolkit.
3. Select **XR Origin** and add the **PXR_Manager** script to it.
4. Check **Use Content Protect**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/440dd4fd187f4b12ae566881d283f866~tplv-goo7wpa0wc-image.image)
   Content protection is enabled for your app.

## Known issue
Using [application spacewarp](/13136/en_application-spacewarp) and content protection together will cause screen jitter and screen ghosting.


# --- END: Content Protection.md ---



# --- BEGIN: Convert and profile models for SecureMR.md ---

This article is a step-by-step guide on how to convert and profile your models for SecureMR.
## Install Docker Desktop
### Windows

1. Enable wsl2 on Windows. For more information, refer to [this page](https://learn.microsoft.com/en-us/windows/wsl/install). 
2. Install terminal on Windows. For more information, refer to [this page](https://github.com/microsoft/terminal?tab=readme-ov-file#microsoft-store-recommended). 
3. Install docker on Windows. For more information, refer to [this page](https://docs.docker.com/desktop/setup/install/windows-install/). 
4. Run Docker Desktop.
5. Enable wsl2 in docker.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09625756d6644e51bdcce09b326178ee~tplv-goo7wpa0wc-image.image" width="1907px" />   

### macOS

1. Install Docker Desktop. You can install Docker Desktop from [this page](https://docs.docker.com/desktop/setup/install/mac-install/).
2. Run Docker Desktop.

### Linux

1. Install docker on Linux. For more information, refer to [this page](https://docs.docker.com/desktop/setup/install/linux/). 
2. Run Docker Desktop.

## Get the to-be-converted model 

1. Download the following SecureMRTools package and unzip it. This package includes the convert_model.sh script.
   <a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89ca95d8a965447c8762cc5a63b818f5~tplv-goo7wpa0wc-image.image" filename="SecureMRTools.zip" download>SecureMRTools.zip</a>
2. Move /pth/tflite/onnx model to the same directory where the convert_model.sh script is placed.

## Convert the model to context binary

1. Run convert script to generate qnn context binary.
   * Convert pth model:
      ```C++
      ./convert_model.sh --input /path/to/pth_model
      ```

   * Convert tflite model: 
      ```C++
      ./convert_model.sh --input /path/to/tilte_model
      ```

   * Convert onnx model: 
      ```C++
      ./convert_model.sh --input /path/to/onnx_model    
      ```

   * (Optional) Convert model with custom_io:
      Qnn supports custom_io to specify the input/output layouts when converting the model. The conversion script also integrates that functionality. For more information, refer to [this page](https://docs.qualcomm.com/bundle/publicresource/topics/80-63442-50/converters.html).

      ```C++
      ./convert_model.sh --input /path/to/onnx_model --custom_io /path/to/custmo_io.yaml
      ```

      Below is a sample custmo_io.yml: 
      ```YAML
      IOName: images
        Layout:
          Model: NCHW
          Custom: NHWC
      - IOName: output0
        Layout:
          Model: NFC
          Custom: NCF
      ```

## Profile model inference

1. Enable the "Developer" mode on your PICO device and connect it to PC. For detailed instructions, refer to [this page](/document/unity/pdc-basic-info/).
2. Run the docker environment.
   ```C++
   ./run_docker_container.sh
   ```

3. Profile the model inference.
   ```C++
   ./profile_model.sh -m /path/to/model.serialized.bin -i 000000.raw 
   ```

   You'll get the log from qnn-net-run for basic profiling information as shown below:
   ```SQL
   Execute Stats (Average): 
   ------------------------ 
   Total Inference Time:  
   --------------------- 
   Graph 0 (yolo11n): 
       NetRun: 20828 us 
       Backend (Number of HVX threads used): 4 count 
       Backend (RPC (execute) time): 18906 us 
       Backend (QNN accelerator (execute) time): 18378 us 
       Backend (Accelerator (execute) time): 18126 us 
       Backend (Accelerator (execute excluding wait) time): 17927 us 
       Backend (QNN (execute) time): 20417 us 
    
   Execute Stats (Min): 
   ------------------------ 
   Total Inference Time:  
   --------------------- 
   Graph 0 (yolo11n): 
       NetRun: 19288 us 
       Backend (Number of HVX threads used): 4 count 
       Backend (RPC (execute) time): 18599 us 
       Backend (QNN accelerator (execute) time): 18142 us 
       Backend (Accelerator (execute) time): 17879 us 
       Backend (Accelerator (execute excluding wait) time): 17772 us 
       Backend (QNN (execute) time): 19067 us 
    
   Execute Stats (Max): 
   ------------------------ 
   Total Inference Time:  
   --------------------- 
   Graph 0 (yolo11n): 
       NetRun: 26170 us 
       Backend (Number of HVX threads used): 4 count 
       Backend (RPC (execute) time): 20134 us 
       Backend (QNN accelerator (execute) time): 19374 us 
       Backend (Accelerator (execute) time): 19178 us 
       Backend (Accelerator (execute excluding wait) time): 18236 us 
       Backend (QNN (execute) time): 25944 us 
   ```


# --- END: Convert and profile models for SecureMR.md ---



# --- BEGIN: Create a QNN model to run algorithms.md ---

This article presents a method for using QNN model inference to run algorithms that are either unsupported by existing SecureMR operators or too complex to implement using native SecureMR pipeline components. In these cases, you can design and train models using familiar frameworks such as PyTorch, TensorFlow, or ONNX, export them into a supported format, and convert them into QNN context binaries using the QNN model conversion tools. These binaries can then be executed in SecureMR using the RunModelInference operator.
## Workflow

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI4NjVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgODY1IDY1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAxMjIgMzIgTCAxNTUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNjAuODggMzIgTCAxNTMuODggMzUuNSBMIDE1NS42MyAzMiBMIDE1My44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZWJmMGZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BbGdvcml0aG08L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDEyIDMyIEwgNDQ1LjYzIDMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDUwLjg4IDMyIEwgNDQzLjg4IDM1LjUgTCA0NDUuNjMgMzIgTCA0NDMuODggMjguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjE2MiIgeT0iMiIgd2lkdGg9IjI1MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZWJmMGZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkltcGxlbWVudCB3aXJoIFB5dG9yY2gvVGVuc29yZmxvdy9PTk5YwqA8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNjAyIDMyIEwgNjM1LjYzIDMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjQwLjg4IDMyIEwgNjMzLjg4IDM1LjUgTCA2MzUuNjMgMzIgTCA2MzMuODggMjguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQ1MiIgeT0iMiIgd2lkdGg9IjE1MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZWJmMGZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogNDUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNvbnZlcnQgdG8gUU5OLmJpbjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNjQyIiB5PSIyIiB3aWR0aD0iMjIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNlYmYwZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiA2NDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+SW50ZWdyYXRlIHdpdGjCoDxzcGFuIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWwiPlJ1bk1vZGVsSW5mZXJlbmNlIG9wZXJhdG9yPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxGraphModel&quot;:{&quot;dx&quot;:&quot;1422&quot;,&quot;dy&quot;:&quot;816&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;tooltips&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;arrows&quot;:&quot;1&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;pageHeight&quot;:&quot;1169&quot;},&quot;mxCellMap&quot;:{&quot;k9Udm6hN&quot;:{&quot;id&quot;:&quot;k9Udm6hN&quot;},&quot;qDveaxSn&quot;:{&quot;id&quot;:&quot;qDveaxSn&quot;,&quot;parent&quot;:&quot;k9Udm6hN&quot;},&quot;Dgeb67Jl&quot;:{&quot;id&quot;:&quot;Dgeb67Jl&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;qDveaxSn&quot;,&quot;source&quot;:&quot;nTTmUGl4&quot;,&quot;target&quot;:&quot;9Uan4rHI&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;nTTmUGl4&quot;:{&quot;id&quot;:&quot;nTTmUGl4&quot;,&quot;value&quot;:&quot;Algorithm&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#EBF0FF;&quot;,&quot;parent&quot;:&quot;qDveaxSn&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;60&quot;,&quot;y&quot;:&quot;140&quot;,&quot;width&quot;:&quot;120&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;gJGshnBE&quot;:{&quot;id&quot;:&quot;gJGshnBE&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;qDveaxSn&quot;,&quot;source&quot;:&quot;9Uan4rHI&quot;,&quot;target&quot;:&quot;rY01nSEF&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;9Uan4rHI&quot;:{&quot;id&quot;:&quot;9Uan4rHI&quot;,&quot;value&quot;:&quot;Implement wirh Pytorch/Tensorflow/ONNX &quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#EBF0FF;&quot;,&quot;parent&quot;:&quot;qDveaxSn&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;220&quot;,&quot;y&quot;:&quot;140&quot;,&quot;width&quot;:&quot;250&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;eDxuWjcp&quot;:{&quot;id&quot;:&quot;eDxuWjcp&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;qDveaxSn&quot;,&quot;source&quot;:&quot;rY01nSEF&quot;,&quot;target&quot;:&quot;S9EdLulF&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;rY01nSEF&quot;:{&quot;id&quot;:&quot;rY01nSEF&quot;,&quot;value&quot;:&quot;Convert to QNN.bin&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#EBF0FF;&quot;,&quot;parent&quot;:&quot;qDveaxSn&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;510&quot;,&quot;y&quot;:&quot;140&quot;,&quot;width&quot;:&quot;150&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;S9EdLulF&quot;:{&quot;id&quot;:&quot;S9EdLulF&quot;,&quot;value&quot;:&quot;Integrate with RunModelInference operator&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#EBF0FF;&quot;,&quot;parent&quot;:&quot;qDveaxSn&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;700&quot;,&quot;y&quot;:&quot;140&quot;,&quot;width&quot;:&quot;220&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}}},&quot;mxCellList&quot;:[&quot;k9Udm6hN&quot;,&quot;qDveaxSn&quot;,&quot;Dgeb67Jl&quot;,&quot;nTTmUGl4&quot;,&quot;gJGshnBE&quot;,&quot;9Uan4rHI&quot;,&quot;eDxuWjcp&quot;,&quot;rY01nSEF&quot;,&quot;S9EdLulF&quot;]},&quot;lastEditTime&quot;:0,&quot;snapshot&quot;:&quot;&quot;}" />

## Example
Algorithm Description: Calculate Rotation Vector from v1 to v2.
This algorithm computes the axis-angle representation (also known as the rotation vector) that represents the 3D rotation needed to rotate vector v1 into vector v2.
```Python
def calculate_rotation_vector(v1, v2):
    # Normalize the input vectors
    v1 = v1 / np.linalg.norm(v1)
    v2 = v2 / np.linalg.norm(v2)
    # Compute the cross product to find the rotation axis
    r = np.cross(v1, v2)
    # Compute the dot product to find the angle
    cos_theta = np.dot(v1, v2)
    theta = np.arccos(np.clip(cos_theta, -1.0, 1.0))  # Clip to handle numerical errors
    # Normalize the rotation axis
    if np.linalg.norm(r) > 0:  # Avoid division by zero
        r = r / np.linalg.norm(r)
    # Scale the rotation axis by the angle
    rotation_vector = theta * r
    return
```

ONNX model:
```Python
import numpy as np
import onnx
from onnx import helper
from onnx import TensorProto

def create_rotation_vector_model():
    # Create input tensors for two 3D vectors
    v1 = helper.make_tensor_value_info('v1', TensorProto.FLOAT, [1, 3])
    v2 = helper.make_tensor_value_info('v2', TensorProto.FLOAT, [1, 3])

    # Calculate norms of vectors
    v1_norm = helper.make_node('ReduceL2', inputs=['v1'], outputs=['v1_norm'], keepdims=0)
    v2_norm = helper.make_node('ReduceL2', inputs=['v2'], outputs=['v2_norm'], keepdims=0)

    # Normalize vectors
    v1_normalized = helper.make_node('Div', inputs=['v1', 'v1_norm'], outputs=['v1_normalized'])
    v2_normalized = helper.make_node('Div', inputs=['v2', 'v2_norm'], outputs=['v2_normalized'])

    # Split normalized vectors into components
    v1_split = helper.make_node('Split', inputs=['v1_normalized'], outputs=['v1_x', 'v1_y', 'v1_z'], axis=1)
    v2_split = helper.make_node('Split', inputs=['v2_normalized'], outputs=['v2_x', 'v2_y', 'v2_z'], axis=1)

    # Calculate cross product components manually
    # x = v1.y * v2.z - v1.z * v2.y
    cross_x_1 = helper.make_node('Mul', inputs=['v1_y', 'v2_z'], outputs=['temp_x_1'])
    cross_x_2 = helper.make_node('Mul', inputs=['v1_z', 'v2_y'], outputs=['temp_x_2'])
    cross_x = helper.make_node('Sub', inputs=['temp_x_1', 'temp_x_2'], outputs=['cross_x'])

    # y = v1.z * v2.x - v1.x * v2.z
    cross_y_1 = helper.make_node('Mul', inputs=['v1_z', 'v2_x'], outputs=['temp_y_1'])
    cross_y_2 = helper.make_node('Mul', inputs=['v1_x', 'v2_z'], outputs=['temp_y_2'])
    cross_y = helper.make_node('Sub', inputs=['temp_y_1', 'temp_y_2'], outputs=['cross_y'])

    # z = v1.x * v2.y - v1.y * v2.x
    cross_z_1 = helper.make_node('Mul', inputs=['v1_x', 'v2_y'], outputs=['temp_z_1'])
    cross_z_2 = helper.make_node('Mul', inputs=['v1_y', 'v2_x'], outputs=['temp_z_2'])
    cross_z = helper.make_node('Sub', inputs=['temp_z_1', 'temp_z_2'], outputs=['cross_z'])

    # Concatenate cross product components
    rotation_axis = helper.make_node('Concat', inputs=['cross_x', 'cross_y', 'cross_z'], outputs=['rotation_axis'], axis=0)

    # Create shape tensors for reshaping
    reshape_shape = helper.make_tensor('reshape_shape', TensorProto.INT64, [2], [1, 3])
    # Change dot_shape to explicitly specify scalar shape [1]
    dot_shape = helper.make_tensor('dot_shape', TensorProto.INT64, [1], [1])
    
    # Reshape normalized vectors for MatMul
    v1_reshape = helper.make_node('Reshape', inputs=['v1_normalized', 'reshape_shape'], outputs=['v1_reshaped'])
    v2_reshape = helper.make_node('Reshape', inputs=['v2_normalized', 'reshape_shape'], outputs=['v2_reshaped'])
    
    # Transpose v2 for dot product
    v2_transpose = helper.make_node('Transpose', inputs=['v2_reshaped'], outputs=['v2_transposed'])
    
    # Compute dot product with proper dimensions
    dot_product = helper.make_node('MatMul', inputs=['v1_reshaped', 'v2_transposed'], outputs=['dot_product_2d'])
    
    # Reshape dot product to scalar (shape [1])
    dot_reshape = helper.make_node('Reshape', inputs=['dot_product_2d', 'dot_shape'], outputs=['dot_product'])

    # Clip dot product to [-1, 1] (using opset 11)
    clipped_dot = helper.make_node('Clip', inputs=['dot_product'], outputs=['clipped_dot'], 
                                 min=-1.0, max=1.0)  # Using attribute-based clip for older opset

    # Approximate acos using piece-wise linear interpolation
    # We'll use: acos(x) ≈ π/2 - x - x³/6 for x in [-1, 1]
    
    # Constants for approximation
    pi_half = helper.make_tensor('pi_half', TensorProto.FLOAT, [], [1.5707963267948966])
    one_sixth = helper.make_tensor('one_sixth', TensorProto.FLOAT, [], [0.16666667])
    
    # Calculate x³
    x_squared = helper.make_node('Mul', inputs=['clipped_dot', 'clipped_dot'], outputs=['x_squared'])
    x_cubed = helper.make_node('Mul', inputs=['x_squared', 'clipped_dot'], outputs=['x_cubed'])
    
    # Calculate x³/6
    x_cubed_div_6 = helper.make_node('Mul', inputs=['x_cubed', 'one_sixth'], outputs=['x_cubed_div_6'])
    
    # Calculate π/2 - x
    minus_x = helper.make_node('Sub', inputs=['pi_half', 'clipped_dot'], outputs=['minus_x'])
    
    # Final approximation: π/2 - x - x³/6
    theta = helper.make_node('Sub', inputs=['minus_x', 'x_cubed_div_6'], outputs=['theta'])

    # Calculate norm of rotation axis
    axis_norm = helper.make_node('ReduceL2', inputs=['rotation_axis'], outputs=['axis_norm'], keepdims=0)

    # Normalize rotation axis
    normalized_axis = helper.make_node('Div', inputs=['rotation_axis', 'axis_norm'], outputs=['normalized_axis'])

    # Scale rotation axis by angle
    rotation_vector = helper.make_node('Mul', inputs=['normalized_axis', 'theta'], outputs=['rotation_vector'])

    # Create graph outputs
    output = helper.make_tensor_value_info('rotation_vector', TensorProto.FLOAT, [3])

    # Create the graph
    graph = helper.make_graph(
        [v1_norm, v2_norm, v1_normalized, v2_normalized,
         v1_split, v2_split,
         cross_x_1, cross_x_2, cross_x,
         cross_y_1, cross_y_2, cross_y,
         cross_z_1, cross_z_2, cross_z,
         rotation_axis, v1_reshape, v2_reshape, v2_transpose, dot_product, dot_reshape,
         clipped_dot, x_squared, x_cubed, x_cubed_div_6, minus_x, theta,
         axis_norm, normalized_axis, rotation_vector],
        'rotation_vector_calculation',
        [v1, v2],
        [output],
        [reshape_shape, dot_shape, pi_half, one_sixth]
    )

    # Create the model with opset 11
    model = helper.make_model(graph)
    model.opset_import[0].version = 11

    # Save the model
    onnx.save(model, 'rotation_vector_model.onnx')

if __name__ == '__main__':
    create_rotation_vector_model()
```

<a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37998040c55742e68012ed3a5e26a5c0~tplv-goo7wpa0wc-image.image" filename="rotation_vector_model.onnx" download>rotation_vector_model.onnx</a>
QNN model (context binary):
```JSON
{
    "model_name": "rotation_vector_model",
    "path_to_zoo": "rotation_vector_model.serialized.bin",
    "engine_type": "qnn",
    "input": [
        {
            "name": "v1",
            "shape": [
                1,
                3
            ],
            "encoding_type": "FP32",
            "alias_name": "v1"
        },
        {
            "name": "v2",
            "shape": [
                1,
                3
            ],
            "encoding_type": "FP32",
            "alias_name": "v2"
        }
    ],
    "output": [
        {
            "name": "rotation_vector",
            "shape": [
                3,
                1
            ],
            "encoding_type": "FP32",
            "alias_name": "rotation_vector"
        }
    ],
    "specific_config": {
        "runtime_order": [
            "HTP_FIXED8_TF"
        ],
        "enable_dynamic_runtime": false
    }
} 
```

<a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f320982f341743ccae6cbfaaf7368be8~tplv-goo7wpa0wc-image.image" filename="rotation_vector_model.serialized.bin" download>rotation_vector_model.serialized.bin</a>


# --- END: Create a QNN model to run algorithms.md ---



# --- BEGIN: Create example hand poses.md ---

This article walks you through how to create the "ThumbUp" and "Okay" poses using the hand pose generator and hand pose event trigger. Before you begin, it is recommended to read the following articles to learn hand tracking and the scripts you use to create hand pose and hand pose events: "[Hand tracking guides](/13136/en_hand-tracking)", "[PXR_Hand Pose Generator script](/13136/en_about-the-pxr-hand-pose-generator-script)", "[PXR_Hand Pose script](/13136/en_about-the-pxr-hand-pose-script)".
## “ThumbUp” pose
### Characteristics

* The thumb points upwards.
* The other four fingers are in the shape of flexion and curl.

### Visualization
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e93a47d892bc4049b0e85c42b6df92fc~tplv-goo7wpa0wc-image.image" width="400px" />

### Create the "ThumbUp" pose

1. Add the **HandPoseGenerator** prefab to the current scene.
2. On the **PXR_Hand Pose Generator (Script)** pane, click **New** to create a new Hand Pose Config file, which stores the hand pose configuration.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f9f63e62b83475ba71a7b3c9fed7852~tplv-goo7wpa0wc-image.image)
3. (Optional) Rename the hand pose configuration file. It is recommended to add the keyword "ThumbUp" for easier searching.
4. Use the **Shapes** component to set up finger shapes. The following settings are for your reference:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89aae3dd6769476998a258935f2f1bca~tplv-goo7wpa0wc-image.image)
5. Use the **Transform** component to configure the orientation of the hand. The following settings are for your reference:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4803daa9b8584f1a83e99cf9746f0014~tplv-goo7wpa0wc-image.image)
6. Add the **PXR_Hand Pose** script to the prefab.
7. Use **PXR_Hand Pose (script)** to set up hand pose events:
   1. In the **Track Type** field, select the hand that the "ThumbUp" pose is applied to. 
   2. In the **Config** field, add the Hand Pose Config file generated for the "ThumbUp" pose.
   3. Add functions for triggering **Hand Pose Start**, **Hand Pose Update**, and **Hand Pose End** events.
8. Build and run the project on your PICO device to try the hand pose and hand pose event you just created, and carry out debugging if necessary.

## “Okay” pose
### **Characteristics**

* The thumb and index finger curl.
* The tips of the thumb and index finger pinch.
* The middle, ring, and little finger are not fully extended or opened.

### Visualization
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c79ebab1dd540bd86716668952f9cde~tplv-goo7wpa0wc-image.image" width="400px" />

### Create the "Okay" pose

1. Add the **HandPoseGenerator** prefab to the current scene.
2. On the **PXR_Hand Pose Generator (Script)** pane, click **New** to create a new Hand Pose Config file, which stores the hand pose configuration.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f9f63e62b83475ba71a7b3c9fed7852~tplv-goo7wpa0wc-image.image)
3. (Optional) Rename the hand pose configuration file. It is recommended to add the keyword "Okay" for easier searching.
4. Use the **Shapes** component to set up finger shapes. The following settings are for your reference:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ae717d914de4dc0b6b950f842b86d9f~tplv-goo7wpa0wc-image.image)
5. Use the **Bones** component to set up the inter-joint relation to make the tips of the thumb and index fingers pinch. The following settings are for your reference:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76be503f180543e5b4bf7ee6e0887166~tplv-goo7wpa0wc-image.image)
6. Use the **Transform** component to configure the orientation of the hand. The following settings are for your reference:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c047f8d4f534cdfb1bcfd66033ff6ec~tplv-goo7wpa0wc-image.image)
7. Add the **PXR_Hand Pose** script to the prefab.
8. Use **PXR_Hand Pose (script)** to set up hand pose events:
   1. In the **Track Type** field, select the hand that the "Okay" pose is applied to. 
   2. In the **Config** field, add the Hand Pose Config file generated for the "Okay" pose.
   3. Add functions for triggering **Hand Pose Start**, **Hand Pose Update**, and **Hand Pose End** events.
9. Build and run the project on your PICO device to try the hand pose and hand pose event you just created, and carry out debugging if necessary.


# --- END: Create example hand poses.md ---



# --- BEGIN: Create immersive scenes.md ---

This article introduces how to create immersive scenes for PICO OS.
## **Mapping scheme**
Under a relatively fixed perspective, various tools can be used to create high-precision rendering results. By projection, high-quality display effects can be simulated with low-consumption assets.
**![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08bad438d6bc4a919e7fab4128c23dd1~tplv-goo7wpa0wc-image.image)**
## **Usable range of mapping**
Large outdoor scenes, immovable.
## **Production method**
It is recommended to use Maya\Blender for creation.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cae5ae5d5a7a4f94a7d4ba3c5132c0c0~tplv-goo7wpa0wc-image.image)
## **Mapping usage logic**
The image information from the camera is projected onto the model based on a fixed perspective.




![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6341bd58dc9f4378998a25d5b5e6318a~tplv-goo7wpa0wc-image.image)
Projection demonstration: No matter how the model is edited, the displayed image information remains unchanged, similar to the concept of a "projector".




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/248dd3ec661945b098c2cb2e939840d5~tplv-goo7wpa0wc-image.image" width="1280px" />

Content seen from the camera's perspective




Conversely, if the rendered images are produced using the current model, they can be projected losslessly based on the perspective.




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0d80ab68bba4e2e95ce94a31fe5b827~tplv-goo7wpa0wc-image.image" width="1280px" />

Before mapping, export the rendered model




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44a86bd281374debba6d8edb8b69f347~tplv-goo7wpa0wc-image.image" width="1280px" />

Map the rendering effect onto the original model




## **Case studies**
The cases displayed in this section are all created with Unreal Engine; you can also use tools such as Maya or Blender for creation.
### Procedure

1. Create the "Spring" scene in Unreal Engine, including terrain setup, vegetation coverage creation, and atmosphere and cloud production.




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e57b506f50324327b8f45e8c2ebeec95~tplv-goo7wpa0wc-image.image" width="1280px" />




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d9130e1b58442578713ed77ce436c29~tplv-goo7wpa0wc-image.image" width="1280px" />




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad8211c68afe437db45b5eabaf4b36e4~tplv-goo7wpa0wc-image.image" width="3417px" />




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab9439f3c6744c5dbba54b25b4580bd3~tplv-goo7wpa0wc-image.image" width="1280px" />




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60ea60a377654a1ca8d58d91dce69be3~tplv-goo7wpa0wc-image.image" width="1280px" />




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bca40b3e4aea44f8aa142dd07a685b81~tplv-goo7wpa0wc-image.image" width="1280px" />




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5281c768218413ea73e918642850f6f~tplv-goo7wpa0wc-image.image" width="1280px" />




2. Obtain a 360-degree rendered image of the scene through 360-degree rendering.




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b93d93e5e734751a68be9f7d9948a76~tplv-goo7wpa0wc-image.image" width="420px" />




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2c41adc0da04dff9921e6dff6320c72~tplv-goo7wpa0wc-image.image" width="1280px" />




3. Export UE assets, optimize them to low-poly models, and also export the camera used for rendering, then import them into Blender together.




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6537f516c12841319f8a9a94b8873b1f~tplv-goo7wpa0wc-image.image" width="1280px" />




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0fcf480b05c4d80b23f0563b86836d9~tplv-goo7wpa0wc-image.image" width="2704px" />




4. Use 360 mapping to transfer the 360 image data to the low-poly model based on the rendering camera. To create richer seethrough variations, it is recommended to focus polygons on close and medium-range scenes, remove polygons not visible from the camera's perspective, and use polygons to process distant scenes with low displacement effects.




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8de70471e03407982d163468819c352~tplv-goo7wpa0wc-image.image" width="1280px" />




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e89882b9d634af492d2c247d4288bfc~tplv-goo7wpa0wc-image.image" width="1280px" />




5. Assign materials to the mapped image in an unlit form.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7e317547a2e41adb7dc4c36487987d2~tplv-goo7wpa0wc-image.image" width="3278px" />

### Resources
The number of resources used in the "spring" scene is as follows:

* Triangles: 110,000
* On-screen polygons: 50,000
* Texture count: 8192*2 ASTC 10*10
* Package size: 23MB

## Sample file
<a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee0c5eb42dab49a39f003d48ca953c7d~tplv-goo7wpa0wc-image.image" filename="simple_scene.unitypackage" download>simple_scene.unitypackage</a>
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34b679867e0f413a874c298261801409~tplv-goo7wpa0wc-image.image" width="2820px" />


# --- END: Create immersive scenes.md ---



# --- BEGIN: Demo(2).md ---

You can get the [GameAPITest](https://github.com/Pico-Developer/PlatformSample-Unity/tree/main/Assets/Samples/GameAPITest) demo on PICO Github. The demo contains all Leaderboard service-related APIs which you can use for API debugging. The [DebugPanel](https://github.com/Pico-Developer/PlatformSample-Unity/tree/main/Assets/Samples/Game/DebugPanel) folder contains UI-related content (as is shown in the figure below), and the [Log](https://github.com/Pico-Developer/PlatformSample-Unity/tree/main/Assets/Samples/Game/Log) folder contains the scripts for log output. 
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e8cd52c7008489eb8457b13e697a95f~tplv-goo7wpa0wc-image.image" width="700px" />

## Prerequisite
The device's ROM version should be 4.8.0 or later.
## Procedure
Use the following steps to try out the demo.

1. Launch the "GameAPITest" demo. 
2. Under **Function type** , select **Leaderboard**. 
   A list of all available APIs for the Leaderboard service appears. 
3. Select the API you want to test. 
   The parameters that need to be configured for the API are then listed under **set parameters here**. 
4. Set the parameters. 
5. Click **Execute**. 
   The results will be displayed under **Log Message** on the right. 
6. (Optional) Click a single log to view the details.


# --- END: Demo(2).md ---



# --- BEGIN: Demo(3).md ---

You can get the "[GameAPITest](https://github.com/Pico-Developer/PlatformSample-Unity/tree/main/Assets/Samples/GameAPITest)" Demo on PICO Github. The demo contains all Leaderboard service-related APIs which you can use for API debugging. The [DebugPanel](https://github.com/Pico-Developer/PlatformSample-Unity/tree/main/Assets/Samples/Game/DebugPanel) folder contains UI-related content (as is shown in the figure below), and the [Log](https://github.com/Pico-Developer/PlatformSample-Unity/tree/main/Assets/Samples/Game/Log) folder contains the scripts for log output.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da659253e77f4581a85bb79628d36ba3~tplv-goo7wpa0wc-image.image" width="700px" />

Below are the steps to using the "GameAPITest" demo: 

1. Launch the demo. 
2. Under **Function type**, select **Achievement**. 
   A list of all available APIs for Achievement service appears. 
3. Select the API you want to test. 
   The parameters that need to be configured for the API are then listed under **set parameters here**. 
4. Set the parameters. 
5. Click **Execute**. 
   The results will be displayed under **Log Message** on the right. 
6. (Optional) Click a single log to view the details.


# --- END: Demo(3).md ---



# --- BEGIN: Demo.md ---

Space Arena Party is a multiplayer social game demo that implements the following PICO platform services: Friends service, Social Interaction service, plus Room & Matchmaking service. You can get the following experiences in the demo:

* Avatar and locomotion
* Creating and joining virtual rooms
* Real-time multiplayer interaction
* Checking out your friend list and inviting friends

## Preview
You can play the following short video to view the demo's visual design and what you can do with it.

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3fedd7a950545949f031bcd66657dd9~tplv-goo7wpa0wc-image.image></video>

## Requirement
Unity Editor's version should be 2021.3.22. Unity 2022 is currently not supported.
## Install the APK & run the demo
Connect your PICO device and PC with a USB cable, use the following command to install the demo's APK file on the PICO device, then open the APK file and enjoy the demo.
```C#
adb install SpaceArenaParty.apk
```

<a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a385cbef3ac476596296c111f747489~tplv-goo7wpa0wc-image.image" filename="SpaceArenaParty.apk" download>SpaceArenaParty.apk</a>
## Complete procedure for using the demo
For more information about the demo and the detailed instructions on using it, refer to the "[Space Arena Party](/en_space-arena-party)" article.


# --- END: Demo.md ---



# --- BEGIN: DLC.md ---

Downloadable content (DLC) represents the contents/files such as expansion packs that users can purchase and download, which can help grow your revenue. Each DLC is associated with an add-on and has an individual SKU as its unique identifier. Users must purchase the app before purchasing the DLCs provided in it. DLCs are downloadable in apps only.
DLC enables you to update your app in a more flexible and lightweight way. Once you want to update the content for a published app, you only need to upload new resources such as levels and cosmetics as DLCs on the PICO Developer Platform, but do not need to upload a new build. Users can thereby purchase, download, and experience the latest resources without having to update or reinstall your app.
## Basic concepts
| **Name** | **Description** |
| --- | --- |
| Add-ons | Products available for purchase in the PICO Store or the app. |
| In-App Purchase (IAP) | Purchases within the app. The products for in-app purchase must be created on the PICO Developer Platform. Common products are in-game cosmetics, props, and coins. |
| DLC | Downloadable content, such as expansion packs. |
## Key features
### Get a list of available DLCs
You can use the following APIs to get a list of available (purchased and/or purchasable) DLCs and display them to users in your app. 
When uploading a DLC, you can specify the oldest version that the DLC supports. If a user installs an older version than the version you specify, the user will be unable to see the DLC in the list.
| **API** | **Description** |
| --- | --- |
| `AssetFileService.GetList()` | Get a list of available DLCs. The returns vary with the country/region where your app is published: <br>  <br> * **Mainland China**: <br>    If the app's type is "Game", only purchased DLCs will be returned because in-app purchase is not supported in Mainland China. <br>    If the app's type is "App", both purchased and purchasable DLCs will be returned. <br> * **Non-Mainland China**: Both purchased and purchasable DLCs will be returned. |
| `AssetFileService.GetNextAssetDetailsListPage()` | Get a paginated list of available DLCs. |
### Purchase & download DLCs
After users purchase a DLC in the PICO Store or in the PICO VR app, they need to return to your app to download the DLC.
The PICO Store does not support downloading DLCs, so you need to enable users to download DLCs in your app.

Below is the overall workflow:

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3NTVweCIgaGVpZ2h0PSIzNzBweCIgdmlld0JveD0iLTAuNSAtMC41IDc1NSAzNzAiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDE2MiAxODIgTCAyMTUuNjMgMTgyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjIwLjg4IDE4MiBMIDIxMy44OCAxODUuNSBMIDIxNS42MyAxODIgTCAyMTMuODggMTc4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIxNDciIHdpZHRoPSIxNjAiIGhlaWdodD0iNzAiIHJ4PSIxMC41IiByeT0iMTAuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTgycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlRoZSB1c2VyIGNoZWNrcyB0aGUgbGlzdCBvZiBhdmFpbGFibGUgYWRkLW9ucyAoYXNzb2NpYXRlZCB3aXRoIERMQ3MpIGluIGFuIGFwcCBvciBpbiB0aGUgUElDTyBTdG9yZS48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjg3IDE0NC41IEwgMjg3IDY4LjM3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjg3IDYzLjEyIEwgMjkwLjUgNzAuMTIgTCAyODcgNjguMzcgTCAyODMuNSA3MC4xMiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMzUyIDE4MiBMIDQyNS42MyAxODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MzAuODggMTgyIEwgNDIzLjg4IDE4NS41IEwgNDI1LjYzIDE4MiBMIDQyMy44OCAxNzguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjg3IDE0NC41IEwgMzUyIDE4MiBMIDI4NyAyMTkuNSBMIDIyMiAxODIgWiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxODJweDsgbWFyZ2luLWxlZnQ6IDIyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5XaGV0aGVyIHRoZSB1c2VyIGhhcyBwdXJjaGFzZWQgYW4gYWRkLW9uIGFzc29jaWF0ZWQgd2l0aCBhIERMQy48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI4MiIgeT0iMTAyIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMTJweDsgbWFyZ2luLWxlZnQ6IDMwMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPk5vPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzNjYiIHk9IjE2MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTcycHg7IG1hcmdpbi1sZWZ0OiAzODZweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5ZZXM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIyNyIgeT0iMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogMjI4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlRoZSB1c2VyIHB1cmNoYXNlcyB0aGUgYWRkLW9uLjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NTIgMTgyIEwgNTgyIDE4MiBMIDU4MiAxMTIgTCA2MjUuNjMgMTEyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjMwLjg4IDExMiBMIDYyMy44OCAxMTUuNSBMIDYyNS42MyAxMTIgTCA2MjMuODggMTA4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ5MiAyMTcgTCA0OTIgMjkwLjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDkyIDI5NS44OCBMIDQ4OC41IDI4OC44OCBMIDQ5MiAyOTAuNjMgTCA0OTUuNSAyODguODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI0MzIiIHk9IjE0NyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI3MCIgcng9IjEwLjUiIHJ5PSIxMC41IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxODJweDsgbWFyZ2luLWxlZnQ6IDQzM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5UaGUgdXNlciBjbGlja3MgdG8gZG93bmxvYWQgdGhlIERMQyBpbiB0aGUgYXBwLjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDMyIiB5PSIyOTciIHdpZHRoPSIxMjAiIGhlaWdodD0iNzAiIHJ4PSIxMC41IiByeT0iMTAuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzMycHg7IG1hcmdpbi1sZWZ0OiA0MzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIHVzZXIgY2FuY2VscyB0aGUgZG93bmxvYWQuPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MzIiIHk9Ijc3IiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjcwIiByeD0iMTAuNSIgcnk9IjEwLjUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDExMnB4OyBtYXJnaW4tbGVmdDogNjMzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRvd25sb2FkIHN1Y2NlZWRzLjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNjMyIiB5PSIyMTIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNzAiIHJ4PSIxMC41IiByeT0iMTAuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjQ3cHg7IG1hcmdpbi1sZWZ0OiA2MzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RG93bmxvYWQgZmFpbHMuPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM0MiAzMiBMIDQ5MiAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQ5MiAzMiBMIDQ5MiAxNDAuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0OTIgMTQ1Ljg4IEwgNDg4LjUgMTM4Ljg4IEwgNDkyIDE0MC42MyBMIDQ5NS41IDEzOC44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTgyIDE4MiBMIDU4MiAyNTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1ODIgMjUyIEwgNjI1LjYzIDI1MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDYzMC44OCAyNTIgTCA2MjMuODggMjU1LjUgTCA2MjUuNjMgMjUyIEwgNjIzLjg4IDI0OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA2OTIgMzMyIEwgNjkyIDI4OC4zNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDY5MiAyODMuMTIgTCA2OTUuNSAyOTAuMTIgTCA2OTIgMjg4LjM3IEwgNjg4LjUgMjkwLjEyIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA1NTIgMzMyIEwgNjkyIDMzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48L2c+PC9zdmc+" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxCellList&quot;:[&quot;Xfazc13W&quot;,&quot;Pect1uf9&quot;,&quot;CExewT3c&quot;,&quot;x1WCBlOW&quot;,&quot;3w1I3Jzu&quot;,&quot;Pqf3G3q0&quot;,&quot;Y5qet5Yz&quot;,&quot;ZCt2C2GU&quot;,&quot;IqT911RA&quot;,&quot;yvNkobVV&quot;,&quot;QbfLWuOJ&quot;,&quot;V0TtuQU1&quot;,&quot;PJuqb7iD&quot;,&quot;4nOCUQ3R&quot;,&quot;T8iXJEIs&quot;,&quot;0qK1HiEq&quot;,&quot;xRYZvFAQ&quot;,&quot;OndXAeR3&quot;,&quot;aiXeNfr7&quot;,&quot;WUlHjr6H&quot;,&quot;HpGEW6UE&quot;,&quot;5LKlwtud&quot;],&quot;mxGraphModel&quot;:{&quot;arrows&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;dx&quot;:&quot;782&quot;,&quot;dy&quot;:&quot;472&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageHeight&quot;:&quot;1169&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;tooltips&quot;:&quot;1&quot;},&quot;mxCellMap&quot;:{&quot;0qK1HiEq&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;70&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;660&quot;,&quot;y&quot;:&quot;270&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;id&quot;:&quot;0qK1HiEq&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;Download fails.&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;3w1I3Jzu&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;315&quot;,&quot;y&quot;:&quot;120&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;3w1I3Jzu&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;Y5qet5Yz&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;value&quot;:&quot;&quot;},&quot;4nOCUQ3R&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;70&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;460&quot;,&quot;y&quot;:&quot;355&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;id&quot;:&quot;4nOCUQ3R&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user cancels the download.&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;5LKlwtud&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;580&quot;,&quot;y&quot;:&quot;390&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;720&quot;,&quot;y&quot;:&quot;390&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;straight&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;5LKlwtud&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=none;html=1;&quot;,&quot;value&quot;:&quot;&quot;},&quot;CExewT3c&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;CExewT3c&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;x1WCBlOW&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;Y5qet5Yz&quot;,&quot;value&quot;:&quot;&quot;},&quot;HpGEW6UE&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;720&quot;,&quot;y&quot;:&quot;390&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;730&quot;,&quot;y&quot;:&quot;350&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;HpGEW6UE&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;entryX=0.5;entryY=1;entryDx=0;entryDy=0;&quot;,&quot;target&quot;:&quot;0qK1HiEq&quot;,&quot;value&quot;:&quot;&quot;},&quot;IqT911RA&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;394&quot;,&quot;y&quot;:&quot;220&quot;},&quot;id&quot;:&quot;IqT911RA&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;Yes&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;OndXAeR3&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;520&quot;,&quot;y&quot;:&quot;90&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;560&quot;,&quot;y&quot;:&quot;40&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;OndXAeR3&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;entryX=0.5;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;target&quot;:&quot;PJuqb7iD&quot;,&quot;value&quot;:&quot;&quot;},&quot;PJuqb7iD&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;70&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;460&quot;,&quot;y&quot;:&quot;205&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;id&quot;:&quot;PJuqb7iD&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user clicks to download the DLC in the app.&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;Pect1uf9&quot;:{&quot;id&quot;:&quot;Pect1uf9&quot;,&quot;parent&quot;:&quot;Xfazc13W&quot;},&quot;Pqf3G3q0&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;460&quot;,&quot;y&quot;:&quot;240&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;Pqf3G3q0&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;Y5qet5Yz&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;value&quot;:&quot;&quot;},&quot;QbfLWuOJ&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-Array&quot;:{&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;610&quot;,&quot;y&quot;:&quot;240&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;610&quot;,&quot;y&quot;:&quot;170&quot;},&quot;as&quot;:&quot;points&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;QbfLWuOJ&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;PJuqb7iD&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;T8iXJEIs&quot;,&quot;value&quot;:&quot;&quot;},&quot;T8iXJEIs&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;70&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;660&quot;,&quot;y&quot;:&quot;135&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;id&quot;:&quot;T8iXJEIs&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;Download succeeds.&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;V0TtuQU1&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;V0TtuQU1&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;PJuqb7iD&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;4nOCUQ3R&quot;,&quot;value&quot;:&quot;&quot;},&quot;WUlHjr6H&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;610&quot;,&quot;y&quot;:&quot;310&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;660&quot;,&quot;y&quot;:&quot;310&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;WUlHjr6H&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;entryX=0;entryY=0.5;entryDx=0;entryDy=0;&quot;,&quot;value&quot;:&quot;&quot;},&quot;Xfazc13W&quot;:{&quot;id&quot;:&quot;Xfazc13W&quot;},&quot;Y5qet5Yz&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;75&quot;,&quot;width&quot;:&quot;130&quot;,&quot;x&quot;:&quot;250&quot;,&quot;y&quot;:&quot;202.5&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Diamond&quot;,&quot;id&quot;:&quot;Y5qet5Yz&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rhombus;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;Whether the user has purchased an add-on associated with a DLC.&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;ZCt2C2GU&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;310&quot;,&quot;y&quot;:&quot;160&quot;},&quot;id&quot;:&quot;ZCt2C2GU&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;No&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;aiXeNfr7&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;610&quot;,&quot;y&quot;:&quot;240&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;610&quot;,&quot;y&quot;:&quot;310&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;straight&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;aiXeNfr7&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=none;html=1;&quot;,&quot;value&quot;:&quot;&quot;},&quot;x1WCBlOW&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;70&quot;,&quot;width&quot;:&quot;160&quot;,&quot;x&quot;:&quot;30&quot;,&quot;y&quot;:&quot;205&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;id&quot;:&quot;x1WCBlOW&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user checks the list of available add-ons (associated with DLCs) in an app or in the PICO Store.&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;xRYZvFAQ&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;370&quot;,&quot;y&quot;:&quot;90&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;520&quot;,&quot;y&quot;:&quot;90&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;width&quot;:&quot;50&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;straight&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;xRYZvFAQ&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;endArrow=none;html=1;&quot;,&quot;value&quot;:&quot;&quot;},&quot;yvNkobVV&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;120&quot;,&quot;x&quot;:&quot;255&quot;,&quot;y&quot;:&quot;60&quot;},&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;id&quot;:&quot;yvNkobVV&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user purchases the add-on.&quot;,&quot;vertex&quot;:&quot;1&quot;}}},&quot;diagramType&quot;:&quot;flowchart&quot;,&quot;lastEditTime&quot;:0}" />

Below is detailed information:

* After purchasing an app, users are able to purchase add-ons associated with DLCs in the app or in the PICO Store. After purchase, the DLC's `IapStatus` becomes `entitled`, otherwise it will be `not-entitled`. To prevent users who have not purchased the DLC from accessing it through illegal installation, we suggest that you include an `IapStatus` check mechanism in your code.
* For purchased DLCs, once users click to download them, `DownloadById()` will be called to launch the download flow. Meanwhile, you can:
   * Call `StatusById()` or `StatusByName()` to check the download status of a specific DLC;
   * Call `GetAssetFileDownloadResult()` to check the download result;
   * Call `DownloadCancelById()` to cancel the download of specific DLC;
   * Call `GetAssetFileDownloadCancelResult()` to check whether a DLC download has been successfully canceled.
* For nonpurchased DLCs, once users click to purchase them, `LaunchCheckoutFlow()` will be called to launch the checkout flow. After successful payment, the user can click to download the DLC.
* Users need to re-download DLCs after reinstalling an app.

### Delete downloaded DLCs
Downloaded DLCs will be saved to the OBB folder in apps. If a user uninstalls an app, the app's folder and the DLCs downloaded in the app will all be deleted.
You can call `DeleteById()` or `DeleteByName()` to delete a specific downloaded DLC from a device. Users are allowed to re-download purchased DLCs after deletion.
## Store presence
DLCs available for purchase are displayed on your app's description page in the PICO Store. Users can view a DLC's poster, brief, name, and price. You can configure this information for your DLC on the PICO Developer Platform, see the "Add a DLC" section below for detailed instructions.
**On the VR headset**
Below is how the DLCs are displayed in the device-end PICO Store.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/0754a9c2513c43a6acf07e96654d4ef2~tplv-em5hxbkur4-noop.image?width=3000&height=1440" width="546px" />

**On the mobile phone**
Below is how the DLCs are displayed in the mobile-end PICO Store.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/27719ec33e284930a2808fafd073875b~tplv-em5hxbkur4-noop.image?width=718&height=1372" width="238px" />

## Implementation
### Complete basic setups
Refer to the "[Platform services overview](/en_platform-services-overview#712343ad)" article to complete all required setups, including adding an app ID, initializing platform services, etc.
### Add a DLC
You can only add DLC files to **Durable** add-ons.

On the PICO Developer Platform, you can add DLC files to your app. Once a DLC file is released, users can purchase and download the DLC file to enjoy specific content in your app. The developer platform implements a DLC file name check mechanism. If you want to upload multiple DLC files for your app, you need to make sure that each DLC file's name is unique.

1. Create an add-on. Refer to "[In-app purchase](/13136/en_in-app-purchase)" for detailed instructions. 
2. Return to the add-on list.
3. Click the name of the add-on or the **Edit** button in the **Actions** column.
   This directs you to the add-on's editing page.
4. In the **DLC Files** tab, upload DLC files for this add-on.
   * The maximum size for a DLC file is 4 GB and you can upload up to 25 files.
   * Carefully name the DLC file. Once the DLC file is approved, you can no longer edit its name.

5. Click the **Go to submission** button.
   The add-on associated with the DLC file will be reviewed by the PICO team. Once approved, users can see and download the DLC file in the app.

### Call APIs
You can call DLC APIs in your app.
## Update a DLC
You can update DLC by adding new DLC files to the corresponding add-on, but you cannot delete old DLC files. Users who have not downloaded the old DLC files will directly see the latest DLC file. For users who have downloaded the old DLC files, they can choose to continue using them. If you want users to use the latest DLC file, you can customize relevant logic (such as a pop-up window) to remind them to update.

1. Go to the **Add-Ons** page.
2. Find the target add-on in the list with the status "Published" and then click the **View** button in the **Actions** column.
   You will enter the version display page of this add-on.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e5974dbd60f4c8397c70341d6c37d9c~tplv-goo7wpa0wc-image.image)
3. Click the **Create New Version** button in the upper-right corner.
   You will enter the edit page for this add-on version.
4. In the **DLC Files** tab, upload new DLC files for this add-on version and save them.
5. Click the **Go to submission** button at the bottom.
   This  add-on version has entered the review process. After approval, the add-on's information within the app and in the PICO Store will be automatically updated to the latest version.

## Test DLCs
After uploading a DLC, no matter whether its corresponding add-on has been submitted for review or not, you can proceed to test the DLC to see if you can successfully run through IAP service.
### Prerequisite
Make sure you have toggled the **Show in PICO Store** switch on.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7c4262a61294484bae9e66aee8c104c~tplv-goo7wpa0wc-image.image)
### Methods
You can test DLCs using the IAP APIs or directly test them in the PICO Store. Below are detailed descriptions:
| **Method** | **Description** |
| --- | --- |
| Use APIs | You can use IAP APIs to get DLC data and then test the overall in-app purchase flow. Visit [here](https://pdocor.pico-interactive.com/reference/unity/platform/2.1.2/class_pico_1_1_platform_1_1_i_a_p_service.html) for API reference. |
| Use the PICO Store | According to the country/region where the add-on is to be released, you can search for the DLC's corresponding add-on in the PICO Store for that country/region. The add-on can be accurately found and then displayed. You can then use the PICO Developer account that uploaded the DLC to test the overall in-app purchase flow. |
### Notes
Pay attention to the following when testing DLCs:

* You **MUST** use the PICO developer account that is used to submit the app package and upload the DLC.
* You must use real payment methods. For **Mainland China**, you can use Alipay or or other valid payment methods. For **elsewhere**, you can use Paypal or other valid payment methods.
* For **Mainland China**, the testing price is 0.1 RMB. For **elsewhere**, the testing price is 0.01 dollar.
* If you want to allow others (e.g., QA) to access the DLC test offer, you need to invite them to become the members of your organization and set their role as **Organization Administrator** or **Application Manager**. Refer to the "[Manage organization members](/13136/en_manage-member)" article for detailed instructions.
* The revenue generated in the test goes to the organization that the PICO developer account belongs to.
* If the DLC's minimum compatible version is deleted, you are unable to obtain any of the DLC's information. You need to reselect the DLC's minimum compatible version on the PICO Developer Platform.
* If you app is published, you can only save the DLC (no need for submission) and then use the corresponding PICO Developer account that has uploaded the DLC to search for and view the DLC's information in the PICO Store.
* You cannot download the testing DLC from the PICO Store. You need to download it in your app and then test it.
* When testing a DLC, if the corresponding app has not been submitted, the platform will display the default app information such as app name, image, and video. This information will be automatically updated when the app is approved.
* After testing, if you want to officially release this DLC, you need to submit its corresponding add-on, and after approval, this DLC will be officially released.

## Demo
You can use the DLC demo to try out basic DLC APIs. For more information, refer to the "[Downloadable content (DLC) demo](/en_dlc-demo)" article.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/0f9f19ff1cf3477f99a608b3f94cc2af~tplv-em5hxbkur4-noop.image?width=1820&height=942" width="700px" />

## API reference
For more information about DLC-related APIs, refer to the [API reference](/reference/unity/client-api/AssetFileService/).


# --- END: DLC.md ---



# --- BEGIN: Does the PICO Unity Integration SDK support desktop app development_.md ---

The PICO Unity Integration SDK only supports Android app development.


# --- END: Does the PICO Unity Integration SDK support desktop app development_.md ---



# --- BEGIN: Download development resources.md ---

In the Download Center, you can download developer tools, SDKs, and samples.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25fa5766e20640308461312ccef120a2~tplv-goo7wpa0wc-image.image)
## Developer tools
### Tool overview
| **Name** | **Description** |
| --- | --- |
| RenderDoc for PICO | RenderDoc for PICO is a tool for graphic analysis and debugging, helping you debug a frame, trace rendering stages, and analyzing draw calls. |
| PICO CLI | PICO Command Line Utility enables you to manage the files on the PICO Developer Platform more easily, including: <br>  <br> * upload APK files, the OBB file, Asset files (extra OBB files added on the PICO Developer Platform)  <br> * manage DLC files for an add-on  <br> * download APK files <br> * clone a build to other release channels. |
| PICO Haptic Editor | PICO Haptic Editor supports editing broadband and multi-channel haptic feedback.  |
### Download, launch, and uninstall tools
| **Action** | **Description** | **Illustration** |
| --- | --- | --- |
| Install tools | Under the **Tools** tab, click **Download** to install RenderDoc for PICO or PICO CLI tool. | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f2592eaa8034b798c5481cbf8abd8fe~tplv-goo7wpa0wc-image.image) |
| launch/uninstall tools <br>  | Under the **Installed** tab, click **Start** to launch a tool, or click the Ellipsis icon > **Uninstall** to uninstall a tool. | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/927c3d67e4c94967879d95d88643bee5~tplv-goo7wpa0wc-image.image) |
### User guides

* For detailed instructions on using RenderDoc for PICO, refer to [RenderDoc for PICO's user guide](/en_renderdoc-for-pico).
* For detailed instructions on using the PICO Command Line Utility, refer to CLI Command Line Utility's user guide.
* For detailed instructions on using the PICO Haptic Editor, refer to [PICO Haptic Editor's user guide](/en_pico-haptic-editor).

## SDKs
Under the **SDK** tab, download your desired SDKs.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9cd3ab3819646568c78f262a0de607f~tplv-goo7wpa0wc-image.image)
## Samples
Under the **Samples** tab, download your desired sample projects.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79b397421853408bb1cc4cf3f92e51b6~tplv-goo7wpa0wc-image.image)


# --- END: Download development resources.md ---



# --- BEGIN: Download the streaming service.md ---

You can monitor your PICO device's performance using the streaming service. If you are using the Windows operating system, you can also preview your Unity project using the streaming service with the PICO Unity Live Preview Plugin.
Use the following steps to download the streaming service:

1. Connect your computer and PICO device with a USB cable.
2. Open the PDC tool.
3. From the left navigation panel, select **Download Center**.
4. On the **Tools** pane, select the corresponding streaming service based on your device model:
   * Project Swan: select the **Streaming Service (Swan)**.
   * Others: select the **Streaming Service**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e31a907dacb84f718ecf53de21b17fb3~tplv-goo7wpa0wc-image.image)
5. Click the **Download** button. 
6. Once downloaded, follow the on-screen instructions to install the streaming service.


# --- END: Download the streaming service.md ---



# --- BEGIN: Enhance image quality.md ---

Image quality hugely affects your app's user experience. There are many causes that lead to low image quality, among which jagged edges of objects and blurry and flickering textures and texts are the most common. Therefore, you can improve your app's image quality by resolving the above-mentioned problems.
## Summary
This article introduces the following three methods that aim to improve your app's image quality:

* **Reduce edges' jaggedness** by enabling 4x MSAA for your project.
* **Improve texture quality** by enabling Mipmap and Trilinear Filtering for all textures and especially enabling Anisotropic Filtering for textures like walls and floors that can be viewed at oblique angles.
* **Improve text quality** by using the TextMeshPro component instead of the Text component to render texts in scenes.

Refer to the rest of the article for detailed instructions.
## Reduce edges' jaggedness
In image rendering, one pixel displays only one color, so each pixel samples the color at its center. However, in low-resolution scenes, the edges of polygons are not accurately sampled by each pixel, which can lead to jagged edges and cause visual discomfort.
**Multisampling Anti-Aliasing (MSAA)** reduces the jagged edges of objects by sampling the jagged areas and then surrounding them with intermediate shades of color, thereby making the lines appear much smoother.
### Different MSAA levels
The figure below demonstrates to what degree different levels of MASS reduce the jaggedness of edges. From left to right: none, 2x MSAA, 4x MSAA, 8x MSAA.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/5bca8f174b3343a5aad515b79fcdc75a~tplv-em5hxbkur4-noop.image?width=1554&height=414)
### Set an MSAA level
"4x MSAA" is the default recommended MASS level provided by the SDK. We recommend using "4x MSAA" as it enhances image quality without using much of the CPU's processing power. However, if your app is experiencing high CPU usage, it is recommended that you set at least "2x MSAA" for it. "2x MSAA" requires a lot less processing power from the CPU than "4x MSAA" and brings a better visual effect to images than those without MSAA enabled. For detailed instructions on using MASS, refer to [this article](/13136/en_anti-aliasing).
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/b3d0a5693a494430b06280327f7fcd53~tplv-em5hxbkur4-noop.image?width=1563&height=742)
<em>Original image vs 4x MSAA</em>

## **Improve texture quality**
When a texture atlas is placed far from the camera, the lines and text on the texture may appear flickering. One cause is the low resolution of the texture, and the other is that the number of pixels sampled for displaying this texture is fewer than the actual number of pixels composing it, which consequently leads to aliasing. You can use Mipmap, Trilinear Filtering, and Anisotropic Filtering to resolve this issue.
### Use mipmaps
**Mipmaps** contain progressively smaller and lower-resolution versions of a single texture. The width and height of each mip level are half of those of the previous mip level. The core logic behind mipmaps is that this technique enables the system to select the most appropriate mip level based on the actual size of the to-be-rendered object displayed in the scene. Specifically, a higher mip level (high-quality and less blurred) is used for objects closer to the camera, and a lower mip level (low-quality and more blurred) is used for a more distant object. Below are example mipmaps:
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/426880725ff64d0d9f929cb66504b7f6~tplv-em5hxbkur4-noop.image?width=720&height=480)
#### Generate mipmaps
Use the following steps to generate mipmaps for a texture:

1. Go to the **Project** window > the **Assets** directory, and select the target texture.
   The Inspector window displays the parameters you can configure for the texture.
2. Set the texture's **Texture Type** to **Sprite (2D and UI)**.
   If you do not complete this step, you will be unable to set the **Source Image** parameter for a UI-class image added to the scene.

3. Expand the **Advanced** tab and check **Generate Mip Maps**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/549ce3e0033f47d5b69dab711ffe09ad~tplv-em5hxbkur4-noop.image?width=794&height=824)
   The editor will generate textures of different mip levels and display them at the bottom of the Inspector window. You can move the slider to view them.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/8e5e6897fd9d418f97388f943faa1560~tplv-em5hxbkur4-noop.image?width=822&height=348)

#### Important note
With mipmaps generated for a texture, if you keep changing the distance between the camera and the texture, the texture will sometimes suddenly appear blurred (as shown in the video below). In VR scenes, this phenomenon can be clearly felt by users and can affect your app's user experience to some extent. Therefore, after generating mipmaps for a texture, it is necessary to use Trilinear Filtering to eliminate the blurriness when switching between different mip levels.
<video src=https://sf1-cdn-tos.huoshanstatic.com/obj/vcloud/e74d20840651f124b9ec72945832c7f6-.mp4></video>
### Use Trilinear Filtering
Trilinear Filtering interpolates between the results of bilinear filtering on the two mipmaps nearest to the detail required for the polygon at the pixel, which mitigates or even eliminates the blurriness and overlaps occurring when switching between different mip levels of textures. Use the following steps to enable Trilinear Filtering for a texture:

1. Go to the **Project** window > the **Assets** directory, and select the target texture.
   The Inspector window displays the parameters you can configure for the texture.
2. Set the texture's **Filter Mode** to **Trilinear**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/194165dc03f24aae99fb8ddaeda0551b~tplv-em5hxbkur4-noop.image?width=795&height=825)

### Use Anisotropic Filtering
When there is a large angle between the surface of an object and the camera, the projection of the texture atlas appears to be non-orthogonal. For example, when a floor or wall is distant from the camera, the width and height of the projection area of the corresponding texture atlas are not the same, so using a square texture atlas is not very appropriate and can lead to blurriness or flicker, or both.
**Anisotropic Filtering** resolves this problem by sampling a non-orthogonal texture. Moreover, Anisotropic Filtering performs more texture sampling, which eliminates blurriness while preserving details at oblique viewing angles. Therefore, for most objects that can be viewed at oblique angles, using Anisotropic Filtering can greatly improve image quality. However, Anisotropic Filtering requires more of the CPU's processing power than Trilinear Filtering, so we recommend using Anisotropic Filtering only for textures like walls and floors which can be viewed at oblique angles.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/709a1c6bccff455895644f4d6b842c32~tplv-em5hxbkur4-noop.image?width=1561&height=567)
Anisotropic Filtering off vs Anisotropic Filtering on

You can select the target texture and set **Aniso Level** for it in the **Inspector** window.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/ecf63f5f4ab442b093c133bd671ddc86~tplv-em5hxbkur4-noop.image?width=826&height=825)
## Improve text quality
The Unity Editor provides two built-in text-rendering components, namely, **TextMeshPro (TMP)** and **Text**. The TMP component renders texts using the signed distance field (SDF) algorithm, enabling high-quality text rendering regardless of the distance between the camera and text, the zoom rate, etc. The Text component uses the TrueType font to render texts, which may lead to blurriness, distortion, etc. Therefore, we recommend using the TMP component to render texts.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/af05a0e4fcf04c7a89fe20eebdb4cc57~tplv-em5hxbkur4-noop.image?width=1670&height=1412)
Text rendered by the TMP component (left) and the Text component (right)

### Use the **TextMeshPro** component
Follow the steps below to render text using the TextMeshPro component:

1. Create a font asset.
   The TextMeshPro component does not support TrueTypeFont and provides only one English font. Therefore, you need to create font assets to display more fonts in scenes. Font assets can be loaded dynamically or statically. Below are detailed instructions on creating a specific type of font asset:
   | **Font Asset Type** | **Description** | **Steps to create** |
   | --- | --- | --- |
   | Dynamic | Dynamic font assets enable you to start with an empty atlas to which characters are added automatically as you use them. Moreover, dynamic font assets require fewer steps to create than static font assets. | Use the following steps to create a dynamic font asset: <br> 1. Open your project in the Unity Editor. <br> 2. In the **Project** window, right-click on the **Assets** directory and select **Import New Assets** from the shortcut menu to import the .ttf file of the font you use. <br> 3. Right-click the .ttf file and select **Create** > **TextMeshPro** > **Font Asset**. A dynamic font asset is then created. <br> ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/7ce84d62afc24511a74cd59e3d243610~tplv-em5hxbkur4-noop.image?width=187&height=192) <br> ***Note***: <br> The default size of a text atlas is 1024x1024. You can adjust the size according to your actual needs. Below are the steps to follow: <br> 1. Under the **Asset** directory, select the dynamic font asset you just created. The **Inspector** window displays the parameters you can configure for the font asset. <br> 2. Under the **Generation Settings** tab, modify **Atlas Width** and/or **Atlas Height**. <br> ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/2d8167a1501c4a9ea3715a86cf8db562~tplv-em5hxbkur4-noop.image?width=784&height=418) |
   | Static | You need to generate a static font asset using the Font Asset Creator, import a .txt file containing the characters you will use, and bake the characters into the font atlas texture. | Use the following steps to create a static font asset: <br> 1. Open your project in the Unity Editor. <br> 2. In the **Project** window, right-click on the **Assets** directory and select **Import New Assets** from the shortcut menu to import the .ttf file of the font you use. <br> 3. Save the characters you will use in a UTF-8 formatted .txt file and import the file into your project. <br> 4. From the top menu bar, select **Window** > **TextMeshPro** > **Font Asset Creator**. <br> 5. In the **Font Asset Creator** window, complete the following: <br> - In **Source Font Flie**, select the font file you want to use. <br> - Set **Character Set** to **Characters from File**. <br> - Int **Character Flie**, select the .txt file you imported in step 3. <br> - Modify **Atlas Resolution** according to the number of characters to use. <br> 6. Click **Generate Font Atlas**. A static font asset is generated as shown below. <br> ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/36d79e0fa0c846d6b103147b57e89585~tplv-em5hxbkur4-noop.image?width=599&height=619) <br> 7. Click **Save** to save the font asset to your local PC. You can import it into your project when you want to use it. |
2. In the **Hierarchy** window, click **+** > **UI** > **Text - TextMeshPro**.
   The TMP component (displayed as Text (TMP)) is then added to the scene.
3. Select **Text (TMP)**.
   The Inspector window displays the components for configuring text atlas.
4. On the **TextMeshPro - Text (UI)** pane, complete the following:
   1. In **Font Asset**, select the font asset of the font your desired font.
   2. In the text box, enter the text you want to display.
   3. (Optional) Modify **Font Style** and other settings according to actual needs.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/9e471cee1ffe4e908993f1d3e908c7a3~tplv-em5hxbkur4-noop.image?width=796&height=645)


# --- END: Enhance image quality.md ---



# --- BEGIN: Enterprise services.md ---

The SDK provides enterprise service APIs. You can use them to develop apps that run on PICO enterprise devices.
## Overview
Enterprise service APIs are divided into the following categories:
| **Category** | **Description** |
| --- | --- |
| Device Info | To get device's information, including specs, status, and more. |
| Device Control | To control the device to perform specified operations, including automatically connecting to a specified WiFi network, scheduled startup/shutdown, and more. |
| System Setup | To customize the device's system settings, including adding boot and shutdown animations, setting the system language, control controller buttons' status, and more. |
| System Switch | To control the device through enabling/disabling specified functionalities. |
| App Management | To set a launcher, automatically start an app after startup, keep apps active, and more. |
| Screencast | To cast PICO headset's screen to the screen of an external device through Miracast or PICO's own screencast capability. |
| Large Space | To enable multiple devices to share the same map in the same coordinate, making the position in the virtual scene consistent with that in the real environment. Supports multi-player collaboration and multi-player battles in a large VR space. |
## API reference 
For more information on enterprise service APIs, such as detailed descriptions of parameters and returns, refer to the [API reference](/reference/unity/client-api/PXR_Enterprise/).
## Learn more
For more information on enterprise services, such as enterprise-level streaming, settings, and enterprise solutions, refer to [PICO Business's documentation](https://business.picoxr.com/cn/doc/Announcement).


# --- END: Enterprise services.md ---



# --- BEGIN: Entitlement check.md ---

Entitlement check is used to verify whether users are entitled to access your app. In other words, to verify whether users have purchased or obtained your app legitimately.
If users pass the entitlement checks, they can start using your app normally. If users fail to pass the checks, they will get notified by a pop-up window and the app automatically quits.
## Use cases

* **When the app is published on the PICO Store, the system automatically triggers the user entitlement check**
   PICO provides the capability to automatically verify a user's entitlement for apps available in the PICO store. This capability covers the following types of apps:
   * Apps that are downloaded and installed from the PICO Store.
   * Apps that are obtained through legitimate means such as redemption codes, gifts, or direct recharge by the operator.
   For the above apps, the PICO system performs user entitlement check upon app startup. If a user passes the check, the user can continue to use the app; otherwise, the system will display a pop-up prompt and close the app. In addition, the system also periodically performs silent entitlement checks during the app's runtime in the background.
* **Within the app, trigger the user entitlement check**
   You can call the related interface to verify a user at any time within the app (for example, when a new scene is loaded). If a user passes the check, the user can continue to use the app; otherwise, you can set a prompt and then close the app.

## Requirement
The SDK version should be 2.1.5 or later. 
## Important notes

* User entitlement checks only apply to the apps that have been published on the PICO Store. 
   For unpublished apps, unlogged-in users always skip entitlement checks and logged-in users always pass them regardless of their entitlement status. For logged-in users testing an unpublished app, they must have internet connection the first time they launch the app so that the app can check PICO's backend and make sure it is not violating any entitlement check rules. Once a user passes the entitlement check the first time, the unpublished app will no longer need internet connection during further testing.
   Once an app is officially published, unentitled users will fail the entitlement check and won't be able to access the app.
* For the convenience of app testing, if the app has been published on the PICO Store, members of the app's organization can skip entitlement checks. For details, refer to the "About app testing" section.
* User entitlement checks must be enabled for a paid app; otherwise, the app won't be approved after submission. We also recommend enabling user entitlement checks for free apps to better protect your app ideas.
* The target API level of your app should be no lower than 23 (i.e. targetSdkVersion>=23), and it is recommended to promptly update your app to Android's latest API level.

## Enable entitlement check
You can call [UserService.EntitlementCheck](/reference/unity/client-api/UserService/#EntitlementCheck) to enable user entitlement check for your app at the time as you see fit, for example, during scene loading. You need to pass the `killApp` parameter when calling this API:

* If you set `killApp` to `true`, the system will notify the user with a pop-up dialog box and then quit the app when the user fails to pass the entitlement check.
* If you set `killApp` to `false`, you need to handle the entitlement check result by yourself. For example, if the user fails to pass the entitlement check, you can use a dialog box to prompt the user to download the genuine app from the PICO Store.

### Code sample 1
In the following example, `killApp` is set to `true`. 
```C#
// Synchronously initialize platform services
try
{
    CoreService.Initialize();
    // Enable user entitlement checks, and you need to check if the request succeeds
    UserService.EntitlementCheck(true).OnComplete(msg =>
    {
        if (msg.IsError)
        {
            Debug.Log($"{msg.Error}");
            return;
        }

        Debug.Log($"Has entitlement:{msg.Data.HasEntitlement} ,status message: {msg.Data.StatusMessage}");
    });
}
catch (UnityException e)
{
    Debug.Log($"Init Platform SDK error:{e}");
    throw;
}
```

### Code sample 2
In the following example, `killApp` is set to `false`.
```C#
// Asynchronously initialize platform services
CoreService.AsyncInitialize().OnComplete(m =>
{
    if (m.IsError)
    {
        Debug.Log($"Async initialize failed: code={m.GetError().Code} message={m.GetError().Message}");
        return;
    }

    if (m.Data != PlatformInitializeResult.Success && m.Data != PlatformInitializeResult.AlreadyInitialized)
    {
        Debug.Log($"Async initialize failed: result={m.Data}");
        return;
    }

    Debug.Log("AsyncInitialize Successfully");
    // Enable user entitlement checks
    UserService.EntitlementCheck(false).OnComplete(checkMessage =>
    {
        if (checkMessage.IsError)
        {
            Debug.Log($"GetLoggedInUser failed:code= {checkMessage.Error}");
            return;
        }

        // Handle the entitlement check result
        var checkResult = checkMessage.Data;
        if (!checkResult.HasEntitlement)
        {
            Debug.Log($"don't has entitlement :{checkResult.StatusCode} {checkResult.StatusMessage}");
            // You can show the checkResult.StatusMessage to users in a pop-up dialog box
            Application.Quit();
        }
    });
});
```

## Prompts for entitlement check failure
If a user fails to pass the entitlement check, a corresponding window will pop up based on the reason for the failure.

* If the user hasn't purchased the app from an acknowledged channel, the following prompt will be given:

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51bc0cb8b5c844f9af735b06002c7152~tplv-goo7wpa0wc-image.image" width="400px" />

* If the user has downloaded a non-genuine app, the following prompt will be given:

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0beabf6498bc47589da9c4a381fe9f0e~tplv-goo7wpa0wc-image.image" width="400px" />

## About app testing
Once you have enabled user entitlement check for your app, you can test it using one of the following methods.
| **Prerequisite** | **Testing Method** |
| --- | --- |
| The app is not published on the PICO Store | Directly install the app's APK file to your PICO device for testing. |
| The app is published on the PICO Store | Following the steps below to skip the entitlement check. <br>  <br> 1. Upgrade the PICO device's system version to 5.6.0 or later. <br> 2. Add the testers as the members of your organization. Refer to the "[Manage organization members](/document/distribute/manage-member/)" article for complete steps. <br>  <br> Otherwise, you need to test your app by installing the APK file through the test channel and opening it on your PICO device. |


# --- END: Entitlement check.md ---



# --- BEGIN: Ergonomics & device limitations.md ---

Designing reasonable and comfortable hand poses requires an understanding of hand-related ergonomics. Additionally, the device's hand tracking capability itself has limitations, and it is crucial to be aware of these limitations in order to develop effective solutions.
## Ergonomics
To ensure a good user experience, the hand poses need to be in line with hand-related ergonomics. Therefore, when designing hand poses, you need to look into the hand's favorable working area, range of motion, optimal operating direction, and more. 
> A book for further information on the topic: *Human Dimension and Interior Space*.

## Limitations
PICO devices support recognizing users' hand poses within a limited range. Therefore, users' hands should be within the range for their hand poses to be recognized.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e038463e5d54be689443178b0d76619~tplv-goo7wpa0wc-image.image" width="700px" />

Below are detailed specifications on PICO's hand pose recognition range:
| **Depth & Orientation** | **Recognition Spec** | **Remarks** |
| --- | --- | --- |
| Depth | 152mm～500mm | If the hands are too far from the device or too close to the body, the device can not recognize hand poses. |
| Upwards | 57.5° | If the hands are lifted too high or put too low, the device can not recognize hand poses. |
| Downwards | 72.5° |  |
| Leftwards | 61.5° | When the angle between the hand and the device is too large, the device can not recognize hand poses. <br>  |
| Rightwards | 60.5° |  |
Obstructions between hand joints can hinder accurate recognition of hand poses by the camera, leading to a poor user experience. Therefore, when designing hand poses, it is advisable to minimize obstruction of the hand joints, such as avoiding dual-hand or single-hand obstructions.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e44e31337bb84b74bb016ebd4e1411d9~tplv-goo7wpa0wc-image.image" width="600px" />


# --- END: Ergonomics & device limitations.md ---



# --- BEGIN: Exercise data authorization.md ---

Exercise Data Authorization provides multiple APIs for you to access users' exercise data from the built-in PICO app — PICO Fitness.
When users are working out with PICO VR headsets, the app records their exercise data, including exercise duration, calories burned, exercise plan, preferences, and more.
With the APIs provided by the service, you can gather data to understand the exercise habits of individuals, thereby providing users with a better exercise experience.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e974e3073ed64d0f89dc8b4ed65d2ef5~tplv-em5hxbkur4-noop.image?width=599&height=362" width="488px" />

## Basic concepts
| **Name** | **Description** |
| --- | --- |
| PICO Fitness | A built-in app in the PICO system to help users manage their exercise program. |
| Exercise plan | The exercise plan set by the user at PICO Fitness, including the exercise duration, the planned calorie to burn, the planned exercise days per week, etc. |
| Sport level | Users' exercise intensity, which ranges from "low", "medium" to "high". |
| Sport target | The exercise goal the user wants to achieve, either "Fat Loss" or "Keep Fit". |
## Key features
You will need to obtain user authorization for API access. If not, the user will be prompted for authorization when you call relevant APIs.

* To request permission from users to access their PICO Fitness data, you can call `UserService.RequestUserPermissions`.
* To view the list of authorized permissions, you can call `UserService.GetAuthorizedPermissions`.

### Get user details and exercise plan
You can call `SportService.GetUserInfo` to get a user's basic information and exercise plan, including gender, age, height, weight, sport level, planned daily exercise hours, planned exercise days per week, exercise target, and more.
### Get today's exercise data
You can call `SportService.GetSummary` to get a summary of a user's exercise data for a specified period within today. That is, the starting point of the query **should be less than 24 hours** from the query occurred. The exercise data returned includes the actual exercise duration and the actual calories burned.
### Get daily exercise data
You can call `SportService.GetDailySummary` to get a summary of a user's daily exercise data for a specified period within the recent 90 days. That is, the starting point of the query **should be less than 90 days** from the query occurred. The exercise data returned includes actual daily exercise duration (in seconds), the planned daily exercise duration (in minutes), the planned daily calories to burn, and the actual daily calorie burned.
## Implementation workflow
### Complete basic setups
Refer to the "[Platform services overview](/en_platform-services-overview#712343ad)" article to complete all required setups, including adding an app ID, initializing platform services, etc.
### Apply for an access
Sport service is currently for experimental use. You will need to submit your app ID to the PICO team for access. Your access will take effect once granted.
### Implement APIs
You can implement `SportService` APIs in your app.
## Demo
You can use the SportCenter demo to debug exercise data authorization-related APIs. For more information, refer to the "[Exercise data authorization demo](/en_sports-demo)" article.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/6f6c9d888ead47dfbdc6dd9b08d84c4f~tplv-em5hxbkur4-noop.image?width=2332&height=1198" width="700px" />

## API reference
For more information about sport-related APIs, refer to the [API reference](/reference/unity/client-api/SportService/).


# --- END: Exercise data authorization.md ---



# --- BEGIN: Highlights.md ---

Highlight service is used to record users' amazing moments while using your app. Users can save these moments as images or videos, review and share them later. Below are the main features of the highlights service:

* **Record highlights**: Provides APIs for capturing and recording the screen to generate images or videos of highlights;
* **Share highlights**: Provides the highlights-sharing API that allows users to preview these amazing moments on the highlights preview UI. Users can save images or videos and directly share them to the "Douyin" app through the HMD. Alternatively, they can share the content to the "PICO VR" app on the mobile phone first and then further share it to the "WeChat" app through the "PICO VR" app.

## Basic concepts
| **Name** | **Description** |
| --- | --- |
| Session | Users can only capture or record the screen in a session. You can retrieve the images and videos for a specified session. |
| Job ID | Each screen capturing or screen recording generates a file with a globally unique Job ID. |
| Cross-platform sharing | Share images or videos from the PICO device to the PICO VR app on a mobile phone. |
## Important note
Currently, the highlight service is only available to apps submitted to the PICO Store (Chinese Mainland).
## Prerequisite
The version of the SDK should be 2.3.0 or later.
## Procedure
### Step 1: Complete general setups
Refer to the "[Platform services overview](/en_platform-services-overview)" article to complete general setups, including registering on the PICO Developer Platform, importing the SDK, completing project settings in the Unity Editor, initializing platform services, and more.
### Step 2: Enable the Highlight service on the PICO Developer Platform

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/organization/).
2. Navigate to the **Overview** screen of your app.
3. From the left navigation panel, select **Platform Service** > **Highlight**.
4. On the **Highlight** screen, click the **Start Service** button.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca6e6d21fbda41ac8f313a3ce93cde39~tplv-goo7wpa0wc-image.image)
5. On the **Start Service** pop-up window, enter the application scenarios of the Highlight service for your app, then click the **Confirm** button. 
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6f5b3648ad64f73a472243b2fc38ed4~tplv-goo7wpa0wc-image.image)
   The platform then enables the Highlight service for your app.

### Step 3: Enable the Highlight service in Unity

1. Open your project in the Unity Editor.
2. From the top menu bar, select **PICO** > **Platform Settings**.
3. On the **PICO Platform Settings** window, check the **Use Highlight** checkbox and click **Apply**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d718af1ac0454ec882f835cde0ef896f~tplv-goo7wpa0wc-image.image)
   Once enabled, the SDK automatically writes the following metadata into your app's AndroidManifest.xml file:
   ```XML
   <meta-data android:name="use_record_highlight_feature" android:value="true" />
   ```

### Step 4: Implement the Highlight service
Call APIs to implement the Highlight service in your app. Below is the workflow:

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIzNTNweCIgaGVpZ2h0PSI4OTVweCIgdmlld0JveD0iLTAuNSAtMC41IDM1MyA4OTUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDE0NyAyNTIgTCAxNDcgMjg1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTQ3IDI5MC44OCBMIDE0My41IDI4My44OCBMIDE0NyAyODUuNjMgTCAxNTAuNSAyODMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDE0NyAzNTIgTCAxNDcgMzg1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTQ3IDM5MC44OCBMIDE0My41IDM4My44OCBMIDE0NyAzODUuNjMgTCAxNTAuNSAzODMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyOTIiIHdpZHRoPSIyOTAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDI4OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMyMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+Q2FsbMKgPGNvZGU+PGZvbnQgZmFjZT0iSGVsdmV0aWNhIj5IaWdobGlnaHRTZXJ2aWNlLlN0YXJ0U2Vzc2lvbjwvZm9udD48L2NvZGU+PC9kaXY+PHNwYW4+PC9zcGFuPjwvZGl2PjxzcGFuPjwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTQ3IDQ2MiBMIDE0NyA0OTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNDcgNTAwLjg4IEwgMTQzLjUgNDkzLjg4IEwgMTQ3IDQ5NS42MyBMIDE1MC41IDQ5My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjM5MiIgd2lkdGg9IjI5MCIgaGVpZ2h0PSI3MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjg4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDI3cHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+PGRpdj48ZGl2PjxkaXY+Q2FsbCA8Y29kZT48Zm9udCBmYWNlPSJIZWx2ZXRpY2EiPkhpZ2hsaWdodFNlcnZpY2UuQ2FwdHVyZVNjcmVlbjwvZm9udD48L2NvZGU+LCA8Y29kZT48Zm9udCBmYWNlPSJIZWx2ZXRpY2EiPkhpZ2hsaWdodFNlcnZpY2UuU3RhcnRSZWNvcmQ8L2ZvbnQ+PC9jb2RlPiwgYW5kIDxjb2RlPjxmb250IGZhY2U9IkhlbHZldGljYSI+SGlnaGxpZ2h0U2VydmljZS5TdG9wUmVjb3JkPC9mb250PjwvY29kZT48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxNDcgNTYyIEwgMTQ3IDU5NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE0NyA2MDAuODggTCAxNDMuNSA1OTMuODggTCAxNDcgNTk1LjYzIEwgMTUwLjUgNTkzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iNTAyIiB3aWR0aD0iMjkwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1MzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PkNhbGzCoDxjb2RlPjxmb250IGZhY2U9IkhlbHZldGljYSI+SGlnaGxpZ2h0U2VydmljZS5MaXN0TWVkaWE8L2ZvbnQ+PC9jb2RlPjwvZGl2PjxzcGFuPjwvc3Bhbj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxNDcgNjgyIEwgMTQ3IDcxNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE0NyA3MjAuODggTCAxNDMuNSA3MTMuODggTCAxNDcgNzE1LjYzIEwgMTUwLjUgNzEzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iNjAyIiB3aWR0aD0iMjkwIiBoZWlnaHQ9IjgwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA2NDJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PjxkaXY+PGRpdj5DYWxsIDxjb2RlPjxmb250IGZhY2U9IkhlbHZldGljYSI+SGlnaGxpZ2h0U2VydmljZS5TYXZlTWVkaWE8L2ZvbnQ+PC9jb2RlPsKgb3LCoDwvZGl2PjxkaXY+PGZvbnQgZmFjZT0iSGVsdmV0aWNhIj48Y29kZT48Zm9udCBmYWNlPSJIZWx2ZXRpY2EiPkhpZ2hsaWdodFNlcnZpY2UuU2hhcmVNZWRpYTwvZm9udD48L2NvZGU+wqA8L2ZvbnQ+PC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjwvZGl2PjwvZGl2PjxzcGFuPjwvc3Bhbj48ZGl2PjxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDIyMiA3NjIgTCAzNDIgNzYyIEwgMzQyIDMyMiBMIDI5OC4zNyAzMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyOTMuMTIgMzIyIEwgMzAwLjEyIDMxOC41IEwgMjk4LjM3IDMyMiBMIDMwMC4xMiAzMjUuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxlbGxpcHNlIGN4PSIxNDciIGN5PSI4NjciIHJ4PSI1NSIgcnk9IjI1IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA4NjdweDsgbWFyZ2luLWxlZnQ6IDkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkVuZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxNDcgODAyIEwgMTQ3IDgzNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE0NyA4NDAuODggTCAxNDMuNSA4MzMuODggTCAxNDcgODM1LjYzIEwgMTUwLjUgODMzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDgyMHB4OyBtYXJnaW4tbGVmdDogMTU2cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+Tm88L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTQ3IDcyMiBMIDIyMiA3NjIgTCAxNDcgODAyIEwgNzIgNzYyIFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzYycHg7IG1hcmdpbi1sZWZ0OiA3M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Db250aW51ZSB1c2luZyB0aGUgYXBw77yfPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyNjIiIHk9Ijc0MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzUycHg7IG1hcmdpbi1sZWZ0OiAyODJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5ZZXM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTQ3IDE0MiBMIDE0NyAxODUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNDcgMTkwLjg4IEwgMTQzLjUgMTgzLjg4IEwgMTQ3IDE4NS42MyBMIDE1MC41IDE4My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMTQ3IDUyIEwgMTQ3IDg1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTQ3IDkwLjg4IEwgMTQzLjUgODMuODggTCAxNDcgODUuNjMgTCAxNTAuNSA4My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxlbGxpcHNlIGN4PSIxNDciIGN5PSIyNyIgcng9IjU1IiByeT0iMjUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI3cHg7IG1hcmdpbi1sZWZ0OiA5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TdGFydDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMiIgeT0iMTkyIiB3aWR0aD0iMjkwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMjJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PkNhbGzCoDxjb2RlPjxmb250IGZhY2U9IkhlbHZldGljYSI+VXNlclNlcnZpY2UuUmVxdWVzdFVzZXJQZXJtaXNzaW9uczwvZm9udD48L2NvZGU+PC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMiIgeT0iOTIiIHdpZHRoPSIyOTAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDI4OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+SUluaXRpYWxpemUgcGxhdGZvcm0gc2VydmljZXM8L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxGraphModel&quot;:{&quot;dx&quot;:&quot;782&quot;,&quot;dy&quot;:&quot;466&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;tooltips&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;arrows&quot;:&quot;1&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;pageHeight&quot;:&quot;1169&quot;},&quot;mxCellMap&quot;:{&quot;Xfazc13W&quot;:{&quot;id&quot;:&quot;Xfazc13W&quot;},&quot;Pect1uf9&quot;:{&quot;id&quot;:&quot;Pect1uf9&quot;,&quot;parent&quot;:&quot;Xfazc13W&quot;},&quot;i8qHZPoR&quot;:{&quot;id&quot;:&quot;i8qHZPoR&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;1YsaLu92&quot;,&quot;target&quot;:&quot;9LkOZxZ2&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;265&quot;,&quot;y&quot;:&quot;270&quot;,&quot;as&quot;:&quot;sourcePoint&quot;}}},&quot;bRjlDSjK&quot;:{&quot;id&quot;:&quot;bRjlDSjK&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0.5;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;9LkOZxZ2&quot;,&quot;target&quot;:&quot;YGVClKwk&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;9LkOZxZ2&quot;:{&quot;id&quot;:&quot;9LkOZxZ2&quot;,&quot;value&quot;:&quot;Call <code><font face=\&quot;Helvetica\&quot;>HighlightService.StartSession</font></code>&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;290&quot;,&quot;width&quot;:&quot;290&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;1AspmTkR&quot;:{&quot;id&quot;:&quot;1AspmTkR&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0.5;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;YGVClKwk&quot;,&quot;target&quot;:&quot;gHLA2FBg&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;YGVClKwk&quot;:{&quot;id&quot;:&quot;YGVClKwk&quot;,&quot;value&quot;:&quot;Call <code><font face=\&quot;Helvetica\&quot;>HighlightService.CaptureScreen</font></code>, <code><font face=\&quot;Helvetica\&quot;>HighlightService.StartRecord</font></code>, and <code><font face=\&quot;Helvetica\&quot;>HighlightService.StopRecord</font></code>&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;390&quot;,&quot;width&quot;:&quot;290&quot;,&quot;height&quot;:&quot;70&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;clPltVfW&quot;:{&quot;id&quot;:&quot;clPltVfW&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;gHLA2FBg&quot;,&quot;target&quot;:&quot;gcaALKFo&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;gHLA2FBg&quot;:{&quot;id&quot;:&quot;gHLA2FBg&quot;,&quot;value&quot;:&quot;Call <code><font face=\&quot;Helvetica\&quot;>HighlightService.ListMedia</font></code>&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;500&quot;,&quot;width&quot;:&quot;290&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;YnEkf4f0&quot;:{&quot;id&quot;:&quot;YnEkf4f0&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;gcaALKFo&quot;,&quot;target&quot;:&quot;pSOcmWHy&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;gcaALKFo&quot;:{&quot;id&quot;:&quot;gcaALKFo&quot;,&quot;value&quot;:&quot;Call <code><font face=\&quot;Helvetica\&quot;>HighlightService.SaveMedia</font></code> or <font face=\&quot;Helvetica\&quot;><code><font face=\&quot;Helvetica\&quot;>HighlightService.ShareMedia</font></code> </font>&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;600&quot;,&quot;width&quot;:&quot;290&quot;,&quot;height&quot;:&quot;80&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;K1xJa0cT&quot;:{&quot;id&quot;:&quot;K1xJa0cT&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;340&quot;,&quot;y&quot;:&quot;760&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;410&quot;,&quot;y&quot;:&quot;320&quot;,&quot;as&quot;:&quot;targetPoint&quot;},&quot;-2-Array&quot;:{&quot;as&quot;:&quot;points&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;460&quot;,&quot;y&quot;:&quot;760&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;460&quot;,&quot;y&quot;:&quot;320&quot;},&quot;-2-mxPoint&quot;:{&quot;x&quot;:&quot;410&quot;,&quot;y&quot;:&quot;320&quot;}}}},&quot;DxwOrE85&quot;:{&quot;id&quot;:&quot;DxwOrE85&quot;,&quot;value&quot;:&quot;End&quot;,&quot;style&quot;:&quot;ellipse;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;oval&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;210&quot;,&quot;y&quot;:&quot;840&quot;,&quot;width&quot;:&quot;110&quot;,&quot;height&quot;:&quot;50&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;k4KvkUnc&quot;:{&quot;id&quot;:&quot;k4KvkUnc&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0.5;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;pSOcmWHy&quot;,&quot;target&quot;:&quot;DxwOrE85&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;CCJqPpSz&quot;:{&quot;id&quot;:&quot;CCJqPpSz&quot;,&quot;value&quot;:&quot;No&quot;,&quot;style&quot;:&quot;edgeLabel;html=1;align=center;verticalAlign=middle;resizable=0;points=[];&quot;,&quot;parent&quot;:&quot;k4KvkUnc&quot;,&quot;connectable&quot;:&quot;0&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;-0.24&quot;,&quot;y&quot;:&quot;2&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;6&quot;,&quot;y&quot;:&quot;2&quot;,&quot;as&quot;:&quot;offset&quot;}}},&quot;pSOcmWHy&quot;:{&quot;id&quot;:&quot;pSOcmWHy&quot;,&quot;value&quot;:&quot;Continue using the app？&quot;,&quot;style&quot;:&quot;rhombus;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Diamond&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;190&quot;,&quot;y&quot;:&quot;720&quot;,&quot;width&quot;:&quot;150&quot;,&quot;height&quot;:&quot;80&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;IK6cTs2c&quot;:{&quot;id&quot;:&quot;IK6cTs2c&quot;,&quot;value&quot;:&quot;Yes&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;380&quot;,&quot;y&quot;:&quot;740&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;iTZJCLRE&quot;:{&quot;id&quot;:&quot;iTZJCLRE&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;target&quot;:&quot;1YsaLu92&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;265&quot;,&quot;y&quot;:&quot;140&quot;,&quot;as&quot;:&quot;sourcePoint&quot;}}},&quot;ETSTPx8T&quot;:{&quot;id&quot;:&quot;ETSTPx8T&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;hlGzyWgX&quot;,&quot;target&quot;:&quot;5oUw5WPQ&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;hlGzyWgX&quot;:{&quot;id&quot;:&quot;hlGzyWgX&quot;,&quot;value&quot;:&quot;Start&quot;,&quot;style&quot;:&quot;ellipse;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;oval&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;210&quot;,&quot;width&quot;:&quot;110&quot;,&quot;height&quot;:&quot;50&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;1YsaLu92&quot;:{&quot;id&quot;:&quot;1YsaLu92&quot;,&quot;value&quot;:&quot;Call <code><font face=\&quot;Helvetica\&quot;>UserService.RequestUserPermissions</font></code>&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;190&quot;,&quot;width&quot;:&quot;290&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;5oUw5WPQ&quot;:{&quot;id&quot;:&quot;5oUw5WPQ&quot;,&quot;value&quot;:&quot;IInitialize platform services&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;120&quot;,&quot;y&quot;:&quot;90&quot;,&quot;width&quot;:&quot;290&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}}},&quot;mxCellList&quot;:[&quot;Xfazc13W&quot;,&quot;Pect1uf9&quot;,&quot;i8qHZPoR&quot;,&quot;bRjlDSjK&quot;,&quot;9LkOZxZ2&quot;,&quot;1AspmTkR&quot;,&quot;YGVClKwk&quot;,&quot;clPltVfW&quot;,&quot;gHLA2FBg&quot;,&quot;YnEkf4f0&quot;,&quot;gcaALKFo&quot;,&quot;K1xJa0cT&quot;,&quot;DxwOrE85&quot;,&quot;k4KvkUnc&quot;,&quot;CCJqPpSz&quot;,&quot;pSOcmWHy&quot;,&quot;IK6cTs2c&quot;,&quot;iTZJCLRE&quot;,&quot;ETSTPx8T&quot;,&quot;hlGzyWgX&quot;,&quot;1YsaLu92&quot;,&quot;5oUw5WPQ&quot;]},&quot;lastEditTime&quot;:0,&quot;snapshot&quot;:&quot;&quot;}" />

Below is the implementation procedure:

1. Call `UserService.RequestUserPermissions` to request screen capturing and recording permission from the user.
2. Call `HighlightService.StartSession` to start a new session. 

  The request returns a string type session ID. All images and videos will be recorded in this session.

3. Call `HighlightService.CaptureScreen`, `HighlightService.StartRecord`, and `HighlightService.StopRecord` to enable users to capture and record the screen as well as stop recording.
   The maximum recording time for a video is 15 minutes. If `StopRecord()` is not called within the 15-minute timeframe or if the screen recording is terminated due to other reasons, the system will automatically end the recording and return information such as the video's path, Job ID, and video size.

4. Call `HighlightService.ListMedia` to retrieve all images and videos for the current session.
   You need to create the highlights preview UI.

5. Call `HighlightService.SaveMedia` to enable users to save images and videos to the local album, or call `HighlightService.ShareMedia` to enable users to share these highlights to social media.
   Users can share only one image or video per time.

## Demo
The HighlightsDemo demonstrates the features of the highlights service, including screen capturing, screen recording, cross-platform sharing, and more. For more information on the demo, refer to the "[Highlights demo](/en_highlights-demo)" article.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50a345b78c304157b63f2e5ef9cb77d8~tplv-goo7wpa0wc-image.image" width="550px" />

## API reference
The following table lists highlights service functions. For details on parameters, returns, and more, refer to the [API reference](/reference/unity/client-api/HighlightService/).
| **Function** | **Description** |
| --- | --- |
| `HighlightService.StartSession` | Start a new session. |
| `HighlightService.CaptureScreen` | Capture the current screen. |
| `HighlightService.StartRecord` | Start recording the screen. |
| `HighlightService.StopRecord` | Stop recording the screen. |
| `HighlightService.ListMedia` | List all images and videos for a specified session. |
| `HighlightService.SaveMedia` | Save an image or a video to the local album. |
| `HighlightService.ShareMedia` | Share an image or a video on social media. |
| `HighlightService.SetOnRecordStopHandler` | A callback function. After the recording is terminated, it returns the information about the video, such as the video's path, Job ID, and video size. |


# --- END: Highlights.md ---



# --- BEGIN: How can I test my apps on PICO Neo 3 for PICO Neo 3 Link_.md ---

* Option 1: Install a Firmware (with PUI version 4.70) which includes OOPC. You can request it from your POC.
* Option 2: Upload your app to the console and the PICO QA team will test it and provide a report.


# --- END: How can I test my apps on PICO Neo 3 for PICO Neo 3 Link_.md ---



# --- BEGIN: Implement the Leaderboard service.md ---

This article introduces the procedure for implementing the Leaderboard service into your app.
## Important note
Testing the Leaderboard service is currently not available in the Unity Editor.
## Prerequisites
Make sure you have imported the PICO Unity Integration SDK into your project and completed required project settings. If you haven't, refer to the following articles to complete these tasks:

* [Import the SDK](/en_import-the-sdk)
* [Complete project settings](/en_complete-project-settings)

## Procedure
### Step 1: Create leaderboards
Create one or more leaderboards for your app on the PICO Developer Platform and configure leaderboard details as needed.

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/organization/).
2. On the **My Apps** screen, click on the target app's card.
   This directs you to the app's **Overview** screen.
3. From the left navigation panel, select **Platform Services** > **Leaderboard**.
   This directs you to the **Leaderboard** screen.
4. Click the **Create Leaderboard** button. 
   This directs you to the following leaderboard creation screen.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/177526973e0e42adac323866cfe5f91b~tplv-goo7wpa0wc-image.image)
5. Select the country/region where the leaderboard is applied. 
6. Set the language of the leaderboard. 
7. Follow the on-screen instructions to complete leaderboard details. 
   | **Field** | **Description** |
   | --- | --- |
   | Display Name | The name of the leaderboard, which users can see in the app. |
   | API Name | The unique identifier of a leaderboard, which is referenced as the leaderboardName parameter in Leaderboard service-related APIs. |
   | Sort By | Defines by what order the entries are arranged. Available options are:  <br>  <br> * **High to low**: Arrange entries in descending order. In other words, the entry with the highest score appears at the top of the list, followed by entries with lower scores. Especially applicable for point-based apps.  <br> * **Low to high**: Arrange entries in asending order. In other words, the entry with the lowest score appears at the top of the list, followed by entries with higher scores. Especially applicable for racing games.  |
   | Type of Sorting Field | Defines by what dimension the entries are arranged, including **Distance (ft)**, **Distance (m)**, **Percentage**, **Score**, **Time (ms)**, and **Time (sec)**. Below are the types of apps that each type of sorting field is suitable for:  <br>  <br> * **Distance**: Arrange entries by distance (in meters or feet). Applicable for distance-based apps such as racing games with limits on time.  <br> * **Percentage**: Arrange entries by percentage. Applicable for apps that rank users by such dimensions as success/kill/hit rates.  <br> * **Score**: Arrange entries by point. Applicable for point-based apps such as collectible card games.  <br> * **Time**: Arrange entries by time (in seconds or milliseconds). Applicable for time-based apps such as racing games with limits on distance.  |
   | Data Write Permission | Defines who is allowed to write entries to the leaderboard:  <br>  <br> * **Writable on the client**: both the client (user) and the server.  <br> * **Writable on the server only**: the server only.  |
   | Associate Destination | Defines whether to associate a leaderboard with a destination (Level, Map, etc.). Once associated, users can jump to the destination from the leaderboard, and you need to design a button for the jump action on the leaderboard UI. Below are available options: <br>  <br> * **No** <br> * Display names of all destinations configured for the current app, in alphabetical order.  <br>  <br> ***Note***: If no destination is configured, only **No** will be available. For more information on creating a destination, refer to [this article](/en_social-interaction-platform-service-setups#1dd5698d). |
   | Whether to enable friend leaderboard | Once enabled, users can view the rankings of their friends on this leaderboard. |
   | Whether to enable notification | If friend leaderboard is enabled, you can choose whether to enable notification. Once enabled, users will receive notifications in their device's notification center when they are surpassed by their friends. By clicking the notification area, the system will launch the corresponding app and direct the user to it. |
8. Click the **Save** button.

Do not close the webpage, you need to proceed to enable the Matchmaking service for your app.
### Step 2: Enable the Matchmaking service
Use the following steps to enable the Matchmaking service for your app.

1. From the left navigation panel, select **Platform Service** > **Matchmaking**.
   This directs you to the following screen:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed85becc19894427b9e006377b0e7740~tplv-goo7wpa0wc-image.image)
2. Select the store region to enable service for: **Chinese Mainland** or **Non-Chinese Mainland**.
3. Click **Start Service**.
   The following pop-up window appears:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/22bf8b5eed9a4a489c5d4d80bb66980e~tplv-em5hxbkur4-noop.image?width=900&height=384)
4. Click **OK**.
   The platform starts to enable Matchmaking service for your app.

### Step 3: Initialize platform services globally and the game module

* Initialize platform services globally. You can call `CoreService.Initialize()` for synchronous initialization or call `CoreService.AsyncInitialize()` for asynchronous initialization.
* Call `CoreService.GameInitialize` to initialize the game module.

For detailed instructions and code samples, refer to the "[Initialization](/en_initialization)" article.
### Step 4: Implement the Leaderboard service
Call APIs to implement the Leaderboard service in your app.
The following table lists the client APIs packaged in the `LeaderboardService` class. For more details about these APIs, refer to the [client API reference](/reference/unity/latest/LeaderboardService/). For use cases and code samples, refer to [this article](/en_leaderboards-use-cases-and-code-samples).
| **API** | **Description** |
| --- | --- |
| LeaderboardService.Get | Get the information about a specified leaderboard. |
| LeaderboardService.GetEntries | Get leaderboard entries, including the total number of entries, entry ID, score, extra information, rank, and more. |
| LeaderboardService.GetEntriesAfterRank | Get the entries after a specified rank. |
| LeaderboardService.GetEntriesByIds | Get the entries for specified users on a specific leaderboard. |
| LeaderboardService.WriteEntry | Write an entry to a leaderboard. |
| LeaderboardService.WriteEntryWithSupplementaryMetric | Write an entry to a leaderboard. The entry can contain supplementary metrics for the tiebreaker. |
Below are server APIs. For details, refer to the [server API reference](/reference/unity-server/latest/create-or-modify-leaderboard/).

* Create or modify a leaderboard
* Get leaderboard details
* Get all the leaderboards in an app
* Delete a specific leaderboard
* Create or modify a leaderboard entry
* Get leaderboard entries
* Delete a specified entry for a leaderboard
* Delete all entries for a leaderboard

## FAQ
**How to specify a "Chinese Mainland"/"Non-Chinese Mainland" leaderboard when they have the same API name?** 
When creating leaderboards for Chinese Mainland and Non-Chinese Mainland on the PICO Developer Platform, you are able to use the same API name for a leaderboard in both regions. In other words, if you create two leaderboards, one for Chinese Mainland and the other for Non-Chinese Mainland, you can set a same API name for both of them. 
In this case, if you call client APIs, the SDK will query the corresponding leaderboard based on the region where the logged-in account is based. If you call server APIs, the system will query the corresponding leaderboard based on the domain name.


# --- END: Implement the Leaderboard service.md ---



# --- BEGIN: Implement the social intraction experience.md ---

This article introduces how to implement the social interaction experience in your app.
## Prerequisites
Make sure you have imported the PICO Unity Integration SDK into your project and completed required project settings. If you haven't, refer to the following articles to complete these tasks:

* [Import the SDK](/en_import-the-sdk)
* [Complete project settings](/en_complete-project-settings)

## Procedure
### Step 1: Create destinations
You can create one or multiple destinations for your app on the PICO Developer Platform and set destination details such as images, descriptions, and deep linking. 

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/organization/).
2. From the left navigation panel, select **My Apps**.
   This directs you to the **My Apps** screen.
3. Click on the target app.
   This directs you to the app's **Overview** screen.
4. From the left navigation panel, select **Platform Services** > **Destinations**.
   This directs you to the **Destinations** screen.
5. Click **Create Destination**.
   This directs you to the destination configuration screen.
6. Select the country/region where the destination is applied.
7. Complete destination details, including **Basic Information** and **Developer Information**.
   After you complete the required fields on the **Basic Information** panel, the tiny circle on the selected language's cube becomes green.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/791d348818104275907c5f10d1ef4946~tplv-goo7wpa0wc-image.image)
   Below are field descriptions for the basic information:
   | **Field** | **Description** |
   | --- | --- |
   | + Manage Languages | Set languages for the destination's basic information. |
   | Display Name | The display name of the destination. Used to present to users in your app. |
   | Description | The description of the destination. Used to present to users in your app. |
   | Image Information | The image of the destination. Used to present to users in your app. |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2a524353bd941feb0ee6987a9129417~tplv-goo7wpa0wc-image.image)
   Below are field descriptions for the developer information:
   | **Field** | **Description** |
   | --- | --- |
   | API Name | The unique identifier of the destination, which can be any combination of letters, digits, and underscores (_). |
   | DeepLink Message | Used to store dynamic configurations. Below is an example: <br> ```JSON <br> {"room_name":"sports game","game_type":"pingpong","game_level":"easy"} <br> ``` <br>  |
   | Whether to enable DeepLink | When you choose "Yes", users can be directed to the target destination via the deep linking capability. |
   | Visible Scope | Set whom the destination is visible to. The options are: <br>  <br> * Developers Only: the destination is only visible to yourself. <br> * All: the destination is visible to all PICO users. |
8. Click **Save** or **Save and Submit**. 
   * If you click **Save**, the destination will enter the "Draft" state. 
   * If you click **Save and Submit**, the destination will enter the "Under Review" state.

### Step 2: Upload a build 
When a user accepts an invitation, the device parses the app package name in the invitation, then launches and directs the user to the corresponding app. To make this happen, you need to upload a build for your app on the PICO Platform. See [this article](/document/distribute/upload-a-build/) for detailed instructions.
### Step 3: Initialize platform services
Initialize platform services globally. You can call `CoreService.Initialize()` for synchronous initialization or call `CoreService.AsyncInitialize()` for asynchronous initialization. For detailed instructions and code samples, refer to the "[Initialization](/en_initialization)" article.
### Step 4: Implement the social interaction experience
Call APIs to implement the social interaction experience in your app, including inviting friends, jumping across different apps, sharing content on social platforms, and more.

* For use cases and code samples, refer to [this article](/en_social-interaction-use-cases).
* For available APIs, refer to [this article](/en_social-interaction-api-list).


# --- END: Implement the social intraction experience.md ---



# --- BEGIN: Improve microphone-related designs.md ---

Audio communication is one of the most fundamental and important app services. PICO apps use users' microphones to capture human voices and environmental sounds, which touches audio data privacy. Therefore, while using audio-related services, users care a lot about how and when their audio data is captured, including when to turn on the microphone, how the status of the microphone is displayed, and how to control the microphone. This article provides best practices for microphone-related designs.
## Core purposes
This article aims to help you realize the following purposes through good microphone-related designs:

* Let users clearly know when and how the microphone will be used in your app.
* Let users clearly know their microphone's status, especially when the microphone is on.
* Let users easily turn their microphones on/off.
* Let users clearly know how the captured audio data is further processed, for example, whether the data will be uploaded to the server for processing.

## Must-follow rules
Follow the rules given below while designing microphone-related services for your app:

* **Off by default & always ask**
   The microphone should be off by default every time a user enters a scene or uses an audio-related functionality. You can also add some prompts to ask users whether they would like to turn on the microphone.
* **Follow user's choice**
   If a user has turned off microphone permissions, the microphone should always be off. Never turn on the microphone without the user's permission.

## Best practices
This part walks you through the best practices for microphone-related design from three aspects: microphone permission authorization, microphone status control and display, and SDK-related practice.
### Microphone permission authorization
Let users control the microphone permission. You can add prompts when asking for permission.
#### Add authorization prompts
Make sure that users receive clear prompts when your app asks for the microphone permission. You can use **layer masks**, **toast notifications**, **pop-ups**, and any other formats that you think can give users clear prompts. Meanwhile, you need to make the prompts appear when and where microphone is needed for users to normally experience your app, so that users know what is going to happen. As shown in the figure below, a pop-up shows up when a user clicks on the microphone button.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/43ff8ea5c7744987940c2284f0f9cd7a~tplv-em5hxbkur4-noop.image?width=3249&height=910" width="800px" />

#### Clarify why to use the microphone
**Tell users why the microphone permission is needed in the prompt**. For example, users may not know what is going to happen after clicking the Join Room button. You therefore need to tell users why your app asks for microphone permission in the prompt.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/9a84bfb781bf449bbabd5a1bb93f52d6~tplv-em5hxbkur4-noop.image?width=5043&height=910)
However, there can be exceptions. If users proactively apply for microphone permission, such as clicking the microphone icon for audio communication or clicking the record button to start audio/video recording, they clearly know what their microphone is for and you generally do not need to add such information in the prompt.
#### Important notes
The following notes are helpful for better designing microphone-related services:

* Try to avoid applying for microphone permission instantly after the app launches. This may not be applicable to audio-intensive apps such as music games.
* Do not apply for microphone permission when there is no microphone-related service.
* If users reject authorization, this should not stop you from providing users with microphone-free functionalities.
* If users reject authorization, users should not be forced to quit the app or be unable to perform other operations in the app.
* Authorizing microphone permission does not necessarily mean that users allow your app to turn on their microphone. In most cases, the microphone should be off by default even if users have granted app permissions for their microphone. Make sure that users can decide whether to turn on the microphone and know what the microphone is for.

### Microphone status control & display
Make sure that users can control and know their microphone's status. This part provides some practices on how to achieve the above-mentioned purposes when users' microphone is on, in-use, or off.
#### On
**Let users decide whether to turn their microphone on**. You can:

* Provide an easy-to-find and easy-to-use UI element, such as a microphone icon.
* Bind the microphone functionality with a controller button so that users can turn their microphone on by simply clicking a specific controller button, which is quite similar to the design of walkie talkies.

**Display a clear prompt when users' microphone is on**. This can not only let users know that the app is going to capture audio data which touches data privacy, but also prevent users from conducting meaningless microphone tests. You can design visual or audio prompts and below are detailed descriptions:
| **Prompt Type** | **Description** |
| --- | --- |
| Visual | Use the visual elements that users are familiar with. For example, you can: <br>  <br> * Add a microphone icon within user's view and let users sense the change of microphone status by changing the icon's style or color. <br> * Use subtitles, toast notifications, or pop-ups to notify users. <br>  <br> ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/eb48389442ab4ae79a4d08468b60eb37~tplv-em5hxbkur4-noop.image?width=3249&height=910) |
| Auditory | Play sound effects such as the "drip" or "beep" sound. |
#### In-use
When users' microphone is in use, you can **provide a lasting visual element** that displays the microphone's status within users' view. Try the following:

* Add a volume indicator to the microphone icon displayed in the main view.
* Add an audio wave icon or other rhythmic graphics (as shown below) to continuously display the volume status and audio status. A well designed graphic can even become a unique visual element in your app. Additionally, you can also use texts, such as "Capturing audio data", to notify users.

One-time prompt may not be as effective as expected.

<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c91a663a392b49758c1484b03f09c459~tplv-em5hxbkur4-noop.image?width=3249&height=910" width="800px" />

#### Off
**Provide users with an easy-to-find and easy-to-use UI element**. Try the following:

* Enable users to turn their microphone off by clicking the microphone icon (the same one used to turn the microphone on) in the main view.

<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/edc1f426ad4f479e811acd6b04194ebf~tplv-em5hxbkur4-noop.image?width=3249&height=911" width="800px" />

* Involve users' body movements. Display the turn-off-microphone button when users move their body in a specific way. As shown in the figure below, the turn-off-microphone button will appear when users look down.

<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c4cb526ad77f4d0ca0f5ae91a1b7827f~tplv-em5hxbkur4-noop.image?width=3249&height=910" width="800px" />

If you are going to try another way, you need to make sure that users can get enough instructions and what users need to do is simple. It would be optimal to let the microphone button appear with one operation.
### SDK-related practice
When using platform capabilities such as RTC that require microphone permissions, it is necessary to pass the microphone's status information to the SDK in time, enabling the SDK to call microphone-related capabilities.


# --- END: Improve microphone-related designs.md ---



# --- BEGIN: In-app purchase (IAP).md ---

For regulatory reasons, games without gaming licenses issued by authorities in Mainland China are unable to access IAP service. This does not affect developers elsewhere.

You can diversify user experience and grow your revenue by selling products such as cosmetics, props, and coins/diamonds within your app. The PICO Unity Integration SDK provides In-App Purchase (IAP) service which enables users to purchase products within your app. The IAP service packages a series of payments systems such as Alipay, bank card, and Paypal, thereby providing you with a one-stop multi-payment-method solution.
## Basic concepts
| **Name** | **Description** |
| --- | --- |
| Add-ons | Products available for purchase in the PICO Store or the app. |
| In-App Purchase (IAP) | Purchases within the app. The products for in-app purchase must be created on the PICO Developer Platform. Common products are in-game cosmetics, props, and coins. |
| Consume | The fulfillment process for consumables. For example, if a user has purchased 100 coins, the third-party app should top up 100 coins to the user's account, after which the consumable order is determined as "fulfilled". Consumables can be purchased again only after the previous order has been fulfilled. |
| SKU | Stock keeping unit, which is the unique identifier of an add-on. An SKU corresponds to one add-on only. |
## Key features
Below is the overall workflow of in-app purchases:

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI0MTVweCIgaGVpZ2h0PSI1MjVweCIgdmlld0JveD0iLTAuNSAtMC41IDQxNSA1MjUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDE0MiA2MiBMIDE0MiAxMDUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNDIgMTEwLjg4IEwgMTM4LjUgMTAzLjg4IEwgMTQyIDEwNS42MyBMIDE0NS41IDEwMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjcyIiB5PSIyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiA3M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5UaGUgdXNlciBnZXRzIGEgbGlzdCBvZiBwdXJjaGFzYWJsZSBwcm9kdWN0czwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxNDIgMTcyIEwgMTQyIDIxNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE0MiAyMjAuODggTCAxMzguNSAyMTMuODggTCAxNDIgMjE1LjYzIEwgMTQ1LjUgMjEzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNzIiIHk9IjExMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNDJweDsgbWFyZ2luLWxlZnQ6IDczcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlRoZSB1c2VyIGxhdW5jaGVzIHRoZSBjaGVja291dCBmbG93IHRvIHB1cmNoYXNlIHRoZSB0YXJnZXQgcHJvZHVjdDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyMTIgMjUyIEwgMjU1LjYzIDI1MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI2MC44OCAyNTIgTCAyNTMuODggMjU1LjUgTCAyNTUuNjMgMjUyIEwgMjUzLjg4IDI0OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAxNDIgMjgyIEwgMTQyIDMyMiBMIDcyIDMyMiBMIDcyIDM0NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDcyIDM1MC44OCBMIDY4LjUgMzQzLjg4IEwgNzIgMzQ1LjYzIEwgNzUuNSAzNDMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI3MiIgeT0iMjIyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI1MnB4OyBtYXJnaW4tbGVmdDogNzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIHVzZXIgbWFrZXMgYSBwYXltZW50PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDE0MiAzMjIgTCAyMjIgMzIyIEwgMjIyIDM0NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIyMiAzNTAuODggTCAyMTguNSAzNDMuODggTCAyMjIgMzQ1LjYzIEwgMjI1LjUgMzQzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA3MiA0MTIgTCA3MiA0NTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MiA0NjAuODggTCA2OC41IDQ1My44OCBMIDcyIDQ1NS42MyBMIDc1LjUgNDUzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMzUyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM4MnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5UaGUgZGV2ZWxvcGVyIGZ1bGZpbGxzIHRoZSBvcmRlciBieSBkaXN0cmlidXRpbmcgdGhlIHByb2R1Y3QgdG8gdGhlIHVzZXIncyBhY2NvdW50PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSI0NjIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDkycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlRoZSB1c2VyIHJlY2VpdmVzIHRoZSBwcm9kdWN0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxNjIiIHk9IjM1MiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzODJweDsgbWFyZ2luLWxlZnQ6IDE2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5UaGUgdXNlciB2aWV3cyBhIGxpc3Qgb2YgcHVyY2hhc2VkIHByb2R1Y3RzwqDCoDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjYyIiB5PSIyMDIiIHdpZHRoPSIxNTAiIGhlaWdodD0iMTAwIiByeD0iMTUiIHJ5PSIxNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjUycHg7IG1hcmdpbi1sZWZ0OiAyNjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIHVzZXIgZmFpbHMgdG8gcHVyY2hhc2UgdGhlIHByb2R1Y3QsIHRoZSByZWFzb24gbWlnaHQgYmUgaW5zdWZmaWNpZW50IGJhbGFuY2Ugb3IgdGhhdCB0aGUgdXNlciBjYW5jZWxzIHRoZSBjaGVja291dCBmbG93wqA8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjE0MiIgeT0iMjkyIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMDJweDsgbWFyZ2luLWxlZnQ6IDE2MnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPlllczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjEyIiB5PSIyMzIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI0MnB4OyBtYXJnaW4tbGVmdDogMjMycHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+Tm88L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxCellList&quot;:[&quot;Xfazc13W&quot;,&quot;Pect1uf9&quot;,&quot;hCrJwlxf&quot;,&quot;35awTjAt&quot;,&quot;fge3RWjO&quot;,&quot;ZLMyLLy9&quot;,&quot;wtdhqHoF&quot;,&quot;d1hqfqPG&quot;,&quot;pktinpQP&quot;,&quot;92oSm25B&quot;,&quot;rKJ8f5wA&quot;,&quot;qIx1gZ6S&quot;,&quot;t2cevj9l&quot;,&quot;Y5hXoQHy&quot;,&quot;1Ot3yRS6&quot;,&quot;xoCnlGa8&quot;,&quot;QcEr2cGN&quot;],&quot;mxGraphModel&quot;:{&quot;arrows&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;dx&quot;:&quot;782&quot;,&quot;dy&quot;:&quot;416&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageHeight&quot;:&quot;1169&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;tooltips&quot;:&quot;1&quot;},&quot;mxCellMap&quot;:{&quot;1Ot3yRS6&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;100&quot;,&quot;width&quot;:&quot;150&quot;,&quot;x&quot;:&quot;530&quot;,&quot;y&quot;:&quot;280&quot;},&quot;id&quot;:&quot;1Ot3yRS6&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user fails to purchase the product, the reason might be insufficient balance or that the user cancels the checkout flow &quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;35awTjAt&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;140&quot;,&quot;x&quot;:&quot;340&quot;,&quot;y&quot;:&quot;80&quot;},&quot;id&quot;:&quot;35awTjAt&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user gets a list of purchasable products&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;92oSm25B&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-mxPoint&quot;:{&quot;as&quot;:&quot;sourcePoint&quot;,&quot;x&quot;:&quot;410&quot;,&quot;y&quot;:&quot;400&quot;},&quot;-1-mxPoint&quot;:{&quot;as&quot;:&quot;targetPoint&quot;,&quot;x&quot;:&quot;490&quot;,&quot;y&quot;:&quot;430&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;92oSm25B&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;value&quot;:&quot;&quot;},&quot;Pect1uf9&quot;:{&quot;id&quot;:&quot;Pect1uf9&quot;,&quot;parent&quot;:&quot;Xfazc13W&quot;},&quot;QcEr2cGN&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;480&quot;,&quot;y&quot;:&quot;310&quot;},&quot;id&quot;:&quot;QcEr2cGN&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;No&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;Xfazc13W&quot;:{&quot;id&quot;:&quot;Xfazc13W&quot;},&quot;Y5hXoQHy&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;140&quot;,&quot;x&quot;:&quot;430&quot;,&quot;y&quot;:&quot;430&quot;},&quot;id&quot;:&quot;Y5hXoQHy&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user views a list of purchased products  &quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;ZLMyLLy9&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;140&quot;,&quot;x&quot;:&quot;340&quot;,&quot;y&quot;:&quot;190&quot;},&quot;id&quot;:&quot;ZLMyLLy9&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user launches the checkout flow to purchase the target product&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;d1hqfqPG&quot;:{&quot;-0-mxGeometry&quot;:{&quot;-0-Array&quot;:{&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;410&quot;,&quot;y&quot;:&quot;400&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;340&quot;,&quot;y&quot;:&quot;400&quot;},&quot;as&quot;:&quot;points&quot;},&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;d1hqfqPG&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;pktinpQP&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;qIx1gZ6S&quot;,&quot;value&quot;:&quot;&quot;},&quot;fge3RWjO&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;fge3RWjO&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;ZLMyLLy9&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;pktinpQP&quot;,&quot;value&quot;:&quot;&quot;},&quot;hCrJwlxf&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;hCrJwlxf&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;35awTjAt&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;ZLMyLLy9&quot;,&quot;value&quot;:&quot;&quot;},&quot;pktinpQP&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;140&quot;,&quot;x&quot;:&quot;340&quot;,&quot;y&quot;:&quot;300&quot;},&quot;id&quot;:&quot;pktinpQP&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user makes a payment&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;qIx1gZ6S&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;140&quot;,&quot;x&quot;:&quot;270&quot;,&quot;y&quot;:&quot;430&quot;},&quot;id&quot;:&quot;qIx1gZ6S&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The developer fulfills the order by distributing the product to the user's account&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;rKJ8f5wA&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;rKJ8f5wA&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;qIx1gZ6S&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;t2cevj9l&quot;,&quot;value&quot;:&quot;&quot;},&quot;t2cevj9l&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;60&quot;,&quot;width&quot;:&quot;140&quot;,&quot;x&quot;:&quot;270&quot;,&quot;y&quot;:&quot;540&quot;},&quot;id&quot;:&quot;t2cevj9l&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;&quot;,&quot;value&quot;:&quot;The user receives the product&quot;,&quot;vertex&quot;:&quot;1&quot;},&quot;wtdhqHoF&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;relative&quot;:&quot;1&quot;},&quot;edge&quot;:&quot;1&quot;,&quot;id&quot;:&quot;wtdhqHoF&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;pktinpQP&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;target&quot;:&quot;1Ot3yRS6&quot;,&quot;value&quot;:&quot;&quot;},&quot;xoCnlGa8&quot;:{&quot;-0-mxGeometry&quot;:{&quot;as&quot;:&quot;geometry&quot;,&quot;height&quot;:&quot;20&quot;,&quot;width&quot;:&quot;40&quot;,&quot;x&quot;:&quot;410&quot;,&quot;y&quot;:&quot;370&quot;},&quot;id&quot;:&quot;xoCnlGa8&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;value&quot;:&quot;Yes&quot;,&quot;vertex&quot;:&quot;1&quot;}}},&quot;diagramType&quot;:&quot;flowchart&quot;,&quot;lastEditTime&quot;:0}" />

### Get purchasable add-ons
After creating add-ons for your app, you can call `GetProductsBySKU` to display these add-ons and their prices and currencies to users.
### Launch the checkout flow
You can call `LaunchCheckoutFlow2()` to let users launch the checkout flow to purchase an add-on. The price and currency of the add-on are required in the request. Therefore, before calling `LaunchCheckoutFlow2()`, you need to call `GetProductsBySKU` to get an add-on's price and currency.
For non-Mainland China apps, the system automatically matches the exchange rate code according to the currency used in the user's country/region, and then converts the price. In other words, even if you have set the currency to USD on the PICO Developer Platform, users in different countries/regions will pay with the converted local currency. Therefore, do not fix the currency in the code.
### Get purchased add-ons
After the purchase flow is complete, you can call `GetViewerPurchases` to display the list of purchased add-ons including consumables and durables to users.
### Fulfill orders
For consumables, you need to set up and implement the order fulfillment logic in your own service system. Take coins as an example. If you create an add-on called "10 coins" and a user purchases it, the service system should top up 10 coins to the user's account. You can call `ConsumePurchase` to record the order fulfillment result. After an order has been fulfilled, `GetViewerPurchases` no longer returns the relevant add-on.
## Implementation workflow
### Complete basic setups
Refer to the "[Platform services overview](/en_platform-services-overview#712343ad)" article to complete all required setups, including adding an app ID, initializing platform services, etc.
### Create an add-on
The app that an add-on is added to must be in the state of being reviewed or published; otherwise you are unable to submit the add-on.

On the PICO Developer Platform, you can create add-ons for your app and set desired add-on details such as name, sku, and type. Below are the steps to follow:

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/organization/).
2. On the **My Apps** screen, click on the target app's card.
   This directs you to the app's **Overview** screen.
3. From the left navigation panel, select **Monetization** > **Add-Ons **.
   You will enter the **Add-Ons** configuration page.
4. In the upper-right corner of the page, click the **Create Add-On** button.
   The **Create Add-On** window appears.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba1d1064cff64fcba89de5bf646d6f93~tplv-goo7wpa0wc-image.image)
5. Configure the add-on. 
   | **Field** | **Note** |
   | --- | --- |
   | SKU | Unique identifier of Add-on. SKU cannot be modified after creation. |
   | Add-On Type | Add-on types, including: <br>  <br> * **Durable**: A durable add-on is permanently available after one purchase, such as a game level. <br> * **Consumable**: A consumable can be repurchased, such as game coins. |
   | Name | Add-on name. |
   | Submission Region | Application stores where add-ons are published, including: <br>  <br> * **PICO Store (Outside Mainland China)** <br> * **PICO Store (Mainland China)** |
6. Click the **Create** button.
   The add-on has been created, and you have been taken to its configuration page.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/219751e04f944df7b126ed0e684961c6~tplv-goo7wpa0wc-image.image)
7. In the upper-right corner of the page, click the **Create New Version** button.
   The **Create Add-On** window is displayed on the page.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d6245eca42b43478e97c44b365a8a63~tplv-goo7wpa0wc-image.image)
8. Choose a creation method: **Use another submission as template** or **Create without template**.
9. Based on the selected creation method, click the **Next** or **Create** button.
   You will enter the configuration page for the add-on of this version.
10. Follow the on-screen instructions to configure the add-on of this version. The configuration items include: **Basic Information**, **Pricing**, **App Ratings**, **Images & Videos**, **DLC Files**, **Supplementary Materials**, and **Release**.
11. Click the **Go to submission** button.
   The add-on will be reviewed by PICO. Once approved, users can see this add-on in your app.

### Call APIs
You can implement in-app purchase APIs in your app.
```C#
//Get purchasable add-ons
Task<ProductList> GetProductsBySKU(string[] skus)
```

```C#
//Launch the checkout flow
Task<Purchase> LaunchCheckoutFlow2(Product product)
```

```C#
//Get purchased add-ons
Task<PurchaseList> GetViewerPurchases()
```

```C#
//Fulfill orders
Task ConsumePurchase(string sku)
```

## Update an add-on
After an add-on has passed review and gone live, to update this add-on's information, create a new version by following these steps:

1. Go to the **Add-Ons** page.
2. Find the add-on in the list with the status "Published" and then click the **View** button in the **Actions** column.
   You will enter the version display page of this add-on.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e5974dbd60f4c8397c70341d6c37d9c~tplv-goo7wpa0wc-image.image)
3. Click the **Create New Version** button in the upper-right corner.
   You will enter the edit page for this add-on version.
4. Set the information for this add-on version and save it.
5. Click the **Go to submission** button at the bottom.
   This  add-on version has entered the review process. After approval, the add-on's information within the app and in the PICO Store will be automatically updated to the latest version.

## Test IAP service
After creating and saving an add-on, you can use it to test if you can successfully run through IAP service. For an unsubmitted add-on, no matter the corresponding app is published or not, you can only test this add-on with your PICO developer account. For a submitted and approved add-on, you can only test it with a non PICO developer account.
### Methods
You can test add-ons using the IAP APIs or directly test them in the PICO Store. Below are detailed descriptions:
| **Method** | **Description** |
| --- | --- |
| Use APIs | You can use IAP APIs to get add-on data and then test the overall in-app purchase flow. Refer to the [API reference](https://pdocor.pico-interactive.com/reference/unity/platform/2.1.4/class_pico_1_1_platform_1_1_i_a_p_service.html) for more details. |
| Use the PICO Store | According to the country/region where the add-on is to be released, you can search for the add-on in the corresponding PICO Store for that country/region. The add-on can be accurately found and then displayed. You can then use the PICO Developer account that created the add-on to test the overall in-app purchase flow. |
### Notes
Pay attention to the following when testing IAP service:

* You must use real payment methods. For **Mainland China**, you can use Alipay or or other valid payment methods. For **elsewhere**, you can use Paypal or other valid payment methods.
* The testing price is the minimum payment amount supported by the local PICO Store.
* The revenue generated in the test goes to the organization that the PICO developer account belongs to.
* When testing an add-on, if the corresponding app has not been submitted, the platform will display the default app information such as app name, image, and video. This information will be automatically updated when the app is approved.
* After testing, if you want to officially release this add-on, you need to submit the add-on, and after approval, this add-on will be officially released.

### Testing price reference
When testing the IAP service, you can refer to the table below for the add-on's testing price you need to set.
| **Country/Region** | **Testing Price** |
| --- | --- |
| Mainland China | 0.1 CNY |
| Korea | 200 KRW |
| Japan | 2 JPY |
| United States | 0.01 USD |
| United Kingdom | 0.01 GBP |
| Australia | 0.05 AUD |
| Singapore | 0.05 SGD |
| Austria, Belgium, Cyprus, Croatia, Estonia, Finland, France, Germany, Greece, Ireland, Italy, Latvia, Lithuania, Luxembourg, Malta, Netherlands, Portugal, Slovakia, Slovenia, Spain. | 0.05 Euro |
| Bulgaria | 0.05 BGN |
| Czech | 0.5 CZK |
| Denmark | 0.1 DKK |
| Hungary | 5 HUF |
| Norway | 0.5 NOK |
| Poland | 0.1 PLN |
| Romania | 0.1 RON |
| Sweden | 0.5 SEK |
| Swiss | 0.05 CHF |
### Before you begin

* Go to the add-on's configuration screen and enable/disable **Payment Test**. If you enable the payment test, you can simulate the situation of successful payments. If you disable the payment test, you can simulate the situation of payment failures.
* (Optional) If you would like to test the add-on in the PICO Store, toggle the **Show in PICO Store** switch.

![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51b0ab9b1fae464fb9870a87df5183cf~tplv-goo7wpa0wc-image.image)
### Steps
#### Test with a developer account
No matter the app is published or not, you can use the following steps to test an unsubmitted add-on with a PICO developer account. The members of your organization can also use their accounts to test IAP service just like the original developer account.

1. Log in to your device with the developer account that you use to create the add-on.
2. Follow the instructions in the "Methods" section to test the add-on.

#### Test with a non developer account
You can only test a submitted and approved add-on with a non PICO developer account. In this case, you test the real payment for the add-on. The steps vary with the status of the app corresponding to the add-on.
If the add-on is rejected, the testing offer will be invalid. In this case, you need to create a new draft using the original SKU and save the draft, then you can normally access the testing offer.
**Published app**

1. Go to the add-on's edit page and click **Go to submission** in the upper-right corner.
   The add-on enters the "Under Review" status.
2. Once the add-on is approved, follow the instructions in the "Methods" section to test it.

**Unpublished app**

1. Submit the app by going to the app's details screen and clicking **Submit** in the lower-right corner. For more information, refer to [this article](/13136/en_formal-app#submit-a-formal-application).
2. Let your AM know to contact the QA to hold the app in the "Under Review" status.
3. Go to the add-on's edit page and click **Go to submission** in the upper-right corner.
   The add-on enters the "Under Review" status.
4. Once the add-on is approved, follow the instructions in the "Methods" section to test it.

## Demo
The IAPDemo integrates all IAP service-related APIs and therefore can be used to show how these APIs work. For more information, refer to the "[In-app purchase (IAP) demo](/en_iap-demo)" article.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/0481238196ae45ada3267d013ea0a527~tplv-em5hxbkur4-noop.image?width=1280&height=1280" width="542px" />

## API reference
For more information about IAP service-related APIs, refer to the [API reference](/reference/unity/client-api/IAPService/).


# --- END: In-app purchase (IAP).md ---



# --- BEGIN: Integrate the Achievement service.md ---

This article introduces the procedure for integrating the Achievement service into your app.
## Important note
Testing the Achievement service is currently not available in the Unity Editor.
## Prerequisites
Make sure you have imported the PICO Unity Integration SDK into your project and completed required project settings. If you haven't, refer to the following articles to complete these tasks:

* [Import the SDK](/en_import-the-sdk)
* [Complete project settings](/en_complete-project-settings)

## Procedure
### Step 1: Create achievements
Create one or multiple achievements for your app on the PICO Developer Platform.

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/organization/).
2. On the **My Apps** screen, click on the target app's card.
   This directs you to the app's **Overview** screen.
3. From the left navigation panel, select **Platform Services** > **Achievement**.
   This directs you to the **Achievements** screen.
4. Click **+ Create Achievement**. 
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eccf1b5003924c5688b1475a2482e4fa~tplv-goo7wpa0wc-image.image)
   This directs you to the achievement details configuration screen.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c9d5f8188674fe7aec14d308d9d8826~tplv-goo7wpa0wc-image.image)
5. Complete achievement details.
   | **Field** | **Description** |
   | --- | --- |
   | Display name | The name of the achievement that users will see. |
   | Description | The description of the achievement. You may want to describe how users can unlock this achievement. |
   | Unlocked Description (optional) | Users can see the description when they unlock this achievement. |
   | API Name | The unique identifier of this achievement. The API Name you create on the PICO Developer Platform should match the one you reference in your code. |
   | Achievement Type | The type of this achievement. Available options are: Simple, Count, and Bitfield. Refer to the "[Achievement types](/en_achievements-service-design#e33f2622)" section for details. |
   | Data Write Permission | Choose one of the following options: <br>  <br> * **Client Authoritative**: This is the default setting, which means both the client app and server are allowed to update achievement progress. <br> * **Server Authoritative**: Only the server is allowed to update achievement progress, but the server may still need to query achievement progress from the client app. |
   | Is Secret | If this is a hidden achievement, you can check this checkbox. Once checked, all the achievement's information is invisible to users. Users can see this achievement only after they unlock it. |
   | Notification Status | Once checked, users will receive a toast notification in the app as well as a notification in the notification center after unlocking this achievement. |
   | Unlocked Icon (optional) | Users will see this icon when they haven't unlocked this achievement. |
   | Locked Icon (optional) | Users will see this icon after they unlock this achievement. |
6. If you need to display the achievement display name, description, and unlocked description in multiple languages, use the following steps:
   1. Click **+ Manage Languages** and add the languages you want.
   2. Click each language button to fill out information in the corresponding language.
      You can also import multi-lingual information in a batch:
      1. Click the **Download CSV template** button.
      2. Fill out the multi-lingual information in the template and delete the rows of the languages you don't want.
      3. Click the **Import CSV** button to import the template.
7. Click the **Save** or **Submit** button. 
   If you click the **Save** button, the achievement will enter the "draft" status, and you can edit its information as needed. If you click the **Submit** button, the achievement will enter the "Under Review" status, and you are unable to edit any of its information. 
8. (Optional) For a published achievement, return to the achievement list and do the following if needed: 
   * Click the **Archive** button to disable an achievement. Archiving will not delete the achievement and users' progress, but will make the achievement invisible to users. 
   * Click the **Activate** button to re-enable an archived achievement.

Do not close the webpage, you need to proceed to enable the Matchmaking service for your app.
### Step 2: Initialize platform services globally and the game module
Initialize platform services globally. You can call `CoreService.Initialize()` for synchronous initialization or call `CoreService.AsyncInitialize()` for asynchronous initialization. For more information and code samples, refer to the "[Initialization](/en_initialization)" article.
### Step 3: Implement the Achievement service
Call APIs to implement the Achievement service in your app.
The following table lists the client APIs packaged in the `AchievementsService` class. To learn more information about these APIs, refer to the [client API reference](/reference/unity/latest/AchievementsService/). For use cases and code samples, refer to [this article](/en_achievements-use-cases-and-code-samples).
| **API** | **Description** |
| --- | --- |
| AchievementsService.GetDefinitionsByName | Get the information of a specified achievement. The information includes the achievement's API name, description, and whether it is unlocked. |
| AchievementsService.GetAllDefinitions | Get the information of all achievements. |
| AchievementsService.GetProgressByName | Get the progress the user has made for unlocking a specified achievement. |
| AchievementsService.GetAllProgress | Get the progress the user has made for unlocking all achievements. |
| AchievementsService.AddCount | Add a count to a specified count achievement. |
| AchievementsService.AddFields | Unlock the bit(s) of a specified bitfield achievement. |
| AchievementsService.Unlock | Unlock a specified achievement of any type even if the target for unlocking this achievement is not reached. |
Below are server APIs. For details, refer to the [server API reference](/reference/unity-server/latest/create-or-update-achievement/).

* Create or update an achievement
* Get the basic information of achievements
* Update a user's achievement progress
* Get a user's achievement progress
* Delete a user's achievement progress


# --- END: Integrate the Achievement service.md ---



# --- BEGIN: Manage files.md ---

You can view the files of your PICO device and the PDC tool.

1. Open the PDC tool.
2. From the left navigation panel, select **File Manager**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b713e015c6924d90b8fc4bef5a1eb26a~tplv-goo7wpa0wc-image.image)
3. View the files.
   | **File Type** | **Description** |
   | --- | --- |
   | On Device | The images, videos, apps, and APKs in your PICO device. |
   | PDC Local | The images, videos, and logs (i.e., performance monitoring files) in the PDC tool. |


# --- END: Manage files.md ---



# --- BEGIN: Metadata review-related FAQs.md ---

Refer to [this article](/document/distribute/content-review-faq-for-cn-pico-store/).


# --- END: Metadata review-related FAQs.md ---



# --- BEGIN: Modify the eye buffer resolution.md ---

In the process of 3D graphic rendering on VR devices, the eye buffer plays an intermediary role. As the system renders the standard view of each eye into the eye buffer, it can then provide the eye buffer as a rendering texture to the ATW thread for distortion and sampling. 
Eye buffer resolution (also known as the rendering resolution) can effect image quality and app performance. A lower eye buffer resolution brings lower image quality, while reducing latency and improving app performance. A higher eye buffer resolution brings higher image quality, while increasing latency and impairing app performance. You can adjust your app's rendering resolution to either increase the image quality or improve performance.  
## Important note
Running the app at a higher resolution could improve image quality while potentially impacting the device's battery life, as well as cause CPU/GPU throttling depending on the content being displayed. By defaulting to a lower resolution, the device can maintain a good balance between power consumption and performance at the cost of lowering the image quality. 
## Recommendations

* If your app is already running with good performance, increasing the rendering resolution by increasing the pixel density in your project's codebase can provide a much sharper and clearer visual experience. Conversely, if your app is struggling to maintain the right performance, lowering the rendering resolution can help to improve performance at the cost of visual quality.
* Modifying eye buffer resolution will always lead to the reallocation of eye texture, which can be a costly operation. Therefore, if you need to dynamically adjust the eye rendering resolution during runtime, it is recommended to [modify the render viewport scale](/en_render-viewport-scaling).
* It's important to keep in mind that the PICO Store has guidelines in place to ensure that apps can run on a fully charged device for at least 45 minutes without triggering a low battery warning. Therefore, it's recommended to test the thermal and battery behavior of your app to avoid any unexpected issues. By ensuring that your app meets these guidelines, you can provide a better experience for your users while also maximizing the performance and battery life of the device.

## How-to
By default, eye buffer resolution is set to `1.0`. In general, editing the default value is not recommended. However, based on actual needs, you can modify eye buffer resolution through modifying the value of [XRSettings.eyeTextureResolutionScale](https://docs.unity3d.com/ScriptReference/XR.XRSettings-eyeTextureResolutionScale.html). The valid value ranges from `0.8` to `2.0`. The higher the value, the higher the eye buffer resolution, and vice versa. Values greater than `1.5` are not recommended.
Below is the method:
```C#
XRSettings.eyeTextureResolutionScale = 1.0f;
```

If you are using the Universal Render Pipeline (URP) in your project, use the following method:
```C#
if (GraphicsSettings.renderPipelineAsset != null) {  ((UniversalRenderPipelineAsset)GraphicsSettings.renderPipelineAsset).renderScale = 1;  
}
```

Note that if you set a resolution greater than `2.0`, the setting is invalid and the system automatically uses the default resolution. If the resolution you set is within the valid range but greater than the maximum resolution supported by the device, the system automatically uses the maximum resolution supported by the device.


# --- END: Modify the eye buffer resolution.md ---



# --- BEGIN: Motion tracking API compatibility information.md ---

This article lists all Body Tracking and Object Tracking APIs and the version of PICO Motion Tracker they are compatible with.
## For PICO Motion Tracker (Beta)
The following APIs are for PICO Motion Tracker (Beta), and they are also compatible with PICO Motion Tracker (Official).
| **API** | **Description** | **Supported Device** |
| --- | --- | --- |
| GetBodyTrackingPose | Gets all body tracking data from the motion tracker. | * PICO Motion Tracker (Beta) <br> * PICO Motion Tracker (Official) <br>  <br>  |
| GetMotionTrackerConnectStateWithID <br> ***Older version***: GetFitnessBandConnectState | Gets the connection state of all current motion trackers. |  |
| GetMotionTrackerBattery <br> ***Older version***: GetFitnessBandBattery | Gets the battery of a specified motion tracker. |  |
| GetMotionTrackerCalibState <br> ***Older version***: GetFitnessBandCalibState | Gets the calibration state of the current motion tracker. |  |
| SetBodyTrackingMode <br> ***Older version***: SetSwiftMode | Sets a Body Tracking mode (default or high-accuracy) for the motion tracker. If you do not use this API, the default mode will be applied. |  |
| SetBodyTrackingBoneLength <br>  | Sets bone lengths for different parts of the avatar. The data will be sent to PICO's algorithm to refine the pose of the avatar. |  |
| MotionTrackerNumberOfConnections <br> ***Older version***: FitnessBandNumberOfConnections | You can use this callback function to get notified when the connection state of the motion tracker changes. |  |
| MotionTrackerBatteryLevel <br> ***Older version***: FitnessBandElectricQuantity | You can use this callback function to get notified when the battery of the motion tracker changes. |  |
| BodyTrackingAbnormalCalibrationData <br> ***Older version***: FitnessBandAbnormalCalibrationData | You can use this callback function to get notified when the calibration data is abnormal. It is recommended to recalibrate with the motion tracker upon receiving this notification. |  |
## For PICO Motion Tracker (Official)
Below are Body Tracking APIs:
| **API** | **Description** | **Supported Device** |
| --- | --- | --- |
| StartMotionTrackerCalibApp <br> ***Older version***: StartBodyTrackingCalibApp <br> ***Deprecated***: OpenFitnessBandCalibrationAPP | Opens the PICO Motion Tracker app to perform calibration.  <br>  <br> * For PICO Motion Tracker (Official), "single-glance calibration" will be performed. When a user has a glance at the PICO Motion Tracker on their lower legs, calibration is completed. <br> * For PICO Motion Tracker (Beta), the user needs to follow the instructions on the home of the PICO Motion Tracker app to complete calibration. | * PICO Motion Tracker (Beta) <br> * PICO Motion Tracker (Official) <br>  <br>  |
| GetBodyTrackingSupported | Gets whether the current PICO device supports body tracking. |  |
| StartBodyTracking | Starts body tracking. |  |
| StopBodyTracking | Stops body tracking. |  |
| GetBodyTrackingState | Gets the state of body tracking data and, if any, the reason for exception. |  |
| GetBodyTrackingData | Gets body tracking data. |  |
| BodyTrackingStateError | You can use this callback function to get notified of the state code and error code for body tracking. |  |
| BodyTrackingAction | You can use this callback function to get notified when the action status of a tracking node changes. |  |
The following APIs are used to retrieve the information about PICO Motion Trackers.
**Note**
There is no need to call `StartBodyTracking` before calling the following APIs.

| **API** | **Description** | **Supported Device** |
| --- | --- | --- |
| GetMotionTrackerConnectStateWithSN <br> ***Older version***: GetMotionTrackerConnectState | Gets the number of the currently connected motion trackers as well as their serial numbers. | PICO Motion Tracker (Official) |
| GetMotionTrackerDeviceType <br> ***Older version***: GetMotionTrackerType | Gets the version (beta or official) of the connected motion tracker. | * PICO Motion Tracker (Beta) <br> * PICO Motion Tracker (Official) |
| GetMotionTrackerMode | Gets the current tracking mode of the motion tracker. | PICO Motion Tracker (Official) |
| CheckMotionTrackerModeAndNumber | Checks if the current tracking mode of the motion tracker of the number of motion trackers currently connected are as required. If not, the PICO Motion Tracker app will be opened for performing corresponding setup. | PICO Motion Tracker (Official) |
| GetMotionTrackerLocations | You can use the callback function to get the location of the motion tracker in the Object Tracking mode. | PICO Motion Tracker (Official) |
| MotionTrackerKeyAction | You can use this callback function to get the key actions of the motion tracker. | PICO Motion Tracker (Official)） |
| MotionTrackingModeChangedAction | You can use this callback function to get notified when the motion tracking mode changes. | PICO Motion Tracker (Official) |
## For external devices
| **API** | **Description** | **Supported Device** |
| --- | --- | --- |
| GetExtDevTrackerConnectState | Gets the connection state of the external device. | PICO Motion Tracker (Official) <br>  |
| SetExtDevTrackerMotorVibrate | Sets haptic feedback for the external device. |  |
| SetExtDevTrackerPassDataState | Sets the state for data passthrough-related APIs. |  |
| SetExtDevTrackerByPassData | Sets data passthrough for the external device. |  |
| GetExtDevTrackerByPassData | Gets the data passed through for an external device. |  |
| GetExtDevTrackerBattery | Gets the battery of the external device. |  |
| GetExtDevTrackerKeyData | Gets the key values of the external device. |  |
| ExtDevConnectAction | You can use this callback function to get notified when the connection state of the external device changes. |  |
| ExtDevBatteryAction | You can use this callback function to get notified when the battery level and charging status of the external device changes. |  |
| ExtDevPassDataAction | You need to listen to this event to decide if you need to call `GetExtDevTrackerByPassData` to get the data passed through. |  |


# --- END: Motion tracking API compatibility information.md ---



# --- BEGIN: Object Tracking.md ---

PICO Motion Tracker (Official) can be attached to objects to track their locations. In Object Tracking mode, if the paired trackers are visible to the PICO VR Headset, it can track and output the 6DoF data of the motion trackers in real time. The data is used for tracking the trackers themselves or the objects they attach to.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ae5673fa0414597be02f7b5feeba709~tplv-goo7wpa0wc-image.image" width="408px" />

## Use cases
Below are some use cases of Object Tracking mode. PICO only provides the capability of tracking the PICO Motion Tracker, and you need to implement these use cases by yourself.

* **Motion & game equipment tracking**
   The tracker can be attached to sports equipment such as table tennis paddles, baseball bats, bows, and guns. By tracking the position of real-world sports equipment and interacting with users in XR games, you can provide a more vivid and immersive experience for users. Together with the tracker's Type-C interface for connecting with external devices, it can receive or transmit data from external devices, enabling you to implement capabilities like trigger pull and haptic feedback.
* **Office supplies tracking**
   The tracker can be affixed to office tools (e.g., pens). By tracking the position of the pen's tip, it offers a more realistic writing experience in XR scenes. With the tracker's Type-C interface for connecting with external devices and a stylus that supports pressure sensitivity and buttons, you can enrich the input experience for users.
* **Enhanced hand tracking**
   The tracker can be mounted on hand tracking gloves or bare hands to track the position of human hands in real time. When combined with hand tracking devices or hand pose recognition, it can cover the general blind spots for hand tracking and therefore provides users with a more accurate and low-latency hand tracking experience.

## Limitations

* In Object Tracking mode, if the distance between the tracker and PICO headset exceeds one meter or if the tracker enters the headset's blind spot, the tracking data may become inaccurate or fail to be updated. Please ensure that the tracker remains within the effective tracking range during debugging or formal use.
* Object Tracking mode and Body Tracking mode are mutually exclusive. Once Object Tracking mode is enabled, there will be no body tracking data.

## Development environment

* PICO device models: PICO 4 series, PICO 4 Ultra series
* PICO device's system version: 5.13.0 or later
* PICO Motion Tracker (Official)

## Prerequisites

* Have added the XR Origin object.
* Have added the PXR_Manager (Script) component to the XR Origin object.

## Integrate the Object Tracking feature
### Step 1: **Enable the Object Tracking capability for your app**
On the **PXR_Manager (Script)** panel of the **Inspector** window, check the **Body Tracking** checkbox to enable the Object Tracking capability for your app. Then you can call Object Tracking APIs to integrate this feature into your app.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c541bfbd3d5c4ade9f990096b891aab1~tplv-goo7wpa0wc-image.image" width="450px" />

### Step 2: Retrieve the information of PICO Motion Trackers
Call APIs to retrieve data from motion trackers, including their connection status, device models, positions, and other information. Additionally, in Object Tracking mode, you can retrieve the position of motion tracker. Below is the API list:
| **API** | **Description** |
| --- | --- |
| CheckMotionTrackerNumber | Gets the required number of connected motion trackers. |
| GetMotionTrackerBattery | Gets the battery of a motion tracker in Object Tracking mode. |
| GetMotionTrackerLocation | Gets the location of a motion tracker in Object Tracking mode. |
| MotionTrackerConnectionAction | Gets the location of the motion tracker in Object Tracking mode. |
| MotionTrackerPowerKeyAction | Callback function for getting the events of the motion tracker's Power key. |
| RequestMotionTrackerCompleteAction | Callback function. You can use it to get the result  after calling `CheckMotionTrackerNumber`. |
Before using motion trackers, your app must first request the desired number of trackers. The system will then compare the number of trackers actually connected with the requested number to determine the next steps.
If the number of connected trackers matches the requested number, your app will receive a `PXR_MotionTracking.RequestMotionTrackerCompleteAction` event.
If the number of connected trackers does not match the requested number, the Runtime will launch the PICO Motion Tracker app to prompt the user to connect the correct number of trackers. Once the user finishes connecting the trackers and exits the PICO Motion Tracker app, your app will receive the `PXR_MotionTracking.RequestMotionTrackerCompleteAction` event.
If the current tracking mode is not set to Object Tracking, the Runtime will also launch the PICO Motion Tracker app and prompt the user to switch to Object Tracking mode within the app.
Below is the code sample:
```C#
using System.Collections.Generic;
using Unity.XR.PXR;
using UnityEngine;
using UnityEngine.Rendering;

public class PXR_ObjectTrackingBlock : MonoBehaviour
{
    private Transform objectTrackers;
    private bool updateOT = true;
    private int objectTrackersMaxNum = 3;
    int DeviceCount = 1;
    List<long> trackerIds = new List<long>();
   

    // Start is called before the first frame update
    void Start()
    {
        objectTrackers = transform;
        for (int i = 0; i < objectTrackersMaxNum; i++)
        {
            GameObject ga = GameObject.CreatePrimitive(PrimitiveType.Cube);
            ga.transform.parent = objectTrackers;
            ga.transform.localScale = Vector3.one * 0f;
#if UNITY_6000_0_OR_NEWER
            if (GraphicsSettings.defaultRenderPipeline != null)
#else
            if (GraphicsSettings.renderPipelineAsset != null)
#endif
            {
                Material material = new Material(Shader.Find("Universal Render Pipeline/Lit"));
                Renderer renderer = ga.GetComponent<Renderer>();
                if (renderer != null)
                {
                    renderer.sharedMaterial = material;
                }
            }
        }
        int res = -1;
                PXR_MotionTracking.RequestMotionTrackerCompleteAction += RequestMotionTrackerComplete;
                res = PXR_MotionTracking.CheckMotionTrackerNumber(MotionTrackerNum.TWO);
        
        
        if (res == 0)
        {
            objectTrackers.gameObject.SetActive(true);
           
        }
    }
    private void RequestMotionTrackerComplete(RequestMotionTrackerCompleteEventData obj)
    {
        DeviceCount = (int)obj.trackerCount;
        for (int i = 0; i < DeviceCount; i++)
        {
            trackerIds.Add(obj.trackerIds[i]);
        }
        
        updateOT = true;
    }
    // Update is called once per frame
    void Update()
    {
#if UNITY_ANDROID
       
        for (int i = 0; i < objectTrackersMaxNum; i++)
        {
            var child = objectTrackers.GetChild(i);
            if (child)
            {
                child.localScale = Vector3.zero;
            }
        }

        // Update motiontrackers pose.
        if (updateOT )
        {
            MotionTrackerLocation location = new MotionTrackerLocation();
            for (int i = 0; i < trackerIds.Count; i++)
            {
                bool isValidPose = false;
                int result = PXR_MotionTracking.GetMotionTrackerLocation(trackerIds[i], ref location, ref isValidPose);

                // if the return is successful
                if (result == 0)
                {
                    var child = objectTrackers.GetChild(i);
                    if (child)
                    {
                        child.localPosition = location.pose.Position.ToVector3();
                        child.localRotation = location.pose.Orientation.ToQuat();
                        child.localScale = Vector3.one * 0.1f;
                    }
                }
            }
        }
#endif
    }
}
```

## Retrieve the information of external devices
Through the Type-C interface of the PICO Sense tracker, external devices can be connected to the PICO headset. This allows information such as the external device's battery level, button operations, and vibration commands to be passed between the external device and your app. For example, when connected to a racket with vibration capability, it can provide haptic feedback to the user upon striking the ball. Additionally, this feature supports custom extension protocols defined by developers. Below is the API list:
| **API** | **Description** |
| --- | --- |
| GetExpandDevice | Gets the IDs of external devices. |
| SetExpandDeviceVibrate | Sets haptic feedback for the external device. |
| SetExtDevTrackerPassDataState | Sets the state for data passthrough-related APIs. |
| SetExpandDeviceCustomData | Sets the data to be passed to external devices. |
| GetExpandDeviceCustomData | Gets the data passed from external devices. |
| GetExpandDeviceBattery | Gets the battery of the external device. |
| ExpandDeviceConnectionAction | You can use this callback function to get notified when the connection state of the external device changes. |
| ExpandDeviceBatteryAction | You can use this callback function to get notified when the battery level and charging status of the external device changes. |
| ExtDevPassDataAction | You need to listen to this event to decide if you need to call `GetExtDevTrackerByPassData` to get the data passed through. |
Below is the code sample:
```C#
bool enable = false;

public void Start()
{
    // Enable data passthrough-related APIs
    PXR_MotionTracking.SetExtDevTrackerPassDataState(true);
    PXR_MotionTracking.ExtDevPassDataAction += ExtDevPassDataAction;
}

public void OnDestroy()
{
    PXR_MotionTracking.ExtDevPassDataAction -= ExtDevPassDataAction;
    // Disable data passthrough-related APIs
    PXR_MotionTracking.SetExtDevTrackerPassDataState(false);
}
private void ExtDevPassDataAction(int value)
{
    if (value == 1) // when receiving `1`, call GetExpandDeviceCustomData to obtain the data passed through
    {
        enable = true;
    }
    else if (value == 0) // When receiving `0`, stop calling GetExpandDeviceCustomData
    {
        enable = false;
    }
}
void Update()
{
    if (enable)
    {
        List<ExpandDevicesCustomData> expandDevicesCustomDatas;
            int res = PXR_MotionTracking.GetExpandDeviceCustomData(out expandDevicesCustomDatas);
            passDataResString  += "res: " + res + ", Length: " + expandDevicesCustomDatas.Count + "\n";
            foreach (ExpandDevicesCustomData data in expandDevicesCustomDatas) {
                passDataResString += "TrackerSN: " + data.deviceId + "\n" + "passData: ";
                foreach (byte byteData in data.data) {
                    passDataResString += byteData.ToString() + "";
                }
                passDataResString += "\n";
            }
    }
}

    public void SetExtDevTrackerByPassData() {
        long[] devices;
        int res1 = PXR_MotionTracking.GetExpandDevice(out devices);
        ExpandDevicesCustomData[] expandDevicesCustomDatas  = new ExpandDevicesCustomData[devices.Length];
        string setPassDataRes = "";
        for (int i = 0; i < devices.Length; i++) {
            setPassDataRes += "GetExpandDevice Res: " + res1 + ", Devices: " + devices[i] + ", ";
        }
        setPassDataRes += "\n";
        for (int i = 0; i < devices.Length; i++) {
            expandDevicesCustomDatas[i].deviceId = devices[i];
            expandDevicesCustomDatas[i].data = new byte[]{0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14};  // set 16 data， only the front 15 will be useful
        }
      
        int res = PXR_MotionTracking.SetExpandDeviceCustomData(ref expandDevicesCustomDatas);
        Debug.Log("SetExpandDeviceCustomData res: " + res);
        setPassDataRes += "Set Res: " + res;
      
    }
```

## About pose assignment for motion trackers
The Unity engine defaults to a left-handed coordinate system, while `localLocation` uses a right-handed coordinate system. Therefore, when assigning poses, you need to convert the right-handed coordinate systems to left-handed coordinate system as follows:
```C#
child.localPosition = localLocation.pose.Position.ToVector3();
child.localRotation = localLocation.pose.Orientation.ToQuat();
```

## API reference
For more details on Object Tracking APIs, such as parameter descriptions and returns, refer to the [API reference](/reference/unity/client-api/PXR_MotionTracking/).


# --- END: Object Tracking.md ---



# --- BEGIN: Parameter details.md ---

When retrieving leaderboard entries, you need to pass the `filter`,`startAt`,`pageSize` and `pageIdx` parameters in the request.

* For parameter and enumeration descriptions, refer to the "[Parameter description](#493bba99)" section.
* To learn details about the scope of returns defined by the `filter` and `startAt` parameters, refer to the "[Returns defined by filter & startAt](#4885ada3)" section.
* To learn details about the scope of returns defined by the `startAt`, `pageSize`, and `pageIdx` parameters as well as example returns, refer to the the "[Returns defined by startAt, pageSize & pageIdx](#b7253181)" section.

## Parameter description
Below are the descriptions of parameter `filter`, `startAt`, `pageSize`, and `pageIdx`.
| **Parameter** | **Description** |
| --- | --- |
| `filter` | Restricts the scope entries returned. Below are enumerations: <br>  <br> * `None`: Do not filter, thereby returning all entries of the leaderboard. <br> * `Friends`: Return the entries for the current user and the current user's friends. <br> * `UserIds` & `Unknown`: Invalid type which returns no entry. Do not use them. |
| `startAt` | Defines where to start returning entries. Below are enumerations: <br>  <br> * `Top`: Return from the top 1 entry. <br> * `CenteredOnViewer`: Place the current user's entry in the middle of the page which is then taken as the benchmark page, then return other entries based on the values given to `pageSize` and `pageIdx`. <br> * `CenteredOnViewerOrTop`: Place the current user's entry on the top of the page, then return other entries based on the values given to `pageSize` and `pageIdx`. <br> * `Unknown`: Invalid type. Do not use it. |
| `pageSize` | Defines the number of entries returned on each page. Valid value range: [0,100]. |
| `pageIdx` | Defines which page of entries to return. Start from `0`. For example, if you want to get the first page of entries, pass `0`; if you want to get the second page of entries, pass `1`. |
## Returns defined by `filter` & `startAt`
The system will first sort out if the current user's entry is on the target leaderboard, then return and lay out entries based on the values given to `filter` and `startAt`.
**If the current user's entry is on the leaderboard:**
| **Values of** **`filter` and `startAt`** | **Return** |
| --- | --- |
| `None`+`CenteredOnViewer` | Return all entries and place the current user's entry in the middle of the page. |
| `None`+`CenteredOnViewerOrTop` | Return all entries and place the current user's entry at the top of the page. |
| `Friends`+`Top` | Return the current user's and the current user's friends' entries. Start returning from the first entry. |
| `Friends`+`CenteredOnViewer` | Return the current user's and the current user's friends' entries. Place the current user's entry in the middle of the page. |
| `Friends`+`CenteredOnViewerOrTop` | Return the current user's and the current user's friends' entries. Place the current user's entry at the top of the page. |
**If the current user's entry is NOT on the leaderboard:**
| **Values of** **`filter` and `startAt`** | **Return** |
| --- | --- |
| `None`+`CenteredOnViewer` | Return no entry. |
| `None`+`CenteredOnViewerOrTop` | Return no entry. |
| `Friends`+`Top` | Return the entries of the current user's friends. Start returning from the first entry. |
| `Friends`+`CenteredOnViewer` | Return the entries of the current user's friends.  |
| `Friends`+`CenteredOnViewerOrTop` | Return the entries of the current user's friends.  |
## Returns defined by `startAt`, `pageSize` & `pageIdx`
The values given to parameter `startAt` and `pageIdx`, as well as the parity of parameter `pageSize`, will determine the returns. Below are detailed descriptions:
| **Value of** **`startAt`** | **Parity of** **`pageSize`** | **Return** |
| --- | --- | --- |
| `CenteredOnViewer` | Odd | If taking the page where the current user's entry is located as the benchmark page (`pageIdx`=0) and placing the current user's entry in the middle of the benchmark page, the returns will be one of the following: <br>  <br> * The numbers of entries queried before and after the current user's entry are both [(`pageSize`-1)/2]. <br>    For example, if the total number of entries is 10, the current user ranks 4th, and: <br>    * `pageIdx`=0, `pageSize`=5, entry 2, 3, 4, 5, 6 will be returned on the target page. <br>    * `pageIdx`=1, `pageSize`=5, entry 7, 8, 9, 10 will be returned on the target page. <br> * The number of entries queried before the current users entry is less than [(`pageSize`-1)/2]. <br>    For example, if the total number of entries is 6, the user ranks 2nd, `pageIdx`=0, and `pageSize`=5, entry 1, 2, 3, 4, 5 will be returned on the target page. <br> * The number of entries queries after the current user's entry is less than [(`pageSize`-1)/2]. <br>    For example, if the total number of entries is 6, the current user ranks 6th, and: <br>    * `pageIdx`=0, `pageSize`=5, entry 4, 5, 6 will be returned on the target page. <br>    * `pageIdx`=1, `pageSize`=5, no entry will be returned on the target page. |
|  | Even | If taking the page where the current user's entry is located as the benchmark page (`pageIdx`=0) and placing the current user's entry in the middle of the benchmark page, the returns will be one of the following: <br>  <br> * The numbers of entries queried before and after the current user's entry are [(`pageSize`/2)-1] and (`pageSize`/2) respectively. <br>    For example, if the total number of entries is 6, the current user ranks 3rd, and: <br>    * `pageIdx`=0, `pageSize`=4, entry 2, 3, 4, 5 will be returned on the target page. <br>    * `pageIdx`=1, `pageSize`=4, only entry 6 will be returned on the target page. <br> * The number of entries queried before the current user's entry is less than [(`pageSize`/2)-1]. <br>    For example, if the total number of entries is 7, the current user ranks 2nd, and: <br>    * `pageIdx`=0, `pageSize`=4, entry 1, 2, 3, 4 will be returned on the target page. <br>    * `pageIdx`=1, `pageSize`=4, entry 5, 6, 7 will be returned on the target page. <br> * The number of entries queried after the current user's entry is less than (`pageSize`/2). <br>    For example, if the total number of entries is 3, the current user ranks 3rd, `pageIdx`=0, and `pageSize`=4, entry 2, 3 will be returned on the target page. |
| `CenteredOnViewerOrTop` | Odd/Even | Place the current user's entry at the top of the page, then query (`pageSize`-1) entries behind the position of the current user's entry. |
##


# --- END: Parameter details.md ---



# --- BEGIN: Performance metrics.md ---

This page introduces the to-be-achieved performance target for applications that run on PICO Neo3 series devices.
| **Metric Name** | **Description** |
| --- | --- |
| FPS | The frame rate of your application should be no lower than 72 FPS. |
| Draw Call | The following may affect Draw Call: <br> ● Switching the state of the pipeline, including changing shaders, textures, and meshes between draws. Sharing meshes and instance meshes as much as possible is recommended. <br> ● (Recommended) Using global texture arrays. <br> ● (Recommended) Using a minimal set of unified shaders that do not generate variants. <br> ● Graphics API: Vulkan vs OpenGL ES. <br> ● Multi-threaded Rendering: low latency vs frame-behind. <br> ● (Recommended) Using bindless textures and indirect draws. <br> ● (Recommended) Limiting the number of triangular surfaces to the maximum of 1 million. |


# --- END: Performance metrics.md ---



# --- BEGIN: PICO Building Blocks.md ---

The PICO Building Blocks system can help you set up features, including the features provided by the PICO Unity Integration SDK and Unity, in your project with a single click.
## XR Interaction Toolkit version
3.x.x
## Configurable functionalities
You can set up the following features with PICO Building Blocks.
| **Module** | **Feature** | **Description** |
| --- | --- | --- |
| PICO Controller | PICO Controller Tracking | Add the controller models provided by the PICO Unity Integration SDK to the scene and set up interaction events. |
|  | Controller Canvas Interaction | Enable the interaction between the controller ray and a canvas. |
| PICO Hand <br>  | PICO Hand Tracking | Add the hand models provided by the PICO Unity Integration SDK to the scene and enable the Hand Tracking capability for your app. |
|  | XR Hand Tracking | Add the hand models provided by Unity's XR Hands package to the scene and enable the Hand Tracking capability for your app. |
|  | XRI Hand Interaction | Use the XR Interaction Toolkit to enable the interaction between hands and 3D objects. |
|  | XRI Grab Interaction | Use the XR Interaction Toolkit to enable the hands or controllers to grab objects. |
|  | XRI Poke Interaction | Use the XR Interaction Toolkit to enable the hands or controllers to poke objects. |
| PICO Video Seethrough | PICO Video Seethrough | Set up the Video Seethrough feature provided by the PICO Unity Integration SDK. |
|  | PICO Video Seethrough Effect | Configure video seethrough effect-related parameters provided by the PICO Unity Integration SDK. |
| PICO Motion Tracking | PICO Body Tracking | Set up the Body Tracking functionality and use 24 cubes to display the tracking status of 24 human body joints in real time. |
|  | PICO Body Tracking Debug | Set up the Body Tracking Debugging functionality, using 24 cubes to show the tracking status of 24 human body joints. Additionally, you can select specific joints and rotate their joint data (X, Y, and Z) to adapt to different avatar models. |
|  | PICO Object Tracking | Set up the Object Tracking functionality and use a 0.1 cubic meter cube to display the movement of the PICO Motion Tracker. |
| PICO Spatial Audio | PICO Spatial Audio Free Field | Complete the settings related to free field of spatial audio. Free field refers to a sound field that simulates the position of a sound source while ignoring all environmental acoustic phenomena. |
|  | PICO Spatial Audio Ambisonics | Complete the settings related to ambisonics. Ambisonics is a global surround sound format that covers the horizontal plane as well as sound sources above and below the listener, providing a highly immersive audio experience.  |
| PICO Sense Pack | PICO Spatial Anchor Sample | A sample of creating, persisting, and destroying spatial anchors configured within a scene. |
|  | PICO Spatial Mesh | Set up the Spatial Mesh functionality and automatically start it. |
|  | PICO Scene Capture | Set up the Scene Capture functionality and automatically start it. |
| PICO Composition Layer | PICO Composition Layer Overlay | Configure an overlay and set it to the cylinder type. |
|  | PICO Composition Layer Underlay | Configure an underlay and set it to the quad type. |
## Open PICO Building Blocks
| **Where to Open** | **Supported Unity Versions** | **Instructions** |
| --- | --- | --- |
| Overlay menu <br>  | * Unity 2022 <br> * Unity 2023 | In the upper-right corner of the **Scene** or **Game** view, click **···** > **Overlay Menu**. From the menu, choose **XR Building Blocks**, and the XR Building Blocks panel will appear in the view. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b43ba18db1146378006982da07e1e7e~tplv-goo7wpa0wc-image.image) |
| Hierarchy window | * Unity 2020 <br> * Unity 2021 <br> * Unity 2022 <br> * Unity 2023 | In the **Hierarchy** window, click **+** > **PICO Building Blocks**. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fb85c4bf62b4e85bf404213ea4c65fd~tplv-goo7wpa0wc-image.image) |
| GameObject menu <br>  | * Unity 2020 <br> * Unity 2021 <br> * Unity 2022 <br> * Unity 2023 | From the top menu bar, select **GameObject** > **PICO Building Blocks**. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e818038e4994809a066f92d450cf471~tplv-goo7wpa0wc-image.image) |
## Set up desired functionalities with PICO Building Blocks
You can use PICO Building Blocks to set up your desired functionalities with one click.
### PICO Controller Tracking
Set up the controller model prefabs and input events provided by the PICO Unity Integration SDK in the scene. The expected result is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9bc61f764ea4a03acb563e5fb23e0b6~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Controller** > **PICO Controller Tracking**. The following actions will be performed automatically:

* Check if the **Starter Assets** sample provided by the XR Interaction Toolkit is installed. If not, it will be installed automatically.
* Check if the **XR Origin** object has been added to the scene. If not, the **[Building Block] XR Origin (XR Rig)** object will be generated automatically.
* Add the **PXR_Manager (Script)** component to the XR Origin object.
* Locate the **Left Controller** and **Right Controller** objects under the XR Origin object, configure their **XR Controller (Action-based)** components with input events (**XRI Default Input Actions**), and set the corresponding PICO controller model prefabs (**LeftControllerModel** and **RightControllerModel**) in the **Model Prefab** parameter.
* Add the **Element 0** object to the **Action Assets** parameter of the XR Origin object's **Input Action Manager** component, and set it to **XRI Default Input Actions**.

For instructions on how to manually set up PICO Controller Tracking, refer to [this article](/en_create-an-xr-scene).
### Controller Canvas Interaction
**Note**
This feature needs to work with the PICO Controller Tracking feature.

Configure the canvas in the scene to be displayed as a 3D canvas on PICO devices, and set up interaction events. The expected result is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e69fcccf0a8d4d729cd4672d65bee1e7~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Controller** > **Controller Canvas Interaction**. The following actions will be performed automatically:

* Check if the **XR Origin** object has been added to the scene. If not, the **[Building Block] XR Origin (XR Rig)** object will be generated automatically.
* Add the **PXR_Manager (Script)** component to the XR Origin object.
* Configure the **EventSystem**.
* Add the **Building Block Controller Canvas Interaction Canvas** object, set its **Event Camera** to the main camera, and configure the **Tracker Device Graphic Raycast** component.
* If the canvas's **RenderMode** is not set to **WorldSpace**, it will be changed to **RenderMode.WorldSpace**, and the canvas will be positioned according to the main camera's location to ensure that the controller ray can interact with the canvas properly.

Additionally, you can add UI objects like **Button - TextMeshPro** and **Dropdown - TextMeshPro** under the **Canvas** object, and then set up PICO Controller Tracking to experience the interaction between the controllers and the canvas.
For instructions on how to manually set up controller-canvas interactions, refer to [this article](/en_create-interactive-ui).
### PICO Hand Tracking
Add the hand model prefabs provided by the PICO Unity Integration SDK to the scene and enable the Hand Tracking capability. The expected result is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93c137fe6b0b474b87a744bbcf73e61e~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Hand** > **PICO Hand Tracking**. The following actions will be performed automatically:

* Check if the **XR Origin** object has been added to the scene. If not, the **[Building Block] XR Origin (XR Rig)** object will be generated automatically.
* Add the hand model prefabs provided by the PICO Unity Integration SDK under the XR Origin object.
* Add the **PXR_Manager (Script)** component to the XR Origin object.
* Check the **Hand Tracking** checkbox on the **PXR_Manager (Script)** component panel to enable the Hand Tracking capability.

For instructions on how to manually set up PICO Hand Tracking, refer to [this article](/en_hand-tracking).
### XR Hand Tracking
Add the hand model prefabs provided by Unity's [XR Hands package](https://docs.unity3d.com/Packages/com.unity.xr.hands@1.5/manual/index.html) to the scene and enable the Hand Tracking capability. The expected result is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c43ed9cd709444fd91e9aa83a1245550~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Hand** > **XR Hand Tracking**. The following actions will be performed automatically:

* Check if the **HandVisualizer** sample provided by the XR Hands package has been imported. If not, it will be imported automatically.
* Check if the **XR Origin** object has been added to the scene. If not, the **[Building Block] XR Origin (XR Rig)** object will be generated automatically.
* Add the left and right hand models provided by the XR Hands package under the main camera object.
* Add the **PXR_Manager (Script)** component to the XR Origin object.
* Check the **Hand Tracking** checkbox on the **PXR_Manager (Script)** component panel to enable the Hand Tracking capability.

For instructions on how to manually set up XR Hand Tracking, refer to [this article](/en_enable-interactions-between-hands-and-3d-objects-using-xr-interaction-toolkit).
### XRI Hand Interaction
Use the XR Interaction Toolkit to enable the interaction between hands and 3D objects. The expected result is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18d537ab1ef04cdb85deacd064abccf6~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Hand** > **XRI Hand Interaction**. The following actions will be performed automatically:

* Check if the **HandVisualizer** sample provided by the XR Hands package has been imported. If not, it will be imported automatically.
* Check if the **Starter Assets** and **Hands Interaction Demo** samples provided by the XR Interaction Toolkit have been imported. If not, they will be imported automatically.
* Set default input actions for **XRI LeftHand** and **XRI RightHand**.

After this, you will need to manually open the **HandsDemoScene** and enable the Hand Tracking capability for the app and the PICO device to use complete hand interactions.
For instructions on how to manually set up XRI Hand Interaction, refer to [this article](/en_enable-interactions-between-hands-and-3d-objects-using-xr-interaction-toolkit).
### XRI Grab Interaction
Use the XRI Interaction Toolkit to enable the hands or controllers to grab objects. The expected result is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c35b0d9194d4e9faaf35bf9fcea48db~tplv-goo7wpa0wc-image.image></video>

Set up XRI Grab Interaction using the following steps:

1. Refer to the "XRI Hand Interaction" section to set up hand interaction using the XRI Interaction Toolkit.
2. In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Hand** > **XRI Grab Interaction**. The following actions will be performed automatically:
   * Add and configure the **Building Blocks XRI Hand Interaction** object in the scene.
   * Add and configure the **Building Blocks XRI Hand Grab Interactable** in the scene.

### XRI Poke Interaction
Use the XRI Interaction Toolkit to enable the hands or controllers to poke objects. The expected result is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/711aa4525b6a4640b8f7b7638f3891fd~tplv-goo7wpa0wc-image.image></video>

Set up XRI Poke Interaction using the following steps:

1. Refer to the "XRI Hand Interaction" section to set up hand interaction using the XRI Interaction Toolkit.
2. In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Hand** > **XRI Poke Interaction**. The following actions will be performed automatically:
   * Add and configure the **Building Blocks XRI Hand Interaction object** in the scene.
   * Add and configure the **Building Blocks XRI Hand Poke Interactable** in the scene.

### PICO Video Seethrough
Set up the Video Seethrough feature provided by the PICO Unity Integration SDK.
In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Video Seethrough** > **PICO Video Seethrough**. The following actions will be performed automatically:

* Check if the **XR Origin** object has been added to the scene. If not, the **[Building Block] XR Origin (XR Rig)** object will be generated automatically.
* Add the **PXR_Manager (Script)** component to the XR Origin object.
* Check the **Video Seethrough** checkbox on the **PXR_Manager (Script)** component panel to enable the Video Seethrough capability.
* Set the **Clear Flags** parameter of the main camera to **Solid Color**, and set the **Background** parameter's RGBA values to 0.
* In the CameraEffectTest.cs script, add the following code:
   ```C#
   // Enable the Video Seethrough capability
   PXR_Manager.EnableVideoSeeThrough = true;
   // Enable video seethrough effect
   PXR_MixedReality.EnableVideoSeeThroughEffect(true);
   ```

For instructions on how to manually set up PICO Video Seethrough, refer to [this article](/en_seethrough).
### PICO Video Seethrough Effect
Set up video seethrough effect-related parameters provided by the PICO Unity Integration SDK.
In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Video Seethrough** > **PICO Video Seethrough Effect**. The following actions will be performed automatically:

* Set up the Video Seethrough feature. For specific automatic actions, refer to the "PICO Video Seethrough" section.
* In the CameraEffectTest.cs script, call the `SetVideoSeeThroughEffect` API to configure video seethrough effect-related parameters, including `ColorMap`, `Brightness`, `Saturation`, and `Contrast`. Additionally, call the `SetVideoSeeThroughLut` API to set the number of rows and columns for the LUT texture. Below is the code:
   ```C#
   public void SetColortemp(float x)
   {
       PXR_MixedReality.SetVideoSeeThroughEffect(PxrLayerEffect.Colortemp, x, 0);
   }
   public void SetBrightness(float x)
   {
       PXR_MixedReality.SetVideoSeeThroughEffect(PxrLayerEffect.Brightness, x, 0);
   }
   public void SetSaturation(float x)
   {
       PXR_MixedReality.SetVideoSeeThroughEffect(PxrLayerEffect.Saturation, x, 0);
   }
   public void SetContrast(float x)
   {
       PXR_MixedReality.SetVideoSeeThroughEffect(PxrLayerEffect.Contrast, x, 0);
   }
   public void SetLutRow(float x)
   {
       if (lutTex)
       {
           row = (int)(lutTex.width * x);
           PXR_MixedReality.SetVideoSeeThroughLut(lutTex, row, col);
       }
   }
   public void SetLutCol(float x)
   {
       if (lutTex)
       {
           col = (int)(lutTex.height * x);
           PXR_MixedReality.SetVideoSeeThroughLut(lutTex, row, col);
       }
   }
   ```

To use complete video seethrough effect, you will also need to add and configure the LUT texture. For detailed instructions on how to manually set up PICO's video seethrough effect, refer to [this article](/en_seethrough).
### PICO Body Tracking
Set up the Body Tracking functionality and use 24 cubes to display the tracking status of 24 body joints in real-time. The expected effect is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8b9e009640a41f0aaaad4c644e1a31b~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Motion Tracking** > **PICO Body Tracking**. The following actions will be performed automatically:

* Check if the **XR Origin** object has been added to the scene. If not, the **[Building Block] XR Origin (XR Rig)** object will be generated automatically.
* Add the **PXR_Manager (Script)** component to the XR Origin object.
* Check the **Body Tracking** checkbox on the **PXR_Manager (Script)** panel.
* Create the **Building Block PICO Body Tracking** object and add **BodyTracking.prefab** as its child object.
   The PXR_BodyTrackingBlock.cs script attached to BodyTracking.prefab implements the complete Body Tracking functionality and uses 24 cubes to represent the 24 body joints tracked by the PICO device.

For how to set up Body Tracking step by step on your own, refer to [this article](/en_body-tracking).
### PICO Body Tracking Debug
Set up the Body Tracking functionality and use 24 cubes to display the tracking status of 24 body joints in real-time. Additionally, you can select specific joints and rotate their joint data (X, Y, and Z) to adapt to different avatars. The expected effect is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f67c0b4596e5497bb7336016e4cf6793~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Motion Tracking** > **PICO Body Tracking Debug**. The following actions will be performed automatically:

* Check if the **XR Origin** object has been added to the scene. If not, the **[Building Block] XR Origin (XR Rig)** object will be generated automatically.
* Add the **PXR_Manager (Script)** component to the XR Origin object.
* Check the **Body Tracking** checkbox on the **PXR_Manager (Script)** panel.
* Create the **Building Block PICO Body Tracking** object and add **BodyTrackingDebug.prefab** as its child object.
   BodyTracking.prefab can be used to display body joints as well as modify selected joints.

### PICO Object Tracking
Set up the Object Tracking functionality and use a 0.1-cubic-meter cube to display the movement of the PICO Motion Tracker. The expected effect is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7365af86eff644729bc67086021559e1~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Motion Tracking** > **PICO Object Tracking**. The following actions will be performed automatically:

* Check if the **XR Origin** object has been added to the scene. If not, the **[Building Block] XR Origin (XR Rig)** object will be generated automatically.
* Add the **PXR_Manager (Script)** component to the XR Origin object.
* Check the **Body Tracking** checkbox on the **PXR_Manager (Script)** panel.
* Create the **Building Block PICO Object Tracking** object and place it under the same parent object as the **Main Camera** object. 
* Attach the **PXR_ObjectTrackingBlock.cs** script to the **Building Block PICO Object Tracking** object. This script implements the complete Object Tracking functionality.

For how to set up Object Tracking manually on your own, refer to [this article](/en_object-tracking).
### PICO Spatial Audio Free Field
Complete the settings related to free field of spatial audio. Free field refers to a sound field that simulates the position of a sound source while ignoring all environmental acoustic phenomena. The expected effect is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/542832f8b6d541cfbf65d17fa6ed8438~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Spatial Audio** > **PICO Spatial Audio Free Field**. The following actions will be performed automatically:

* Check if the **XR Origin** object has been added to the scene. If not, the **[Building Block] XR Origin (XR Rig)** object will be generated automatically.
* Add the **XR Interaction Manager** object.
* Add the **[Building Block] PICO Spatial Audio Free Field** object, then add the **SpatialAudioFreeField** and **SoundSphere** sub-objects to it.
* In the **SptialAudioFreeField** and **SoundShpere** sub-objects, complete free field-related settings. For details, refer to [this article](/en_spatial-audio).

### PICO Spatial Audio Ambisonics
Complete the settings related to ambisonics. Ambisonics is a global surround sound format that covers the horizontal plane as well as sound sources above and below the listener, providing a highly immersive audio experience. The expected effect is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47200b252ac94ea78437c0cb1e7e4a6b~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Spatial Audio** > **PICO Spatial Audio Ambisonics**. The following actions will be performed automatically:

* Check if the **XR Origin** object has been added to the scene. If not, the **[Building Block] XR Origin (XR Rig)** object will be generated automatically.
* Add the **XR Interaction Manager** object.
* Add the **[Building Block] PICO Spatial Audio Ambisonics** object, then add the **SpatialAudioAmbisonics** and **Sphere** sub-objects to it.
* In the **SpatialAudioAmbisonics** and **Sphere** sub-objects, complete free field-related settings. For details, refer to [this article](/en_spatial-audio).

### PICO Spatial Anchor Sample
Set up the sample of creating, persisting, and destroying spatial anchors configured within a scene.
In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Sense Pack** > **PICO Spatial Anchor Sample**. The following actions will be performed automatically:

* Check whether the **Starter Assets** have been imported into the project.
* Check if an **XR Origin** object has been added to the scene. If not, add a **[Building Block] XR Origin (XR Rig) XRI300** object. Then:
   * Add an **XR Origin (XR Rig)** child object to it.
   * Add the **PXR_Manager (Script)** component to the child object. 
   * In the **PXR_Manager (Script)** panel, enable the **Video Seethrough**, **Spatial Anchor**, and **Scene Capture** options.
* Add **Camera Offset** and **Locomotion** child objects to the **XR Origin (XR Rig)** object, and configure these objects with the necessary settings for spatial anchors.

### PICO Spatial Mesh
Set up the Spatial Mesh functionality and automatically start it.
In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Sense Pack** > **PICO Spatial Mesh**. The following actions will be performed automatically:

* Add an **XR Interaction Manager** object.
* Check if an **XR Origin** object has been added to the scene. If not, add a **[Building Block] XR Origin (XR Rig)** object.
* Add the **PXR_Manager (Script)** component to the **[Building Block] XR Origin (XR Rig)** object, and enable the **Video Seethrough** and **Spatial Mesh** options in the **PXR_Manager (Script)** panel.
* Add a **[Building Block] PICO Spatial Mesh** object and configure the **MeshPrefab**.

### PICO Scene Capture
Set up the Scene Capture functionality and automatically start it.
In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Sense Pack** > **PICO Scene Capture**. The following actions will be performed automatically:

* Add an **XR Interaction Manager** object.
* Check if an **XR Origin** object has been added to the scene. If not, add a **[Building Block] XR Origin (XR Rig)** object 
* Add the **PXR_Manager (Script)** component to the **[Building Block] XR Origin (XR Rig)** object, and enable the **Video Seethrough** and **Scene Capture** in the **PXR_Manager (Script)** panel.
* Add the **PXR_Scene Capture Manager (Script)** component to the **[Building Block] XR Origin (XR Rig)** object, and configure the **Box 2D Prefab** and **Box 3D Prefab**.

### PICO Composition Layer Overlay
Configure an overlay and set it to the cylinder type. The expected result is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/550080a683624c9fadde97aa75d98d9e~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Composition Layer** > **PICO Composition Layer Overlay**. The following actions will be performed automatically:

* Add an **XR Interaction Manager** object.
* Check if an **XR Origin** object has been added to the scene. If not, add a **[Building Block] XR Origin (XR Rig)** object and attach the **PXR_Manager (Script)** component to it.
* Add a **[Building Block] PICO Composition Layer Overlay** object, attach the **PXR_Composition Layer (Script)** component to it, and complete the overlay-related configuration in the component.

### PICO Composition Layer Underlay
Configure an underlay and set it to the quad type. The expected result is as follows:

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e81615bf2b04599b549ba860f29f7b8~tplv-goo7wpa0wc-image.image></video>

In the **XR Building Blocks** menu or **PICO Building Blocks** menu, select **PICO Composition Layer** > **PICO Composition Layer Underlay**. The following actions will be performed automatically:

* Add an **XR Interaction Manager** object. 
* Check if an **XR Origin** object has been added to the scene. If not, add a **[Building Block] XR Origin (XR Rig)** object and attach the **PXR_Manager (Script)** component to it.
* Add a **[Building Block] PICO Composition Layer Underlay** object.
* Add an **UnderlayHole** child object to the **[Building Block] PICO Composition Layer Underlay** object, and assign the **PXR_SDK/PXR_UnderlayHole** shader to create a “hole” that reveals the underlay layer.
* Add an **Underlay** child object to the **UnderlayHole** object, attach the **PXR_Composition Layer (Script)** component to it, and complete the underlay-related configuration in the component.

## Changes brought by XR Interaction Toolkit 3.x.x
The PICO Building Blocks system in PICO Unity Integration SDK version 3.1.0 and above is developed based on the XR Interaction Toolkit version 3.x.x. Compared to the Building Blocks system developed on XR Interaction Toolkit 2.x.x, the following changes have occurred.

* XR Origin does not include LeftHand Controller and RightHand Controller.




   XR Interaction Toolkit 2.x.x:

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1434b4125e94429ab13a9834239b3141~tplv-goo7wpa0wc-image.image" width="250px" />




   XR Interaction Toolkit 3.x.x:

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24c14e42ce774679b10f4ee7d3c37c14~tplv-goo7wpa0wc-image.image" width="200px" />




   As a result, the controller configuration and functionalities relying on controller rays, including PICO Controller Tracking and Controller Canvas Interaction, are affected. You need to replace the original XR Origin with the XR Origin (XR Rig).prefab provided in the /Assets/XR Interaction Toolkit/{version}/prefabs directory of XR Interaction Toolkit 3.x.x.
* The names of the action maps in XRI DefaultInputActions.inputactions have had the "Hand" term removed.
   | **Before** | **After** |
   | --- | --- |
   | XRI LeftHand | XRI Left |
   | XRI LeftHand Interaction | XRI Left Interaction |
   | XRI LeftHand Locomotion | XRI Left Locomotion |
   | XRI RightHand | XRI Right |
   | XRI RightHand Interaction | XRI Right Interaction |
   | XRI RightHand Locomotion | XRI Right Locomotion |




   XR Interaction Toolkit 2.x.x:

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a5d49105c4a4130bad5087fb11054f5~tplv-goo7wpa0wc-image.image" width="250px" />




   XR Interaction Toolkit 3.x.x:

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c99f241c9f5f47b8b144df46fb996c02~tplv-goo7wpa0wc-image.image" width="200px" />




* You need to replace the main camera "XR Interaction Hands Setup" previously used by hand tracking-related functionalities with "XR Origin Hands (XR Rig)".




   XR Interaction Toolkit 2.x.x：

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0de09f3c4e124c638cda1a00503cddcd~tplv-goo7wpa0wc-image.image" width="300px" />




   XR Interaction Toolkit 3.x.x：

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edad56c4d8d44957b0e8d48c4bf8167d~tplv-goo7wpa0wc-image.image" width="250px" />




* When using canvas and interacting with controllers in XR Interaction Toolkit 3.x.x, you need to hide the EventSystem.


# --- END: PICO Building Blocks.md ---



# --- BEGIN: PICO XR Portal.md ---

PICO XR Portal is a developer portal consisting of four sections: Configs, Tools, Samples, and About. Through this portal, you can quickly access developer documentation, community, samples, and open-source codes on GitHub, set PICO project settings based on your development needs, and complete project validation to ensure the app you build runs smoothly.
## Open PICO XR Portal
After importing SDK 3.2.0 or higher into your project, click **PICO** in the top menu bar and select **Portal** from the shortcut menu to open PICO XR **Portal**.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac001f208f064af6b03ccecaded0eae8~tplv-goo7wpa0wc-image.image" width="550px" />

## Configs
In this section, you can learn about the supported Unity editor version, fix and validate the essential configurations for using the SDK, and quickly set the PICO project settings.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e79e9071a1a464aaae4b3fb0bcd29e3~tplv-goo7wpa0wc-image.image)
UI Overview:
| **UI** | **Description** |
| --- | --- |
| Information | Notifies the Unity versions supported by the SDK: Unity 2020.3.21 or later. |
| Configuarion | Shows the requirements that Unity project configurations must meet, such as: <br>  <br> * PICO XR Plugin needs to be the only XR Plugin enabled. <br> * The build platform must be Android. <br> * The current required Android software development kit version (AndroidSDKVersions) must be AndroidApiLevel29 or above. <br>  <br> For configurations that do not meet the requirements, you can click **To Apply** to fix them one by one, or click **To Apply All** to fix all configurations at once. <br> For more configuration rules, refer to [Project Validation](/en_project-validation). |
| PICO XR Project Setting | You can click **Open PICO XR Project Setting** to navigate to the path where the PXR_ProjectSetting.asset file is located. You can modify project settings in this file. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a821955593646b293492043533edf35~tplv-goo7wpa0wc-image.image) |
## Tools
In this section, you can learn about Unity editor tools and developer tools provided by the SDK. You can click **Documentation** for detailed documents about the tools.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/920a1b432af04bba986b53b99b577542~tplv-goo7wpa0wc-image.image)
## Samples
This section introduces the sample projects provided by the SDK. You can click **Documentation** for the detailed documents about the samples on the PICO Developer Platform, or click **GitHub** to jump to the GitHub repository of the samples.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/830562cbc6d444ea975614324d640cbb~tplv-goo7wpa0wc-image.image)
## About
In this section, you can learn basic information about PICO Unity Integration SDK, including the features, documents, and installation instructions.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e473347e41d24457984c49e553b6d66a~tplv-goo7wpa0wc-image.image)


# --- END: PICO XR Portal.md ---



# --- BEGIN: Pipeline synchronization.md ---

To create a SecureMR app, you use pipelines to run some operators with some data inputs and outputs. If you need to run multiple pipelines, the way you transfer data between different pipelines is by using a global Tensor to store the output of one pipeline, which will then be used as the input of the next pipeline.
When doing this, you should be aware that the data stored in global Tensors use a "lock free" mechanism for synchronizing access, both read and write. What this means is that when one Pipeline is running which is going to access a global Tensor either as input or output, no other Pipeline that access that Tensor will run, but rather will wait for the first Pipeline to be done with it before proceeding. In this sense, the Tensor data itself does not have to be locked because we prevent multiple pipelines from accessing this data at once. Any access from one pipeline does not have to be locked since each pipeline is run within a single task thread.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1NTVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgNTU1IDY1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAxNDIgMzIgTCAyMTUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMjAuODggMzIgTCAyMTMuODggMzUuNSBMIDIxNS42MyAzMiBMIDIxMy44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZDVlOGQ0IiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5QaXBlbGluZSAxIChydW5uaW5nKTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzNDIgMzIgTCA0MTUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MjAuODggMzIgTCA0MTMuODggMzUuNSBMIDQxNS42MyAzMiBMIDQxMy44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjIyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNlOGUzZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAyMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+R2xvYmFsIFRlbnNvciAxPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0MjIiIHk9IjIiIHdpZHRoPSIxMzAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZjZmZlNiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTI4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDQyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5QaXBlbGxpbmUgMiAod2FpdGluZyk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjE2MiIgeT0iMTIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIycHg7IG1hcmdpbi1sZWZ0OiAxODJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5PdXQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjM2MiIgeT0iMTIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIycHg7IG1hcmdpbi1sZWZ0OiAzODJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5JbjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxGraphModel&quot;:{&quot;dx&quot;:&quot;1422&quot;,&quot;dy&quot;:&quot;816&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;tooltips&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;arrows&quot;:&quot;1&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;pageHeight&quot;:&quot;1169&quot;},&quot;mxCellMap&quot;:{&quot;smfNQ1WE&quot;:{&quot;id&quot;:&quot;smfNQ1WE&quot;},&quot;hyQsOqfE&quot;:{&quot;id&quot;:&quot;hyQsOqfE&quot;,&quot;parent&quot;:&quot;smfNQ1WE&quot;},&quot;gItGtf55&quot;:{&quot;id&quot;:&quot;gItGtf55&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;source&quot;:&quot;SY0yPSTZ&quot;,&quot;target&quot;:&quot;XoaqtI96&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;SY0yPSTZ&quot;:{&quot;id&quot;:&quot;SY0yPSTZ&quot;,&quot;value&quot;:&quot;Pipeline 1 (running)&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;90&quot;,&quot;y&quot;:&quot;190&quot;,&quot;width&quot;:&quot;140&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;2W6RlLMD&quot;:{&quot;id&quot;:&quot;2W6RlLMD&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;source&quot;:&quot;XoaqtI96&quot;,&quot;target&quot;:&quot;y5KdQMDd&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;XoaqtI96&quot;:{&quot;id&quot;:&quot;XoaqtI96&quot;,&quot;value&quot;:&quot;Global Tensor 1&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#E8E3FF;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;310&quot;,&quot;y&quot;:&quot;190&quot;,&quot;width&quot;:&quot;120&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;y5KdQMDd&quot;:{&quot;id&quot;:&quot;y5KdQMDd&quot;,&quot;value&quot;:&quot;Pipelline 2 (waiting)&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#FCFFE6;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;510&quot;,&quot;y&quot;:&quot;190&quot;,&quot;width&quot;:&quot;130&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;tjozmlJ2&quot;:{&quot;id&quot;:&quot;tjozmlJ2&quot;,&quot;value&quot;:&quot;Out&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;250&quot;,&quot;y&quot;:&quot;200&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;GzsXfxh2&quot;:{&quot;id&quot;:&quot;GzsXfxh2&quot;,&quot;value&quot;:&quot;In&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;450&quot;,&quot;y&quot;:&quot;200&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}}},&quot;mxCellList&quot;:[&quot;smfNQ1WE&quot;,&quot;hyQsOqfE&quot;,&quot;gItGtf55&quot;,&quot;SY0yPSTZ&quot;,&quot;2W6RlLMD&quot;,&quot;XoaqtI96&quot;,&quot;y5KdQMDd&quot;,&quot;tjozmlJ2&quot;,&quot;GzsXfxh2&quot;]},&quot;lastEditTime&quot;:0,&quot;snapshot&quot;:&quot;&quot;}" />

With this awareness, if you have a long running pipeline that is going to produce an output global Tensor, but after a long time, your next pipeline that is waiting for this global Tensor will also be slowed down waiting for the first pipeline to be done. If you are fine with using a stored value of the global Tensor in the second pipeline until the producing pipeline is done producing the latest value, then you can speed up your second pipeline run using the following method: create an intermediary pipeline to "latch" the value of the global Tensor and that waits for producing pipeline to update its copy of the global Tensor. The pipeline will copy that newly produced value to another global Tensor which will not be accessed until the update needs to be done. Thus, if the second pipeline will now depend on this copy of the global Tensor, it will not be slowed down by the producing pipeline.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI5NzVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgOTc1IDY1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAxNDIgMzIgTCAyMTUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMjAuODggMzIgTCAyMTMuODggMzUuNSBMIDIxNS42MyAzMiBMIDIxMy44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZDVlOGQ0IiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5QaXBlbGluZSAxIChydW5uaW5nKTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzNDIgMzIgTCA0MTUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MjAuODggMzIgTCA0MTMuODggMzUuNSBMIDQxNS42MyAzMiBMIDQxMy44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjIyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNlOGUzZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAyMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+R2xvYmFsIFRlbnNvciAxPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDU1MiAzMiBMIDYyNS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDYzMC44OCAzMiBMIDYyMy44OCAzNS41IEwgNjI1LjYzIDMyIEwgNjIzLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI0MjIiIHk9IjIiIHdpZHRoPSIxMzAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZjZmZlNiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTI4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDQyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Db3BpZXIgUGlwZWxsaW5lICh3YWl0aW5nKTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3NjIgMzIgTCA4MzUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4NDAuODggMzIgTCA4MzMuODggMzUuNSBMIDgzNS42MyAzMiBMIDgzMy44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNjMyIiB5PSIyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNlOGUzZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEyOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiA2MzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+R2xvYmFsIFRlbnNvciAxIENvcHk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9Ijg0MiIgeT0iMiIgd2lkdGg9IjEzMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZDVlOGQ0IiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogODQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBpcGVsbGluZSAyIChydW5uaW5nZyk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjE2MiIgeT0iMTIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIycHg7IG1hcmdpbi1sZWZ0OiAxODJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5PdXQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjM2MiIgeT0iMTIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIycHg7IG1hcmdpbi1sZWZ0OiAzODJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5JbjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTcyIiB5PSIxMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjJweDsgbWFyZ2luLWxlZnQ6IDU5MnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPk91dDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNzgyIiB5PSIxMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjJweDsgbWFyZ2luLWxlZnQ6IDgwMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPkluPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxGraphModel&quot;:{&quot;dx&quot;:&quot;1166&quot;,&quot;dy&quot;:&quot;669&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;tooltips&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;arrows&quot;:&quot;1&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;pageHeight&quot;:&quot;1169&quot;},&quot;mxCellMap&quot;:{&quot;smfNQ1WE&quot;:{&quot;id&quot;:&quot;smfNQ1WE&quot;},&quot;hyQsOqfE&quot;:{&quot;id&quot;:&quot;hyQsOqfE&quot;,&quot;parent&quot;:&quot;smfNQ1WE&quot;},&quot;gItGtf55&quot;:{&quot;id&quot;:&quot;gItGtf55&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;source&quot;:&quot;SY0yPSTZ&quot;,&quot;target&quot;:&quot;XoaqtI96&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;SY0yPSTZ&quot;:{&quot;id&quot;:&quot;SY0yPSTZ&quot;,&quot;value&quot;:&quot;Pipeline 1 (running)&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;90&quot;,&quot;y&quot;:&quot;190&quot;,&quot;width&quot;:&quot;140&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;2W6RlLMD&quot;:{&quot;id&quot;:&quot;2W6RlLMD&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;source&quot;:&quot;XoaqtI96&quot;,&quot;target&quot;:&quot;y5KdQMDd&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;XoaqtI96&quot;:{&quot;id&quot;:&quot;XoaqtI96&quot;,&quot;value&quot;:&quot;Global Tensor 1&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#E8E3FF;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;310&quot;,&quot;y&quot;:&quot;190&quot;,&quot;width&quot;:&quot;120&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;mwSBlqn7&quot;:{&quot;id&quot;:&quot;mwSBlqn7&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;source&quot;:&quot;y5KdQMDd&quot;,&quot;target&quot;:&quot;MYIKj20r&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;y5KdQMDd&quot;:{&quot;id&quot;:&quot;y5KdQMDd&quot;,&quot;value&quot;:&quot;Copier Pipelline (waiting)&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#FCFFE6;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;510&quot;,&quot;y&quot;:&quot;190&quot;,&quot;width&quot;:&quot;130&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;hXT9nwCZ&quot;:{&quot;id&quot;:&quot;hXT9nwCZ&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;source&quot;:&quot;MYIKj20r&quot;,&quot;target&quot;:&quot;GjCQTPUz&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;MYIKj20r&quot;:{&quot;id&quot;:&quot;MYIKj20r&quot;,&quot;value&quot;:&quot;Global Tensor 1 Copy&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#E8E3FF;gradientColor=none;&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;720&quot;,&quot;y&quot;:&quot;190&quot;,&quot;width&quot;:&quot;130&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;GjCQTPUz&quot;:{&quot;id&quot;:&quot;GjCQTPUz&quot;,&quot;value&quot;:&quot;Pipelline 2 (runningg)&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;930&quot;,&quot;y&quot;:&quot;190&quot;,&quot;width&quot;:&quot;130&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;tjozmlJ2&quot;:{&quot;id&quot;:&quot;tjozmlJ2&quot;,&quot;value&quot;:&quot;Out&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;250&quot;,&quot;y&quot;:&quot;200&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;GzsXfxh2&quot;:{&quot;id&quot;:&quot;GzsXfxh2&quot;,&quot;value&quot;:&quot;In&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;450&quot;,&quot;y&quot;:&quot;200&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;64evYRcE&quot;:{&quot;id&quot;:&quot;64evYRcE&quot;,&quot;value&quot;:&quot;Out&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;660&quot;,&quot;y&quot;:&quot;200&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;NceHxTSj&quot;:{&quot;id&quot;:&quot;NceHxTSj&quot;,&quot;value&quot;:&quot;In&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;parent&quot;:&quot;hyQsOqfE&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;870&quot;,&quot;y&quot;:&quot;200&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}}},&quot;mxCellList&quot;:[&quot;smfNQ1WE&quot;,&quot;hyQsOqfE&quot;,&quot;gItGtf55&quot;,&quot;SY0yPSTZ&quot;,&quot;2W6RlLMD&quot;,&quot;XoaqtI96&quot;,&quot;mwSBlqn7&quot;,&quot;y5KdQMDd&quot;,&quot;hXT9nwCZ&quot;,&quot;MYIKj20r&quot;,&quot;GjCQTPUz&quot;,&quot;tjozmlJ2&quot;,&quot;GzsXfxh2&quot;,&quot;64evYRcE&quot;,&quot;NceHxTSj&quot;]},&quot;lastEditTime&quot;:0,&quot;snapshot&quot;:&quot;&quot;}" />


# --- END: Pipeline synchronization.md ---



# --- BEGIN: Plane detection.md ---

Plane detection is a key environmental sensing technology in augmented reality (AR) and mixed reality (MR), enabling systems to identify planes in the real world so that virtual objects can interact and integrate precisely with the physical environment.
Through plane detection, MR applications can identify and track horizontal, vertical, or inclined surfaces, such as floors, tabletops, walls, and sloped roofs, ensuring that virtual objects are accurately placed and stably aligned with the real-world space.




![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/517ae49b926243a8a35643280e348021~tplv-goo7wpa0wc-image.image)




![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/292c4a1b8cba45739b1f10477b6fd668~tplv-goo7wpa0wc-image.image)




![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b1ab05cc0f342638769be9618df9b76~tplv-goo7wpa0wc-image.image)




## Semantic labels
The semantic labels supported by plane detection (`PxrSemanticLabel`) are as follows:
| **Semantic Label** | **Description** |
| --- | --- |
| UnKnown | Objects that are not associated with any semantic label below. |
| Floor | A floor. |
| Ceiling | A ceiling. |
| Wall | A real-world wall. Doors and windows must exist within wall faces. |
| Door | A door, which must exist within a wall face. |
| Window | A window, which must exist within a wall face. |
| Opening | An open area. |
| Table | A table. |
| Sofa | A sofa. |
| Chair | A chair. |
| Curtain | A curtain. |
| Cabinet | A cabinet. |
| Bed | A bed. |
| Plant | A plant. |
| Screen | A screen. |
| VirtualWall | Virtual walls are automatically generated when scene capture stops. They have nothing to do with the real-world walls. Doors and windows cannot exist within virtual walls. <br> The virtual walls will form an enclosed space, containing both the real-world and virtual objects within it. In your app, you can add codes for detecting when the user enters or exits this enclosed space, and provide appropriate safety prompts or notifications. |
| Refrigerator | A refrigerator. |
| WashingMachine | A washing machine. |
| AirConditioner | An air conditioner |
| Lamp | A lamp. |
| WallArt | A wall art, which must exist within a wall face. |
## Start/stop plane detection functionality
Call `StartSenseDataProvider` and `StopSenseDataProvider` to start or stop the plane detection feature.
```C#
// Start plane detection functionality
PXR_MixedReality.StartSenseDataProvider(PxrSenseDataProviderType.PlaneDetection);
 
// Stop the plane detection function
PXR_MixedReality.StopSenseDataProvider(PxrSenseDataProviderType.PlaneDetection)
```

## Get the status of the Plane Detection Data Provider
Use `GetSenseDataProviderState` to obtain the status of the plane detection data provider.
```C#
PXR_MixedReality.GetSenseDataProviderState(PxrSenseDataProviderType.PlaneDetection,out var state)
```

## Get the plane detection data
By listening to the `PlaneDetectionDataUpdated` event, obtain data with `ChangeState`.
```C#
// Indicates the type of mesh data change in plane detection
public enum MeshChangeState
{
  Added, // Newly added mesh
  Updated, // Updated mesh
  Removed, // Removed meshes
  Unchanged, // Unchanged mesh
}

// Defines the spatial orientation type of detected planes
public enum PxrPlaneOrientation
{
    HorizontalUpward = 0, // A horizontal surface (such as the ground or a table)
    HorizontalDownward = 1, // Horizontally downward-facing surface (such as a ceiling)
    Vertical = 2, // Vertical plane (such as a wall surface)
    Arbitrary = 3, // Plane in any direction
}

// Contains complete information about the planes identified by the plane detection system
public struct PxrPlaneData
{
    public Guid uuid; // Unique identifier for the plane
    public Vector3 position; // Position of the plane in the world coordinate system
    public Quaternion rotation; // Rotation of a plane in the world coordinate system
    public PxrSemanticLabel label; // Semantic labels for surfaces (such as walls, floors, ceilings, and so on)
    public PxrSceneBox2D box2D; // Planar 2D bounding box information
    public ushort[] indices; // Index array of the planar mesh, used for constructing triangles
    public Vector3[] vertices; // Vertex array of the planar mesh
    public MeshChangeState state; // Planar mesh change state
    public PxrPlaneOrientation orientationMode; Plane direction mode
}

// Subscribe to plane detection data update event
void OnEnable()
{
    PXR_Manager.PlaneDetectionDataUpdated += PlaneDetectionDataUpdated;
}

// Unsubscribe from plane detection data update event to prevent memory leaks
void OnDisable()
{
    PXR_Manager.PlaneDetectionDataUpdated -= PlaneDetectionDataUpdated;
}

// This method is called when the PXR system detects changes in planar data
void PlaneDetectionDataUpdated(List<PxrPlaneData> planeDatas)
{
    //...
}
```

## AR Foundation
The SDK also supports implementing plane detection via AR Foundation. The specific capabilities supported are as follows:
| **Horizontal plane detection** | Horizontal plane detection: Indicates whether the provider's implementation supports detecting horizontal planes, such as the ground. |
| --- | --- |
| **Vertical plane detection** | Vertical plane detection: Indicates whether the provider's implementation supports detecting vertical planes, such as walls. |
| **Arbitrary plane detection** | Arbitrary plane detection: Indicates whether the provider's implementation supports detecting planes that are not aligned with either the horizontal or vertical axis. |
| **Boundary vertices** | Boundary vertex: Indicates whether the provider's implementation supports supplying boundary vertices for its planes. |
| **Classification** | Category: Indicates whether the provider implementation can supply values for [ARPlane.classifications](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@5.1/api/UnityEngine.XR.ARFoundation.ARPlane.html#UnityEngine_XR_ARFoundation_ARPlane_classification). |


# --- END: Plane detection.md ---



# --- BEGIN: Play HDR videos.md ---

Compositor layers of the "External Surface" texture type supported playing back HDR videos and dynamically setting the HDR type (`HDRFlags`) based on the video's type during playback. Below are the enumerations of `HDRFlags`:
```C#
public HDRFlags hdr = HDRFlags.None;
public enum HDRFlags
{
    None, // disable HDR video playback
    HdrPQ, // PQ mode, which supports remapping HDR sources that comply with the ST.2084 standard to SDR in order to achieve accurate display effects.
    HdrHLG, // HLG mode, which supports remapping HDR sources that comply with the HLG standard to SDR in order to achieve accurate display effects.
 }
```


# --- END: Play HDR videos.md ---



# --- BEGIN: Preview scenes in real time.md ---

Based on the streaming capability, you can use the PDC tool to preview your app in real time on the HMD.
## What you can preview

* Virtual scenes
* Hand tracking

## Supported operating system
Windows only.
## Important notes

* Using the PICO Connect app will cause the PDC streaming service to malfunction. Therefore, before using the PDC tool, ensure you have closed the PICO Connect app on both your PC and headset.
* Using the PICO Connect app and the PDC tool together will cause exceptions to the PDC tool. Therefore, make sure to close the PICO Connect software on both your PC and HMD before using the PDC tool.
   This restriction does not apply to PICO 4 Ultra or Project Swan series devices.

## Before you begin
Refer to the "[PICO Developer Center overview](/13136/en_pdc-basic-info#f5a5a632)" article to complete preparatory tasks, including installing the PDC tool, enabling the "Developer" mode for your PICO device, and connecting your PICO device to the PC.
## Procedure
### Project Swan

1. Download the [PICO Unity SDK (OS-6 Preview)](https://developer.picoxr.com/resources/?platform=unity).
2. Preview scenes in real time by using the steps given in [this article](/document/unity-swan/live-preview-tool/).

### PICO 4 Ultra and other device models
Use the following steps to preview scenes in real time using the PDC tool:

1. Download the [PICO Unity Live Preview Plugin](https://developer-global.pico-interactive.com/resources/#sdk) package and unzip it.
   This gives you a package.json file in the folder.
2. Connect your PC and the headset with a streaming cable.
3. Open your project in the Unity Editor.
4. Go to **Window** > **Package Manager** > **+** > **Add package from disk**, and import the package.json file into your project.
5. Go to **Edit** > **Project Settings** > **XR Plug-in Management** > **PC Standalone Settings**, and check **PICO Live Preview**.
   If this list shows the **PICO** option, make sure it is NOT selected.

   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b4277b6480544d0b7454ecdb5be2625~tplv-goo7wpa0wc-image.image)
6. Open the target scene and click the **Play** button at the top of the scene.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1c8580ed5dd49d1ae842e15c774314e~tplv-goo7wpa0wc-image.image)
   The device's status becomes "Streaming" in the PDC tool, which indicates that the preview capability is working and the HDM is therefore displaying the scene in real time.

## Troubleshooting
Refer to the "[PDC Troubleshooting](/en_pdc-troubleshooting)" article.
###


# --- END: Preview scenes in real time.md ---



# --- BEGIN: Profanity detection.md ---

Your apps must adhere to the laws and regulations of their respective distribution regions, otherwise you and your apps risk facing penalties such as fines, removal from the market, or bans. The PICO platform services provides the profane word detection capability to help you prevent compliance-related issues.
## Use cases
The SDK supports detecting profane words in texts such as user names, room names, and in-room-chat messages.
## Important note
The profanity detection service is only available in Mainland China.
## Details
The profanity detection service covers profane word detection, strategy detection, and model detection. These three types of detection work together to ensure that users can express themselves freely while also limiting the publication of malicious user-generated content as much as possible.
| **Detection Type** | **Description** |
| --- | --- |
| Profane word detection <br>  | To detect instances of profane words in text and prevent the publication of such text. This type of detection is capable of recognizing profane words related to political topics, pornography, and more. |
| Strategy detection <br> (back-end capability) | To identify specific styles of user-generated content (UGC) samples by combining and analyzing the characteristics of UGC.  |
| Model detection <br> (back-end capability) | To identify specific UGC using the models trained by machine learning. |
## API reference

* [Client API](/reference/unity/client-api/ComplianceService/)
* [Server API](/reference/unity-server/latest/detect-sensitive-words/)


# --- END: Profanity detection.md ---



# --- BEGIN: Push URLs to a PICO device.md ---

You can use the quick tools provided by the PICO Developer Center to push specified URLs to a PICO device, and the PICO Browser app on the device will open these URLs.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d21936fb5b24ffdbfa498cfec12a7d5~tplv-goo7wpa0wc-image.image" width="700px" />

## Before you begin
Refer to the "[PICO Developer Center overview](/13136/en_pdc-basic-info#f5a5a632)" article to complete general setups, including installing the PDC tool, enabling the "Developer" mode for your PICO device, and connecting your PICO device to the PC.
## Procedure

1. Launch the PICO Developer Center.
2. In the **PICO Browser** field of the **Quick Tools** section, enter the URL you want to open on the device, and click **Run**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f82f03a989c845c2bd7b5b87a674f04f~tplv-goo7wpa0wc-image.image)
   The website will be opened within the PICO Browser app on your headset.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9723f9d9b7394295a56cb4103c8c721b~tplv-goo7wpa0wc-image.image)


# --- END: Push URLs to a PICO device.md ---



# --- BEGIN: Room & Matchmaking.md ---

Room & Matchmaking service offers features such as player-to-player networking, matchmaking, room management, and inter-player messaging. The major features are room management, matchmaking, and messaging.
## Use cases
The key application scenarios of Room & Matchmaking service are as follows:

* **Real-time gaming**
   Provides features like room management and matchmaking. Matched players can join the same room to play games together.
* **Real-time interaction**
   Provides the feature of real-time in-room messaging. Players in the same room can send messages to and receive messages from others to enjoy real-time interaction.

## Basic concepts
The basic concepts of Room & Matchmaking service are described below.
| **Concept** | **Description** |
| --- | --- |
| Matchmaking pool | Matchmaking pools are created by developers for matchmaking. Developers can configure matchmaking options for matchmaking pools to make results more in line with expectations. |
| Room | Rooms can be created by players or the system. Matched players join the same room for gaming. |
| Lock a room | After a room is locked, players outside the room are unable to join it. |
## Key features
### Room
The Room feature covers sub-features such as creating rooms, getting room information, editing room data, changing room ownership, and leaving a room.
#### Room types
The Room feature supports four types of rooms, including private rooms, named rooms, moderated rooms, and matchmaking rooms. 
| **Room Type** | **Description** |
| --- | --- |
| Private room | Private rooms are created by players. Relevant descriptions are as follows: <br>  <br> * You can call `RoomService.Get()` and specify the `roomID` parameter to get the information of a specific room and display the information to relevant users. <br> * You can call `RoomService.UpdateMembershipLockStatus()` to allow room owners to lock their rooms. After a room is locked, users outside the room are unable to join it and users who already joined the room before it was locked can rejoin after leaving the room. <br> * You can call `RoomService.CreateAndJoinPrivate2()` to allow users to create rooms, join the rooms they create, and become the owner of these rooms at the same time. `RoomService.CreateAndJoinPrivate2()` includes the `joinPolicy` and `maxUsers` parameters. The `joinPolicy` parameter is for defining who can join the room, and the `maxUsers` parameter is for specifying the maximum number of players allowed in the room. <br> * You can call relevant APIs to allow room owners to kick users out (`RoomService.KickUser`), update rooms' metadata (`RoomService.UpdateDataStore`), update rooms' join policies (`RoomService.UpdatePrivateRoomJoinPolicy`), lock rooms' membership (`RoomService.UpdateMembershipLockStatus`), and set or edit rooms' descriptions (`RoomService.etDescription`). <br> * In-room users can receive event notifications when someone joins or leaves the room. They can also send messages to and receive messages from other in-room users. <br> * You can call `RoomService.Leave()` to allow users to leave rooms. <br> * After the room owner leaves the room, the ownership of the room will be automatically given to the user that has stayed in the room for the longest period of time. You can call `RoomService.UpdateOwner` to allow room owners to manually transfer ownership to someone else. <br> * After all users have left a room, the room will be destroyed. |
| Named room | Named rooms are created by users. Users can name rooms when creating them. Below are relevant functions: <br>  <br> * `RoomService.JoinOrCreateNamedRoom`: Join or create a named room. <br> * `RoomService.GetCreateNamedRoomOptions`: Get the options to set for joining or creating a named room. <br> * `RoomService.GetNamedRooms`: Get a list of named rooms for the current app. |
| Moderated room | Moderated rooms are created by game servers and are visible to all users. You can create and manage the lifecycle of moderated rooms using Restful API. Users can choose to use their own servers to interact with PICO rooms using Restful API |
| Matchmaking room | Matchmaking rooms are created by the matchmaking service. After a matchmaking room is created, the matchmaking service will randomly select an in-room user as the room owner. Relevant descriptions are as follows: <br>  <br> * You need to create matchmaking pools on the PICO Developer Platform for matchmaking. <br> * You can call `Enqueue2` to allow users to join matchmakings. Users can set the values of the fields specified in the custom data and also set the pre-selected query to improve matchmaking accuracy. <br> * You can call `MatchmakingCancel2` to allow users to exit matchmakings at any time. <br> * Matched users will receive a notification (`Notification_Matchmaking_MatchFound`). You then need to obtain the room number from the notification and call `JoinRoom2` to let matched users join the same room. <br> * In-room users will get event notifications when someone joins or leaves the room. They can also send messages to and receive messages from other in-room users. |
#### In-room notification
You can add a listener to the game loop to get notifications. For example, you can call `Notification_Room_RoomUpdate` to allow users to get room updates. The callback function of this API is configured as follows:
```C#
public static void SetUpdateNotificationCallback(Message<Room>.Handler handler) 
{ 
    Looper.RegisterNotifyHandler(
        MessageType.Notification_Room_RoomUpdate, 
        handler
    ); 
}
```

### Matchmaking
The Matchmaking feature covers sub-features such as joining matchmakings, browsing the rooms that match the configured matchmaking options, creating matchmaking rooms, and notifying players when games start.
#### Matchmaking process
The typical matchmaking process is as follows:

1. You create one or multiple matchmaking pools.
2. You associate one or multiple matchmaking pools to one or more apps.
3. The system adds users to one or more pools after receiving matchmaking requests and adds users that match the preset matchmaking options to the same pool.
4. The system notifies matched users when a match is made.
5. The matched users join the same room.

* The matchmaking result is determined by the matching value (match_val) which ranges from 0 to 1. The higher the matching value, the higher the matching level. When determining the matching value among users, the system will refer to their skill levels and other related statistics as well. When the matching value exceeds the preset minimum matching threshold (matchbias), a match is made. The longer the users wait in matchmaking pools, the smaller the minimum matching threshold and the easier for them to be matched.
* To make matchmaking easier in complex matchmaking scenarios, in addition to automatic system matchmaking, you can call `RoomService.CreateAndJoinPrivate2()` to allow players to create and join rooms and call `Browse2` to allow players to browse existing rooms.

#### Matchmaking modes
Three matchmaking modes can be implemented through corresponding matchmaking pool configuration. Refer to the *Create a matchmaking pool* section for details.
### Messaging
The Messaging feature covers the following sub-features. You can define the content and format of messages.

* In-room messaging customization
* Inter-user messaging in the same room
* Message broadcasting to all users in the same room

## Important notes

* You need to monitor network events when using "Room & Matchmaking" service. If users come across network disconnection and reconnection issues, you will receive the following event notification:
   ```C#
   void Start()
   {
       NetworkService.SetNotification_Game_ConnectionEventCallback(OnGameConnectionEvent);
   }
   
   ...
   void OnGameConnectionEvent(Message<GameConnectionEvent> msg)
   {
       var state = msg.Data;
       LogHelper.LogInfo(TAG, $"OnGameConnectionEvent: {state}");
       if (state == GameConnectionEvent.Connected)
       {
           LogHelper.LogInfo(TAG, "GameConnection: success！");
       }
       else if (state == GameConnectionEvent.Closed)
       {
           Uninitialize();
           LogHelper.LogInfo(TAG, "GameConnection: fail！Please re-initialize！");
       }
       else if (state == GameConnectionEvent.GameLogicError)
       {
           Uninitialize();
           LogHelper.LogInfo(TAG, "GameConnection: fail！After successful reconnection, the logic state is found to be wrong，Please re-initialize！");
       }
       else if (state == GameConnectionEvent.Lost)
       {
           LogHelper.LogInfo(TAG, "GameConnection: Reconnecting, please wait！");
       }
       else if (state == GameConnectionEvent.Resumed)
       {
           LogHelper.LogInfo(TAG, "GameConnection: successful reconnection！");
       }
       else if (state == GameConnectionEvent.KickedByRelogin)
       {
           Uninitialize();
           LogHelper.LogInfo(TAG, "GameConnection: Repeat login! Please reinitialize！");
       }
       else if (state == GameConnectionEvent.KickedByGameServer)
       {
           Uninitialize();
           LogHelper.LogInfo(TAG, "GameConnection: Server kicks people! Please reinitialize！");
       }
       else
       {
           LogHelper.LogInfo(TAG, "GameConnection: unknown error！");
       }
   }
   ```

   The `Lost` event indicates that the user has been disconnected, and you need to stop sending requests to the client. The `Resumed` event indicates that the user has been reconnected. It is recommended that you notify users of a reconnecting status through adding a reconnecting icon in the middle of the screen or other practical ways.
* If an app is moved to the background, `popMessage` will cease, causing the server to be unable to receive heartbeats from the app. If this situation lasts for a long period of time, the app will be disconnected from the server, and messages generated during the disconnection period will be lost. After the app is moved to the foreground, it will reconnect with the server.

## Integrate the Room & Matchmaking service
### Step 1: Import the SDK and complete project settings
Import the PICO Unity Integration SDK into your project and complete required project settings. Refer to the following articles for detailed instructions:

* [Import the SDK](/en_import-the-sdk)
* [Complete project settings](/en_complete-project-settings)

### Step 2: Enable Matchmaking service
You need to enable Matchmaking service for your app on the PICO Developer Platform. If your app is published on both the PICO Store (Chinese Mainland) and PICO Store (Outside Chinese Mainland), you can enable Matchmaking service for your app in one or both of the store regions.Below are the steps to follow:

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/organization/).
2. From the left navigation pane, select **My Apps**.
   This directs you to the **My Apps** screen.
3. Click on the target app.
   This directs you to the app's **Overview** screen.
4. From the left navigation pane, select **Platform Service** > **Matchmaking**.
   This directs you to the following screen:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed85becc19894427b9e006377b0e7740~tplv-goo7wpa0wc-image.image)
5. Select the store region to enable service for: **Chinese Mainland** or **Non-Chinese Mainland**.
6. Click **Start Service**.
   The following pop-up window appears:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/22bf8b5eed9a4a489c5d4d80bb66980e~tplv-em5hxbkur4-noop.image?width=900&height=384)
6. Click **OK**.
   The platform starts to enable Matchmaking service for your app. After that, you need to create matchmaking pools for your app.

### Step 3: Create a matchmaking pool
After enabling Matchmaking service for your app, you can create one or multiple matchmaking pools for it and configure desired matchmaking pool details. Then you can add queries and custom data to the matchmaking pool for desired matchmaking effects. If your app is published on both the PICO Store (Chinese Mainland) and PICO Store (Outside Chinese Mainland), you can create matchmaking pools for your app in one or both of the store regions.
**Create a matchmaking pool** 
Use the following steps to create a matchmaking pool:

1. Select the store region to create a matchmaking pool for: **Chinese Mainland** or **Non-Chinese Mainland**.
2. Click **Add Matchmaking Pool**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a57adacd81b4bd0a3342b73da097823~tplv-goo7wpa0wc-image.image)
3. Follow the on-screen instructions to configure matchmaking pool settings. 
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df6729a15d49491ebf681e606ca0aa04~tplv-goo7wpa0wc-image.image)
   Below are field descriptions:
   | **Field** |  | **Description** |
   | --- | --- | --- |
   | Name |  | The name of the matchmaking pool. |
   | Key |  | The unique identifier of the matchmaking pool. |
   | Number of Matchmade Users <br>  |  | Includes: <br>  <br> * Minimum Number of Users <br> * Recommended Minimum Number of Users <br> * Recommended Maximum Number of Users <br> * Maximum Number of Users <br>  <br> If the number of players is between the **recommended minimum and maximum number of users**, a match is made instantly. <br> If the number of players is not in the recommended range but is between the **minimum and maximum number of users**, users have to wait for a certain period of time for the number of users to reach the preferred range. However, if the number of users is still out of the preferred range after that period of time, a match is made. |
   | Managed Rooms <br> > Set the four fields provided on the right side if you select **Yes** for this field. <br>  <br>  | Who Can Create Rooms <br>  | Set who can create rooms. Below are available options. You can select multiple options if needed. <br>  <br> * **User**: Allow users to create private rooms <br> * **Matchmaking Service**: Allow the matchmaking service to create matchmaking rooms <br>  <br> You need to select at least one option; otherwise, there will be no room for matchmaking. If you select both options, both private rooms and matchmaking rooms will be available in the matchmaking pool. In this case, users sending a matchmaking request will randomly join the user-created private rooms or mathmaking-service-created matchmaking rooms. |
   |  | Allow Unmatched Users to Join Matchmaking Rooms | Set whether to allow non-matchmaking-service-matched users to join the room, in other words, whether allow users to browse joinable rooms and select one from them to join. <br> If enabled, users not matched by the matchmaking service may join rooms. For example, room members can invite their friends to join.  <br> If disabled, only matchmaking-service-matched users can join. |
   |  | Allow Matching Into the Same Room | Set whether to allow users to join the same room after a match has been made, for example, joining an in-progress game. <br> If enabled, the matchmaking service may match users to the same room multiple times, for example, matching users to an in-progress game.  <br> If disabled, the room will be removed from the matchmaking queue once a match is made. |
   |  | Automatic Transfer When Owner Leaves Room | If enabled, after the current room owner leaves the room or disconnects, the user staying in the room for the longest time will automatically become the new room owner.  <br> If disabled, after the current room owner leaves the room or disconnects, there will be no room owner. |
   | Matchmaking Degree Threshold |  | The minimum match-made threshold that ranges from 0 to 1, and 1 indicates a perfect match. A match is made only if the actual matchmaking degree is equal to or greater than the configured threshold. |
   | Matchmaking Reserved Period (s) |  | Room reservation time (in seconds). When a user has been matched to a room, the system will reserve a certain period of time for the user to enter the room. If the user does not enter the room after the reserved period, the room will be released. |
   | Suggested Cooldown Time (s) |  | Matchmaking cooldown time (in seconds). If a user has been matched to a room but the room is released because the user has not entered the room within the reserved period, the user will be able to be matched to the same room after the cooldown time. |
   Three matchmaking modes can be implemented through corresponding matchmaking pool settings. The details are described below:
   | **Mode** | **Matchmaking Pool Configuration** | **Description** |
   | --- | --- | --- |
   | Basic | Configures matchmaking pools as described below: <br>  <br> * **General settings**: Set rampdown, number of players, and so on. <br> * **datasetting**: Set the fields used in queries. <br> * **query**: Create expressions that use the preset datasetting, and set importance levels for expressions. <br> * **Managed Rooms** = No <br>  <br>  | In the Basic mode, all users join matchmakings in the same matchmaking pool. Matched users will join the same room, and other users cannot join this room later or midway. After all users have left a room, the room will be destroyed.  <br> **What you need to do:** <br>  <br> * Provide a "Search for Matches" entry for users as well as matchmaking options including available matchmaking pools, available expressions, and relevant fields for users to choose and configure. <br> * Call `RoomService.Join2` to allow matched users to join a room after receiving the match-found notification. <br> * Call `RoomService.UpdateDataStore` to allow users to configure and read room-related data such as the current on-going game level and game progress. <br>  <br> **User experience:** <br>  <br> * Users are unable to create rooms. They can only join rooms after being matched by the system. <br> * Users are allowed to select game types. For the internal feature logic, game types represent matchmaking pools. <br> * Users are allowed to set search conditions for auto-matchmaking. For the internal feature logic, setting search conditions represents selecting expressions and setting the values of the fields defined in the custom data. For example, users can set the values of corresponding fields to require playing a certain game level with users of similar skill levels. |
   | Advanced | The specific configuration for Advanced mode is as follows: <br>  <br> * **Managed Rooms** = Yes <br> * **Who Can Create Rooms** = User / Matchmaking Service / User & Matchmaking Service <br> * **Allow Unmatched Users to Join Matchmaking Rooms** = Disable <br> * **Allow Matching Into the Same Room**: Set the value of this field according to whether to allow users to join a room midway <br>  <br>  | In Advanced mode, users are allowed to create rooms and wait for matched users to join the rooms for gaming. You can set advanced matchmaking options to satisfy a broader range of matchmaking requirements. <br> **What you need to do:** <br>  <br> * Provide a "Search for Matches" entry for users. Matched users will join the same room for gaming. <br> * Provide users with room-creation related options including the available matchmaking pool(s) and field settings if users are allowed to create rooms. <br> * Call `NetworkService.SendPacket` to allow players to send messages to a specified player in the room. <br> * Call `NetworkService.SendPacketToCurrentRoom` to allow players to send messages to all other players in the room. <br> * Call `NetworkService.ReadPacket` to allow players in the room to read the messages. <br>  <br> **User experience:** <br>  <br> * Users are allowed to set search conditions for auto-matchmaking.  <br> * If users are allowed to create rooms, they can set room-creation options to create rooms of desired characteristics. <br> * According to the value of the **Allow Matching Into the Same Room** field, users can usually join the rooms where games are in progress. |
   | Browsing | The specific configuration for Browsing matchmaking mode is as follows: <br>  <br> * **Managed Rooms** = Yes <br> * **Who Can Create Rooms** = User / User & Matchmaking Service <br> * **Allow Unmatched Users to Join Matchmaking Rooms** = Enable <br> * **Allow Matching Into the Same Room**: Set the value of this field according to whether to allow users to join midway <br>  <br>  | Browsing mode enables users to create rooms and to join a room chosen from the list of private rooms. In this mode, all rooms are created by users, and users are not matched by the matchmaking service. The system will return a list of joinable rooms to the user. <br> **What you need to do:** <br>  <br> * Must provide users with the "Create Room" entry and room-creation related options, including available matchmaking pools and field settings. <br> * After receiving requests for room lists from users, query room lists from the server and display the lists to them. <br> * Call `NetworkService.SendPacket` to allow players to send messages to a specified player in the room. <br> * Call `NetworkService.SendPacketToCurrentRoom` to allow players to send messages to all other players in the room. <br> * Call `NetworkService.ReadPacket` to allow players in the room to read the messages. <br>  <br> **User experience:** <br>  <br> * If users are allowed to create rooms, they can set room-creation related options to create rooms with desired settings. <br> * Users are allowed to configure browsing options to query and join target rooms. <br> * Users need to send requests to the server when joining rooms. |
4. Click **Save**.
   The platform will then add the matchmaking pool to the app. You can proceed to add the custom data.

**Add the custom data**
You need to configure the parameters and values for matchmaking in the code by yourself, then add them here as custom data.

Custom data is used to configure queries. After creating a matchmaking pool, you can add custom data. Below are the steps to follow:

1. Return to the matchmaking pool list.
2. Click the number (**0** for a newly-created pool) on the **Queries** column.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3722e8b5f0ce41dcbfb072de54b2153e~tplv-goo7wpa0wc-image.image)
   This directs you to the following screen:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc9eb03c53e34c5ca67c49435fd6595e~tplv-goo7wpa0wc-image.image)
3. Click **+ Custom Data**.
   This directs you to the Create Custom Data pane.
4. Follow the on-screen instructions to set the custom data. Below are field descriptions:
   | **Field** | **Description** |
   | --- | --- |
   | Data Key | The unique identifier of the custom data, for example, Level, which should be the same as the name of the corresponding parameter you set in the code. |
   | Data Type | Includes: <br>  <br> * Floating Point <br> * Integer <br> * Hexadecimal |
   | Default Value | The default value for the custom data, which works as a baseline value. For example, if: <br>  <br> * The parameter (corresponds to the data key) you set in the code is `Level`. <br> * Value `0` represents level 20 and value `1` represents level 30. <br> * The data key you set on the PICO  Developer Platform is **Level** and the default value you configure for it is **0**. <br>  <br> When a user with no historical data joins matchmaking in this matchmaking pool, the system values this user as **0** by default, which means that the system regards this user as a level 20 user by default. |
5. Click **Save**.
   The custom data is created. You can proceed to add a query.

**Add a query（Query）**
Before adding queries, you must add custom data first.

Queries are used to determine whether several players meet the matchmaking conditions. A query consists of one or multiple expressions used to calculate the matchmaking degree among players. If the matchmaking degree is equal to or exceeds the predefined matchmaking degree threshold, a match is made, otherwise, the matchmaking fails. Below are the steps to adding a query:

1. Return to the following screen:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b00bfed0943f43bbba2e4edc0605b1cd~tplv-goo7wpa0wc-image.image)
2. Click **+ Create Query**.
   This directs you to the **Create Query** pane.
3. Follow the on-screen instructions to configure query fields. Below are field descriptions:
   | **Field** | **Description** |
   | --- | --- |
   | Query Key | The unique identifier of the query. |
   | Expression Weight | The weight (importance level) of an expression, including **Required**, **High**, **Medium**, and **low**. The higher the expression's weight, the less the value it has when calculating the final matchmaking degree by multiplication. For the factors each weight has, Required=0, High=0.55, Medium=0.75, and Low=0.9. Therefore: <br>  <br> * If two users fail to meet the required expression, the matchmaking definitely fails as the matchmaking degree is multiplied by 0.  <br> * If the two users meet the required expression but fail to meet the expression(s) of other weight(s), the matchmaking result is then determined by the final matchmaking degree generated by multiplying all expressions' values. |
   | Expression | Expressions are used to calculate the matching degree among players. A query can consist of multiple expressions, and each expression is given an individual weight (required, high, medium, or low). The result of an expression is a bool value which will be turned into an expression value according to the expression's weight. To be specific: <br>  <br> * If the result of an expression is `true`, which indicates the expression has been met by players (for example, two players are of the same level), the expression's value will be 1. <br> * If the result of an expression is `false`, the expression's value will be calculated from the expression's weight.  <br>  <br> The system then multiplies all expressions' values to come up with the final matching degree. |
4. Click **Save**.
   A query is created. At this point, the matchmaking pool has been fully created and configured.

### Step 4: Initialize platform services globally and the game module

* Initialize platform services globally. You can call `CoreService.Initialize()` for synchronous initialization or call `CoreService.AsyncInitialize()` for asynchronous initialization.
* Call `CoreService.GameInitialize` to initialize the game module.

For detailed instructions and code samples, refer to the "[Initialization](/en_initialization)" article.
### Step 5: Implement the Room & Matchmaking service
The SDK provides a series of APIs, and you can use them to implement the Room & Matchmaking service in your app.

* For more details about APIs, refer to the [API reference](/en_matchmaking#API%20reference) section.
* For code samples, refer to the [Demo](/en_matchmaking#Demo) section.

## Demo

* You can use the RoomAndMatchmakingEntry demo and GameAPITest demo to debug "Room & Matchmaking" service. For more information, refer to the "[Room & Matchmaking demo](/en_room-and-matchmaking-demo)" article.

<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/144969f983c2479181c0085b9d039311~tplv-em5hxbkur4-noop.image?width=1790&height=1000" width="700px" />

<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/119d41c74dd847f2b2073ea8c5cbd9d5~tplv-em5hxbkur4-noop.image?width=2128&height=1040" width="700px" />

* The Space Arena Party demo integrates the Room & Matchmaking service. For more information, refer to the "[Space Arena Party](/en_space-arena-party)" article.

## API reference
You can use "Room & Matchmaking" APIs for relevant management and settings:

* [Room](/reference/unity/client-api/RoomService/)
* [Matchmaking](/reference/unity/client-api/MatchmakingService/)


# --- END: Room & Matchmaking.md ---



# --- BEGIN: RTC.md ---

Real-time communications (RTC) technology enables users in the same room to communicate with each other through voice chat.
PICO RTC service uses a centralized communication structure instead of an end-to-end one. After users have joined a room and enabled voice chat, the microphone keeps capturing audio data from users and uploading the data to the RTC server. Then, the RTC server transmits the audio data to each client in the room, and the client broadcasts the audio data received.
## Basic concepts
The basic concepts of the RTC service are as follows:
| **Concept** | **Description** |
| --- | --- |
| RTC | Real-time communications. Mainly refers to real-time voice chat here. |
| Room | Room is the basic unit for voice chat. Users in the same room can communicate with each other. Therefore, the developer only needs to join users in the same room to let them communicate with each other. |
| Room ID | Room ID (`roomID`) is a nun-empty string consisting of no more than 128 bytes. It is defined by the developer. The following character sets are supported: <br> ● Uppercase letters: A ~ Z <br> ● Lowercase letters: a ~ z <br> ● Numbers: 0 ~ 9 <br> ● Special characters: underline (_), at symbol (@), minus sign (-) |
| Stream | A continuous audio data flow. |
## Feature descriptions
"Stream publish/subscribe" is also an important concept that helps you to better understand the RTC service. The process of "stream publish/subscribe" is as follows:

1. After users join a room and start voice chat, the microphone keeps capturing audio data and uploading the data to the RTC server.
2. The RTC server transmits the audio data to all clients in the room.
3. Clients play the audio.

RTC service offers three levels of "audio stream publish/subscribe":

* Global audio stream publish/subscribe
* In-room audio stream publish/subscribe
* User-specific audio stream publish/subscribe

### Room
Joining and leaving rooms is the most basic room-related operation. Developers will be notified after users join or leave rooms.
Token is used for permission management in RTC service is required for joining a room. Developers can bind one or more permissions to a token and set a validity period for each permission. The developer will be notified when the token is about to expire. In this case, the developer can call `updateToken` to renew the token. Once a token has expired, the in-room users will be unable to enjoy the permissions bound to the token.
After users have joined a room, the server will regularly send room statistics to the developer, such as the number of in-room users and how long the users have stayed in the room. In addition, RTC service allows users to join multiple rooms at the same time and subscribe to the audio streams of all these rooms. However, a user can only publish local audio streams to one room at the same time.
After all users have left a room, a room object will be left in memory. The developer needs to destroy the room to release resources.
### Audio management
RTC service offers global audio control APIs covering the following features:

* Start/stop audio recording
* Set audio recording volume
* Set playback volume
* Set in-ear monitoring volume
   In RTC service, volume is an int value which ranges from 0 to 400. 100 represents the original volume, [0,100] indicates that the volume decreases, and [100,400] indicates that the volume increases.
* Enable/Disable in-ear monitoring
   If in-ear monitoring is enabled, the speaker will play local audio. By default, in-ear monitoring is not enabled.
* Set the volume for a remote user
* Set audio scenarios
   RTC service provides a range of audio scenarios. In different scenarios, the audio will be processed in different ways, including noise cancellation, echo elimination, and more. Meanwhile, the volume type applied also varies by the audio scenario type. RTC service provides the following two volume types:
   * Call volume: using call volume can better eliminate echos.
   * Media volume: using media volume can better keep the initial status of the audio.
   Specifically, the volume type applied is determined by the following:
   * Audio scenario type
   * Device's recording status
   * Earphone type: system, wired, bluetooth.
   When adjusting the volume, only the media volume will be displayed on the UI. Therefore, when adjusting the call volume, the volume bar may not change. Using the pure media-volume scenario or game streaming scenario can solve this problem.

   | **Audio Scenario Type** | **Description** | **Earphone Type** | **Volume Type (non-recording)** | **Volume Type (recording)** |
   | --- | --- | --- | --- | --- |
   | Music scenario (default) | Suitable for scenarios that require high musical performance, such as live music streaming. | System | Media volume | Call volume |
   |  |  | Wired | Media volume | Media volume |
   |  |  | Bluetooth | Media volume | Media volume |
   | High-quality calling scenario | This scenario balances the audio experience with/without the bluetooth headset and avoids changes in hearing caused by volume type switching when using the bluetooth headset. <br> Suitable for scenarios where high musical performance is required. However, you may need to use the microphone on the bluetooth headset for audio capture. | System | Media volume | Call volume |
   |  |  | Wired | Media volume | Media volume |
   |  |  | Bluetooth | Call volume | Call volume |
   | Pure call-volume scenario | In this scenario, call volume is used throughout the process regardless of the audio publish/subscribe status.. This scenario has the following advantages: <br>  <br>    * Uses one audio mode throughout the process, thereby avoiding sudden volume change. <br>    * Eliminates echos to the greatest extent possible so as to bring the optimal call quality. <br>  <br>  <br> However, the volumes of other audios played with the media volume will be lowered and the sound quality will be lowered as well. <br> Suitable for scenarios (e.g., conferences) where the users frequently turn their microphone on and off. | System | Call volume | Call volume |
   |  |  | Wired | Call volume | Call volume |
   |  |  | Bluetooth | Call volume | Call volume |
   | Pure media-volume scenario | Not recommended for use. <br> In this scenario, media volume is used throughout the process regardless of the audio publish/subscribe status. <br> ***Note***: When using the speaker, echoes and whistles are very likely to occur. | System | Media volume | Media volume |
   |  |  | Wired | Media volume | Media volume |
   |  |  | Bluetooth | Media volume | Media volume |
   | Game streaming scenario | In this scenario, bluetooth headsets use the call volume, while other audio devices use the media volume. <br> Suitable for games only. <br> ***Note***: When this scenario is used without canceling game sound effects, echoes and whistles are very likely to occur. | System | Media volume | Media volume |
   |  |  | Wired | Media volume | Media volume |
   |  |  | Bluetooth | Call volume | Call volume |

### Audio stream publish/subscribe
Stream is a continuous audio data flow. After subscribing to audio streams, the RTC server will continuously push captured audio streams to the client. After publishing audio streams, the client will continuously push local audio streams to the RTC server. RTC service offers audio stream publish/subscribe APIs covering the following features:

* **Publish/Unpublish local audio stream**
   * Call `RtcService.PublishRoom()` to publish the local audio stream, thereby making other in-room users hear the local user's voice.
   * Call `RtcService.UnPublishRoom()` to cancel publishing the local audio stream, thereby "muting" the local user in the room.
   A user can only publish the local audio stream to one room at the same time. If the user wants to publish the local audio stream to another room, `RtcService.UnPublishRoom()` should be called first to stop publishing the local audio stream to the current room and then `RtcService.PublishRoom()` should be called.
* **Handle remote audio stream publishing/unpublishng event**
   * When calling `RtcService.PublishRoom()`, other in-room users will receive a notification that a remote user has published audio streams. You can set the callback through `RtcService.SetOnUserPublishStream()`.
   * When calling `RtcService.UnPublishRoom()`, other in-room users will receive a notification that a remote user has cancelled publishing audio streams. You can set the callback through  `RtcService.SetOnUserUnPublishStream()`.
* **Subscribe/Unsubscribe to remote audio streams**
   * **All in-room audio streams**: call `RtcService.RoomResumeAllSubscribedStream()` to subscribe to the audio streams from all in-room users, thereby making the local user hear other users' voices; call `RtcService.RoomPauseAllSubscribedStream()` to cancel subscribing to the audio streams from all in-room users, thereby making the local user unable to hear other users' voices.
   * **A specific user's audio stream**: call `RtcService.RoomSubscribeStream()` to subscribe to the audio stream from a specific user; call `RtcService.RoomUnSubscribeStream()` to cancel subscribing the audio stream from a specific user.

### Custom message
Custom messages include text messages and binary messages. Users can send messages to a room or to a specific user. For those sent to a room, all in-room users can read them. For those sent to a specific user, only the user can read them. Each of the two types of message maintains an auto-incrementing int64 message ID for both the text or binary message.
After calling the APIs for sending custom messages, an int64 message ID will be returned. Later, the local user will receive a callback indicating whether the message was successfully sent, including the message ID. It should be noted that the size of a binary message should not exceed 64KB, and the size of a text message (UTF-8 format) should not exceed 64KB.
| **API** | **Description** | **Sending-Result Callback** <br> i.e., the callback received by the message sender | **Receiving-Result Callback** <br> i.e., the callback received by the message receiver |
| --- | --- | --- | --- |
| `SendUserMessage()` | Send a text message to a specified user in the room. | `SetOnUserMessageSendResult()` | `SetOnUserMessageReceived()` <br>  |
| `SendRoomMessage()` | Send a text message to all users in the room. | `SetOnRoomMessageSendResult()` | `SetOnRoomMessageReceived()` |
| `SendUserBinaryMessage()` | Send a binary message to a specified user in the room. | `SetOnUserMessageSendResult()` | `SetOnUserBinaryMessageReceived()` |
| `SendRoomBinaryMessage()` | Send a binary message to all users in the room. | `SetOnRoomMessageSendResult()` | `SetOnRoomBinaryMessageReceived()` |
### Stream sync info
The stream sync info will be uploaded to the server with the audio data. All users subscribing to the corresponding audio stream will receive the stream sync info. The size of stream sync info should be limited to 255 bytes, otherwise audio data transmission will be affected.
### Audio report
Audio report is an optional feature. After initializing the RTC service, developers can call the audio report API to regularly receive local and remote audio statistics. The audio statistics include user and volume data, which the developer can use to figure out the current speaker.
| **API** | **Description** | **Remarks** |
| --- | --- | --- |
| `EnableAudioPropertiesReport` | Enable the audio properties report. | You can set the interval (in milliseconds) between one report and the next. |
| `SetOnLocalAudioPropertiesReport` | Set the callback for local audio properties report. | - |
| `SetOnRemoteAudioPropertiesReport` | Set the callback for remote audio properties report. | The remote audio properties report returns a list. Each item in the list contains information including the user ID, the user's room, volume, etc. |
### User behavior notification
User behavior notifications allow each player to know the behavior of others, such as joining the room, starting/stopping audio recording, and local mute.
## Implementation workflow
### Complete basic setups
Refer to the "[Platform services overview](/en_platform-services-overview#712343ad)" article to complete all required setups, including adding an app ID, initializing platform services, etc.
### Enable RTC service
You need to enable RTC service for your app on the PICO Developer Platform. Below are the steps to follow:

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/organization/).
2. From the left navigation pane, select **My Apps**.
   This directs you to the **My Apps** screen.
3. Click on the target app.
   This directs you to the app's **Overview** screen.
4. From the left navigation pane, select **Platform Service** > **Real-Time Communication**.
   This directs you to the following screen:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/ffd84c10df2343e68f2ec35abb355398~tplv-em5hxbkur4-noop.image?width=2511&height=1096)
5. Click **Enable**.
   The following pop-up window appears:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c776909e71de47d7ba45efbc8d854ad7~tplv-em5hxbkur4-noop.image?width=903&height=340)
6. Click **Confirm**.
   The PICO Developer Platform will then enable RTC service for your app.

### Configure publishing settings
Follow the steps below to configure publishing settings before using RTC service:

1. From the top menu bar, select **Edit** > **Project Settings** .
   The **Project Settings** pop-up window appears.
2. Go to **Player** > **Android settings icon** > **Publishing Settings**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c1f4c6526e4b4e3c93c77ff31111baa6~tplv-em5hxbkur4-noop.image?width=1424&height=987)
3. Scroll down to the **Build** section, check **Custom Main Manifest** and **Custom Main Gradle** **Template**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f606ece8bb3c4d6c90ee8502119a9401~tplv-em5hxbkur4-noop.image?width=1424&height=995)
   The **AndroidManifest.xml** file will be generated under the **Assets/Plugins/Android** directory.
4. Edit the **AndroidManifest.xml** file. Refer to the following example to add necessary permission and configuration covering network, audio recording, storage, and bluetooth to the **AndroidManifest.xml** file.
   ```XML
   <?xml version="1.0" encoding="utf-8"?>
   
   <manifest
       xmlns:android="http://schemas.android.com/apk/res/android"
       package="com.unity3d.player"
       xmlns:tools="http://schemas.android.com/tools">
   
       <uses-feature
               android:name="android.hardware.vulkan.version"
               android:required="false" />
   
       <uses-permission android:name="android.permission.INTERNET" />
       <uses-permission android:name="android.permission.RECORD_AUDIO" />
       <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
       <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
       <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
       <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
       <uses-permission android:name="android.permission.BLUETOOTH" />
       <uses-permission android:name="android.permission.ACCESS\_WIFI\_STATE"  />
       <uses-permission android:name="android.permission.READ_PHONE_STATE" />
   
       <uses-feature
               android:glEsVersion="0x00020000"
               android:required="true" />
       <uses-feature
               android:name="android.hardware.touchscreen"
               android:required="false" />
       <uses-feature
               android:name="android.hardware.touchscreen.multitouch"
               android:required="false" />
       <uses-feature
               android:name="android.hardware.touchscreen.multitouch.distinct"
               android:required="false" />
   
       <application>
           <activity android:name="com.unity3d.player.UnityPlayerActivity"
                     android:theme="@style/UnityThemeSelector">
               <intent-filter>
                   <action android:name="android.intent.action.MAIN" />
                   <category android:name="android.intent.category.LAUNCHER" />
               </intent-filter>
               <meta-data android:name="unityplayer.UnityActivity" android:value="true" />
           </activity>
       </application>
   </manifest>
   ```

### Initialize RTC service
You need to initialize the RTC service. The initialization code should be added to the global initialization section. Below is the code sample:
```C#
void initRtc()
{
    var res = RtcService.InitRtcEngine();
    if (res != RtcEngineInitResult.Success)
    {
        Log($"Init RTC Engine Failed{res}");
        throw new UnityException($"Init RTC Engine Failed:{res}");
    }

    RtcService.EnableAudioPropertiesReport(2000);
}
private void Start()
{
    CoreService.AsyncInitialize().OnComplete(m =>
    {
        if (m.IsError)
        {
            Log($"Init PlatformSdk failed:code={m.Error.Code},message={m.Error.Message}");
            return;
        }
    
        if (m.Data == PlatformInitializeResult.Success || m.Data == PlatformInitializeResult.AlreadyInitialized)
        {
            Log($"Init PlatformSdk successfully");
            initRtc();
        }
        else
        {
            Log($"Init PlatformSdk failed:{m.Data}");
        }
    });
}

```

### Bind an event to a UI element
The developer can bind events to UI elements for executing relevant RTC operations. For example, the developer can bind the "join room" event to the **JoinRoom** button, thereby acquiring a token and joining a user in a room when the user clicks the **JoinRoom** button.
```C#
buttonEnterRoom.onClick.AddListener(OnClickJoinRoom);
```

Meanwhile, the developer can set up a relevant event handler to respond to the token acquisition and room joining operation. Below is the code sample:
```C#
private void OnClickJoinRoom()
{
    if (!(CheckRoomId() && CheckUserId()))
    {
        return;
    }

    var roomProfile = (RtcRoomProfileType) dropdownRoomProfile.value;
    var roomId = _inputFieldRoomId.text;
    var userId = _inputFieldUserId.text;
    Log($"userId={userId} roomId={roomId} scenarioType={roomProfile}");
    var privilege = new Dictionary<RtcPrivilege, int>();
    privilege.Add(RtcPrivilege.PublishStream, 3600 * 2);
    privilege.Add(RtcPrivilege.SubscribeStream, 3600 * 2);
    RtcService.GetToken(roomId, userId, 3600 * 2, privilege).OnComplete(msg =>
    {
        if (msg.IsError)
        {
            Log($"Get rtc token failed: code={msg.GetError().Code} message={msg.GetError().Message}");
            return;
        }

        var token = msg.Data;
        Log($"Got RTC Token:{token}");
        int result = RtcService.JoinRoom(roomId, userId, token, roomProfile, true);
        Log($"Join Room Result={result} RoomId={_inputFieldRoomId.text}");
    });
}
```

### Set callback
Developers can use the following callback functions to monitor the result of API call.
| **Callback Function** | **Description** |
| --- | --- |
| `RtcService.SetOnJoinRoomResultCallback` | Set the callback function for `JoinRoom`. After `JoinRoom` is called, the developer may get `RtcJoinRoomResult` later. |
| `RtcService.SetOnLeaveRoomResultCallback` | Set the callback function for `LeaveRoom`. After `LeaveRoom` is called, the developer may get `RtcLeaveRoomResult` later. |
| `RtcService.SetOnUserJoinRoomResultCallback` | The developer will be informed when other people join the room. |
| `RtcService.SetOnUserLeaveRoomResultCallback` | The developer will be informed when other people leave the room. |
Developers can refer to the following code sample to implement a callback function.
```C#
private void OnConnectionStateChange(Message<RtcConnectionState> message)
{
    Log($"ConnectionState {message.Data}");
}

private void OnRoomError(Message<RtcRoomError> message)
{
    var e = message.Data;
    Log($"RtcRoomError:RoomId={e.RoomId} Code={e.Code}");
}
```

## Demo
You can use the RtcDemo to debug RTC service. For more information, refer to the "[RTC demo](/en_rtc-demo)" article.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/70d6d0374b7e48a5b8ea2b3787f8eacd~tplv-em5hxbkur4-noop.image?width=1280&height=639" width="700px" />

## API reference
You can use RTC related APIs for relevant management and settings. Refer to the [API reference](/reference/unity/client-api/RtcService/) for more details.


# --- END: RTC.md ---



# --- BEGIN: Scene Capture.md ---

If the mixed reality experience you are building requires information about the structure of the user's real-world environment, and your app needs to obtain the geometric structure and semantic information of the real environment to provide a richer interactive experience, then it is recommended using the Scene Capture feature within your app to capture the user's real-world environment.
## Feature refactoring info
Starting from version 3.0.0, PICO refactorred the Scene Capture feature. Refer to the "[Compatibility & porting guide for MR features](/en_compatibility-and-porting-guide-for-mr-features)" article for details.
## About the Room Capture app
Room Capture is a system-level app provided by PICO. Through this app, users can capture the walls, doors, windows, tables, chairs, sofas, and other objects in their real-world environment. This allows for interaction between the captured real-world objects and virtual objects in the mixed reality scene. PICO developers can use the SDK to access the space and scene anchor data created by the "Room Capture" app, and apply it in their own apps.
After launching the Room Capture app, it will guide the user to complete a preliminary scan of the real-world scene and construct the geometric structure of that scene. It will identify the ceiling, floor, walls, doors, windows, and open areas in that scene. The Room Capture app will also identify room features and furniture, such as tables, chairs, and sofas. This information will help your app build a universal mixed reality experience, ensuring that users can experience your app with the current surroundings integrated, regardless of the actual structure of their real-world environment.
The Room Capture app automatically captures a user's current surroundings. The user only needs to walk and look around in the real-world scene, then the app automatically captures objects (as shown in the video below), associates them with scene anchors, and matches them with semantic labels and component types.

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4b51d3b080f4a27b37bbd4ef21d03f6~tplv-goo7wpa0wc-image.image></video>

## About scene anchors
The scene anchors are system-level anchors created by the Room Capture app. Scene anchors are used to record information about the user's surrounding environment, such as the position and size of objects like sofas, floors, and walls. When the Room Capture app scans these objects, it automatically adds scene anchors for them. The scene anchors belong to the PICO system, so they cannot be modified by your apps. However, with the user's permission, your apps can discover and use the scene anchors.
**Note**
Your apps cannot capture spaces, but can add spatial anchors to the spaces created by the Room Capture app.

Scene anchor data permissions are described below:

* **Permission to edit data**: Only the Room Capture app can edit scene anchor data.
* **Permission to access data**: The Room Capture app and all your apps can access the scene anchor data. 

## Component types & semantic labels
Scene anchors carry component type (`PxrSceneComponentType`) and semantic label (`PxrSemanticLabel`) information, which are used to describe the real-world objects that the anchors represent. You can use the component type and semantic label information to access specific scene anchors.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3fad84d0a044718b88b14eb33b46394~tplv-goo7wpa0wc-image.image" width="1280px" />

Below are the available component types:
| **Component Type** | **Description** |
| --- | --- |
| Location | The location of a scene anchor. All scene anchors have this component type. |
| Semantic | The semantic label of a scene anchor. All scene anchors have this component type. |
| Box2D | Planar objects with a rectangular shape will be given this component type. |
| Polygon | Planar objects with a non-rectangular shape will be given this component type. |
| Box3D | Non-plane objects will be given this component type. |
Below are the available semantic labels and the corresponding component type for each semantic label:
| **Semantic Label** | **Description** | **Component Type** |
| --- | --- | --- |
| UnKnown | Objects that are not associated with any semantic label below. | / |
| Floor | A floor. | Polygon |
| Ceiling | A ceiling. | Polygon |
| Wall | A real-world wall. Doors and windows must exist within wall faces. | Box2D |
| Door | A door, which must exist within a wall face. | Box2D |
| Window | A window, which must exist within a wall face. | Box2D |
| Opening | An open area. | Box2D |
| Table | A table. | Box3D |
| Sofa | A sofa. | Box3D |
| Chair | A chair. | Box3D |
| Curtain | A curtain. | Box3D |
| Cabinet | A cabinet. | Box3D |
| Bed | A bed. | Box3D |
| Plant | A plant. | Box3D |
| Screen | A screen. | Box3D |
| VirtualWall | Virtual walls are automatically generated when scene capture stops. They have nothing to do with the real-world walls. Doors and windows cannot exist within virtual walls. <br> The virtual walls will form an enclosed space, containing both the real-world and virtual objects within it. In your app, you can add codes for detecting when the user enters or exits this enclosed space, and provide appropriate safety prompts or notifications. | Box2D |
| Refrigerator | A refrigerator. | Box3D |
| WashingMachine | A washing machine. | Box3D |
| AirConditioner | An air conditioner | Box3D |
| Lamp | A lamp. | Box3D |
| WallArt | A wall art, which must exist within a wall face. | Box2D |
## Development environment

* PICO device models: PICO 4 series, PICO 4 Ultra series
* PICO device's system version: 5.14.0 or later

## Prerequisites

* Have added the XR Origin object and added the PXR_Manager (Script) component to it.
* Have set the position and rotation of XR Origin and Camera Offset objects to (0,0,0) on the **Tranform** component.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1c45f9f418c4a87be39f594cda72fe5~tplv-goo7wpa0wc-image.image)
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d17ba1e3870f4fdb8fc6c0f9a8b0a3ae~tplv-goo7wpa0wc-image.image)
* Have set up the Video Seethrough feature for your app. Refer to the "[Video Seethrough](/en_seethrough)" article for detailed instructions.

## Integrate the Scene Capture feature using APIs
### Step 1: Enable the Scene Capture capability for your app
Check the **Scene Capture** checkbox on the **PXR_Manager (Script)** panel to enable the Scene Capture capability for your app. Then, use Scene Capture APIs to implement this feature in your app.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22ee0181d0594c308dbf3fbb387c2a50~tplv-goo7wpa0wc-image.image" width="450px" />

### Step 2: Start scene capture in your app
Before calling other Scene Capture APIs to perform operations, call `StartSenseDataProvider` to start the Scene Capture feature in your app.
```C#
async Task<PxrResult> StartSenseDataProvider(PxrSenseDataProviderType type)
```

### Step 3: Query scene anchor data
You can implement custom experiences in your app through using scene anchor data. Before accessing the data, call `QuerySceneAnchorAsync` to check if scene anchor data currently exists.

* If the request returns scene anchor data, you can proceed to access the data without calling `QuerySceneAnchorAsync` again, see Step 4 for details.
* If the request does not return any scene anchor data or if the data does not meet your needs, call `StartSceneCaptureAsync` to launch the Room Capture app and let the user capture their current physical scene first. If `PxrResult` is `SUCCESS`, it indicates that the user has captured the scene, and you can proceed to access the scene anchor data.

```C#
async Task<PxrResult> StartSceneCaptureAsync()
```

### Step 4: Access scene anchor data
The Room Capture app turns what it scans into parameter data, which enables your app to easily modify the structure and layout of the scanned rooms. You can create diverse experiences in your app using scene anchor data, such as:

* Estimating the size, distance, and furniture dimensions of specific areas within the space;
* Implementing mixed reality effects for space decor design;
* Enhancing interaction between the virtual scene and physical environment.

**Note**
To improve the success rate of data retrieval, it is recommended to guide the user back to the space previously created, or to create a new space.

Use the following APIs to retrieve scene anchor data:
| **API** | **Description** |
| --- | --- |
| QuerySceneAnchorAsync | Loads scene anchors with specified semantic label(s). |
| GetSceneAnchorComponentTypes | Gets the component type of a scene anchor. |
| GetSceneSemanticLabel | Gets the semantic label for a scene anchor. |
| GetAnchorUuid | Gets the UUID of a scene anchor. <br> ***Note***: This is an optional API. If you want to store the loaded scene anchor data so that it can be used directly the next time the app is opened without needing to reload the data, you can use UUIDs to save the data of corresponding scene anchors. |
| GetSceneBox3DData | Gets information about a 3D box object associated with a scene anchor, including its position and rotation relative to the center of the anchor as well as its length, width, and height. |
| GetSceneBox2DData | Gets information about a 2D box object associated with a scene anchor, including its offset relative to the center of the anchor as well as its length and width. |
| GetScenePolygonData | Gets the vertice array of a polygon object associated with a scene anchor. |
| LocateAnchor | Locates a scene anchor by getting its real-time position and rotation. |
Below is the procedure for implementation:

1. Call `QuerySceneAnchorAsync` to retrieve scene anchors with the specified semantic labels. You can pass multiple semantic labels in a single request. If you do not pass any semantic labels, all types of scene anchors will be returned. The request will return a list of anchor handles, but it will not match the corresponding semantic label for each anchor on the list. 
   **Note**
   If the scene anchor data retrieved in the above-mentioned step 3 is available, you do not need to call `QuerySceneAnchorAsync` again here.

   ```C#
   async Task<(PxrResult result, List<ulong> anchorHandleList)> QuerySceneAnchorAsync(PxrSemanticLabel[] labels)
   ```

2. Call `GetSceneSemanticLabel` to get the semantic label for a specified scene anchor. The anchor handle to be passed in this request can be retrieved from the anchor handle list returned by `QuerySceneAnchorAsync`.
   ```C#
   PxrResult GetSceneSemanticLabel(ulong anchorHandle,out PxrSemanticLabel label)
   ```

3. Call `LocateAnchor` to retrieve the pose data of scene anchors. For scene anchors, the pose data returned by `LocateAnchor` will only be updated after you call `QuerySceneAnchorAsync`. If you do not call `QuerySceneAnchorAsync` again, the data returned by `LocateAnchor` will remain the same.
4. According to the returned semantic labels, call corresponding APIs given below to retrieve the information about the objects associated with scene anchors.
   ```C#
   // Gets the information about a 3D box object
   PxrResult GetSceneBox3DData(ulong anchorHandle, out Vector3 position, out Quaternion rotation, out Vector3 extent)
   
   // Gets the information about a 2D box object
   PxrResult GetSceneBox2DData(ulong anchorHandle, out Vector2 offset, out Vector2 extent)
   
   // Gets the information about a polygon object
   PxrResult GetScenePolygonData(ulong anchorHandle, out Vector2[] vertices)
   ```

5. Listen for the `PXR_Manager.SceneAnchorDataUpdated` event. Receiving this event indicates that new scene anchor data has been discovered, and then you need to repeat the above steps to access the new data.
   When the number of anchors decreases, the system will not push this event. For example, as the user walks around, the system continues to discover new anchors; however, old anchors that were previously discovered will not be automatically deleted as the user moves away.

### Step 5: Stop scene capture
When everything is done, call `StopSenseDataProvider` to stop scene capture.
```C#
PxrResult StopSenseDataProvider(PxrSenseDataProviderType type)
```

### Code sample
```C#
// Click the button to load scene anchor data
private async void OnBtnPressedLoadSceneData()
{
    var result = await PXR_MixedReality.QuerySceneAnchorAsync(null);
    if (result.result == PxrResult.SUCCESS)
    {
        if (result.anchorHandleList.Count > 0)
        {
            foreach (var item in result.anchorHandleList)
            {
                var result1 = PXR_MixedReality.GetSceneSemanticLabel(item, out var label);
                if (result1 == PxrResult.SUCCESS)
                {
                    DrawSceneModel(item, label);
                }
            }
        }
    }
}

// Draw corresponding objects
private void DrawSceneModel(ulong anchorHandle,PxrSemanticLabel label)
{
    /*
     * UnKnown0,
       Floor-------Polygon
       Ceiling,----Polygon
       Wall,-------Box2D
       Door,-------Box2D
       Window,-----Box2D
       Opening,----Box2D
       Table,------Box3D
       Sofa,-------Box3D
       Chair,------Box3D
     */
    
    switch (label)
    {
        case PxrSemanticLabel.UnKnown:
            break;
        case PxrSemanticLabel.Floor:
        case PxrSemanticLabel.Ceiling:
            {
                var result = PXR_MixedReality.GetScenePolygonData(anchorHandle, out var vertices);
                if (result == PxrResult.SUCCESS)
                {
                    var verVector3S = Array.ConvertAll(vertices, v2 => new Vector3(v2.x, v2.y, 0f));

                    var sceneAnchor = new GameObject(anchorHandle.ToString());
                    var polygon = new GameObject();
                    var lineRenderer = polygon.AddComponent<LineRenderer>();
                    lineRenderer.startColor = Color.red;
                    lineRenderer.endColor = Color.red;
                    lineRenderer.startWidth = 0.1f;
                    lineRenderer.positionCount = verVector3S.Length;
                    lineRenderer.loop = true;
                    lineRenderer.useWorldSpace = false;
                    lineRenderer.endWidth = 0.1f;
                    lineRenderer.material = new Material(Shader.Find("Sprites/Default"));
                    lineRenderer.SetPositions(verVector3S);
                    polygon.transform.SetParent(sceneAnchor.transform);
                    PXR_MixedReality.LocateAnchor(anchorHandle, out var anchorPosition, out var anchorRotation);
                    sceneAnchor.transform.rotation = anchorRotation;
                    sceneAnchor.transform.position = anchorPosition;
                }
                else
                {
                    // log
                }
            }
            break;
        case PxrSemanticLabel.Wall:
        case PxrSemanticLabel.Door:
        case PxrSemanticLabel.Window:
        case PxrSemanticLabel.Opening:
        case PxrSemanticLabel.VirtualWall:
            {
                var result = PXR_MixedReality.GetSceneBox2DData(anchorHandle, out var offset,out var extent);
                if (result == PxrResult.SUCCESS)
                {
                    //currently,offset not support
                    var sceneAnchor = new GameObject(anchorHandle.ToString());
                    var box2D = GameObject.CreatePrimitive(PrimitiveType.Cube);
                    box2D.transform.localScale = new Vector3(extent.x,0, extent.y);
                    box2D.transform.localEulerAngles = new Vector3(90f, 0, 0);
                    PXR_MixedReality.LocateAnchor(anchorHandle, out var anchorPosition, out var anchorRotation);
                    box2D.transform.SetParent(sceneAnchor.transform);
                    sceneAnchor.transform.rotation = anchorRotation;
                    sceneAnchor.transform.position = anchorPosition;
                }
                else
                {
                    // log
                }
            }
            break;
        case PxrSemanticLabel.Table:
        case PxrSemanticLabel.Sofa:
        case PxrSemanticLabel.Chair:
            {
                var result = PXR_MixedReality.GetSceneBox3DData(anchorHandle, out var position,out var rotation,out var extent);
                if (result == PxrResult.SUCCESS)
                {
                    var sceneAnchor = new GameObject(anchorHandle.ToString());
                    var box3D = GameObject.CreatePrimitive(PrimitiveType.Cube);
                    //currently,rotation not support
                    box3D.transform.localPosition = position;
                    box3D.transform.localScale = extent;
                    PXR_MixedReality.LocateAnchor(anchorHandle, out var anchorPosition, out var anchorRotation);
                    box3D.transform.SetParent(sceneAnchor.transform);
                    sceneAnchor.transform.rotation = anchorRotation;
                    sceneAnchor.transform.position = anchorPosition;
                }
                else
                {
                    // log
                }
            }
            break;
    }
}
```

## Integrate the Scene Capture feature using the PXR_Scene Capture Manager (Script) component
The **PXR_Scene Capture Manager (Script)** component integrates the functionalities of enabling scene data providers, retrieving data, and rendering models. You can directly add this component to a GameObject, then add the Box2D and Box3D prefabs you want to display in the scene. The component will automatically complete the entire process and directly display the prefabs you add in the scene.
### Step 1: Enable the Scene Capture capability for your app
Check the **Scene Capture** checkbox on the **PXR_Manager (Script)** panel to enable the Scene Capture capability for your app. Then, use Scene Capture APIs to implement this feature in your app.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49f7792e0b0640ed9e6af9ada364d9a9~tplv-goo7wpa0wc-image.image" width="450px" />

### Step 2: Complete setup in the PXR_Scene Capture Manager (Script) component

1. Select a GameObject.
2. In the **Inspector** window, add the **PXR_Scene Capture Manager (Script)** component to the GameObject.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae8388b50c72472ca3aa43149204bccb~tplv-goo7wpa0wc-image.image)
3. In **Box 2D Prefab** and **Box 3D Predab**, add the Box 2D and Box 3D prefabs that need to be displayed in the scene. You can add both prefabs or just one of them.

## Preview scene capture data
After completing scene capture using the "Room Capture" app on your PICO device, the app generates a SceneAnchorData.json file to save the scene capture data and stores the file in the /sdcard directory of the PICO device. You can preview the scene capture data in the Unity Editor using the PXR_Scene Capture Manager (Script) component.
### Requirements

* PICO device model: PICO 4 Ultra series
* PICO device's system version: 5.13.0 or later

### Procedure

1. Use the `adb pull /sdcard/SceneAnchorData.json` command to export the SceneAnchorData.json file from the PICO device to your PC.
2. (Optional) Adjust the data in the SceneAnchorData.json file as needed.
3. Open your project in the Unity Editor.
4. Select a GameObject, then in the **Inspector** window, add the **PXR_Scene Capture Manager (Script)** component to that GameObject.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae8388b50c72472ca3aa43149204bccb~tplv-goo7wpa0wc-image.image)
5. In the **Scene Capture Data** section, add the SceneAnchorData.json file.
   The Unity Editor will read the data from the file and display the virtualized room.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c5eb1ac57a54bce9222911491983d1e~tplv-goo7wpa0wc-image.image)

## API reference
For more details on Scene Capture APIs, such as parameter descriptions and returns, refer to the [API reference](/reference/unity/client-api/PXR_MixedReality/).


# --- END: Scene Capture.md ---



# --- BEGIN: Screen Fade.md ---

Screen fade is a pretty basic and standard effect in app design. It usually takes place in loading scenes, scene transitions, cutscenes, and many other situations.
You can use the PXR_Manager and PXR_Screen Fade scripts that PICO Unity Integration SDK offers to design the screen fade effect for your app.
## Example
In the following example, the screen-fade parameters applied are:

* **Fade Time**: 5s
* **Fade Color**: black
* **Render Queue**: 5000

<video src=https://sf1-cdn-tos.huoshanstatic.com/obj/vcloud/e372d09fb7588ad992893138a0ee2fd1-.mp4></video>
## Set up screen fade effect
Below are the steps to setting up the screen fade effect illustrated in the above example:

1. Open your project in the Unity Editor.
2. In the **Hierarchy** window, select **+** > **XR** > **XR Origin (VR)**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f7f1ec4178674bb3a61bdf0047052f9a~tplv-em5hxbkur4-noop.image?width=588&height=401)
3. Delete the **Main Camera** that originally exists in the scene by default.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/736fe420f2914874bda5e4af9fe366c2~tplv-em5hxbkur4-noop.image?width=588&height=401)
4. Select **XR Origin**.
   The scripts and components for configuring the XR Origin object are then displayed in the Inspector window.
5. Click **Add Component** at the bottom of the **Inspector** window.
6. Search for the **PXR_Manager** script and double-click to add it.
   The script's UI appears as below:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/02d34c65c27b4b039a66fd508268612a~tplv-em5hxbkur4-noop.image?width=565&height=295)
7. Check **Open Screen Fade** .
   This directs you to the Inspector window for Main Camera. The **PXR_Screen Fade** script has been automatically mounted to Main Camera. The script's UI appears as below:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/be9154e118b7444290ccf90812b64a1e~tplv-em5hxbkur4-noop.image?width=788&height=177)
8. Configure the following parameters as needed:
   | **Parameter** | **Description** |
   | --- | --- |
   | Gradient Time | The duration of screen fade effect, which is set to **5** (in seconds) by default. |
   | Fade Color | The color the screen fades in/out from, which is set to black by default. |


# --- END: Screen Fade.md ---



# --- BEGIN: SecureMR Privacy Notice.md ---

Welcome to the PICO SecureMR experience. Your privacy is very important to us. This notice explains how your personal data is processed in connection with SecureMR during your use of the SecureMR supported application(s) ("**Application**"). 
SecureMR is a secured service of the PICO Operating System ("**PICO OS**") to ensure that Applications do not access your camera related data when providing you with mixed reality ("**MR**") experience. Typically, applications need to acquire and process the headset's camera related data, with your permission, to deliver you MR service. However, SecureMR prevents any such transfer of camera related data to Applications, without disabling any MR features, by requiring Applications to separate and deploy their MR feature modules in the segregated SecureMR service within PICO OS. SecureMR ensures that such MR modules may only locally process camera related data within the SecureMR service, and that the processing output is directly delivered to your screen, and that **no camera data or MR outputs will be shared with Applications**. In addition, all data within SecureMR is only locally processed within the PICO OS in accordance with the terms of our [PICO Privacy Policy](https://www.picoxr.com/global/legal/privacy-policy), and will be deleted once the MR output is delivered.
Please note that SecureMR only prevents Applications from accessing any camera related data and MR outputs and does not intervene with any functioning of the MR modules. Only the Applications have control on how their MR modules process camera data in SecureMR and deliver MR experience.
In the event that an Application needs to acquire your camera data for features not adopting SecureMR, it shall apply for your permission to camera data (only available for certain PICO models). Whenever an Application is accessing your camera data, PICO OS will display a camera status indicator on your screen.
Please refer to the [PICO Privacy Policy](https://www.picoxr.com/global/legal/privacy-policy) for more information on how your camera data is generated and processed.


# --- END: SecureMR Privacy Notice.md ---



# --- BEGIN: SecureMR samples.md ---

PICO provides samples that demonstrate how to use SecureMR to build privacy-preserving XR apps. These samples highlight how to integrate machine learning inference, securely access MR data, and render results within Unity.
## **Git repository**
[SecureMR_Unity_Samples](https://github.com/Pico-Developer/SecureMR-Unity-Sample)
## **Requirements**

* Unity version: Unity 6
* PICO Unity Integration SDK: 3.2.0
* PICO device models: PICO 4 Ultra series
* PICO device's system version: 5.13.0 or later

## Samples
### Minst
A minimal sample demonstrating the SecureMR pipeline for image-based model inference, including:

* Running a lightweight digit classification model (MNIST-style).
* Captures VST input and doing preprocess (forexample, resizing and cropping).
* Demonstrating the integration of model pipeline with SecureMR service.
         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f736cd3146e44bc80af2b57de9ab84d~tplv-goo7wpa0wc-image.image></video>

### ColorPicker
An interactive sample showing how to process color information from the environment, including

* Capturing a VST image and doing preprocessing.
* Extracting pixel information through a SecureMR operator.
* Demonstrating real-time data flow from camera to data processing pipeline and Unity rendering.
         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/278cdbb1240d4ee8b0a0aa34b8c9e08e~tplv-goo7wpa0wc-image.image></video>


# --- END: SecureMR samples.md ---



# --- BEGIN: SecureMR use cases.md ---

You can use SecureMR to display more diverse content in the scene. This article provides use cases for your reference.
## Prerequisites
You have enabled the SecureMR capabilities and configured the Video Seethrough (VST) functionality for the app. For more information, refer to [Quickstart](/en_securemr-quickstart).
## Display gITF models
By creating `SwitchGltfRenderStatusOperator`, you can display gITF models in the scene.
### Demo video
Display a gITF model in the VST scene.

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e1051bed57841529c23922e2fd869de~tplv-goo7wpa0wc-image.image></video>

### **Operator rules**
You need to follow the rules below to set the operator:
| **Operand** | **Required** | **Description** |
| --- | --- | --- |
| gltf | Yes | Tensor of the target glTF model. It must be of the glTF type. |
| world pose | No | If not empty, the specified glTF model starts rendering. This operand should provide the initial world coordinates of the glTF model in the OpenXR Local coordinate system. If empty, the glTF model rendering stops. |
| visible | No | Used to determine whether the glTF model is visible. If the tensor is non-zero, the model is visible and starts rendering; otherwise, the model stops rendering. Visible by default. |
| view locked | No | Used to determine whether the glTF model follows View Space. If the Tensor is non-zero, the model uses OpenXR's View space as the reference frame; otherwise, it uses OpenXR's Local Space as the reference frame. |
### Code sample
The complete code sample is as follows:
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.XR.PXR;
using Unity.XR.PXR.SecureMR;
public class ShowGltfModel : MonoBehaviour
{
    private Provider provider;
    private Pipeline pipeline;
    int image_width = 3248;   // Same as VST_IMAGE_WIDTH
    int image_height = 2464;  // Same as VST_IMAGE_HEIGHT
    private Tensor debugGltfPlaceholder;
    public TextAsset tvGltf;
    private Tensor debugGltfTensor;
    
    // Start is called before the first frame update
    void Start()
    {
        PXR_Manager.EnableVideoSeeThrough = true;
        
        provider = new Provider(image_width, image_height);

        CreateRender();
    }
    
    void CreateRender()
    {
        pipeline = provider.CreatePipeline();
        
        var renderGltfOp = pipeline.CreateOperator<SwitchGltfRenderStatusOperator>();
        var poseMat  = pipeline.CreateTensor<float,Matrix>(1, new TensorShape(4,4));
        
        debugGltfPlaceholder = pipeline.CreateTensorReference<Gltf>();
        var gltfData = tvGltf.bytes;
        debugGltfTensor  = provider.CreateTensor<Gltf>(gltfData);

        renderGltfOp.SetOperand("gltf",debugGltfPlaceholder);
        renderGltfOp.SetOperand("world pose",poseMat);
        float[] poseMatValue = 
        {0.5f, 0.0f, 0.0f, -0.5f,
            0.0f, 0.5f, 0.0f, 0.0f,
            0.0f, 0.0f, 0.5f, -1.5f,
            0.0f, 0.0f, 0.0f, 1.0f};
        poseMat.Reset(poseMatValue);
        
        InvokeRepeating(nameof(RenderFrame), 0, 0.02f);
    }
    
    void RenderFrame()
    {
        var pipelineIOPair = pipeline.CreateTensorMapping();
        pipelineIOPair.Set(debugGltfPlaceholder,debugGltfTensor);
        pipeline.Execute(pipelineIOPair);
    }
}
```

## Display the gITF model and text
Create a gITF model in the scene through `RenderTextOperator`, and display text on the gITF model.
### Demo video
A black monitor model is displayed in the VST scene with the text "Hello World" shown on it.

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23c0eb2dbe2d4ad19f87be2fcdfd73bd~tplv-goo7wpa0wc-image.image></video>

### **Operator rules**
You need to follow the rules below to set the operator:
| **Operand** | **Required** | **Description** |
| --- | --- | --- |
| text | Yes | Any Tensor. If it is a 1-channel UINT8 or INT8 Scalar Tensor, the contents of the tensor is treated as a UTF-8 encoded string. If it is another type of tensor, the raw value of the tensor is printed directly. For example, if you input a Scalar Tensor of type UINT8 with a value of `{110, 105, 114, 114, 117}`, it will ultimately render as the string "HELLO"; if you input a Mat Tensor with identical content, the rendered result will be "110 105 114 114 117". |
| start | Yes | The starting X and Y coordinates. In accordance with Android Canvas requirements, they are at the baseline of the lower-left corner of the first character. Must be a float32/64 point2 with a shape of `{1,}`. X and Y should be relative values within the range of 0 to 1 corresponding to the width and height of the Canvas. |
| colors | Yes | Text color and background color. It must be a 4-channel UINT8 Color Tensor with a shape of `{2,}`, where the first is the text color and the second is the background color. |
| gltf | Yes | Target glTF material. It must be a glTF Tensor. |
| texture ID | Yes | The ID of the target Texture for rendering text. It must be a 1-channel UINT16 Scalar Tensor with a shape of {1, }. It must be the ID of a Texture already existing in glTF (including those newly added via 3.30 LOAD TEXTURE). |
| font size | Yes | Font size, measured in pt. It must be a 1-channel float32/64 type Scalar Tensor, with a shape of `{1, }`. |
When creating Operator, you need to set the font type, country code, Canvas length and width.

### **Code sample**
The complete code sample is as follows:
```C#
using System.Collections;
using System.Collections.Generic;
using System.Text;
using UnityEngine;
using Unity.XR.PXR;
using Unity.XR.PXR.SecureMR;
using Color = Unity.XR.PXR.SecureMR.Color;

public class ShowText : MonoBehaviour
{
    private Provider provider;
    private Pipeline pipeline;
    int image_width = 3248;   // Same as VST_IMAGE_WIDTH
    int image_height = 2464;  // Same as VST_IMAGE_HEIGHT
    private Tensor debugGltfPlaceholder;
    public TextAsset tvGltf;
    private Tensor debugGltfTensor;
    
    // Start is called before the first frame update
    void Start()
    {
        PXR_Manager.EnableVideoSeeThrough = true;
        
        provider = new Provider(image_width, image_height);

        CreateRender();
    }
    
    void CreateRender()
    {
        pipeline = provider.CreatePipeline();
        
        RenderTextOperatorConfiguration renderTextConfiguration = new RenderTextOperatorConfiguration(SecureMRFontTypeface.SansSerif, "en-US", 1440, 960);
        var renderTextOp = pipeline.CreateOperator<RenderTextOperator>(renderTextConfiguration);
        var renderGltfOp = pipeline.CreateOperator<SwitchGltfRenderStatusOperator>();
        
        var text = pipeline.CreateTensor<sbyte,Scalar>(1, new TensorShape(30));
        var startPosition = pipeline.CreateTensor<float,Point>(2, new TensorShape(1));
        var colors = pipeline.CreateTensor<byte,Color>(4, new TensorShape(2));
        var textureId = pipeline.CreateTensor<ushort,Scalar>(1, new TensorShape(1));
        var fontSize = pipeline.CreateTensor<float,Scalar>(1, new TensorShape(1));
        var poseMat  = pipeline.CreateTensor<float,Matrix>(1, new TensorShape(4,4));
        
        debugGltfPlaceholder = pipeline.CreateTensorReference<Gltf>();
        var gltfData = tvGltf.bytes;
        debugGltfTensor  = provider.CreateTensor<Gltf>(gltfData);

        renderTextOp.SetOperand("text",text);
        renderTextOp.SetOperand("start",startPosition);
        renderTextOp.SetOperand("colors",colors);
        renderTextOp.SetOperand("texture ID",textureId);
        renderTextOp.SetOperand("font size",fontSize);
        renderTextOp.SetOperand("gltf",debugGltfPlaceholder);
        renderGltfOp.SetOperand("gltf",debugGltfPlaceholder);
        renderGltfOp.SetOperand("world pose",poseMat);
        
        float[] poseMatValue = 
        {0.5f, 0.0f, 0.0f, -0.5f,
            0.0f, 0.5f, 0.0f, 0.0f,
            0.0f, 0.0f, 0.5f, -1.5f,
            0.0f, 0.0f, 0.0f, 1.0f};
        poseMat.Reset(poseMatValue);
        
        string textValue = "Hello World";
        text.Reset(Encoding.UTF8.GetBytes(textValue));

        float[] startValue = {0.1f, 0.3f};
        startPosition.Reset(startValue);

        byte[] colorsValue = {255, 255, 255, 255, 0, 0, 0, 255};
        colors.Reset(colorsValue);

        int[] textureId_value = {0};
        textureId.Reset(textureId_value);

        float[] fontSize_value = {144.0f};
        fontSize.Reset(fontSize_value);
        
        InvokeRepeating(nameof(RenderFrame), 0, 0.02f);
    }
    
    void RenderFrame()
    {
        var pipelineIOPair = pipeline.CreateTensorMapping();
        pipelineIOPair.Set(debugGltfPlaceholder,debugGltfTensor);
        pipeline.Execute(pipelineIOPair);
    }
}
```

## Use the gITF model to display the VST image
Obtain the VST image using  `RectifiedVstAccessOperator`; perform image affine transformation using `GetAffineOperator` and `ApplyAffineOperator`; render the obtained VST image onto the gITF model using `LoadTextureOperator`, `UpdateGltfOperator`, and `SwitchGltfRenderStatusOperator`.
### Demo video
The monitor model is replaced with the VST image.

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34141587670e40c8ac11fb00e27ec55b~tplv-goo7wpa0wc-image.image></video>

### **Operator rules**
You need to follow the rules below to set the operator:

* **`RectifiedVstAccessOperator`**
   This operator does not require any operand and has the following four optional results:
   | **Result** | **Description** |
   | --- | --- |
   | right image | The VST RGB image of the right eye. It is required to be of the Mat type, with a data type of 3-channel UINT8. The shape must be `(W, H)`, where `W` and `H` must match the width and height of the VST image set when creating the Framework Handle. |
   | left image | The VST RGB image of the left eye. It is required to be of the Mat type, with a data type of 3-channel UINT8. The shape must be `(W, H)`, where `W` and `H` must match the width and height of the VST image set when creating the Framework Handle. |
   | timestamp | Camera timestamp. It is required to be of the TimeStamp type. |
   | camera matrix | The camera's intrinsic matrix. It can be used for SolvePNP. It must be of the Mat type, with a data type of 1-channel float32/64 and a shape of `(3, )`. |
* **`GetAffineOperator`**
   There are the following two operands, both of which must be set.
   | **Operand** | **Description** |
   | --- | --- |
   | src | The coordinates of three points in the source space of the affine transformation. It is required to be of the Point type, with a data type of 2-channel float32/64 and a shape of `(3,)`. |
   | dst | The coordinates of three points in the target space of the affine transformation, which should correspond one-to-one with the three points in `src`. They are required to be of the Point type, with a data type of 2-channel float32/64 and a shape of `(3,)`. |
   There is one optional result named `result`. It is used to store the affine matrix. It is required to be of the Mat type, with a data type of 1-channel float32/64 and a shape of `(2, 3)`.
* **`ApplyAffineOperator`**
   There are the following two operands, both of which must be set.
   | **Operand** | **Description** |
   | --- | --- |
   | affine | Affine matrix. It is required to be of the Mat type, with a data type of 1-channel float32/64 and a shape of `(2, 3)`. |
   | src image | Source image. It is required to be of the Mat type, with no specific requirements for the data type. The shape must have exactly two dimensions. |
   There is one optional result named `dst image`. It is the result of the affine transformation. It is required to be of the Mat type, with a data type compatible with `src image`.
* **`LoadTextureOperator`**
   There are the following two operands, both of which must be set.
   | **Operand** | **Description** |
   | --- | --- |
   | gltf | The target glTF model Tensor. It must be of the glTF type. |
   | rgb image | The source image of the newly added texture for the glTF model. It is required to be of the Mat type, with a data type of 3/4-channel UINT8 (corresponding to RGB and RGBA, respectively). The shape must be `{N, HEIGHT, WIDTH}` or `{HEIGHT, WIDTH}` (only when N==1). |
   There is one mandatory result named `texture ID`. It is used to store the newly added Texture Index in the glTF model so that the Texture can be bound as a Texture property of a Material through `UpdateGltfOperator`. It must be a 1-channel UINT16 type Scalar Tensor, with a shape of `{N, }`.
* **`UpdateGltfOperator`**
   Updates a parameter of the glTF model. For details, refer to [API Overview](/securemr-api-overview).
* **`SwitchGltfRenderStatusOperator`**
   There are the following operands:
   | **Operand** | **Required** | **Description** |
   | --- | --- | --- |
   | gltf | Yes | The target glTF model Tensor. It must be of the glTF type. |
   | world pose | No | If not empty, the rendering of the specified glTF model starts. This Operand should provide the initial coordinates of the glTF model (the reference frame default is OpenXR Local coordinate system but can be modified through the `view locked` Operand below); if empty, the rendering of the glTF model stops. |
   | visible | No | Used to determine whether the glTF model is visible. If the tensor is non-zero, the model is visible and starts rendering; otherwise, the model stops rendering. Visible by default. |
   | view locked | No | Used to determine whether the glTF model follows View Space. If the Tensor is non-zero, the model uses OpenXR's View Space as the reference frame; otherwise, it uses OpenXR's Local Space as the reference frame. <br> ***Note***: When `view locked` is `true`, `CAMERA SPACE TO WORLD` should not be used because `CAMERA SPACE TO WORLD` uses OpenXR's Local coordinate system as the reference frame. |

### **Code sample**
The complete code sample is as follows:
```C#
using System.Collections;
using System.Collections.Generic;
using System.Text;
using UnityEngine;
using Unity.XR.PXR;
using Unity.XR.PXR.SecureMR;
using Color = Unity.XR.PXR.SecureMR.Color;

public class ShowVST : MonoBehaviour
{
    private Provider provider;
    private Pipeline pipeline;
    private Pipeline pipeline2;
    
    int image_width = 3248;   // Same as VST_IMAGE_WIDTH
    int image_height = 2464;  // Same as VST_IMAGE_HEIGHT
    int crop_x1 = 1444;
    int crop_y1 = 1332;
    int crop_x2 = 2045;
    int crop_y2 = 1933;
    int crop_width = 224;
    int crop_height = 224;
    
    private Tensor debugGltfPlaceholder;
    private Tensor debugGltfPlaceholder2;
    public TextAsset tvGltf;
    private Tensor debugGltfTensor;
    private Tensor debugGltfTensor2;
    
    private Tensor cropRgbWrite;
    private Tensor cropRgbGlobal;
    private Tensor cropRgbRead;
    
    // Start is called before the first frame update
    void Start()
    {
        PXR_Manager.EnableVideoSeeThrough = true;
        
        provider = new Provider(image_width, image_height);

        CreatePipeline();
        
        CreateRender();
    }
    
    void CreatePipeline()
    {
        //create provider and pipeline
        pipeline2 = provider.CreatePipeline();
        cropRgbGlobal = provider.CreateTensor<byte,Matrix>(3, new TensorShape(crop_width, crop_height));
    
        //create operator
        var vstOp = pipeline2.CreateOperator<RectifiedVstAccessOperator>();
        var getAffineOp = pipeline2.CreateOperator<GetAffineOperator>();
        var applyAffineOp = pipeline2.CreateOperator<ApplyAffineOperator>();

        //create tensor
        var rawRgb = pipeline2.CreateTensor<byte,Matrix>(3, new TensorShape(image_height, image_width));
        cropRgbWrite = pipeline2.CreateTensorReference<byte,Matrix>(3, new TensorShape(crop_width, crop_height));
        var affineMat = pipeline2.CreateTensor<float,Matrix>(1, new TensorShape(2,3));
        var srcPoints  = pipeline2.CreateTensor<float,Point>(2, new TensorShape(3));
        var dstPoints  = pipeline2.CreateTensor<float,Point>(2, new TensorShape(3));
    
        float[] srcPointsData = {crop_x1,crop_y1,crop_x2,crop_y1,crop_x2,crop_y2};
        float[] dstPointsData = {0,0,crop_width,0,crop_width,crop_height};
    
        srcPoints.Reset(srcPointsData);
        dstPoints.Reset(dstPointsData);
    
        //set operator input and output
        vstOp.SetResult("left image", rawRgb);
    
        getAffineOp.SetOperand("src",srcPoints);
        getAffineOp.SetOperand("dst",dstPoints);
        getAffineOp.SetResult("result",affineMat);
    
        applyAffineOp.SetOperand("affine",affineMat);
        applyAffineOp.SetOperand("src image",rawRgb);
        applyAffineOp.SetResult("dst image",cropRgbWrite);
        
        InvokeRepeating(nameof(RunPipeline), 0, 0.02f);
    
    }
    
    void RunPipeline()
    {
        var pipelineIOPair = pipeline2.CreateTensorMapping();
        pipelineIOPair.Set(cropRgbWrite,cropRgbGlobal);
    
        pipeline2.Execute(pipelineIOPair);
    }

    void CreateRender()
    {
        pipeline = provider.CreatePipeline();
        
        var loadTextureOp = pipeline.CreateOperator<LoadTextureOperator>();
        UpdateGltfOperatorConfiguration updateGltfConfiguration = new UpdateGltfOperatorConfiguration(SecureMRGltfOperatorAttribute.MaterialBaseColorTexture);
        var updateGltfOp = pipeline.CreateOperator<UpdateGltfOperator>(updateGltfConfiguration);
        var renderGltfOp2 = pipeline.CreateOperator<SwitchGltfRenderStatusOperator>();
        
        var gltfMaterialIndex = pipeline.CreateTensor<ushort,Scalar>(1, new TensorShape(1));
        var gltfTextureIndex = pipeline.CreateTensor<ushort,Scalar>(1, new TensorShape(1));
        var poseMat2 = pipeline.CreateTensor<float,Matrix>(1, new TensorShape(4,4));
        debugGltfPlaceholder2 = pipeline.CreateTensorReference<Gltf>();
        cropRgbRead = pipeline.CreateTensorReference<byte,Matrix>(3, new TensorShape(crop_width, crop_height));
        
        loadTextureOp.SetOperand("rgb image", cropRgbRead);
        loadTextureOp.SetOperand("gltf", debugGltfPlaceholder2);
        loadTextureOp.SetResult("texture ID", gltfTextureIndex);

        updateGltfOp.SetOperand("gltf",debugGltfPlaceholder2);
        updateGltfOp.SetOperand("material ID",gltfMaterialIndex);
        updateGltfOp.SetOperand("value",gltfTextureIndex);

        renderGltfOp2.SetOperand("gltf",debugGltfPlaceholder2);
        renderGltfOp2.SetOperand("world pose",poseMat2);

        float[] poseMatValue2 =
        {0.5f, 0.0f, 0.0f, 0.0f,
            0.0f, 0.5f, 0.0f, 1.0f,
            0.0f, 0.0f, 0.5f, -1.5f,
            0.0f, 0.0f, 0.0f, 1.0f};
        poseMat2.Reset(poseMatValue2);
    
        var gltfData = tvGltf.bytes;
        debugGltfTensor2 = provider.CreateTensor<Gltf>(gltfData);
        
        InvokeRepeating(nameof(RenderFrame), 0, 0.02f);
    }
    
    void RenderFrame()
    {
        var pipelineIOPair = pipeline.CreateTensorMapping();
        pipelineIOPair.Set(debugGltfPlaceholder2,debugGltfTensor2);
        pipelineIOPair.Set(cropRgbRead,cropRgbGlobal);
        pipeline.Execute(pipelineIOPair);
    }
}
```

## Run the machine learning model
A handwritten digit classification model (file listed below) is used to demonstrate how to use SecureMR to run a machine learning model.
<a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87ef725fec3843f2a3058f56e1481eae~tplv-goo7wpa0wc-image.image" filename="mnist_md5_48fe972.bin" download>mnist_md5_48fe972.bin</a>
This is a category model. After inputting a grayscale image of a handwritten digit, the model will output the identified number, as shown in the figure below:
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b6b8c753b7f404abebac25394c4e96b~tplv-goo7wpa0wc-image.image" width="600px" />

Here is a demo video:

            <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cfbd0f1d15349589b879d9cffa4b5f5~tplv-goo7wpa0wc-image.image></video>

When deploying this model, you also need to extract the small part of the image where the number is located from the entire VST image, convert the RGB image into grayscale, and normalize the input data before feeding it into the network. The complete pipeline is as follows:
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5744a36acd114f468d85eb5b2784e7b9~tplv-goo7wpa0wc-image.image)
Since the model is relatively large, it is recommended to store it in StreamingAssets and then use UnityWebRequest to load it. The key code for this step is as follows:
```C#
IEnumerator Initialize()
{
    yield return LoadData();

    if (fileBytes != null)
    {
        CreatePipeline();
        
        CreateRender();
    }
}
IEnumerator LoadData()
{
    string filepath = Path.Combine(Application.streamingAssetsPath, "mnist_md5_48fe972.bin");
    
    UnityWebRequest request = UnityWebRequest.Get(filepath);
    yield return request.SendWebRequest();

    if (request.result == UnityWebRequest.Result.Success)
    {
        fileBytes = request.downloadHandler.data;
    }
}

ColorConvertOperatorConfiguration colorConvertConfiguration = new ColorConvertOperatorConfiguration(7);
var rgbToGrayOp = pipeline2.CreateOperator<ConvertColorOperator>(colorConvertConfiguration);
var uint8ToFloat32Op = pipeline2.CreateOperator<AssignmentOperator>();
ArithmeticComposeOperatorConfiguration normalizeConfiguration = new ArithmeticComposeOperatorConfiguration("{0} / 255.0");
var normalizeOp = pipeline2.CreateOperator<ArithmeticComposeOperator>(normalizeConfiguration);

//create mnist model
SecureMROperatorModelConfig modelInput = new SecureMROperatorModelConfig
{
    encodingType = SecureMRModelEncoding.Float32,
    nodeName = "input_1",
    operatorIOName = "input_1",
};
SecureMROperatorModelConfig modelOutput = new SecureMROperatorModelConfig
{
    encodingType = SecureMRModelEncoding.Float32,
    nodeName = "_538",
    operatorIOName = "_538",
};
SecureMROperatorModelConfig modelOutput2 = new SecureMROperatorModelConfig
{
    encodingType = SecureMRModelEncoding.Int32,
    nodeName = "_539",
    operatorIOName = "_539",
};
List<SecureMROperatorModelConfig> inputConfigs = new List<SecureMROperatorModelConfig>();
List<SecureMROperatorModelConfig> outputConfigs = new List<SecureMROperatorModelConfig>();
inputConfigs.Add(modelInput);
outputConfigs.Add(modelOutput);
outputConfigs.Add(modelOutput2);
ModelOperatorConfiguration modelConfiguration = new ModelOperatorConfiguration(inputConfigs, outputConfigs, fileBytes,SecureMRModelType.QnnContextBinary,"mnist");
var modelOp = pipeline2.CreateOperator<RunModelInferenceOperator>(modelConfiguration);
var inputTensor = pipeline2.CreateTensor<float,Matrix>(1, new TensorShape(224,224));
predScoreWrite = pipeline2.CreateTensorReference<float,Scalar>(1, new TensorShape(1));
predClassWrite = pipeline2.CreateTensorReference<int,Scalar>(1, new TensorShape(1));

modelOp.SetOperand("input_1",inputTensor);
modelOp.SetResult("_538",predScoreWrite);
modelOp.SetResult("_539",predClassWrite);
```

After this step, the model can run successfully, but you can not preview the effect. Therefore, additional logic needs to be added. The key code is as follows:
```C#
var text3 = pipeline.CreateTensor<sbyte,Scalar>(1, new TensorShape(30));
var startPosition3 = pipeline.CreateTensor<float,Point>(2, new TensorShape(1));
var colors3 = pipeline.CreateTensor<byte,Color>(4, new TensorShape(2));
var textureId3 = pipeline.CreateTensor<ushort,Scalar>(1, new TensorShape(1));
var fontSize3 = pipeline.CreateTensor<float,Scalar>(1, new TensorShape(1));
var poseMat3= pipeline.CreateTensor<float,Matrix>(1, new TensorShape(4,4));
debugGltfPlaceholder3= pipeline.CreateTensorReference<Gltf>();
predClassRead = pipeline.CreateTensorReference<int,Scalar>(1, new TensorShape(1));
predScoreRead = pipeline.CreateTensorReference<float,Scalar>(1, new TensorShape(1));
renderTextOp3.SetOperand("text",predScoreRead);
renderTextOp3.SetOperand("start",startPosition3);
renderTextOp3.SetOperand("colors",colors3);
renderTextOp3.SetOperand("texture ID",textureId3);
renderTextOp3.SetOperand("font size",fontSize3);
renderTextOp3.SetOperand("gltf",debugGltfPlaceholder3);
renderGltfOp3.SetOperand("gltf",debugGltfPlaceholder3);
renderGltfOp3.SetOperand("world pose",poseMat3);

text3.Reset(Encoding.UTF8.GetBytes(textValue));
startPosition3.Reset(startValue);
colors3.Reset(colorsValue);
textureId3.Reset(textureId_value);
fontSize3.Reset(fontSize_value);
float[] poseMatValue3 = {0.5f, 0.0f, 0.0f, 1.0f,
    0.0f, 0.5f, 0.0f, 0.0f,
    0.0f, 0.0f, 0.5f, -1.5f,
    0.0f, 0.0f, 0.0f, 1.0f};
poseMat3.Reset(poseMatValue3);

void RenderFrame()
{
    pipelineIOPair.Set(debugGltfPlaceholder3,debugGltfTensor3);
    pipelineIOPair.Set(predClassRead,predClassGlobal);
    pipelineIOPair.Set(predScoreRead,predScoreGlobal);
    
    pipeline.Execute(pipelineIOPair);
}
```

The complete code example is as follows:
```C#
using System;
using System.Collections;
using System.Collections.Generic;
using System.IO;
using System.Text;
using Unity.VisualScripting;
using UnityEngine;
using Unity.XR.PXR;
using Unity.XR.PXR.SecureMR;
using UnityEngine.Networking;
using Color = Unity.XR.PXR.SecureMR.Color;

public class UseMLModel : MonoBehaviour
{
    int image_width = 3248;   // Same as VST_IMAGE_WIDTH
    int image_height = 2464;  // Same as VST_IMAGE_HEIGHT
    int crop_x1 = 1444;
    int crop_y1 = 1332;
    int crop_x2 = 2045;
    int crop_y2 = 1933;
    int crop_width = 224;
    int crop_height = 224;
    
    private Provider provider;
    private Pipeline pipeline;
    private Pipeline pipeline2;
    
    private Tensor debugGltfTensor;
    private Tensor debugGltfTensor2;
    private Tensor debugGltfTensor3;
    
    private Tensor debugGltfPlaceholder;
    private Tensor debugGltfPlaceholder2;
    private Tensor debugGltfPlaceholder3;
    
    private Tensor cropRgbWrite;
    private Tensor cropRgbGlobal;
    private Tensor cropRgbRead;
    
    private Tensor predClassGlobal;
    private Tensor predScoreGlobal;
    private Tensor predClassWrite;
    private Tensor predScoreWrite;
    private Tensor predClassRead;
    private Tensor predScoreRead;

    public TextAsset tvGltf;
    private byte[] fileBytes;
    
    // Start is called before the first frame update
    void Awake()
    {
        StartCoroutine(Initialize());
        
        PXR_Manager.EnableVideoSeeThrough = true;
        
        provider = new Provider(image_width, image_height);
    }

    IEnumerator Initialize()
    {
        yield return LoadData();

        if (fileBytes != null)
        {
            CreatePipeline();
            
            CreateRender();
        }
    }
    IEnumerator LoadData()
    {
        string filepath = Path.Combine(Application.streamingAssetsPath, "mnist_md5_48fe972.bin");
        
        UnityWebRequest request = UnityWebRequest.Get(filepath);
        yield return request.SendWebRequest();

        if (request.result == UnityWebRequest.Result.Success)
        {
            fileBytes = request.downloadHandler.data;
        }
    }
    
    void CreatePipeline()
    {
        //create provider and pipeline
        pipeline2 = provider.CreatePipeline();
        cropRgbGlobal = provider.CreateTensor<byte,Matrix>(3, new TensorShape(crop_width, crop_height));
        predClassGlobal = provider.CreateTensor<int,Scalar>(1, new TensorShape(1));
        predScoreGlobal = provider.CreateTensor<float,Scalar>(1, new TensorShape(1));
        
        //create operator
        var vstOp = pipeline2.CreateOperator<RectifiedVstAccessOperator>();
        var getAffineOp = pipeline2.CreateOperator<GetAffineOperator>();
        var applyAffineOp = pipeline2.CreateOperator<ApplyAffineOperator>();
        
        ColorConvertOperatorConfiguration colorConvertConfiguration = new ColorConvertOperatorConfiguration(7);
        var rgbToGrayOp = pipeline2.CreateOperator<ConvertColorOperator>(colorConvertConfiguration);
        var uint8ToFloat32Op = pipeline2.CreateOperator<AssignmentOperator>();
        ArithmeticComposeOperatorConfiguration normalizeConfiguration = new ArithmeticComposeOperatorConfiguration("{0} / 255.0");
        var normalizeOp = pipeline2.CreateOperator<ArithmeticComposeOperator>(normalizeConfiguration);
        
        //create tensor
        var rawRgb = pipeline2.CreateTensor<byte,Matrix>(3, new TensorShape(image_height, image_width));
        cropRgbWrite = pipeline2.CreateTensorReference<byte,Matrix>(3, new TensorShape(crop_width, crop_height));
        var affineMat = pipeline2.CreateTensor<float,Matrix>(1, new TensorShape(2,3));
        var srcPoints  = pipeline2.CreateTensor<float,Point>(2, new TensorShape(3));
        var dstPoints  = pipeline2.CreateTensor<float,Point>(2, new TensorShape(3));
        
        var cropGray = pipeline2.CreateTensor<byte,Matrix>(1, new TensorShape(crop_width,crop_height));
        var cropGrayFloat = pipeline2.CreateTensor<float,Matrix>(1, new TensorShape(crop_width, crop_height));
        
        //create mnist model
        SecureMROperatorModelConfig modelInput = new SecureMROperatorModelConfig
        {
            encodingType = SecureMRModelEncoding.Float32,
            nodeName = "input_1",
            operatorIOName = "input_1",
        };
        SecureMROperatorModelConfig modelOutput = new SecureMROperatorModelConfig
        {
            encodingType = SecureMRModelEncoding.Float32,
            nodeName = "_538",
            operatorIOName = "_538",
        };
        SecureMROperatorModelConfig modelOutput2 = new SecureMROperatorModelConfig
        {
            encodingType = SecureMRModelEncoding.Int32,
            nodeName = "_539",
            operatorIOName = "_539",
        };
        List<SecureMROperatorModelConfig> inputConfigs = new List<SecureMROperatorModelConfig>();
        List<SecureMROperatorModelConfig> outputConfigs = new List<SecureMROperatorModelConfig>();
        inputConfigs.Add(modelInput);
        outputConfigs.Add(modelOutput);
        outputConfigs.Add(modelOutput2);
        ModelOperatorConfiguration modelConfiguration = new ModelOperatorConfiguration(inputConfigs, outputConfigs, fileBytes,SecureMRModelType.QnnContextBinary,"mnist");
        var modelOp = pipeline2.CreateOperator<RunModelInferenceOperator>(modelConfiguration);
        var inputTensor = pipeline2.CreateTensor<float,Matrix>(1, new TensorShape(224,224));
        predScoreWrite = pipeline2.CreateTensorReference<float,Scalar>(1, new TensorShape(1));
        predClassWrite = pipeline2.CreateTensorReference<int,Scalar>(1, new TensorShape(1));
        
        float[] srcPointsData = {crop_x1,crop_y1,crop_x2,crop_y1,crop_x2,crop_y2};
        float[] dstPointsData = {0,0,crop_width,0,crop_width,crop_height};
        
        srcPoints.Reset(srcPointsData);
        dstPoints.Reset(dstPointsData);
        
        //set operator input and output
        vstOp.SetResult("left image", rawRgb);
        
        getAffineOp.SetOperand("src",srcPoints);
        getAffineOp.SetOperand("dst",dstPoints);
        getAffineOp.SetResult("result",affineMat);
        
        applyAffineOp.SetOperand("affine",affineMat);
        applyAffineOp.SetOperand("src image",rawRgb);
        applyAffineOp.SetResult("dst image",cropRgbWrite);
        
        rgbToGrayOp.SetOperand("src",cropRgbWrite);
        rgbToGrayOp.SetResult("dst",cropGray);
        
        uint8ToFloat32Op.SetOperand("src",cropGray);
        uint8ToFloat32Op.SetResult("dst",cropGrayFloat);
        
        modelOp.SetOperand("input_1",inputTensor);
        modelOp.SetResult("_538",predScoreWrite);
        modelOp.SetResult("_539",predClassWrite);
        
        normalizeOp.SetOperand("{0}",cropGrayFloat);
        normalizeOp.SetResult("result",inputTensor);
        
        InvokeRepeating(nameof(RunPipeline), 0, 0.02f);
    }
    
    void RunPipeline()
    {
        var pipelineIOPair = pipeline2.CreateTensorMapping();
        pipelineIOPair.Set(cropRgbWrite,cropRgbGlobal);
        pipelineIOPair.Set(predClassWrite,predClassGlobal);
        pipelineIOPair.Set(predScoreWrite,predScoreGlobal);
        
        pipeline2.Execute(pipelineIOPair);
    }

    void CreateRender()
    {
        pipeline = provider.CreatePipeline();
        
        //create operator
        RenderTextOperatorConfiguration renderTextConfiguration = new RenderTextOperatorConfiguration(SecureMRFontTypeface.SansSerif, "en-US", 1440, 960);
        var renderTextOp = pipeline.CreateOperator<RenderTextOperator>(renderTextConfiguration);
        var renderGltfOp = pipeline.CreateOperator<SwitchGltfRenderStatusOperator>();
        
        var loadTextureOp = pipeline.CreateOperator<LoadTextureOperator>();
        UpdateGltfOperatorConfiguration updateGltfConfiguration = new UpdateGltfOperatorConfiguration(SecureMRGltfOperatorAttribute.MaterialBaseColorTexture);
        var updateGltfOp = pipeline.CreateOperator<UpdateGltfOperator>(updateGltfConfiguration);
        var renderGltfOp2 = pipeline.CreateOperator<SwitchGltfRenderStatusOperator>();
        
        var renderTextOp3 = pipeline.CreateOperator<RenderTextOperator>(renderTextConfiguration);
        var renderGltfOp3 = pipeline.CreateOperator<SwitchGltfRenderStatusOperator>();
        
        //create tensor
        var text = pipeline.CreateTensor<sbyte,Scalar>(1, new TensorShape(30));
        var startPosition = pipeline.CreateTensor<float,Point>(2, new TensorShape(1));
        var colors = pipeline.CreateTensor<byte,Color>(4, new TensorShape(2));
        var textureId = pipeline.CreateTensor<ushort,Scalar>(1, new TensorShape(1));
        var fontSize = pipeline.CreateTensor<float,Scalar>(1, new TensorShape(1));
        var poseMat  = pipeline.CreateTensor<float,Matrix>(1, new TensorShape(4,4));
        debugGltfPlaceholder = pipeline.CreateTensorReference<Gltf>();
        
        var gltfMaterialIndex = pipeline.CreateTensor<ushort,Scalar>(1, new TensorShape(1));
        var gltfTextureIndex = pipeline.CreateTensor<ushort,Scalar>(1, new TensorShape(1));
        var poseMat2 = pipeline.CreateTensor<float,Matrix>(1, new TensorShape(4,4));
        debugGltfPlaceholder2 = pipeline.CreateTensorReference<Gltf>();
        cropRgbRead = pipeline.CreateTensorReference<byte,Matrix>(3, new TensorShape(crop_width, crop_height));
        
        var text3 = pipeline.CreateTensor<sbyte,Scalar>(1, new TensorShape(30));
        var startPosition3 = pipeline.CreateTensor<float,Point>(2, new TensorShape(1));
        var colors3 = pipeline.CreateTensor<byte,Color>(4, new TensorShape(2));
        var textureId3 = pipeline.CreateTensor<ushort,Scalar>(1, new TensorShape(1));
        var fontSize3 = pipeline.CreateTensor<float,Scalar>(1, new TensorShape(1));
        var poseMat3= pipeline.CreateTensor<float,Matrix>(1, new TensorShape(4,4));
        debugGltfPlaceholder3= pipeline.CreateTensorReference<Gltf>();
        predClassRead = pipeline.CreateTensorReference<int,Scalar>(1, new TensorShape(1));
        predScoreRead = pipeline.CreateTensorReference<float,Scalar>(1, new TensorShape(1));
        
        //set input and output
        renderTextOp.SetOperand("text",predClassRead);
        renderTextOp.SetOperand("start",startPosition);
        renderTextOp.SetOperand("colors",colors);
        renderTextOp.SetOperand("texture ID",textureId);
        renderTextOp.SetOperand("font size",fontSize);
        renderTextOp.SetOperand("gltf",debugGltfPlaceholder);
        renderGltfOp.SetOperand("gltf",debugGltfPlaceholder);
        renderGltfOp.SetOperand("world pose",poseMat);
        
        string textValue = "Hello World";
        text.Reset(Encoding.UTF8.GetBytes(textValue));
        float[] startValue = {0.1f, 0.3f};
        startPosition.Reset(startValue);
        byte[] colorsValue = {255, 255, 255, 255, 0, 0, 0, 255};
        colors.Reset(colorsValue);
        int[] textureId_value = {0};
        textureId.Reset(textureId_value);
        float[] fontSize_value = {144.0f};
        fontSize.Reset(fontSize_value);
        float[] poseMatValue = {0.5f, 0.0f, 0.0f, -0.5f,
            0.0f, 0.5f, 0.0f, 0.0f,
            0.0f, 0.0f, 0.5f, -1.5f,
            0.0f, 0.0f, 0.0f, 1.0f};
        poseMat.Reset(poseMatValue);
        
        loadTextureOp.SetOperand("rgb image", cropRgbRead);
        loadTextureOp.SetOperand("gltf", debugGltfPlaceholder2);
        loadTextureOp.SetResult("texture ID", gltfTextureIndex);
        updateGltfOp.SetOperand("gltf",debugGltfPlaceholder2);
        updateGltfOp.SetOperand("material ID",gltfMaterialIndex);
        updateGltfOp.SetOperand("value",gltfTextureIndex);
        renderGltfOp2.SetOperand("gltf",debugGltfPlaceholder2);
        renderGltfOp2.SetOperand("world pose",poseMat2);

        float[] poseMatValue2 =
            {0.5f, 0.0f, 0.0f, 0.0f,
            0.0f, 0.5f, 0.0f, 1.0f,
            0.0f, 0.0f, 0.5f, -1.5f,
            0.0f, 0.0f, 0.0f, 1.0f};
        poseMat2.Reset(poseMatValue2);
        
        renderTextOp3.SetOperand("text",predScoreRead);
        renderTextOp3.SetOperand("start",startPosition3);
        renderTextOp3.SetOperand("colors",colors3);
        renderTextOp3.SetOperand("texture ID",textureId3);
        renderTextOp3.SetOperand("font size",fontSize3);
        renderTextOp3.SetOperand("gltf",debugGltfPlaceholder3);
        renderGltfOp3.SetOperand("gltf",debugGltfPlaceholder3);
        renderGltfOp3.SetOperand("world pose",poseMat3);
        
        text3.Reset(Encoding.UTF8.GetBytes(textValue));
        startPosition3.Reset(startValue);
        colors3.Reset(colorsValue);
        textureId3.Reset(textureId_value);
        fontSize3.Reset(fontSize_value);
        float[] poseMatValue3 = {0.5f, 0.0f, 0.0f, 1.0f,
            0.0f, 0.5f, 0.0f, 0.0f,
            0.0f, 0.0f, 0.5f, -1.5f,
            0.0f, 0.0f, 0.0f, 1.0f};
        poseMat3.Reset(poseMatValue3);
        
        var gltfData = tvGltf.bytes;
        debugGltfTensor = provider.CreateTensor<Gltf>(gltfData);
        debugGltfTensor2 = provider.CreateTensor<Gltf>(gltfData);
        debugGltfTensor3 = provider.CreateTensor<Gltf>(gltfData);
        
        InvokeRepeating(nameof(RenderFrame), 0, 0.02f);
    }
    
    void RenderFrame()
    {
        var pipelineIOPair = pipeline.CreateTensorMapping();
        pipelineIOPair.Set(debugGltfPlaceholder,debugGltfTensor);
        pipelineIOPair.Set(debugGltfPlaceholder2,debugGltfTensor2);
        pipelineIOPair.Set(cropRgbRead,cropRgbGlobal);
        pipelineIOPair.Set(debugGltfPlaceholder3,debugGltfTensor3);
        pipelineIOPair.Set(predClassRead,predClassGlobal);
        pipelineIOPair.Set(predScoreRead,predScoreGlobal);
        
        pipeline.Execute(pipelineIOPair);
    }
}
```

## Related resources

* gITF monitor model:
   <a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/027c39ec348e4b9a8bd614cbe1c858cf~tplv-goo7wpa0wc-image.image" filename="tv.gltf.bytes" download>tv.gltf.bytes</a>
* Handwritten digit classification model:
   <a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96e97bf2967d46efbd192e648b6713bb~tplv-goo7wpa0wc-image.image" filename="mnist_md5_48fe972 (1).bin" download>mnist_md5_48fe972 (1).bin</a>

## Related content
PICO SecureMR provides different types of operators with different features. You can select operators based on your needs. For details, refer to [Use different operators](/en_use-different-operators).


# --- END: SecureMR use cases.md ---



# --- BEGIN: Service design(2).md ---

Incorporating achievements into your app can create a positive feedback loop, increase its level of challenge, and boost user engagement. By offering prizes like trophies and badges, you can reward users for accomplishing specific goals. This article takes you into the design of PICO SDK's achievement service, including the introductions to different types of achievement, achievement information structure, hidden achievements, and more.
## Achievement types
You can create simple, count, and bitfiled achievements for your app.
| **Type** | **Description** |
| --- | --- |
| Simple | Simple achievements are either locked or unlocked. A simple achievement is unlocked when a corresponding event or task is complete, such as completing the beginner tutorial or reaching a specific level. |
| Count | A count achievement has an integer target for unlocking it. For example, a count achievement can be unlocked after a user defeats 100 enemies. |
| Bitfield | A bitfield achievement has a predefined number of bits for users to unlock. In other words, when the number of completed bits(tasks/events) reaches the predefined target to the total number, which is similar to setting the bits in a bitfield, a bitfield achievement is then unlocked. For example, collecting any 7 of the 10 gems can unlock a bitfield achievement. |
## Achievement info structure
The following table describes the fields included in the `AchievementDefinition` structure. 
| **Field** | **Type** | **Description** |
| --- | --- | --- |
| Type | AchievementType | The type of achievement. |
| Name | string | The API name of the achievement. An API name serves as the unique identifier of an achievement. |
| BitfieldLength | uint | The requirement that users should meet for unlocking a bitfield achievement. |
| Target | long | The requirement that users should meet for unlocking a count achievement. |
| Description | string | The description of the achievement. |
| Title | string | The display name of the achievement. |
| IsArchived | bool | Indicates whether the achievement is archived. Archived achievements are invisible to users. |
| IsSecret | bool | Indicates whether the achievement is a hidden achievement. |
| ID (not used） | ulong | The ID of the achievement. |
| UnlockedDescription | string | The description displayed to users after they unlock the achievement. |
| WritePolicy | AchievementWritePolicy | The data-writing policy of the achievement, which indicates whether the client or server are allowed to update the achievement's progress. |
| LockedImageURL | string | The image displayed to users when the achievement is still locked. |
| UnlockedImageURL | string | The image displayed to users after they unlock the achievement. |
## Hidden achievements
Hidden achievements are a special set of achievements that are normally invisible to users. These achievements only become visible if the specified requirements are met. Therefore, hidden achievements can bring surprises to users. When creating an achievement on the PICO Developer Platform, you can decide whether to set it as a hidden achievement.
## Achievement notification
Users will receive notifications in both the app and the notification center after they unlock achievements.  When creating an achievement on the PICO Developer Platform, you can enable the notification function for it.
| **In-app toast notification (in the lower-middle area)**  | **Notification center**  |
| --- | --- |
| ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f46f912dec6c4e109a55ea2d58be91d6~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f26d0c256ea6435aaa5e04c378cad2e7~tplv-goo7wpa0wc-image.image) |
## Related article
For how to create an achievement and configure achievement details, refer to the "[Achievements: Platform service setups](/en_achievements-platform-service-setups)" article.


# --- END: Service design(2).md ---



# --- BEGIN: Service design.md ---

Leaderboard is fundamental and significan to an app. By displaying users' rankings to each other, leaderboards can create healthy competitions among users. This article takes you into the design of PICO SDK's leaderboard service, involving the introduction to the unique identifier of leaderboard, leaderboard entries, ranking exceed notification, and more.
## API name
An API name serves as a unique identifier for a leaderboard, which is created by yourself on the PICO Developer Platform. You can use the API name to retrieve the information of a specified leaderboard or retrieve and update entries for a specified leaderboard.
## Leaderboard entries
Each user has only one entry on a leaderboard. The entry is associated with the user's ID and displays the user's best score by default.  You can use the leaderboard service with the achievement service, unlocking an achievement for a user when the user obtains a certain score or ranking on the leaderboard.
## Ranking exceed notification
When creating a leaderboard, you have the option to enable the ranking exceed notification. Once enabled, users will receive notifications in their device's notification center when they are surpassed by their friends. By clicking the notification area, the system will launch the corresponding app and direct the user to it.
## Association with a destination
When creating a leaderboard, you can associate a destination with the leaderboard. Once associated, users can jump to the destination from the leaderboard, and you need to design a button for the jump action on the leaderboard UI. For more information on destinations, refer to the "[Social Interaction: Key concepts](/en_social-interaction-key-concepts#410cf2f3)" article.
## Learn more

* For detailed instructions on creating a leaderboard on the PICO Developer Platform, refer to the "[Leaderboards: Platform service setups](/en_leaderboards-platform-service-setups)" article.
* For more information on the use cases of the leaderboard service and code samples, refer to the "[Leaderboards: Use cases & code samples](/en_leaderboards-use-cases-and-code-samples)" article.


# --- END: Service design.md ---



# --- BEGIN: Set up a camera for each eye and display content in two cameras separately.md ---

This page introduces how to set a camera for each eye and display content in two cameras separately.
### Step1: Set up the Main Camera
Follow the steps below to set up the Main Camera.

1. Open your project in Unity Editor.
2. Select an **XR Rig** (or XR Origin).
   You'll see the **XR Rig** settings box under the **Inspector** tab.
3. In the **Camera Game Object** field, select a camera object (e.g., **Main Camera** ).
      * In general, **Main Camera** is selected by default.
      * You can rename **Main Camera** as needed.

   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/26161898b9064aad96b9ef704bf6e76a~tplv-em5hxbkur4-noop.image?width=2560&height=1316)
4. Click **Main Camera**.
   You'll see the **Tracked Pose Driver** settings box under the **Inspector** tab.
5. On the **Camera** pane, set **Target Eye** to **None (Main Display)**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8803285b5c44ffdafdbee2bb2a36a04~tplv-goo7wpa0wc-image.image)
6. (Optional) Configure the following parameters for **Main Camera** as needed.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/2b3a159396424fc88424438bdd75a086~tplv-em5hxbkur4-noop.image?width=629&height=307)

### Step2: Add left-eye and right-eye cameras
Follow the steps below to add a camera for each eye.

1. Create two cameras under the **Main Camera** object, and name two cameras as needed (e.g., **LeftCamera** and **RightCamera** ).
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/39f0129b03764e22a146faabaa28d15d~tplv-em5hxbkur4-noop.image?width=552&height=634)
2. Click **LeftCamera** .
   You'll see the **Camera** settings box under the **Inspector** tab.
3. Set **Target Eye** to **Left** .
4. Click **RightCamera** .
   You'll see the **Camera** settings box under the **Inspector** tab.
5. Set **Target Eye** to **Right** .

### Step3: Associate objects with layers
Before associating object with left-eye and right-eye cameras, you need to associate objects with layers. The steps are as follows.

1. Select an object (e.g., **Cube** ).
2. In the **Layer** field under the **Inspector** tab, select layer(s) for **Cube** .
   **Cube** is associated with the selected layer(s).
   You can click **Add Layer** to add layer(s) and name them as needed (e.g., **LeftCamera** layer and **RigtCamera** layer)

   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/3d9589fc202d405abea94669d95787fd~tplv-em5hxbkur4-noop.image?width=2560&height=1317)

### Step4: Associate layers with left-eye and right-eye cameras
Follow the steps below to associate layers with left-eye and right-eye cameras. After association, the left-eye camera and right-eye camera will display the objects associated with each layer separately. The steps are as follows.

1. Click **LeftCamera**.
2. In the **Culling Mask** field, select layer(s) for **LeftCamera**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/78117eaccacd414282d926a12f75712e~tplv-em5hxbkur4-noop.image?width=2560&height=1316)
3. Click **RightCamera** .
4. In the **Culling Mask** field, select layer(s) for **RightCamera**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/df8bf51267284b5ab180ef0ab92e147f~tplv-em5hxbkur4-noop.image?width=2560&height=1313)


# --- END: Set up a camera for each eye and display content in two cameras separately.md ---



# --- BEGIN: Settlement-related questions.md ---

Refer to [this article](/document/distribute/settlement-related-faqs/).


# --- END: Settlement-related questions.md ---



# --- BEGIN: Spatial data permission control.md ---

You can provide users with a brand new mixed reality experience using the Sense Pack of PICO SDK. The implementation of mixed reality-related features involves the usage of users' spatial data, including spatial anchor data, scene capture data, and more. For PICO apps, users can decide whether to authorize your app to use their spatial data. If users refuse to authorize your app to use their spatial data, they will not be able to experience mixed reality-related content within your app.
## Related features

* Spatial Anchor
* Shared Spatial Anchor
* Scene Capture
* Spatial Mesh

## Spatial data authorization
After checking the **Spatial Anchor**, **Shared Spatial Anchor**, **Scene Capture**, and/or **Spatial Mesh** checkboxes on the **PXR_Manager (Script)** panel, the SDK automatically writes the following user permission information to the app's AndroidManifest.xml file:
```XML
<uses-permission android:name="com.picovr.permission.SPATIAL_DATA" > </uses-permission>
```

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a728b1b244cd40bdbd2093784141f3e4~tplv-goo7wpa0wc-image.image" width="500px" />

When a user opens your app, the system will pop up the following panel to request the user's permission to access spatial data. The user can choose to grant or deny authorization. After completing the operation in the pop-up window, the user can subsequently go to the device's **Settings** > **General** to modify the permission settings.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80bafc47b9054321b1ad23af621da176~tplv-goo7wpa0wc-image.image" width="400px" />

## Provide alternatives for declined or revoked authorization
If the user denies authorization for your app to use spatial data in the pop-up window, or revokes the authorization later, you need to handle such situations properly. You can remove or guide the user to skip the content that is designed on spatial data. For example, you can gradually fade out such content, or redirect the user to other parts of the app.
If your app uses spatial data as input, you can use the HMD, controllers, or other input methods to ensure the user can still use your app even without authorizing the use of spatial data.


# --- END: Spatial data permission control.md ---



# --- BEGIN: SpatialMLCapture Terms of Service.md ---

**You hereby acknowledge that SpatialMLCapture is a tool intended for developers, who** **are acting for purposes relating to their trade, business, research and development, craft or profession.**

1. **YOUR RELATIONSHIP WITH US**

Welcome to SpatialMLCapture! SpatialMLCapture ("**App**") is a data capture service provided by Pico Immersive Pte. Ltd. ("**we**", "**us**", or "**our**"). 
These Terms of Service (the/these "**Terms**") govern the relationship and serve as an agreement between you and us and set forth the terms and conditions by which you may access and use the App and our related services, applications, products and content (collectively, our "**Services**"). For the purposes of these Terms, "**you**" and "**your**" means you as the user of our Services.
The Terms form a legally binding agreement between you and us. Please take the time to read them carefully.
We may, in our sole and absolute discretion, perform our obligations under these Terms, whether in whole or in part, through one or more of our subsidiaries, or associated or related companies or corporations, or Third-Party Providers (as defined below), and the full and complete performance by any such person(s) shall constitute full performance by us of our corresponding obligations.

2. **ACCEPTING THE TERMS**

Your access and use of each of our Services shall be subject to these Terms. You acknowledge and agree that you may also be subject to additional terms, conditions, guidelines or policies applicable to certain Services, which are incorporated into these Terms by reference. By accessing or using any of our Services, you agree that a legally binding contract is formed between you and us, and that you accept these Terms and you agree to comply with them. Your access and use of our Services is also subject to our [Community Guidelines](https://www.picoxr.com/global/legal/community-guide), as amended from time to time, the terms of which may also be made available on such other channels as we may designate. If you do not agree to any of these Terms, you must not access or use any of our Services.
We may from time to time notify you of supplemental terms applicable to you in respect of access and/or use from particular jurisdictions ("**Jurisdiction-Specific Terms**"), and in the event of a conflict between the provisions of the Jurisdiction-Specific Terms and the rest of these Terms, the relevant Jurisdiction-Specific Terms will supersede and control. 
IF YOU ACCESS AND/OR USE OUR SERVICES, YOU CONFIRM (AND WE ARE ENTITLED TO ASSUME WITHOUT FURTHER INQUIRY) THAT YOU ARE AT LEAST 13 YEARS OF AGE OR OF THE RELEVANT AGE UNDER APPLICABLE LAW. IF YOU ARE YOUNGER THAN 18 YEARS OF AGE OR THE RELEVANT AGE OF MAJORITY UNDER APPLICABLE LAW ("**MINOR**"): (A) YOU MUST OBTAIN PERMISSION FROM A PARENT OR A LEGAL GUARDIAN (IF APPLICABLE) TO ACCESS AND/OR USE OUR SERVICES; (B) THAT PARENT OR LEGAL GUARDIAN (AS THE CASE MAY BE) MUST AGREE TO THESE TERMS; AND (C) YOU MUST ONLY USE ANY OF OUR SERVICES ONLY IN CONJUNCTION WITH AND UNDER THE SUPERVISION OR CONSENT OF A PARENT OR LEGAL GUARDIAN. IF YOU ARE THE PARENT OR LEGAL GUARDIAN OF A MINOR, YOU MUST ACCEPT THIS AGREEMENT ON THE MINOR'S BEHALF AND YOU WILL BE RESPONSIBLE FOR ALL ACCESS AND/OR USE OF OUR SERVICES UNDER THESE TERMS.
If you are the parent or legal guardian of a Minor, you further agree, acknowledge, and undertake to us that: 

* you must carefully supervise that Minor's access and/or use of our Services;
* it is your responsibility to determine whether any part of our Services is appropriate and/or safe for that Minor, and to ensure that the Minor does not access and/or use any content available on our Services which may not be suitable (or are otherwise indicated to be unsuitable) for that Minor;
* YOU MUST PAY IN FULL ALL SUMS DUE ARISING FROM THE ACTIVITIES OF THAT MINOR IN CONNECTION WITH OUR SERVICES, INCLUDING WITHOUT LIMITATION ANY TRANSACTIONS MADE ON OR THROUGH OUR SERVICES BY THAT MINOR ASSOCIATED WITH YOUR ACCESS CREDENTIALS, EVEN IF THE MINOR DID SO WITHOUT YOUR KNOWLEDGE AND/OR CONSENT; and
* YOU HEREBY EXPRESSLY CONSENT on behalf of that Minor to the collection, use, disclosure and/or processing of that Minor's personal data in accordance with these Terms and our Privacy Policy, and you agree that we may deem the same.

We may also prescribe additional age limitations for certain aspects of our Services that may be higher or lower than 13 years of age, as well as additional requirements for users to view age-restricted content available on our Services. Certain Services (or part thereof) may not be made available to you if you are under the relevant additional minimum age requirement. By using our Services where such additional limitations and/or additional requirements are prescribed, you confirm that you are over the relevant age specified and that you comply with the additional requirements (as applicable). If we learn that someone under the relevant age allowed is using our Services, we shall have the right to terminate that user's account or the user's access to our Services, in full or in part. 

3. **CHANGES TO THESE TERMS**

We may amend these Terms and/or the Privacy Policy from time to time, for instance when we update the functionality of any of our Services, when we combine multiple apps or services operated by us or our affiliates into a single combined service or app, or when there are regulatory changes. We may use commercially reasonable efforts to generally notify users of such changes, such as by sending an email notification to the address you have provided and/or notice through other measures. You should look at the Terms regularly to check for such changes. We will notify you of changes to the Terms that are material or having substantial impact on you.
We may also update the "*Last Updated*" date at the top of these Terms, which indicates the effective date of such updated Terms. Your continued access or use of any of our Services from the effective date of any such changes constitutes your acceptance of the updated Terms. If you do not agree to the updated Terms, you must stop accessing or using our Services.

4. **LICENSE TO SERVICES**

As a condition of your access to and use of any of our Services, you agree not to use our Services to infringe any intellectual property rights. We shall have the right, with or without notice, at any time and in our sole and absolute discretion to block access to and/or terminate the accounts of any user who infringes or is alleged to infringe any copyright, trade mark or other intellectual property or moral rights.
Subject to these Terms and your continuing compliance thereof, you are hereby granted a non-exclusive, limited, non-transferable, non-sublicensable, revocable license to access and use our Services wherever they are available at the time of use, including access to the PICO Content (as defined below) as part of our Services and solely in compliance with these Terms. We reserve all rights not expressly granted to you.
In the event of potential legal or regulatory restrictions in your jurisdiction, you: (a) may not be able to access or use any of our Services in or from a jurisdiction; and/or (b) may be infringing certain legal or regulatory requirements under applicable laws when accessing or using our Services in or from such jurisdiction. It is your sole responsibility to ascertain whether any such legal or regulatory restrictions exist, and we shall not be liable for any losses arising out of your inability to access or use such Services or any contravention of such legal or regulatory requirements. You shall fully indemnify us from and against any losses that we may be subject to or suffer in connection with any failure by you to comply with any such legal or regulatory restrictions. Notwithstanding anything in these Terms, we shall have the right to take steps to prevent any of our Services from being accessed or used in any jurisdiction as we may determine in our sole and absolute discretion from time to time.
 You shall bear full responsibility for all your actions in using our Services and ensure that you do not use our Services to conduct any illegal acts. You may on your own discretion, choose to download and use the following open-source SDK (available at [https://github.com/Pico-Developer/SpatialMP4](https://github.com/Pico-Developer/SpatialMP4)) to help you analyze the data you collect through our Services. The use of the SDK shall comply with the relevant open-source agreements. We do not provide any additional guarantees and shall not bear relevant responsibilities. THE SDK IS PROVIDED "AS IS" AND WE MAKE NO WARRANTY OR REPRESENTATION TO YOU WITH RESPECT TO THE SDK. TO THE FULLEST EXTENT PERMITTED BY LAW, WE SHALL NOT BE LIABLE TO YOU FOR USE OF THE SDK.

5. **YOUR ACCESS TO AND USE OF OUR SERVICES**

You must not (except where such prohibition is not allowed under applicable law) without our express written consent:

* access or use any of our Services if you are not fully able and legally competent to agree to these Terms;
* make unauthorized copies, modify, adapt, translate, reverse engineer, disassemble, decompile or create any derivative works of any of our Services or any content therein, including any files, tables or documentation (or any portion thereof) or determine or attempt to determine any source code, algorithms, methods or techniques embodied by any of our Services or any derivative works thereof;
* rent, lease, loan, assign, distribute, license, transfer, or sell, in whole or in part, any of our Services, or any derivative works thereof;
* use any of our Services for any unauthorized purpose, including: (i) communicating or facilitating any commercial advertisement or solicitation or spamming; and/or (ii) market, rent or lease any of our Services for a fee or charge. However, use of our Services for the purpose of developing or optimizing your own commercial software or services is an authorized purpose unless otherwise conflicts with the Terms.
* interfere with or attempt to interfere with the proper working of our Services, disrupt any aspect of our Services, website or any networks connected to our Services, or bypass any measures we may use to prevent or restrict access to our Services;
* incorporate our Services or any portion thereof into any other program or product. In such case, we shall have the right to refuse to provide any of our Services, terminate account(s) or limit access to our Services in our sole and absolute discretion;
* attempt to probe, scan, test the vulnerability of or gain unauthorized access to a system or network or to breach or circumvent security or authentication measures without proper authorization;
* use automated scripts to collect information from or otherwise interact with our Services;
* mask or alter the geographical location from which you appear to our systems to be accessing and/or using any of our Services, or use IP proxying or other methods to disguise the place of your residence;
* use or attempt to use an account, service or system without authorization from us;
* use our Services in a manner that may create a conflict of interest or undermine the purposes of our Services, such as trading reviews with other users or writing or soliciting fake reviews;
* use any of our Services in a way that could damage, disable, overburden, impair or compromise our Services or interfere with another person's usage or access to any of our Services; 
* use our Services to upload, transmit, distribute, store, communicate, portray or otherwise make available in any way any content that we have removed and/or suspended;
* use our Services in connection with gaming or advertising activity that qualifies as gambling or advertising that is not authorised by applicable law (including without limitation the Gambling Control Act 2022 of Singapore);
* use our Services to upload, generate and distribute or otherwise make available any false, misleading, defamatory, abusive or bad-faith content ;
* take any action that may undermine and/or abuse the rating or review systems on the PICO Store and/or any of our Services, including, without limitation, manipulating downloads, ratings or reviews by using bots, scripts or any other automated process, by providing or accepting any compensation or incentive, or by any other means; 
* use our Services to upload, post, transmit, distribute, store, communicate, portray or otherwise make available in any way: (i) viruses, trojans, worms, logic bombs or other material that is malicious or technologically harmful; (ii) any unsolicited or unauthorized advertising, solicitations, promotional materials, "junk mail", "spam", "chain letters", "pyramid schemes", or any other prohibited form(s) of solicitation; (iii) any private information or personal data of or about any individual, including for example addresses, phone numbers, email addresses, number and feature in the personal identity document (e.g., national insurance numbers, passport numbers, etc.) or credit card numbers, including without limitation any information or picture that may not be published or broadcasted under applicable laws (including without limitation laws relating to the protection of minors); (iv) any material which does or may infringe any copyright, trade mark or other intellectual property or privacy rights or moral rights of any other person; (v) any material which is defamatory of any person, obscene, offensive, pornographic, hateful or inflammatory or harmful; (vi) any material that would constitute, encourage or provide instructions for a criminal offence, dangerous activity, suicide, or self-harm, including without limitation detailed instructions on methods of crime or killings; (vii) any material that is designed to provoke or antagonize people, especially trolling and bullying, or is intended to or may intimidate, threaten, abuse, harass, harm, hurt, scare, distress, embarrass or upset people; (viii) any material that contains a threat of any kind, including threats of physical violence; (ix) any material that is racist or discriminatory, including discrimination on the basis of someone's nationality, race, religion, age, gender, disability or sexuality; (x) any answers, responses, comments, opinions, analyses, recommendations, or any other content that you are not properly licensed or otherwise qualified to provide; (xi) nudity; (xii) sexual violence or sexual activity; (xiii) incest, paedophilia, bestiality and/or necrophilia; (xiv) detailed or relished acts of violence or cruelty, physical abuse of, or acts of torture or other infliction of serious physical harm; (xv) glorification, incitement, endorsement of ethic, racial or religious hatred, strife or intolerance, or any matter of race or religion that is likely to cause feelings of enmity, hatred, ill will or hostility against, or contempt for or ridicule of, different racial or religious groups; (xvi) conduct which is an offence under applicable laws relating to gambling; (xvii) solicitation of prostitution or for any other immoral activity; (xviii) flashing lights and certain types of regular visual patterns that may cause problems for some viewers suffering from photosensitive epilepsy or other related conditions; (xix) depictions of potentially dangerous imitable behaviour; (xx) promotion of drug or psychoactive substance abuse, or detailed and instructive depictions of the same; (xxi) conduct that obstructs or is likely to obstruct any public health measure or is likely to result in a public health risk; (xxii) advocacy of or instruction on terrorism; (xxiii) any content in breach of such policies, standards and/or guidelines in connection with our Services as may be notified to you from time to time; and/or (xxiv) any material that, in the sole judgment of PICO, (1) is objectionable or which restricts or inhibits any other person from using our Services, or (2) may expose PICO, our Services or our users to any harm or liability of any type; and/or
* use our Services for any illegal or unlawful purposes or in any manner which violates any applicable law.

In addition to the above, your access to and use of the Services must, at all times, be compliant with our [Community Guidelines](https://www.picoxr.com/global/legal/community-guide). 
You acknowledge and agree that you may also be subject to additional terms and conditions prescribed by Third Party Providers (as defined below) in connection with such functionalities, as may be notified to you from time to time. You shall solely be responsible for checking your obligations under such additional terms (if any) and your compliance with such additional terms and conditions.
We may from time to time, without giving any prior reason or notice, upgrade, modify, alter, suspend, discontinue the provision of, or remove, whether in whole in part, any of our Services and/or PICO Content (as defined below), and/or any functionality provided therein, and to the maximum extent permitted by applicable law, we shall not thereby be liable to you or any third party. 
We reserve the right, at any time and without prior notice, to permanently or temporarily remove or suspend access to our Services if in our sole opinion your use of our Services violates or potentially violates these Terms or our [Community Guidelines](https://www.picoxr.com/global/legal/community-guide), third party rights (including intellectual property rights), applicable laws or regulations or is otherwise harmful to our Services, our users or third parties. 

6. **PERSONAL DATA AND SECURITY **

All data collection and processing via our Services only takes place locally in your device, and must be initiated by your own command. We do not upload any data to our server in our Services. You hereby agree that you are the sole controller of all data collected via our Services. As the App will collect and process camera, microphone and/or spatial data, which may include your personal data and the personal data of other individuals in your surroundings, for the purpose of providing the Services and recording such data as initiated by you, please refrain from using the App in a public location, and confirm that you have obtained the consent of surrounding individuals prior to any recording.
 By accessing any of our Services, you acknowledge and agree that you are at or above the legal age of majority in your jurisdiction and have read, understood and accepted these Terms. If you do not accept these Terms, you must not use any of our Services. If you are under the legal age of majority in your jurisdiction, you must have your parent or legal guardian's consent to and accept these Terms.
By continuing to access or use our Services after any updates to these Terms, you shall be deemed to have read, understood and accepted such updates.
We do not guarantee that our Services will be secure or free from bugs or viruses. You are solely responsible for configuring your device(s), information technology, computer programme(s) and platform(s) to access our Services. It is your responsibility to use an appropriate virus protection software. We cannot guarantee any transmissions made on or through the Internet by you will be secure or confidential. 
You acknowledge and agree that: (a) any content or information you submit or transmit via the Internet may not be protected by encryption, and may be vulnerable to interception during transmission; and (b) if you choose to use any public features available on our Services, any data provided therein may become publicly accessible.

7. **INTELLECTUAL PROPERTY AND CONTENT RIGHTS**

PICO Content
As between you and PICO, all content, materials, software, hardware, firmware code, algorithms, images, artworks, animations, models, text, graphics, illustrations, logos, patents, trade marks, service marks, copyrights, photographs, audio, videos, music on, and "look and feel" of our Services, and all intellectual property rights related thereto (the "**PICO Content**"), are either owned by or licensed to PICO, it being understood that you or your licensors will own the User Content (as defined below) that you upload or transmit through our Services unless such content is already owned by or licensed to us. Use of the PICO Content for any purpose not expressly permitted by these Terms is strictly prohibited. PICO Content may not be copied, reproduced, distributed, transmitted, broadcast, displayed, performed, adapted, edited, published, sold, licensed, reverse-engineered, decompiled, disassembled or otherwise exploited for any purpose whatsoever without our or, where applicable, our licensors', prior written consent. We and our licensors reserve all rights not expressly granted to you in and to PICO Content. Nothing in these Terms confers on you any rights to use or otherwise exploit "PICO" and any other trademarks, service marks, logos, get-up, trade names, goodwill, internet domain names, slogans, product names and designations and other proprietary indicia used as part of any of our Services, all of which are and remain the property of PICO or the relevant owner(s).
You acknowledge and agree that when you view content available on our Services, you are doing so at your own risk. We make no representations, warranties or guarantees, whether express or implied, that any PICO Content and/or User Content is/are accurate, complete or up to date. You acknowledge that we have no obligation to pre-screen, monitor, review, or edit any content transmitted or uploaded by you and other users on our Services (including PICO Content and/or User Content). The content on our Services is provided for general information only. It is not intended to amount to advice on which you should rely. You must obtain professional or specialist advice before taking, or refraining from, any action on the basis of the content on our Services. Where our Services contain links to other sites and resources provided by third parties, these links are provided for your information only. We have no control over the contents of those sites or resources. Such links should not be interpreted as approval by us of those linked websites or information you may obtain from them.
User Content
Users of our Services may be permitted to extract or transmit or otherwise make available content through our Services including, without limitation, any text, photographs, user videos, artworks, animations, model, sound recordings and the musical works embodied therein, comments, reviews, and ratings ("**User Content**"). The information and materials in the User Content have not been verified or approved by us. The views expressed by other users on our Services do not represent our views or values.
While our Services does not provide any feature to allow you upload or transmit User Content, you may still extract your user content via other offline approaches. If you then choose to upload or transmit your User Content on sites or platforms hosted by third parties, you must comply with their content guidelines as well as with the standards set out at "*Your Access to and Use of Our Services*" above, and any other policies, standards and/or guidelines as may be notified to you from time to time. You warrant that any such upload, transmission, and/or contact complies with those standards, and you shall be liable to us and fully indemnify us for any breach of that warranty -- this means you shall be fully responsible for any loss or damage we suffer as a result of your breach of this warranty.
When you create and extract any User Content from our Services, you agree and represent that you own that User Content, or that you have received all necessary permissions, clearances from, or are authorized by, the owner of any part of such User Content to use such User Content for all purposes contemplated under these Terms. You must not expose us or other users to any intellectual property or other claims relating to User Content that you create in our Service and use for any purpose. 
Despite the above, we do not represent or warrant the accuracy, integrity, appropriateness, quality of any User Content, nor that the User Content does not infringe intellectual property rights, and under no circumstances shall we be liable in any way for any User Content (including for the avoidance of doubt any third party materials incorporated in User Content). We shall have no liability in respect of any User Content published by you or by third parties.
Feedback
If you choose to contribute by sending us any ideas for products, services, features, modifications, enhancements, content, refinements, technologies, content offerings (such as audio, visual, games, or other types of content), promotions, strategies, or product/feature names, or any related documentation, artwork, computer code, diagrams, or other materials (collectively "**Feedback**"), then regardless of what your accompanying communication may say, the following terms will apply, so that future misunderstandings can be avoided. Accordingly, by sending Feedback to us, you agree that:

* PICO has no obligation to review, consider, or implement your Feedback, or to return to you all or part of any Feedback for any reason;
* Feedback is provided on a non-confidential basis, and we are not under any obligation to keep any Feedback you send confidential or to refrain from using or disclosing it in any way; and
* you irrevocably grant us perpetual and unlimited permission to reproduce, distribute, create derivative works of, modify, publicly perform (including on a through-to-the-audience basis), communicate to the public, make available, publicly display, and otherwise use and exploit the Feedback and derivatives thereof for any purpose and without restriction, free of charge and without attribution of any kind, including by making, using, selling, offering for sale, importing, and promoting commercial products and services that incorporate or embody Feedback, whether in whole or in part, and whether as provided or as modified.

8. **EXCLUSION OF WARRANTIES**

NOTHING IN THESE TERMS SHALL AFFECT ANY RIGHTS THAT YOU CANNOT CONTRACTUALLY AGREE TO ALTER OR WAIVE AS A CONSUMER UNDER APPLICABLE LAWS.
OUR SERVICES ARE PROVIDED "AS IS" AND WE MAKE NO WARRANTY OR REPRESENTATION TO YOU WITH RESPECT TO THEM. IN PARTICULAR WE DO NOT REPRESENT OR WARRANT TO YOU THAT:

* ANY OF OUR SERVICES WILL MEET YOUR REQUIREMENTS;
* ANY OF OUR SERVICES WILL BE UNINTERRUPTED, TIMELY, SECURE OR FREE FROM ERROR; 
* ANY INFORMATION OBTAINED BY YOU AS A RESULT OF OUR SERVICES WILL BE ACCURATE OR RELIABLE; AND/OR
* DEFECTS IN THE OPERATION OR FUNCTIONALITY OF ANY SOFTWARE PROVIDED TO YOU AS PART OF OUR SERVICES WILL BE CORRECTED.

OUR SERVICES MAY BE SUBJECT TO LIMITATIONS, DELAYS AND OTHER PROBLEMS INHERENT IN THE USE OF SUCH COMMUNICATIONS FACILITIES.
WE HEREBY EXPRESSLY DISCLAIM ALL WARRANTIES, WHETHER EXPRESS, STATUTORY OR IMPLIED, ORAL OR IN WRITING, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF NON-INFRINGEMENT OF THIRD PARTY RIGHTS, TITLE, SATISFACTORY QUALITY, ACCURACY, ADEQUACY, COMPLETENESS, TIMELINESS, MERCHANTABILITY, CURRENCY, RELIABILITY, PERFORMANCE, SECURITY, FITNESS FOR A PARTICULAR PURPOSE, CONFORMANCE WITH DESCRIPTION, CONTINUED AVAILABILITY, OR INTER-OPERABILITY WITH OTHER SYSTEMS OR SERVICES, AND NO SUCH WARRANTY OR REPRESENTATION IS GIVEN IN CONJUNCTION WITH OUR SERVICES, PICO CONTENT, USER CONTENT, AND/OR THIRD PARTY ELEMENTS. WE MAY CHANGE, SUSPEND, WITHDRAW OR RESTRICT THE AVAILABILITY OF ALL OR ANY PART OF OUR SERVICES FOR BUSINESS AND OPERATIONAL REASONS AT ANY TIME WITHOUT NOTICE.

9. **LIMITATION OF LIABILITY**

NOTHING IN THESE TERMS SHALL EXCLUDE OR LIMIT OUR LIABILITY FOR LOSSES WHICH MAY NOT BE LAWFULLY EXCLUDED OR LIMITED UNDER APPLICABLE LAWS, SUCH AS LIABILITY FOR DEATH OR PERSONAL INJURY RESULTING FROM NEGLIGENCE.
TO THE FULLEST EXTENT PERMITTED BY LAW, WE SHALL NOT BE LIABLE TO YOU FOR:

* ANY (i) LOSS OF BUSINESS; (ii) LOSS OF GOODWILL; (iii) BUSINESS REPUTATION; (iv) BUSINESS INTERRUPTION; (v) LOSS OF PROFIT (WHETHER INCURRED DIRECTLY OR INDIRECTLY); (vi) LOSS OF OPPORTUNITY; (vii) LOSS OF DATA SUFFERED BY YOU; AND/OR (viii) INDIRECT OR CONSEQUENTIAL LOSSES WHICH MAY BE INCURRED BY YOU; AND/OR
* ANY LOSS OR DAMAGE WHICH MAY BE INCURRED BY YOU AS A RESULT OF:
   1. ANY RELIANCE PLACED BY YOU ON THE COMPLETENESS, ACCURACY OR EXISTENCE OF ANY ADVERTISING, OR AS A RESULT OF ANY RELATIONSHIP OR TRANSACTION BETWEEN YOU AND ANY ADVERTISER OR SPONSOR WHOSE ADVERTISING APPEARS ON OR IN CONNECTION WITH OUR SERVICES;
   2. ANY CHANGES WHICH WE MAY MAKE TO OUR SERVICES, OR FOR ANY PERMANENT OR TEMPORARY CESSATION IN THE PROVISION OF OUR SERVICES (OR ANY FEATURES WITHIN OUR SERVICES);
   3. THE DELETION OF, CORRUPTION OF, OR FAILURE TO STORE, ANY CONTENT AND OTHER COMMUNICATIONS DATA MAINTAINED OR TRANSMITTED OR UPLOADED BY OR THROUGH YOUR USE OF OUR SERVICES;
   4. YOUR FAILURE TO PROVIDE US WITH ACCURATE ACCOUNT INFORMATION; AND/OR
   5. YOUR FAILURE TO KEEP YOUR PASSWORD OR ACCOUNT DETAILS SECURE AND CONFIDENTIAL.

IF DEFECTIVE DIGITAL CONTENT THAT WE HAVE SUPPLIED DAMAGES A DEVICE OR DIGITAL CONTENT BELONGING TO YOU AND THIS IS CAUSED SOLELY BY OUR FAILURE TO USE REASONABLE CARE AND SKILL, WE MAY DECIDE IN OUR SOLE AND ABSOLUTE DISCRETION TO EITHER REPAIR THE DAMAGE OR PAY YOU COMPENSATION. HOWEVER, WE SHALL NOT IN ANY EVENT BE LIABLE FOR DAMAGE THAT YOU COULD HAVE AVOIDED BY FOLLOWING OUR ADVICE TO APPLY AN UPDATE OFFERED TO YOU FREE OF CHARGE OR FOR DAMAGE THAT WAS CAUSED BY YOU FAILING TO CORRECTLY FOLLOW INSTALLATION INSTRUCTIONS OR TO HAVE IN PLACE THE MINIMUM SYSTEM REQUIREMENTS ADVISED BY US OR FOR DAMAGE THAT ARISES IN CONNECTION WITH YOUR BREACH OF ANY OF THESE TERMS.
THESE LIMITATIONS ON OUR LIABILITY TO YOU SHALL APPLY WHETHER OR NOT WE HAVE BEEN ADVISED OF OR SHOULD HAVE BEEN AWARE OF THE POSSIBILITY OF ANY SUCH LOSSES ARISING.
YOU ARE RESPONSIBLE FOR ANY MOBILE CHARGES THAT MAY APPLY TO YOUR USE OF OUR SERVICES, INCLUDING TEXT-MESSAGING AND DATA CHARGES. IF YOU ARE UNSURE WHAT THOSE CHARGES MAY BE, IT IS YOUR RESPONSIBILITY TO ASK YOUR SERVICE PROVIDER BEFORE USING OUR SERVICES.
TO THE FULLEST EXTENT PERMITTED BY LAW, ANY DISPUTE YOU HAVE WITH ANY THIRD PARTY ARISING OUT OF YOUR USE OF OUR SERVICES, INCLUDING, BY WAY OF EXAMPLE AND NOT LIMITATION, ANY CARRIER, INTELLECTUAL PROPERTY RIGHT OWNER OR OTHER USER, IS DIRECTLY BETWEEN YOU AND SUCH THIRD PARTY, AND YOU IRREVOCABLY RELEASE US AND OUR AFFILIATES FROM ANY AND ALL CLAIMS, DEMANDS AND DAMAGES (ACTUAL AND CONSEQUENTIAL) OF EVERY KIND AND NATURE, KNOWN AND UNKNOWN, ARISING OUT OF OR IN ANY WAY CONNECTED WITH SUCH DISPUTES.
TO THE EXTENT NOT EXCLUDED AND/OR TO THE EXTENT NOT LAWFULLY EXCLUDED, PICO'S MAXIMUM AGGREGATE LIABILITY FOR ALL CLAIMS, SUITS, DEMANDS, ACTIONS OR OTHER LEGAL PROCEEDINGS IN CONNECTION WITH THESE TERMS, WHETHER BASED ON AN ACTION OR CLAIM IN CONTRACT, NEGLIGENCE, TORT, OR OTHERWISE, SHALL NOT EXCEED SGD 1,000. 

10. **INDEMNITY**

You agree to defend, indemnify, and hold harmless PICO, its parents, subsidiaries, and affiliates, and each of their respective officers, directors, employees, agents and advisors from any and all claims, liabilities, costs, and expenses, including, but not limited to, attorneys' fees and expenses, arising out of a breach by you or any user of your account under these Terms or arising out of a breach of your obligations, representation and warranties under these Terms, including without limitation in connection with User Content.

11. **OTHER TERMS**

**Applicable Law and Jurisdiction.** These Terms, their subject matter and their formation, are governed by the laws of Singapore. Any dispute arising out of or in connection with these Terms, including any question regarding existence, validity or termination of these Terms, shall be referred to and finally resolved by arbitration administered by the Singapore International Arbitration Centre ("**SIAC**") in accordance with the Arbitration Rules of the Singapore International Arbitration Centre ("**SIAC Rules**") for the time being in force, which rules are deemed to be incorporated by reference in this clause. The seat of the arbitration shall be Singapore. The Tribunal shall consist of one (1) arbitrator. The language of the arbitration shall be English.
**Language.** These Terms are prepared in English and may be translated into multiple languages other than English. In the event of inconsistency between the English language text and any translation, to the maximum extent permitted under applicable laws, the English version shall prevail. 
**Open Source.** Aspects of our Services may contain open source software. Each item of open source software is subject to its own applicable license terms, which can be found at PICO Open Source Notice.
**Entire Agreement.** These Terms, and the documents referred to herein, embodies the entire agreement and understanding between the you and us relating to the subject matter of these Terms, and supersedes all prior agreements and understandings relating to our Services.
**No Waiver.** Our failure to insist upon or enforce any provision of these Terms shall not be construed as a waiver of any provision or right.
**Severability.** If any court of law, having jurisdiction to decide on this matter, rules that any provision of these Terms is illegal or invalid, then that provision will be removed from the Terms without affecting the rest of the Terms, and the remaining provisions of the Terms shall continue to be valid and enforceable.
**Third Party Rights.** A person who is not a party to these Terms has no right under the Contracts (Rights of Third Parties) Act 2001 to enforce any of these Terms.
*If you find inappropriate content that violates these Terms or have any other concerns or questions you would like to raise, contact us at* [support.global@picoxr.com](mailto:support.global@picoxr.com)*.*


# --- END: SpatialMLCapture Terms of Service.md ---



# --- BEGIN: SpatialMLCapture.md ---

SpatialMLCapture App is an application designed specifically for PICO devices, aimed at helping users and developers easily record MultiModal Machine Learning data containing rich spatial information. This data includes synchronized stereo RGB images, depth information, and real-time pose (position and orientation) of the device, and is stored uniformly as SpatialMP4 format files.
This application mainly serves developers, researchers who need high-quality spatial data, and users interested in spatial computing and robotics technology. It can be used in various scenarios such as Machine Learning Model Training, robot navigation, scene understanding, and algorithm debugging.
## Requirements

* PICO device models: PICO 4 Ultra series
* PICO device's system version: 5.14.0 or later (For specific version requirements, please refer to the official PICO release information or app store instructions)

## Key features

* **Spatial Data Recording**: Real-time recording of stereoscopic RGB images of the surrounding environment of the device, depth maps, and Six Degrees of Freedom (6DoF) pose data of the device.
* **Synchronous storage**: Synchronize all sensor data in time and encapsulate it into a single SpatialMP4 file for convenient subsequent processing and analysis.
* **Data Export**: Support exporting recorded SpatialMP4 files from PICO devices for offline analysis or Model Training on other platforms.

## Use cases

* **Machine Learning and AI Modeling Training**:
   * Train and optimize models for XR applications such as gesture recognition, scene understanding, object detection.
   * Development of robot navigation and autonomous obstacle avoidance algorithms.
* **Robot technology research**:
   * Collect interaction data from First-Person Perspective for training embodied agents.
   * Enhance the understanding and interaction ability of robots in three-dimensional space.
* **Algorithm development and debugging**:
   Quickly generate video files containing RGB and pose for debugging algorithms such as visual odometry (VIO), SLAM, or image stabilization, without the need for complex multi-module data capture and alignment processes.

## Use SpatialMLCapture
### Prerequisites
Before launching the SpatialMLCapture app, make sure that Video Seethrough is already enabled; otherwise, the app will exit automatically.
### Get the app
Go to the PICO Store on your PICO headset, search for SpatialMLCapture, and install it.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49eae53228fb434894eccc9adf069776~tplv-goo7wpa0wc-image.image" width="100px" />

### Launch the app
Find the SpatialMLCapture App icon on your PICO device and click to launch it.
### Record

1. Prepare to record:
   * Ensure that the equipment is fully charged.
   * Select an environment with suitable lighting conditions for recording to ensure image and depth data quality.
   * Before recording begins, it is recommended to make small movements in the environment to help the system better initialize and track poses.
   * The first time you run the app, you need to confirm the legal notice and allow the app to obtain camera, audio, and spatial data permissions. Otherwise, the app will automatically exit.
2. Start recording:
   * On the main interface of the App, use the controller trigger or press the "Volume +" button to start recording spatial data.
   * During the recording process, please try to keep the device stable and avoid violent shaking to obtain more accurate posture and sensor data.
3. Stop recording:
   * After completing the recording, use the handle trigger again or press the "Volume +" button to end the recording.
   * The app will automatically process the data and save it as a SpatialMP4 file (with the file extension .mp4).

### Manage and export recordings

* View files:
   * Connect your PICO device to your computer.
   * The default save path is /sdcard/Movies/SpatialMP4/xxxx.mp4 , which can be viewed through the adb command:
      ```Bash
      adb shell ls /sdcard/Movies/SpatialMP4
      ```

* Export files:
   Use adb to copy the .mp4 (SpatialMP4) file that needs to be analyzed on your desktop computer or other storage device.
   ```Bash
   # Replace xxxx with existing filename.
   adb pull /sdcard/Movies/SpatialMP4/3DVideo_xxxx.mp4
   ```

## About the recorded data
The files generated by SpatialMLCapture App are in the SpatialMP4 format. This is an extended format based on standard MP4 containers, specifically designed for storing MultiModal Machine Learning data required for spatial computing.
### Data content
A SpatialMP4 file typically contains the following data streams:

* **Stereoscopic RGB video**: a sequence of color images of the left and right eyes.
* **Depth data**: a sequence of depth images synchronized with RGB images, using timestamps for soft synchronization.
* **Posture data**: Real-time Six Degrees of Freedom Posture (Translation and Rotation) of the head of the device during recording.
* **Camera parameters**: including internal and external parameters of RGB cameras and depth cameras, used for data parsing and 3D reconstruction.
* **Audio data**: (based on actual support) includes audio recorded synchronously. The parsing tool does not support parsing for the time being, but it may be supported in future versions.

### Data parsing 
To parse and work with data in SpatialMP4 files, we recommend using the accompanying SpatialMP4 C++/Python SDK (https://github.com/Pico-Developer/SpatialMP4). The SDK provides convenient APIs to read and process various data streams.
Main functions of SDK (refer to SpatialMP4 SDK documentation):

* Read RGB images, depth maps, and pose data.
* Obtain camera internal and external parameters.
* Support multiple data reading modes (such as RGB-only, Depth-only, Depth-first).
* Supports random access to frames.

```C++
#include "spatialmp4/reader.h"
#include "spatialmp4/data_types.h"

// Create reader
SpatialML::Reader reader("path/to/your/spatial_video.mp4");

// Check data type
if (reader.HasRGB()) { /* ... */ }
if (reader.HasDepth()) { /* ... */ }
if (reader.HasPose()) { /* ... */ }

// Load data frame
while (reader.HasNext()) {
    SpatialML::rgb_frame rgb_frame_data;
    SpatialML::depth_frame depth_frame_data;
    reader.Load(rgb_frame_data, depth_frame_data);
    // Process rgb_frame_data.left_rgb, depth_frame_data.depth 
    ...
}
```

```Python
# WIP
from spatialmp4 import Reader
reader = Reader("path/to/your/spatial_video.mp4")
```

Quickly parse and visualize the spatial mp4 files you recorded:

1. Build FFmpeg and the test executable file `test_reader` according to the description in the README of the repository at https://github.com/Pico-Developer/SpatialMP4
2. Place the file you recorded in `SpatialMP4/video/test.mp4` (refer to https://github.com/Pico-Developer/SpatialMP4/tree/main/video), and ensure the file name is `test.mp4`.
3. Run the test: `./build/test_reader`.
4. The visualization results are saved in `tmp_vis_*`. 

For more detailed usage and API references of the SpatialMP4 SDK, please refer to its official documentation (https://github.com/Pico-Developer/SpatialMP4 README in the repository).
## FAQs

* Q: Is there a limit to the duration of a single recording?
   A: The recording duration is mainly limited by device storage space and battery life. It is recommended to record longer scenes in segments according to actual needs.
* Q: How much space will the recorded SpatialMP4 file take up?
   A: The file size depends on the recording duration, resolution, and data complexity. Videos with depth and high frame rate RGB are usually larger.
* Q: How to ensure the quality of recorded data?
   A: Try to record in a well-lit and even environment; avoid camera obstruction or blurry lenses; move the device smoothly during the recording process.
* Q: Where can I find more detailed SpatialMP4 format instructions or SDK documentation?
   A: Please refer to the documentation in the official code repository (https://github.com/Pico-Developer/SpatialMP4) of the SpatialMP4 SDK, such as README.md.

## Support and feedback

* For SpatialMP4 SDK related questions, you can submit issues in its code repository (https://github.com/Pico-Developer/SpatialMP4).
* For issues with the DataCapture App itself, please contact the PICO App Store's feedback channel or PICO Developer Support.


# --- END: SpatialMLCapture.md ---



# --- BEGIN: Speech-to-text.md ---

The speech-to-text service uses the automatic speech recognition (ASR) technology to support real-time recognition of speech and conversion into text. You can convert Chinese or English audio of up to 60 seconds into text in real time.
## Details
| **Aspect** | **Description** |
| --- | --- |
| Supported languages | Chinese, English. |
| Capabilities | Speech recognition, automatic punctuating (optional). |
| Response time | Real-time, provide text while speaking. |
| Audio input format | Mono channel. |
| Time limit | Maximum of 60 seconds for each speech recognition process. |
## Prerequisite
The version of SDK should be 2.3.0 or later.
## Procudure
### Flowchart
Implement the speech-to-text service in your app through the following flow.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIzNzNweCIgaGVpZ2h0PSI3NjVweCIgdmlld0JveD0iLTAuNSAtMC41IDM3MyA3NjUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDE1NyAxMTIgTCAxNTcgOTguMzciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNTcgOTMuMTIgTCAxNjAuNSAxMDAuMTIgTCAxNTcgOTguMzcgTCAxNTMuNSAxMDAuMTIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDE1NyAxNTIgTCAxNTcgMTg1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTU3IDE5MC44OCBMIDE1My41IDE4My44OCBMIDE1NyAxODUuNjMgTCAxNjAuNSAxODMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSI5MiIgd2lkdGg9IjMxMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+PGRpdj5DYWxswqA8Y29kZT48Zm9udCBmYWNlPSJIZWx2ZXRpY2EiPlNwZWVjaFNlcnZpY2UuSW5pdEFzckVuZ2luZTwvZm9udD48L2NvZGU+wqB0byBpbml0aWFsaXplIHRoZSBBU1IgZW5naW5lPC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDE1NyAzNTIgTCAxNTcgMzg1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTU3IDM5MC44OCBMIDE1My41IDM4My44OCBMIDE1NyAzODUuNjMgTCAxNjAuNSAzODMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyOTIiIHdpZHRoPSIzMTAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDMwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMyMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+Q2FsbMKgPGNvZGU+PGZvbnQgZmFjZT0iSGVsdmV0aWNhIj5TcGVlY2hTZXJ2aWNlLlN0YXJ0QXNyPC9mb250PjwvY29kZT7CoHRvIHN0YXJ0IHRoZSBzcGVlY2gtdG8tdGV4dCBwcm9jZXNzPC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PGVsbGlwc2UgY3g9IjE1NyIgY3k9IjczNyIgcng9IjU1IiByeT0iMjUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDczN3B4OyBtYXJnaW4tbGVmdDogMTAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkVuZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxNTcgNDUyIEwgMTU3IDQ4MC42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE1NyA0ODUuODggTCAxNTMuNSA0NzguODggTCAxNTcgNDgwLjYzIEwgMTYwLjUgNDc4Ljg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMzkyIiB3aWR0aD0iMzEwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0MjJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PjxkaXY+PGRpdj5DYWxswqA8Y29kZT48Zm9udCBmYWNlPSJIZWx2ZXRpY2EiPlNwZWVjaFNlcnZpY2UuU3RvcEFzcjwvZm9udD48L2NvZGU+wqB0byBzdG9wIHRoZSBzcGVlY2gtdG8tdGV4dCBwcm9jZXNzPC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjwvZGl2PjwvZGl2PjxzcGFuPjwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTU3IDI1MiBMIDE1NyAyODUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNTcgMjkwLjg4IEwgMTUzLjUgMjgzLjg4IEwgMTU3IDI4NS42MyBMIDE2MC41IDI4My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjE5MiIgd2lkdGg9IjMxMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjIycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+PGRpdj5SZWdpc3RlciBjYWxsYmFjayBmdW5jdGlvbnPCoDxjb2RlPjxmb250IGZhY2U9IkhlbHZldGljYSI+U3BlZWNoU2VydmljZS5TZXRPbkFzclJlc3VsdENhbGxiYWNrPC9mb250PjwvY29kZT7CoGFuZDwvZGl2PjxkaXY+wqA8Y29kZT48Zm9udCBmYWNlPSJIZWx2ZXRpY2EiPlNwZWVjaFNlcnZpY2UuU2V0T25TcGVlY2hFcnJvckNhbGxiYWNrPC9mb250PjwvY29kZT48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTU3IDY3MiBMIDE1NyA3MDUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNTcgNzEwLjg4IEwgMTUzLjUgNzAzLjg4IEwgMTU3IDcwNS42MyBMIDE2MC41IDcwMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjQ5MiIgd2lkdGg9IjMxMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTIycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+PGRpdj5HZXQgdGhlIHJlc3VsdCB0aGUgY2FsbGJhY2sgZnVuY3Rpb25zPC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDE1NyA1MiBMIDE1NyA4NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE1NyA5MC44OCBMIDE1My41IDgzLjg4IEwgMTU3IDg1LjYzIEwgMTYwLjUgODMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZWxsaXBzZSBjeD0iMTU3IiBjeT0iMjciIHJ4PSI1NSIgcnk9IjI1IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyN3B4OyBtYXJnaW4tbGVmdDogMTAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlN0YXJ0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDIzMiA2MzIgTCAzNjIgNjMyIEwgMzYyIDMyMiBMIDMxOC4zNyAzMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzMTMuMTIgMzIyIEwgMzIwLjEyIDMxOC41IEwgMzE4LjM3IDMyMiBMIDMyMC4xMiAzMjUuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMTU3IDU5MiBMIDIzMiA2MzIgTCAxNTcgNjcyIEwgODIgNjMyIFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNjMycHg7IG1hcmdpbi1sZWZ0OiA4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Db250dW51ZSB1c2luZyB0aGUgYXBwPzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxNTcgNTUyIEwgMTU3IDU4NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE1NyA1OTAuODggTCAxNTMuNSA1ODMuODggTCAxNTcgNTg1LjYzIEwgMTYwLjUgNTgzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTUyIiB5PSI2ODIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDY5MnB4OyBtYXJnaW4tbGVmdDogMTcycHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+Tm88L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI3MiIgeT0iNjExIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA2MjFweDsgbWFyZ2luLWxlZnQ6IDI5MnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPlllczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxGraphModel&quot;:{&quot;dx&quot;:&quot;782&quot;,&quot;dy&quot;:&quot;466&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;tooltips&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;arrows&quot;:&quot;1&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;pageHeight&quot;:&quot;1169&quot;},&quot;mxCellMap&quot;:{&quot;Xfazc13W&quot;:{&quot;id&quot;:&quot;Xfazc13W&quot;},&quot;Pect1uf9&quot;:{&quot;id&quot;:&quot;Pect1uf9&quot;,&quot;parent&quot;:&quot;Xfazc13W&quot;},&quot;bRjlDSjK&quot;:{&quot;id&quot;:&quot;bRjlDSjK&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0.5;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;target&quot;:&quot;YGVClKwk&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;265&quot;,&quot;y&quot;:&quot;360&quot;,&quot;as&quot;:&quot;sourcePoint&quot;}}},&quot;SOw2Wwm0&quot;:{&quot;id&quot;:&quot;SOw2Wwm0&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;YGVClKwk&quot;,&quot;target&quot;:&quot;j4d3BF17&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;YGVClKwk&quot;:{&quot;id&quot;:&quot;YGVClKwk&quot;,&quot;value&quot;:&quot;Call <code><font face=\&quot;Helvetica\&quot;>SpeechService.InitAsrEngine</font></code> to initialize the ASR engine&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;110&quot;,&quot;y&quot;:&quot;340&quot;,&quot;width&quot;:&quot;310&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;DankLkLK&quot;:{&quot;id&quot;:&quot;DankLkLK&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;gHLA2FBg&quot;,&quot;target&quot;:&quot;dGvdYX8h&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;gHLA2FBg&quot;:{&quot;id&quot;:&quot;gHLA2FBg&quot;,&quot;value&quot;:&quot;Call <code><font face=\&quot;Helvetica\&quot;>SpeechService.StartAsr</font></code> to start the speech-to-text process&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;110&quot;,&quot;y&quot;:&quot;540&quot;,&quot;width&quot;:&quot;310&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;DxwOrE85&quot;:{&quot;id&quot;:&quot;DxwOrE85&quot;,&quot;value&quot;:&quot;End&quot;,&quot;style&quot;:&quot;ellipse;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;oval&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;210&quot;,&quot;y&quot;:&quot;960&quot;,&quot;width&quot;:&quot;110&quot;,&quot;height&quot;:&quot;50&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;h1xYMFhv&quot;:{&quot;id&quot;:&quot;h1xYMFhv&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;dGvdYX8h&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;265&quot;,&quot;y&quot;:&quot;735&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;dGvdYX8h&quot;:{&quot;id&quot;:&quot;dGvdYX8h&quot;,&quot;value&quot;:&quot;Call <code><font face=\&quot;Helvetica\&quot;>SpeechService.StopAsr</font></code> to stop the speech-to-text process&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;110&quot;,&quot;y&quot;:&quot;640&quot;,&quot;width&quot;:&quot;310&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;YZQ5q7m0&quot;:{&quot;id&quot;:&quot;YZQ5q7m0&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;j4d3BF17&quot;,&quot;target&quot;:&quot;gHLA2FBg&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;j4d3BF17&quot;:{&quot;id&quot;:&quot;j4d3BF17&quot;,&quot;value&quot;:&quot;Register callback functions <code><font face=\&quot;Helvetica\&quot;>SpeechService.SetOnAsrResultCallback</font></code> and <code><font face=\&quot;Helvetica\&quot;>SpeechService.SetOnSpeechErrorCallback</font></code>&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;110&quot;,&quot;y&quot;:&quot;440&quot;,&quot;width&quot;:&quot;310&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;w0Fmx8OE&quot;:{&quot;id&quot;:&quot;w0Fmx8OE&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;DgmjzCjn&quot;,&quot;target&quot;:&quot;DxwOrE85&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;1wbsLSo3&quot;:{&quot;id&quot;:&quot;1wbsLSo3&quot;,&quot;value&quot;:&quot;Get the result the callback functions&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;110&quot;,&quot;y&quot;:&quot;740&quot;,&quot;width&quot;:&quot;310&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;YYV4DHdx&quot;:{&quot;id&quot;:&quot;YYV4DHdx&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;n8RFtp9V&quot;,&quot;target&quot;:&quot;YGVClKwk&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;n8RFtp9V&quot;:{&quot;id&quot;:&quot;n8RFtp9V&quot;,&quot;value&quot;:&quot;Start&quot;,&quot;style&quot;:&quot;ellipse;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;oval&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;210&quot;,&quot;y&quot;:&quot;250&quot;,&quot;width&quot;:&quot;110&quot;,&quot;height&quot;:&quot;50&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;KmTgF37b&quot;:{&quot;id&quot;:&quot;KmTgF37b&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;DgmjzCjn&quot;,&quot;target&quot;:&quot;gHLA2FBg&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;60&quot;,&quot;y&quot;:&quot;930&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;390&quot;,&quot;y&quot;:&quot;600&quot;,&quot;as&quot;:&quot;targetPoint&quot;},&quot;-2-Array&quot;:{&quot;as&quot;:&quot;points&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;470&quot;,&quot;y&quot;:&quot;880&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;470&quot;,&quot;y&quot;:&quot;570&quot;}}}},&quot;DgmjzCjn&quot;:{&quot;id&quot;:&quot;DgmjzCjn&quot;,&quot;value&quot;:&quot;Contunue using the app?&quot;,&quot;style&quot;:&quot;rhombus;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;diagramName&quot;:&quot;Diamond&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;190&quot;,&quot;y&quot;:&quot;840&quot;,&quot;width&quot;:&quot;150&quot;,&quot;height&quot;:&quot;80&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;YoAlrWoA&quot;:{&quot;id&quot;:&quot;YoAlrWoA&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;source&quot;:&quot;1wbsLSo3&quot;,&quot;target&quot;:&quot;DgmjzCjn&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;265&quot;,&quot;y&quot;:&quot;800&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;265&quot;,&quot;y&quot;:&quot;900&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;tNl2oLOq&quot;:{&quot;id&quot;:&quot;tNl2oLOq&quot;,&quot;value&quot;:&quot;No&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;260&quot;,&quot;y&quot;:&quot;930&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;shMOnS8R&quot;:{&quot;id&quot;:&quot;shMOnS8R&quot;,&quot;value&quot;:&quot;Yes&quot;,&quot;style&quot;:&quot;text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;&quot;,&quot;parent&quot;:&quot;Pect1uf9&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;380&quot;,&quot;y&quot;:&quot;859&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}}},&quot;mxCellList&quot;:[&quot;Xfazc13W&quot;,&quot;Pect1uf9&quot;,&quot;bRjlDSjK&quot;,&quot;SOw2Wwm0&quot;,&quot;YGVClKwk&quot;,&quot;DankLkLK&quot;,&quot;gHLA2FBg&quot;,&quot;DxwOrE85&quot;,&quot;h1xYMFhv&quot;,&quot;dGvdYX8h&quot;,&quot;YZQ5q7m0&quot;,&quot;j4d3BF17&quot;,&quot;w0Fmx8OE&quot;,&quot;1wbsLSo3&quot;,&quot;YYV4DHdx&quot;,&quot;n8RFtp9V&quot;,&quot;KmTgF37b&quot;,&quot;DgmjzCjn&quot;,&quot;YoAlrWoA&quot;,&quot;tNl2oLOq&quot;,&quot;shMOnS8R&quot;]},&quot;lastEditTime&quot;:0,&quot;snapshot&quot;:&quot;&quot;}" />

### Step 1: Complete general setups
Refer to the "[Platform services overview](/en_platform-services-overview)" article to complete general setups, including registering on the PICO Developer Platform, importing the SDK, completing project settings in the Unity Editor, initializing platform services, and more.
### Step 2: Call speech-to-text service APIs
Call APIs in the following order to integrate the speech-to-text service into your app.

1. Call `SpeechService.InitAsrEngine` to initialize the ASR engine.
2. Register callback functions `SpeechService.SetOnAsrResultCallback` and `SpeechService.SetOnSpeechErrorCallback` for the result, including the text and error information.
3. Call `SpeechService.StartAsr` to start the speech-to-text process.
4. Call `SpeechService.StopAsr` to stop the speech-to-text process.
5. Get the result information from the callback functions.

## Demo
The SpeechToTextDemo demonstrates the features of the speech-to-text service, including initializing the ASR engine, starting/stopping speech recognition, and more. For more information on the demo, refer to the "[Speech-to-text demo](/en_speech-to-text-demo)" article.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e20145d77d047eeb5d86e70de0ac280~tplv-goo7wpa0wc-image.image" width="550px" />

## API reference
The following table lists speech-to-text service functions. For details on parameters, returns, and more, refer to the [API reference](/reference/unity/client-api/SpeechService/).
| **Function** | **Description** |
| --- | --- |
| `SpeechService.InitAsrEngine` | Initialize the ASR engine. |
| `SpeechService.StartAsr` | Start converting speech to text. |
| `SpeechService.StopAsr` | Stop converting speech to text. |
| `SpeechService.SetOnAsrResultCallback` | Callback function which returns the speech-to-text result. |
| `SpeechService.SetOnSpeechErrorCallback` | Callback function which returns error information. |
## Error handling
| **Error Code** | **Description** |
| --- | --- |
| -1 ~ -9  | SDK internal errors, such as failing to create instances. |
| -100 ~ -103 | Internal network error. |
| -200 ~ -202 | Internal address error. |
| -402 | Failed to start  audio recording: no permission to record audio or audio recording is already occupied. |
| -700 | Audio recording is already occupied. |
| -601 -605  | Internal ASR engine error. |
| -900 ~ -903  | Internal command composition error。 |
| -1000 | Internal ASR engine status error. You can call `StopAsr` to reset ASR engine's status. |
| -1100 / -1101  | Internal authentication failure. |
| 1001 ~ 1099  | Internal service error. |
| 1013  | Invalid audio. |
| 1014  | Waiting audio timeout. |
| 1015  | The audio input is too long. |
| 1022 | Service processing exception. |
| 4001 | Receiving data timeout. |
| 4003  | Internal network error. |
| 4020 ~ 4022 | Internal signal library exception. |
| 4040 ~ 4042 | Internal exception in awakening the ASR engine. |
| 4050 ~ 4052 | Player exception. |
| 5000  | External error. |


# --- END: Speech-to-text.md ---



# --- BEGIN: Splash Screen.md ---

After a user clicks on an app icon, the PICO system requires some time to initialize the rendering system and the XR system before launching the app. Since version 2.1.5, the SDK has reduced the initialization time and supports adding an image as the app's splash screen (i.e., the screen before the appearance of the Unity log and the "MADE WITH Unity" text ). You can set up the splash screen in the Unity Editor.
## Expected effect
In the following video, the screen before the appearance of the unity-logo-attached screen is the app's splash screen.
<video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4265c5b6c4a14678a5e79d6261c5d67f~tplv-goo7wpa0wc-image.image></video>
## Use cases

* **Reduce the duration of the initialization loading screen**
   For a good user experience, the initialization loading screen of your app should last no more than 5 seconds. To determine the app's initialization duration, close all background apps and launch the target app. If the app takes longer than 5 seconds to initialize, consider adding a splash screen for a better user experience.
* **Promote app ideas**
   You can design relevant materials on the splash screen based on the app's theme to create a memorable impression on users.
* **Increase brand awareness**
   You can add developer information on the splash screen to increase brand awareness.

## Requirements

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series
* PICO device's system version: 5.5.0 or later

## Set up a splash screen for your app

1. Open an existing scene or create a new scene in the Unity Editor.
2. Go to **Edit** > **Project Settings** > **XR Plug-in Management** > **PICO**.
3. Select an image as the **System Splash Screen**.
   * The image format must be PNG, and its size should not exceed 1024 x 1024 pixels.
   * Semi-transparent effects are not supported.

   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe502a7e564f4d1f83d320eadf8987c8~tplv-goo7wpa0wc-image.image)


# --- END: Splash Screen.md ---



# --- BEGIN: Subscription.md ---

For regulatory reasons, games without gaming licenses issued by authorities in Mainland China are unable to access IAP service. This does not affect developers elsewhere.

Subscriptions provide a recurring payment model that allows users to purchase the premium content in your app. PICO provides auto-renewable subscriptions. After integrating the Subscriptions service into your app, the order fulfillment and deduction processes are automatically done by the PICO system.
Subscription service is an important part of the IAP service. Currently, you can create durable, consumable, and subscription add-ons for your app. Subscription add-ons have their own subscription periods, for example, monthly/annual membership, so users can only use subscription add-ons within the subscription periods that they purchase.
## Important notes
We recommend reading the following notes before using subscriptions in your app.
| **For Developers** | **For Users** |
| --- | --- |
| * Currently, the total number of in-review and published subscription add-ons should be no more than 20. <br> * You can create subscription add-ons with subscription periods of 1 month, 3 months, and 1 year. <br> * For in-review or approved add-ons, you cannot edit their existing prices, subscription periods, or trial periods, but can add new subscription periods to them. <br> * You can add new subscription periods to approved subscription add-ons, or edit approved subscription add-ons' descriptions, images and videos, and content rating by form of draft. <br> * Approved add-ons cannot be removed. If you want to remove an approved add-on, please contact the PICO team. <br> * It is recommended to create different subscription periods with the same interest under the same subscription add-on. <br> * Different official subscription periods under the same subscription add-on have the same trial period. In other words, you can only set one trial period for one subscription add-on. <br> * You can create subscription add-ons for unpublished apps. <br> * DLC files cannot be associated with subscription add-ons. | * Currently, subscriptions cannot be refunded. <br> * The first-time purchase of a subscription add-on can only be done in the app. <br> * Users can view subscription information, and renew or unsubscribe subscription add-ons in the PICO Store or PICO VR Assistance. <br> * Below are the auto-deduction rules for subscription renewal： <br>    * For monthly, quarterly, and annual subscriptions, payments are automatically deducted on a cycle of 30, 90, and 365 days respectively. <br>    * When there are 3 minutes remaining before the current subscription period expires, the system tries to deduct the fee for the next subscription period for the first time. <br>    * If the first try fails, there will be a 5-minute grace period. During the remaining validity period plus the grace period, the system tries to deduct the fee for a second time. <br>    * If the second try fails, the subscription will expire after the grace period is over. <br> * The deduction results are sent to users via SMS (for Mainland China users) or email (for non-Mainland China users). <br> * Users will not be charged any subscription fees during the trial period. Once the trial period ends, users will be charged subscription fees if they still subscribe to the premium content. However, if users cancel their subscriptions during the trial period, the official subscription will not start once the trial period ends, and users do not need to pay any fee. <br> * If multiple accounts share the same PICO device, only the account that purchases the subscription add-on can enjoy relevant benefits. <br> * Users can renew subscriptions anytime within the grace period: <br>    * If the automatic renewal deduction fails during the subscription period due to insufficient balance, we will provide a grace period outside of the subscription period for the user. The grace period is 24 hours. <br>    * Within the grace period, users that want a renewal should make a payment in the PICO Store or the PICO VR Assistant; otherwise, the subscription will expire when the grace period ends. |
## Key features
### Supported subscription models
You can create the following subscription models:

* Model 1: One subscription add-on with only one subscription period.
* Model 2: One subscription add-on with multiple subscription periods.

In addition to SKUs that identify add-ons, we have introduced OuterIDs to identify subscription periods. Each subscription add-on corresponds to one unique SKU, and each subscription period corresponds to one unique OuterID, as illustrated below:
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/20389e85848c49ecb3630d618c0ae19b~tplv-em5hxbkur4-noop.image?width=982&height=572" width="450px" />

### Get purchasable add-ons
After creating add-ons for your app, you can call `GetProductsBySKU` to display them to users. For purchasable subscription add-ons, the `AddonsType` field returns `Subscription`.
```C#
Request<ProductList> GetProductsBySKU(string[] skus)
```

### Launch the checkout flow
You can call `LaunchCheckoutFlow2()` to allow users to launch the checkout flow to purchase an add-on. The price for the purchased add-on should be passed in the request. You can call `GetProductsBySKU` to get the price.
```C#
Request<Purchase> LaunchCheckoutFlow2(Product product)
```

### Get purchased add-ons
After the purchase flow is complete, you can call `GetViewerPurchases` to display the list of purchased add-ons including durables, unfulfilled consumables, and effective subscriptions.
```C#
Request<PurchaseList> GetViewerPurchases()
```

### Get an add-on's subscription status
You can call  `GetSubscriptionStatus` to get the subscription status of a subscription add-on for the user.
## Implementation workflow
### Complete basic setups
Refer to the "[Platform services overview](/en_platform-services-overview#712343ad)" article to complete basic setups.
### Create subscription add-ons
You can create subscription add-ons on the PICO Developer Platform and set parameters such as the trial period, official subscription period, price, description, and SKU. You can create one or multiple subscription periods for one subscription add-on. Below are the steps to follow:

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/organization/).
   This directs you to the **My Apps** screen.
2. Click the card of the target app to enter its **Overview** screen.
3. From the left navigation bar, select **Monetization** > **Subscription**.
   You will enter the **Subscription** configuration page.
4. In the upper right corner of the page, click the **Add** button.
5. In the **Create Add-on** window, configure Add-on parameters, including: **Name**, **SKU**, **Genres**, **Published In**, **Price (Other Regions)**, and **Trial Period**. Specifically, **Type** needs to be set to **Subscription**.
   Subscriptions are only available for developers outside Mainland China.

5. In the **Create Add-On** window, configure the new add-on by setting the name, SKU, genre, published country/region, price, subscription period, and trial period.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/36b174f3d5fd4cf29b6aa978e2266f58~tplv-em5hxbkur4-noop.image?width=1325&height=1026)
6. Click the **Create** button.
   The newly created subscription add-on is displayed in the list.
7. In the list, click the name of the subscription add-on.
   This directs you to the following subscription add-on editing page.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/fbb5d4361f4e42efbdf86177b5f513e4~tplv-em5hxbkur4-noop.image?width=1990&height=1086)
8. Follow the on-screen instructions to edit the add-on.
9. In the upper-right corner, click the **Submit** button.
   This add-on will enter the review session.

### Implement APIs
You can implement subscription APIs in your app. Below is the API implementation workflow. For code sample, refer to the [IAPDemo.cs](https://github.com/Pico-Developer/PlatformSample-Unity/blob/main/Assets/Samples/IAP/IAPDemo.cs) file.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3ODVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgNzg1IDY1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSA1ODUgMzIgTCA2MDUgMzIgTCA1OTIgMzIgTCA2MDUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2MTAuODggMzIgTCA2MDMuODggMzUuNSBMIDYwNS42MyAzMiBMIDYwMy44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNDA1IiB5PSIyIiB3aWR0aD0iMTgwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogNDA2cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxzcGFuIHN0eWxlPSJmb250LXZhcmlhbnQtbGlnYXR1cmVzOm5vLWNvbW1vbi1saWdhdHVyZXMiPkxhdW5jaCB0aGUgc3Vic2NyaXB0aW9uIGFkZC1vbiBwdXJjaGFzZSBmbG93Ojwvc3Bhbj48YnIgc3R5bGU9Im1hcmdpbjowcHg7cGFkZGluZzowcHg7LXdlYmtpdC1mb250LXNtb290aGluZzphbnRpYWxpYXNlZDtmb250LXZhcmlhbnQtbGlnYXR1cmVzOm5vLWNvbW1vbi1saWdhdHVyZXMiIC8+PHNwYW4gc3R5bGU9Im1hcmdpbjowcHg7cGFkZGluZzowcHg7LXdlYmtpdC1mb250LXNtb290aGluZzphbnRpYWxpYXNlZDtmb250LXNpemU6MTEuOXB4O2NvbG9yOnJnYig3MSwgMTAxLCAxMzApO2ZvbnQtZmFtaWx5OnNvdXJjZS1jb2RlLXBybywgTWVubG8sIE1vbmFjbywgQ29uc29sYXMsICZxdW90O0NvdXJpZXIgTmV3JnF1b3Q7LCBtb25vc3BhY2U7dGV4dC1hbGlnbjpzdGFydDtiYWNrZ3JvdW5kLWNvbG9yOnJnYmEoMjcsIDMxLCAzNSwgMC4wNSkiPkxhdW5jaENoZWNrb3V0RmxvdzIoKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzczIDMyIEwgMzkzIDMyIEwgMzg1IDMyIEwgMzk4LjYzIDMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDAzLjg4IDMyIEwgMzk2Ljg4IDM1LjUgTCAzOTguNjMgMzIgTCAzOTYuODggMjguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIxNSIgeT0iMiIgd2lkdGg9IjE1OCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU2cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDIxNnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5GaWx0ZXIgc3Vic2NyaXB0aW9uIGFkZC1vbnM8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjYxMiIgeT0iMiIgd2lkdGg9IjE3MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDYxM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48c3BhbiBzdHlsZT0iY29sb3I6cmdiKDAsIDAsIDApO2ZvbnQtZmFtaWx5OkhlbHZldGljYTtmb250LXNpemU6MTJweDtmb250LXN0eWxlOm5vcm1hbDtmb250LXZhcmlhbnQtbGlnYXR1cmVzOm5vLWNvbW1vbi1saWdhdHVyZXM7Zm9udC12YXJpYW50LWNhcHM6bm9ybWFsO2ZvbnQtd2VpZ2h0OjQwMDtsZXR0ZXItc3BhY2luZzpub3JtYWw7b3JwaGFuczoyO3RleHQtYWxpZ246Y2VudGVyO3RleHQtaW5kZW50OjBweDt0ZXh0LXRyYW5zZm9ybTpub25lO3dpZG93czoyO3dvcmQtc3BhY2luZzowcHg7LXdlYmtpdC10ZXh0LXN0cm9rZS13aWR0aDowcHg7YmFja2dyb3VuZC1jb2xvcjpyZ2IoMjQ4LCAyNDksIDI1MCk7dGV4dC1kZWNvcmF0aW9uLXRoaWNrbmVzczppbml0aWFsO3RleHQtZGVjb3JhdGlvbi1zdHlsZTppbml0aWFsO3RleHQtZGVjb3JhdGlvbi1jb2xvcjppbml0aWFsO2Zsb2F0Om5vbmU7ZGlzcGxheTppbmxpbmUgIWltcG9ydGFudCI+RGlzcGxheSBlZmZlY3RpdmUgc3Vic2NyaXB0aW9uIGFkZC1vbnM6PC9zcGFuPjxiciBzdHlsZT0iYm94LXNpemluZzpjb250ZW50LWJveDttYXJnaW46MHB4O3BhZGRpbmc6MHB4Oy13ZWJraXQtZm9udC1zbW9vdGhpbmc6YW50aWFsaWFzZWQ7Y29sb3I6cmdiKDAsIDAsIDApO2ZvbnQtZmFtaWx5OkhlbHZldGljYTtmb250LXNpemU6MTJweDtmb250LXN0eWxlOm5vcm1hbDtmb250LXZhcmlhbnQtbGlnYXR1cmVzOm5vLWNvbW1vbi1saWdhdHVyZXM7Zm9udC12YXJpYW50LWNhcHM6bm9ybWFsO2ZvbnQtd2VpZ2h0OjQwMDtsZXR0ZXItc3BhY2luZzpub3JtYWw7b3JwaGFuczoyO3RleHQtYWxpZ246Y2VudGVyO3RleHQtaW5kZW50OjBweDt0ZXh0LXRyYW5zZm9ybTpub25lO3dpZG93czoyO3dvcmQtc3BhY2luZzowcHg7LXdlYmtpdC10ZXh0LXN0cm9rZS13aWR0aDowcHg7YmFja2dyb3VuZC1jb2xvcjpyZ2IoMjQ4LCAyNDksIDI1MCk7dGV4dC1kZWNvcmF0aW9uLXRoaWNrbmVzczppbml0aWFsO3RleHQtZGVjb3JhdGlvbi1zdHlsZTppbml0aWFsO3RleHQtZGVjb3JhdGlvbi1jb2xvcjppbml0aWFsIiAvPjxzcGFuIHN0eWxlPSJib3gtc2l6aW5nOmNvbnRlbnQtYm94O21hcmdpbjowcHg7cGFkZGluZzowcHg7LXdlYmtpdC1mb250LXNtb290aGluZzphbnRpYWxpYXNlZDtmb250LXNpemU6MTEuOXB4O2ZvbnQtc3R5bGU6bm9ybWFsO2ZvbnQtdmFyaWFudC1jYXBzOm5vcm1hbDtmb250LXdlaWdodDo0MDA7bGV0dGVyLXNwYWNpbmc6bm9ybWFsO29ycGhhbnM6Mjt0ZXh0LWluZGVudDowcHg7dGV4dC10cmFuc2Zvcm06bm9uZTt3aWRvd3M6Mjt3b3JkLXNwYWNpbmc6MHB4Oy13ZWJraXQtdGV4dC1zdHJva2Utd2lkdGg6MHB4O3RleHQtZGVjb3JhdGlvbi10aGlja25lc3M6aW5pdGlhbDt0ZXh0LWRlY29yYXRpb24tc3R5bGU6aW5pdGlhbDt0ZXh0LWRlY29yYXRpb24tY29sb3I6aW5pdGlhbDtjb2xvcjpyZ2IoNzEsIDEwMSwgMTMwKTtmb250LWZhbWlseTpzb3VyY2UtY29kZS1wcm8sIE1lbmxvLCBNb25hY28sIENvbnNvbGFzLCAmcXVvdDtDb3VyaWVyIE5ldyZxdW90OywgbW9ub3NwYWNlO2ZvbnQtdmFyaWFudC1saWdhdHVyZXM6bm9ybWFsO3RleHQtYWxpZ246c3RhcnQ7YmFja2dyb3VuZC1jb2xvcjpyZ2JhKDI3LCAzMSwgMzUsIDAuMDUpIj5HZXRWaWV3UHVyY2hhc2VzKCk8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDE4MiAzMiBMIDIwMiAzMiBMIDE5NSAzMiBMIDIwOC42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIxMy44OCAzMiBMIDIwNi44OCAzNS41IEwgMjA4LjYzIDMyIEwgMjA2Ljg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iMTgwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EaXNwbGF5IGEgbGlzdCBvZiBwdXJjaGFzYWJsZSBhZGQtb25zOjxiciAvPjxzcGFuIHN0eWxlPSJjb2xvcjpyZ2IoNzEsIDEwMSwgMTMwKTtmb250LWZhbWlseTpzb3VyY2UtY29kZS1wcm8sIE1lbmxvLCBNb25hY28sIENvbnNvbGFzLCAmcXVvdDtDb3VyaWVyIE5ldyZxdW90OywgbW9ub3NwYWNlO2ZvbnQtc2l6ZToxMS45cHg7dGV4dC1hbGlnbjpzdGFydDtiYWNrZ3JvdW5kLWNvbG9yOnJnYmEoMjcsIDMxLCAzNSwgMC4wNSkiPkdldFByb2R1Y3RzQnlTS1UoKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxGraphModel&quot;:{&quot;dx&quot;:&quot;1038&quot;,&quot;dy&quot;:&quot;645&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;tooltips&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;arrows&quot;:&quot;1&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;pageHeight&quot;:&quot;1169&quot;},&quot;mxCellMap&quot;:{&quot;hGed7mIv&quot;:{&quot;id&quot;:&quot;hGed7mIv&quot;},&quot;F3pqduvV&quot;:{&quot;id&quot;:&quot;F3pqduvV&quot;,&quot;parent&quot;:&quot;hGed7mIv&quot;},&quot;UW7rvZye&quot;:{&quot;id&quot;:&quot;UW7rvZye&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;F3pqduvV&quot;,&quot;source&quot;:&quot;pwo1dv5A&quot;,&quot;target&quot;:&quot;gHJoYp9z&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;pwo1dv5A&quot;:{&quot;id&quot;:&quot;pwo1dv5A&quot;,&quot;value&quot;:&quot;Launch the subscription add-on purchase flow:<br style=\&quot;margin:0px;padding:0px;-webkit-font-smoothing:antialiased;font-variant-ligatures:no-common-ligatures\&quot; />LaunchCheckoutFlow2()&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;F3pqduvV&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;443&quot;,&quot;y&quot;:&quot;310&quot;,&quot;width&quot;:&quot;180&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;5A0lzV8N&quot;:{&quot;id&quot;:&quot;5A0lzV8N&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;F3pqduvV&quot;,&quot;source&quot;:&quot;LSWzz2iY&quot;,&quot;target&quot;:&quot;pwo1dv5A&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;LSWzz2iY&quot;:{&quot;id&quot;:&quot;LSWzz2iY&quot;,&quot;value&quot;:&quot;Filter subscription add-ons&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;F3pqduvV&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;253&quot;,&quot;y&quot;:&quot;310&quot;,&quot;width&quot;:&quot;158&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;gHJoYp9z&quot;:{&quot;id&quot;:&quot;gHJoYp9z&quot;,&quot;value&quot;:&quot;Display effective subscription add-ons:<br style=\&quot;box-sizing:content-box;margin:0px;padding:0px;-webkit-font-smoothing:antialiased;color:rgb(0, 0, 0);font-family:Helvetica;font-size:12px;font-style:normal;font-variant-ligatures:no-common-ligatures;font-variant-caps:normal;font-weight:400;letter-spacing:normal;orphans:2;text-align:center;text-indent:0px;text-transform:none;widows:2;word-spacing:0px;-webkit-text-stroke-width:0px;background-color:rgb(248, 249, 250);text-decoration-thickness:initial;text-decoration-style:initial;text-decoration-color:initial\&quot; />GetViewPurchases()&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;F3pqduvV&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;650&quot;,&quot;y&quot;:&quot;310&quot;,&quot;width&quot;:&quot;170&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;9neN7Anc&quot;:{&quot;id&quot;:&quot;9neN7Anc&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;F3pqduvV&quot;,&quot;source&quot;:&quot;KeSERZ8G&quot;,&quot;target&quot;:&quot;LSWzz2iY&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;KeSERZ8G&quot;:{&quot;id&quot;:&quot;KeSERZ8G&quot;,&quot;value&quot;:&quot;Display a list of purchasable add-ons:<br />GetProductsBySKU()&quot;,&quot;style&quot;:&quot;rounded=0;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;F3pqduvV&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;Rectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;310&quot;,&quot;width&quot;:&quot;180&quot;,&quot;height&quot;:&quot;60&quot;,&quot;as&quot;:&quot;geometry&quot;}}},&quot;mxCellList&quot;:[&quot;hGed7mIv&quot;,&quot;F3pqduvV&quot;,&quot;UW7rvZye&quot;,&quot;pwo1dv5A&quot;,&quot;5A0lzV8N&quot;,&quot;LSWzz2iY&quot;,&quot;gHJoYp9z&quot;,&quot;9neN7Anc&quot;,&quot;KeSERZ8G&quot;]},&quot;lastEditTime&quot;:0,&quot;snapshot&quot;:&quot;&quot;}" />

## Create non-renewing subscriptions

1. Create a "Consumable" add-on on the PICO Developer Platform. See [here](/en_in-app-purchase#Create%20an%20add-on) for the steps.
2. Define a desired validity period for the add-on.
3. Call `IAPService.ConsumePurchase` to consume the add-on.
   Once the add-on is consumed, users can purchase it again immediately.

## Test a subscription add-on
You can use testing subscription add-ons to try and test the overall workflow of Subscription service. Once a subscription add-on is created, the platform automatically generates a testing version for it. You can use the developer account that creates the official subscription add-on to call `GetProductsBySKU()` to retrieve the testing subscription add-on and purchase it. Based on the subscription period and trial period you create for an official subscription add-on, there will be corresponding testing versions for these periods as illustrated in the following table.
The payment period is shorter for testing subscription add-ons. For example, if an official subscription add-on requires a payment every month, its testing version requires a payment every 10 minutes. Grace period is also provided in tasting subscription add-ons. Testing and official subscription add-ons share the same auto-deduction rules for renewal, refer to the "Important notes" part above for details. For more information on add-on testing, check out [this article](/13136/en_in-app-purchase).
|  | **Official Subscription Add-on** | **Testing Subscription Add-on** |
| --- | --- | --- |
| Subscription period | 1 month | 10 minutes |
|  | 3 months | 20 minutes |
|  | 1 year | 30 minutes |
| Trial period | 7 days | 7 minutes |
|  | 14 days | 14 minutes |
|  | 30 days | 30 minutes |
|  | 365 days | 365 minutes |
## Subscription presence & management
In the PICO Store or the PICO VR Assistant app, users can view the purchasable subscriptions in apps or manage their subscriptions including renewal and unsubscription.
### In the PICO Store
Subscription service is only supported by PICO Store 3.5.5 or later.

In the PICO Store, when users activate subscriptions within the app, a payment window appears. If your app offers a 7-day free trial, users can view the actual charge date.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c33a6d449f40447bad7efcd5f40a658b~tplv-goo7wpa0wc-image.image)
Users can go to an app's details pane to view the app's subscribable add-ons.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/2a9371f0dee945778ad400fc687c78da~tplv-em5hxbkur4-noop.image?width=1542&height=733)
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/1a19a5ddb4144b34b8b3b956280c0825~tplv-em5hxbkur4-noop.image?width=1546&height=735)
Users can view their subscriptions by clicking the **My Apps icon** > **Subscriptions**.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c08c2cd5bc41475f9cb552bfce032f9f~tplv-em5hxbkur4-noop.image?width=1535&height=729)
By clicking a subscribed add-on, users can view its details, renew or cancel subscriptions.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7562e42b5534c2eb6fbf4470e2b0c46~tplv-goo7wpa0wc-image.image)
By clicking an add-on that is in trial, users can view its trial end time, payment methods and subscription plan.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/1ab255c889f64cbdaaafb0d026fde05a~tplv-em5hxbkur4-noop.image?width=1526&height=725)
### In the PICO VR Assistant
Subscription service is only supported by PICO VR Assistant 1.1.4 or later.

In the PICO VR Assistant app, users can go to an app's details pane to view the app's subcription add-ons.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/7646b341756c48cfba6dbdf9d674aa07~tplv-em5hxbkur4-noop.image?width=1816&height=1198)
Users can go to **Menu** > **Subscriptions** to view purchased subscriptions and renew/cancel subscriptions as needed.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/5d026d422a024efcb037f175073f6e66~tplv-em5hxbkur4-noop.image?width=2385&height=1133)
## Demo
You can use the IAPDemo to try out the Subscription service. For more information, refer to the "[Subscription demo](/en_subscription-demo)" article.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/0481238196ae45ada3267d013ea0a527~tplv-em5hxbkur4-noop.image?width=1280&height=1280" width="546px" />

## API reference
To include Subscription service, we added new input parameters and returned data to IAP service APIs, and also added the `LaunchCheckoutFlow2` API which you can use to launch the flow for purchasing subscription add-ons. For details about in-app purchase APIs, refer to the [API reference](/reference/unity/client-api/IAPService/).


# --- END: Subscription.md ---



# --- BEGIN: Support for the Unity OpenXR Plugin.md ---

Starting from version 3.3.0, the PICO Unity Integration SDK will support the Unity OpenXR Plugin. After importing the PICO Unity Integration SDK into your project and enabling the Unity OpenXR Plugin, you can use the Unity OpenXR Plugin to integrate XR functionalities into your app.
## Enable the Unity OpenXR Plugin
Refer to the section titled "Enable the Unity OpenXR Plugin" in the "[Set up your Unity project](/complete-project-settings)" article for instructions.
## Changes and modifications
If you previously used the PICO Unity OpenXR SDK to integrate the following functionalities into your app, you will need to refer to the following changes and make corresponding modifications when using PICO Unity Integration SDK version 3.0.0 or later.
|  | **Before (PICO Unity OpenXR SDK 1.4.0 and earlier)** | **(PICO Unity Integration SDK 3.3.0 and later)** |
| --- | --- | --- |
| Screen fade | Add PICOScreenFade. | Add PXR_ScreenFade. |
| Display refresh rate | Obtain relevant information through the following two interfaces: <br>  <br> * (Deprecated)` TryGetSupportedDisplayRefreshRates`: Get all supported display refresh rates for the current device. <br> * (Deprecated) `GetDisplayRefreshRateCount`: Get the number of display refresh rates supported by the current device. | Use `GetDisplayFrequenciesAvailable` to directly obtain all display refresh rates supported by the current device. |
| Passthrough | To integrate the Passthrough Layer Feature, you need to add the PICO Manager (Script) component. | Not required. |
|  | `EnableSeeThroughManual` has been deprecated. | Use `EnableVideoSeeThrough`. |
| Composition layers | All interfaces have been deprecated. | Refer to [Composition layer-related articles](/compositor-layer-overview) for usage. |
| Namespaces for enums and structs | The relevant enums or structs are as follows: <br>  <br> * Content protection: `SecureContentFlag` <br> * Full-body motion capture: <br>    * `BodyJointSet` <br>    * `BodyTrackingData` <br>    * `BodyTrackingDataInfo` <br>    * `BodyTrackingBoneLength` <br> * Safe zone: `GeometryInstanceTransform` <br> * Passthrough: `PassThroughStyle` | The namespaces of the enums and structs mentioned in the left column have been changed to `pxr`,and the relevant code has been migrated to the PXR_Type.cs file. You need to update the namespaces. |
## Related articles
If you need to use the Unity OpenXR Plugin to develop apps, after importing PICO Unity Integration SDK version 3.3.0 or later into your project and enabling the Unity OpenXR Plugin, directly refer to [PICO Unity OpenXR SDK's documentation](https://developer-cn.picoxr.com/document/unity-openxr/) to integrate the desired features into your app.


# --- END: Support for the Unity OpenXR Plugin.md ---



# --- BEGIN: System Keyboard.md ---

With the in-app keyboard, users can effortlessly input text in a wide range of scenarios, including text chats and text-based information settings. The SDK provides the system keyboard, allowing you to easily incorporate it into your app.
## Expected effect
When clicking on the input field, the system keyboard appears.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa355d68134f49f18d8e79e18178a544~tplv-goo7wpa0wc-image.image" width="546px" />

## Important note
When the app displays the system keyboard, it loses the input focus.
## Before you begin

* Upgrade the XR Interaction Toolkit to version 2.1.0 or later and import the "Starter Assets" package into your project.
* Add the XR Origin to your scene and set up the controllers.

For detailed instructions, refer to the [Quickstart](/13136/en_create-an-xr-scene#782faf9d) guide.
## Set up the system keyboard
Use the following steps to enable the system keyboard for your app:

1. In the **Hierarchy** window, complete the following steps:
   1. Click **+** > **UI** > **Event System** to add the event system to the scene.
   2. Click **+** > **UI** > **Canvas** to add a canvas to the scene.
2. Select **Canvas**, and complete the following steps in the **Inspector** window: 
   1. Set the canvas's **Render Mode** to **World Space**.
   2. Set the canvas's **Event Camera** to the scene's main camera.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c06f0cb6645401ebb6f38031f1a5fb0~tplv-goo7wpa0wc-image.image)
   3. Add the **Tracked Device Graphic Raycast** script to the canvas.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/060f211d366849ba9c46c28bece84d54~tplv-goo7wpa0wc-image.image)
3. In the **Hierarchy** window, right-click **Canvas** and select **UI** > **Input Field - TextMeshPro** from the shortcut menu to add an input field to the scene.
4. Adjust the positions of the main camera and the canvas, making the input field shown in the scene (as illustrated below).
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75d6d4c3a86341d79a21b497ccd6df26~tplv-goo7wpa0wc-image.image)
5. Select the **Left Controller** and **Right Controller** objects under XR Origin, then set the **Max Raycast Distance** parameter (i,e., the maximum ray length) on the **XR Ray Interactor** component of the **Inspector** window to make the ray color turn white upon touching the input field, which indicates that the input field and ray can interact.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5640aadac33f485e9a9e46aebad9eee0~tplv-goo7wpa0wc-image.image)


# --- END: System Keyboard.md ---



# --- BEGIN: The number of APK files associated with a key exceeds the limit.md ---

Since device system version 5.11.0, a single key can be associated with a maximum of 50 APK files. APK files exceeding the limit will not be able to run on PICO devices. If this issue happens, you can follow the step below to set up a new key for your project.

1. Go to **Edit** > **Project Settings** > **Player** > **Publishing Settings**, check the **Custom Keystore** checkbox, and click the **Keystore Manager...** button.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5e517cb74dc444db0094e4f876a4442~tplv-goo7wpa0wc-image.image)
2. In the upper left of the **Keystore Manager** window, select **Keystore...** > **Create New** > **Anywhere...** and confirm the storage location of the new keystore in the pop-up window.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aaff2ef73fe14f03bd18db1db7ac262c~tplv-goo7wpa0wc-image.image)
3. In the **Keystore Manager** window, set a password for the new keystore and set an alias and a password for the new key. 
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d92625b946e4e7881db5ce306335753~tplv-goo7wpa0wc-image.image)
4. Click the **Add Key** button in the lower right of the window.
   The **Keystore and Key created** pop-up window appears.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f73f4e68076b445aaded23d76e004d9e~tplv-goo7wpa0wc-image.image)
5. Click the **Yes** button.
   The newly created keystore and key are then applied to your project.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f371cf9f81e41fa8e305944ebc87d46~tplv-goo7wpa0wc-image.image)


# --- END: The number of APK files associated with a key exceeds the limit.md ---



# --- BEGIN: The SpatialMP4 Whitepaper.md ---

Spatial video combines stereo RGB , depth , and pose data to enable immersive 3D experiences (e.g., AR/VR, robotics, 3D reconstruction). This document defines an MP4-based container format for synchronizing and storing these data streams efficiently.
## Key features

* Multiple data tracks: In addition to audio and video tracks, tracks such as stereo image depth and pose are provided to facilitate business-side applications.
* Synchronization: The image frame, depth map, and pose data tracks are all equipped with their respective timestamp base, which facilitates data synchronization by business parties based on this timebase.
* Compatibility: Supports the legacy stereo 3D side-by-side and MV-HEVC codec format.

## MP4 Container Extension
### Stereo RGB Track
The stereo RGB track is used to save the video stream from the left and right RGB cameras. This track is mandatory.
#### Basic

* Codec : AVC/HEVC/MV-HEVC
* Layout : Multi-Layer(MV-HEVC)/Side-by-side (left/right or top-bottom) 
* BitDepth：8/10 bit

#### VideoExtendedUsage Box (vexu)
This box is mandatory for delivery.
This box is proposed by Apple and consistent with the Apple spatial video format. We mainly focus on these newly added boxes. For others, please refer to Apple's white paper：
https://developer.apple.com/av-foundation/Stereo-Video-ISOBMFF-Extensions.pdf
| **FourCC** | **FourCC** | **FourCC** | **FourCC** | **Box syntax element** | **Description** |
| --- | --- | --- | --- | --- | --- |
| vexu |  |  |  | VideoExtendedUsageBox |  |
|  | eyes |  |  | Video Stereo  |  |
|  |  | stri |  | StereoViewInformationBox | 1: left, 2: right, 3: both |
|  |  | hero |  | HeroStereoEyeDescriptionBox | Main view id, 0: left as main, 1: right as main. |
|  |  | cams |  | CamerasBox |  |
|  |  |  | blin | BaselineBox <br>  | ipd:the distance from the optical center of the left-eye camera to the optical center of the right-eye camera. unit(um). e.g. 2cm ipd: 20000 |
|  |  | cmfy |  |  |  |
|  |  |  | dadj <br>  | DisparityAdjustmentBox <br>  | Disparity adjustment must be in the range [-1, 1]. A positive adjustment value of 0.02 (2%) is a common default. Multiply a number by 10000 and convert it to an integer. For example, 0.02 adjustment: 200. |
|  |  |  | dads | DisparityAdjustmentScaleBox | PICO added |
|  | proj |  |  | ProjectionBox | Projection description |
|  |  | prji |  | ProjectionInformationBox | The projection_kind shall only be ‘rect' |
|  | pack |  |  |  |  |
|  |  | pkin <br>  |  |  | If frame packing is used, view_packing_kind must be 'side' or ‘over', but 'side' is preferred. |
#### DisparityAdjustmentScaleBox(dads)
##### Definition
Box Type: `dads`
Container: `cmfy`
Mandatory: No 
Quantity: Zero or one
##### Syntax
```C++
aligned(8) class DisparityAdjustmentScale extends FullBox(‘dads’, 0, 0) {
    unsigned float(32) scale;
}
```

##### Semantics
| **Item** | **Description** |
| --- | --- |
| scale | - Identifies scale ratio for image. type: float32. |
#### IntrinsicCameraParametersBox (icam)
This box is optional, used for MR and ML developer scenarios.
This box specifies intrinsic camera parameters that link the pixel coordinates of an image point with the corresponding coordinates in the camera reference frame. A specification of focal length and parameters related to geometric distortion due to camera optics is given in Annex H of ISO/IEC 14496-10. For more details, refer to ISO/IEC 14496-15:2024: https://www.iso.org/standard/89118.html
##### Syntax
```C++
  class IntrinsicCameraParametersBox extends FullBox ('icam', version=0, flags) {
    unsigned int(6) reserved=0; 
    unsigned int(10) ref_view_id;
    unsigned int(32)prec_focal_length;
    unsigned int(32)prec_principal_point;
    unsigned int(32)prec_skew_factor;
    unsigned int(8)exponent_focal_length_x;
    signed   int(64)mantissa_focal_length_x;
    unsigned int(8)exponent_focal_length_y;
    signed   int(64)mantissa_focal_length_y; 
    unsigned int(8)exponent_principal_point_x;
    signed   int(64)mantissa_principal_point_x;
    unsigned int(8)exponent_principal_point_y;
    signed   int(64)mantissa_principal_point_y;
  }
```

##### Semantics
| **Item** | **Description** |
| --- | --- |
| ref_view_id | the view_id identifying a view for which intrinsic camera parameters are indicated in this Intrinsic Camera Parameters Box |
| prec_focal_length | reserved |
| prec_principal_point | reserved |
| prec_skew_factor | the exponent of the maximum allowable truncation error for skew factor as given by 2­prec_skew_factor. The value of prec_skew_factor shall be in the range of 0 to 31, inclusive. |
| exponent_focal_length_x <br>  |  the exponent part of the focal length in the horizontal direction. The value of exponent_focal_length_x shall be in the range of 0 to 62, inclusive. The value 63 is reserved for future use by ITUT \| ISO/IEC. Decoders shall treat the value 63 as indicating an unspecified focal length. <br> mantissa_focal_length_x specifies the mantissa part of the focal length of the i-th camera in the horizontal direction. |
| mantissa_focal_length_x |  the mantissa part of the focal length of the i-th camera in the horizontal direction. |
| exponent_focal_length_y | the exponent part of the focal length in the vertical direction. The value of exponent_focal_length_y shall be in the range of 0 to 62, inclusive. The value 63 is reserved for future use by ITUT \| ISO/IEC. Decoders shall treat the value 63 as indicating an unspecified focal length. |
| mantissa_focal_length_y | the mantissa part of the focal length in the vertical direction. |
| exponent_principal_point_x | the exponent part of the principal point in the horizontal direction. |
| mantissa_principal_point_x |  the mantissa part of the principal point in the horizontal direction. |
| exponent_principal_point_y |  the exponent part of the principal point in the vertical direction.  |
| mantissa_principal_point_y | the mantissa part of the principal point in the vertical direction |
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bb8eb6d3c3f45cb8123f5c50c6c096c~tplv-goo7wpa0wc-image.image)
#### ExtrinsicCameraParametersBox（ecam）
This box is optional, used for MR and ML developer scenarios.
This subclause specifies extrinsic camera parameters that define the location and orientation of the camera reference frame with respect to a known world reference frame. A specification of extrinsic camera parameters including translation vector and rotation matrix is given in Annex H of ISO/IEC 14496-10. For more details, refer to ISO/IEC 14496-15:2024: https://www.iso.org/standard/89118.html
##### Syntax
```C++
class ExtrinsicCameraParametersBox extends FullBox ('ecam', version=0, flags) {
    unsigned int(6) reserved=0;
    unsigned int(10) ref_view_id;
    unsigned int(8)prec_rotation_param;
    unsigned int(8)prec_translation_param;
    for (j=1; j<=3; j++) { /* row */
        for (k=1; k<=3; k++) { /* column */
              unsigned int(8)exponent_r[j][k];
              signed   int(64)mantissa_r [j][k];
        }
        unsigned int(8)exponent_t[j];
        signed   int(64)mantissa_t[j];
    }
}
```

##### Semantics
| **Item** | **Description** |
| --- | --- |
| ref_view_id <br>  | - Identifies the view ID (view_id) corresponding to the current camera parameters, which is consistent with the ref_view_id in the IntrinsicCameraParametersBox to ensure that the internal and external parameters are associated with the same view. |
| prec_rotation_param | - reserved |
| prec_translation_param | - reserved |
| exponent_r[j][k] | - The exponent part of the element in the j-th row and k-th column of the rotation matrix (\(j, k \in \{1, 2, 3\}\)). |
| mantissa_r[j][k] | - The mantissa part of the element in the j-th row and k-th column of the rotation matrix. |
| exponent_t[j] | - The exponent part of the j-th component (\(x, y, z\)) of the translation vector. |
| mantissa_t[j] | - The mantissa part of the j-th component of the translation vector. |

* Rotation matrix (R): Represents the rotation of the camera coordinate system relative to the world coordinate system. The matrix elements are calculated by combining the exponent and mantissa with the precision parameter to ensure the accurate representation of the rotation pose.
* Translation vector (T): Represents the position of the origin of the camera coordinate system in the world coordinate system. The components are calculated by the exponent and mantissa and, together with the rotation matrix, define the external parameters of the camera.

![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d36eed20ed749399ca070ee2f855313~tplv-goo7wpa0wc-image.image)
#### Horizontal Field Of View Box（hfov）
Refer to 3.2.4 Horizontal Field Of View Box. This box is mandatory for delivery.
### Depth Track
The depth track is used to store a depth map from the ToF sensor or the estimated depth from the left or right camera. This track is optional, used for MR and ML developer scenarios.
#### Basic

* Codec : video/raw (uncompress)
* Format：12/16bit mono-chrome

#### VideoRawSampleDescriptor（rawc）
##### Definition
Box Type: `rawc`
Container: `SampleTableBox` (‘stbl’)
Mandatory: Yes
Quantity: Exactly one
Defines a new uncompressed visual sample type "rawc". Its hierarchical level is within the "stbl" container box. Meanwhile, metadata boxes "hfov" and "vfox" are defined to show the horizontal and vertical fields of view of the depth map respectively. The metadata box "dfmt" is defined to show the depth map format.
##### Syntax
```C++
aligned(8) class VisualSampleEntry extends SampleEntry(‘rawc’, 0, 0) {
  //skip common element from parent
  ...
        Box(dfmt); 
        Box(hfov);
        Box(vfov);
}
```

#### Depth format Box (dfmt)
##### Definition
Box Type: `dfmt`
Container: `rawC`
Mandatory: Yes
Quantity: Exactly one
Define the metadata box of the depth map format ("dfmt"), which represents the specifications of the depth map video stream, including the data type of the depth map, the valid range of values, and the data precision. 
##### Syntax
```C++
aligned(8) class DepthFormatBox  extends Box(‘dfmt’) {
      int(32) data_type //int16, int8      
      int(32) valid_range 
      char(32) data_precision //mm,dm,cm
}
```

##### Semantics
dfmt box describes some parameters of the depth track.
| **Item** | **Description** |
| --- | --- |
| data_type <br>  | - Depth data types, refer to qucktime <br> https://developer.apple.com/documentation/quicktime-file-format/well-known_types |
| valid_range  | - defines the valid range of the depth data. range: 0-32, unit:bit |
| data_precision | - specifies the measurement unit for spatial data (meters: "m", decimeters: "dm", millimeters: "mm") |
#### Horizontal Field Of View Box（hfov）
##### Definition
Box Type: `hfov`
Container: `VisualSampleEntry `(e.g., rawc)
Mandatory: No 
Quantity: Zero or one
Stores additional horizontal fov information for the video track(depth). This box must come after non-optional boxes defined by the ISOBMFF specification and before optional boxes at the end of the VisualSampleEntry definition such as the CleanApertureBox and PixelAspectRatioBox.
##### Syntax
```C++
aligned(8) class HorizontalFieldOfView extends FullBox(‘hfov’, 0, 0) {
    int(16) hfov;
}
```

##### Semantics
`hfov `is a 16-bit signed integer that specifies horizontal fov for this video track(depth). 
| **Item** | **Description** |
| --- | --- |
| fhov | horizontal fov for video track(depth) (unit: micro degree), e.g. 90 degree fov = 90000 micro degree |
#### Vertical Field Of View Box（vfov）
##### Definition
Box Type: `vfov`
Container: `VisualSampleEntry `(e.g., rawc)
Mandatory: No 
Quantity: Zero or one
Stores additional vertical fov information for the video track(depth). This box must come after non-optional boxes defined by the ISOBMFF specification and before optional boxes at the end of the VisualSampleEntry definition such as the CleanApertureBox and PixelAspectRatioBox.
##### Syntax
```C++
aligned(8) class VerticalFieldOfView extends FullBox(‘hfov’, 0, 0) {
    int(16) vfov;
}
```

##### Semantics
`vfov `is a 16-bit signed integer that specifies vertical fov for this video track(depth). 
| **Item** | **Description** |
| --- | --- |
| vhov | Vertical fov for video track(depth) (unit: micro degree), e.g. 90 degree fov = 90000 micro degree |
### Pose Track(Text-Timed Metadata)
Pose track is used to save pose info from the 6dof sensors. This track is optional, used for MR and ML developer scenarios.
#### Basic

* Format：Text-based
* FrameRate: aligned with stereo video track

Timed metadata track:
https://www.iso.org/obp/ui/es/#iso:std:iso-iec:14496:-12:ed-6:v1:en
Refer to *12.3 Metadata media*
| **Box Syntax Element** | **Metadata Track** |
| --- | --- |
| tkhd.width/tkhd.height | 0 (Non-visual) |
| hdlr.handler_type | 'meta' |
| stsd.data_format | 'mebx'/'mett' |
| Sample content | Metadata key-value pairs (e.g., {"face_detect": true}) |
| cdsc reference | Optional (associated with a specific track or globally) |
#### TextMetaDataSampleEntry(mett)
use 'mett' box directly. 
##### Definition
Box Type: `mett`
Container:  `stsd`
Mandatory: Yes
Quantity: Exactly one
The timed metadata sample description contains information that defines how to interpret timed metadata media samples. This sample description is based on the standard sample description header, as described in [Sample description atom ('stsd')](https://developer.apple.com/documentation/quicktime-file-format/sample_description_atom).
The metadata sample description is a derived sample description format which describes metadata values represented in atoms. It may also include other atoms not holding metadata values.
Zero, one, or more values may be carried in a metadata sample description for a particular time.
##### Syntax
```C++
class MetaDataSampleEntry(‘mett’) extends SampleEntry (‘mett’)
{    
} 
class TextMetaDataSampleEntry() extends MetaDataSampleEntry (‘mett’) 
{ 
 string content_encoding; // optional  
       string mime_format; 
 BitRateBox (); // optional
} 
aligned(8) class SampleDescriptionBox (unsigned int(32) handler_type)  extends FullBox('stsd', 0, 0)
{
  int i ; 
        unsigned int(32) entry_count; 
  for (i = 1 ; i <= entry_count ; i++) {  
  switch (handler_type) {  
          case ‘soun’: // for audio tracks 
    AudioSampleEntry(); 
    break;  
    case ‘vide’: // for video tracks 
    VisualSampleEntry(); 
    break; 
    case ‘hint’: // Hint track 
    HintSampleEntry(); 
    break; 
    case ‘meta’: // Metadata track 
    MetadataSampleEntry(); 
    break;  
      } 
      } 
}
```

##### Semantics
| **Item** | **Name** | **Type** | **Description** |
| --- | --- | --- | --- |
| mime_format | "application/pose" | string | Definition of pos metadata track mine type |
| data | x | double | Displacement distance along the x-axis relative to the boot position, unit: meter |
|  | y | double | Displacement distance along the y-axis relative to the boot position, unit: meter |
|  | z | double | Displacement distance along the z-axis relative to the boot position, unit: meter |
|  | rx | double | Quaternion of rotation angle x |
|  | ry | double | Quaternion of rotation angle y |
|  | rz | double | Quaternion of rotation angle z |
|  | rw | double | Quaternion of rotation angle w |


# --- END: The SpatialMP4 Whitepaper.md ---



# --- BEGIN: Tips on dealing with semitransparent objects.md ---

This article provides tips on dealing with semitransparent objects in mixed reality scenes.
## Unable to correctly render multiple layers of semitransparent objects
Currently, rendering multiple layers of semitransparent objects is not supported. It is recommended that you use as few semitransparent objects as possible or do not use them.
## Semitransparent objects intersect with non-semitransparent objects
When semitransparent objects intersect with non-semitransparent objects, you need to manually set their render queue values.
In the following picture, the wall and skybox appear inside the semitransparent square objects in the red and yellow areas. For the red area, the wall and the semitransparent square object have the same render queue value, so the engine renders the semitransparent square object first and then the wall, causing the skybox to appear in the semitransparent square object. The yellow area has a similar situation in which the light green semitransparent green cylinder is rendered before the semitransparent square object, causing the wall and skybox to appear in the semitransparent square object.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a73ffaa549974c9ca772b8980e1e514f~tplv-goo7wpa0wc-image.image" width="550px" />

Below is the solution:

1. Set the wall's rendering mode to "Opaque" and adjust its render queue to match that of semitransparent objects.

    After these adjustments, the skybox is no longer visible inside the semitransparent square object in the red area.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bc6e9ad5b4a418e81d0be2513d10f09~tplv-goo7wpa0wc-image.image" width="550px" />

2. Increase the render queue value of the semitransparent square object in the yellow area, making the object be rendered much later.
   Below are the final render queue values of the objects in the yellow area:
   * Wall: 1000
   * Semitransparent green cylinder: 3000
   * Semitransparent square object: 4000
   After making adjustments, the scene appears as follows:

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b06e232a2cf4426bc669bb09807766f~tplv-goo7wpa0wc-image.image" width="550px" />

## Need to render a double-sided material when rendering the same object
Take the following picture as an example. You can try the following solutions:
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2874193d2bf945e6857084e47fca14d0~tplv-goo7wpa0wc-image.image" width="250px" />

* Disable the writing of depth.
   ```C#
   ZWrite Off
   ```

* Divide the object into two passes, one for the front face and one for the back face, and process them separately.

## Enable PremultipliedAlpha
To ensure consistent rendering of semitransparent objects across devices from different manufacturers, you can use the following code to enable `PremultipliedAlpha`. After enabling `PremultipliedAlpha`, the RGB channels will be multiplied by the Alpha value (R × A, G × A, B × A), which enhances the performance and visual quality of semitransparent elements, such as UI elements and particles.
```C#
PXR_Plugin.Render.UPxr_EnablePremultipliedAlpha(true);
```


# --- END: Tips on dealing with semitransparent objects.md ---



# --- BEGIN: Tracking Origin.md ---

The system sets a positional origin for a user when the user enters an app. Afterward, when the user moves in the virtual scene, the system tracks and calculates the user's positional changes based on the origin.
## Available tracking origin modes
The SDK provides the following tracking origin modes:
| **Mode** | **Description** |
| --- | --- |
| Not Specified | This mode indicates that the device does not know, or is unable to determine how it is reporting pose data. This value should be treated as an error condition. |
| Device | Also known as the Eye mode. The system sets the HMD's initial position as the origin. The device's height from the floor is not calculated.  <br> ***Note***:  <br>  <br> * This mode requires you to manually set the camera Y offset for simulating the user's height.  <br> * This mode is recommended for apps experienced in a sitting pose.  |
| Floor | The initial position of the HMD is vertically mapped onto the floor, serving as the origin. This mode requires the device to have floor detection capability and is therefore only supported by PICO Neo3 and PICO 4.  <br> ***Note***: This mode is recommended for apps experienced in a standing pose.. |
| Floor + Stage Mode | The same as the Floor mode, but the user is unable to recenter the screen by pressing the Home button. <br> ***Note****:*  <br>  <br> * The **Stage Mode** checkbox is on the PXR_Manager (Script) pane. <br> * The **Stage Mode** checkbox is checkable only when **Tracking Origin Mode** is set to Floor. |
## Set a tracking origin mode

1. Open your project in Unity Editor.
2. Add the **XR Origin** to the scene.
3. Select the **XR Origin**, then add the **PXR_Manager** script to it in the **Inspector** window.
4. On the **XR Origin** pane, set the **Tracking Origin Mode**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ed28dca46ba40acb247957f3d1fed04~tplv-goo7wpa0wc-image.image)
5. Set the **Camera Y Offset**. Camera Y offset refers to the offset added to the camera's Y direction, which is for simulating user height and is only applicable if you select the Device mode.

## Get your app's tracking origin mode
Call `PXR_System.GetTrackingOrigin` to get your app's tracking origin mode.
## API list
For details, refer to the [API reference](/reference/unity/latest/PXR_System/).

* `SetTrackingOrigin`: Set the tracking origin mode for the app.
* `GetTrackingOrigin`: Get the app's tracking origin mode.


# --- END: Tracking Origin.md ---



# --- BEGIN: Use cases & code samples(2).md ---

This article introduces the use cases of leaderboard service. For each use case, a code sample is provided for your reference.
## Retrieve leaderboard information
You can call `LeaderboardService.Get` to retrieve the information of the leaderboard for your app. The returned information includes the leaderboard's API name, associated destination, and total number of entries.
```C#
LeaderboardService.Get("Leaderboard API name").OnComplete(OnLeaderboardGet);

void OnLeaderboardGet(Message<LeaderboardList> message)
{
    if (!message.IsError)
    {
        Debug.Log($"LeaderboardService.Get success");
        // Process message.Data
    }
    else
    {
        var error = message.GetError();
        Debug.Log($"LeaderboardService.Get error: {error.Message}");
    }
}
```

## Retrieve leaderboard entries
Entries record the scores that users have obtained in your app. You can get the following types of entries on the leaderboard: all entries, entries after a specified rank, entries of specified users. `filter`, `startAt`, `pageSize`, and `pageIdx` are the parameters that need to be passed when retrieving leaderboard entries, and you can refer to the "[Parameter details](/en_leaderboards-parameter-details)" article for parameter descriptions and the scope of returns defined by different enumeration combinations as well as example returns.
```C#
// Get the entries of a leaderboard, including the entries' scores, supplementary metrics, entry ID, ranking, and more.
LeaderboardService.GetEntries("Leaderboard API name", 5, 0, LeaderboardFilterType.None, LeaderboardStartAt.Top).OnComplete(OnLeaderboardGetEntries);

void OnLeaderboardGetEntries(Message<LeaderboardEntryList> message)
{
    if (!message.IsError)
    {
        Debug.Log($"LeaderboardService.GetEntries success");
        // Process message.Data
    }
    else
    {
        var error = message.GetError();
        Debug.Log($"LeaderboardService.GetEntries error: {error.Message}");
    }
}

// Get the entries after a specified ranking. OnLeaderboardGetEntriesAfterRank is similar to OnLeaderboardGetEntries.
LeaderboardService.GetEntriesAfterRank("Leaderboard API name", 5, 0, 2).OnComplete(OnLeaderboardGetEntriesAfterRank);

// Get the entries of specified users. OnLeaderboardGetEntriesByIds is similar to OnLeaderboardGetEntries.
string[] userIds = new[] { "123" };
LeaderboardService.GetEntriesByIds("Leaderboard API name", 5, 0, LeaderboardStartAt.Top, userIds).OnComplete(OnLeaderboardGetEntriesByIds);
```

## Update leaderboard entries
Each user has only one entry on a leaderboard, and this entry records and displays the user's best score by default. Therefore, by default, a user's score will only be uploaded when the user achieves a better score than their current one. However, you can also configure the app to mandatorily upload a user's score whenever they get a new score.
You can call `LeaderboardService.WriteEntry` and `LeaderboardService.WriteEntryWithSupplementaryMetric` to update leaderboard entries. `LeaderboardService.WriteEntryWithSupplementaryMetric` supports writing additional metrics for the tiebreaker.
```C#
// Write an entry to a leaderboard. This entry is not mandatorily updated, which means it always displays the user's best score.
LeaderboardService.WriteEntry("Leaderboard API name", 100, null).OnComplete(OnLeaderboardWriteEntry);

// Write an entry to a leaderboard. This entry is mandatorily updated, which means it always displays the user's latest score.
LeaderboardService.WriteEntry("Leaderboard API name", 100, null, true).OnComplete(OnLeaderboardWriteEntry);
void OnLeaderboardWriteEntry(Message<bool> message)
{
    if (!message.IsError)
    {
        Debug.Log($"LeaderboardService.WriteEntry success");
        // Process message.Data
    }
    else
    {
        var error = message.GetError();
        Debug.Log($"LeaderboardService.WriteEntry error: {error.Message}");
    }
}

// Write an entry to a leaderboard. This entry contains supplementary metrics for the tiebreaker. OnLeaderboardWriteEntryWithSupplementaryMetric is similar to OnLeaderboardWriteEntry.   
LeaderboardService.WriteEntryWithSupplementaryMetric("Leaderboard API name", 100, 123, null, true).OnComplete(OnLeaderboardWriteEntryWithSupplementaryMetric);
```

## Unlock achievements for specific rankings
If a user obtains a specific ranking, such as top 3 and top 5, on your app's leaderboard, the app can unlock an achievement for the user. For how to create achievements, refer to [this article](/en_achievements-platform-service-setups#cc4e5c58).
```C#
public void CheckUnlockAchievementByLeaderboardRank(string yourUserID)
{
    LeaderboardService.GetEntries(
        "Leaderboard API name", 
        0, 
        5, 
        LeaderboardFilterType.None, 
        LeaderboardStartAt.Top)
        .OnComplete((message)=>{ // Message type is Message<LeaderboardEntryList>
            if (!message.IsError)
            {
                var entryList = message.Data;
                var list = entryList.GetEnumerator();
                while (list.MoveNext())
                {
                    var item = list.Current;
                    if (item.User.ID == yourUserID)
                    {
                        UnlockAchievement("yourAchievementName");
                        break;
                    }
                }
            }
        });
}

public void UnlockAchievement(string yourAchievementName)
{
    AchievementsService.Unlock(yourAchievementName, null).OnComplete(OnAchievementUnlockComplete);
    void OnAchievementUnlockComplete(Message<AchievementUpdate> message)
    {
        if (!message.IsError)
        {
            Debug.Log($"{message.Data.Name} unlock success");
        }
    }
}
```


# --- END: Use cases & code samples(2).md ---



# --- BEGIN: Use cases & code samples(3).md ---

This article introduces the use cases of achievement service. For each use case, a code sample is given for your reference.
## Example achievement
In the following example implementation, the achievement created on the PlCO Developer Platform is named COLLECT_SEVEN_RINGS, which will be unlocked when a user collects 7 rings. Otherwise, the game goes on and the system keeps counting and updating the number of rings the user has collected.
```C#
using UnityEngine; 
using System.Collections; 
using Pico.Platform; 
using Pico.Platform.Models;public class AchievementsService : MonoBehaviour 
  { 
    // The API name (COLLECT_SEVEN_RINGS) of the achievement defined on the PICO Developer Platform 
    private const string COLLECT_SEVEN_RINGSOptional= "COLLECT_SEVEN_RINGS"; 
    // Pass true if a player has collected 7 rings 
    private bool m_collectSevenRingsUnlocked; 
     
    public bool CollectSevenRings 
    { 
        get { return m_collectSevenRingsUnlocked; } 
    } 
    public void CheckForAchievmentUpdates() 
    { 
        Achievements.GetProgressByName(new string[]{ COLLECT_SEVEN_RINGSOptional}).OnComplete( 
            (Message<AchievementProgressList> msg) => 
            { 
                foreach (var achievement in msg.Data) 
                { 
                    if (achievement.Name == COLLECT_SEVEN_RINGS) 
                    { 
                        m_collectSevenRingsUnlocked = achievement.IsUnlocked; 
                    } 
                } 
            } 
        ); 
    } 
    public void RecordWinForLocalUser() 
    { 
        Achievements.AddCount(COLLECT_SEVEN_RINGS, 1); 
        CheckForAchievmentUpdates(); 
    } 
}
```

## Get achievement information
An achievement's information includes its API name, description, type, and the goal to accomplish for unlocking it.
```C#
// Get the basic information of a specified achievement
AchievmentsService.GetDefinitionsByName(new string[]{"yourAchievementName"}).OnComplete(
    (msg)=>{ // Message<AchievementDefinitionList>
        if (!msg.IsError)
        {
            var list = msg.Data.GetEnumerator();
            while (list.MoveNext())
            {
                var item = list.Current;
                Debug.Log($"Name: {item.Name}" +
                $"Target: {item.Target}" +
                $"Type: {item.Type}" +
                $"BitfieldLength: {item.BitfieldLength}" +
                $"Description: {item.Description}" +
                $"Title: {item.Title}" +
                $"IsArchived: {item.IsArchived}" +
                $"IsSecret: {item.IsSecret}" +
                $"ID: {item.ID}" +
                $"UnlockedDescription: {item.UnlockedDescription}" +
                $"WritePolicy: {item.WritePolicy}" +
                $"LockedImageURL: {item.LockedImageURL}" +
                $"UnlockedImageURL: {item.UnlockedImageURL}";)
            }
        }
    }
);

// Get the basic information of the achievements on a spcified page. The following code sample demonstrates how to get the information of the achievements on the first page, the page index is 0 and each page displays 5 achievements.
AchievmentsService.GetAllDefinitions(0, 5).OnComplete(
    (msg)=>{ // Message<AchievementDefinitionList>
        if (!msg.IsError)
        {
            var list = msg.Data.GetEnumerator();
            var totalSize = msg.Data.TotalSize; // The total number of achievements
            while (list.MoveNext())
            {
                var item = list.Current;
                Debug.Log($"Name: {item.Name}" +
                $"Target: {item.Target}" +
                $"Type: {item.Type}" +
                $"BitfieldLength: {item.BitfieldLength}" +
                $"Description: {item.Description}" +
                $"Title: {item.Title}" +
                $"IsArchived: {item.IsArchived}" +
                $"IsSecret: {item.IsSecret}" +
                $"ID: {item.ID}" +
                $"UnlockedDescription: {item.UnlockedDescription}" +
                $"WritePolicy: {item.WritePolicy}" +
                $"LockedImageURL: {item.LockedImageURL}" +
                $"UnlockedImageURL: {item.UnlockedImageURL}";)
            }
        }
    }
);
```

## Get achievement progress
The app needs to get the progress the user has made on a specific achievement, so as to determine if it should unlock the achievement for the user.
```C#
AchievementsService.GetProgressByName(new string[]{"yourAchievementName"}).OnComplete(
    (msg)=>{ // Message<AchievementProgressList>
        var list = obj.GetEnumerator();
        while (list.MoveNext())
        {
            var item = list.Current;
            Debug.Log($"IsUnlocked: {item.IsUnlocked}" + // Simple achievements has no progress information and they only have two status: locked, unlocked.
                $"UnlockTime: {item.UnlockTime}" +
                $"ID: {item.ID}" +
                $"Name: {item.Name}" +
                $"Bitfield: {item.Bitfield}" + // The progress of bitfield achievement
                $"Count: {item.Count}" + // The progress of count achievement
                $"ExtraData: {Encoding.UTF8.GetString(item.ExtraData)}";)
        }
    }
);
```

## Update achievement progress
The app should timely update achievement progress for a user. 

* For a count achievement, a count should be added. 
* For a bitfield achievement, a bit should be unlocked.
* Simple achievements have no progress information and they only have two statuses which are "locked" and "unlocked".

```C#
// Update progress for a count achievement
int count = 1;
byte[] bytes = new byte[]{};
AchievementsService.AddCount("yourAchievementName", count, bytes).OnComplete(
    (msg)=>{ // msg:Message<AchievementUpdate>
        if (!msg.IsError)
        {
            var updateData = msg.Data;
            Debug.Log($"achievementName: {updateData.Name}");
            Debug.Log($"JustUnlocked: {updateData.JustUnlocked}");
        }
    }
);

// Update progress for a bitfield achievement
byte[] bytes = new byte[]{};
string fields = "100011"
AchievementsService.AddFields("yourAchievementName", fields, bytes).OnComplete(
    (msg)=>{ // msg:Message<AchievementUpdate>
        if (!msg.IsError)
        {
            var updateData = msg.Data;
            Debug.Log($"achievementName: {updateData.Name}");
            Debug.Log($"JustUnlocked: {updateData.JustUnlocked}");
        }
    }
);
```

## Unlock an achievement
When a user reaches the target for unlocking an achievement, the app should immediately unlock the achievement for the user.
| **Achievement Type** | **How to unlock** |
| --- | --- |
| Count & Bitfield | Call `AchievementsService.AddCount()` and `AchievementsService.AddFields()` to ensure that a user's achievement progress is timely updated. When a user reaches the target count or completes the last task, the achievement will be unlocked automatically. If you want to unlock the achievement before the requirement is met, you can call `AchievementsService.Unlock()`. |
| Simple | Call `AchievementsService.Unlock()` to unlock an achievement for a user after the user completes the task. |
```C#
// Count achievements and bitfield achievement are automatically unlocked after the requirements are met, and you can also call AchievementService.Unlock to unlock them. For simple achievements, you need to call AchievementService.Unlock to unlock them.
byte[] bytes = new byte[]{};
AchievementsService.Unlock("yourAchievementName", bytes).OnComplete(
    (msg)=>{ // msg:Message<AchievementUpdate>
        if (!msg.IsError)
        {
            var updateData = msg.Data;
            Debug.Log($"achievementName: {updateData.Name}");
            Debug.Log($"JustUnlocked: {updateData.JustUnlocked}");
        }
    }
);
```

To send users a notification after they unlock an achievement, you need to check the **Notification Status** checkbox when creating the achievement on the PICO Developer Platform.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b16a4d6d7a1430fad57920020521d4a~tplv-goo7wpa0wc-image.image" width="837px" />

## Unlock achievements for specific leaderboard rankings
If a user obtains a specific ranking, such as top 3 and top 5, on your app's leaderboard, the app can unlock an achievement for the user. For how to create leaderboards, refer to [this article](/en_leaderboards-platform-service-setups#0d6de01e).
```C#
public void CheckUnlockAchievementByLeaderboardRank(string yourUserID)
{
    LeaderboardService.GetEntries(
        "Leaderboard API name", 
        0, 
        5, 
        LeaderboardFilterType.None, 
        LeaderboardStartAt.Top)
        .OnComplete((message)=>{ // Message type is Message<LeaderboardEntryList>
            if (!message.IsError)
            {
                var entryList = message.Data;
                var list = entryList.GetEnumerator();
                while (list.MoveNext())
                {
                    var item = list.Current;
                    if (item.User.ID == yourUserID)
                    {
                        UnlockAchievement("yourAchievementName");
                        break;
                    }
                }
            }
        });
}

public void UnlockAchievement(string yourAchievementName)
{
    AchievementsService.Unlock(yourAchievementName, null).OnComplete(OnAchievementUnlockComplete);
    void OnAchievementUnlockComplete(Message<AchievementUpdate> message)
    {
        if (!message.IsError)
        {
            Debug.Log($"{message.Data.Name} unlock success");
        }
    }
}
```

## Create an achievement wall
You can design an achievement wall for your app. An achievement wall displays the achievements a user has obtained in your app. An icon will be lit up on the wall when a corresponding achievement is unlocked. The achievement wall is visible to the user's friends or other users.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/898ad89cfc914f86be36f6a93160c0d2~tplv-goo7wpa0wc-image.image" width="546px" />


# --- END: Use cases & code samples(3).md ---



# --- BEGIN: Use cases & code samples.md ---

This article describes the use cases of the Social Interaction service in detail and provides corresponding code samples.
## Set/Update/Clear presence info
Call `PresenceService.Set` to set all types of presence information for a user. When you use this API, you need to create `PresenceOptions` first, then set the current user's presence information, and finally, print the user's presence information after the request succeeds. When the user leaves the current room or your app, you need to call `PresenceService.Clear` to clear the user's presence information. 
```C#
// Set and update presence information
var options = new PresenceOptions();
options.SetDestinationApiName("destinationApiName");
options.SetExtra("extraData");
options.SetIsJoinable(true);
options.SetMatchSessionId("matchSessionId");
options.SetLobbySessionId("lobbySessionId");
var message = await PresenceService.Set(options).Async();
if (message.IsError)
    Debug.LogError(message.Error);
else
    Debug.Log("Presence Set successfully.");
    
// Clear presence information
PresenceService.Clear();
```

## View friends' locations and presence info
Users can view their friends' locations and presence information.
```C#
var message = await UserService.GetFriends().Async();
if (message.IsError)
    Debug.LogError(message.Error);
else
    // You can add custom logic here
    foreach (var friend in message.Data)
    {
        Debug.Log("Friend: " + friend.DisplayName);
        Debug.Log($"Api name: {friend.PresenceDestinationApiName}");
        Debug.Log($"Extra: {friend.PresenceExtra}");
        Debug.Log($"Match session id: {friend.PresenceMatchSessionId}");
        Debug.Log($"Lobby session id: {friend.PresenceLobbySessionId}");
    }
```

## Invite friends
"Inviting friends" and "joining friends" are a pair of behaviors accounted as a fundamental and significant social interaction experience. Destinations, deep links, and presence work together to make this experience come true in your app. Currently, the PICO SDK enables users to invite friends by sending invitation messages. Below is the overall workflow:

1. User A sends an invitation to Friend B.
2. The system retrieves User A's presence information and stores it in the invitation message.
3. Friend B clicks on the invitation message to launch the corresponding app.
4. You retrieve the launch details, such as destination, lobby session ID, and match session ID, from the deep link, then parse the launch details and send Friend B to User A's location.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50c6f4dc9eef48b0a5ea6d54e760d1a9~tplv-goo7wpa0wc-image.image" width="546px" />

Users need to send invitations to friends via the Invite UI. The Invite UI displays all of the user's friends. You can directly use the system default Invite UI (as shown below) and invitation workflow provided by the PICO Friends app, which is an easier and quicker implementation. Otherwise, you need to customize the invitation workflow and UI design.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3620b19a900c4504981bd036a9b9c759~tplv-goo7wpa0wc-image.image" width="300px" />

### Prerequisites
Make sure you have created destination(s) and enabled DeepLink for them on the PICO Developer Platform. For detailed instructions, refer to "[Social Interaction: Platform service setups](/en_social-interaction-platform-service-setups#1dd5698d)".
### Via the system default Invite UI
Users can use the system default Invite UI to invite friends to a destination, private room, and challenge. 

* Invite friends to an in-app destination (i.e., presence invitation)
   ```C#
   // Send invitation
   var message = await PresenceService.LaunchInvitePanel().Async();
   if (message.IsError)
       Debug.LogError(message.Error);
   else
       Debug.Log("Presence invite panel launched successfully.");
       
   // Register the callback to get notified when the invitation is received
   PresenceService.SetJoinIntentReceivedNotificationCallback(message =>
   {
       var intent = message.Data;
       // You can add custom logic here, join the user to the target location according to the JoinIntent
       Debug.Log($"DestinationApiName: ${intent.DestinationApiName} ");
       Debug.Log($"MatchSessionId: ${intent.MatchSessionId}");
       Debug.Log($"LobbySessionIda: ${intent.LobbySessionId}");
       Debug.Log($"DeeplinkMessage: ${intent.DeeplinkMessage}");
   });
   ```

* Invite friends to a private room
   ```C#
   // Send invitation
   var message = await RoomService.LaunchInvitableUserFlow(roomId).Async();
   if (message.IsError)
       Debug.LogError(message.Error);
   else
       Debug.Log("Room invite panel launched successfully.");
    
    // Register the callback to get notified when the invitation is received
   RoomService.SetRoomInviteAcceptedNotificationCallback((message) =>
   {
       var roomId = message.Data;
       // You can add custom logic here, join the user to the target room according to the RoomID
       Debug.Log($"RoomId: ${roomId}");
   });
   ```

* Invite friends to a challenge
   ```C#
   // Send invitation
   var message = await ChallengesService.LaunchInvitableUserFlow(challengeID).Async();
   if (message.IsError)
       Debug.LogError(message.Error);
   else
       Debug.Log("Challenge invite panel launched successfully.");
       
   // Register the callback to get notified when the invitation is received
    ChallengesService.SetChallengeInviteAcceptedOrLaunchAppNotificationCallback((message) =>
   {
       var challengeId = message.Data;
       // You can add custom logic here, join the user to the target challenge according to the ChallengeID
       Debug.Log($"ChallengeId: ${challengeId}");
   });
   ```

### Via the custom Invite UI
Users can use the custom Invite UI to invite friends to a destination, private room, and challenge. 

* Invite friends to an in-app destination (i.e., presence invitation)
   ```C#
   // Send invitation
   string[] userIds = { "userId1", "userId2" };
   PresenceService.SendInvites(userIds);
   
   // Register the callback to get notified when the invitation is received
   PresenceService.SetJoinIntentReceivedNotificationCallback(message =>
   {
       var intent = message.Data;
       // You can add custom logic here, join the user to the target location according to the JoinIntent
       Debug.Log($"DestinationApiName: ${intent.DestinationApiName} ");
       Debug.Log($"MatchSessionId: ${intent.MatchSessionId}");
       Debug.Log($"LobbySessionIda: ${intent.LobbySessionId}");
       Debug.Log($"DeeplinkMessage: ${intent.DeeplinkMessage}");
   });
   ```

* Invite friends to a private room
   ```C#
   // Get the invitee's invite token
   RoomOptions options = new RoomOptions();
   var message = await RoomService.GetInvitableUsers2(options).Async();
   if (message.IsError)
   {
       Debug.LogError(message.Error);
       return;
   }
   
   // Send invitation
   var userList = message.Data;
   for (int i = 0; i < userList.Capacity; i++)
   {
       RoomService.InviteUser(roomId, userList[i].InviteToken);
   }
   
   // Register the callback to get notified when the invitation is received
   RoomService.SetRoomInviteAcceptedNotificationCallback((message) =>
   {
       var roomId = message.Data;
       // You can add custom logic here, join the user to the target room according to the RoomID
       Debug.Log($"RoomId: ${roomId}");
   });
   ```

* Invite friends to a challenge
   ```C#
   // Send invitation
   ChallengesService.Invite(challengeID, new[] { "userId1", "userId2" });
   
   // Register the callback to get notified when the invitation is received
    ChallengesService.SetChallengeInviteAcceptedOrLaunchAppNotificationCallback((message) =>
   {
       var challengeId = message.Data;
       // You can add custom logic here, join the user to the target challenge according to the ChallengeID
       Debug.Log($"ChallengeId: ${challengeId}");
   });
   ```

### Get launch details
There are two app launch types, cold launch and hot launch. You need to define both of them in your code.

* For a **cold launch**, you can directly call `ApplicationService.GetLaunchDetails` to retrieve launch details. 
* For a **hot launch**, if `LaunchDetails` has changed and the callback function you set in `ApplicationService.SetLaunchIntentChangedCallback` has been triggered, you can immediately call `ApplicationService.GetLaunchDetails` after receiving the callback function.

```C#
// First cold launch
var launchDetails = ApplicationService.GetLaunchDetails();
// You can add custom logic here
Debug.Log(launchDetails.LaunchType);

// Hot launch
ApplicationService.SetLaunchIntentChangedCallback((message) =>
{
    var launchDetails = ApplicationService.GetLaunchDetails();
    // You can add custom logic here
    Debug.Log(launchDetails.LaunchType);
});
```

## Jump to another app
The PICO system supports jumping between apps, in other words, directing users to another app from the current app. To provide users with this experience, you need to call `ApplicationService.LaunchApp` or `ApplicationService.LaunchAppByAppId`, and set the function object `SetDeeplinkMessage` in the `Options` parameter. In `SetDeeplinkMessage`, you need to define the jumping rule.
```C#
// Direct the user to another app by specifying the app package name
var options = new ApplicationOptions();
options.SetDeeplinkMessage("message");
ApplicationService.LaunchApp("com.pico.example", options);

// Direct the user to another app by specifying the app ID
var options = new ApplicationOptions();
options.SetDeeplinkMessage("message");
ApplicationService.LaunchAppByAppId("APP_ID", options);
```

The `ApplicationOptions` parameter must be passed when using these two APIs. Below is an example:
```C#
ApplicationOptions options = new ApplicationOptions();
options.SetDeeplinkMessage("");
ApplicationService.LaunchApp("com.company.example", options);
ApplicationService.LaunchAppByAppId("RaplaceWithYourAppid", options);
```

## Jump to the PICO Store
If you want to encourage users to upgrade your app to the latest version for new feature promotion and bug fixing, you can direct users to your app's details page on the PICO Store where users can click on the upgrade button to upgrade your app.
```C#
public async Task LaunchToAppStoreIfOutdated()
{
    var appVersionMsg = await ApplicationService.GetVersion().Async();
    var appVersion = appVersionMsg.Data;
    var outdated = appVersion.CurrentCode < appVersion.LatestCode;
    if (outdated)
        ApplicationService.LaunchStore();
    else
        Debug.Log("App version is up to date");
}
```

## Share content on Douyin
> Only available for Chinese Mailand developers.

Recording and sharing highlights on social platforms is a common social interaction bahavior among users. The SDK provides content sharing APIs that enable users to share screenshots and videos to Douyin in your app. The to-be-shared content must be located in the public directory.
```C#
// Shares videos attached with thumbnails on the Douyin app.
PresenceService.ShareVideo("/video-path", "/video-thumb-path");

// Shares screenshots on the Douyin app.
var imagePaths = new List<string> { "/image-path-1", "/image-path-2" };
PresenceService.ShareVideoByImages(imagePaths);
```


# --- END: Use cases & code samples.md ---



# --- BEGIN: Use different operators.md ---

The SDK provides different types of operators. You need to pass in different parameters according to different `OperatorType`, and some operators require additional configurations. This document introduces all the operators provided by the SDK and their usage methods.
## Important note

* Operators cannot be destroyed individually. They can only be destroyed along with the pipelines they belong to.
* All operators can have their inputs and outputs set.

## API reference

* `CreateOperator`: used to create an operator.
   ```C#
   //Create an operator
   var xxxOperator= currentPipeline.CreateOperator<ArithmeticComposeOperator>();
   ```

* `SetOperand`: used to set the inputs of the operator, or operand.
   ```C#
   xxxOperator.SetOperand("operand0", operand0);
   xxxOperator.SetOperand("operand1", operand1);
   ```

* `SetResult`: used to set the outputs of the operator, or result.
   ```C#
   xxxOperator.SetResult("result", result);
   ```

## Usage methods of different operators
### ArithmeticComposeOperator
`ArithmeticComposeOperator` is used to perform arithmetic operations. You can define operations using addition (`+`), subtraction (`-`), multiplication (`*`), division (`/`), parentheses, and constants. You need to pass in the operation expression in string form. In the expression, `{X}` represents the operand with the sequence number `X`. For example, `{0} * 2.0 + ({1} / 6)` means operand0 multiplied by 2.0 plus operand1 divided by 6.
In use, you need to meet the following requirements:

* The number of operands in the operator cannot exceed 10.
* All operands used in the operation expression are mandatory and must be of the `Mat` type. Other operands are optional.
* The name of each operand is `{X}`, where `X` represents the sequence number of the operand.
* The operator has exactly one mandatory result.
* When creating the operator, the calculation steps need to be determined in advance. An example is as follows:
   ```C#
   var arithmeticComposeConfig = new ArithmeticComposeConfiguration("{0} * 2.0 + ({1} / 6)")
   var arithmeticComposeOp = currentPipeline.CreateOperator<ArithmeticComposeOperator>(arithmeticComposeConfig);
   arithmeticComposeOp.SetOperand("operand0", tensor0);
   arithmeticComposeOp.SetOperand("operand1", tensor1);
   arithmeticComposeOp.SetResult("result", tensorX);
   ```

### ElementwiseMinOperator
`ElementwiseMinOperator` is used to compare the minimum values of two elements. In use, you need to meet the following requirements:

* There are two required operands. Their names are `operand0` and `operand1` respectively.
* There is one required result. Its name is `result`.

When binding tensors, the types, data types, and shapes of the operands and the result are not verified. However, during runtime, if the shapes of `operand0`, `operand1`, and `result` are inconsistent, or their data types are different, the pipeline where they are located will be terminated and an error log will be printed.
An example is as follows:
```C#
var elementwiseMinOp = currentPipeline.CreateOperator<ElementwiseMinOperator>();
elementwiseMinOp.SetOperand("operand0", tensor0);
elementwiseMinOp.SetOperand("operand1", tensor1);
elementwiseMinOp.SetResult("result", tensorX);
```

### ElementwiseMaxOperator
`ElementwiseMaxOperator` is used to compare the maximum values of two elements. In use, you need to meet the following requirements:

* There are two required operands. Their names are `operand0` and `operand1` respectively.
* There is one required result. Its name is `result`.

When binding tensors, the types, data types, and shapes of the operands and the result are not verified. However, during runtime, if the shapes of `operand0`, `operand1`, and `result` are inconsistent, or their data types are different, the pipeline where they are located will be terminated and an error log will be printed.
An example is as follows:
```C#
var elementwiseMaxOp = currentPipeline.CreateOperator<ElementwiseMaxOperator>();
elementwiseMaxOp.SetOperand("operand0", tensor0);
elementwiseMaxOp.SetOperand("operand1", tensor1);
elementwiseMaxOp.SetResult("result", tensorX);
```

### ElementwiseMultiplyOperator
`ElementwiseMultiplyOperator` is used to calculate the product of two elements. In use, you need to meet the following requirements:

* There are two required operands. Their names are `operand0` and `operand1` respectively.
* There is one required result. Its name is `result`.

When binding tensors, the types, data types, and shapes of the operands and the result are not verified. However, during runtime, if the shapes of `operand0`, `operand1`, and `result` are inconsistent, or their data types are different, the pipeline where they are located will be terminated and an error log will be printed.
An example is as follows:
```C#
var elementwiseMultiplyOp = currentPipeline.CreateOperator<ElementwiseMultiplyOperator>();
elementwiseMultiplyOp.SetOperand("operand0", tensor0);
elementwiseMultiplyOp.SetOperand("operand1", tensor1);
elementwiseMultiplyOp.SetResult("result", tensorX);
```

### CustomizedCompareOperator
`CustomizedCompareOperator`  is used to compare two elements and write the boolean result of each element comparison as an integer into the result (write `0` if it is `false`, and write `1` if it is `true`). In use, you need to meet the following requirements:

* There are two required operands. Their names are `operand0` and `operand1` respectively.
* There is one required result. Its name is `result`.
* When creating the operators, you need to pass in the comparison rules you want to use. 
* The data type of the result must be integer.

When binding tensors, the types, data types, and shapes of the operands and the result are not verified. However, during runtime, if the shapes of `operand0`, `operand1`, and `result` are inconsistent, or the channels of their data types are different, the pipeline where they are located will be terminated and an error log will be printed.
The values of the `CustomizedComparison` enumeration are as follows:
```C#
public enum CustomizedComparison
{
    LargerThan, // If the corresponding element of operand0 is larger than that of operand1, the result is true.
    SmallerThan, // If the corresponding element of operand0 is smaller than that of operand1, the result is true.
    SmallerOrEqual, // If the corresponding element of operand0 is smaller than or equal to that of operand1, the result is true.
    LargerOrEqual, // If the corresponding element of operand0 is larger than or equal to that of operand1, the result is true.
    EqualTo, // If the corresponding element of operand0 is equal to that of operand1, the result is true.
    NotEqual, // If the corresponding element of operand0 is not equal to that of operand1, the result is true.
}
```

An example is as follows:
```C#
var customizedCompareConfig = new ComparisonOperatorConfiguration(CustomizedComparison.LargerThan)
var customizedCompareOp = currentPipeline.CreateOperator<CustomizedCompareOperator>(customizedCompareConfig);
customizedCompareOp.SetOperand("operand0", tensor0);
customizedCompareOp.SetOperand("operand1", tensor1);
customizedCompareOp.SetResult("result", tensorX);
```

### ElementwiseOrOperator
`ElementwiseOrOperator` is used to perform elementwise `bool or` calculations. In use, you need to meet the following requirements:

* There are two required operands. Their names are `operand0` and `operand1` respectively. The data types of the operands must be integers, which will be verified during the binding process.
* There is one required result. Its name is `result`. The data type of the result must be integer, which will be verified during the binding process.

An example is as follows:
```C#
var elementwiseOrOp = currentPipeline.CreateOperator<ElementwiseOrOperator>();
elementwiseOrOp.SetOperand("operand0", tensor0);
elementwiseOrOp.SetOperand("operand1", tensor1);
elementwiseOrOp.SetResult("result", tensorX);
```

### ElementwiseAndOperator
`ElementwiseAndOperator` is used to perform elementwise `bool and`  calculations. In use, you need to meet the following requirements:

* There are two required operands. Their names are `operand0` and `operand1` respectively. The data types of the operands must be integers, which will be verified during the binding process.
* There is one required result. Its name is `result`. The data type of the result must be integer, which will be verified during the binding process.

An example is as follows:
```C#
var elementwiseAndOp = currentPipeline.CreateOperator<ElementwiseAndOperator>();
elementwiseAndOp.SetOperand("operand0", tensor0);
elementwiseAndOp.SetOperand("operand1", tensor1);
elementwiseAndOp.SetResult("result", tensorX);
```

### AllOperator
`AllOperator` is used to perform the `ALL` operation on the entire tensor. In use, you need to meet the following requirements:

* There is one required operand. Its name is `operand`.
* There is one required result. Its name is `result`. Its type must be `Scalar`, with the data type being 1-channel integer and the shape being `(1,)`. These will be verified during the binding process.

An example is as follows:
```C#
var allOp = currentPipeline.CreateOperator<AllOperator>();
allOp.SetOperand("operand", tensor0);
allOp.SetResult("result", tensorX);
```

### AnyOperator
`AnyOperator` is used to perform `ANY` operation on the entire tensor. In use, you need to meet the following requirements:

* There is one required operand. Its name is `operand`.
* There is one required result. Its name is `result`. It is required to be of the `Scalar` type, with a data type of 1-channel integer and a shape of `(1,)`. These will be verified during the binding process.

```C#
var anyOp = currentPipeline.CreateOperator<AnyOperator>();
anyOp.SetOperand("operand", tensor0);
anyOp.SetResult("result", tensorX);
```

### NmsOperator
`NmsOperator` is used to perform Non-Maximum Suppression (NMS) on bounding boxes. In use, you need to meet the following requirements:

* There are two required operands as follows:
   | **Operand** | **Description** |
   | --- | --- |
   | scores | The confidence of each bounding box. It must be either of the `Scalar ` type, with a data type of 1-channel float32/64 and a shape of `(N,)`, or of the `Matrix`  type, with a data type of 1-channel float32/64 and a shape of `(1, N)` or `(N, 1)`. `N` represents the number of input bounding boxes. |
   | boxes | The coordinate of each bounding box in XXYY format. It must be either of the `Matrix`  type, with a data type of 4-channel float32/64 and a shape of `(1, N)` or `(N, 1)`, or of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(N, 4)`. `N` represents the number of input bounding boxes. |
* There are three optional results as follows:
   | **Result** | **Description** |
   | --- | --- |
   | scores | The corresponding confidences of the bounding boxes that have passed NMS, arranged in descending order of confidence. The confidences must be either of the `Scalar` type, with a data type of 1-channel float32/64 and a shape of `(M,)`, or of the `Matrix `type, with a data type of 1-channel float32/64 and a shape of `(1, M)` or `(M, 1)`. `M` represents the maximum number of bounding boxes that have passed NMS. |
   | boxes | The coordinates in XXYY format corresponding to the bounding boxes that have passed NMS, arranged in descending order of confidence. The coordinates must be of the `Matrix` type, with a data type of 4-channel float32/64 and a shape of `(1, M)` or `(M, 1)`, or of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(M, 4)`. `M` represents the maximum number of bounding boxes that have passed NMS. |
   | indices | The indices in the operand `boxes` corresponding to the bounding boxes that have passed NMS, arranged in descending order of confidence. It must be either of the `Scalar` type, with a data type of 1-channel integer and a shape of `(M,)`, or of the `Matrix` type, with a data type of 1-channel integer and a shape of `(1, M)` or `(M, 1)`. `M` represents the maximum number of bounding boxes that have passed NMS. |
* When creating this operator, you need to pass in a float threshold to specify the threshold for the overlapping ratio of two bounding boxes during the NMS operation.

An example is as follows:
```C#
var nmsConfig = new NmsConfiguration(0.85f)
var nmsOp = currentPipeline.CreateOperator<NmsOperator>(nmsConfig);
nmsOp.SetOperand("scores", scoresTensor);
nmsOp.SetOperand("boxes", boxesTensor);
nmsOp.SetResult("scores", nmsScores);
nmsOp.SetResult("boxes", nmsBoxes);
```

### SolvePnPOperator
`SolvePnPOperator` is used to solve the Perspective-n-Point (PNP) problem. Given the two-dimensional coordinates of the projected points, the three-dimensional coordinates of each point in the world coordinate system, and the camera projection matrix, it then calculates the rotation and translation transformations of the camera coordinate system relative to the world coordinate system. This operator is a wrapper for the `solvePnP` function in OpenCV. In use, you need to meet the following requirements:

* There are three required operands as follows:
   | **Operand** | **Description** |
   | --- | --- |
   | object points | The three-dimensional coordinates of points in the world coordinate system. They are required to be of the `Point` type, with a data type of 3-channel float32/64 and a shape of `(P,)`. |
   | image points | The two-dimensional coordinates of points on the camera projection plane. They are required to be of the `Point` type, with a data type of 2-channel float32/64 and a shape of `(P,)`. |
   | camera matrix | The camera projection matrix. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(3, 3)`. |
* There are two optional results as follows:
   | **Result** | **Description** |
   | --- | --- |
   | rotation | Rotation vector, using the axis-angle representation method. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(1, 3)` or `(3, 1)`. |
   | translation | Translation vector. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(1, 3)` or `(3, 1)`. |

An example is as follows:
```C#
var solvePnPOp = currentPipeline.CreateOperator<SolvePnPOperator>();
solvePnPOp.SetOperand("object points", objectPointsTensor);
solvePnPOp.SetOperand("image points", imagePointsTensor);
solvePnPOp.SetOperand("camera matrix", cameraMatrixTensor);
solvePnPOp.SetResult("rotation", rvecTensor);
solvePnPOp.SetResult("translation", tvecTensor);
```

### GetAffineOperator
`GetAffineOperator` is used to obtain an affine transformation matrix in a two-dimensional space. This operator is a wrapper for the `getAffineTransform` function in OpenCV. In use, you need to meet the following requirements:

* There are two required operands as follows:
   | **Operand** | **Description** |
   | --- | --- |
   | src | The coordinates of three points in the source space of the affine transformation. It is required to be of the `Point` type, with a data type of 2-channel float32/64. The shape must be `(3,)`. |
   | dst | The coordinates of three points in the target space of the affine transformation, which should correspond one-to-one with the three points in `src`. It is required to be of the `Point` type, with a data type of 2-channel float32/64. The shape must be `(3,)`. |
* There is one optional result named `result`. It is used to store the affine matrix. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64. The shape must be `(2, 3)`. 

An example is as follows:
```C#
var getAffineOp = currentPipeline.CreateOperator<GetAffineOperator>();
getAffineOp.SetOperand("src", srcTensor);
getAffineOp.SetOperand("dst", dstTensor);
getAffineOp.SetResult("result", resultTensor);
```

### ApplyAffineOperator
`ApplyAffineOperator` is used to apply the affine transformation to an image. This operator is a wrapper for the `warpAffine` function in OpenCV. In use, you need to meet the following requirements:

* There are two required operands as follows:
   | **Operand** | **Description** |
   | --- | --- |
   | affine | Affine matrix. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64. The shape must be `(2, 3)`. |
   | src image | Source image. It is required to be of the `Matrix` type. There is no requirement for the data type, but the shape must have exactly two dimensions. |
* There is one optional result named `dst image`. It represents the result of the affine transformation. It is required to be of the `Matrixt` type, and its data type should be compatible with `src image`.

An example is as follows:
```C#
var applyAffineOp = currentPipeline.CreateOperator<ApplyAffineOperator>();
applyAffineOp.SetOperand("affine", affineTensor);
applyAffineOp.SetOperand("src image", srcTensor);
applyAffineOp.SetResult("dst image", resultTensor);
```

### ApplyAffinePointOperator
`ApplyAffinePointOperator` is used to apply affine transformation to points on a plane. This operator is a wrapper for the `transform` function in OpenCV. In use, you need to meet the following requirements:

* There are two required operands as follows:
   | **Operand** | **Description** |
   | --- | --- |
   | affine | Affine matrix. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64. The shape must be `(2, 3)`. |
   | src points | Source points. It is required to be of the `Point` type. The data type can be any type with 2 channels. The shape must be `(N,)`, where `N` represents the number of points. |
* There is one optional result named `dst points`. It represents the result of the affine transformation. It is required to be of the `Point` type. The data type and shape must be exactly the same as those of `src points`.

An example is as follows:
```C#
var applyAffinePointOp = currentPipeline.CreateOperator<ApplyAffinePointOperator>();
applyAffinePointOp.SetOperand("affine", affineTensor);
applyAffinePointOp.SetOperand("src points", srcTensor);
applyAffinePointOp.SetResult("dst points", resultTensor);
```

### UvTo3DInCameraSpaceOperator
`UvTo3DInCameraSpaceOperator` is used to convert the UV coordinates on the left-eye RGB image into 3D coordinates in the left RGB camera coordinate system. It is generally used together with `CAMERA_SPACE_TO_WORLD` to project the AI calculation results (such as those from object detection models, segmentation models, etc.) on the left-eye RGB image into the world coordinate system for rendering purposes. In use, you need to meet the following requirements:

* There are five required operands as follows:
   | **Operand** | **Description** |
   | --- | --- |
   | uv | The UV coordinate on the left-eye RGB image. It is of the `Point` type, with 2 channels and an `int32` data type. |
   | timestamp | The timestamp corresponding to the left-eye image, from `RECTIFIED_VST_ACCESS`. |
   | camera intrinsic | The intrinsic parameters of the left-eye RGB camera, from `RECTIFIED_VST_ACCESS`. |
   | left image | Left-eye RGB image, from `RECTIFIED_VST_ACCESS`. |
   | right image | Right-eye RGB image, from `RECTIFIED_VST_ACCESS`. |
* There is one result named `point_xyz`. It represents the 3D coordinates in the coordinate system of the left RGB camera. It is of the `Point` type with a data type of 3-channel float32/64, or of the `Matrix` type, with a shape of {1, 3} {3, 1}. Its length is the same as that of the UV coordinates.

An example is as follows:
```C#
var uvTo3DOp = currentPipeline.CreateOperator<UVTo3DInCameraSpaceOperator>();
uvTo3DOp.SetOperand("uv", uvTensor);
uvTo3DOp.SetOperand("timestamp", timestampTensor);
uvTo3DOp.SetOperand("camera intrisic", K_rgbTensor);
uvTo3DOp.SetOperand("left image", leftImageTensor);
uvTo3DOp.SetOperand("right image", rightImageTensor);
uvTo3DOp.SetResult("point_xyz", xyzTensor);
```

### AssignmentOperator
`AssignmentOperator` is used for copy assignment operations. By combining different operands and results, you can use this operator to perform operations such as slicing, data type conversion, and tensor type conversion. In use, you need to meet the following requirements:

* There are five operands:
   | **Operand** | **Required** | **Description** |
   | --- | --- | --- |
   | src | Yes | The source tensor for copying. It can be of any type, data type, and shape. |
   | src slices | No | The slice of each dimension of the source tensor for copying. It is required to be of the `Scalar` type. The data type should be 2/3-channel integer. The shape is `(Sn,)`. `Sn` represents the dimensions of `src`, or the size of the shape of `src`. If it is empty, it means the entire source tensor is selected. |
   | src channel slice | No | The slice on the channel of the source tensor for copying. It is required to be of the `Scalar` type. The data type should be 2/3-channel integer. The shape is `(1,)`. If it is empty, it means that each channel in the selected slice of the source tensor will be copied. |
   | dst slices | No | The slice on each dimension of the destination tensor for copying. It is required to be of the `Scalar` type. The data type should be 2/3-channel integer. The shape is `(Dn,)`. `Dn` represents the dimensions of `dst`, or the size of the shape of `dst`. If it is empty, it means the entire destination tensor will be viewed as the target for copying. |
   | dst channel slice | No | The slice along the channel of the target tensor for copying. It is required to be of `Scalar` type. The data type should be 2/3-channel integer. The shape is `(1,)`. If it is empty, it means each channel in the selected slice of the target tensor will be copied. |
* There is one mandatory result named `dst`. It represents the target tensor for copying. It can be of any type, data type, and shape.

An example is as follows:
```C#
var assignmentOp = currentPipeline.CreateOperator<AssignmentOperator>();
assignmentOp.SetOperand("src", srcTensor);
assignmentOp.SetOperand("src slices", srcSlicesTensor);
assignmentOp.SetOperand("src channel slice", srcChannelSliceTensor);
assignmentOp.SetOperand("dst slices", dstSlicesTensor);
assignmentOp.SetOperand("dst channel slice", dstChannelSliceTensor);
assignmentOp.SetResult("dst", dstTensor);
```

### RunModelInferenceOperator 
`RunModelInferenceOperator` is used to encapsulate an NPU operator built by a developer for isolated execution. The numbers of operands and results are dynamically determined according to the NPU operator built by the developer. A developer should use the QNN compilation tool to generate a binary file from their algorithms offline in advance and package it into the APK file, or directly download the file from the network. In use, you need to meet the following requirements:

* Before creating the operator, you must first read or download the algorithm binary file into memory.
* The `operatorInfo` in the `XrSecureMrOperatorCreateInfoPICO` structure should point to an instance of the `XrSecureMrOperatorModelPICO` structure. The variables in this structure are as follows:
   | **Variable**  | **Description** |
   | --- | --- |
   | buffer | Points to the binary file loaded in memory. |
   | bufferSize | The length of the algorithm binary file in memory. |
   | modelName | A unique identification string specified by the developer. |
   | modelInputs | Points to an array of `XrSecureMrOperatorIOMapPICO` with a length of `modelInputCount`, while `modelOutputs` points to an array of `XrSecureMrOperatorIOMapPICO` with a length of `modelOutputCount`. These two arrays are used to inform the SecureMR server that when encapsulating the operator built by the developer, the operands and results to be prepared, as well as their corresponding nodes in the algorithm binary file, are as follows: <br>  <br> * The `encodingType` of `XrSecureMrOperatorIOMapPICO` is used to specify whether the operand or result accepts the FLOAT32 or UINT8 data type. <br> * The `operatorIOName` of `XrSecureMrOperatorIOMapPICO` is used to specify the name of the operand or result, so that the tensor can be bound by the name. <br> * The `nodeName` of `XrSecureMrOperatorIOMapPICO` is used to specify the corresponding node ID of the operand or result in the algorithm binary file. |

### NormalizeOperator
`NormalizeOperator` is used for data normalization, such as subtracting the mean and dividing by the variance. In use, you need to meet the following requirements:

* There are two operands:
   | **Operand** | **Required** | **Description** |
   | --- | --- | --- |
   | operand0 | Yes | The source tensor for normalization. It has no specific requirements. |
   | alpha_beta | No | Used to specify the α and β parameters for normalization. It is required to be of the `Scalar` type, with a data type of 1-channel float32/64 and a shape of `(2,)`. |
* There is one required output `result`. Its types (tensor type, data type, channel, etc.) need to be consistent with those of `operand0`.
* When creating this operator, the `normalizeType` needs to be passed in. The enumeration values are as follows:
   ```C#
   enum NormalizeType
   {
       L1,  // Points to the L1 normalization in OpenCV.
       L2, // Points to the L2 normalization in OpenCV.
       Inf, // Points to the INF normalization in OpenCV.
       MinMax // Points to the Min-Max normalization in OpenCV.
   }
   ```

An example is as follows:
```C#
var normalizeConfig = new NormalizeConfiguration(NormalizeType.L1)
var normalizeOp = currentPipeline.CreateOperator<NormalizeOperator>(normalizeConfig);
normalizeOp.SetOperand("operand0", tensor0);
normalizeOp.SetOperand("alpha_beta", tensor1);
normalizeOp.SetResult("result", tensorX);
```

### CameraSpaceToWorldOperator
`CameraSpaceToWorldOperator` is used to obtain the transformation matrix from the VST camera coordinate system to the Local world coordinate system in OpenXR at a specified moment. In use, you need to meet the following requirements:

* There is one required operand named `timestamp`. It is used to provide the camera timestamp. It must be a tensor of the `Timestamp` type.
* There are two optional results:
   | **Result** | **Description** |
   | --- | --- |
   | right | The transformation matrix from the right-eye VST camera coordinate system to the OpenXR Local coordinate system. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(4, 4)`. |
   | left | The transformation matrix from the left-eye VST camera coordinate system to the OpenXR Local coordinate system. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(4, 4)`. |

An example is as follows:
```C#
var cameraSpaceToWorldOp = currentPipeline.CreateOperator<CameraSpaceToWorldOperator>();
cameraSpaceToWorldOp.SetOperand("timestamp", timestampTensor);
cameraSpaceToWorldOp.SetResult("right", rightTensor);
cameraSpaceToWorldOp.SetResult("left", leftTensor);
```

### RectifiedVstAccessOperator
`RectifiedVstAccessOperator` is used to obtain the VST images of the left and right eyes, as well as the corresponding camera intrinsic matrices and camera timestamps.
This operator does need an operand. There are four optional results:
| **Result** | **Description** |
| --- | --- |
| right image | The VST RGB image of the right eye. It is required to be of the `Matrix` type, with a data type of 3-channel UINT8. The shape must be `(W, H)`. `W` and `H` must be consistent with the width and height of the VST image set when creating the framework handle. |
| left image | The VST RGB image of the left eye. It is required to be of the `Matrix` type, with a data type of 3-channel UINT8. The shape must be `(W, H)`. `W` and `H` must be consistent with the width and height of the VST image set when creating the framework handle. |
| timestamp | The camera timestamp. It is required to be of the `Timestamp` type. |
| camera matrix | The camera intrinsic matrix, which can be used for `SolvePNP`. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64. The shape must be `(3, 3)`. |
An example is as follows:
```C#
var rectifiedVstAccessOp = currentPipeline.CreateOperator<RectifiedVstAccessOperator>();
rectifiedVstAccessOp.SetResult("right image", rightImageTensor);
rectifiedVstAccessOp.SetResult("left image", leftImageTensor);
rectifiedVstAccessOp.SetResult("timestamp", timestampTensor);
rectifiedVstAccessOp.SetResult("camera matrix", cameraMatrixTensor);
```

### ArgmaxOperator
`ArgmaxOperator` is used to find the index corresponding to the maximum value of each channel. In use, you need to meet the following requirements:

* There is one required operand named `operand`. It is a source tensor and can be of any type.
* There is one required result named `result`. It is used to store the index of the maximum value of each channel. The data type must be an integer type with N channels ( `N` represents the dimension of the `operand`), and the shape must be `(C,)`, `(C, 1)`, or `(1, C)` (`C` represents the number of channels of the data type of `operand`).

An example is as follows:
```C#
var argmaxOp = currentPipeline.CreateOperator<ArgmaxOperator>();
argmaxOp.SetOperand("operand", operandTensor);
argmaxOp.SetResult("result", resultTensor);
```

You can understand this operator through the following specific example:
The operand is a (2, 2) Mat with a data type of 3-channel float, and the correspondence between the index and the data is as follows:

* `Index[0, 0]: { 3.0, 1.3, 0.68}`
* `Index[0, 1]`: `{5.7, 2.6, 0.52}`
* `Index[1, 0]`: `{2.2, -5.7, 0.01}`
* `Index[1, 1]`:`{6.0, -0.01, 0.30}`

Note that this Mat has a total of four data points arranged in two rows and two columns, and each data point is a 3-channel floating-point number.
The result of its argmax can be a Mat with 2 channels and a shape of (3, 1). This Mat contains three data points, and each data point corresponds to the index of the maximum value in one channel of the operand. Meanwhile, since each index of the operand consists of two integers, the row index and the column index, the data type of the result should be a 2-channel integer type. The result should be:

* `{1, 1}` --- The maximum value on channel 0 is 6.0, and the corresponding index is `[1, 1]`.
* `{0, 1}`--- The maximum value on channel 1 is 2.6, and the corresponding index is `[0, 1]`.
* `{0, 0}`--- The maximum value on channel 2 is 0.68, and the corresponding index is `[0, 0]`.

### ConvertColorOperator
`ConvertColorOperator` is used for color space conversion. This operator is a wrapper for the `cvtColor` function in OpenCV. In use, you need to meet the following requirements:

* There is one required operand named `src`. It must be of the `Matrix` type. The data type should be consistent with the input data type requirements of the `cvtColor` function in OpenCV. The shape should be `(W, H)`.
* There is one required result named `dst`. It must be of the `Matrix` type. The data type should be consistent with the input data type requirements of the `cvtColor` in OpenCV. The shape should be `(W, H)`, consistent with operand `src`.
* When creating this operator, you need to pass in the `int` value corresponding to the color conversion enumeration value. For details, refer to [opencv color conversions](https://docs.opencv.org/3.4/d8/d01/group__imgproc__color__conversions.html).

An example is as follows:
```C#
var convertColorConfig = new ConvertColorConfiguration(13)
var convertColorOp = currentPipeline.CreateOperator<ConvertColorOperator>(customizedCompareConfig);
convertColorOp.SetOperand("src", srcTensor);
convertColorOp.SetResult("dst", dstTensor);
```

### SortVectorOperator
`SortVectorOperator` is used to sort one-dimensional vectors. In use, you need to meet the following requirements:

* There is one required operand named `operand0`. It is used to specify the tensor to be sorted. It is required to be of the `Scalar` type, with any data type of 1-channel. The shape must be `(N,)`.
* There are two optional results:
   | **Result** | **Description** |
   | --- | --- |
   | sorted | The sorted vector. It is required to be of the `Scalar` type, with any data type of 1-channel. The shape must be `(N,)`. |
   | indices | The index of each element in the sorted vector within `operand0`. It is required to be of the `Scalar` type, with an integer data type of 1-channel. The shape must be `(N,)`. |

An example is as follows:
```C#
var sortVectorOp = currentPipeline.CreateOperator<SortVectorOperator>();
sortVectorOp.SetOperand("operand0", operand0Tensor);
sortVectorOp.SetResult("sorted", sortedTensor);
sortVectorOp.SetResult("indices", indicesTensor);
```

### InversionOperator
`InversionOperator` is used to calculate the inverse matrix of a matrix. This operator is a wrapper for the `Mat::inv` method in OpenCV. In use, you need to meet the following requirements:

* There is one required operand named `operand`. It must be of the `Matrix` type. The data type must be 1-channel float32/64. The shape must be `(W, W)` (i.e., a square matrix).
* There is one required result named `result`. It must be of the `Matrix` type. The data type must be consistent with that of `operand`. The shape must be `(W, W)`.

An example is as follows:
```C#
var inversionOp = currentPipeline.CreateOperator<InversionOperator>();
inversionOp.SetOperand("operand", operandTensor);
inversionOp.SetResult("result", resultTensor);
```

### GetTransformMatrixOperator
`GetTransformMatrixOperator` is used to generate a 4x4 transformation matrix through rotation, scaling, and translation vectors. In use, you need to meet the following requirements:

* There are three operands:
   | **Operand** | **Required** | **Description** |
   | --- | --- | --- |
   | rotation | Yes | Rotation vector (represented in axis-angle notation). It is required to be of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(1, 3)` or `(3, 1)`. |
   | translation | Yes | Translation vector. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(1, 3)` or `(3, 1)`. |
   | scale | No | Scaling vector. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(1, 3)` or `(3, 1)`. |
* There is one required result named `result`. It is required to be of the `Matrix` type, with a data type of 1-channel float32/64 and a shape of `(4, 4)`.

An example is as follows:
```C#
var getTransformMatrixOp = currentPipeline.CreateOperator<GetTransformMatrixOperator>();
getTransformMatrixOp.SetOperand("rotation", rotationTensor);
getTransformMatrixOp.SetOperand("translation", translationTensor);
getTransformMatrixOp.SetOperand("scale", scaleTensor);
getTransformMatrixOp.SetResult("result", resultTensor);
```

### SortMatrixOperator
`SortMatrixOperator` is used to sort a matrix by rows or columns. This operator is a wrapper for the `sortMat` function in OpenCV. In use, you need to meet the following requirements:

* There is a required operand named `operand`, which is used to specify the tensor to be sorted. It is required to be of the `Matrix` type, with a data type of any 1-channel type. The shape must be `(W, H)`.
* There are two optional results:
   | **Result** | **Description** |
   | --- | --- |
   | sorted | A vector sorted by rows or columns. It is required to be of the `Matrix` type, with a data type of any 1-channel type that is consistent with that of `operand`. The shape must be `(W,H)`. |
   | indices | The index of each element in the sorted vector within the rows/columns of `operand`. It is required to be of the `Matrix` type, with a data type of 1-channel integer. The shape must be `(W, H)`. |
* When creating an operator, you need to set whether to sort by rows or columns. The enumeration values are as follows:
   ```C#
   public enum MatrixSortType
   {
       Column, // Sort by columns.
       Row, // Sort by rows.
   }
   ```

An example is as follows:
```C#
var sortMatrixOpConfig = new SortMatrixOpConfiguration(MatrixSortType.Row)
var sortMatrixOp = currentPipeline.CreateOperator<SortMatrixOperator>(sortMatrixOpConfig);
sortMatrixOp.SetOperand("operand", operandTensor);
sortMatrixOp.SetResult("sorted", sortedTensor);
sortMatrixOp.SetResult("indices", indicesTensor);
```

### SwitchGltfRenderStatusOperator
`SwitchGltfRenderStatusOperator` is used to start or stop rendering a certain glTF model. This operator has four operands:
| **Operand** | **Required** | **Description** |
| --- | --- | --- |
| gltf | Yes | Target glTF model tensor. It is required to be a tensor of the `Gltf` type. |
| world pose | No | * If it is not empty, the specified glTF model will start to be rendered. This operand should provide the initial world coordinates of the glTF model in the OpenXR Local coordinate system. <br> * If it is empty, the rendering of the glTF model will stop. |
| visible | No | Used to determine whether the glTF model is visible. If the tensor is non-zero, the model is visible and the rendering starts; otherwise, the rendering of the model will be stopped. The default state is visible. |
| view locked | No | Used to determine whether the glTF model follows the view space. If the tensor is non-zero, the model uses OpenXR's view space as the reference frame; otherwise, it uses OpenXR's local space as the reference frame. |
The relationship between the operand settings and the model visibility is shown in the following table:
| **`world pose`** | **`visible`** | **Model visibility** |
| --- | --- | --- |
| Not null | Null | Visible, rendered according to the pose specified by `world pose` |
|  | Non-zero tensor | Visible, rendered according to the pose specified by `world pose` |
|  | Zero tensor | Invisible |
| Null | Null | Invisible <br>  |
|  | Non-zero tensor |  |
|  | Zero tensor |  |
An example is as follows:
```C#
var switchGltfRenderStatusOp = currentPipeline.CreateOperator<SwitchGltfRenderStatusOperator>();
switchGltfRenderStatusOp.SetOperand("gltf", gltfTensor);
switchGltfRenderStatusOp.SetOperand("world pose", world poseTensor);
```

### UpdateGltfOperator
`UpdateGltfOperator` is used to update a certain parameter of the glTF model and is applied to data-driven animation. The glTF model must have started rendering via `SwitchGltfRenderStatusOperator`; otherwise, this operator will not take effect. The enumeration and usage instructions of the attributes are as follows:
| **Attribute enumeration**  | **Usage instructions** |  | **Operands** |
| --- | --- | --- | --- |
| TEXTURE | Used to update the content of an existing glTF texture. Different from LOAD TEXTURE, LOAD TEXTURE operator is used to load a new texture from memory. |  | * `gltf`: The target glTF material. It must be a `Gltf` tensor. <br> * `texture ID`: The ID of the texture to be updated. It must be a 1-channel UINT16 `Scalar` tensor with a shape of `{N, }` (`N` represents the number of textures to be updated). <br> * `rgb image`: New texture content. It must be a 3/4-channel UINT8 `Matrix` tensor with a shape of `{N, HEIGHT, WIDTh}` or `{HEIGHT, WIDTH}` (only when `N==1` ). The `WIDTH` and `HEIGHT` must be consistent with the current size of the specified texture. |
| ANIMATION | Used to control the preset animations in glTF. |  | * `gltf`: The target glTF material. It must be a `Gltf` tensor. <br> * `animation ID`: The sequence number of the target animation. It must be a 1-channel UINT16 `Scalar` tensor with a shape of `{1, }`. The sequence number value must be a valid animation sequence number in glTF. <br> * `animation timer`: Adjusts the time of the animation. It must be a 1-channel FLOAT32/64 `Scalar` tensor with a shape of `{1, }`. The animation will start playing from the moment obtained by taking the remainder of the timer value divided by the animation duration. |
| WORLD_POSE | Used to update the pose of the glTF in the world coordinate system. |  | * `gltf`: The target glTF material. It must be a `Gltf` tensor. <br> * `world pose`: The updated pose matrix in the world coordinate system. It must be a 1-channel FLOAT32/64 `Matrix` tensor with a shape of `{4, 4}`. |
| LOCAL_TRANSFORM | Used to update the local pose of a specified node in the glTF. |  | * `gltf`: The target glTF material. It must be a `Gltf` tensor. <br> * `node ID`: The ID of the node to be updated. It must be a 1-channel UINT16 `Scalar` tensor with a shape of `{N, }` (`N` represents the number of nodes to be updated). <br> * `transform`: The new pose matrix (4x4) for each node. It must be a 1-channel FLOAT32/64 `Matrix` tensor with a shape of `{N, 4, 4}` or `{4, 4}` (only when `N == 1`). |
| METERIAL_METALLIC_FACTOR | Used to modify the properties of materials in glTF. <br>  | Modifies the metallic value (float) | * `gltf`: The target glTF material. It must be a `Gltf` tensor. <br> * `material ID`: The ID of the material to be updated. It must be a 1-channel UINT16 `Scalar` tensor with a shape of `{N, }` (`N` represents the number of materials to be updated). <br> * `value`: New material attribute value. The shape should be `{N, }` (`N` represents the number of materials to be updated). The tensor type requirements are as follows: <br>    * For the subtypes marked as float on the left, it must be a 1-channel FLOAT32/64 `Scalar` tensor. <br>    * For the subtypes marked as RGBA on the left, it must be a 4-channel UINT8 `Color` tensor. <br>    * For the subtypes marked as texture ID on the left, it must be a 1-channel UINT16 `Scalar` tensor. <br>  <br>  |
| METERIAL_ROUGHNESS_FACTOR |  | Modifies the roughness value (float) |  |
| METERIAL_OCCLUSION_MAP_TEXTURE |  | Replaces the ID of the texture used as the occlusion map |  |
| METERIAL_BASE_COLOR_FACTOR |  | Modifies the base color (RGBA) |  |
| METERIAL_EMISSIVE_FACTOR |  | Modifies the emissive color (RGBA) |  |
| METERIAL_EMISSIVE_STRENGTH |  | Modifies the emissive intensity value (float) |  |
| METERIAL_EMISSIVE_TEXTURE |  | Replaces the ID of the texture used as the emissive map |  |
| METERIAL_BASE_COLR_TEXTURE |  | Replaces the ID of the texture used as the base color |  |
| METERIAL_NORMAL_MAP_TEXTURE |  | Replaces the ID of the texture used as the normal map |  |
| METERIAL_METALLIC_ROUGHNESS_TEXTURE |  | Replaces the ID of the texture used as the metallic-roughness map |  |
Additional notes:

* Node ID is the serial number (starting from 0) of the corresponding node in the glTF file and the nodes array.
* In glTF, the relationships among nodes, materials, and textures are as follows:
   * A glTF file can contain multiple nodes, and each node can contain multiple mesh primitives.
   * Each mesh primitive is bound to a material. A material is a preset set of attributes. The attribute can be a single factor (such as metallic) or a texture ID (such as a normal map).
   * Currently, dynamically adding or modifying mesh primitives or materials is not supported. However, the attribute values of specified materials can be modified through the sub-operators in the above table.
   * Material ID can be found in the glTF file and is clearly written in the meshes array of the glTF.

```C#
public enum GltfOperatorAttribute
{
    Texture,
    Animation,
    WorldPose,
    LocalTransform,
    MaterialMetallicFactor,
    MaterialRoughnessFactor,
    MaterialOcclusionMapTextureFactor,
    MaterialBaseColorFactor,
    MaterialEmissiveFactor,
    MaterialEmissiveStrengthFactor,
    MaterialEmissiveTextureFactor,
    MaterialBaseColorTextureFactor,
    MaterialNormalMapTextureFactor,
    MaterialMetallicRoughnessTexture,
}
```

### RenderTextOperator
`RenderTextOperator` is used to draw text on the texture of the glTF. This operator requires the following six required operands to be set:
| **Operand** | **Description** |
| --- | --- |
| text | Any tensor. If it is a 1-channel UINT8 or INT8 `Scalar` tensor, the content of the tensor will be treated as a UTF-8 encoded string. If it is a tensor of other types, the original values of the tensor will be directly printed. For example, if you input a UINT8 `Scalar` tensor with values `{110, 105, 114, 114, 117}`, the string "HELLO" will be rendered at the end; if you input a `Matrix` tensor with exactly the same content, the rendering result will be "110 105 114 114 117". |
| start | The starting XY coordinates. According to the requirements of the Android Canvas, it refers to the baseline at the bottom-left corner of the first character. It must be `Point2` of float32/64 type with a shape of `{1,}`. X and Y should be relative values of the length and width of the canvas within the range of 0 to 1. |
| colors | The text color and background color. It must be a `Color` tensor of 4-channel UINT8 type, with a shape of `{2,}` (the first element is the text color, and the second is the background color). |
| gltf | Target glTF asset. It must be a `Gltf` tensor. |
| texture ID | The ID of the target texture for text drawing. It must be a `Scalar` tensor of 1-channel UINT16 type, with a shape of `{1, }`. It must be the ID of an existing texture in the glTF (including those newly added through LOAD TEXTURE). |
| font size | The font size, with the unit of pt. It must be a `Scalar` tensor of 1-channel float32/64 type, and the shape is required to be `{1, }`. |
When creating the operator, you need to set the font type, country code, and the length and width of the canvas.
```C#
// Font type enumeration.
public enum FontTypeFace
{
    Default,
    SansSerif,
    Serif,
    MonoSpace,
    Bold,
    Italic
}
```

An example is as follows:
```C#
var renderTextOpConfig = new RenderTextConfiguration(FontTypeFace.Bold,"zh-cn",width,height);
var renderTextOp = currentPipeline.CreateOperator<RenderTextOperator>(renderTextOpConfig);
sortMatrixOp.SetOperand("text", textTensor);
sortMatrixOp.SetOperand("start", startTensor);
sortMatrixOp.SetOperand("gltf", gltfTensor);
sortMatrixOp.SetOperand("colors", colorsTensor);
sortMatrixOp.SetOperand("texture ID", textureIDTensor);
sortMatrixOp.SetOperand("font size", fontSizeTensor);
```

### LoadTextureOperator
`LoadTextureOperator` is used to create a new texture for the glTF model from a tensor. In use, you need to meet the following requirements:

* There are two required operands as follows:
   | **Operand** | **Description** |
   | --- | --- |
   | gltf | Target glTF model tensor. It is required to be a tensor of the `Gltf` type. |
   | rgb image | The source image of the newly added texture for the glTF model. It is required to be of the `Matrix` type, with a data type of 3/4-channel UINT8 (corresponding to RGB and RGBA respectively), and the shape can only have two dimensions. |
* There is one required result named `texture ID`. It is used to store the index of the newly added texture to the glTF model. In this way, the texture can be bound as the map of a material through `UpdateGltfOperator`.

An example is as follows:
```C#
var loadTextureOp = currentPipeline.CreateOperator<LoadTextureOperator>();
loadTextureOp.SetOperand("gltf", gltfTensor);
loadTextureOp.SetOperand("rgb image", rgbImageTensor);
loadTextureOp.SetResult("texture ID", textureIdTensor);
```

###   vd

* Perform singular value decomposition of the matrix.
* This operator mandatorily requires an operand:
   * `src`: Must be a two-dimensional matrix-type tensor.
* There are three optional results: `w`, `u`, and `vt`. All must be tensors of the two-dimensional matrix type, corresponding to the results in the SVD method of OpenCV.

###   Norm

* Computational norm for tensors (default is L2 norm).
* This operator mandatorily requires an operand:
   * `operand0`: Must be a tensor of any type except gltf.
* There is a result named `result0`, which must be a tensor of any type except gltf, must have only one channel, and must contain only one element.

###   Swap Hwc Chw

* Transfer content from an HWC tensor (that is, a tensor with two dimensions: HxW and C channels) to a CHW tensor (that is, a tensor with three dimensions: CxHxW and one channel), or transfer content from a CHW tensor to an HWC tensor.
* This operator mandatorily requires an operand and a result:
   * `operand0`
   * `result0`
* If one is HWC, the other must be CHW. HWC must be a tensor of one matrix, with two dimensions (H, W) and C channels, while CHW must be a tensor of one matrix, with three dimensions (C, H, W) and one channel.
* In addition, the last two numbers of the dimensions of CHW and HWC tensors must match.

### Javascript
Used to execute JavaScript scripts submitted by developers. Input and output are defined by the developer's JS script.
Example:
```C#
string script =
"var in_1;\n"
"var in_2;\n"
"var out_result;\n"
"var sum2 = 0;\n"
"var multi1 = 1;\n"
"for(let i = 0; i < in_2.length; i++)\n"
"{\n"
"   sum2 += in_2[i];\n"
"}\n"
"for(let i = 0; i < in_1.length; i++)\n"
"{\n"
"   multi1 *= in_1[i];\n"
"}\n"
"if (multi1 < sum2)\n"
"{\n"
"   out_result[0] = 2;\n"
"}\n"
"else if (multi1 === sum2)\n"
"{\n"
"   out_result[0] = 0;\n"
"}\n"
"else\n"
"{\n"
"   out_result[0] = 1;\n"
"}";

var javaScriptOpConfig = new JavascriptOperatorConfiguration(script);
var javaScriptOp = currentPipeline.CreateOperator<JavascriptOperator>(javaScriptOpConfig);
javaScriptOp.SetOperand("in_1",inputTensor1);
javaScriptOp.SetOperand("in_2",inputTensor2);
javaScriptOp.SetOperand("out_result",outputTensor);
```

Note that:
Unlike other operators, whose operand (Input) and result (Output) names and indexes are predefined, ... However, for the JavaScript Operator, the operand and result are determined by the global `var` variables defined in the submitted JavaScript code, and their names and order are consistent with the global variables declared in the code. Only global `var` variables in JavaScript that are uninitialized and not `const` will be recognized as operand or result.
For example, in the following example, only `variable1`, `variable2`, and `variable3` can be used as operand or result; `sum2`, since it has already been defined, cannot be used as operand or result. In the JavaScript Operator, each global `var` variable that is not predefined can be mapped as an operand, result, or both as operand and result.
```JavaScript
var variable1;
var variable2;
var variable3;
var sum2 = 0;
let multi1 = 1
for(let i = 0; i < variable2.length; i++)
{
   sum2 += variable2[i];
}
for(let i = 0; i < variable1.length; i++)
{
    multi1 *= variable1[i];
}
if (multi1 < sum2)
{
    variable3[0] = 2;
}
else if (multi1 === sum2)
{
    variable3[0] = 0;
}
else
{
    variable3[0] = 1;
}
```


# --- END: Use different operators.md ---



# --- BEGIN: Use the dynamic texture.md ---

`GlobalTensor` declared as a dynamic texture can be loaded as a GPU texture in the pipeline with zero-copy, for use by glTF tensors.
With dynamic texture, SecureMR-rendered glTF scenes can update their material maps with extremely low latency, making them especially suitable for the following scenarios:

* The map originates from a camera video stream
* The map content needs to be updated in real time by the MR pipeline

## Limitations
Only `GlobalTensor` or `PipelinePlaceholder` can be declared as a dynamic texture.
## Declaration method for dynamic texture
Dynamic texture is declared via relevant enumeration values in `TensorDataType` and `TensorUsage`.
Only when both `TensorDataType` and `TensorUsage` meet the following requirements will the `GlobalTensor` be considered a dynamic texture.

* **TensorDataType**
   The `DataType` of `GlobalTensor` must be set to one of the following:
   * `TensorDataType.DynamicTextureByte`
   * `TensorDataType.DynamicTextureFloat`
   This setting declares that the underlying data of the tensor has dynamic texture semantics and determines the data format when creating the texture on the GPU side.
* **TensorUsage**
   At the same time, the `GlobalTensor`'s `Usage` must be set to `TensorUsage.DynamicTexture`.
   This setting clarifies the purpose of the tensor in the pipeline, indicating that it will be used to create and bind a dynamic texture for subsequent operators related to texture and material.

## Placeholder rules
As with all `GlobalTensor`, to read or write a dynamic texture type `GlobalTensor` in the pipeline, the following operations must be completed:

* Declare the corresponding dynamic texture placeholder
* Explicitly reference the `GlobalTensor` when submitting the pipeline

## Texture creation and update mechanism
In the pipeline, you can use `Operator Load_Texture` to create a texture from the input tensor. The behavior depends on the type of the input tensor:

* **Non-dynamic texture tensor**
   * The created texture is a static texture.
   * The texture content is consistent with the data in the tensor at creation.
   * To update the texture content, you must explicitly call `Operator Update_Texture` to copy the tensor data to the texture again.
* **Dynamic Texture Tensor**
   * The created texture will be bound to the tensor as a dynamic texture.
   * The texture and the underlying data of the tensor remain bound.
   * When the data in the tensor changes, the texture will be updated automatically.
   * It is not necessary, nor is it allowed, to call `Operator Update_Texture`.

Calling Operator Update_Texture` on a tensor already bound as a dynamic texture is not supported`. To update the content of a dynamic texture, you must write directly to the data of the tensor it is bound to.

## glTF material update
After binding the dynamic texture tensor as a dynamic texture via `Operator Load_Texture`, you can use `Operator UpdateMaterial` to apply the texture to the following properties of the glTF material (including but not limited to):

*  `BaseColor`
*  `NormalMap`
* Other supported material map channels


# --- END: Use the dynamic texture.md ---



# --- BEGIN: Use the hand interactables of the XR Interaction toolkit.md ---

The XR Interaction Toolkit plugin provides a sample project called "Hands Interaction Demo" that showcases hand interactions. This article explains how to adopt the interaction methods provided by this sample project in your Unity project, enabling interaction between hands and 3D objects.
## Expected effect
Use hands to grab, move, scale objects, and more.

      <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/535de67db6c645e8b693426ca78c3c1e~tplv-goo7wpa0wc-image.image></video>

## Requirements

* PICO device models: PICO Neo3 and PICO 4 series
* PICO device's system version: 5.12.0 or later
* XR Interaction Toolkit's version: 2.3.0 - 2.6.2 or 3.x (you can go to **Window** > **Package Manager** > **Unity Registry** to install or update this plugin)

## Procedure
### Step 1: Install the XR Hands package and import the Hand Visualizer sample
The implementation of the Hand Interaction Demo requires Unity's XR Hands package and the Hand Visualizer sample.

1. In the Unity Editor, open an existing project or create a new one.
2. Go to **Window** > **Package Manager**.
3. In the **Package Manager** window, install the XR Hands package into your project. Refer to [Unity's documentation](https://docs.unity3d.com/Packages/com.unity.xr.hands@1.2/manual/project-setup/install-xrhands.html) for detailed instructions.
4. Import the **Hand Visualizer** sample provided by the XR Hands package.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d326e87ac4dc411eb1243faa1f3455fd~tplv-goo7wpa0wc-image.image)

### Step 2: Import the samples of XR Interaction Toolkit
In the **Package Manager** window, import the **Starter Assets** and **Hands Interaction Demo** samples provided by the XR Interaction Toolkit.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28a055a0356242098daa89a5ef8067ab~tplv-goo7wpa0wc-image.image" width="800px" />

### Step 3: Set up default input actions

1. Go to the **Project** window.
2. Under the /Assets/Samples/XR Interaction Toolkit/{version_number}/Starter Assets directory, click **XRI Default Input Actions** to open it.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5e5bd757a494b8391a092250ae4eb15~tplv-goo7wpa0wc-image.image)
   The **XRI Default Input Action (Input Actions)** window appears.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eedc598a47944959a12c1cb4606caae7~tplv-goo7wpa0wc-image.image)
3. Set up default input actions for the left hand:
   1. On the left **Action Maps** list, select **XRI LeftHand**.
   2. On the **Actions** list in the middle, click **+** > **Add Binding** next to the **Aim Position**, **Aim Rotation**, and **Aim Flags** actions.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef789b8170f14fc0852e99e46a11a1ac~tplv-goo7wpa0wc-image.image)
   3. In the **Path** parameter on the right **Binding Properties** pane, bind the following input actions to the above-mentioned actions.
      Binding path: Tracked Device/PICO Aim Hand/PICO Aim Hand (LeftHand)
      | **Action Name** | **PICO Input Actions to Bind** | **Corresponding Path** |
      | --- | --- | --- |
      | Aim Position | devicePosition [LeftHand Pico Aim Hand] | <PicoAimHand>{LeftHand}/devicePosition |
      | Aim Rotation | deviceRotation [LeftHand Pico Aim Hand] | <PicoAimHand>{LeftHand}/deviceRotation |
      | Aim Flags | aimFlags [LeftHand Pico Aim Hand] | <PicoAimHand>{LeftHand}/aimFlags |
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ced5ea8e912443039e205ddf17e4eb53~tplv-goo7wpa0wc-image.image)
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bf19b6bc28d4f178e86c88a92b8c212~tplv-goo7wpa0wc-image.image)
      In addition to searching for the PICO input actions to bind from the **Path** list, you can also click the **T** button on the far right of the **Path** parameter to enable text input, enter the corresponding path for a PICO input action given in the above table, and press the Enter key on your keyboard to bind the PICO input action.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a6ab6da915640cdb5e6e4970ad6574a~tplv-goo7wpa0wc-image.image)
   4. Bind PICO's input actions to the **Select**, **Select Value**, **UI Press**, and **UI Press Value** actions of **XRI LeftHand Interaction**. You can search for the target PICO input action from the **Path** list, or click the **T** button on the far right of the **Path** parameter to enable text input, enter the corresponding path for a PICO input action given in the following table, and press the Enter key on your keyboard to bind the PICO input action.
      | **Action Name** | **PICO Input Actions to Bind** | **Corresponding Path** |
      | --- | --- | --- |
      | Select | indexPressed [LeftHand Pico Aim Hand] | <PicoAimHand>{LeftHand}/indexPressed |
      | Select Value | pinchStrengthIndex [LeftHand Pico Aim Hand] | <PicoAimHand>{LeftHand}/pinchStrengthIndex |
      | UI Press | indexPressed [LeftHand Pico Aim Hand] | <PicoAimHand>{LeftHand}/indexPressed |
      | UI Press Value | pinchStrengthIndex [LeftHand Pico Aim Hand] | <PicoAimHand>{LeftHand}/pinchStrengthIndex |
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3348944663e463f930aa4f3f759207e~tplv-goo7wpa0wc-image.image)
4. Use the same steps to set up default input actions for the right hand. 
   Binding path: Tracked Device/PICO Aim Hand/PICO Aim Hand (RightHand)
   PICO's input actions for **XRI RightHand**:
   | **Action Name** | **PICO Input Actions to Bind** | **Corresponding Path** |
   | --- | --- | --- |
   | Aim Position | devicePosition [RightHand Pico Aim Hand] | <PicoAimHand>{RightHand}/devicePosition |
   | Aim Rotation | deviceRotation [RightHand Pico Aim Hand] | <PicoAimHand>{RightHand}/deviceRotation |
   | Aim Flags | aimFlags [RightHand Pico Aim Hand] | <PicoAimHand>{RightHand}/aimFlags |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e72c4840e714752a0e10a8148cd46b4~tplv-goo7wpa0wc-image.image)
   PICO's input actions for **XRI RightHand Interaction**:
   | **Action Name** | **PICO Input Actions to Bind** | **Corresponding Path** |
   | --- | --- | --- |
   | Select | indexPressed [RightHand Pico Aim Hand] | <PicoAimHand>{RightHand}/indexPressed |
   | Select Value | pinchStrengthIndex [RightHand Pico Aim Hand] | <PicoAimHand>{RightHand}/pinchStrengthIndex |
   | UI Press | indexPressed [RightHand Pico Aim Hand] | <PicoAimHand>{RightHand}/indexPressed |
   | UI Press Value | pinchStrengthIndex [RightHand Pico Aim Hand] | <PicoAimHand>{RightHand}/pinchStrengthIndex |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b670e4dc48934a19975a705c189f2cd5~tplv-goo7wpa0wc-image.image)

### Step 4: Open the Hands**DemoScene**
In the Project window, go to the /Assets/Samples/XR Interaction Toolkit/{version_number}/Hands Interaction Demo/Runtime directory, and click **HandsDemoScene** to open the scene.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/128737a7518d432fbe5470daa74ff600~tplv-goo7wpa0wc-image.image" width="800px" />

### Step 5: Enable the Hand Tracking functionality for your app and PICO device

1. In the **Hierarchy** window, click **+** > **XR** > **XR Origin (VR)** to add the XR Origin object.
2. Select the **XR Origin** object.
3. In the **Inspector** window, click the **Add Component** button at the bottom, and add the **PXR_Manager (script)** component to the XR Origin object.
4. On the **PXR_Manager (Script)** pane, check the **Hand Tracking** checkbox.
   The Hand Tracking functionality is enabled for your app.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9b2d82bf63549c8b7318a32ea753fb7~tplv-goo7wpa0wc-image.image)
5. Enable the Hand Tracking functionality for your PICO device. For detailed steps, refer to [this article](/en_hand-tracking#a209744d).

## Troubleshooting
### After packaging, the grab model cannot rotate with the rotation of the hand and remains in the initial grab state
If you encounter this issue, please upgrade the XR Interaction Toolkit in the project to the latest version in 2.x, or directly upgrade the SDK to version 3.1.0 or later.


# --- END: Use the hand interactables of the XR Interaction toolkit.md ---



# --- BEGIN: Use the Readback tensor.md ---

Readback tensor is used to enable access to camera-related data. When the application has both Camera and Spatial-Data permissions, it can read the data of a specified GlobalTensor in SecureMR.
## Data reading methods
Currently, two reading methods are supported.
| **Method** | **Restrictions on the target tensor** | **Advantages** | **Disadvantages** |
| --- | --- | --- | --- |
| Read into the application's own CPU memory | Any GlobalTensor that is not a glTF tensor is supported. | Wide applicability; data can be obtained directly. | * Involves cross-process copying, which takes a relatively long time; <br> * The copy is a one-time operation. If the target tensor is updated after copying, the application must perform the copy again to obtain the latest data. |
| Read as GPU resource (Vulkan Image / OpenGL ES Image) | Only `dynamic-texture` type tensor are supported. | * Zero-copy, low overhead; <br> * The obtained Vulkan / OpenGL ES Image is also a dynamic texture, and subsequent updates to the tensor can be synchronized in real time to the corresponding GPU resource. | * Can only be used in GPU rendering scenarios and only as a GPU sampler; <br> * If the application does not perform GPU-to-CPU copying itself, it cannot obtain the latest data of the tensor on the CPU side. |
## Permission requirements
Regardless of the reading method used, the application must have sufficient permissions before calling the Readback tensor interface.
The definition of "sufficient permissions" is as follows:

* **Camera permission**
   If any pipeline in the current SecureMR Framework Session uses a camera-related operator (for example, `Rectified_VST_Access`), regardless of whether the pipeline is actually executed, the application must be granted the Android camera permission: `android.permission.CAMERA`
* **Spatial data permission**
   If any pipeline in the current SecureMR Framework Session uses a spatial data-related operator (for example, `UV_to_Camera_Space`), regardless of whether the pipeline is actually executed, the application must be granted the spatial data permission: `com.picovr.permission.SPATIAL_DATA`

## Related API
To copy the contents of a tensor to the app's own CPU memory, call `tensor.CreateBufferAsync`.


# --- END: Use the Readback tensor.md ---



# --- BEGIN: Where can I download an older version of the SDK_.md ---

If you are developing an app/game for PICO Consumer Store, you need to use the consumer version devices from the PICO Neo 3, PICO 4, PICO 4 Pro, or PICO 4 Ultra series, and use the latest version of the PICO SDK for development. If you encounter technical issues while using the latest SDK, please contact [developer@support.picoxr.com](mailto:developer@support.picoxr.com).
If you are developing on PICO enterprise devices or creating content for enterprise-level industry application scenarios, please contact the PICO enterprise support team ([pico-business-techsupport@bytedance.com](mailto:pico-business-techsupport@bytedance.com)) to obtain an older version of the SDK.


# --- END: Where can I download an older version of the SDK_.md ---



# --- BEGIN: Where can I get the SDK demo_.md ---

You can go to the [PICO GitHub](https://github.com/Pico-Developer) to download the Pico SDK Demo. For detailed instructions on how to use these demos, refer to the "[Samples](/en_space-arena-party)" chapter.


# --- END: Where can I get the SDK demo_.md ---

