# Troubleshooting and FAQ

## Table of Contents
- How to check the serial number of my PICO device_
- How to deal with streaming issues_
- How to deal with _Copyright Verification Failed_ Illegal Signature__
- How to enable users to interact with my app_
- How to get an app's access token_
- How to get DEBUG logs_
- How to make the avatar move_
- How to offline upgrade my PICO device's system version_ 
- How to set read and write access to external files for projects running on PICO 4 Ultra_
- How to view logs_
- Known issues
- Stuck on the loading screen when running a demo built with the Release mode 
- Toubleshooting
- Tracking is disabled after the app loses focus (native UI pops up).
- Troubleshooting guide for PDC
- Troubleshooting
- Why can't my app be recentered by long pressing the Home key_
- Why can't the Preview Tool be connected to a Neo3 device via wired connection_
- Why don't the apps installed on the device appear in the Library's app list_

---



# --- BEGIN: How to check the serial number of my PICO device_.md ---

Turn on your PICO device and go to **Settings** > **General** > **About** to check its serial number.


# --- END: How to check the serial number of my PICO device_.md ---



# --- BEGIN: How to deal with streaming issues_.md ---

For streaming issues, such as how to play with DP mode and exit streaming, refer to [PICO Streaming Help Center](https://flowus.cn/share/a232a446-a2e3-4a1a-a11e-ce47598c1f60).


# --- END: How to deal with streaming issues_.md ---



# --- BEGIN: How to deal with _Copyright Verification Failed_ Illegal Signature__.md ---

When encountering the issue of "Copyright Verification Failed", refer to the following troubleshooting steps:
If the APK file of the app has not been uploaded to the PICO Developer Platform, troubleshoot this issue as follows:

*  Check the app's package name. If you are using the default package name provided by the Unity template, such as com.UnityTechnologies.com.unity.template.urpblank or com.DefaultCompany.VR, change the package name and then repackage it for testing.
* Open your project in the Unity Editor, go to **Edit > Project Settings > Player**, and set the **Scripting Backend** parameter to **IL2CPP**. Then repackage the app for testing.
* You may have triggered the issue where the number of apps with the same signature but different package names has reached its limit. In this case, upload the APK file to the PICO Developer Platform. You only need to upload the APK file and keep it in "Draft" status without submitting it for review.

If the APK file of the app has already been uploaded to the PICO Developer Platform, troubleshoot this issue as follows:

* For app uploaded to the PICO Developer Platform, ensure you are logged in to the headset with a developer account that belongs to your organization during testing.
* Verify that the package name and signature of the new APK file match those of the previously uploaded APK file. If they do not match and you need to use a new package name or signature, you will need to re-upload the APK file for testing.
* Ensure that the app ID you entered matches the app ID of the app you created.


# --- END: How to deal with _Copyright Verification Failed_ Illegal Signature__.md ---



# --- BEGIN: How to enable users to interact with my app_.md ---

The PICO Unity Integration SDK provides the XR Interaction Toolkit to help you achieve user-app interactions such as UI clicking, grabbing objects, and teleportation. In addition, you can also achieve user-app interaction with VRTK4.0 plugin.
Refer to the following examples for details:

* [XR Interaction Toolkit example](https://github.com/Unity-Technologies/XR-Interaction-Toolkit-Examples)
* [VRTK4.0 example](https://github.com/ExtendRealityLtd/VRTK)


# --- END: How to enable users to interact with my app_.md ---



# --- BEGIN: How to get an app's access token_.md ---

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/).
2. Click an app's card to enter its **Overview** screen.
3. From the left navigation panel, select **Platform Service** > **API Test**.
4. In the **Authorization management** field, select the to-be-authorized information, and click the **Get Access Token** button.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50e32f76ac0e4c8bb6dc9bf2326637e2~tplv-goo7wpa0wc-image.image)
   The platform displays the access token in a pop-up window.


# --- END: How to get an app's access token_.md ---



# --- BEGIN: How to get DEBUG logs_.md ---

By default, INFO logs are provides. DEBUG log level is lower than INFO log level. Therefore, if you want to get DEBUG logs, you need to use the `adb shell setprop persist.log.tag V` command to downgrade log level first.


# --- END: How to get DEBUG logs_.md ---



# --- BEGIN: How to make the avatar move_.md ---

Using the Final IK plugin is recommended. You can buy this plugin from [Unity Asset Store](https://assetstore.unity.com/packages/tools/animation/final-ik-14290#description).


# --- END: How to make the avatar move_.md ---



# --- BEGIN: How to offline upgrade my PICO device's system version_ .md ---

If you need to offline upgrade the system version for PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series devices, use the following steps:

1. Connect the PICO device to the PC using a USB cable.
2. Create the “dload” folder in the root directory of the PICO device.
3. Download the latest version of PICO OS from [this website](https://www.picoxr.com/global/software/pico-os).
4. Copy the OS package (do not decompress the zip package) to the “dload” folder. 
5. Disconnect the network to your PICO device. 
6. Go to **Settings** > **System Update** > **Offline Update**, and check for updates.


# --- END: How to offline upgrade my PICO device's system version_ .md ---



# --- BEGIN: How to set read and write access to external files for projects running on PICO 4 Ultra_.md ---

Due to the PICO 4 Ultra series devices using Android 14, when the project's Write Permission is set to External (SDCard) and the Android API Level used is greater than 32, the external file reading method provided by Unity becomes ineffective on PICO 4 Ultra devices. Two solutions are provided for this issue, choose one based on your actual needs.
## Solution 1
This method is more convenient. If there are no special needs, you can directly use the Android API of version 32 or lower within your project.

1. Open your project in the Unity Editor.
2. Go to **Edit** > **Project Settings** > **Player** > **Other Settings**.
3. In the **Identification** section, set the **Target API Level** parameter by choosing one between API Level 29 and API Level 32.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a81840e313548bf82cb2f86b20bea62~tplv-goo7wpa0wc-image.image)

## Solution 2
After requesting permissions using this method, the Project Validation tool within the project may still report errors. You can ignore them.

If you still need to use the Android API of version greater than 32 within your project, you will need to manually request the MANAGE_EXTERNAL_STORAGE permission. This permission cannot be requested directly using Unity's `Permission.RequestUserPermission()` method. Follow these steps to request it:

1. Open your project in the Unity Editor.
2. Go to the **Project** window and create a Java file under the /Assets/Plugins/Android directory.
3. In the Java file, set a package name and class name, and add a method for requesting read/write permissions.
   Below is the code sample:
   ```Java
   package packageName;
   
   import android.app.Activity;
   import android.content.Intent;
   import android.net.Uri;
   import android.os.Build;
   import android.os.Environment;
   import android.provider.Settings;
   
   public class className {
       private Activity mUnityActivity;
       protected static final String TAG = "mUnityActivity";
   
       // Must call in unity to initialize Activity
       public void setUnityActivity(Activity unityActivity) {
           this.mUnityActivity = unityActivity;
       }
   
       public void requestExternalStorage() {
           // Request permissions
           if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.R) {
               if (!Environment.isExternalStorageManager()) {
                   Intent intent = new Intent(Settings.ACTION_MANAGE_APP_ALL_FILES_ACCESS_PERMISSION);
                   Uri uri = Uri.fromParts("package", mUnityActivity.getPackageName(), null);
                   intent.setData(uri);
                   mUnityActivity.startActivity(intent);
               } else {
                   // The user has granted full access permissions, and you can proceed with the relevant operation
               }
           } else {
               // For Android 10 and lower versions, there is no need to request the MANAGE_EXTERNAL_STORAGE permission separately
           }
       }
   }
   ```

4. After implementing the method in the Java file, actively call the relevant methods in Unity where permissions are requested. The following example shows how to request permissions as soon as the app starts:
   ```C#
   ...
   void RequestStoragePermission()
   {
       if (!Permission.HasUserAuthorizedPermission(Permission.ExternalStorageWrite))
       {
           Permission.RequestUserPermission(Permission.ExternalStorageWrite);
       }
       if (!Permission.HasUserAuthorizedPermission(Permission.ExternalStorageRead))
       {
           Permission.RequestUserPermission(Permission.ExternalStorageRead);
       }
   }
   void Awake()
   {
       AndroidJavaObject  javaObj = new AndroidJavaObject("packageName.className");
       AndroidJavaClass jc = new AndroidJavaClass("com.unity3d.player.UnityPlayer");
       AndroidJavaObject jo = jc.GetStatic<AndroidJavaObject>("currentActivity");
       javaObj.Call("setUnityActivity", jo);
       javaObj.Call("requestExternalStorage");
       RequestStoragePermission()；
   }
   ...
   ```

5. Go to **Edit** > **Project Settings** > **Player** > **Publishing Settings** > **Build** and check the **Custom Main Manifest** checkbox.
   The AndroidManifest.xml file is generated under the \Assets\Plugins\Android directory.
6. Add the following content to the app's AndroidManifest.xml file.
   ```XML
   <uses-permission android:name="android.permission.MANAGE_EXTERNAL_STORAGE" />
   ```

   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9218b238e1b4439d960fe2112d0a89d9~tplv-goo7wpa0wc-image.image)


# --- END: How to set read and write access to external files for projects running on PICO 4 Ultra_.md ---



# --- BEGIN: How to view logs_.md ---

You can figure out and analyze issues using logs.

1. Launch the PICO device.
2. For PICO 4 Ultra, go to **Settings** > **Help & Feedback** and toggle the **Log Records** switch; for other device models, go to **Settings** > **General** and toggle the **Log Records** switch. 
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/943c7d9fb6f0412c878174fe76b3c5b2~tplv-goo7wpa0wc-image.image)
3. Restart the PICO device.
4. Reproduce the issue occurred previously.
5. Connect the HMD to the PC with a USB cable.
6. Go to PICO device's storage location on the PC, which is "**Internal shared storage**".
7. Copy the **logcat.log** file in the **logcatch** folder to check out the logs.
   If you need help from the PICO Developer Support team ([developer@support.picoxr.com](mailto:developer@support.picoxr.com)), please provide the complete logcat.log file.


