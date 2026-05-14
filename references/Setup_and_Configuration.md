# Setup and Configuration

## Table of Contents
- 1. Create a developer account, organization, and app
- 2. Set up the development environment
- 3. Import the SDK
- 4. Complete project settings
- 5. Create an XR scene
- 6. Build and run the scene
- About the PICO Unity Integration SDK
- Android Manifest
- Architecture
- Developer Tools Overview
- Hardware and software requirements
- Initialization
- Interaction Pack overview
- Key concepts
- Key concepts_ tensor, operator, and pipeline
- Overview(2)
- Overview(3)
- Overview(4)
- Overview(5)
- Overview(6)
- Overview(7)
- Overview
- PICO Developer Center quickstart
- Platform services overview
- Project Validation
- Quickstart
- Sense Pack overview

---



# --- BEGIN: 1. Create a developer account, organization, and app.md ---

This article introduces how to create a PICO Developer account, organization, and app on the PICO Developer Platform.
## Step 1: Sign up for a PICO Developer account
A PICO Developer account is what you need for app management on the PICO Developer Platform.

1. Go to the [PICO Developer Platform](https://developer.picoxr.com/console/#/organization).
   This directs you to the following screen:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a9ddb7f43474c70b6f4c1e9fd13bcad~tplv-goo7wpa0wc-image.image)
2. Select **Other regions** as the region where your account is located.
3. Check the **I confirm that I have read and agree to the PICO Developer Terms** checkbox.
4. Click **Sign up**.
   This directs you to the sign-up screen.
5. Follow the on-screen instructions to complete sign-up.
   After signup, you are directed to the following screen. Then, follow the instructions in the next section to create an organization.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a626b609c3ae417185991faea4848aa6~tplv-goo7wpa0wc-image.image)

## Step 2: Create an Organization
An organization is a subject that publishes apps on the PICO Store. The organization's name will be displayed on the app's details page on the PICO Store. You can create multiple organizations using one PICO Developer account.

1. Click **Create Organization** in the middle of the screen.
   The **Create a New Organization** window appears.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/435ee64f9d034e5bb7ed0c078fcaaeb6~tplv-goo7wpa0wc-image.image)
2. In the **Create a New Organization** window, fill in organization information. Fields marked with * are required.
3. Click **Create**.
   The following pop-up window appears.
   If you only want to experience the app development process, you can close the following window, skip the rest of the steps in this section, and refer to the "Create an app" section to create your first app. However, if you want to experience the app distribution process, you need to follow the steps below to complete organization details (mainly the qualification information). After submitting the qualification information for review, you can proceed to create an app.

   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06f7a81e8e424142a0b4dadc47083b72~tplv-goo7wpa0wc-image.image)
4. Click **go**.
   This directs you to the **Organization details** screen.
5. Click **Edit** to fill in the information for qualification certification.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6955ac7d2ce9419eb6d6c87aeaddc87e~tplv-goo7wpa0wc-image.image)
   Below are field descriptions:
   | **Field** | **Description** |
   | --- | --- |
   | Developer Type | The platform will automatically fill in this field based on the type you choose in the previous step. It can not be changed once you settle it. |
   | Country/Region | The platform will automatically fill in this field based on the contry/region you choose in the previous step. It can not be changed once you settle it. |
   | Full name of the company / Name | * For an enterprise developer, fill in the full name of your company. <br> * For an individual developer, fill in your full name. |
   | Qualification photo | Upload a certificate photo that can prove your business qualification or personal identity. <br>  <br> * For an enterprise developer, upload the photo of your enterprise registration certificate, tax certificate, enterprise registration certificate, etc; <br> * For an individual developer, upload the photo of your passport, driver's license, identity information certificate, etc. |
   | Qualification number | Fill in the qualification number on your corporate qualification photo or personal identity photo. The qualification number can not be changed after submission. |
6. Click **Submit**.
   After submission, the qualification information will enter the review process, and you can proceed to create an app. You can go to **Settings** > **Organization** **Details** to check the review status of your qualification information.
   Once the qualification information is approved, it cannot be changed. If the qualification information is rejected, you need to modify the qualification information and submit it again for review.

## Step 3: Create an app
Apps are what you finally publish on the PICO Store. 

1. Choose the organization you just created.
2. On the **My Apps** screen, click **Create App** or **Create**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a08a7d5a7a643edba6cdb653930bfe2~tplv-goo7wpa0wc-image.image)
3. In the **Create a New App** window, enter the **App Name** and select a **Platform**.
   * 3 DOF Platform
   * 6 DOF Platform (recommended)
4. Click **Create**. 
   On the **My Apps** screen, the newly-created app appears.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb1debebf14a439597f23436e8568f8e~tplv-goo7wpa0wc-image.image)

## What's next
Follow the instructions in the "[Set up the development environment](/13136/en_set-up-the-development-environment)" article to enable the "Developer" mode for your PICO device and install a desired version of Unity Editor.


# --- END: 1. Create a developer account, organization, and app.md ---



# --- BEGIN: 2. Set up the development environment.md ---

This article introduces how to set up the development environment. Before the setup, learn the [hardware and software requirements](/en_hardware-and-software-requirements).
## Step 1: Enable the "Developer" mode for your PICO device
You do not need an extra device for PICO XR app development. Any PICO VR headset on the market can be used as a development device with the "Developer" mode enabled. 




1. Turn on your PICO VR headset.
2. Go to **Settings** > **General** > **About**.
3. Keep clicking on the **Software Version** field until the **Developer** option appears at the bottom of the left navigation panel.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac15b57b23b647cd83bed6d1fac00898~tplv-goo7wpa0wc-image.image)
4. Click **Developer**.
5. On the **Developer** screen, toggle the **USB Debug** switch.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1608b08d0cc04f8782a1ff0c299f065d~tplv-goo7wpa0wc-image.image)
   The "Developer" mode has been enabled for your PICO VR headset.




1. Turn on your PICO VR headset.
2. Go to **Control Center** > **Settings** > **About**.
3. Keep clicking on the **Software Version** field until the **Developer** option appears at the bottom of the left navigation panel.
4. Click **Developer**.
5. On the **Developer** screen, toggle the **USB Debug** switch.



## Step 2: Log in to your PICO account
If you are using a non-Mainland China PICO device, you need to log in to your PICO account on the headset in order to run APKs on it.

1. Click the profile icon on the bottom navigation bar.
2. Follow the on-screen instructions to enter your PICO account and password for a login.

## Step 3: Install the Unity Editor

1. Download the Unity Hub from the [Unity download page](https://unity.com/download).
2. Launch the Unity Hub.
3. From the left navigation pane, select **Installs**.
4. On the **Installs** pane, click **Install Editor**.
5. Find the target Unity Editor version and click **Install**. For the Unity versions supported by the SDK, refer to the "[Hardware and software requirements](/en_hardware-and-software-requirements)" article.
6. In the **Add modules** window, check **Android SDK & NDK Tools** and **OpenJDK**.
   You must check all the options under **Android Build Support** . This will help you set up the environment required by Android app development.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/d1959ad231bf476fae0e94f780ed4066~tplv-em5hxbkur4-noop.image?width=1411&height=821)
7. Click **Continue**.
8. Read the terms and conditions, and then check **I have read and agree with the above terms and conditions**.
9. Click **Install**.
   The Unity Editor will be installed with Android support.
10. After installation, go to **Preferences** > **Licenses**, click **Add**, and select your desired license to activate in the **Add new license** window.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce9da54c683f45f1bb7003c9e7d437ce~tplv-goo7wpa0wc-image.image)

## What's next
Follow the instructions in the "[Import the SDK](/13136/en_import-the-sdk)" article to create a project using the Unity Hub and import the PICO Unity Integration SDK into the project.


# --- END: 2. Set up the development environment.md ---



# --- BEGIN: 3. Import the SDK.md ---

The PICO Unity Integration SDK offers vital VR features, components, and plugins. This article introduces how to create a project on the Unity Hub and import the SDK into the project.
## Step 1: Create a project
You need to create a project in the Unity Hub before importing the SDK. 

1. Launch the Unity Hub.
2. Go to **Projects** > **New project**.
   This directs you to the **New project** window.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/847b4da3543948ebbe45690247ce8c47~tplv-em5hxbkur4-noop.image?width=2048&height=1019)
3. Select **Core** > **3D**.
4. Under **PROJECT SETTINGS**, name your project and select a storage location.
5. Click **Create project**.
   After project initialization, you are then directed to the Unity Editor window.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/d5df5bc597a84f0fafd9b267f018f957~tplv-em5hxbkur4-noop.image?width=2560&height=1316)

## Step 2: Import the PICO Unity Integration SDK
Import the PICO Unity Integration SDK into your project by any of the following methods.
| **Method** | **Steps** |
| --- | --- |
| Import the local SDK package | 1. Go to the [Download](https://developer-global.pico-interactive.com/resources/#pdc) screen. <br> 2. Download the latest version of the PICO Unity Integration SDK. <br> 3. Unzip the downloaded package. <br>    You get a folder containing the **package.json** file. <br> 4. Return to the Unity Editor. <br> 5. From the top menu bar, select **Windows** > **Package Manager**. <br> 6. In the **Package Manager** window, click **+** > **Add package from disk**. <br>    ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/d5d5788b5f48471383af4ca5e37a5f3b~tplv-em5hxbkur4-noop.image?width=1600&height=537) <br> 7. Select the **package.json** file and import it into the project. <br>    The **PXR SDK Setting** window appears.  Close it. |
| Import the Git URL | 1. Go to the [PICO-Unity-Integration-SDK respository](https://github.com/Pico-Developer/PICO-Unity-XR-SDK). <br> 2. Click the **<> Code**  button, and then copy the HTTPS URL of the repository. <br>    ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de0c4a1303f24b528ce2509254e1d3cb~tplv-goo7wpa0wc-image.image) <br> 3. Return to the Unity Editor. <br> 4. From the top menu bar, select **Windows** > **Package Manager**. <br> 5. In the **Package Manager** window, click **+** > **Add package from git URL**. <br>    ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c58b3696671a4a72bc285d0462f2b2e0~tplv-goo7wpa0wc-image.image) <br> 6. In the pop-up panel, enter the HTTPS URL you copied, and then click **Add**. <br>    Unity Editor starts importing the SDK from the Git URL. |
## What's next
Follow the instructions in the "[Complete project settings](/13136/en_complete-project-settings)" article to set up your project for PICO app development.


# --- END: 3. Import the SDK.md ---



# --- BEGIN: 4. Complete project settings.md ---

This article introduces how to complete required project setting, thereby ensuring that your app can implement XR capabilities and be built to run on PICO devices.
## Step 1: Enable the XR plugin
You can use either the PICO XR Plugin or the Unity OpenXR Plugin to enable XR features in your app.
### Limitations

* If both the PICO XR Plugin and the Unity OpenXR Plugin are enabled in the same project, only the PICO XR Plugin will take effect. 
*  If you need to use the Unity OpenXR Plugin, enable the Unity OpenXR Plugin only.

### Enable the PICO XR Plugin

1. From the top menu bar, select **Edit** > **Project Settings**.
2. In the **Project Settings** window, click **XR Plug-in Management** > **Android settings icon**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a478a50787434e4da3cf7848134596de~tplv-goo7wpa0wc-image.image)
3. Check the **PICO** checkbox.
   Do not select other plug-in providers; otherwise, your app will not run normally on PICO devices.

   The PICO XR plug-in is enabled. Do not close the **Project Settings** window, you need to name and version your app on it in the next section. 

### Enable the Unity OpenXR Plugin

1. From the top menu bar, select **Window** > **Package Manager**.
2. In the top-left corner of the **Package Manager** window, click **+** > **Add package by name**.
   The package information input panel appears.
3. In the **Name** input box, fill in **com.unity.xr.openxr** and click **Add**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df2d520a828646b587ceb795a82f3a0a~tplv-goo7wpa0wc-image.image)
   Unity begins installing the **OpenXR Plugin** package into the project. Once the installation is complete, **OpenXR** will appear under **XR Plug-in Management** in the **Project Settings** window.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f294cac3db5494c965c13ff9ac24bed~tplv-goo7wpa0wc-image.image)

## Step 2: Version and name the app
Package names are used to identify Android apps and should be described in the format of `com.companyName.productName`. When exporting an APK file, the Unity Editor will automatically add these names to the AndroidManifest.xml file. The version number is what users will see. In each app release, make sure that the app's version number is higher than the previous one.

1. In the **Project Settings** window, click **Player** on the left navigation pane.
2. On the **Player** pane, set the **Company Name**, **Product Name**, and **Version**.
   Once complete, do not quit the **Player** pane, you need to complete other settings on it in the next section.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2216e49660c046c08f70118916e62e9b~tplv-goo7wpa0wc-image.image)

## Step 3: Complete player-related settings
Player-related settings define the system version the app supports and how the app is to be built. To ensure that you can successfully complete the entire development process and have your app published on the PICO Store, you need to set the following:

* **Minimum API Level**: The minimum Android SDK version (API level) required to run your app. The minimum version supported by PICO SDK is 10.0 (API level 29). Lower versions will cause an error while building the app.
* **Target API Level**: The target Android SDK version (API level) against which to compile your app. It must be equal to or higher than the minimum API level; otherwise, the editor reports an error while building the app.
* **Scripting Backend**: The scripting backend determines how Unity compiles and executes C# code in your project.
* **Target Architectures**: The CPU you want to allow the app to run on.

Below are the steps to follow:

1. Click the **Android Settings icon** on the **Player** pane.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85d06d57f9f9459aa0611330bc72a7b2~tplv-goo7wpa0wc-image.image)
2. Expand the **Other Settings** tab.
3. Under **Identification**, complete the following: 
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c114c51d196340f797932e50f245184e~tplv-goo7wpa0wc-image.image)
   1. Set the **Minimum API Level** to **Android 10.0 (API Level 29)**.
   2. Set the **Target API Level** to **Automatic (highest installed)**. This is typically the default setting.
      The **Automatic (highest installed)** option enables the system to automatically use the highest local Android SDK version to compile your app.
4. Under **Configuration**, complete the following: 
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/8e8bdf99d48f470f91d94a52a98ea884~tplv-em5hxbkur4-noop.image?width=1280&height=909)
   1. Set the **Scripting Backend** to **IL2CPP**.
      IL2CPP provides better support for cross-platform app development than Mono. To be specific, IL2CPP converts MSIL code, such as the C# code in scripts, to C code, and then generates a native binary file (for example, .exe, .apk, or .xap) for your chosen development platform using the C code.
   2. Set the **Target Architectures** to **ARM64** and uncheck **ARMv7**.
      Running Android apps in a 64-bit environment is recommended as this brings performance benefits. In addition, 64-bit apps address more than 4GB of memory space and support dynamic memory allocation.

## Step 4: Add the app ID
APP ID is the unique identifier of an app.
**Get your app's ID**

1. Log in to the [PICO Developer Platform](https://developer.pico-interactive.com/console#/).
2. On the **My Apps** screen, click the card of the app you previously created.
   This directs you to the app's **Overview** screen.
3. On the left navigation panel, click **Platform  Service** > **API Test**.
   The **API** screen shows the **APP ID** field.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b5fbf655ace49829e9d648fe46b029d~tplv-goo7wpa0wc-image.image)

**Fill in the APP ID**

1. Return to the Unity Editor and click **PICO** > **Platform Settings**.
   The **PICO Platform Settings** window appears.
2. Fill in the app ID and click **Apply**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c50b8e8670e94692963cf08ab94cffd6~tplv-goo7wpa0wc-image.image)

## Step 5: (Optional) Configure the AndroidManifest.xml file
As PICO VR headsets run on the Android operating system, every app must have an AndroidManifest.xml file which contains the app's essential metadata, such as app configurations, permissions, software & hardware support, and supported Android versions.
If you use the Unity Engine to build PICO XR apps, an AndroidManifest.xml file containing the required metadata will be automatically generated in the APK file. These metadata are generated based on your project's configuration. For example, when you set up eye tracking for your app in the Unity Editor, the corresponding metadata will be added to the AndroidManifest.xml file. Therefore, you basically do not need to manually add any extra content to the file and can directly compile and run your app with it. 
If you want to customize the AndroidManifest.xml file, go to **Edit** > **Project Settings** > **Player** > **Publishing Settings** > **Build** and check **Custom Main Manifest**.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/549c19279cd9454982e7da8005a19019~tplv-em5hxbkur4-noop.image?width=1401&height=996)
The AndroidManifest.xml file then appears under **Assets**/**Plugins**/**Android**. You can open it and add desired configurations.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/72ee62958b714c318751227674024333~tplv-em5hxbkur4-noop.image?width=1734&height=554)

* For more information about manifest configuration for PICO apps, refer to the "[Android Manifest](/en_android-manifest)" article.
* For more information about Android app manifest configuration, visit [this page](https://developer.android.com/guide/topics/manifest/manifest-intro).

## What's next
Follow the instructions in the "[Create an XR scene](/13136/en_create-an-xr-scene)" article to create an XR scene made up of an XR camera, a floor, a pair of controllers and rays.


# --- END: 4. Complete project settings.md ---



# --- BEGIN: 5. Create an XR scene.md ---

This article introduces how to upgrade the XR Interaction Toolkit and create a simple XR scene made up of an XR camera, a floor, plus a pair of controllers and rays. Additionally, this article also provides information on how to set up user entitlement check, preview and debug the scene. Below is scene you are going to create:
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/bd433ef2803b4ddbb380933971ba47ff~tplv-em5hxbkur4-noop.image?width=613&height=351" width="546px" />

## Step 1: Import the samples of XR Interaction Toolkit
Currently, the PICO Unity Integration SDK does not support XR Interaction Toolkit of version 3.x.x.

To create a basic XR scene, you are going to use the [XR Interaction Toolkit](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@2.1/manual/index.html), a high-level interaction system for creating XR experiences.

1. From the top menu bar, select **Windows** > **Package Manager**.
2. In the **Package Manager** window, set the package type as **Unity Registry**.
   The packages offered in the Unity registry are then displayed.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/a6a416e4b28f4f1488878bc345e8d854~tplv-em5hxbkur4-noop.image?width=1600&height=1135)
3. Find **XR Interaction Toolkit** and click it.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92425637a1314a29a493027d15efffb8~tplv-goo7wpa0wc-image.image)
4. Expand the **Samples** list.
5. Click **Import** to import the **StarterAssets** and **XR Device Simulator** samples.
   | **Sample** | **Description** |
   | --- | --- |
   | Starter Assets | By default, the sample folder is in **Assets** / **Samples** / **XR** **Interaction Toolkit** / **[version]** / **Starter Assets**. The folder provides assets to streamline behaviour setups, including a set of default input actions and presets. |
   | XR Device Simulator | By default, the sample folder is in **Assets** / **Samples** / **XR** **Interaction Toolkit** / **[version]** / **XR Device Simulator** . The folder provides assets to simulate XR HMD and controllers, which allow you to manipulate HMD and controllers with mouse and keyboard input. Furthermore, the folder contains bindings used with the simulator and a prefab that you can quickly use in a scene. |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3eb1bf37e0e4cff98ec498c337b235e~tplv-goo7wpa0wc-image.image)

## Step 2: Add an XR camera
By default, a new project contains a **SampleScene** with a directional light and a general camera. 
Cameras capture the virtual world and display it to the player. You can customize and control cameras to give a unique presentation of your app. You can add an unlimited number of cameras to a scene. These cameras can be configured to render the scene in any order and at any place, or they can be set up to render mere parts of the scene.
For the normal depiction of scenes on XR devices, you need to add one general camera to both the left and right eyes for rendering scenes to both eyes.
XR camera is a default component offered in the XR Interaction Toolkit. An XR camera can render scenes to both the left and right eyes. In addition, XR cameras can perform 3DoF or 6DoF motion with HMD and body movements, thereby presenting users with an authentic XR experience. 
Use the following steps to replace the general camera with an XR camera:

1. In the **Hierarchy** window, right-click on **Main Camera** and click **Delete** to remove it.
2. Click **+** > **XR** > **XR Origin (VR)**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/9f5df0d8c4a34de6b0a1adf5a3f85c06~tplv-em5hxbkur4-noop.image?width=1901&height=1169)
   The XR Origin is added to the scene. It includes the following child objects:
   | **Element** | **Description** |
   | --- | --- |
   | XR Origin | Mounts the components and scripts for scene management and control. |
   | Camera Offset | Synchronizes the HMD's 6DoF data to make the camera and hand controllers move in the scene. |
   | Main Camera | The XR camera that captures the virtual world and displays it on the screen of the HMD. |
   | Left Controller | The left-hand controller. |
   | Right Controller | The right-hand controller. |
3. Select **XR Origin**.
   The components and scripts mounted by the XR Origin are then displayed in the **Inspector** window.
4. Click **Add Component** at the bottom of the **Inspector** window.
5. Search for the [PXR_Manager](/13136/en_about-pxr-manager) script and double-click to add it.

## Step 3: Add a floor

1. In the **Hierarchy** window, click **+** > **3D Object** > **Plane**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c5f21a0d58d54ce59d0236ee9c316f45~tplv-em5hxbkur4-noop.image?width=1896&height=622)
   A default white floor is added to the scene.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/9c2ab16f6ecb41cd9089739ecc59162b~tplv-em5hxbkur4-noop.image?width=1900&height=622)
2. In the **Hierarchy** window, select **Plane**.
   The properties of the Plane object appear in the **Inspector** window.
3. Under the **Transform** component:
   1. Set the **Position** to (0, 0, 0). This is typically the default setting.
   2. Set the **Scale** to (10, 1, 10).
   You have created a 10×10 floor with the world's origin at its center.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/5794dfa4d3434c94a646868c79e4b9c8~tplv-em5hxbkur4-noop.image?width=1350&height=622)

## Step 4: Set up controllers
Hand controllers are also an essential part of an XR app. They enable users to interact with the virtual world, thereby enhancing the immersive experience. The SDK provides controller prefabs which you can directly use and enable them to move with the physical controllers. 
If you are using version 3.x of the XR Interaction Toolkit, set up controllers by using the PICO Controller Tracking feature in [PICO Building Blocks](/en_pico-building-blocks).
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ba4406b0a004463bfa2c548b2df68b6~tplv-goo7wpa0wc-image.image)
If you are using version 2.x of the XR Interaction Toolkit, you can either choose to set up controllers using PICO Building Blocks or follow the steps below to manually set up them:

1. In the **Hierarchy** window, expand **XR Origin** > **Camera Offset**.
2. Select **Left Controller**.
3. In the **Inspector** window, click the **Preset** button in the upper-right corner of the **XR Controller (Action-Based)** pane.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dcef3b32a6a643eb9d6ccb7ee66e4400~tplv-goo7wpa0wc-image.image)
   The **Select Preset** window appears.
4. Double-click **XRI Default Left Controller** to add default settings to the left-hand controller.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/15026220b6574108b6b9d7c2c6379377~tplv-em5hxbkur4-noop.image?width=400&height=230)
5. Find the **Model Prefab** option in the **XR Controller (Action-Based)** pane.
6. In the **Project** window, go to **Packages** > **PICO Integration** > **Assets** > **Resources** > **Prefabs**.
7. Drag **LeftControllerModel** to **Model Prefab**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52341b9a46994ce49b2eba6b33838ee5~tplv-goo7wpa0wc-image.image)
8. Configure the **Right Controller** through the same steps as above.

As the PICO Unity Integration SDK uses Unity's latest [Input System](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.4/manual/index.html), you need to add the **Input Action Manager** script for input control. Below are the steps to follow:

9. In the **Hierarchy** window, select **XR Origin**.
10. Click **Add Component** at the bottom of the **Inspector** window.
11. Search for the **Input Action Manager** script and double-click to add it.
12. In the **Input Action Manager** area, expand the **Action Assets** list, then click **+** to add an action asset (e.g., **Element 0**).
13. Click the **Circle** icon.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c2335fe77a5748d680f3d49eb68a62e0~tplv-em5hxbkur4-noop.image?width=676&height=228)
   The **Select InputActionAsset** window appears.
14. Double-click **XRI Default Input Actions** to add it to **Element 0**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f29042d052f54ba291424452bf3d650a~tplv-em5hxbkur4-noop.image?width=400&height=257)
   You have created a simple XR scene.