# --- END: How to view logs_.md ---



# --- BEGIN: Known issues.md ---

This article records all the known issues of the PICO Unity Integration SDK. For the known issues and bugfixes of a specific SDK version, refer to the [release notes](/document/updates-unity/).
## Build-related
With Unity 2022, building development builds will cause crashes.
## Fixed Foveated Rendering-related

* If you are using the Universal Render Pipeline (URP) in your project and you enable fixed foveated rendering, fixed foveated rendering may not work.
   * **Cause 1**: At present, fixed foveated rendering is tied to the eye buffer. However, with the introduction of intermediate texture in URP, graphics will be rendered to the intermediate texture first, instead of the eye buffer, which causes fixed foveated rendering to fail.
      **Solution**: Disable post-processing, HDR, and the renderer feature that uses the intermediate texture.
   * **Cause 2**: In URP 10.10.1, the behavior of setting a camera's **Clear Flags** has changed. Specifically, if you choose **Skybox**, the Invalidate setting for Color Attachment will be lost, which will cause the failure of fixed foveated rendering.
      This issue may also exist in versions later than 10.10.1, and what happens in your actual use shall prevail.

      **Solution**: As shown in the figure below, comment out the `CameraClearFlags.Skybox` part in the `GetCameraClearFlag` method of `ScriptableRenderer`, thereby making it return `ClearFlag.All` as well.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9807f4ab1c6d4902898fff8e1bf2123f~tplv-goo7wpa0wc-image.image)