## Step 5: (Recommended) Enable user entitlement check
User entitlement check protects your app's copyright. After publishing your app on the PICO Store, only entitled users are able to run the app on their devices. For more information on this topic, refer to the "[User entitlement check ](/13136/en_user-entitlement-check)" article.
## Step 6: (Optional) Preview and debug the scene
You can use the PICO Developer Center (PDC) to preview your app in real time and debug it as needed. For detailed instructions, check out the "[Preview app scenes](/13136/en_pdc-basic-info)" article.
## What's next
Follow the instructions in the "[Build and run the scene](/13136/en_build-and-run-the-scene)" article to build the scene into an APK file and run it on a PICO device.


# --- END: 5. Create an XR scene.md ---



# --- BEGIN: 6. Build and run the scene.md ---

Let's build the XR scene into an APK file that can be run on PICO devices.
## Step 1: Switch the build platform
Android is the target build platform for PICO XR apps and must be set as such before you can build and run the scene. 

1. From the top menu bar, select **File** > **Build Settings**.
2. In the **Build Settings** window, select **Android** from the **Platform** list.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/134dc6545ed84feaa80fcaae18b6dcb7~tplv-em5hxbkur4-noop.image?width=1260&height=1202)
3. Click **Switch Platform**.
   If the **Switch Platform** button shifts to the **Build** button, the build platform has been successfully switched.

## Step 2: Build and run the scene
You can use the Unity Editor's in-built Build Tool to build the basic XR scene into an app that can be run on the PICO VR headset. 

1. Log in to your PICO account on the headset.
2. Connect the headset and PC with a USB cable.
3. In the **Build Settings** window, click **Add Open Scenes** to add the SampleScene as the scene to build.
4. In the **Run Device** field, select the **All compatible devices** option or the model of the device connected to the PC.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06eb7722e7804851885e7bb8e2420683~tplv-goo7wpa0wc-image.image)
5. Click **Build And Run**.
6. In the **Build Android** window, select a storage location for the APK file.
   The Unity Editor starts to build the scene into an app. The VR headset will automatically run the app once the build is complete.

## What's next
Follow the instructions in [distribution-related articles](/document/distribute/app-distribution-overview/) to go through the complete app distribution process.


# --- END: 6. Build and run the scene.md ---



# --- BEGIN: About the PICO Unity Integration SDK.md ---

The PICO Unity Integration SDK is a Unity-based software development kit developed by PICO. The SDK packages a series of features covering rendering, input, tracking, mixed reality, platform services, etc.
## Important notes
Since the version of 3.1.0, the PICO Unity Integration SDK only supports developing 64-bit apps.
## Where to get the SDK?