* If you use the Built-in Render Pipeline, you will also need to disable post-processing, otherwise fixed foveated rendering will not work.
* If your project uses OpenGLES graphics API, Gamma color space, and fixed foveated rendering at the same time, subsampling cannot be enabled.

## Application SpaceWarp-related
Using AppSW and content protection together will cause screen jitter and screen ghosting.
## Late Latching-related
Using late latching and compositor layers (overlay/underlay) together will make these layers jitter.
## Spatial Audio-related
For macOS users, if you run any samples from /Packages/Pico Integration/SpatialAudio/Samples in the Unity Editor and press any keyboard key, you might hear some beeping sound. This is caused by a known Unity bug that can be fixed by Unity only. You can click [here](https://issuetracker.unity3d.com/issues/macos-funk-error-sound-plays-when-pressing-any-non-shortcut-key-in-play-mode) to discuss this issue in Unity Community.
## Universal Render Pipeline-related
Before Unity fixes the following issues, please use the Universal Render Pipeline carefully.

* For Unity 2021 or later, setting MSAA while using the Universal Render Pipeline will cause a drop in frame rate.
* For Unity 2020 or later, compared with OpenGLES, adding Vulkan to Graphics API can cause low frame rate, high memory and GPU usage.
* Using Vulkan, URP, and HDR at the same time will cause the underlay layers and VST layer fail to be displayed.
* For Unity 2021 or later, enabling Screen Space Ambient Occlusion (SSAO) in URP Renderer will cause low frame rate, high memory and GPU usage.
* For Unity 2022 and above, if you are using OpenGLES and MultiView in your project and have added the Universal Render Pipeline but are not using it, you should actively remove the URP package, remove the current light and add a new one. Otherwise, the app may crash during runtime.
* If you use Unity6, URP, OpenGL, Multi-pass, and MSAA (not in the Disabled state) simultaneously, it will cause the content of the eye buffer to fail to render. Changing any of the above configurations will resolve this issue.

## Publishing settings-related
Enabling Minify-related options will cause crashes.
## Others
PICO 4 series devices have compatibility issues with apps developed using Unity 6 and Vulkan simultaneously. It is recommended to use Unity 2022 LTS or an earlier version for better compatibility.


# --- END: Known issues.md ---



# --- BEGIN: Stuck on the loading screen when running a demo built with the Release mode .md ---

[minifyRelease](https://docs.unity3d.com/ScriptReference/PlayerSettings.Android-minifyRelease.html) minifies your java code in release configuration, but it can sometimes remove needed code. This problem can be solved by keeping the needed code in the "proguard-user.txt" file. Below are the steps to follow:

1. Go to **Edit** > **Project Settings** > **Player** > **Android Settings** > **Publishing Settings**.
2. Check the **Custom Proguard File** checkbox.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f3bfc084d134e39b892bc884ee5ec48~tplv-goo7wpa0wc-image.image)
   The "proguard-user.txt" file is generated under Assets\Plugins\Android.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70a5be4293cb4823b9f5545a0e1c0bdb~tplv-goo7wpa0wc-image.image)
3. Add the following code in the "proguard-user.txt" file:
   ```Plain Text
   -keep class com.psmart.aosoperation.**{
      *;
   }
   -keep public class com.pxr.xrlib.**{
      public *;
   }
   ```


# --- END: Stuck on the loading screen when running a demo built with the Release mode .md ---



# --- BEGIN: Toubleshooting.md ---

This article lists the errors you may come across while using the Sense Pack and provides solutions for troubleshooting.
| **Error Code** | **Description** | **Solution** |
| --- | --- | --- |
| ERROR_VALIDATION_FAILURE = -1 | Validation failure. | Check if the parameters passed in are correct. |
| ERROR_FUNCTION_UNSUPPORTED = -7 | The function used is not supported. | Check if the functions used are correct. |
| ERROR_FEATURE_UNSUPPORTED = -8 | The feature used is not supported. | Check if the current device model or device system version supports this feature. |
| ERROR_EXTENSION_NOT_PRESENT = -9 | The feature used is not supported. | Check if the current device model or device system version supports this feature. |
| ERROR_SIZE_INSUFFICIENT = -11 | The number of resources has reached the limit. | Resources have exceeded the limit, such as an excessive number of anchors. It is recommended to prompt the user to delete unnecessary anchors. |
| ERROR_HANDLE_INVALID = -12 | Invalid handle. | Check if the handle passed in is correct. |
| ERROR_ANCHOR_SHARING_NETWORK_TIMEOUT = -601 | Network request timeout while sharing anchors. | Network timeout. It is recommended to try uploading the anchors again. If this error occurs multiple times, suggest prompting the user to check their network connection status. |
| ERROR_ANCHOR_SHARING_AUTHENTICATION_FAILURE = -602 | The user hasn't logged in with their PICO account or your app is not registered. | Check if you have added the app's ID in Platform Settings within the Unity Editor. If you have, prompt the user to log in to their PICO account on the PICO device. |
| ERROR_ANCHOR_SHARING_NETWORK_FAILURE = -603 | Network request failure while sharing anchors. | Prompt the user to check their network settings. |
| ERROR_ANCHOR_SHARING_LOCALIZATION_FAIL = -604 | Failed to retrieve anchors while sharing anchors. | Prompt the user to go to a location nearby the anchor sharer and then try to retrieve the anchor again. |
| ERROR_ANCHOR_SHARING_MAP_INSUFFICIENT = -605 | Insufficient environment mapping while sharing anchors. | Prompt the user to look around to retrieve the anchor. |
| ERROR_SPATIAL_SENSING_SERVICE_UNAVAILABLE = -1005 | The system-level spatial sensing service has crashed abnormally. | Recommend promoting the user to restart the app. |
| ERROR_PERMISSION_INSUFFICIENT = -1000710000 | Insufficient permission. | Prompt the user to go to the settings center and authorize the app to access spatial data permissions. |