* [PICO developer website](https://developer.picoxr.com/resources/?platform=unity)
* [PICO-Unity-Integration-SDK repository](https://github.com/Pico-Developer/PICO-Unity-XR-SDK)

## What's in the PICO Integration folder?
After importing the SDK into your project on the Unity Editor, the **PICO Integration** folder appears under the **Package** directory as shown below:
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9036e4e04f254ff7b0881f92f2cf1cd7~tplv-goo7wpa0wc-image.image" width="250px" />

| **Name** | **What's inside** |
| --- | --- |
| Assets | Provides the assets that you can quickly use, including controller & hand assets, prefabs, and shaders. |
| Editor | Provides scripts that cover key SDK features and editor features, including PXR_BuildProcessor, PXR_MetaData, PXR_OverLayEditor, etc. |
| Platform | Provides platform service-related resources, including editor scripts, Android and Windows plugins, samples, and platform service scripts. |
| Runtime | Provides runtime-related resources and scripts. |
| SpatialAudio | Provides spatial audio-related resources, including editor scripts, plugins, prefabs, runtime scripts, and samples. |


# --- END: About the PICO Unity Integration SDK.md ---



# --- BEGIN: Android Manifest.md ---

As PICO VR headsets run on the Android operating system, every app must have an AndroidManifest.xml file which contains the app's essential metadata, such as app configurations, permissions, software & hardware support, and supported Android versions.
If you use the Unity Engine to build PICO XR apps, an AndroidManifest.xml file containing the required metadata will be automatically generated in the APK file. These metadata are generated based on your project's configuration.
This article introduces how to add extra required metadata and permissions for PICO apps.
## Special metadata
You need to manually add the following metadata to the AndriodManifest.xml file for your app, otherwise it will cause display exceptions in activities.

* <meta-data android:name=" pvr.app.type " android:value="vr"/>
* <meta-data android:name=" pvr.display.orientation " android:value="180"/>

## Android permissions
If you want to use the following functionalities in your app, you need to manually add the corresponding Android permissions to the AndriodManifest.xml file.
| **Functionality**  | **Permission** |
| --- | --- |
| Read external storage | <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />  |
| Bluetooth | * <uses-permission android:name="android.permission.BLUETOOTH" /> <br> * <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" /> <br> * <uses-permission android:name="android.permission.INJECT_EVENTS" />  |
| Internet | * <uses-permission android:name="android.permission.INTERNET" /> <br> * <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> |
| Vibrate | <uses-permission android:name="android.permission.VIBRATE"/> |
| Write settings | <uses-permission android:name="android.permission.WRITE_SETTINGS" /> |
| Change settings | <uses-permission android:name="android.permission.CHANGE_CONFIGURATION" /> |
## Optional metadata & permissions
After enabling specific features provided by the SDK, the SDK will automatically write corresponding metadata and permissions into the AndroidManifest.xml file.
Do not edit the permission declaration content if not needed. If you would like to customize the AndroidManifest.xml file, add permission declarations corresponding to the SDK features enabled for your app.

### Eye tracking
After enabling [eye tracking](/en_eye-tracking) for your app, the SDK automatically writes the following metadata and permission into the AndroidManifest.xml file:

* <meta-data android:name="picovr.software.eye_tracking" android:value="1" /> 
* <uses-permission android:name="com.picovr.permission.EYE_TRACKING" /> 

### Face tracking
Based on the [face tracking](/en_face-tracking) mode you enable for your app, the SDK automatically writes corresponding metadata and permission into the AndroidManifest.xml file.
| **Face Tracking Mode** | **Metadata & Permission** |
| --- | --- |
| Hybrid  | * <meta-data android:name="picovr.software.face_tracking" android:value="false/true" />  <br> * <uses-permission android:name="com.picovr.permission.FACE_TRACKING" />  <br> * <uses-permission android:name="android.permission.RECORD_AUDIO" />  |
| Face Only  | * <meta-data android:name="picovr.software.face_tracking" android:value="false/true" />  <br> * <uses-permission android:name="com.picovr.permission.FACE_TRACKING" />  |
| Lipsync Only  | * <meta-data android:name="picovr.software.face_tracking" android:value="false/true" />  <br> * <uses-permission android:name="android.permission.RECORD_AUDIO" />  |
## Customize the AndroidManifest.xml file
If you want to customize the AndroidManifest.xml file, go to **Edit** > **Project Settings** > **Player** > **Publishing Settings** > **Build** and check **Custom Main Manifest**.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/549c19279cd9454982e7da8005a19019~tplv-em5hxbkur4-noop.image?width=1401&height=996)
The AndroidManifest.xml file then appears under /**Assets**/**Plugins**/**Android**. You can open it and add desired configurations.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/72ee62958b714c318751227674024333~tplv-em5hxbkur4-noop.image?width=1734&height=554)
For more information about Android app manifest configuration, visit [this page](https://developer.android.com/guide/topics/manifest/manifest-intro).
## Example AndroidManifest.xml file
The following example AndroidManifest.xml file is for your reference.
<a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0b76dedf5844e5aa31ed3aa11776362~tplv-goo7wpa0wc-image.image" filename="AndroidManifest.xml" download>AndroidManifest.xml</a>


# --- END: Android Manifest.md ---



# --- BEGIN: Architecture.md ---

The core of SecureMR is an isolated, secure runtime service that allows developers to deploy custom MR algorithms requiring access to RGB and depth data. This service also supports rendering 3D mixed reality content directly to the screen. Communication between client applications and the SecureMR service is strictly unidirectional: developers can send in data, 3D assets, algorithms, and execution commands — but no sensitive output (such as camera frames or depth maps) is ever returned to the app. This design ensures robust user privacy by preventing access to potentially sensitive sensor data.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/461049ca15514b9b9649a7d79cf70f18~tplv-goo7wpa0wc-image.image" width="650px" />

Under this architecture, the application never gains direct access to camera or sensor data. Instead, the isolated SecureMR service acts as a delegate — executing custom algorithms and render commands on behalf of the app, and presenting the final mixed reality output directly to the user.
Once launched, the SecureMR service will also maintain an overlay OpenXR session, associated with the client app's XR session. The app can render its non-MR stuff, such as UI or static assets, where the SecureMR service will execute the pipelines submitted by the app, and render the pipeline outcomes on a separated layer beneath the app's layer. 
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd05c473556d4c488e1aa5d95a0fedc8~tplv-goo7wpa0wc-image.image" width="500px" />


# --- END: Architecture.md ---



# --- BEGIN: Developer Tools Overview.md ---

PICO provides a range of developer tools covering app debugging, performance monitoring, haptic editing, and more. 
| **Tool** | **Description** |
| --- | --- |
| PICO Developer Center | A PC client tool platform that encompasses various types of PICO app development tools or components.  See [PICO Developer Center](/en_pdc-basic-info) for details. |
| PICO Emulator (Beta) | You can install your app on PICO Emulator and run it, so as to preview how your app performs. See [PICO Emulator (Beta)](/en_pico-emulator) for details. |
| RenderDoc for PICO | For graphic analysis and debugging. See [RenderDoc for PICO](/en_renderdoc-for-pico) for details. |
| PICO Command Line Utility | For managing the files on the PICO Developer Platform more easily. See [PICO Command Line Utility](/en_command-line-utility) for details. |
| Metrics HUD | Used to monitor the performance metrics of a running app in real time. See [Metrics HUD](/en_metrics-hud) for details. |
| PICO Haptic Editor | Used to edit broadband and multi-channel haptic feedback. See [PICO Haptic Editor](/en_pico-haptic-editor) for details. |
| PICO Graphics Probe Tool | Used to analyze and debug your app's performance. See [PICO Graphics Probe Tool](/en_pico-graphics-probe-tool) for details. |
| Snapdragon Profiler | Used to analyze CPU, GPU, DSP, memory usage, power consumption, heat dissipation, and network data, which are useful references for finding and fixing performance bottlenecks. See [Snapdragon Profiler](/en_242767) for details. |


# --- END: Developer Tools Overview.md ---



# --- BEGIN: Hardware and software requirements.md ---

This article describes the hardware and software requirements for PICO app development.
## PICO VR Headset
### Device model
The SDK supports developing on PICO Neo3 series, PICO 4 series, and PICO 4 Ultra devices. The following table provides the device models required by each feature of the PICO Unity Integration SDK. **√** indicates that a specific feature is supported by a device model, and **ⅹ** indicates not supported.
| **SDK Feature** |  | **PICO Neo3 Series** |  |  | **PICO 4 Series** |  |  | **PICO 4 Ultra** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  |  | PICO Neo3 Link | PICO Neo3 Pro | PICO Neo3 Pro Eye | PICO 4 | PICO 4 Pro | PICO 4 Enterprise |  |
| Rendering | Splash screen | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Screen fade | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Fixed foveated rendering | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Display refresh rate | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | VR compositor layers | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Multiview rendering | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Anti-aliasing | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Focus awareness | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Application SpaceWarp | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Late Latching | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Buffer discards optimization | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Render viewport scaling | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Adaptive resolution | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
| Interaction Pack | Input mapping | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | System keyboard | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Haptic feedback | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Tracking origin | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Eye tracking | **ⅹ** | **ⅹ** | **√** | **ⅹ** | **√** | **√** | **ⅹ** |
|  | Hand tracking | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Face tracking | **ⅹ** | **ⅹ** | **ⅹ** | **ⅹ** | **√** | **√** | **ⅹ** |
|  | Body tracking | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
| Sense Pack | Video seethrough | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
|  | Spatial anchors | **ⅹ** | **ⅹ** | **ⅹ** | **√** | **√** | **√** | **√** |
|  | Space calibration | **ⅹ** | **ⅹ** | **ⅹ** | **√** | **√** | **√** | **√** |
| Mixed reality capture |  | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
| Spatial audio |  | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
| Content protection |  | **√** | **√** | **√** | **√** | **√** | **√** | **√** |
| Platform services (All) |  | **√** | **√** | **ⅹ** | **√** | **√** | **ⅹ** | **√** |
### System version (OS)

* PICO 4 series: 5.13.0
* PICO 4 Ultra series: 5.14.0 or later

## PC
You can use the PICO Unity Integration SDK on Windows or macOS. The minimum system requirements are given below.
| **Operating System** | **Minimum Requirements** |
| --- | --- |
| Windows | **Windows 10** is recommended. Some development tools, such as the PICO Developer Center, need to be run on Windows 10. The system requirements are as follows: <br>  <br> * **CPU**: Intel i5-4590 / AMD Ryzen 5 1500X or higher <br> * **Graphics card**: NVIDIA GTX 1060 / AMD Radeon RX 480 <br> * **RAM**: 8 GB or higher <br> * **Port**: USB 3.0 |
| macOS | * **System**: macOS Sierra 10 or later <br> * **CPU**: Intel I5-4590 / Apple M1 or later <br> * **RAM**: 8 GB or higher |
## Unity Editor
**2021.3.26** is the minimum and **Unity 6.0** is the maximum Unity version supported by the PICO Unity Integration SDK. It is recommended using Unity's LTS releases. 
To develop PICO apps with Unity 2022, please ensure that you are using SDK 2.1.5 or a more recent version, and that the PICO device's system version is 5.5.0 or later. 
To develop PICO apps with Unity 2023, please ensure that you are using SDK 3.0.0 or a more recent version, and that the PICO device's system version is 5.11.0 or later. 
**Known issues**

* For Unity 2022.1.14 or later versions, a crash will occur when using URP, Linear color space, 4x MSAA, and OpenGL simultaneously in a project. This issue is pending resolution from the Unity engine team.
* For Unity 2022, using Vulkan and enabling the Development Build option together will lead to a crash when running the corresponding APK file on a PICO device.


# --- END: Hardware and software requirements.md ---



# --- BEGIN: Initialization.md ---

Platform services can be initialized either synchronously or asynchronously. Regardless of the chosen method, it is important to ensure that other platform service APIs are called only after successful initialization of platform services.
## Initialize platform services
### Synchronous initialization
If synchronous initialization fails, an exception will be thrown. You need to handle the error in the `catch` section.
Synchronous initialization involves network request, which may cause a brief lag during the app's startup.

```C#
try
{
    CoreService.Initialize();
    UserService.GetLoggedInUser().OnComplete(userMessage =>
    {
        if (userMessage.IsError)
        {
            Debug.Log($"GetLoggedInUser failed:code= {userMessage.Error.Code} message={userMessage.Error.Message}");
            return;
        }

        Debug.Log($"name={userMessage.Data.DisplayName}");
    });
}
// Handle the error here
catch (UnityException e)
{
    Debug.Log($"Init Platform SDK error:{e}");
    throw;
}
```

### Asynchronous initialization
If you use asynchronous initialization, you need to first check `m.IsError` and then check `m.Data`. If the value of `m.Data` is `PlatformInitializeResult.Success` ** or `PlatformInitializeResult.AlreadyInitialized`, it indicates successful initialization.
```C#
CoreService.AsyncInitialize().OnComplete(m =>
{
    // An error message returned
    if (m.IsError)
    {
        Debug.Log($"Async initialize failed: code={m.GetError().Code} message={m.GetError().Message}");
        return;
    }
    
    // If async init succeeds, return Message<PlatformInitializeResult>; if m.Date indicates failure, init has failed
    if (m.Data != PlatformInitializeResult.Success && m.Data != PlatformInitializeResult.AlreadyInitialized)
    {
        Debug.Log($"Async initialize failed: result={m.Data}");
        return;
    }

    // If async init succeeds, proceed to call other platform service APIs
    Debug.Log("AsyncInitialize Successfully");
    UserService.GetLoggedInUser().OnComplete(userMessage =>
    {
        if (userMessage.IsError)
        {
            Debug.Log($"GetLoggedInUser failed:code= {userMessage.Error.Code} message={userMessage.Error.Message}");
            return;
        }

        Debug.Log($"name={userMessage.Data.DisplayName}");
    });
});
```

Below is the example of an incorrect API call. In the example, `UserService.GetLoggedInUser()` is called before async initialization is completed.
```C#
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
});
UserService.GetLoggedInUser().OnComplete(userMessage =>
{
    if (userMessage.IsError)
    {
        Debug.Log($"GetLoggedInUser failed:code= {userMessage.Error.Code} message={userMessage.Error.Message}");
        return;
    }

    Debug.Log($"name={userMessage.Data.DisplayName}");
});
```

### Handle initialization failures
Initialization failure is frequently due to user-side network problems, although other causes cannot be completely dismissed. The following are common ways to address typical initialization failures:

* Enable your app to work in offline mode
* Redirect users to a page/window where the user is notified of the network problem and is able to contact the developer. Include a refresh button on the page/window so users can easily re-initialize the platform services.

## Initialize the game module
### Prerequisite
Make sure you have completed basic setups and enabled the matchmaking service on the PICO Developer Platform. For detailed instructions, refer to the "[Room & Matchmaking](/en_matchmaking)" guide.
### Procedure

1. Call `CoreService.GameInitialize` to send the initialization request.
   ```C#
   public static Task<GameInitializeResult> GameInitialize(string accessToken) 
   { 
       if (Initialized) 
       { 
           return new Task<GameInitializeResult>(CLIB.ppf_Game_InitializeWithToken(accessToken)); 
       } 
   
       Debug.LogError(UninitializedError); 
       return null; 
    }
   ```

2. Set the callback function for the initialization request.
   If the response message is `GameInitializeResult.Success`, the Game module has been initialized and ready for use. If the initialization fails, you need to handle errors according to the returned error response. For example, if the error is caused by a network problem, you need to notify users to check their network.

### Monitor network events
You need to monitor network events when using "Room & Matchmaking" service. If users come across network disconnection and reconnection issues, you will receive the following event notifications. The `Lost` event indicates that the user has been disconnected, and you need to stop sending requests to the client. The `Resumed` event indicates that the user has been reconnected. It is recommended that you notify users of a reconnecting status through adding a reconnecting icon in the middle of the screen or other practical ways.
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

### Important note
If an app is moved to the background, `popMessage` will cease, causing the server to be unable to receive heartbeats from the app. If this situation lasts for a long period of time, the app will be disconnected from the server, and messages generated during the disconnection period will be lost. After the app is moved to the foreground, it will reconnect with the server.
### Game service-related articles

* [Room & Matchmaking](/en_matchmaking)
* [Leaderboard](/en_leaderboard)
* [Achievements](/en_achievements)
* [Challenges](/en_challenges)

## API reference
For details on CoreService APIs, refer to the [API reference](/reference/unity/client-api/CoreService/).


# --- END: Initialization.md ---



# --- BEGIN: Interaction Pack overview.md ---

Interaction Pack provides features like input mapping, system keyboard, motion tracking, and more.
## What's in the Interaction Pack
| **function** | **Description** |
| --- | --- |
| [Input mapping](/en_input-mapping) | The PICO Unity Integration SDK uses Unity's official keycodes for input event mapping. Every controller/HMD action will be mapped to an input event.  |
| [System Keyboard](/en_system-keyboard) | With the in-app keyboard, users can input text in a wide range of scenarios, including text chats and text-based information settings.  |
| [Haptic Feedback](/en_haptic-feedback) | Haptic feedback makes it possible to simulate most haptic output in the real world, thereby giving users a wonderful haptic experience. |
| [Tracking Origin](/en_tracking-origin) | The system sets a positional origin for a user when the user enters an app. Afterward, when the user moves in the virtual scene, the system tracks and calculates the user's positional changes based on the origin. |
| [Eye Tracking](/en_eye-tracking) | Eye tracking is a sensor technology that enables a device to track a user's gaze in real time. It converts a user's eye movements into data streams as PICO devices' input. |
| [Hand Tracking](/en_hand-tracking-overview) | Hand tracking enables users' hand poses as PICO devices' input, thereby enhancing user-app interaction for your app. |
| [Face Tracking](/en_face-tracking) | Face tracking detects and captures users' facial movements. The face tracking APIs convert captured data into blendshapes and pass them to the app for implementing face tracking.  |
| [Body Tracking](/en_body-tracking) | Body tracking is a motion capture technology that collects a user's body positions, converting them to positions and actions within a virtual environment. |
| [Object Tracking](/en_object-tracking) | Object Tracking is used to track and output the 6DoF data of the motion trackers in real time. The data is used for tracking the trackers themselves or the objects they attach to. |


# --- END: Interaction Pack overview.md ---



# --- BEGIN: Key concepts.md ---

This article introduces the key concepts of the Social Interaction service, including destination, presence, deep link, and more. You can learn the definitions of these concepts plus how they function and co-work with each other.
## Destination
In the real world, people's social activities usually require a specific gathering place, such as a restaurant or a concert hall. In the VR world, the gathering place is called **destination**. More specifically, a destination can be a game lobby, game level, room, and more. Users can show and share their destinations with friends and invite them to join.
You can create multiple destinations for your app on the PICO Developer Platform. For each destination, you can customize its settings, including the description, API name, deeplink message, and more. For instructions on how to create destinations, see the "[Platform service setups](/13136/en_social-interaction-platform-service-setups#1dd5698d)" article.
## Lobby session & match session
For multiplayer experiences, you may also need to use lobby sessions and match sessions in addition to destinations.
| **Name** | **Description** |
| --- | --- |
| Lobby Session  | Used to identify user groups or teams. Users in the same team have the same lobby session ID. |
| Match Session  <br>  | Used to identify all users in the same room or match session. These users have the same match session ID. Users with different lobby session IDs have the same match session ID when they are playing the same match. |
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c316fdc226404947a44fbd87846fa67a~tplv-goo7wpa0wc-image.image" width="650px" />

In social interaction scenarios:

* If user A invites friend B to join a game level, and they join a match as a team, you need to retrieve and parse user A's destination, match session ID, and lobby session ID from launch details.
* If user A invites friend B to join a game level for a 1v1 match, you need to retrieve and parse user A's destination and match session ID from launch details.

## Presence
**Presence** contains a user's current location and status information, such as the destination, lobby session, match session, and whether the user is joinable. You can display a user's presence as you see fit, such as in the game lobby or matchmaking panel. In this way, users can view each other's location and status information, then decide whether to invite or join others.
It is recommended that you timely set and update a user's presence. When a user leaves a room or exits the app, you should immediately clear the user's presence.
## Deep link
In Android, a deep link directs someone to a specific destination within an app. Deep links contain location information. In PICO's Social Interaction service, deep links are mainly used invite-and-join experiences, link sharing, and jumping between apps. For PICO apps, deep links are currently implemented through invitation message cards sent between friends (as shown in the figure below). Users can click on the card to accurately go to a target location using the invisible deep linking capability.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/710b4b258f85490b94111ed77576086c~tplv-goo7wpa0wc-image.image" width="260px" />

When creating destinations on the PICO Developer Platform, you can enable the deep linking capability and set deeplink messages for them.
## Deeplink message
**Deeplink message** is used to store dynamic configurations. Deeplink messages do not necessarily have to be used with destinations. For example, in the jump-between-apps scenario, you need to separately customize the jumping rules in the deeplink message.
## Launch details
[Launch details](/reference/unity/client-api/platform_sdk_model_list/#LaunchDetails) contain an app's launch type, destination API name, lobby session ID, match session ID, and more. After the app launches, you need to retrieve and parse launch details to teleport users to the target location.
## Related content
If you would like to learn how these concepts are implemented in different use cases and relevant code samples, refer to the "[Use cases](/13136/en_social-interaction-use-cases)" article.


# --- END: Key concepts.md ---



# --- BEGIN: Key concepts_ tensor, operator, and pipeline.md ---

This article introduces the key concepts of SecureMR, including tensor, operator, and pipeline.
## Overview
Below are brief introductions to the key concepts of SecureMR.
| **Concept** | **Description** |
| --- | --- |
| Tensor |  A tensor is any chunk of data. The contents of a tensor will be stored only in the SecureMR service. The app will be given only a handle as the reference to the tensor. |
| Operator | Operators are nodes to implement a developer-defined algorithm. They intake some tensors (called *operands*), perform operations, and output the results to some other tensors (called *results*).  |
| Pipeline | If operators are considered algorithm nodes, then tensors represent the edges between these nodes, facilitating data flow among them. From this perspective, operators and tensors form a computation graph. In SecureMR, such computation graphs are called "pipelines." |
A SecureMR app that wants to implement a feature will usually use the concepts above to create functionality that it needs. 
If we take, for example, the mnist classification application, we can break down its functionality into this simplified view of the operations it needs to do:

1. Get the video see through (vst) image
2. Pass that image as input into a mnist model inference
3. The outputs of the inference are a label and confidence value
4. We can pass the outputs into a rendertext command to render the outputs as text

So, for this case, we will start with creating a pipeline for inference. In this pipeline, we will create a RectifiedVstAccessOperator, which has no inputs, but we will set it up to output the vst image as a result tensor. 
Then we will create a RunModelInferenceOperator in the pipeline, configured to use the mnist model binary we provide. To this operator, we will provide the vst image tensor from the previous step as an operand (input) and set up the outputs of this operator to write to two output tensors, one for the integer value tensor of the index that is predicted by the inference, and the other for the float confidence value tensor of the inference prediction. 
Finally, we will create two RenderTextOperators in the pipeline, one of which will take the index tensor as input and print its value and the other prints the confidence tensor value on the screen. (This is a simplification to convey the idea).
Once the app has created this pipeline, it can execute the pipeline on every update cycle of the application and it will work as expected. 
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f712ddf8400744918f487b62c1663e33~tplv-goo7wpa0wc-image.image)
## Tensor
SecureMR uses the term "tensor" to describe any chunk of data. This term is widely used in ML circles, but in SecureMR it has more restricitve definition. Because SecureMR is designed to be an isolated MR service to delegate an app's algorithms, the contents of a tensor will be stored only in the SecureMR service. The app will be given only a handle as the reference to the tensor.
Apps are allowed to create and write data to them via the handles. Additionally, an app can use tensors in an algorithm delegated to the SecureMR service. But apps are restricted from retrieving tensor data using the tensor handles they created or wrote to.
Normally, a tensor is defined by four attributes, namely, shape, channel. data type, and usage. Below are detailed descriptions:
| **Attribute Name** | **Description** |
| --- | --- |
| Shape | An array of unsigned integers, defining the size of the tensor per dimension. |
| Channel | A single unsigned integer, defining the number of channels.  <br> Following OpenCV's convention, a channel will not be a dimension in the tensor's shape. For instance, a 1-channel tensor of shape `[1024, 1024, 3]` is different from a 3-channel tensor of shape `[1024, 1024]`, even though both have 1024x1024x3 elements in total. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0c18f38973b4cf9a6c394f41806b26b~tplv-goo7wpa0wc-image.image) |
| Data type | For specifying the data type of each element in the tensor. The accepted data types are: `UInt8`, `Int8`,`UInt16`,`Int16`, `Int32`, `Float32`, `Float64`, consistent with OpenCV's data type.  |
| Usage | A usage is a flag to declare how a tensor's content will be interpreted when digested in an algorithm. The usage flag shall be one of the following, each with different restrictions on its shape, channel or data type:  <br>  <br> * `Matrix`, the tensor will be treated as a collection of matrices; naturally, such as tensor must have at least 2 dimensions. This is the default usage.  <br> * `Scalar`, the tensor will be treated as a collection of single values; naturally, the channel must be 1.  <br> * `Timestamp`, the tensor will be used to store camera timestamp; the channel must be 4, the data type must be `Int32`, and the shape must be `[1, ]` <br> * `Color`, the tensor will be treated as a collection of RGB or RGBA colors; for RGB colors, the channel must be 3, whereas for RGBA colors, the channel must be 4; the data type must be integral.  <br> * `Point`, the tensor will be treated as a collection of 2D or 3D points; hence, its channel must be 2 or 3.  <br> * `Slice`, the tensor will be used to describe a python-style slice on other tensors; it is required the channel must be 2 or 3, and the data type must be integer. A 2-channel slice will be treated as `(START, END)`, whereas a 3-channel slice will be treated as `(START, END, SKIP)`. <br>    For example, a 2-channel slice tensor whose content is `(0, -1)` is equivalent to such codes in python: <br>    ```Python <br>    arr[0:-1] # all from the first to the last <br>    ``` <br>  <br>    A 3-channel slice tensor whose content is `(5, 10, 2)` is equivalent to this python: <br>    ```Python <br>    arr[5:10:2] # elements at Index 5, 7, 9 <br>    ``` <br>  |
For example, a 1-channel `Float32` tensor of shape `[10, 3, 4]`:

* If its usage is declared as `Matrix`, it will be treated as 10 3x4 matrices in calculation.
* If its usage is declared as `Scalar`, it will be treated as 120 (=10x3x4) independent scalars, so it will not be applied to matrix operations but only elementwise computation. 




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f166f48d4ac54682a679c7f184d218a6~tplv-goo7wpa0wc-image.image" width="362px" />

10 3x4 Matrices, if usage = <code>Matrix</code>




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a915e24d3d641a880b0bc9f4053f959~tplv-goo7wpa0wc-image.image" width="284px" />

120(10x3x4) scalars, if usage = <code>Scalar</code>




One more example, a 3-channel `Int32` tensor of shape `[20,]`:

* If its usage is declared as `Point3`, it will be treated as 20 point3 coordinates, where the 3 channels will respectively describe the X, Y and Z coordinates of the point.
* If its usage is declared as `Color`, it will then be treated as 20 RGB colors, where the 3 channels will each be color components for R, G and B. 

There are also special types of tensors for non-data-storage usage. The only special type of tensor we currently support is the GLTF tensor. The GLTF tensor is also a handle, like any other tensor, but it refers to a glTF instance to be rendered instead. The GLTF tensor has no shape, no channel, and no datatype, only a special usage flag: `Gltf`.
The SDK provides the following methods for tensor management:

* `CreateTensor`
   * Create a specific type of tensor, including `Matrix` tensor, `Point` tensor, and more.
      ```C#
      float[] matrixData = { 1.0f, 2.0f, 3.0f, 4.0f };
      currentPipeline.CreateTensor<float,Matrix>(1,tensorShape0,matrixData);
      ```

   * Create a glTF tensor：
      ```C#
      byte[] data = File.ReadAllBytes(filePath);
      var gltfTensor = secureMRProvider.CreateTensor<Gltf>(data);
      ```

* `Destroy`

      Destroy a tensor. Only global tensors can be destroyed.

   ```C#
   floatTensor.Destroy();
   ```

* `Reset`
   Tensor data can be reset or updated. You can use the `Reset` method to reuse tensors.
   ```C#
   float [] floatBuffer2 = [4.0f, 5.0f, 3.0f, 2.0f];
   floatTensor.Reset(floatBuffer2);
   ```

## Operator
## Operator
Operators are nodes to implement a developer-defined algorithm. They intake some tensors (called *operands*), perform operations, and output the results to some other tensors (called *results*). Thus, app developers can easily use operators and tensors to build an algorithm and hand it over to the SecureMR server for execution.
Similar to tensors, operators are constructed and executed on the SecureMR server side; what the app developers can manipulate are handles to the operators.
Developers can write their algorithms, whether they are machine learning ones or not, in PyTorch, TensorFlow, or ONNX, convert them using Qualcomm Neural Network (QNN) SDK into binary algorithm package, and load the package to the SecureMR operators. These operators will be executed on Qualcomm NPUs. 
For development simplicity, PICO also provides some pre-defined CPU operators, for pre-/post-processing, such as matrix algebra, value assignment, sorting, and non maximum suppression (NMS), etc. 
Mixed-reality operators are also available to display algorithm outcomes on screen. These MR operators can be utilized to render glTF tensors, display text, track objects of interest, modify the materials or textures of glTFs, or even animate them.
Below are the methods for operator:

* `Create`
   ```C#
   // Create an operator
   var xxxOperator= currentPipeline.CreateOperator<ArithmeticComposeOperator>();
   ```

* `SetOperand`/ `SetResult`
   ```C#
   // Set the input for an operator
   xxxOperator.SetOperand("operand0", operand0);
   xxxOperator.SetOperand("operand1", operand1);
   
   // Set the output for an operator
   xxxOperator.SetResult("result", result);
   ```

For detailed instructions on using different types of operators, refer to "[Use different operators](/en_use-different-operators)".
## Pipeline
If operators are considered algorithm nodes, then tensors represent the edges between these nodes, facilitating data flow among them. From this perspective, operators and tensors form a computation graph. In SecureMR, such computation graphs are called "pipelines."
Operators in the pipeline will be executed in the same order they are added to the pipeline. This sequential execution is the reason they are referred to as "pipelines."

Once a pipeline is created, developers can add operators and tensors within it. The pipeline is not executed until developers submit it. Each submission will schedule the SecureMR server to run the entire pipeline **once** and return a "run handle" as a reference to the scheduled execution.
When submitting a pipeline, developers can specify two scheduling hints: `wait-for` and `condition`. 

* Developers can use a previous run handle as the `wait-for` hint, to indicate to the SecureMR server that this execution shall be scheduled **after** the completion of the one referred to by the hint. 
* Developers can use a tensor handle as the `condition` hint, to indicate that this execution will be conducted **on condition that** the tensor is true (non-zero). Otherwise, the execution will be discarded. 

### Global tensors
A pipeline encapsulates tensors and operators as its local members, making it challenging to share data between pipelines. Global tensors provide a solution to this issue. 
Typically, a tensor is defined within a pipeline for data flow between operators created in the same scope, namely a "local tensor." Conversely, a global tensor is defined independently of any pipeline, allowing its data to be shared across them.
All the previous discussions regarding data types, shapes, channels, usage flags, and their limitations apply equally to both local and global tensors. The only difference lies in their scope: local to a single pipeline, or shared among all pipelines.
* The condition hint of a pipeline's execution must be a global tensor. 
* Currently, glTF tensors can only be created as global ones due to the lifecycle of the render assets. 

### Placeholders
For thread safety, global tensors cannot be bound to operators directly. They have to go through a mechanism called placeholder mapping. 
A placeholder is a dummy local tensor defined in the pipeline as if it were a local tensor. Hence, it can be bound to operators as operands or results. However, placeholders, as the name suggests, behave like "pointers," with no underlying content or data storage but holding a *reference* to some global tensor.
When a pipeline is submitted for execution, developers can map local placeholders to compatible global tensors. The mapping will only be valid for a single submission, allowing developers to reuse the same pipeline with different data inputs for different executions.
Below is an illustration of data sharing between pipeline one and pipeline two using placeholder mapping. Placeholders i and ii in Pipeline One are mapped to global tensors (a) and (b), writing the pipeline's outputs to them; while Pipeline Two has placeholders mapped to the same global tensors, reading the latest values. 
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8be009c7f274efeba9323f913bfb130~tplv-goo7wpa0wc-image.image)
### Execution scheduling
Scheduling of pipeline execution follows these principles: 

* Multiple executions of the same pipeline will not happen concurrently. 
* If an execution involves reading from a global tensor, it will wait until there are no other executions writing to the same global tensor. 
* If an execution involves writing to a global tensor, it will wait until there are no other executions writing to or reading from the same global tensor. 
* An execution will always happen after the one specified by its `wait-for` hint is completed, if not null. 
* An execution will be discarded if the `condition` hint is not null and refers to an all-zero tensor. 
* The SDK does not limit the execution frequency of pipelines, but there is a queuing mechanism. If the previously submitted pipeline has not finished executing, any newly submitted pipeline will be added to the queue. You need to control the execution frequency based on the execution time of the pipeline.

### Related methods

* `Create`/`Destroy`
   ```C#
   // Create an pipeline
   var currentPipeline = secureMRProvider.CreatePipeline();
   // Destroy an pipeline
   currentPipeline.Destroy();
   ```

* `Execute` / `ExecuteAfter` / `ExecuteConditional`
   ```C#
   // Create tensorMapping
   var tensorReference = currentPipeline.CreateTensorReference<float,Matrix>(2,new TensorShape(1,2));
   var globalTensor = secureMRProvider.CreateTensor<float,Matrix>(2,new TensorShape(1,2));
   var pipelineTensorMapping = currentPipeline.CreateTensorMapping();
   pipelineTensorMapping.Set(tensorReference, globalTensor);
   
   // tensorMapping is not a required parameter
   // Executes a pipeline
   var runId = currentPipeline.Execute(pipelineTensorMapping);
   // Executes a new pipeline task in order after the previous one is finished.
   var runId2 = nextPipeline.ExecuteAfter(runId,pipelineTensorMapping2); 
   // Executes the conditional SecureMR pipeline based on the state of the condition tensor.
   var runId3 = conditionalPipeline.ExecuteConditional(runId2,pipelineTensorMapping3);
   ```

## Learn more: about providers
The Provider Session is a session handle between the app and the SecureMR server. Each app can only have one Provider Session that has not been destroyed. Once this session is destroyed, all resources created within it will be reclaimed and released.
The width and height provided when creating the provider represent the desired size of the video seethrough image. A size that is too small will lower the final effect, while a size that is too large may impact performance. Ensure that the input is a positive number; currently, there are no restrictions, and the default size is 1024x1024. It is recommended to set this size to match the input of the AI model being used to avoid potential resizing, thereby improving efficiency.
The SDK offers two provider-related methods: `Create` and `Destroy`, which can be freely combined and called at runtime. Note that once a provider is created, its size cannot be changed; to set a new size, you must first destroy the current provider and then recreate a new one.
```C#
// Create a provider
var secureMRProvider = new Provider(1024, 1024);
// Destroy a provider
secureMRProvider.Destroy();
```


# --- END: Key concepts_ tensor, operator, and pipeline.md ---



# --- BEGIN: Overview(2).md ---

Hand tracking enables users' hand poses as PICO devices' input, thereby enhancing user-app interaction for your app.
## Disclaimer for the use of hand tracking data
Operating your PICO devices necessitates the tracking of the HMD and controllers. Therefore, we will collect and use your 6DoF tracking data and turn on the camera, which is only used for 6DoF tracking and recognition. If you enable the hand tracking capability for your PICO device, we will also capture and generate hand pose data through the camera. We will not store any raw images or videos collected by the camera, nor will we share your raw sensor data with any third party without your consent.
## Iteration of hand tracking

* SDK v2.3.0 upgrades the hand tracking algorithm and fully aligns it with the OpenXR standard. The new version of the hand tracking feature is no longer compatible with the old versions of the SDK. If you want to incorporate hand tracking into your app, make sure to use the SDK version 2.3.0 or higher, along with a PICO device running system version 5.7.0 or higher.
* SDK v2.1.5 releases the hand pose editor which is made up of PXR_Hand Pose Generator (Script) and PXR_Hand Pose (Script). You can use the hand pose editor to create hand poses and hand pose events.

## Important note
Currently, PICO devices only support tracking controllers or hands, instead of both.
## Related articles

* [Use hand tracking](/en_hand-tracking)
   Learn the complete procedure for using hand tracking in your app, and the reference information about development environment requirements, hand joint conventions, and PICO hand model prefabs.
* [Enable interactions between hands and 3D objects using XR Interaction Toolkit](/en_enable-interactions-between-hands-and-3d-objects-using-xr-interaction-toolkit)
   Adopt the interaction methods provided by the Hands Interaction Demo in your Unity project, enabling interaction between hands and 3D objects.
* [Ergonomics & device limitations](/en_ergonomics-and-limitations)
   Learn the ergonomic factors and PICO device's recognition limitations that you need to consider when designing hand poses.


# --- END: Overview(2).md ---



# --- BEGIN: Overview(3).md ---

Spatial anchors can anchor positions in a virtual environment to specific locations in the real world. They allow developers to create persistent virtual coordinate points in the real world that can be recognized and shared by multiple devices, thereby achieving a consistent experience across devices. Once an anchor is created and persisted into the PICO device's local disk, when you return to the location where the anchor was placed, the system will retrieve the anchor information and return it to the app.
Shared spatial anchors allow multiple users or devices to share the positioning information of the same virtual object. When a spatial anchor is uploaded to PICO's cloud, it becomes a "shared spatial anchor." Within the same space, when other users obtain the UUID of the shared spatial anchor, they can download and use that anchor.
## Use cases
Below are the key use cases of the Spatial Anchor and Shared Spatial Anchor features.

* **Place and interact with virtual objects**
   Characters, props, and other virtual objects from the app can be placed within the user's actual surroundings, while accurately remembering their positions. When the user returns to the scene later, the previously placed objects can be displayed.
* **Environmental perception and game level design**
   By leveraging spatial anchors, apps can detect the real environment where the user is, then automatically generate or adjust game levels based on environmental characteristics, allowing apps' content to blend more seamlessly with the real-world setting.

## Spatial anchors vs scene anchors
PICO apps can utilize two types of anchor: spatial anchors and scene anchors.

* **Spatial Anchor**: Spatial anchors are created by an app to record the environmental information of that app. For example, when a user places a virtual object within a scene, a apatial anchor can be used to anchor that virtual object. Spatial anchors only belong to the app that creates them and can only be used by that app. For detailed instructions, refer to "[Spatial Anchor](/en_spatial-anchors)" and "[Shared Spatial Anchor](/en_shared-spatial-anchors)".
* **Scene Anchor**: Scene anchors are system-level anchors created by the Room Capture app. Scene anchors are used to record information of the user's surroundings, such as the positions and dimensions of objects like sofas, floors, and walls. When the Room Capture app scans these objects, it automatically adds anchors for them. Scene anchors belong to the PICO system and cannot be modified by third-party apps. However, with the user's permission, third-party apps can discover and utilize scene anchors within them. For more details, refer to "[Scene Capture](/en_scene-capture)".

## Lifecycle of spatial anchors
To place virtual objects in the real world, you need to create spatial anchors first. Then, you need to persist the anchors into the PICO device's local disk so that the app can query and load them. After removing the virtual object, promptly destroy or unpersist the corresponding anchors to free up resources.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7f26ca49caa46f6afdba4d2ee71835e~tplv-goo7wpa0wc-image.image" width="500px" />

* **Create**
   Creating anchors in the app's memory. The request to create an anchor in the app's memory will return the UUID and handle of the created anchor, which will be used to specify the anchor in subsequent operations.
* **Persist**
   Persist the anchor into the PICO device's local disk. After saving the anchor, when using the same device to enter the same space multiple times, you can retrieve the persisted anchor.
* **Share (optional)**
   Upload the spatial anchor to PICO's cloud and share the anchor's UUID with other users, allowing them to download and use the anchor.
* **Query**
   As the user moves within the scene, the app queries and loads previously persisted anchors, let them appear within the scene.
* **Destroy/Unpersist (optional)**
   After destroying an anchor in the app's memory, the app can still load the anchor from the PICO device's local disk. Once the anchor is unpersisted from the local disk, it cannot be queried or loaded.

## Considerations
Considering the following in your app design can help provide a better spatial anchor experience for users.

* Pay attention to the environmental requirements of spatial anchors. Things like white walls and repetitive patterns can affect the accuracy of anchors. To ensure the precision and stability of spatial anchors, it is advisable to avoid or minimize the interference of such environmental factors in your use cases.
* The intensity and direction of lighting can affect the detection accuracy of sensors. Bright light or dim environments may lead to tracking failure. Even and moderate ambient light are the most desired.
* If there are many changes or dynamic objects in the scene, it may affect the use of anchors.
* The user's movement speed and method can affect the stability of tracking. Slow and steady movement helps maintain good positioning accuracy.


# --- END: Overview(3).md ---



# --- BEGIN: Overview(4).md ---

Mixed Reality (MR) has long captured the imagination of developers with its potential to seamlessly blend the virtual and physical worlds. With the latest XR devices now equipped with stereo RGB cameras, Time-of-Flight (ToF) depth sensors, and video see-through (VST) capabilities, the hardware foundation for immersive MR experiences is already in place.
However, building custom MR applications remains challenging. Unlike mobile platforms, developers face restricted access to RGB camera feeds and depth data due to privacy concerns. As a result, they are limited to predefined, OS-level MR features such as static anchors and basic hand gesture recognition.
As Spatial Computing continues to gain traction, these limitations hinder the creativity and innovation that developers seek. To address this, we introduce PICO Secure Mixed Reality (SecureMR) — a privacy-preserving extension that empowers developers to unlock the full potential of MR. SecureMR enables secure, AI-powered mixed reality use cases while maintaining rigorous protection of user data and privacy.
## Requirements

* PICO device model: PICO 4 Ultra series
* PICO device system version: 5.13.0 or later

## Learn about PICO SecureMR
Before developing PICO SecureMR apps, it is recommended to dive into the details about the PICO SecureMR extension, including:

* [The architecture of PICO SecureMR](/en_securemr-architecture)
* [The key concepts: tensor, operator, and pipeline](/en_securemr-key-concepts)

## Create your first Unity SecureMR app
Now that you’ve been introduced to the basics of PICO SecureMR. See [Quickstart](/en_securemr-quickstart) for step-by-step instructions on building your first Unity SecureMR app.
## Developer workflow
You may need to use some of the following sections while developing your apps:

* [Convert and profile models for SecureMR](/en_profile-securemr-models)
* [Use different operators](/en_use-different-operators)
* [Debug tensors in pipelines](/en_debug-tensors-in-a-pipeline)
* [SecureMR use cases](/en_securemr-use-cases)

## Seek ideas from samples
In order to demonstrate the functionalities of SecureMR, PICO provides the following samples for your reference:

* **Minst**: A minimal sample demonstrating the SecureMR pipeline for image-based model inference.
* **ColorPicker**: An interactive sample showing how to process color information from the environment.

For more information, refer to [SecureMR samples](/en_securemr-samples).
## Optimize SecureMR apps
Enhancing the performance of your SecureMR apps should bring a better user experience. You can follow the best practices below to optimize your SecureMR apps:

* [Pipeline synchronization](/en_pipeline-synchronization)
* [Create a QNN model to run algorithms](/en_create-a-qnn-model-to-run-algorithms)

## Troubleshoot issues
Refer to the [Troubleshooting](en_securemr-troubleshooting) guide to deal with the issues you encounter while using PICO SecureMR.


# --- END: Overview(4).md ---



# --- BEGIN: Overview(5).md ---

Social interaction is an essential part of app experience. The Social Interaction service provided by the SDK enables users to enjoy your app with their friends and share their experiences on social platforms.
## Uses
You can provide a variety of social interaction experiences for your users.

* **Interact with friends**
   * Users can invite friends to their destinations.
   * Users can proactively join their friends' destinations.
* **Jump between apps**
   * Users can jump from the current app to another app. 
   * Users can jump to the details page of the current app in the PICO Store. 
* **Share content**
   Users can share screenshots or videos from the current app to the "[Douyin](https://www.douyin.com/)" app.

## Learn more
If you would like to learn more, you can proceed to read the following articles:

* [Key concepts](/13136/en_social-interaction-key-concepts): Learn the definitions of key concepts plus how they function and co-work with each other.
* [Platform service setups](/13136/en_social-interaction-platform-service-setups): Provides a step-by-step guide on how to create destinations.
* [Use cases](/13136/en_social-interaction-use-cases): Check out the detailed descriptions and code samples for different use cases.
* [API list](/13136/en_social-interaction-api-list): Check out the APIs that you can use to implement the Social Interaction service.
* [Demo](/13136/en_social-interaction-demo): Download and play the Space Arena Party demo on the Unity Editor and your PICO device.


# --- END: Overview(5).md ---



# --- BEGIN: Overview(6).md ---

Leaderboard is one of the basic and important features of an app. By displaying users' rankings to each other, leaderboards can give rise to a healthy competitive atmosphere among users.
## Use cases

* **Get leaderboard information and entries**
   Supports retrieving the information and entries of leaderboards.
* **Update leaderboard entries**
   Supports updating a user's entry when the user's score or other ranking-related metrics change.

## Related articles

* [Service design](/en_leaderboards-service-design): Learn the leaderboard service's functional design covering its unique identifier, entries, and more.
* [Platform service setups](/en_leaderboards-platform-service-setups): Complete general platform service setups and create a learboard for your app.
* [Use cases & code samples](/en_leaderboards-use-cases-and-code-samples): Learn the use cases of leaderboard service and check out the code samples for development.
* [Parameter details](/en_leaderboards-parameter-details): Learn the `filter`, `startAt`, `pageSize`, and `pageIdx` parameters that need to be passed when retrieving leaderboard entries.
* [API list](/en_leaderboards-api-list): Get an overview of leaderboard APIs.
* [Demo](/en_leaderboards-demo): Try out our leaderboard demo in the Unity Editor or on your PICO device.


# --- END: Overview(6).md ---



# --- BEGIN: Overview(7).md ---

Incorporating achievements into your app can create a positive feedback loop, increase its level of challenge, and boost user engagement. By offering prizes like trophies and badges, you can reward users for accomplishing specific goals, such as finishing the beginner tutorial or reaching a particular level.
Below are related articles:

* [Service design](/en_achievements-service-design): Learn the achievement service's functional design.
* [Platform service setups](/en_achievements-platform-service-setups): Complete general platform service setups and create achievements for your app.
* [Use cases & code samples](/en_achievements-use-cases-and-code-samples): Learn the use cases of achievement service and check out the code samples for development.
* [API list](/en_achievements-api-list): Get an overview of achievement APIs.
* [Demo](/en_achievements-demo): Try out our achievement demo in the Unity Editor or on your PICO device.


# --- END: Overview(7).md ---



# --- BEGIN: Overview.md ---

VR compositor layers are used to display information, text, video, or texture that is intended to be the focal part of a scene or to display simple environments and backgrounds.
In general, when rendering VR content, the left-eye and right-eye cameras firstly render the content to the eye buffer, and then the ATW thread distorts and samples the eye buffer, after which the content is rendered to the screen.
With VR compositor layers, the content is directly passed to the ATW thread for processing such as distortion, sampling, and synthesis. The whole rendering process is therefore simplified.
## Limitations

* Currently, a single scene supports up to 7 compositor layers, but it is recommended not to exceed 4 layers.
* Nearby objects should occlude distant ones, otherwise slight shakes can occur to cause visual discomfort.
* If you are using the Universal Render Pipeline (URP) in your project, and you need to use underlay layers at the same time, you must disable HDR. Otherwise, the underlay layers will not work.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43e97d637b0b40fa81c793cc3a2cee6e~tplv-goo7wpa0wc-image.image)


# --- END: Overview.md ---



# --- BEGIN: PICO Developer Center quickstart.md ---

If you are using the PICO Unreal Integration SDK, read [this article](https://developer-global.pico-interactive.com/document/ue4/pdc-tool).

PICO Developer Center (referred to as PDC tools below) is a developer service platform that integrates essential tools like the ADB command debugging tool and real-time preview tool. You can efficiently manage, develop, and debug your apps using the PDC tool.
## Requirements

* **Operating system**: Windows 10 20H2 or later, macOS Intel, macOS Apple Silicon
* **CPU**: Intel Core i5-4590 / AMD Fx8350 or later
* **RAM**: 8GB or higher
* **Graphics card**: NVIDIA GeForce GTX 1060 6GB / AMD Radeon RX 480 or higher
* **PICO VR headset**: PICO Neo3, PICO 4, and PICO 4 Ultra series
* **PICO VR headset's system version**: 5.11.0 or later

## Important notes

* Using the PICO Connect app will cause the PDC streaming service to malfunction. Therefore, before using the PDC tool, ensure you have closed the PICO Connect app on both your PC and headset.
* Using the PICO Connect app and the PDC tool together will cause exceptions to the PDC tool. Therefore, make sure to close the PICO Connect software on both your PC and HMD before using the PDC tool.
   This restriction does not apply to PICO 4 Ultra or Project Swan series devices.

* The command prompt (cmd) needs to be in English, otherwise the PDC tool may not recognize that the streaming is properly installed.
* Currently, if there is a virtual graphics card (GPU) present on the PC, using the PDC tool for live preview may still experience a black screen issue. In this case, it is necessary to go to **Device Manager** > **Display Adapters** and disable the virtual GPU.
* If the Windows system has the power-saving mode enabled, it's possible that the PDC tool may fail to detect the USB connection status of the device. In this case, it is necessary to go to **Control Panel** > **Hardware and Sound** > **Power Options** > **Change plan settings** > **Change** **advaneced power settings**, then disable **USB selective suspend** **setting** in **USB settings**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/241969d9520d4140bb0231a5daeb5d09~tplv-goo7wpa0wc-image.image)
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a49b784c96344308a66dfcded09a0623~tplv-goo7wpa0wc-image.image)

## Before you begin
Before using the PDC tool, you need to do the following: install the PDC tool to your computer, enable the "Developer" mode for your headset, and use a USB cable to connect your headset and computer.
### Install the PDC tool
Download and install the [PICO Developer Center](https://developer-global.pico-interactive.com/resources/#pdc) on your computer. The PDC tool's installation package needs to be run as an administrator. During installation, an authorization window will pop up, and you need to grant permission.
### Install the streaming service
If you need to connect your PICO device to the PDC tool, you need to install the streaming service. For detailed instructions, refer to "[Install the streaming service](https://arcosite.bytedance.net/download-streaming-service)".
### Enable the "Developer" mode for the headset
You need to enable the "Developer" mode for your headset; otherwise, the PDC tool will not display device information once the headset and computer are connected. Below are the steps to follow:

1. Turn on your PICO VR headset. 
2. Go to **Settings** > **General** > **About**.
3. Keep clicking on the **Software Version** field until the **Developer** option appears at the bottom of the left navigation pane. 
4. Click **Developer**. 
5. In the **Developer** section, enable **USB Debug**. 
6. (Only for PICO 4 Ultra) Go to **Settings** > **General**, toggle the **PICO Connect Auto Discovery** switch off and then toggle it on again to enable the streaming mode for the PDC tool.

### Connect the headset and PC

1. Launch the PDC tool, select your region, and log in with your PICO Developer account.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4aaebf0dd0f4dd2bb6b97089b3a714e~tplv-goo7wpa0wc-image.image)
2. Use a USB cable to connect the headset and computer. If connected, the **Device Information** pane will display the information of the connected device.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efead1eae68b4830a1655e43ae919fec~tplv-goo7wpa0wc-image.image)

## Use the PDC tool

* [Debug adb commands](/13136/en_create-and-debug-adb-commands)
* [Preview app scenes in real time](/13136/en_preview-app-scenes)
* [Monitor device performance](/13136/monitor-device-performance)
* [Capture, record, and cast screen](/13136/quick-tools)
* [Download resources](/en_download-developer-tools), including SDKs, developer tools, and samples. 
* [Push URLs to a PICO device](/en_push-url-to-pico-device)
* Submit feedback

About device status
After connecting the headset and PC using a USB cable, the PDC tool screen will display one of the following device statuses:
| **Status** | **Description** |
| --- | --- |
| Connected | The device and PC are connected and the streaming service is working normally. |
| Streaming | Preview is working normally. |
| Connection failed | The ADB or streaming service is abnormal. |
## Access logs
If you come across issues while using the PDC tool, you can check logs for troubleshooting.
### Enable "Log Records"
On your device, go to **Settings** > **General**, and toggle the **Log Records** switch. Logs generated while running the PDC tool will then be recoded and stored.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a86a9d0a1e416bbb43092305b75e3a~tplv-goo7wpa0wc-image.image)
### Log paths
**PC logs:**
| **OS** | **Log Paths** |
| --- | --- |
| Windows | * PDC: C:\Users\${user}\AppData\Roaming\PICO Developer Center\logs <br> * Streaming service:  <br>    * Project Swan: C:\ProgramData\PICO\PICO Streaming Service <br>    * Other device models: C:\Program Files\Streaming Service\ps_server.log  |
| macOS | * PDC: ～/Library/Application Support/PICO Developer Center/logs <br> * Streaming service: <br>    * Project Swan: ~/Library/Application Support/PICO Streaming Service/swan <br>    * Other device models: ～/Library/Application Support/PICO Streaming Service/ |
**HMD logs:**
Use command `adb shell setprop persist.log.tag D` to enable Debug logs (skip this step for PICO 4 Ultra and Project Swan series devices), then use command `adb pull data/logs` to pull the logs to local storage.


# --- END: PICO Developer Center quickstart.md ---



# --- BEGIN: Platform services overview.md ---

This article walks you through the use cases of platform services, the platform services provided by PICO, the procedure for using PICO's platform services, and the information on asynchronous API calls.
## Use cases
Platform services are fundamental and necessary for apps. You can provide users with a unique experience by using one or multiple platform services in your app. Below are the key benefits of platform services:

* **Security**
   Protect your app and users through identity verification and entitlement check.
* **Revenue**
    Grow your revenue by using in-app purchases, subscriptions, etc.
* **Social interaction**
   Enable users to experience the joy of socializing within the app through adding others as friends, playing with others via matchmaking, etc.
* **Engagement**
   Give rise to a competitive atmosphere in your app by creating achievements and leaderboards.

## Important note
Platform services only support developing 64-bit apps.
## PICO's platform services
PICO SDK provides the following platform services:
| **Service Name** | **Description** |
| --- | --- |
| Accounts & Friends | Account & Friends service allows you to access the info of a specified account, get the friends list of the currently logged-in users, enable users to send friend requests, and more.  |
| Account linking | Account linking links users' PICO accounts to your self-established account system. You can retrieve users' PICO account information, allowing them to log in to your app using their PICO accounts. |
| RTC | Real-time communications (RTC) service enables users in the same room to communicate with each other through voice chat.  |
| Speech-to-text | The speech-to-text service uses the automatic speech recognition (ASR) technology to support real-time recognition of speech and conversion into text. |
| Room & Matchmaking | Room & Matchmaking service enables player-to-player networking, matchmaking, room management, and inter-player messaging. Its major features are room management, matchmaking, and messaging. |
| Social interaction | Social interaction is an important part of app experience. Users can have social and sharing experiences in your apps, such as inviting friends or joining friends to play a game together. |
| Leaderboard | Leaderboard is one of the basic and important features of an app. By displaying users' rankings in a multi-dimensional approach, leaderboards can give rise to a competitive atmosphere among users. |
| Achievement | Achievements help build a "positive feedback mechanism" in your games. You can  distribute prizes to users when they hit specific goals. |
| Challenge | Challenges create fun-to-join competitions among users, which can therefore provide users with more opportunities to interact with others. Both you and your app's users are able to create challenges. |
| Highlights | Highlights service is used to record users' amazing moments while using your app. Users can save these moments as images or videos, review and share them later. |
| In-app purchase (IAP) | You can diversify user experience and grow your revenue by selling products such as cosmetics, props, and coins/diamonds within your app.  |
| Downloadable content (DLC) | Downloadable content (DLC) represents the contents/files such as expansion packs that users can purchase and download, which can help grow your revenue. |
| Subscription | Subscriptions provide a recurring payment model that allows users to purchase the premium content in your app.  |
| Exercise data authorization | You can use users' exercise data to better understand their exercise habits, then optimize your app accordingly to provide users with a better exercise experience. |
| Cloud storage | Cloud storage is used to back up users' app data, such as identities, custom settings, preference settings, and game progress, on specific devices. |
| Profanity detection | Profanity detection service enables the detection of profane words in texts such as user names, room names, and in-room-chat messages. |
## Procedure for using platform services

1. Register on the PICO Developer Platform, set up the development environment, import the PICO Unity Integration SDK into your project, and complete project settings. Refer to the "[Quicksart](/en_create-a-developer-account-organization-and-app)" guide for detailed instructions.
2. Initializes platform services. If you would like to use game-related services (Room & Matchmaking, Leaderboard, Achievement, Challenge), you need to initialize the game module as well. Refer to the "[Initilization](/en_initialization)" article for detailed instructions.
3. Integrate desired platform services into your app. Refer to the guides and [client API reference](/reference/unity/client-api/AchievementsService/) of desired platform services for details instructions. If you would like to enable your app to access PICO's server, you need to use server APIs. Refer to the [server API reference](/reference/unity-server/latest/) for details.

## Use asynchronous API calls 
Starting from version 2.1.4, you can use the async/await method to asynchronously call platform service APIs. This method makes the code clearer when executing multiple requests in a serial manner. 
For example, when using `UserService.GetLoggedInUser` to retrieve the current logged-in user, you must set a callback function in the `Task<T>.OnComplete()` function without using the async/await method. 
```C#
UserService.GetLoggedInUser().OnComplete(m =>
{
    if (m.IsError)
    {
        Debug.Log($"GetLoggedInUser failed:code={m.Error.Code} message={m.Error.Message}");
        return;
    }
    Log($"DisplayName={m.Data.DisplayName} UserId={m.Data.ID}");
});
```

If you use the async/await method, calling `Task<T>.Async()` will return an asynchronous task `System.Threading.Tasks.Task<Message<T>>`. After executing the await expression, you can obtain the final result of the request. 
```C#
var userMessage = await UserService.GetLoggedInUser().Async();
if (userMessage.IsError)
{
    Debug.Log($"GetLoggedInUser failed:code={userMessage.Error.Code} message={userMessage.Error.Message}");
    return;
}
Log($"DisplayName={userMessage.Data.DisplayName} UserId={userMessage.Data.ID}");
```


# --- END: Platform services overview.md ---



# --- BEGIN: Project Validation.md ---

Project Validation can display the validation rules required by the installed XR package. For any validation rules that are not properly set up, you can use this feature to automatically fix them with a single click. This article introduces how to use the Project Validation feature.
## Validation statuses
After checking the XR package, the system will match validation rules with corresponding status icons and show them.
| **Status Icon** | **Description** |
| --- | --- |
| ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88c76f5063c147b8a6baefdca07ec000~tplv-goo7wpa0wc-image.image) | This validation rule is correctly set up or is not applicable. |
| ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08771b452d70410c905512e9a9d08bde~tplv-goo7wpa0wc-image.image) | This is an optional validation rule. This rule is not correctly set up, but it will not block the building of your project. You can ignore this rule according to your project configuration. |
| ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5534b9f0db7d48b8b2a187ebd3306743~tplv-goo7wpa0wc-image.image) | This is a required validation rule. This rule is not correctly set up and it will block the building of your project. You must fix this issue. |
## Validation rules
Validation rules are categorized into Required (required configuration), Recommended (recommended configuration), and Optional (optiopnal configuration).

* **Required configuration：**
   * Check if `minSdkVersion` is greater than `AndroidApiLevel29`. If not, report an error.
   * When **Target Architectures** is set to **ARM64**, check if **IL2CPP** is selected. If not, report an error.
   * Check if there is only one object with the Tag `MainCamera` in the currently opened scene. If not, report an error.
   * Check if there is only one **Audio Listener** in the currently opened scene. If not, report an error.
   * Check if the project's target build platform is set to **Android**. If not, report an error.
   * Check if **PICO** is selected in the **Plug-in Providers** list. If not, report an error.
   * Check if **Scripting Backend** is set to **IL2CPP** and **Target Architectures** is set to **ARM64**. If not, report an error.
   * Check if **Graphics API** is set to either **Vulkan** or **OpenGLES3.0**. If not, report an error.
   * When using **Unity 2022** and **Vulkan** together, check if the **Development Build** option is selected. If selected, report an error.
   * Check if Unity 2022.1.14, URP, Linear color space, MSAAx4, and OpenGLES are used together. If so, report an error.
   * Check if the currently opened scene has the **PXR_Manager (Script)** component added. If not, report an error.
   * When using Eye Tracked Foveated Rendering (ETFR), check if the first item in the **Graphics API** list is **OpenGLES3.0**. If not, report an error.
   * When configuring Face Tracking, check if the **unsafe code** option is enabled. If not, report an error.
   * When using URP, check if the **HDR** option is enabled. If it is, report an error.
   * When using URP, check if both **Scriptable Render Pipeline Settings** and **Render Pipeline Asset** are properly configured. If not, report an error.
   * When using mixed reality-related functionalities, check if **Scripting Backend** is set to **IL2CPP** and **Target Architectures** is set to **ARM64**. If not, report an error.
   * Check if there is only one **XR Origin** object in the current scene. If not, report an error.
   * Check if the `keystoreName` and `keystorePass` fields in **Project Keystore** are empty. If they are, report an error.
   * Check if the `keyaliasName` and `keyaliasPass` fields in **Project Key** are empty. If they are, report an error.
   * Check if **Default Orientation** is set to **LandscapeLeft**. If not, report an error.
   * Check if **Application Entry Point** is set to **Activity**. If not, report an error.
   * Check if the **Write Permission** parameter is set to **External( SDCard)** and Android API's version is later than 32.
   * Check if the currently used Unity version is supported by the current SDK version. If not, report an error.
   * When URP is enabled, check if the Main Camera in the current scene has Video Seethrough set and whether post processing has been enabled for the Main Camera. If both conditions are met, report an error.
   * Check if the Fixed Foveated Rendering functionality is enabled while using URP. If so, an error will be reported.
   * When Application SpaceWarp (AppSW) is enabled, check if the current Unity version is 2021 LTS or later. If not, report an error.
   * When the Late Latching functionality is enabled, check if the current Unity version is 2021.3.19f or later and is earlier than 2022. If not, report an error.
   * Whether composition layers (Overlay/Underlay) and the Late Latching functionality are used simultaneously in the current project. If so, report an error.
   * Check if the number of composition layers in the current scene exceeds 7, which is the supported maximum. If so,report an error.
   * Check if the Super Resolution and Subsampling functionalities are used simultaneously in the current project. If so, report an error.
   * Check if the Sharpening and Subsampling functionalities are used simultaneously in the current project. If so, report an error.
   * When the current project uses Unity 6, URP, OpenGLES, and Multipass, check if MSAA is disabled. If it is not disabled, report an error.
   * Check if the current project uses Vulkan and MRC, check if the **Color Space** parameter is set to **Linear**. If not, report an error.
* **Recommended configuration:**
   * Check if `targetSdkVersion` is set to **Auto**. If not, report an error.
   * If **Install Location** is set to **Auto**. If not, report an error.
   * Check if `Physics.defaultContactOffset` is greater than or equal to `0.01f`. If not, report an error.
   * Check if `Physics.sleepThreshold` is greater than or equal to `0.005f`. If not, report an error.
   * Check if `Physics.defaultSolverIterations` is less than or equal to `8`. If not, report an error.
   * Check if `QualitySettings.pixelLightCount` is less than or equal to `1`. If not, report an error.
   * Check if `QualitySettings.globalTextureMipmapLimit` is equal to `0`. If not, report an error.
   * Check if `QualitySettings.anisotropicFiltering` is set to `AnisotropicFiltering.Enable`. If not, report an error.
   * Check if `androidBuildSubtarget` is set to **ETC2** or **ASTC**. If not, report an error.
   * Check if **Color Space** is set to **Linear**. If not, report an error.
   * Check if **Graphics Jobs** option is enabled. If it is, report an error.
   * Check if multithreaded rendering is enabled. If not, report an error.
   * Check if **Use 32-bit Display Buffer** option is enabled. If not, report an error.
   * Check if **Rendering Path** is set to **Forward**. If not, report an error.
   * Check if **Stereo Rendering Mode** is set to **Multiview**. If not, report an error.
   * Check if **Intermediate Texture Mode** is set to **Auto**. If not, report an error. 
   * When using URP, check if **Screen Space Ambient Occlusion** is disabled. If not, report an error.
   * When using Fixed Foveated Rendering (FFR) and Eye Tracked Foveated Rendering (ETFR), check if **Subsampling** is enabled. If not, report an error.
   * Check if the **Use Recommended MSAA** checkbox is selected. If not, report an error.
   * Check if App SpaceWarp (AppSW) and Content Protection are both enabled at the same time. If so, report an error.
   * In the current scene, check if **Tracking Origin Mode** is set to **Not Specified**. If so, report an error.
   * Check if the URP package has been downloaded but not configured or used. If so, report an error.
   * Check if the number of composition layers in the current scene exceeds 4, which is the recommended number. If so, report an error.
   * When using Unity6, check if the current project has the **Run In Background** option checked. If not, report an error.
   * Check if the **MRC** checkbox is checked in the **PXR_Manager (Script)** panel. If not, report an error.
   *  Verify if the **Display Refresh Rates** parameter is set to **Default**. If not, report an error.
   *  When using Vulkan, check if the **Optimize Buffer Discards** option is checked. If not, report an error.
* **Optional configuration:**
   * Check if `Lightmapping.realtimeGI` is disabled. If not, report an error.
   * Check if **GPU Skinning** is enabled. If not, report an error.
   * Check if the **Eye Tracking Calibration** option is selected when using Eye Tracking or Eye Tracked Foveated Rendering. If not, report an error.

## Prerequisites
The SDK version should be 3.0.0 or later. You can go to the [PICO Developer Platform](https://developer.picoxr.com/resources/#sdk) to download the latest SDK.
## Procedure for validating your project

1. Open your project in the Unity Editor.
2. Go to **Edit** > **Project Settings** > **XR Plug-in Management** > **Project Validation**.
   You'll see the following Project Validation panel, which shows the validation rules that are not correctly set up.
   **Note**
   
   * Keep the default setting (**Turn Off**) of the **Selected Profiles** parameter.
   * To show the validation rules that are correctly set up or are not applicable, check the **Show all** checkbox.

   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bd92f427aac4120a6c1113ee885afe4~tplv-goo7wpa0wc-image.image)
3. Click the **Fix All** button to fix all configuration issues, or click the **Fix** button to fix a specified issue.
   **Note**
   For a required validation rule that is not correctly set up, if you do not want it to block the building of your project, you can check the **Ignore build errors** checkbox to ignore this rule. Consequently, the related XR features may not work properly.


# --- END: Project Validation.md ---



# --- BEGIN: Quickstart.md ---

This quick start guide for PICO SecureMR introduces how to implement SecureMR capabilities within PICO applications.
## Requirements

* PICO device model: PICO 4 Ultra series
* PICO device system version: 5.13.0 or later

## Procedure
### Step 1: Enable SecureMR capabilities
On the **PXR_Manager (Script)** panel, check the **SecureMR** checkbox to enable the system-level SecureMR capabilities for the application.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db3f1e0f069f4f9d808faf334289d74c~tplv-goo7wpa0wc-image.image" width="400px" />

### Step 2: Configure the video see-through feature
Video Seethrough (VST) can break the fully enclosed virtual environment provided by VR headsets. It uses the cameras on the headset to collect real-time views of the surrounding environment, and then presents them on the headset screen through image processing algorithms, allowing users to directly view the real-world scene on the headset screen. Eventually, the VST image can be fused with the virtual scene in the application to present a mixed-reality effect. Therefore, VST is the foundation for implementing SecureMR capabilities. Refer to [this article](/en_seethrough) to configure the VST feature for the application. 
### Step 3: Implement SecureMR capabilities
Implement SecureMR capabilities within the application for typical user experiences, such as displaying glTF models and using glTF models to show VST images. For details, refer to [SecureMR use cases](/en_securemr-use-cases).


# --- END: Quickstart.md ---



# --- BEGIN: Sense Pack overview.md ---

Sense pack includes mixed reality-related features, including video seethrough, spatial anchors, and space calibration, enabling you to blend the real and virtual environments in a scene. The physical and digital objects in the scene coexist and interact in real time.
## Important note
Sense pack only supports developing 64-bit apps.
## What's in the Sense Pack
| **Name** | **Description** |
| --- | --- |
| Video Seethrough | Video seethough (VST) enables the real physical environment to be displayed on the screen of the PICO VR headset in real time. |
| Spatial Anchor | Spatial anchors enable the alignment of positions between a virtual environment and the real world. It is used to anchor virtual objects to locations or objects in the physical world. Once anchored, users will see virtual objects at the same anchor positions if they re-enter the same space multiple times using the same PICO device. |
| Shared Spatial Anchor | Within the same physical space, the Shared Spatial Anchors feature allows users to share scene content when experiencing the same app. |
| Spatial Mesh | Spatial meshes are primarily the representation of the physical environment in a mixed reality scene. By reconstructing the physical environment into spatial meshes, it becomes easier to enable interactions between virtual and real-world objects.  |
| Scene Capture | The Room Capture app is PICO's system-level app used for space calibration. Users can use it to calibrate the walls, doors, windows, tables, sofas, and more other objects in a real space, enabling them to interact with virtual objects. You can use the SDK to retrieve the spaces and calibration information created by the Room Capture app and use them in your own apps. |
| MR Safeguard | When the distance between the objects in the virtual scene and the PICO headset or controllers is within a certain range, the virtual scene will become semi-transparent, revealing the real-world scene. |
## Mixed reality sample
The PICO Mixed Reality Sample is a technical sample project that demonstrates the MR features in the PICO Unity Integration SDK, including video passthrough, scene calibration, spatial mesh, spatial anchors, shared spatial anchors, and more. 
In this sample, you can find example MR application scenarios such as room decoration and shooting mini-games. Additionally, this project provides minimal scenes for using the feature APIs. Developers can experience MR functionalities with simulated data in the Unity Editor or by building individual scenes for testing.
For more information, refer to [this article](/en_mixed-reality-sample).


# --- END: Sense Pack overview.md ---