# --- END: Toubleshooting.md ---



# --- BEGIN: Tracking is disabled after the app loses focus (native UI pops up)..md ---

In Unity, if the new Input System is in use, any event that triggers `OnApplicationFocus(false)` can disable tracking.
The "Tracked Pose Driver (Input System)" component that is attached to the main camera is the component responsible for this functionality. Using the non-input system version doesn't stop tracking as it's not a part of the new input system.
If this happens, you can resolve this by following the steps below:

1. Go to **Edit** > **Project Settings** > **Player** > **Settings for Windows, Mac, Linux**.
2. In the **Resolution and Presentation** section, check the **Run in Background*** checkbox.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2ad0f4eb0ec47a78cc4d92492ad6f8b~tplv-goo7wpa0wc-image.image)
3. Go to **Input System Package** settings, and then set the **Background Behavior** parameter to **Ignore Focus**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5cc6a3dd06b4d1fa4a01085b2bcd6ed~tplv-goo7wpa0wc-image.image)


# --- END: Tracking is disabled after the app loses focus (native UI pops up)..md ---



# --- BEGIN: Troubleshooting guide for PDC.md ---

This article lists the issues you may come across when using the PICO Developer Center and provides solutions accordingly.
## Client issues
This section lists issues related to the PICO Developer Center application.
### PICO device cannot connect to PDC tool

1. Make sure that the PICO device's system version is 5.11.0 or later, and the version of SDK you are using is 2.5.0 or later.
2. Check the USB cable to ensure that there aren't  issues such as loose ports or damaged wiring.

### How to obtain PDC logs
Retrieve PDC logs using the following path:
| **OS** | **Log Paths** |
| --- | --- |
| Windows | * PDC: C:\Users\${user}\AppData\Roaming\PICO Developer Center\logs <br> * Streaming service: <br>    * Project Swan: C:\ProgramData\PICO\PICO Streaming Service <br>    * Other device models: C:\Program Files\Streaming Service\ps_server.log  |
| macOS | * PDC: ~/Library/Application Support/PICO Developer Center/logs <br> * Streaming service: <br>    * Project Swan: ~/Library/Application Support/PICO Streaming Service/swan <br>    * Other device models: ~/Library/Application Support/PICO Streaming Service/ |
### How to obtain PICO device **logs**

1. Launch the PICO device.
2. Go to **Settings** > **General** and toggle the **Log Records** switch.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddd6b986ec8346e79edb10afcf1f5abe~tplv-goo7wpa0wc-image.image)
3. Use the command `adb shell setprop persist.log.tag D` to enable debug logs. Skip this step for PICO 4 Ultra and Project Swan series devices.
4. Use the command `adb pull data/logs` to pull logs to local storage.

## Streaming issues
This section lists issues related to streaming.
### After connecting the PICO 4 Ultra device to the PC, the PDC indicates a streaming error

1. In the headset, go to **Settings** > **General**, toggle the **PICO Connect Auto Discovery** switch off and then toggle it on again to enable the streaming mode for the PDC tool.
2. Restart the PDC tool.

### Streaming service is not correctly installed
Follow the steps below to check if you have installed the streaming service correctly.

1. When the PDC tool is running, open the "Task Manager" (Windows) or "Activity Monitor" (macOS) on your computer.
2. In the **Services** tab, check if the "ps_service" service (Windows) or "ps_server" service (macOS) is in the list. If not, this indicates that you have not installed the streaming service correctly, and it is recommended that you [reinstall the streaming service](/en_download-streaming-service) to solve this issue.




   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/390bc6402e16455baa3ee139001856c3~tplv-goo7wpa0wc-image.image" width="943px" />   




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5725d9dee1c749948fd6821a20f99690~tplv-goo7wpa0wc-image.image" width="376px" />




### Operating system issue
The streaming service requires the Windows 10 operating system or later. Make sure your operating system is an official genuine version of Windows, otherwise it may cause problems such as network authorization blocks by the system firewall and incompatible graphics card drivers. Go to [Microsoft official website ](https://www.microsoft.com/zh-cn/software-download)to download the Windows operating system. Go to the [NVIDIA official website ](https://www.nvidia.cn/geforce/drivers/)or [AMD official website ](https://www.amd.com/zh-hans/support)to download the latest drivers.
### Unable to connect to streaming
There are many reasons why you can't connect to streaming. Follow the steps below to check if the streaming environment is functioning properly:

1. Open the PICO device and enter the Launcher interface.
2. Connect the PICO device to the PC using a USB cable.
3. Search for and open the **Device Manager** on your PC.
   You will see a list of available devices for your computer. When the streaming connection is normal,  the Device Manager should display the following PICO-related devices:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfe21085bcfe4c6081bb7c29746aa656~tplv-goo7wpa0wc-image.image)
   The description for these devices is as follows:
   | **Name** | **Description** |
   | --- | --- |
   | PICO Composite ADB Interface | The interface for debugging. If you enable the developer mode for your PICO device, this device will appear. |
   | PICO Composite Streaming Interface | The interface for Streaming feature. Also named as PICO Accessory Interface. |
   | PICO 4 | This indicates that you can transfer files. Once you switch the PICO device's USB connection mode to "File Transfer," this device will appear. |

If the aforementioned PICO-related devices are not displayed in your Device Manager, refer to the following common issues and their solutions.
#### Be prompted that the streaming service is not installed
If you have installed the streaming service, but PDC still indicates that the streaming service is not installed, follow these steps to troubleshoot the issue:

1. Open the command line tool on your PC and check the language environment of the command line tool.
2. If it is not in English, run command `chcp 437` in the command line tool to switch to the English environment.
3. Restart PDC.

#### "PICO Device" not displayed in Device Manager
If the "PICO Device" entry is not visible in the Device Manager, it indicates that your USB driver is not properly installed, or the device is not successfully connected. Refer to the following two methods to determine if PICO device is successfully connected:

* **Method 1: Search for PICO Device Using PowerShell command**
   Open the **Windows PowerShell** app on your computer with administrator privileges and execute the following command:
   ```C++
   pnputil /enum-devices /ids /connected | select-string "VID_2D40|VID_05C6"
   ```

   If the device is successfully connected, you will observe multiple distinct hardware IDs as shown below. If the device is not successfully connected, you will not be able to see any IDs.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15877047889141b8a6271cf09aad8279~tplv-goo7wpa0wc-image.image)
* **Method 2: View the hardware ID in the Device Manager**
   1. In the Device Manager, check if there are any unrecognized devices (devices with a warning icon in front of the device icon) under **Other devices**. You can also check for new devices under **Universal Serial Bus Devices**.
   2. Right-click on the device, and in the drop-down box, select **Properties**.
   3. In the Properties window, click **Details**.
   4. In the **Details** tab, click the **Properties** drop-down box, select **Hardware Id**, and view the value of hardware ID. If the hardware ID matches the value shown in the image below, the device is indeed the PICO device.

If you determine that the PICO device has successfully connected using the above methods, the issue is likely related to incorrect USB driver installation. The troubleshooting steps are as follows:

1. Navigate to the installation path of "Streaming Runtime Service" at Streaming Runtime Service\drivers\picousb. Right-click on **picousb.inf,** and select **Install**, which requires administrator privileges.
2. After the installation is complete, restart your computer.
3. Open the Device Manager again to confirm if "PICO Device" is now displayed.

#### Periodic flickering refresh in Device Manager
If the Device Manager periodically flickers and refreshes after you connect the USB cable between the PC and the PICO device, it's likely due to unstable signals from the cable or USB port. Consider the following:

* For the USB cable, use a fully functional cable that meets USB 3.2 Gen1 standards or higher.
* For the USB port on the computer, connect to a USB 3.0 or higher port. If you are using a desktop computer, connect the cable to the USB 3.0 or higher ports located on the rear motherboard.

#### Abnormal Device Manager service
If the Device Manager doesn't refresh after connecting the USB cable between the PC and the PICO device, select the top device and then click **Action** > **Scan for hardware changes** to detect hardware updates.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d930a821fe34e56916183227851165d~tplv-goo7wpa0wc-image.image)
If the Device Manager is unresponsive at this point, try disconnecting other non-essential external devices, then restarting the computer, and scan for hardware changes again. If the issue persists, consider reaching out to professionals to examine the system for incorrectly installed drivers or problematic external devices. If necessary, you might also consider reinstalling the system.
#### Streaming service is exceptionally prohibited
If you encounter the following scenarios, the likely cause is that the streaming service is exceptionally prohibited:

* With successful installation of the "Streaming Runtime Service," the PDC interface displays "Connection Failed" or "Streaming Failed."
* Under **Task Manager** > **Processes** > **Background Processes**, there is no process named "ps_server".
* Under **Task Manager** > **Services**, the status of the "ps_service" service is "Stopped."

To resolve this issue, follow these steps:

1. Check the security software installed on your PC to ensure that no restrictions have been placed on the "ps_service" service, including disabling startup, or prohibiting service optimization.
2. In **Task Manager** > **Services** tab, right-click on the **ps_service** entry and select **Start** to bring the service to a running status.

#### Streaming service conflicts
Using the PICO Connect software will cause exceptions to the PICO Developer Center's streaming service. Therefore, make sure to close PICO Connect on both your PC and HMD before using the PICO Developer Center. This issue does not exist on PICO 4 Ultra series devices.
## Live Preview issues
This section lists the common issues related to [previewing app scenes](/en_preview-app-scenes).
### Click **VR Preview** to find an abnormal lag occurring 
Under normal circumstances, graphics cards with performance lower than NVIDIA GeForce GTX 1060 6GB or AMD Radeon RX480 8G (or other graphics cards with similar performance levels) may cause lag during preview.
### Unity Editor crashes after clicking the Play button
Currently, the preview capability only supports DirectX 11 (DX11) Graphic APIs. You need to go to **Edit** > **Project Settings** > **Player** > **Other Settings** to check if the **Graphic APIs for Windows** field has been set to **Direct3D11** or other Graphic APIs. Additionally, you need to check if non-DX11 Graphic APIs are mandatorily used in Command Line Arguments.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb3ec359d5af43659e8a8f32305cfc12~tplv-goo7wpa0wc-image.image)
### Unable to preview the scene after clicking the Play button
Go to **Edit** > **Project Settings** > **XR Plug-in Management** > **PC Settings**, check if you have enabled other plugins in addition to the **PICO Live Preview** plugin; if you have, disable the others.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24d573d0ec864bdcb58c96f01fdc7823~tplv-goo7wpa0wc-image.image)
### The preview screen is stuck
Click the **Stats** button under the **Game** view, and check if the current frame rate is higher than 72 FPS.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d5547bb8c08433f9611768703b70452~tplv-goo7wpa0wc-image.image)

* If the current frame rate is beyond 72 FPS,  you need to bring it down by adding `Application.targetFrameRate = 72;` to the `Awake` or `Start` section in your code.
* If the preview screen is stuck even if the frame rate is below 72 FPS, refer to [this article](/13136/en_pdc-basic-info#access-logs) to access logs for analysis.

### The brightness of the preview image in the HMD is lower than it is in the Game view
As DirectX 11 does not support Linear color space, you need to go to **Edit** > **Project Settings** > **Player** > **PC Settings** > **Other Settings**, and set **Color Space** to **Gamma**.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2b7a15e1c2844ed83dfdeecedce7e6b~tplv-goo7wpa0wc-image.image)
### The preview screen is black
Go to "Device Manager" and then to "Display Adapters" to check if there is a virtual graphics card in your PC. If there is, you need to disable the virtual graphics card.


# --- END: Troubleshooting guide for PDC.md ---



# --- BEGIN: Troubleshooting.md ---

This article introduces how to troubleshoot the errors you may come across while using SecureMR.
## Server Err: [INVALID PARAMETER]
**Error message:**
```Plain Text
01-15 06:48:37.800 6956 11741 E Secure MR::Server: [06:48:37.800][Error ] Operator<23> >>> result 1 size (2464x3248) mismatches the config (256x256)
01-15 06:48:37.800 6956 11741 E Secure MR::Server: [06:48:37.800][Error ] setNamedResult >>> Server Err: [INVALID PARAMETER]: operator result 1 is incompatible with tensorb4000076967c7d18. You may need to double check the extension specification for the operator's operand requirements
```

**Solution:**
According to the error in the first line, the 23rd operator is `XR_SECURE_MR_OPERATOR_TYPE_RECTIFIED_VST_ACCESS_PICO`. The mismatch between `2464x3248` and `256x256` is caused by the error resulting from the resolution of the VST image set in the framework not matching the shape of the result provided by the `RECTIFIED_VST_ACCESS` operator.
## Server Err: [HANDLE NOT INITIALIZED]
**Error message:**
```Plain Text
01-15 07:09:16.919 6956 11741 E Secure MR::Server: [07:09:16.919][Error ] setNamedResult >>> Server Err: [HANDLE NOT INITIALIZED]: queryLocalTensor(0) >>> cannot find the local tensor with ID = 0 in pipeline ID = b40000776b92e718; check whether it has been registered
```

**Solution:**
Check if there are tensors that have not been registered into the pipeline. The ID of the pipeline is b40000776b92e718.
## Server Err: [HANDLE NOT INITIALIZED]
**Error message:**
```Plain Text
01-13 07:58:57.826 7235 7255 E Secure MR::Server: [07:58:57.826][Error ] submitPipeline >>> Server Err: [HANDLE NOT INITIALIZED]: isLocalTensorPlaceHolder(ffffffffffffffff) >>> cannot find the local tensor with ID = ffffffffffffffff in pipeline ID = b4000077a552de58; check whether it has been registered
```

**Solution:**
There are tensors that have not been registered into the pipeline. Tensors are registered into the pipeline through `xrCreateSecureMrPipelineTensorPICO`. You need to check your code to see if there are variable command errors that cause the tensors used in the pipeline not to be registered by `xrCreateSecureMrPipelineTensorPICO`.


# --- END: Troubleshooting.md ---



# --- BEGIN: Why can't my app be recentered by long pressing the Home key_.md ---

Use the following steps to resolve this issue:

1. Add XR Origin to the scene.
2. Click **XR Origin** to select it.
3. In the **Inspector** window, complete the following:
   1. Click the **Add Component** button and add the **PXR_Manager** script to XR Origin.
   2. On the **XR Origin** pane, set **Tracking Origin Mode** as **Device** or **Floor**.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18e7d7376f7b47129e74359aa228772d~tplv-goo7wpa0wc-image.image)


# --- END: Why can't my app be recentered by long pressing the Home key_.md ---



# --- BEGIN: Why can't the Preview Tool be connected to a Neo3 device via wired connection_.md ---

If you are unable to connect the Preview Tool to a Neo3 series device via wired connection, try the following:

1. Turn off the firewall on your PC, or add PreviewTool.exe to the firewall's allowlist (i.e., whitelist) and check the **Public** and **Private** options. It is recommended that you disable the antivirus software at the same time.
2. Use the DP interface to wiredly connect the Neo3 device to the PC.


# --- END: Why can't the Preview Tool be connected to a Neo3 device via wired connection_.md ---



# --- BEGIN: Why don't the apps installed on the device appear in the Library's app list_.md ---

The situation varies depending on whether the app has been published on the PICO Store.

* **Published**
   Once an app has been installed on a PICO device, it will show as an Android icon with the package name under the **Unknown Source** directory. If you cannot find the app in the **Unknown Source** directory, check if the `"<category android:name="android.intent.category.LAUNCHER" />"` tag is included in the AndroidManifest.xml file. However, in certain cases, the tag will be tampered with by third-party SDKs during packaging and building. If so, troubleshoot according to the actual project configuration.
* **Not published**
   Once an app is purchased by a user, it will show as an Android icon with the package name under the specified directory.


# --- END: Why don't the apps installed on the device appear in the Library's app list_.md ---

