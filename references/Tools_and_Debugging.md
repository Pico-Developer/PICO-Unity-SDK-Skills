# Tools and Debugging

## Table of Contents
- Create and debug adb commands
- Debug tensors in pipelines
- How to get DEBUG logs_
- Metrics HUD
- Monitor app performance
- Monitor device performance
- PC-End Debugging Tool
- PICO Command Line Utility
- PICO Debugger
- PICO Developer Center quickstart
- PICO Emulator (Beta)
- PICO Graphics Probe Tool
- PICO Haptic Editor
- RenderDoc for PICO
- Snapdragon Profiler
- View draw calls
- View overdraw
- XR Profiling Toolkit

---



# --- BEGIN: Create and debug adb commands.md ---

You can use the PDC tool to debug system default commands or create and debug custom commands.
## Before you begin
Refer to the "[PICO Developer Center overview](/13136/en_pdc-basic-info#f5a5a632)" article to complete preparatory tasks, including installing the PDC tool, enabling the "Developer" mode for your PICO device, and connecting your PICO device to the PC.
## **Debug system default commands**
The PDC tool provides the following default adb commands:
| **Feature** | **Command** |
| --- | --- |
| Enable/disbale Wi-Fi | Enable: `adb shell svc wifi enable` <br> disable: `adb shell svc wifi disable` |
| Mute/resume audio <br>  | Mute：`adb shell media volume --stream 3 --set 0` <br> Resume audio：`adb shell media volume --stream 3 --set 8` <br> ***Note***: PICO 4 Ultra or Project Swan series devices do not support muting or resuming audio using the above commands. Instead, you can mute or resume audio by repeatedly calling the `adb shell input keyevent 24` and `adb shell input keyevent 25` commands. |
| Shut down the device | `adb shutdown` |
| Reboot the device | `adb reboot` |
## **Create and debug custom commands**
Use the following steps to create an adb command. After creation, you can run, edit, or delete the command as needed.

1. In the **ADB Command** pane, click **+ Create Command** or **Add**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2496e51b3745417880fdb537464b8177~tplv-goo7wpa0wc-image.image)
   The **Create Command** pop-up window appears:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/627549ef053f4dc8a62d83fd030d0a1b~tplv-goo7wpa0wc-image.image)
2. Enter the **Command Name** and **Command Content**. 
   For command content, you do not need to enter `adb` which will be automatically added by the system. For example, you can enter `devices` for `adb devices` and `shell getprop` for `adb shell getprop`.
3. (Optional) Select **Display the output in a new window**. Once selected, the following pop-up showing command execution information will appear when you run the command:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bb6653d642142d1b8b11405b1335370~tplv-goo7wpa0wc-image.image)
4. Click **Save**.

  This adb command will appear in the command list.

5. Perform the following operations as needed:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4b73f631f8346d8aa8408f2c1cd2baf~tplv-goo7wpa0wc-image.image)
   | **No.** | **Description** |
   | --- | --- |
   | 1 | Click **Run** to run the command. |
   | 2 | Click **Edit** to edit the command. |
   | 3 | Click **Delete** to delete the command. |


# --- END: Create and debug adb commands.md ---



# --- BEGIN: Debug tensors in pipelines.md ---

In the SecureMR pipeline, tensors are used as the primary data structure for data flow. There are two types of tensors: global tensors, which can be shared across pipelines, and local tensors, which are created and used exclusively within a single pipeline. Additionally, placeholders are used to map global tensors for use inside individual pipelines. 
However, these tensors are typically inaccessible at the application level—developers can write data to tensors but cannot read or save their contents. This limitation can make debugging, particularly during the integration of machine learning models, challenging. 
This article presents several methods for inspecting tensor values within the SecureMR pipeline. These techniques are intended to assist developers in debugging and building apps using SecureMR more effectively. 
## Use text renderer to render tensor values 
The RenderText operation takes a "text" operand as input. This input can be a UTF-8 encoded string or any tensor type (for example, Matrix, Vector, or Scalar). When a tensor is provided, the renderer visualizes its contents by displaying a matrix representation of the values. 
By default, the renderer displays up to a 5x5 matrix to summarize the tensor data. This is useful for quickly inspecting the contents of a tensor during pipeline execution, especially when debugging intermediate outputs or verifying model inference results.
```Java
private void CreateTextRenderer(var textTensor)
{        
    // Operand 1: start
    var start  = new float[] {0.1f, 0.3f};
    var startDim = new[] { 1 };
    var startTensorShape = new TensorShape(startDim);
    var startTensor = pipeline.CreateTensor<float, Point>(2, startTensorShape, start);
    
    // Operand 2: colors
    var colors = new byte[] {255, 255, 255, 255, 0, 0, 0, 255}; // white text, black background
    var colorDim = new[] { 2 }; //we have two colors
    var colorTensorShape = new TensorShape(colorDim);
    var colorTensor = pipeline.CreateTensor<byte, Color>(4, colorTensorShape, colors);
    
    //Create global gltf tensor
    gltfTensor = provider.CreateTensor<Gltf>(tvGltfAsset.bytes);
    
    //Create placeholder tensor in pipeline
    gltfTensorPlaceholder = pipeline.CreateTensorReference<Gltf>();
    
    //Operand 4: textureID
    var textureID = new ushort[] {0};
    var texIDDim = new[] { 1 };
    var texIDShape = new TensorShape(texIDDim);
    var textureIDTensor = pipeline.CreateTensor<ushort, Scalar>(1, texIDShape, textureID);
    
    //Operand 5: font size
    var fontSize = new [] {72.0f};
    var fontSizeDim = new[] { 1 };
    var fontSizeShape = new TensorShape(fontSizeDim);
    var fontSizeTensor = pipeline.CreateTensor<float, Scalar>(1, fontSizeShape, fontSize);

    // Create render text operator
    var renderTextOperatorConfiguration = new RenderTextOperatorConfiguration(SecureMRFontTypeface.SansSerif, "en-US", 1440, 960);
    var renderTextOperator = pipeline.CreateOperator<RenderTextOperator>(renderTextOperatorConfiguration);

    renderTextOperator.SetOperand("text", textTensor);
    renderTextOperator.SetOperand("start", startTensor);
    renderTextOperator.SetOperand("colors", colorTensor);
    renderTextOperator.SetOperand("texture ID", textureIDTensor);
    renderTextOperator.SetOperand("font size", fontSizeTensor);
    renderTextOperator.SetOperand("gltf", gltfTensorPlaceholder);

    // update gltf operator
    var pose = new float[] {0.5f, 0.0f, 0.0f, 0.0f,
        0.0f, 0.5f, 0.0f, 0.0f,
        0.0f, 0.0f, 0.5f, -0.5f,
        0.0f, 0.0f, 0.0f, 1.0f};
    var poseDim = new[] { 4, 4 };
    var poseShape = new TensorShape(poseDim);   
    var poseTensor = pipeline.CreateTensor<float, Matrix>(1, poseShape, pose);
    var renderGltfOperator = pipeline.CreateOperator<SwitchGltfRenderStatusOperator>();
    
    renderGltfOperator.SetOperand("gltf", gltfTensorPlaceholder);
    renderGltfOperator.SetOperand("world pose", poseTensor);
    renderGltfOperator.SetOperand("view locked", poseTensor);
    renderGltfOperator.SetOperand("visible", isTestPassed);
}
```


# --- END: Debug tensors in pipelines.md ---



# --- BEGIN: How to get DEBUG logs_.md ---

By default, INFO logs are provides. DEBUG log level is lower than INFO log level. Therefore, if you want to get DEBUG logs, you need to use the `adb shell setprop persist.log.tag V` command to downgrade log level first.


# --- END: How to get DEBUG logs_.md ---



# --- BEGIN: Metrics HUD.md ---

You can use the Metrics HUD to monitor your device's performance via a variety of metrics.
## Requirement
The VR headset's system version should be 5.4.0 or later.
## Before you begin
Use the following steps to enable the "Developer" mode for your device.

1. Turn on your PICO VR headset.
2. Go to **Settings** > **General**.
3. Keep clicking on the **Software Version** field until the **Developer** option appears at the bottom of the left navigation pane.
4. Click **Developer**.
5. On the **Developer** screen, enable **USB Debugging**.
   The "Developer" option has been enabled for your PICO VR headset.

## Enable Metrics HUD
Use the following steps to enable Metrics HUD on the device.

1. Turn on your VR headset.
2. Go to **Settings** > **Developer**.
3. Toggle the **Enable Metrics HUD** switch.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e7b52c9e8c0402691a7516e84cce877~tplv-goo7wpa0wc-image.image)

## Configure settings
### Basic settings
On the **SETTINGS** pane, set the parameters related to the display of Metrics HUD.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/289a45240b814ea08d9b933c0c08c625~tplv-goo7wpa0wc-image.image" width="470px" />

| **Parameter** | **Description** |
| --- | --- |
| Quick-set Enabled Stats | NONE: do not display the Metrics HUD. <br> BASIC: display basic metrics on the HUD. |
| Display Stats on Overlay <br>  | Set whether to display the real-time metric statistics as shown in the red frame below. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4066351a9fd64fdfb510d0aca22bafa5~tplv-goo7wpa0wc-image.image) |
| Display Graph on Overlay | Set whether to display the real-time metric graph as shown in the red frame below. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18357bd9858644e59617053a1430d8a6~tplv-goo7wpa0wc-image.image) |
| Scale | Set the size of the HUD. |
| Distance | Set the distance between the eyes and the HUD. |
| Pitch | Set the HUD's pitch angle along the X-axis. |
| Yaw | Set the HUD's yaw angle along the Y-axis. |
### Select metrics
On the **STATS** pane, select the performance metrics that you would like to monitor. For available metrics and descriptions, refer to the "Metrics description" section.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/789d0382e15c4c0db862a6e670da6828~tplv-goo7wpa0wc-image.image" width="546px" />

| **Option** | **Description** |
| --- | --- |
| Enable | You can check the box to display a corresponding metric on the HUD. |
| Graph | You can check the box to display a corresponding metrics in the form of a graph. |
## Metric reference
| **Metric Name** | **Description** |
| --- | --- |
| GPU Utilization (GPU U) | Overall GPU utilization rate (%). |
| CPU Utilization (CPU U) | Overall CPU utilization rate (%). |
| FPS (FPS) | Framerate (FPS) <br> ***Note***: Normally speaking, an app's framerate is the same as the display's refresh rate. |
| Available Memory (A MEM) | Available memory (MB). |
| Performance Score (Perf S) <br>  | The device's overall performance: <br>  <br> * <80: good performance <br> * [80,100]: in certain situations, there may be FPS drops, such as during extended periods of operation, particular overloaded scenes, frequency limitations due to low battery, power outages, and so forth. <br> * >100: frequent framerate drops |
| Foveation Level (FRL) | The foveated rendering level used by the app. The higher the level, the lower the GPU utilization rate and the blurrier the area around the foveal point. There are four values indicating different foveation levels: <br>  <br> * -1: disabled <br> * 0: low <br> * 1: medium <br> * 2: high <br> * 3: top high |
| Eye Buffer Width (EBW)  | The width of the rendered texture. <br> Resolution directly affects the GPU rendering time. For the fragment shader, the higher the resolution you require (i.e., the more the pixels), the longer the rendering time. |
| Eye Buffer Height (EBH) <br>  | The height of the rendered texture. <br> Resolution directly affects the GPU rendering time. For the fragment shader, the higher the resolution you require (i.e., the more the pixels), the longer the rendering time. |
| Used Memory (U MEM) | Used memory (MB). |
| Singlepass | Is Multiple rendering enabled: <br>  <br> * 0: disabled <br> * 1: enabled |
| CPU Temperature | The device's CPU temperature (°C). |
| GPU Temperature | The device's GPU temperature (°C). |
| CPU Level (CPU L) | The CPU level you set for the app. The higher the level, the higher the CPU utilization. The default level is 0, indicating that the system automatically adjusts the app's CPU level. |
| GPU Level (GPU L) | The GPU level you set for the app. The higher the level, the higher the GPU utilization. The default level is 0, indicating that the system automatically adjusts the app's GPU level. |
| Display Refresh Rate (DRR) | The device's display refresh rate, which can be 72/90/120 Hz. |
| Battery Level (BAT) | The device's battery level (%). |
| Battery Temperature (B TEM) | The device's battery temperature (°C). |
| Power Voltage (POW V) | The device's power voltage (mV). |
| App VSS (VSS) | The total amount of virtual memory that the app is using. |
| App PSS (PSS) | The actual amount of physical memory (RAM) that the app is using. |
| App RSS (RSS) | The amount of physical memory (RAM) occupied by the app. |
| Battery Current ( BAT C) | The current from the battery (mA). |
| GPU Frequency ( GPU F) | The GPU clock speed, which indicates how fast the cores of the GPU are. |
| CPU Frequency (covers core0 to core7, including CPU0 F, CPU1 F, CPU2 F, CPU3 F, CPU4 F, CPU5 F, CPU6 F, and CPU7 F) | The clock speed of each CPU core, which measures the number of cycles your CPU executes per second. The app runs on core 5, 6, and 7. <br>  |
| CPU Utilization (covers core0 to core7, including GPU0 U, GPU1 U, GPU2 U, GPU3 U, GPU4 U, GPU5 U, GPU6 U, and GPU7 U) | The utilization of each CPU core. The app runs on core 5, 6, and 7. <br>  |
| Current Now (CUR) | The real-time current. |
| Scene Average Current (SAC) | The average current of the scene. |
| GPU Frequency Proportion (GFP) | The proportion of the current scene's GPU frequency. |
| CPU User Average Load (CUAL) | The average CPU load of foreground apps. |
## Can I export raw metric data?
You can only monitor your app's performance metrics in real time, but cannot export raw metric data.


# --- END: Metrics HUD.md ---



# --- BEGIN: Monitor app performance.md ---

This page details how to use the performance monitoring and analysis tool (Unity Profiler) provided in the PICO Unity Integration SDK.
## Unity Profiler
### Overview
Unity Profiler displays the performance statistics about your application in areas such as CPU, memory, renderer, and audio. You can identify the areas for improvement in your application through these statistics.
While you are developing an application, you can have an overview of resource allocation using Unity Profiler. After you have developed an application, you can connect Unity Profiler with your PICO VR headset to test how the application runs on target release platforms. For more information, see [Profiler overview](https://docs.unity3d.com/2020.3/Documentation/Manual/Profiler.html) on Unity website.
You need to lock the level of target metrics before profiling so as to get consistent profiling statistics.

### Open the Profiler window
Follow the step below to open Unity Profiler:

1. Open your project in Unity Editor.
2. Open Unity Profiler through one of the following methods:
   * From the top menu bar, select **Window** > **Analysis** > **Profiler**.
   * Use the keyboard shortcut **Ctrl+7** ( **Command+7** on macOS).
   The **Profiler** window appears. For detailed information about the **Profiler** window, see [The Profiler window](https://docs.unity3d.com/2020.3/Documentation/Manual/ProfilerWindow.html) on Unity website.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/8ad760592fe04274abf2df9725a05505~tplv-em5hxbkur4-noop.image?width=1496&height=979)

## Metrics Tool
You can use the Metrics Tool to monitor the performance of your application. See [this article](/13136/en_metrics-tool) for details.


# --- END: Monitor app performance.md ---



# --- BEGIN: Monitor device performance.md ---

The PDC tool allows you to monitor your device's performance metrics on the PC. You can select the metrics you would like to monitor and add flag rules. **Flags** are used to notify you that some of your device's metrics are abnormal. After setting up flag rules for metrics, the PDC tool reports alarms when a metric's real-time value triggers its flag rule. The Flags pane displays the metric that triggers its flag rule, the number of alarms reported, and the condition that triggers the flag. 
## Before you begin
Refer to the "[PICO Developer Center overview](/13136/en_pdc-basic-info#f5a5a632)" article to complete general setups, including installing the PDC tool, enabling the "Developer" mode for your PICO device, and connecting your PICO device to the PC.
## Procedure
Complete setups and monitor performance metrics.
### Step 1: Enable metrics
You need to enable the metrics you would like to monitor on the **Performance Analyzer** pane.

1. On the left navigation pane, click **Performance Analyzer**.
   This directs you to the following pane:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc350034d2b74e4fb11e4235db7fef4a~tplv-goo7wpa0wc-image.image)
2. Click the **Settings** icon in the upper-right corner.
   The **Settings** window appears.
3. On the **Display Settings** pane, enable the metrics you want to monitor.
   Enabled metrics appear on the **Performance Analyzer** pane.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e07d632c6fc84380a5e88007d99979a4~tplv-goo7wpa0wc-image.image)

### Step 2: Add flag rules
On the **Flag Settings** pane, you can add flag rules for metrics.

1. In the area selected by the red frame, add flag rules:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37efa41ccb1d4859a29b06ef8f93d488~tplv-goo7wpa0wc-image.image)
   1. Select a metric.
   2. Select a direction. Available options are as follows:
      * **Above**: report alarms when a metric's value is above the threshold.
      * **AboveOrEqual**: report alarms when a metric's value is above or equal to the threshold.
      * **Below**: report alarms when a metric's value is below the threshold.
      * **BelowOrEqual**: report alarms when a metric's value is below or equal to the threshold.
      * **Equals**: report alarms when a metric's value equals the threshold.
   3. Set a threshold, which should be a positive integer.
   4. Click **Add**.
      The new flag rule is added and automatically enabled.
2. Perform the following operations as needed:
   * Toggle the switch to enable/disable flag rules.
   *  Click the trash bin icon to delete flag rules.

### Step 3: Start monitoring 
Turn on your PICO device and run an app on it, then click the **Start** button to start getting metric data for monitoring. The **Performance Analyzer** pane and the **Flags** pane show your device's performance data and flag, if any, in real time. While monitoring, you need to stay on the current pane, switching to the UI of another PDC feature will cause performance monitoring to stop.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/174eeb6daf244eafa22623dbf7f5db82~tplv-goo7wpa0wc-image.image)
Take the flag in the following red frame as an example:

* **FPS** is the metric that triggers the flag rule.
* **x30** indicates the number of alarms reported, which is 30.
* **Below 50** is the flag rule for "FPS", which lets the PDC tool report alarms when FPS is below 50.

![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b34582cf5fd14586bc278fe29345efd2~tplv-goo7wpa0wc-image.image)
If you would like to download logs, first click the **Pause** icon to stop further getting metrics data and then click the **Download** icon to download logs.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a748dee1f9a4ef79df1c73f85fe949a~tplv-goo7wpa0wc-image.image)
## Metric reference
The following table describes the metrics that you can monitor using the PDC tool.
| **Metric Name** | **Description** |
| --- | --- |
| GPU Utilization (GPU U)  | Overall GPU utilization rate (%).  |
| CPU Utilization (CPU U)  | Overall CPU utilization rate (%).  |
| FPS (FPS)  | Framerate (FPS)  <br> ***Note***: Normally speaking, an app's framerate is the same as the display's refresh rate.  |
| Available Memory (A MEM)  | Available memory (MB).  |
| Performance Score (Perf S)  <br>   | Indicates the device's overall performance:  <br>  <br> * <80: good performance  <br> * [80,100]: in certain situations, there may be FPS drops, such as during extended periods of operation, particular overloaded scenes, frequency limitations due to low battery, power outages, and so forth.  <br> * >100: frequent framerate drops  |
| Foveation Level (FRL)  | The app's foveated rendering level. The higher the level, the lower the GPU utilization rate and the blurrier the area around the foveal point. There are four values indicating different foveation levels:  <br>  <br> * -1: disabled  <br> * 0: low  <br> * 1: medium  <br> * 2: high  <br> * 3: top high  |
| Eye Buffer Width (EBW)   | The width of the rendered texture.  <br> Resolution directly affects the GPU rendering time. For the fragment shader, the higher the resolution you require (i.e., the more the pixels), the longer the rendering time.  |
| Eye Buffer Height (EBH)  <br>   | The height of the rendered texture.  <br> Resolution directly affects the GPU rendering time. For the fragment shader, the higher the resolution you require (i.e., the more the pixels), the longer the rendering time.  |
| Used Memory (U MEM)  | Used memory (MB).  |
| Singlepass  | Is Multiple rendering enabled:  <br>  <br> * 0: disabled  <br> * 1: enabled  |
| CPU Temperature  | The device's CPU temperature (°C).  |
| GPU Temperature  | The device's GPU temperature (°C).  |
| CPU Level (CPU L)  | The CPU level you set for the app. The higher the level, the higher the CPU utilization. The default level is 0, indicating that the system automatically adjusts the app's CPU level.  |
| GPU Level (GPU L)  | The GPU level you set for the app. The higher the level, the higher the GPU utilization. The default level is 0, indicating that the system automatically adjusts the app's GPU level.  |
| Display Refresh Rate (DRR)  | The device's display refresh rate, which can be 72/90/120 Hz.  |
| Battery Level (BAT)  | The device's battery level (%).  |
| Battery Temperature (B TEM)  | The device's battery temperature (°C).  |
| Power Voltage (POW V)  | The device's power voltage (mV).  |
| App VSS (VSS)  | The total amount of virtual memory that the app is using.  |
| App PSS (PSS)  | The actual amount of physical memory (RAM) that the app is using.  |
| App RSS (RSS)  | The amount of physical memory (RAM) occupied by the app.  |
| Battery Current ( BAT C)  | The current from the battery (mA).  |
| GPU Frequency ( GPU F)  | The GPU clock speed, which indicates how fast the cores of the GPU are.  |
| CPU Frequency (covers core0 to core7, including CPU0 F, CPU1 F, CPU2 F, CPU3 F, CPU4 F, CPU5 F, CPU6 F, and CPU7 F)  | The clock speed of each CPU core, which measures the number of cycles your CPU executes per second. The app runs on core 5, 6, and 7.  <br>   |
| CPU Utilization (covers core0 to core7, including GPU0 U, GPU1 U, GPU2 U, GPU3 U, GPU4 U, GPU5 U, GPU6 U, and GPU7 U)  | The utilization of each CPU core. The app runs on core 5, 6, and 7.  <br>   |
## Learn more
Metrics HUD is an HMD-end performance metrics monitoring tool. Once enabled, you can monitor your device's performance metrics on the HMD. For more information, check out [this article](/13136/en_metrics-hud).


# --- END: Monitor device performance.md ---



# --- BEGIN: PC-End Debugging Tool.md ---

The PC-End Debugging Tool (hereinafter simplified as "the tool") makes it much easier for you to debug PICO platform services. Instead of repeatedly building APK files and running them on the headset for debugging, you can use the tool to directly debug platform service in the Unity Editor on your PC. Currently, the PC-End Debugging Tool is available for the following services: Accounts & Friends, RTC, Interaction, Multiplayer, and In-app purchase (IAP).
## Operating system
Windows.
## Important note
If you are going to debug platform services for many times in a short period of time, make sure to click the **Play** button again after closing the debug screen for at least 5 seconds to ensure that the process created by the last debugging is completely exited.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c2f710b4a30b4636b9c0f2dc1e3145f3~tplv-em5hxbkur4-noop.image?width=1462&height=474" width="546px" />

## Before you begin
Before you can use the tool, you need to successively:

1. Import the PICO Unity Integration SDK
2. Get the access token
3. Set up PC Debugging

### Import the PICO Unity Integration SDK
First of all, you need to create a project on the Unity Hub, and then import the PICO Unity Integration SDK into the project. For detailed instructions, refer to the "[Import the SDK](/13136/en_import-the-sdk)" article.
### Get the access token
Then, you need to get your app's access token from the PICO Developer Platform. Below are the steps to follow:

1. Log in to the [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/).
2. Click the target app's card.
   This directs you to the app's overview screen.
3. On the left navigation panel, click **Platform  Service** > **API Test**.
   The **API** screen shows the **APP ID** field.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa77549084554b1092da81e7f3654989~tplv-goo7wpa0wc-image.image)
4. In **Authorization management**, select the permission(s) you need:
   * If you want to debug Accounts & Friends service and/or Interaction service, you need to select both **Your PICO friends relationship to find each other who use the same app with you** and **Your profile picture, alias**.
   * If you want to debug Multiplayer service and/or In-App Purchase service, you need to select **Your profile picture, alias**.
5. Click **Get Access Token**.
   A pop-up window displaying the access token appears.
6. Click **Copy**.

### Set up PC Debugging
Finally, you need to set up the PC Debugging mode for your app. You can select from Auto Setup or Manual Setup.
**Auto Setup**
Below are the steps to follow:

1. Return to the project configuration screen in the Unity Editor. If you close the project configuration screen after importing the SDK, you can reopen it via the Unity Hub.
2. From the top menu bar, select **PICO** > **PC Debug Settings**.
   The following pane is then displayed in the Inspector window:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/ca0712d12a334ff09d5e22e2892683ee~tplv-em5hxbkur4-noop.image?width=847&height=247)
3. Configure the following parameters:
   | **Parameter** | **Description** |
   | --- | --- |
   | Script | The configuration file. By default, the PcConfig script provided in the SDK is selected. |
   | Region | The location of your app: <br>  <br>    * **Cn**: Mainland China <br>    * **I18n**：Non-Mainland China |
   | Access Token | Your app's access token. Paste the access token you got from the PICO Developer Platform here. |
   The configurations are then automatically saved to the PicoSdkPCConfig.json file.

**Manual Setup**
Below are the steps to follow:

1. In the **Project** window, Go to the **Assets** > **Resources**.
2. Double-click the **PicoSdkPCConfig.json** file to open it.
3. Follow the content format below to set up PC Debugging in the file:
   ```JSON
   {
     "general": {
       "region": "cn"
     },
     "account": {
       "access_token": "act.e64df68e8cxxxxxxxxxxxxxxxd6d7860lg7o6V44LpCWEPJT7P1tq0AkU5yR"
     },
     "package": {
       "package_name": "com.bytedance.PlatformDemoOnline",
       "package_version_code": 2,
       "package_version_name": "2"
     }
   }
   ```

   You have completed all preparations. You can proceed to debug PICO platform services using the tool.
   You can edit PC debugging settings. Once edited, if you have used the PC Debugging Tool to debug platform services in the Unity Editor, you MUST exit the Unity Editor and Unity Hub, kill all Unity.exe-related processes in the Task Manager; otherwise, the new settings will NOT take effect.

## Debug platform services
This section walks you through the debugging process step by step. The services referenced here are Accounts & Friends service and Multiplayer service.
### Accounts & Friends
You can debug Accounts & Friends service using the UserDemo. Below are the steps to follow:

1. In the Project window, go to **Assets** > **Samples** > **UserDemo**.
2. Open the **UserDemo** folder and double-click the **UserDemo** file.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c95e374e59bb4803a2ead3efb405eceb~tplv-em5hxbkur4-noop.image?width=1210&height=357)
   The UserDemo pane is then displayed in the Game view as shown below:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/9c1efb6591d44dfc90fc10279cbcc99a~tplv-em5hxbkur4-noop.image?width=1701&height=908)
3. Click the **Play** icon at the top of the **Game** view.
   The UserDemo pane is then changed into the following:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/9af92c2f42be4fbb9b5ce1672c7880e8~tplv-em5hxbkur4-noop.image?width=1653&height=960)
4. Enter a command (For example, `a`) and click **Go**.
   The system will call `UserService.GetAccessToken` to get the current user's access token.

### Multiplayer
You can debug Multiplayer service using the GameAPITest Demo. Below are the steps to follow:

1. From the top menu bar, select **PXR_SDK** > **Platform Settings**.
2. In the **Inspector** window, check **User Entitlement Check**.
3. In **App ID**, enter your app's ID.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/be400b4bed55426eb94671f87f42b8d7~tplv-em5hxbkur4-noop.image?width=816&height=358)
4. Download [GameAPITest Demo](https://github.com/Pico-Developer/PlatformSample-Unity/tree/main/Assets/Samples/GameAPITest) from PICO GitHub.
5. In the **Project** window, place the **GameAPITest** folder under a desired directory (for example, under the Assets directory).
6. Open the **GameAPITest** folder and double-click the **GameAPITestScene** file.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/d65652ffe5834758af95303dddc25588~tplv-em5hxbkur4-noop.image?width=1202&height=363)
   The GameAPITest pane is then displayed in the Game view as follows:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/272cd91eeacd431bb2e08ce392342975~tplv-em5hxbkur4-noop.image?width=1280&height=743)
7. Click the **Play** icon at the top of the **Game** view.
8. Debug Multiplayer service using the pane. For how to use the pane, refer to the "[Room & Matchamking demo](/en_room-and-matchmaking-demo#b5e9919d)" article.

## API support
* Currently, all notification-related functions are unavailable.
* This part only lists the key APIs supported by the tool. For a supported API, the tool essentially supports all the API's corresponding field-setting and operation APIs. For more information about platform service APIs, read the [API reference](/reference/unity/latest/AchievementsService/).

The key APIs that the tool supports for each platform service are given in tables below.
### Accounts & Friends
| **API** | **Description** |
| --- | --- |
| `UserService.GetAccessToken` | Returns the value set in the PicoSdkPCConfig.toml file. |
| `UserService.GetLoggedInUser` | Available |
| `UserService.Get` | Available |
| `UserService.LaunchFriendRequestFlow` | Available |
| `UserService.GetFriends` | Available |
| `UserService.GetNextUserListPage` | Available |
| `UserService.GetFriendsAndRooms` | Available |
| `UserService.GetNextUserAndRoomListPage` | Available |
### RTC
| **API** | **Description** |
| --- | --- |
| `RTCService.JoinRoom` | Available |
| `RTCService.LeaveRoom` | Available |
| `RTCService.PublishRoom` | Available |
| `RTCService.UnPublishRoom` | Available |
| `RTCService.DestroyRoom` | Available |
| `RTCService.InitRtcEngine` | Available |
| `RTCService.StartAudioCapture` | Available |
| `RTCService.StopAudioCapture` | Available |
| `RTCService.SetAudioScenario` | Available |
| `RTCService.SetEarMonitorMode` | Available |
| `RTCService.SetEarMonitorVolume` | Available |
| `RTCService.SetCaptureVolume` | Available |
| `RTCService.SetPlaybackVolume` | Available |
| `RTCService.MuteLocalAudio` | Available |
| `RTCService.UpdateToken` | Available |
| `RTCService.GetToken` | Available |
| `RTCService.RoomPauseAllSubscribedStream` | Available |
| `RTCService.RoomResumeAllSubscribedStream` | Available |
| `RTCService.SetAudioPlaybackDevice` | Available |
| `RTCService.EnableAudioPropertiesReport` | Available |
| `RTCService.PublishRoom` | Available |
| `RTCService.RoomSetRemoteAudioPlaybackVolume` | Available |
| `RTCService.RoomSubscribeStream` | Available |
| `RTCService.UnPublishRoom` | Available |
| `RTCService.RoomUnSubscribeStream` | Available |
| `RTCService.SendRoomBinaryMessage` | Available |
| `RTCService.SendRoomMessage` | Available |
| `RTCService.SendStreamSyncInfo` | Available |
| `RTCService.SendUserBinaryMessage` | Available |
| `RTCService.SendUserMessage` | Available |
### Interaction
| **API** | **Description** |
| --- | --- |
| `ApplicationService.GetLaunchDetail` | Returns the value set in the PicoSdkPCConfig.toml file. |
| `ApplicationService.LogDeeplinkResult` | Available |
| `ApplicationService.LaunchApp` | Invalid |
| `PresenceService.GetInvitableUsers` | Available |
| `PresenceService.GetSentInvites` | Available |
| `PresenceService.GetNextApplicationInviteListPage` | Available |
| `PresenceService.SendInvites` | Available |
| `PresenceService.GetDestinations` | Available |
| `PresenceService.GetNextDestinationListPage` | Available |
| `PresenceService.Clear` | Available |
| `PresenceService.Set` | Available |
| `PresenceService.SetDestination` | Available |
| `PresenceService.SetIsJoinable` | Available |
| `PresenceService.SetLobbySession` | Available |
| `PresenceService.SetMatchSession` | Available |
| `PresenceService.SetExtra` | Available |
### Multiplayer
**Initialization**
| **API** | **Description** |
| --- | --- |
| `CoreService.GameInitialize(string accessToken)` | Available |
| `CoreService.GameInitialize()` | Available |
| `CoreService.GameUninitialize` | Available |
**Room & Matchmaking**
| **API** | **Description** |
| --- | --- |
| `RoomService.CreateAndJoinPrivate2` | Available |
| `RoomService.Get` | Available |
| `RoomService.GetCurrent` | Available |
| `RoomService.GetCurrentForUser` | Available |
| `RoomService.GetInvitableUsers2` | Available |
| `RoomService.GetModeratedRooms` | Available |
| `RoomService.InviteUser` | Available |
| `RoomService.Join2` | Available |
| `RoomService.KickUser` | Available |
| `RoomService.LaunchInvitableUserFlow` | Available |
| `RoomService.Leave` | Available |
| `RoomService.SetDescription` | Available |
| `RoomService.UpdateDataStore` | Available |
| `RoomService.UpdateMembershipLockStatus` | Available |
| `RoomService.UpdateOwner` | Available |
| `RoomService.UpdatePrivateRoomJoinPolicy` | Available |
| `MatchmakingService.Browse2` | Available |
| `MatchmakingService.Cancel2` | Available |
| `MatchmakingService.CreateAndEnqueueRoom2` | Available |
| `MatchmakingService.Enqueue2` | Available |
| `MatchmakingService.GetAdminSnapshot` | Available |
| `MatchmakingService.GetStats` | Available |
| `MatchmakingService.ReportResultInsecure` | Available |
| `MatchmakingService.StartMatch` | Available |
| `MatchmakingService.CrashTest` | Available |
**Leaderboards**
| **API** | **Description** |
| --- | --- |
| `LeaderboardService.Get` | Available |
| `LeaderboardService.GetEntries` | Available |
| `LeaderboardService.GetEntriesAfterRank` | Available |
| `LeaderboardService.GetEntriesByIds` | Available |
| `LeaderboardService.WriteEntry` | Available |
| `LeaderboardService.WriteEntryWithSupplementaryMetric` | Available |
**Achievements**
| **API** | **Description** |
| --- | --- |
| `AchievementsService.AddCount` | Available |
| `AchievementsService.AddFields` | Available |
| `AchievementsService.GetAllDefinitions` | Available |
| `AchievementsService.GetAllProgress` | Available |
| `AchievementsService.GetDefinitionsByName` | Available |
| `AchievementsService.GetProgressByName` | Available |
| `AchievementsService.Unlock` | Available |
**Challenges**
| **API** | **Description** |
| --- | --- |
| `ChallengeService.Invite` | Available |
| `ChallengeService.Get` | Available |
| `ChallengeService.GetEntries` | Available |
| `ChallengeService.GetEntriesAfterRank` | Available |
| `ChallengeService.GetEntriesByIds` | Available |
| `ChallengeService.GetList` | Available |
| `ChallengeService.Join` | Available |
| `ChallengeService.Leave` | Available |
### In-app purchase
IAP service testing relies on the payment pop-up, which is not yet available for the tool. Therefore, the following IAP APIs are mock APIs, and the date generated through them is not real.
| **API** | **Description** |
| --- | --- |
| `IAPService.ConsumePurchase` | Available |
| `IAPService.GetNextProductListPage` | Available |
| `IAPService.GetNextPurchaseListPage` | Available |
| `IAPService.GetProductsBySKU` | Available |
| `IAPService.GetViewerPurchases` | Available |
| `IAPService.LaunchCheckoutFlow` | Available |
## View debugging logs
The debugging logs are located at /{Project Folder}/Logs.


# --- END: PC-End Debugging Tool.md ---



# --- BEGIN: PICO Command Line Utility.md ---

PICO Command Line Utility is a command line tool that enables you to manage the files on the PICO Developer Platform more easily. It allows you to:

* upload APK files, the OBB file, Asset files (extra OBB files added on the PICO Developer Platform) 
* manage DLC files for an add-on
* download APK files.
* clone a build to other release channels.

## Release notes
| **Date** | **Version** | **What's new** |
| --- | --- | --- |
| June 21, 2023 | 1.0.3 | Increased the number of asset files allowed to be uploaded when uploading a build to 1000. |
| February 16, 2023 | 1.0.2 | Supported adding multiple DLC files to an add-on. |
| January 12, 2023 | 1.0.1 | Released the PICO Command Line Utility. |
## Key features
You can manage the CLI tool and files on the PICO Developer Platform. 
### Manage the CLI tool
Type a specific command in CLI to manage the tool and get help.
| **Feature** | **Description** | **Command field** | **Syntax** |
| --- | --- | --- | --- |
| Update CLI tool <br>  | Update the tool to the latest version and it cannot be rolled back currently. | `self-update` <br>  | ```Bash <br> pico-cli self-update <br> ``` <br>  |
| View CLI tool info | View the tool's version code. | `version` | ```Bash <br> pico-cli version <br> ``` <br>  |
| Get help | Show the description of a specific command, such as its syntax, feature, parameters, etc. | `help` | ```Bash <br> pico-cli help <br> ``` <br>  |
### Manage builds
Type a specific command in CLI to manage builds and release channels on the PICO Developer Platform.
| **Feature** | **Description** | **Command field** | **Syntax** |
| --- | --- | --- | --- |
| Get build info | According to the parameters passed in, you can get the corresponding build information, including: <br>  <br> * information about all builds of a specific app <br> * Information about the build specified by Build ID <br> * Information about the build on the corresponding release channel(s) | `query-build-parameter` <br>  | ```Bash <br> pico-cli query-build-parameter --app-id <AppID> --app-secret <AppSecret> --region <cn\|noncn> --info <device-type\|release-channel\|build-id\|all> <br> ``` <br>  <br>  |
| Upload a build <br>  | Upload a build to the PICO Developer Platform. | `upload-build` <br>  | ```Bash <br> pico-cli upload-build --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --device <'Device1,Device2...'> --apk <FilePath> --obb <FilePath> --assets-dir <FilePath> --channel <ReleaseChannel> --note-cn <ReleasesNotes> --note-en <ReleasesNotes> <br> ``` <br>  |
| Download a build | Download a specific build on the PICO Developer Platform. | `download-build` | ```Bash <br> pico-cli download-build --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --build-id <BuildID> --output-dir <Directory> <br> ``` <br>  |
| Change the release channel | Set or change the release channel of a build. | `clone-release-channel-build` | ```Bash <br> pico-cli clone-release-channel-build --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --build-id <BuildID> --destination-channel <Channel> <br> ``` <br>  |
### Manage DLC files
| **Feature** | **Description** | **Command field** | **Syntax** |
| --- | --- | --- | --- |
| Query an add-on's DLC file info | Query the information about the DLC files that you have added to a specified add-on. | `query-add-on` | ```Bash <br> pico-cli query-add-on --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --sku <SKU>  <br> ``` <br>  |
| Add a DLC file to an add-on <br>  | Add a DLC file to a specified add-on. You can add no more than 10 DLC files to an add-on. | `upload-add-on` <br>  | ```Bash <br> pico-cli upload-add-on --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --cmd-type add --sku <SKU> --file <FilePath>  <br> ``` <br>  |
| Update a DLC file  <br>  | Update a specified DLC for an add-on. In other words, replace an existing DLC file with a new one. | `upload-add-on` | ```Bash <br> pico-cli upload-add-on --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --cmd-type update --sku <SKU> --file-id <FileID> --file <FilePath>  <br> ``` <br>  |
| Set the minimum compatible build version for a DLC file <br>  | Set the minimum compatible build version for a DLC file. Based on the app's availability in different regions, you need to set a DLC file's minimum compatible build version for the specific region where the corresponding build is published. | `upload-add-on` <br>  | ```Bash <br> pico-cli upload-add-on --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --cmd-type set-min-version --sku <SKU> --mainland-min-version <VersionCode> --nonmainland-min-version <VersionCode> <br> ``` <br>  |
| Delete a DLC file <br>  | Delete a DLC file from an add-on. <br>  | `upload-add-on` <br>  | ```Bash <br> pico-cli upload-add-on --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --cmd-type delete --sku <SKU> --file-id <FileID> <br> ``` <br>  |
## Prerequisite
Before using the CLI tool, make sure you have [created an app](/en_create-an-app) on the PICO Developer Platform.
## Quickstart
### Step 1: Download and launch the CLI tool
**Method one**
Click one of the links in the following table to download the version that suits your operating system and region, then launch the CLI tool downloaded.
| **Operating system** | **Version** | **Download** |
| --- | --- | --- |
| Windows 32-bit and 64-bit | Mainland China version | * [Mainland China download](https://p3-platform-cn-static.picovr.com/tos-cn-i-1l663x1b0h/windows-cn/202304111056/pico-cli.exe?r=1681181814847245000) <br> * [Outside Mainland China download](https://p16-platform-static-va.ibyteimg.com/tos-maliva-i-jo6vmmv194-us/windows-cn/202304111056/pico-cli.exe?r=1681181814847245000) |
|  | Outside Mainland China version | * [Mainland China download](https://p3-platform-cn-static.picovr.com/tos-cn-i-1l663x1b0h/windows-noncn/202304111056/pico-cli.exe?r=1681181814847245000) <br> * [Outside Mainland China download](https://p16-platform-static-va.ibyteimg.com/tos-maliva-i-jo6vmmv194-us/windows-noncn/202304111056/pico-cli.exe?r=1681181814847245000) |
| macOS X | Mainland China version | * [Mainland China download](https://p3-platform-cn-static.picovr.com/tos-cn-i-1l663x1b0h/darwin-cn/202304111056/pico-cli?r=1681181814847245000) <br> * [Outside Mainland China download](https://p16-platform-static-va.ibyteimg.com/tos-maliva-i-jo6vmmv194-us/darwin-cn/202304111056/pico-cli?r=1681181814847245000) |
|  | Outside Mainland China version  | * [Mainland China download](https://p3-platform-cn-static.picovr.com/tos-cn-i-1l663x1b0h/darwin-noncn/202304111056/pico-cli?r=1681181814847245000) <br> * [Outside Mainland China download](https://p16-platform-static-va.ibyteimg.com/tos-maliva-i-jo6vmmv194-us/darwin-noncn/202304111056/pico-cli?r=1681181814847245000) |
| Linux | Mainland China version | * [Mainland China download](https://p3-platform-cn-static.picovr.com/tos-cn-i-1l663x1b0h/linux-cn/202304111056/pico-cli?r=1681181814847245000) <br> * [Outside Mainland China download](https://p16-platform-static-va.ibyteimg.com/tos-maliva-i-jo6vmmv194-us/linux-cn/202304111056/pico-cli?r=1681181814847245000) |
|  | Outside Mainland China version | * [Mainland China download](https://p3-platform-cn-static.picovr.com/tos-cn-i-1l663x1b0h/linux-noncn/202304111056/pico-cli?r=1681181814847245000) <br> * [Outside Mainland China download](https://p16-platform-static-va.ibyteimg.com/tos-maliva-i-jo6vmmv194-us/linux-noncn/202304111056/pico-cli?r=1681181814847245000) |
**Method two**
Download and launch the CLI tool using the PICO Developer Center:

1. Launch the [PICO Developer Center](/en_pdc-basic-info).
2. From the left navigation pane, select **Download**.
3. On the **Tools** list, click the **Download** button in the **PICO CLI** area.
   PICO Developer Center starts to download the PICO CLI tool.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9148c687e6574eb797bd6c0022f224c1~tplv-goo7wpa0wc-image.image)
4. After the download is complete, go to the **Installed** list and click the **Start** button to launch the PICO CLI tool.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14f1550d6515442ca33260b6e9e7a796~tplv-goo7wpa0wc-image.image)

### Step 2: (macOS) Change CLI tool's access permission 
If you are using the macOS operating system, you need to change the access permission for the CLI tool.

1. In the Terminal, type `cd/{CLI directory}`.
2. Type `chmod +x . /pico-cli`.

  If you see the warning `pico-cli" cannot be opened because the developer cannot be verified`, you can:

   1. click the Apple icon in the upper left corner of your desktop and select **System Preferences** > **Security & Privacy** > **General**.
   2. in the **General** pane, click the **Allow Anyway** button and enter your Mac password.
3. Type `./pico-cli` **** and **** a command (e.g. `pico-cli help`) to run the CLI tool.

### Step 3: Obtain credentials to use CLI tool
When using the CLI tool, you will need:

* App ID and App Secret: For verifying access to the app
* Build ID: For downloading a specific build

#### Get App ID and App Secret
Refer to [View App ID and App Secret](https://developer-cn.pico-interactive.com/docs/unreal/en/13156/create-an-app/#view-app-id-and-app-secret).
#### Get Build ID

1. Log in to [PICO Developer Platform](https://developer-global.pico-interactive.com/console#/).
2. Choose your organization.
3. Enter the **My Apps** page and click the target app card to enter the app's **Overview** page.
4. On the left navigation pane, click **Release Channel** and enter the channel detail page.
5. Find the target channel and click **Edit** in the **Actions** column.
   This directs you to the channel version list screen.
6. Find the target version and click **View** in the **Actions** column.
   This directs you to the **Store Builds** screen where you can view the **Build ID** under the **Build Info** tab.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fb998dabe78475aa6eae59d52f61b06~tplv-goo7wpa0wc-image.image)
   On the **Store Builds** page, you can view **Build ID** under the **Build Info** tab.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/176be40088b14ec889491837ddfefbb8~tplv-goo7wpa0wc-image.image)

### Step 4: Use commands to complete tasks
Use commands to manage the CLI tool, builds, and DLC files. Refer to the "[Commend details](#a467a1ed)" section for more information.
## Command details
Below are descriptions of commands and parameters.
### Update the CLI tool
Update the CLI tool to the latest version.
**Input**
```Bash
pico-cli self-update
```

### Get the tool version
Get the version of the CLI tool.
**Input**
```Bash
pico-cli version
```

### Get help
Get help info, including commands and descriptions, options and descriptions, examples, and release channels with corresponding parameters.
**Input**
```Bash
pico-cli help
```

### Get build info
Get build info according to parameters passed in.
**Input**
```Bash
pico-cli query-build--parameter --app-id <AppID> --app-secret <AppSecret> --region <cn|noncn> --info <device-type|release-channel|build-id|all>
```

**Parameter description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--app-id <ID>` or `-a <ID>` <br>  | Yes | App ID, which is the unique identifier that specifies an app. |
| `--app-secret <AppSecret>` or `-s <AppSecret>` | Yes | App secret, which verifies your app permissions.  |
| `--region <cn｜noncn>`or `-r <cn｜noncn>` | Yes | Specifies the region where the user is located. |
| ` --info <device-type\|release-channel\|build-id\|all>` <br>  | Yes <br>  | Specifies the build info to be obtained with the following parameters (choose from four options): <br>  <br> * `device-type`: Gets the device model (e.g. PICO 4, PICO Neo3). <br> * `release-channel`: Fills in the parameter to get the build information of the corresponding release channel. The parameters and corresponding channels are as follows. <br>    * `1`: PICO Store (Mainland China) <br>    * `2`: PICO Store (Outside Mainland China) <br>    * `3`: Beta <br>    * `4`: Alpha <br>    * `5`: Release Candidate <br>    * `6`: PICO Enterprise Store(Mainland China) <br>    * `7`: PICO Enterprise Store(Outside Mainland China) <br> * `build-id`: Fills in Build ID to get the information about the corresponding build. <br> * `all`: Returns the above three types of info. |
### Upload a build
Upload a build or upload OBB and asset files to a specific build on the PICO Developer Platform.
**Input**
```Bash
pico-cli upload-build --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --device <'Device1,Device2...'> --apk <FilePath> --obb <FilePath> --assets-dir <DirPath> --channel <ReleaseChannel> --note-cn <ReleasesNotes> --note-en <ReleasesNotes>
```

**Parameter description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--app-id <ID>` or `-a <ID>` <br>  | Yes | App ID, which is the unique identifier that specifies an app. |
| `--app-secret <AppSecret>` or `-s <AppSecret>` | Yes | App secret, which verifies your app permissions.  |
| `--region <cn｜noncn>` or `-r <cn｜noncn>` | Yes | Specifies the region where the user is located. |
| `--device<'Device1,Device2...'>` | Yes | Specifies the supported device models for the build, e.g. `--device 'PICO Neo3,PICO 4'`. |
| `--apk <FilePath>` | Yes | Specifies the local path to the build. |
| `--assets-dir <DirPath>` | No | Specifies the local path to the DLC file corresponding to the build. |
| `--obb <FilePath>` | No | Specifies the local path to the OBB file. |
| `--channel <ReleaseChannel>` or `-c <ReleaseChannel>` | Yes | Specifies the release channel for the build: <br>  <br> * `1`：PICO Store (Mainland China) <br> * `2`：PICO Store (Outside Mainland China) <br> * `3`：Beta <br> * `4`：Alpha <br> * `5`：Release Candidate |
| `--notes-en <Text>` | No | Uploads the English release notes. |
| `--notes-cn <Text>` | No | Uploads the Chinese release notes. |
**Option description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--help` | No | Displays the instructions on using this command. |
### Download a build
Download a build on the PICO Developer Platform.
**Input**
```Bash
pico-cli download-build --app-id <AppID> --app-secret <AppSecret> --build-id <BuildID> --output-dir <Directory> --region <cn｜noncn>
```

**Parameter description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--app-id <ID>` or `-a <ID>` | Yes | App ID, which is the unique identifier that specifies an app. |
| `--app-secret <AppSecret>` or `-s <AppSecret>` | Yes | App secret, which verifies your app permissions.  |
| `--region <cn｜noncn>`or `-r <cn｜noncn>` | Yes | Specifies the region where the user is located. |
| `--build-id <BuildID>` or `-b <BuildID>` | Yes | Specifies the ID of the to-be-downloaded build. |
| `--output-dir <DirPath>` or `-d <DirPath>` | Yes <br>  | Specify the local path to save the build. <br>  |
### Clone a build to other release channels
clone a specific build to other release channels.
**Input**
```Bash
pico-cli clone-release-channel-build --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --build-id <BuildID> --destination-channel <Channel>
```

**Parameter description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--app-id <ID>` or `-a <ID>` | Yes | App ID, which is the unique identifier that specifies an app. |
| `--app-secret <AppSecret>` or `-s <AppSecret>` | Yes | App secret, which verifies your app permissions.  |
| `--region <cn｜noncn>`or `-r <cn｜noncn>` | Yes | Specifies the region where the user is located. |
| `--build-id <BuildID>` or `-b <BuildID>` | Yes | Specifies the ID of the to-be-downloaded build. |
| `--destination-channel <ReleaseChannel>` | Yes | Specifies the target release channel: <br>  <br> * `1`：PICO Store (Mainland China) <br> * `2`：PICO Store (Outside Mainland China) <br> * `3`：Beta <br> * `4`：Alpha <br> * `5`：Release Candidate |
**Option description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--help` | No | Displays the instructions on using this command. |
### Query an add-on's DLC file info
Query the DLC file info for an add-on. This command is only supported by the "draft" add-on that you have added DLC file(s) to.
**Input**
```Bash
pico-cli query-add-on --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --sku <SKU> 
```

**Parameter description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--app-id <ID>` or `-a <ID>` | Yes | App ID, which is the unique identifier that specifies an app. |
| `--app-secret <AppSecret>` or `-s <AppSecret>` | Yes | App secret, which verifies your app permissions.  <br>  |
| `--region <cn｜noncn>` or `-r <cn｜noncn>` | Yes | The region where the user is located. |
| `--sku <SKU>` or `-p <SKU>` <br>  | Yes | The SKU of the add-on. <br> ***Note***: SKU is an add-on's unique identifier, which is configured on the PICO Developer Platform when creating an add-on. |
### Add a DLC file
Add a DLC file to an add-on. You can add no more then 10 DLC files to an add-on.
**Input**
```Bash
pico-cli upload-add-on --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --cmd-type add --sku <SKU> --file <FilePath>
```

**Parameter description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--app-id <ID>` or `-a <ID>` | Yes | App ID, which is the unique identifier that specifies an app. |
| `--app-secret <AppSecret>` or `-s <AppSecret>` | Yes | App secret, which verifies your app permissions.  |
| `--region <cn｜noncn>` or `-r <cn｜noncn>` | Yes | The region where the user is located. |
| `--cmd-type <add \| update \| delete \| set-min-version>` <br>  | Yes | The operation on the DLC file: <br>  <br> * `add`: add a DLC file to an add-on <br> * `update`: Update a DLC file for an add-on <br> * `set-min-version`: set a DLC file's minimum compatible build version <br> * `delete`: delete a DLC file from an add-on |
| `--sku <SKU>` or `-p <SKU>` <br>  | Yes | The SKU of the add-on. <br> ***Note***: SKU is an add-on's unique identifier, which is configured on the PICO Developer Platform when creating an add-on. |
| `--file <file-path>` or `-f <file-path>` | Yes | The local path to the DLC file. |
### Update a DLC file 
Update a DLC file for an add-on. In other words, replace an existing DLC file with a new one.
**Input**
```Bash
pico-cli upload-add-on --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --cmd-type update --sku <SKU> --file-id <FileID> --file <FilePath> 
```

**Parameter description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--app-id <ID>` or `-a <ID>` | Yes | App ID, which is the unique identifier that specifies an app. |
| `--app-secret <AppSecret>` or `-s <AppSecret>` | Yes | App secret, which verifies your app permissions.  |
| `--region <cn｜noncn>` or `-r <cn｜noncn>` | Yes | Specifies the region where the user is located. |
| `--cmd-type <add \| update \| delete \| set-min-version>` | Yes | The operation on the DLC file: <br>  <br> * `add`: add a DLC file to an add-on <br> * `update`: Update a DLC file for an add-on <br> * `set-min-version`: set a DLC file's minimum compatible build version <br> * `delete`: delete a DLC file from an add-on |
| `--sku <SKU>` or `-p <SKU>` <br>  | Yes | The SKU of the add-on. <br> ***Note***: SKU is an add-on's unique identifier, which is configured on the PICO Developer Platform when creating an add-on. |
| `--file-id <FileID>` | Yes | The ID of the to-be-replaced DLC file, which can be retrieved through `query-add-on`. |
| `--file <file-path>` or `-f <file-path>` | Yes | The local path to the new DLC file. <br>  |
### Set a DLC file's minimum compatible build version
Set the minimum compatible build version for a DLC file. Based on the app's availability in different regions, you need to set a DLC file's minimum compatible build version for the specific region where the corresponding build is published.
**Input**
```Bash
pico-cli upload-add-on --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --cmd-type set-min-version --sku <SKU> --mainland-min-version <VersionCode> --nonmainland-min-version <VersionCode>
```

**Parameter description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--app-id <ID>` or `-a <ID>` | Yes | App ID, which is the unique identifier that specifies an app. |
| `--app-secret <AppSecret>` or `-s <AppSecret>` | Yes | App secret, which verifies your app permissions.  |
| `--region <cn｜noncn>` or `-r <cn｜noncn>` | Yes | Specifies the region where the user is located. |
| `--cmd-type <add \| update \| delete \| set-min-version>` | Yes | The operation on the DLC file: <br>  <br> * `add`: add a DLC file to an add-on <br> * `update`: Update a DLC file for an add-on <br> * `set-min-version`: set a DLC file's minimum compatible build version <br> * `delete`: delete a DLC file from an add-on |
| `--sku <SKU>` or `-p <SKU>` <br>  | Yes | The SKU of the add-on. <br> ***Note***: SKU is an add-on's unique identifier, which is configured on the PICO Developer Platform when creating an add-on. |
| `--mainland-min-version <version-code>` | Yes | The DLC file's minimum compatible version for Mainland China build. |
| `--nonmainland-min-version <version-code>` | Yes | The DLC file's minimum compatible version for non-Mainland China build. |
### Delete a DLC file
Delete a DLC file from an add-on.
**Input**
```Bash
pico-cli upload-add-on --app-id <AppID> --app-secret <AppSecret> --region <cn｜noncn> --cmd-type delete --sku <SKU> --file-id <FileID>
```

**Parameter description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--app-id <ID>` or `-a <ID>` | Yes | App ID, which is the unique identifier that specifies an app. |
| `--app-secret <AppSecret>` or `-s <AppSecret>` | Yes | App secret, which verifies your app permissions.  |
| `--region <cn｜noncn>` or `-r <cn｜noncn>` | Yes | Specifies the region where the user is located. |
| `--cmd-type <add \| update \| delete \| set-min-version>` | Yes | The operation on the DLC file: <br>  <br> * `add`: add a DLC file to an add-on <br> * `update`: Update a DLC file for an add-on <br> * `set-min-version`: set a DLC file's minimum compatible build version <br> * `delete`: delete a DLC file from an add-on |
| `--sku <SKU>` or `-p <SKU>` <br>  | Yes <br>  | The SKU of the add-on. <br> ***Note***: SKU is an add-on's unique identifier, which is configured on the PICO Developer Platform when creating an add-on. |
| `--file-id <FileID>` | Yes | The ID of the DLC file, which cen be retrieved through `query-add-on`. |
**Option description**
| **Syntax** | **Required** | **Description** |
| --- | --- | --- |
| `--help` | No | Displays the instructions on using this command. |
## Learn more
For more information on add-on and DLC, refer to [In-app purchase](/13136/en_in-app-purchase) and [DLC](/13136/en_downloadable-content).


# --- END: PICO Command Line Utility.md ---



# --- BEGIN: PICO Debugger.md ---

PICO Debugger is a debugging tool that allows you not only to view logs and scene information, but also to use its built-in tools to optimize your application in a more targeted way.
## Configuration and building
Go to **Edit** > **Project Settings**, then configure the tool's parameters in the **PICO Debugger** panel.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06ce5f6d9d2f4a7aae9392a0fe01f87c~tplv-goo7wpa0wc-image.image" width="600px" />

| **Module** | **Parameters** | **Description** |
| --- | --- | --- |
| Default Panel <br>  | Enable/Disable | Whether to enable the PICO Debugger tool. Enabled by default. |
|  | Launcher Button | Configure how to open PICO Debugger and assign the corresponding buttons on the controller. The available options are: PressA, PressX, and PressY. <br> Press the configured button to display the tool’s main interface; press it again to hide it. |
|  | Movement > Initial Position | The initial display position of PICO Debugger is determined by the distance between it and the camera. Available options are: Far, Near, and Medium. <br> After configuration, each time the PICO Debugger is activated, the distance between its interface and the user remains fixed. |
| Console Panel | Maximum Count | Maximum number of log entries that can be displayed in the log interface. |
| Tool Panel | Ruler Tools > Launcher Button | Configure how to close the measuring ruler using the relevant button on the controller. The available options are: PressA, PressX, and PressY. |
As a debugging tool, PICO Debugger is only supported in development builds. When building the project, you must select the **Development Build** option.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d7732539ae1424e970c527a406b81fe~tplv-goo7wpa0wc-image.image" width="500px" />

## Main interface
The main interface consists of three primary buttons: the **Logger** button, the **Inspector** button, and the **Tools** button. Pressing any of these buttons will display the corresponding sub-interface. Additionally, dragging the blue fist icon button allows you to move the entire PICO Debugger interface.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfd41834eae64d59ac398b55c517ae41~tplv-goo7wpa0wc-image.image" width="500px" />

## Logger interface
The logging system collects various logs generated during operation to assist in troubleshooting. The main interface of the log system is as follows:

* The three icons in the upper left corner correspond to the Info, Warning, and Error log types. After clicking the icon, only logs of the corresponding type will be displayed.
* The log list displays the timestamp, content (logString), and details (stackTrace) for each log entry.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ae18a955b2a41208ce37d9102d7dc16~tplv-goo7wpa0wc-image.image" width="500px" />

## Inspector interface
The Inspector interface is divided into left and right sections:

* On the left is the structure tree for the current scene, which can be expanded level by level by clicking the **+** icon. After clicking a node, the right side displays the transform data of the object corresponding to that node.
* On the right is the transform data for the corresponding object, which includes position, rotation, and scale information. The transform data of the observed object is updated in real time. To avoid excessive performance overhead, the Inspector interface does not update scene data in real time. You can click the refresh button in the upper left corner to force update the data, including after new objects are added to the scene. However, when the current observed object is deleted, the data will be refreshed automatically, and this refresh is mandatory.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c1d6981def84a16b9e87344ec77470f~tplv-goo7wpa0wc-image.image" width="500px" />

## Tools interface
The Tools interface displays all current tools. Hover the pointer over a tool icon, then press the Trigger button to select the current tool. Note that:

* When a tool is selected, the controller model is hidden and the model of the current tool is displayed.
* Tools are mutually exclusive. When you switch to a different tool, the model for the right hand will also switch.

When you need to continue using the controller, just click the recycle icon in the upper left corner.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4765d2614b7b49cea4844671130d6084~tplv-goo7wpa0wc-image.image" width="300px" />

Available tools are as follows:
| **Tool name** | **Description** |
| --- | --- |
| Measuring ruler | A measuring ruler is used to measure the dimensions of virtual and real objects within a scene. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3291aef8ae344d3aa0393611d96834b3~tplv-goo7wpa0wc-image.image) <br> Press and hold the Grip button on the right controller, move the measuring ruler along the object to be measured, then release the Grip button. The interface will display a ruler with scale marks, with the measured length displayed at the center of the ruler. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41ed4b0682eb402d80b61ce0084ea845~tplv-goo7wpa0wc-image.image) |
| Time controller | The time controller is used to pause and start time. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/023cf2b776a84ddc8026e42a47b9961f~tplv-goo7wpa0wc-image.image) <br> When you press the Grip button on the right controller again and again, the button will continuously toggle between the on and off states. After enabling this feature, the time in the scene is paused. |
##


# --- END: PICO Debugger.md ---



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



# --- BEGIN: PICO Emulator (Beta).md ---

You can install your app on PICO Emulator and run it, so as to preview how your app performs.
## Release notes
| **Version** | **What's new** |
| --- | --- |
| 0.8.1 beta | Hardware acceleration setup is automatically done in the backend. |
| 0.8.0 beta | PICO Emulater (Beta) is released. |
## Download PICO Emulator
Download PICO Emulator from one of the following methods:

* Download from [PICO Developer website](https://developer.picoxr.com/resources/#emulator).
* Download from the "Download Center" of the [PICO Developer Center](https://developer.picoxr.com/resources/#pdc).

## Hardware requirements
Make sure your hardware meets the minimum requirements given below.
| **Operating System** | **Minimum Requirements** |
| --- | --- |
| Windows | 64-bit Windows 10 or higher. <br>  <br> * RAM: 16GB <br> * Available disk space: 32GB <br> * CPU: Intel Core i5 <br> * GPU: NVIDIA GeForce GTX 1060  |
| macOS | macOS v14.0 or higher. <br>  <br> * RAM: 16GB <br> * Available disk space: 32GB <br> * CPU: M1 Pro |
## Instructions on using PICO Emulator
### Open PICO Emulator

* **Windows**: Go to the storage path of PICO Emulator and click the following icon in the "picoemulator" folder to open it.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b07b409264843fc9f63c3e65369f8a4~tplv-goo7wpa0wc-image.image" width="150px" />   

* **macOS**: Open the command line tool, enter the storage path of PICO Emulator, and execute command `start-emulator.sh` to open it.

Wait for a moment, and you will see the following screen in the emulator.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7bc67e5a0464ae59b5059aa03272c5d~tplv-goo7wpa0wc-image.image" width="600px" />

The following will introduce common operations, the functionalities of different buttons, and what you can do with different user interfaces.
### Common operations
| **Operation** | **Expected Effect** |
| --- | --- |
| Press the W/S/A/D keys | Move the view forward/backward/leftward/rightward. |
| Left-click with the mouse | To confirm. |
| Scroll the mouse wheel | Move the view forward/backward. |
| Right-click and drag the mouse | Rotate the view. |
### Buttons
| **Button Name** | **Functionality** |
| --- | --- |
| Home <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ced4be51e2144b9384479710116be5cd~tplv-goo7wpa0wc-image.image) | This button works the same as the Home button on the device. It is usually used to exit full-screen 3D apps. |
| Enable Controller Mode <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80ce80ba647140fba95bcc8112ac9193~tplv-goo7wpa0wc-image.image) | Click this button to enable the Controller mode.  <br> Once enabled, keyboard keys will be mapped to corresponding controller buttons based on the mapping settings in **Setting** > **Controller Setting**. |
| Enable Keyboard Mode <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7a8d317edb7433c9a24c2e5d9237bd9~tplv-goo7wpa0wc-image.image) | Click this button to enable the Keyboard mode.  <br> Once enabled, keyboard keys will be directly injected into PICO Emulator. This mode is typically used for text input. |
| Take Screenshot <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5d3d70dac5043ad86500aa5da5c4d87~tplv-goo7wpa0wc-image.image) | Click this button to capture the current screen. |
| Record Screen <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccb522fb28a64f7dbc6982a45871c7a1~tplv-goo7wpa0wc-image.image) | Click the button to record the current screen and click it again to pop up the window for playing back and saving the recording. |
| Setting <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/038673965a8249ec8cc5b62789acb9e3~tplv-goo7wpa0wc-image.image) | Click this button to open the Setting center. |
| Operation Mode <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67478a1b034e49dc97b5791e019e5c9c~tplv-goo7wpa0wc-image.image) | From left to right: Controller Mode, Pan Mode, Dolly Mode, Look Around Mode, and Orbit Mode. <br> The default Controller Mode (right controller) is the mostly used. You can click the Controller Mode button again to switch to using the right controller. |
| Reset Camera <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd2e3e851f8c4b8b8ecae2bb1b7e9aff~tplv-goo7wpa0wc-image.image) | Click this button to reset the camera. <br>  |
### User interfaces
| **User Interface** | **Functionality** |
| --- | --- |
| Battery | You can simulate power and charging status settings. |
| Record Playback | You can record screens, play back recordings, or save recordings. |
| Shortcut Key | You can check out keyboard shortcuts. |
| Controller Setting | You can customize the mapping between keyboard keys and controller buttons as well as adjust the angle of the ray. |
| Bug Report | You can report bugs or any problems to PICO. |
| About Simulator | You can view information such as the current version of PICO Emulator and system. |
| Debugging | You can change system language and theme for PICO Emulator. |
### Install apps
PICO Emulator supports installing and running most of the apps that you can run on the PICO device. You and use one of the following methods to install an app's APK file on PICO Emulator.

* *Method 1*: Directly drag the app's package into PICO Emulator and the emulator will automatically start installing the app.
* *Method 2*: Use command `adb install`. Receiving `Success` indicates that the app has been installed.

### Install OBB files
If there are OBB files within the project, you can follow the steps below to push these files to PICO Emulator.

1. Rename the OBB file in the format **main.version_number.package_name.obb** (for example: main.100.com.PicoGame.GameName.obb).
   The version number (i.e., versionCode) and package name in the file name must match the corresponding details in the installed APK file.

2. Use command `adb push` to push the renamed OBB file to the /storage/emulated/0/Android/obb/{package_name} directory.
   If there is not the {package_name} directory, use command `adb shell` to create one.

3. Launch your app in PICO Emulator.
   If the app fails to launch (for example, if  PICO Emulator's screen remains in a loading state in black), you can go to the /storage/emulated/0/Android/obb directory and check whether all OBB files are correct.

### Install bundle files
If there are bundle files within the project, you can follow the steps below to push these files to PICO Emulator.

1. Download bundle files.
2. Use command `adb push` to push all bundle files to the /storage/emulated/0/Android/obb/{package_name} directory.
3. Launch your app in PICO Emulator.
   If the app fails to launch (for example, if  PICO Emulator's screen remains in a loading state in black), you can go to the /storage/emulated/0/Android/obb directory and check whether all bundle files are correct.

## Troubleshooting
### macOS-related issues
When running the PICO Emulator on macOS and encountering issues such as "XX is damaged and cannot be opened. You should move it to the trash", navigate to the directory where the PICO Emulator is located, and then execute the following command in the terminal:
```Bash
sudo xattr -r -d com.apple.quarantine ./pico_emulator
```


# --- END: PICO Emulator (Beta).md ---



# --- BEGIN: PICO Graphics Probe Tool.md ---

You can use the PICO Graphics Probe Tool to analyze and debug your app's performance.
## Use cases

* **System GPU data capture and analysis**
   Capture GPU real-time data while the system is running. The data includes metrics such as GPU utilization, texture cache hit rate, texture filtering methods, and video memory (VRAM) read/write speeds.
* **App rendering stage data trace and analysis**
   Launch an app to capture data during its rendering stages. The data includes per-frame rendering time, the number of surfaces rendered, the count of bins in TBR (Tile-Based Rendering), the rendering mode used, and more.
* **Draw Call-related data trace and analysis**
   Start an app to capture its real-time data of individual draw call commands. The data includes the number of ALU (Arithmetic Logic Unit) instructions, the number of culled faces with hardware, the quantity of vertices processed by the vertex shader, the number of fragments processed by the pixel shader, and more.

## Requirements

* PICO device: PICO Neo3 and PICO 4 Series
* PICO device system version: 5.8.0 and later

## Prerequisites

* Make sure the [Andorid Debug Bridge](https://developer.android.com/tools/adb) (ADB) tool is downloaded on your computer.
* Ensure that you've connected your PICO device to the computer using a USB cable. You can use the command `adb devices` to view the connected PICO device's ID.

## Command-line parameter description
The PICO Graphics Probe Tool supports the following command-line parameters, which can be used to gather GPU performance data, trace rendering stage information, capture draw call data, and more.
| **Parameter** | **Complete command** | **Description** |
| --- | --- | --- |
| `-r` or `--realtime` | `adb shell gprobe -r` or` adb shell gprobe --realtime` | Obtain real-time data from the GPU. Data output can be terminated using keyboard shortcuts supported by the terminal, for example: Ctrl + C, Ctrl + Z. |
| `-e` or `--enable-detailed` <br>  | `adb shell gprobe -e` or `adb shell gprobe --enabled-detailed` | Launch the GPU performance detailed analysis feature. This is a prerequisite for tracing rendering stage data and draw call data. This command takes effect during the app's initialization phase. Therefore, you must enable this feature before launching the target app. If the target app has already started running before you enable this feature, you must restart the app. <br> ***Note***: <br> Enabling this feature may increase the GPU load by up to approximately 10%. |
| `-d` or `--disable-detailed` | `adb shell gprobe -d` or `adb shell gprobe --disable-detailed`  | Disable the GPU performance detailed analysis feature. <br>  |
| `-t` or `--trace` | `adb shell gprobe -t` or `adb shell gprobe --trace` | Perform a one-time rendering stage data tracing. <br>  |
| `-x` or `--drawcall` | `adb shell gprobe -x` or `adb shell gprobe --drawcall` | Perform a one-time draw call data tracing. |
| `-s` or `--select` | `adb shell gprobe -s {packagename}` or `adb shell gprobe --select {packagename}` | Specify an app by its package name, such as `adb shell gprobe -s com.pico.testpackage`. <br> ***Note***: When this command is not used, the `adb shell gprobe -a `command is used by default to select all apps that can be tracked for performance data. |
| `-a` or `--all` | `adb shell gprobe -a` or  `adb shell gprobe --all` | Bind all currently traceable apps, including PICO's system-level apps such as runtime, veshell, xrshell, seethrough, and other third-party apps launched after enabling GPU performance detailed analysis. If successful, it returns the process IDs of all the selected apps. |
| `-h` or `--help` | `adb shell gprobe -h` or  `adb shell gprobe --help` | Get an overview and explanation of the command-line parameters. <br>  |
When using the command, you can combine the following optional parameters to achieve different data output effects.
| **Parameter** | **Description** |
| --- | --- |
| `--time n` | `--time` is used to set the interval or duration for data retrieval in seconds. This parameter can be used with `-r`(or `--realtime`), `-t`(or `--trace`), and `-x`(or `--drawcall`) parameters. For example, `adb shell gprobe -r --time 2` means fetching rendering stage data every 2 seconds. |
| `-l` or `--low-mode` | To perform a one-time render stage data tracing in low-GPU-load mode. It should be used in combination with `-t` (or `--trace`), and the final command is `adb shell gprobe -t -l`. When this parameter is set, detailed rendering stage and bin information will not be output. Instead, a general `Workload(us)` metric will be provided. |
| `-b` or `--bin` | To obtain detailed information related to bins in the rendering stage, including bin distribution, bin's rendering time, and partial Fixed Foveated Rendering (FFR) information. This parameter should be used with `-t` (or `--trace`), and the final command is `adb shell gprobe -t -b`. |
| `-p` or `--poll-mode` | To output data in a continuous polling manner, which reduces memory pressure. Data output can be terminated using Ctrl+C. It can be used in combination with `-t` (or `--trace`) and `-x` (or `--drawcall`) parameters, such as `adb shell gprobe -t -p`. |
| `-m` or `--message` | To list the metric IDs and metric names for real-time GPU data and draw call data. This should be used with `-r` (or `--realtime`) and `-x` (or `--drawcall`) parameters, like `adb shell gprobe -m -r`. |
| `--table` | To print draw call-related data in a tabular format for comparative analysis. Subsequently, you can save the table locally using the `adb shell gprobe -x --table > {file_name}.txt` command. |
## Retrieve real-time GPU performance data
Obtain real-time GPU performance data, including GPU usage, GPU frequency, and data related to textures, vertices, and shaders.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb524925e4874ff8931897295d719cb1~tplv-goo7wpa0wc-image.image" width="800px" />

### Procedure

1. Execute command `adb shell gprobe -r` or `adb shell gprobe --realtime` to obtain real-time GPU performance data. You can use the following optional parameters to access additional data output effects (refer to the [Command-line parameter description](#e1c075c3) section for details).
   | **Optional Parameter** | **Description** |
   | --- | --- |
   | `-- time n` | Customize the time interval for obtaining real-time data. |
   | `-r id1 id2 id3 ...` <br>  | Specify the metrics you want to retrieve. "idn" is the metric ID and you can refer to the "[GPU performance metrics reference](#9542a2d8)" section for details. <br> ***Note***: It's recommended to retrieve no more than 10 metrics at once to maintain data accuracy. |
2. Terminate data output using keyboard shortcuts supported by the terminal, such as Ctrl + C.

### GPU performance metrics reference
Below is a reference table for GPU real-time data metric IDs and their corresponding metric names.
| **Metric ID** | **Metric name** | **Description** |
| --- | --- | --- |
| 1 | Clocks | Total number of GPU clocks consumed by all system processes (time unit: seconds). |
| 2 | GPU % Utilization | GPU usage. |
| 3 | GPU % Bus Busy | Approximate percentage of GPU busy on the system memory bus. |
| 4 | % Vertex Fetch Stall | Percentage of clock cycles where the GPU cannot make any more requests for vertex data. |
| 5 | % Texture Fetch Stall | Percentage of clock cycles where the shader processors cannot make any more requests for texture data. |
| 6 | L1 Texture Cache Miss Per Pixel | Average number of Texture L1 cache misses per pixel. |
| 7 | % Texture L1 Miss | Percentage of L1 texture cache misses. Formula: number of L1 texture cache misses / L1 texture cache requests. |
| 8 | % Texture L2 Miss | Percentage of L2 texture cache misses. Formula: Number of L2 texture cache misses / L2 texture cache requests. |
| 9 | % Stalled on System Memory | Percentage of draw call cycles the L2 cache is stalled while waiting for data from system memory. |
| 10 | % Instruction Cache Miss | Percentage of instruction cache misses on the CPU. Formula: Number of L1 instruction cache misses / L1 instruction cache requests. |
| 11 | Pre-clipped Polygon | Number of polygons submitted to the GPU before any hardware clipping. |
| 12 | % Prims Trivially Rejected  | Percentage of primitives that are trivially rejected. A primitive can be trivially rejected if it is outside the visible region of the render surface. These primitives are ignored by the rasterizer. |
| 13 | % Prims Clipped | Percentage of primitives clipped by the GPU, where new primitives are generated. |
| 14 | Average Vertices / Polygon | Average number of vertices per polygon. |
| 15 | Reused Vertices / Second | Number of vertices used from the post-transform vertex buffer cache. |
| 16 | Average Polygon Area | Average number of pixels per polygon. |
| 17 | % Wave Context Occupancy | Percentage of time that all shader cores are idle with at least one active wave. |
| 18 | % Shaders Busy | Percentage of time that all shader cores are busy. |
| 19 | % Shaders Stalled | Average percentage of wave context occupancy per cycle. |
| 20 | Vertices Shaded | Number of vertices submitted to the shader engine. |
| 21 | Fragments Shaded | Number of fragments submitted to the shader engine. |
| 22 | Vertex Instructions | Total number of scalar vertex shader instructions issued. |
| 23 | Fragment Instructions | Total number of fragment shader instructions issued. |
| 24 | Fragment ALU Instructions(Full) | Total number of full precision fragment shader instructions issued. Does not include medium precision instructions or texture fetch instructions. |
| 25 | Fragment ALU Instructions(Half) | Total number of half precision scalar fragment shader instructions issued. Does not include full precision instructions or texture fetch instructions. |
| 26 | Fragment EFU Instructions | Total number of scalar fragment shader Elementary Function Unit (EFU) instructions issued, including math functions like sin, cos, pow, and more. |
| 27 | Textures / Vertex | Average number of textures referenced per vertex. |
| 28 | Textures / Fragment | Average number of textures referenced per fragment. |
| 29 | ALU / Vertex | Average number of vertex scalar shader ALU instructions issued per shaded vertex. |
| 30 | ALU / Fragment <br>  | Average number of scalar fragment shader ALU instructions issued per shaded fragment, expressed as full precision ALUs (2 mediump = 1 highp). |
| 31 | EFU / Fragment | Average number of scalar fragment shader EFU instructions issued per shaded fragment. Does not include Vertex EFU instructions. |
| 32 | EFU / Vertex | Average number of scalar vertex shader EFU instructions issued per shaded vertex. Does not include fragment EFU instructions. |
| 33 | % Time Shading Fragments | Percentage of time spent shading fragments. Formula: Time spent on shading fragments / Total time spent on shading. |
| 34 | % Time Shading Vertices | Percentage of time spent shading vertices. Formula: Time spent on shading vertices / Total time spent on vertices. |
| 35 | % Time Compute | Percentage of time spent in compute work. Formula: time spent in compute work / the total time spent shading everything. |
| 36 | % Shader ALU Capacity Utilized | Percent of maximum shader capacity (ALU operations) utilized. For each cycle that the shaders are working, the average percentage of the total shader ALU capacity that is utilized for that cycle. |
| 37 | % Time ALUs Working | Percentage of time the ALUs are working while the shaders are busy. Formula: ALU working time / Shader working time. |
| 38 | % Time EFUs Working | Percentage of time the EFUs are working while the shaders are busy. Formula: EFU working time / Shader working time. |
| 39 | % Nearest Filtered | Percentage of texels filtered using the nearest sampling method. |
| 40 | % Linear Filtered | Percentage of texels filtered using the linear sampling method. |
| 41 | % Anisotropic Filtered | Percentage of texels filtered using the anisotropic sampling method. |
| 42 | % Non-Base Level Textures | Percentage of texels coming from a non-base MIP level. |
| 43 | % Texture Pipes Busy | Percentage of time that any texture pipe is busy. |
| 44 | Read Total (Bytes) | Total number of bytes read by the GPU from memory. |
| 45 | Write Total (Bytes) | Total number of bytes written by the GPU to memory. |
| 46 | Texture Memory Read BW (Bytes) | Bytes of texture data read from memory. |
| 47 | Vertex Memory Read (Bytes) | Bytes of vertex data read from memory. |
| 48 | SP Memory Read (Bytes) | Bytes of data read from memory by the shader processors. |
| 49 | Avg Bytes / Fragment | Average texture data read from memory per fragment (in bytes). Formula: Total number of texture bytes read from memory / Total number of fragments. |
| 50 | Avg Bytes / Vertex <br>  | Average vertex data read from memory per vertex (in bytes). Formula: Total number of vertex bytes read from memory / Total number of vertices. |
| 51 | Preemption | The number of GPU preemptions that occurred. |
| 52 | Avg Preemption Delay | Average duration of GPU preemption, which is the average time from the preemption request to preemption start. |
| 53 | GPU Frequency | GPU frequency. |
## Trace **rendering stage data** 
Trace rendering stage data for the app, including rendering duration, anti-aliasing (MSAA) level, and more. 
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e919805378e4cd79a2013c1cb93372e~tplv-goo7wpa0wc-image.image" width="800px" />

Below are the steps to follow:

1. Execute command `adb shell gprobe -e` or `adb shell gprobe --enable-detailed` to enable GPU performance detailed analysis.
2. Launch the target app on the headset.
3. Execute command `adb shell gprobe -t` or `adb shell gprobe --trace` to trace rendering stage data. You can use the following optional parameters to access additional data output effects (refer to the [Command-line parameter description](#e1c075c3) section for details).
   | **Optional Parameter** | **Description** |
   | --- | --- |
   | `--time n` | Specify the duration of a single render stage data trace, with a default of 0.05 seconds. For example, `adb shell gprobe -t --time 0.25` indicates obtaining rendering stage data within 0.25 seconds. |
   | `-l` | Perform a one-time render stage data tracing in low-GPU-load mode. |
   | `-p` | Output data in a continuous polling manner. |
   | `-b` | Obtain detailed information related to bins in the rendering stage. |

## Trace draw call data
Trace draw call data for the app, including call duration, and data related to textures, vertices, and shaders.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e3171bc7f0d4a11960e63b6f3fd97d0~tplv-goo7wpa0wc-image.image" width="800px" />

### Procedure

1. Execute command `adb shell gprobe -e` or `adb shell gprobe --enable-detailed` to enable GPU performance detailed analysis.
2. Launch the target app on the headset.
3. Execute command `adb shell gprobe -x` or `adb shell gprobe --drawcall` to trace draw call data. You can use the following optional parameters to access additional data output effects (refer to the [Command-line parameter description](#e1c075c3) section for details).
   | **Optional Parameter** | **Description** |
   | --- | --- |
   | `--time n` | Specify the duration of a single draw call data trace, with a default of 0.05 seconds. For example, `adb shell gprobe -x --time 0.1` indicates obtaining all the draw call data within 0.1 seconds. |
   | `--table` | Print draw call-related data in a tabular format. |
   | `-x id1 id2 id3 ...` | Specify the metrics you want to output. "idn" is the metric ID and you can refer to the "[Draw call metrics reference](#58e407ca)" section for details. <br> ***Note***: It's recommended to retrieve no more than 10 metrics at once to maintain data accuracy. |

### Draw call metrics reference
| **Metric ID** | **Metric name** | **Description** |
| --- | --- | --- |
| 1 | Clocks | Number of GPU clocks that elapsed while a draw call was being executed. |
| 2 | % Vertex Fetch Stall | Percentage of clock cycles where the GPU cannot make any more requests for vertex data. |
| 3 | % Texture Fetch Stall | Percentage of clock cycles where the shader processors cannot make any more requests for texture data. |
| 4 | L1 Texture Cache Miss Per Pixel | Average number of Texture L1 cache misses per pixel. |
| 5 | % Texture L1 Miss | Percentage of L1 texture cache misses. Formula: number of L1 texture cache misses / L1 texture cache requests. |
| 6 | % Texture L2 Miss | Percentage of L2 texture cache misses. Formula: Number of L2 texture cache misses / L2 texture cache requests. |
| 7 | % Stalled on System Memory | Percentage of draw call cycles the L2 cache is stalled while waiting for data from system memory. |
| 8 | % Instruction Cache Miss | Percentage of instruction cache misses on the CPU. Formula: Number of L1 instruction cache misses / L1 instruction cache requests. |
| 9 | Pre-clipped Polygon | Number of polygons submitted to the GPU before any hardware clipping. |
| 10 | % Prims Trivially Rejected  | Percentage of primitives that are trivially rejected. A primitive can be trivially rejected if it is outside the visible region of the render surface. These primitives are ignored by the rasterizer. |
| 11 | % Prims Clipped | Percentage of primitives clipped by the GPU, where new primitives are generated. |
| 12 | Average Vertices / Polygon | Average number of vertices per polygon. |
| 13 | Reused Vertices / Second | Number of vertices used from the post-transform vertex buffer cache. |
| 14 | Average Polygon Area | Average number of pixels per polygon. |
| 15 | % Wave Context Occupancy | Percentage of time that all shader cores are idle with at least one active wave. |
| 16 | % Shaders Busy | Percentage of time that all shader cores are busy. |
| 17 | % Shaders Stalled | Average percentage of wave context occupancy per cycle. |
| 18 | Vertices Shaded | Number of vertices submitted to the shader engine. |
| 19 | Fragments Shaded | Number of fragments submitted to the shader engine. |
| 20 | Vertex Instructions | Total number of scalar vertex shader instructions issued. |
| 21 | Fragment Instructions | Total number of fragment shader instructions issued. |
| 22 | Fragment ALU Instructions(Full) | Total number of full precision fragment shader instructions issued. Does not include medium precision instructions or texture fetch instructions. |
| 23 | Fragment ALU Instructions(Half) | Total number of half precision scalar fragment shader instructions issued. Does not include full precision instructions or texture fetch instructions. |
| 24 | Fragment EFU Instructions | Total number of scalar fragment shader Elementary Function Unit (EFU) instructions issued, including math functions like sin, cos, pow, and more. |
| 25 | Textures / Vertex | Average number of textures referenced per vertex. |
| 26 | Textures / Fragment | Average number of textures referenced per fragment. |
| 27 | ALU / Vertex | Average number of vertex scalar shader ALU instructions issued per shaded vertex. |
| 28 | ALU / Fragment <br>  | Average number of scalar fragment shader ALU instructions issued per shaded fragment, expressed as full precision ALUs (2 mediump = 1 highp). |
| 29 | EFU / Fragment | Average number of scalar fragment shader EFU instructions issued per shaded fragment. Does not include Vertex EFU instructions. |
| 30 | EFU / Vertex | Average number of scalar vertex shader EFU instructions issued per shaded vertex. Does not include fragment EFU instructions. |
| 31 | % Time Shading Fragments | Percentage of time spent shading fragments. Formula: Time spent on shading fragments / Total time spent on shading. |
| 32 | % Time Shading Vertices | Percentage of time spent shading vertices. Formula: Time spent on shading vertices / Total time spent on vertices. |
| 33 | % Time Compute | Percentage of time spent in compute work. Formula: time spent in compute work / the total time spent shading everything. |
| 34 | % Shader ALU Capacity Utilized | Percent of maximum shader capacity (ALU operations) utilized. For each cycle that the shaders are working, the average percentage of the total shader ALU capacity that is utilized for that cycle. |
| 35 | % Time ALUs Working | Percentage of time the ALUs are working while the shaders are busy. Formula: ALU working time / Shader working time. |
| 36 | % Time EFUs Working | Percentage of time the EFUs are working while the shaders are busy. Formula: EFU working time / Shader working time. |
| 37 | % Nearest Filtered | Percentage of texels filtered using the nearest sampling method. |
| 38 | % Linear Filtered | Percentage of texels filtered using the linear sampling method. |
| 39 | % Anisotropic Filtered | Percentage of texels filtered using the anisotropic sampling method. |
| 40 | % Non-Base Level Textures | Percentage of texels coming from a non-base MIP level. |
| 41 | % Texture Pipes Busy | Percentage of time that any texture pipe is busy. |
| 42 | Read Total (Bytes) | Total number of bytes read by the GPU from memory. |
| 43 | Write Total (Bytes) | Total number of bytes written by the GPU to memory. |
| 44 | Texture Memory Read BW (Bytes) | Bytes of texture data read from memory. |
| 45 | Vertex Memory Read (Bytes) | Bytes of vertex data read from memory. |
| 46 | SP Memory Read (Bytes) | Bytes of data read from memory by the shader processors. |
| 47 | Avg Bytes / Fragment | Average texture data read from memory per fragment (in bytes). Formula: Total number of texture bytes read from memory / Total number of fragments. |
| 48 | Avg Bytes / Vertex | Average vertex data read from memory per vertex (in bytes). Formula: Total number of vertex bytes read from memory / Total number of vertices. |
| 49 | Preemption | The number of GPU preemptions that occurred. |
| 50 | Avg Preemption Delay | Average duration of GPU preemption, which is the average time from the preemption request to preemption start. |
## Known issues
For the PICO 4 Ultra series devices, using the PICO Graphics Probe Tool to execute the command `gprobe -r id1 id2 ... id10` causes the device to freeze and restart after running for a few minutes.


# --- END: PICO Graphics Probe Tool.md ---



# --- BEGIN: PICO Haptic Editor.md ---

PICO Haptic Editor supports editing broadband and multi-channel haptic feedback. You can import PHF files (.phf), audio files (.wav), and video files (.mp4), or use PICO's assets library to edit desired haptic feedback, and then experience it on your PICO device. Once you have crafted some haptic feedback, you can export the final file and use the same set of haptic feedback on different PICO devices.
## Before you begin
Download and install the [PICO Developer Center](https://developer-global.pico-interactive.com/resources/#pdc) on your computer. The PDC tool's installation package needs to be run as an administrator. During installation, an authorization window will pop up, and you need to grant permission.
## Install the PICO Haptic Editor

1. Launch the PICO Developer Center.
2. Go to **Download Center** > **Tools**.
3. Find the PICO Haptic Edit and click the **Download** button.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/919153b7fcce4bacafde3f6ebaa99a26~tplv-goo7wpa0wc-image.image)
   Once downloaded, you can find the PICO Haptic Editor under the **Installed** tab.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be4866a03a734f71be87070200171bf6~tplv-goo7wpa0wc-image.image)

## Edit haptic feedback

1. Go to the **Installed** tab, and click the **Start** button to launch the PICO Haptic Editor.
   Below is the UI of the PICO Haptic Editor:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df63558230204becaef8146ca3de0574~tplv-goo7wpa0wc-image.image)
2. Add a new track by one of the following methods:
   | **No.** | **Description** |
   | --- | --- |
   | 1 | Click **+ Add a new track**. |
   | 2 | Import and use your own asset files. <br>  <br> 1. On the top menu bar, click **File** > **Add Asset File**. <br> 2. Select and import desired asset files. <br>    ***Note***: Support importing .phf, .wav, and .mp4 files. <br>    You can find imported asset files in the **Asset** area. <br> 3. Drag an asset file from the **Asset** area to the track area. |
   | 3 | Drag an asset file from the **Library** to the track. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d55718fe773c4f2eb076776dd806d353~tplv-goo7wpa0wc-image.image) |
   If you drag an .mp4 file to the track, you can click the play icon on the top and preview the video file in the **Preview** area.

3. Select the controller that the haptic feedback is applied to. Available options: **Left** (left controller), **Right** (right controller), **Both** (both controllers).
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5000cddd5c774b139bb29b3b36efece9~tplv-goo7wpa0wc-image.image)
4. Edit the **Intensity** and **Frequency** nodes.
   * The vibration intensity value ranges from 0 to 1
   * The vibration frequency value ranges from 50 to 500 Hz
   Choose from the following methods:
   | **No.** | **Description** |
   | --- | --- |
   | 1 <br>  | Directly move the nodes up and down to increase or decrease vibration intensity or vibration requency. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2dd2bb07f13408a9e8441b9eb25f2ba~tplv-goo7wpa0wc-image.image) |
   | 2 (Recommended) | Select a node or a clip and edit its vibration intensity or vibration frequency value in the **Settings** area. <br>  <br> * If you select a node, edit the vibration intensity or vibration frequency value only for this node. <br> * If you select a clip, the vibration intensity and vibration frequency values of all the nodes of the clip will collectively increase or decrease by the same amount after you drag the slider. <br>  <br> ***Note***: This method is recommended because you can view the specific vibration intensity or frequency value in the **Settings** area. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25edf7a194bb4de69b6153365eaeb029~tplv-goo7wpa0wc-image.image) |
5. (Optional) Drag the slider to increase or decrease the duration of the track.
   * Increasing the duration adds new nodes.
   * Decreasing the duration reduces nodes (the original four nodes are always retained).
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b9bfff5c69e471e830afccd20c75a29~tplv-goo7wpa0wc-image.image)
6. (Optional) Perform the following operations as needed.
   | **No.** | **Description** |
   | --- | --- |
   | 1 | Undo the current setting, which means returning to the previous setting. |
   | 2 | Redo the latter setting. |
   | 3 | Clip the track. |
   | 4 | Paste a track. |
   | 5 | Delete a track. |
   | 6 | Play a track. Only supported by .mp4 files. |
   | 7 | Lengthen/shorten the track. This only visually changes the track's length, and the track's duration remains the same. |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a61e48c3bc249d9bd7e7356ff75e5ff~tplv-goo7wpa0wc-image.image)
7. (Optional) On the top menu bar, click **File** > **Export to PHF File** to export the current haptic settings as a .phf file.

## About .phf file
PHF haptic stream enables highly flexible haptic effects. Relevant settings are stored in the .phf file. For more information, refer to the "[Haptic feedback](/en_haptic-feedback#PHF%20haptic%20stream)" guide.


# --- END: PICO Haptic Editor.md ---



# --- BEGIN: RenderDoc for PICO.md ---

RenderDoc for PICO is a tool for graphic analysis and debugging.
## Release notes
| **Version** | **Release Time** | **Updates** |
| --- | --- | --- |
| 1.3 | August, 2025 | * Integrated updates from official RenderDoc v1.38. <br> * Enabled render stage and draw call tracing features. |
| 1.2 | March, 2024 | Deleted the "render stage tracing" and "draw call tracing" features. |
## Use cases
RenderDoc for PICO enables you to inspect the OpenGLES or Vulkan functions invoked by the target frame, to analyze textures, image meshes, and Pipelines, and to debug shaders.
## Requirements

* Operating system: Windows
* PICO Device system version: 5.6.0 or later versions

## Supported graphics APIs

* OpenGLES
* Vulkan
   For PICO 4 Ultra series devices, RenderDoc for PICO currently cannot capture frames for apps developed with Vulkan graphics APIs.

## Important notes
When using RenderDoc for PICO for debugging, ensure that your PICO device's screen remains on and the device is always connected with RenderDoc for PICO using a USB cable, otherwise the debugging process will be interrupted.
## Quickstart
This section outlines how to download and connect RenderDoc for PICO and how to perform basic debugging on the target frame, including inspecting the OpenGLES or Vulkan functions invoked by the frame, and analyzing textures, image meshes, and Pipelines.
### Step 1: Download and install RenderDoc for PICO
| **Method One** | **Method Two** |
| --- | --- |
| Click the following link to download: [http://lf-renderdoc-for-pico.picovr.com/obj/renderdoc-for-pico/RenderdocForPico_installer_edition_v1.3.msi](http://lf-renderdoc-for-pico.picovr.com/obj/renderdoc-for-pico/RenderdocForPico_installer_edition_v1.3.msi) <br>  | If you download RenderDoc for PICO using this method, you can only launch it through the PICO Developer Center. Use the following steps to download it: <br>  <br> 1. Launch the PICO Developer Center. <br> 2. From the left navigation panel, select **Download**. <br> 3. On the **Tools** list, click the **Download** button in the **RenderDoc for PICO** area. <br>  <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0fb887ad6e541ee8d2023bad595be11~tplv-goo7wpa0wc-image.image) <br>  |
### Step 2: Launch RenderDoc for PICO
| **Method One** | **Method Two** |
| --- | --- |
| Go to the folder where RenderDoc for PICO is located and double-click **qrenderdoc.exe** to launch RenderDoc for PICO. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1998e763d4d4450394e93cdf3e791737~tplv-goo7wpa0wc-image.image) <br>  | 1. Go to the **Installed** list of the **Download** center. <br> 2. Click the **Start** button to launch RenderDoc for PICO. <br>  <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/955eb54288dd4dffb64b2aa864f24138~tplv-goo7wpa0wc-image.image) <br>  |
After launching, you will see the following window:
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34d22dc664bd43e489784873910962a9~tplv-goo7wpa0wc-image.image" width="546px" />

### Step 3: Connect the PICO device to RenderDoc for PICO
Connect the PICO device to RenderDoc for PICO, and then use the Normal mode for regular debugging purposes.
**Prerequisites**
Before connecting the PICO device to RenderDoc for PICO, make sure that the device is awake, remains on its default desktop scene which appears after startup, and the track movement function is turned off.
* To keep the device screen always on, toggle the **Keep Device Awake** switch in the **System Settings** panel on the home page of the PDC tool.
* To disable the track movement function, go to PICO Device's **Settings** > **General** > **Track Movement** to turn it off.

**Steps**

1. Connect the PICO device to the computer using a USB cable.
2. In the bottom left corner of RenderDoc for PICO, click **Replay Context: Local** to select the connection mode.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/930c0a5d00a440569287d4691cdc5b2a~tplv-goo7wpa0wc-image.image" width="524px" />   

   If you see the words "Remote Server Ready," at the bottom of the interface, it means the connection is successful. Upon the first successful connection, RenderDoc for PICO will automatically install two APK files, namely `com.picoxr.renderdoccmd.arm32` and `com.picoxr.renderdoccmd.arm64`, and launch the 64-bit `com.picoxr.renderdoccmd.arm64` file.

### Step 4: Launch the Activity file within the target APK folder

1. Go to the **Launch Application** window.
2. Click the "**...**" button on the right side of the **Executable Path** field.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ca1e09995824e2196e637772579485f~tplv-goo7wpa0wc-image.image)
3. In the **File Browser** window, select the Activity file within the target APK folder that you want to capture and debug frames for, then click **OK**. If you can't find the target APK folder, check the **Show hidden files** checkbox at the bottom of the **File Browser** window and try again.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d2b18422fec4130b54239e602d5e211~tplv-goo7wpa0wc-image.image)
4. Click **Launch** in the bottom right corner of the **Launch Application** window.
   On the PICO device, the system will start up and enter the selected app.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c2407160d6f4b198548a994b6fd0c50~tplv-goo7wpa0wc-image.image)

### Step 5: Capture a frame
Go to the device window, then click the **Capture Frame(s) Immediately** to capture a frame.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc3eb8ec2530436b8699983ea8b48bbc~tplv-goo7wpa0wc-image.image)
Then you can see the preview frame in the **Captures collected** section.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aad4afd8cc1b42cc9d81df9e0f723ec1~tplv-goo7wpa0wc-image.image)
**Note**
Due to GPU driver issues, if you need to capture frames of a Vulkan app, you need to set the value of the property "persist.pxr.sdk.prop.vulkan_debug" to 1 and restart the device:
```Plain Text
adb shell setprop persist.pxr.sdk.prop.vulkan_debug 1
adb reboot
```

When RenderDoc for PICO detects that you have not completed this setting, the following dialog box will appear, asking if you need assistance with the setup. If you choose **Yes**, RenderDoc for PICO will help you complete the setting and restart the device.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97d0122441b94f628150afc68b3d0455~tplv-goo7wpa0wc-image.image" width="300px" />

After using RenderDoc for PICO, execute the following command to restore the configuration environment.
```Plain Text
adb shell setprop persist.pxr.sdk.prop.vulkan_debug 0
adb reboot
```

### Step 6: (Optional) Save a frame
Right-click on the preview frame and select **Save** from the context menu to save the frame locally.
Once saved, if you need to continue debugging the frame later, there is no need to capture it again. You can go to **File** > **Open Capture** or **Open Capture with Options** to import the saved frame.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f54d815b7cfb43f8b8bcd0531a9845b2~tplv-goo7wpa0wc-image.image)
### Step 7: Load a frame
| **Method One** | **Method Two** |
| --- | --- |
| To analyze a new frame, it is recommended to load it using the following method: <br> Double-click on the preview frame in the **Captures Collected** section to load the frame file. <br>  | To reanalyze a saved frame, you can load it using the following method. Of course, you can also use this method to load a new frame for analysis. <br>  <br> 1. From the menu bar at the top, select **File** > **Open Capture** or **Open Capture with Options**. <br> 2. If you choose **Open Capture**, directly select and import the target capture file in the pop-up window. If you choose **Open Capture with Options**, you can configure the loading options while selecting the target capture file, follow the step below: <br>    ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dff4342c1b624014a4131a50e16a9f32~tplv-goo7wpa0wc-image.image) <br>    1. In the **Capture File** field, click the **...** button and select the target capture file. <br>    2. In the **GPU Selection Override** field, choose the GPU type. It is recommended to select Qualcomm Adreno GPU, which corresponds to the GPU of the PICO device, to ensure consistency of the hardware during debugging. <br>    3. In the **Replay optimisation level** field, select the level of replay optimization. <br>       * **No Optimisation**: No optimization is performed. <br>       * **Conservative**: Some optimizations are performed with no perceivable impact on the user's side. <br>       * **Balanced** (default): Some optimizations are performed with minor, noticeable impact. <br>       * **Fastest**: More optimizations are performed, potentially leading to some data that is difficult to understand or "impossible" during analysis. <br>       ***Note***: In Profiling mode, regardless of selecting **Balanced** or **Fastest** level, the tool uses the **Fastest** level. For more information about replay optimization levels, refer to [the official documentation of RenderDoc](https://renderdoc.org/docs/how/how_control_replay.html). <br> 3. Click **Open**. |
After successful loading, the **Event Browser** window will display the rendering flow of this frame.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f7da55bfd8a468499fd684b5d978493~tplv-goo7wpa0wc-image.image)
### Step 8: Debug a frame
The basic debugging actions are shown in the table below. 
| **Debugging action** | **Description** |
| --- | --- |
| Browse events <br>  | The **Event Browser** window displays the OpenGL ES or Vulkan functions called during the rendering of the frame. Functions with the keyword "Draw" are scene rendering functions, and you can double-click on them to replay. For more information, refer to the official RenderDoc documentation: [Event Browser](https://renderdoc.org/docs/window/event_browser.html). <br> After double-clicking on a "Draw" function, RenderDoc replays it, and you can view the replayed rendering results in the **Texture Viewer** window. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7992cf9b66c9457296cc645c02e5fe2c~tplv-goo7wpa0wc-image.image) |
| Analyze textures | Analyze the textures of the frame in the **Texture Viewer** window. For more information, refer to the official RenderDoc documentation: [Texture Viewer](https://renderdoc.org/docs/window/texture_viewer.html.). <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/095bd5e951cc4c7bb2bde28fe5caf848~tplv-goo7wpa0wc-image.image) |
| Analyze mesh data | Analyze the mesh data of the frame in the **Mesh Viewer** window. For more information, refer to the official RenderDoc documentation: [Mesh Viewer](https://renderdoc.org/docs/window/mesh_viewer.html). <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/525c49b781e54916b1ff4728aec17e9f~tplv-goo7wpa0wc-image.image) |
| Debug a shader <br>  | Debug a shader of the frame in the **Pipeline State** window. Follow these steps: <br>  <br> 1. Click on a shader node in the pipeline diagram. <br> 2. Click **Edit**. <br> 3. Debug the shader. <br>  <br> For more information, refer to the official RenderDoc documentation: [Pipeline State](https://renderdoc.org/docs/window/pipeline_state.html). <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19dd5a7fa53543e0b5eb76e89d02f709~tplv-goo7wpa0wc-image.image) <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6effaa244a640eda7a62c4a1e3c951e~tplv-goo7wpa0wc-image.image) <br>  |
| Inspect OpenGLES / Vulkan resources | Analyze all the API objects contained in the frame in the **Resource Inspector** window. For more information, refer to the official RenderDoc documentation: [Resource Inspector](https://renderdoc.org/docs/window/resource_inspector.html). <br>  <br> 1. In the **Event Browser** window, click on the openGL ES (starting with "gl") or Vulkan functions (starting with "vk"). <br>  <br>   The **API Inspector** window will display the API objects contained in that function. <br>  <br> 2. Click on the target API object. <br>  <br>   The **Resource List** section in the **Resource Inspector** window will display the resources contained in that API object. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62c55d28b11e41188ec4a4ffe16e0266~tplv-goo7wpa0wc-image.image) |
## Retrieve logs
| **Log object** | **View method** |
| --- | --- |
| PICO device | Use the following ADB commands: <br>  <br> * adb pull /data/logs  <br> * adb logcat  |
| PC-end RenderDoc | * Use the following ADB commands: C:\Users\<username>\AppData\Local\Temp\RenderDocForPico <br> * In the RenderDoc for PICO: click **Window** > **Diagnostic Log**. <br>  <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f65f4da563fa40ebbcb6185d7902cea2~tplv-goo7wpa0wc-image.image) |
## Troubleshooting
### Why can't RenderDoc for PICO connect with my PICO device?
Try the following solutions:

* Keep your PICO device awake and remain on its default desktop scene which appears after startup, then try again.
   **Notes**:
   When connecting with the PICO device, RenderDoc for PICO will install an APK in the PICO device and then launch its Activity to establish a socket connection with the PC. If the headset is in the Seethrough state or turned off, the Activity may fail to start and the socket connection fails to be established. For example, when establishing a connection, the following window may appear, requiring you to click **Exit and Continue** and then to try again.
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/224e5b046e34415895bd797dc8be3125~tplv-goo7wpa0wc-image.image" width="300px" />   

* Close other programs that may use adb.

### Why can't I find the APK to capture frames for?
Check the **Show hidden files** checkbox in the lower-right area of the **File Browser** window, and then try again. Meanwhile, ensure that your APK is debuggable. For details, see the Android NDK documentation [Enable layers](https://developer.android.com/ndk/guides/rootless-debug-gles#enable-layers).
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/273c81e13da54820a8069320234181ae~tplv-goo7wpa0wc-image.image" width="546px" />

### Why is the "Capture Frame(s) Immediately" button grayed out？
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9aa490faace46fc80c4d6a0e28ab149~tplv-goo7wpa0wc-image.image" width="546px" />

* If you are using the Vulkan API, check whether frame markers are enabled. Try the following steps to resolve this:
   ```Bash
   adb shell setprop persist.pxr.sdk.prop.vulkan_debug 1
   adb reboot
   ```

* If you are using the OpenGLES API, feel free to provide specific feedback to PICO.

### Why did I fail to launch a 32-bit app?
If your app is a 32-bit app, you need to change it to a 64-bit app. This is because when running RenderDoc for PICO, the application requires more memory. However, 32-bit apps have limitations on the size of memory, which may result in memory allocation failures.
You can identify this issue by the keyword "kgsl_sharedmem_alloc() failed" in the log:
```C++
42009:7-08 16:56:06.185  2640 12506 E Adreno-GSL: <gsl_memory_alloc_pure:3013>: ERROR: kgsl_sharedmem_alloc() failed! Allocation size: (20352 KB); Flags: (0xcd5f3375)
```


# --- END: RenderDoc for PICO.md ---



# --- BEGIN: Snapdragon Profiler.md ---

Snapdragon Profiler is an analysis software that can run on the Windows, Mac, and Linux platforms. It connects with Android devices powered by Snapdragon® processors over USB. Snapdragon Profiler allows developers to analyze CPU, GPU, DSP, memory usage, power consumption, heat dissipation, and network data, thereby assisting them to find and fix performance bottlenecks. Below are the key features and benefits:

* Offers a real-time view of system resource usage
* Visualizes kernel and system events using the Trace Capture mode to assist event analysis
* Allows developers to capture and debug rendered frames through the Snapshot Capture mode
* Offers the following GPU APIs: OpenGL ES 3.1, OpenCL 2.1, and Vulkan 1.0

For more information, see the [Snapdragon Profiler official documentation](https://developer.qualcomm.com/software/snapdragon-profiler).


# --- END: Snapdragon Profiler.md ---



# --- BEGIN: View draw calls.md ---

This page introduces how to use the **Frame Debugger** to view the draw calls used in your application.
## Frame Debugger Overview
Frame Debugger allows you to freeze a game on a particular frame, and list the draw calls used to render this frame. You can view the order of draw calls, or walk through the draw calls one by one to see how the scene is built from graphical elements. For more information, see [The Frame Debugger window](https://docs.unity3d.com/2020.3/Documentation/Manual/FrameDebugger.html) on Unity website.
## Open the Frame Debugger window
Follow the steps below to open the Frame Debugger window:

1. Open your project in Unity Editor.
2. From the top menu bar, select **Window** > **Analysis** > **Frame Debugger**.
   The **Frame Debug** window appears.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/88ec38a36d484437b9b430aeef3bc439~tplv-em5hxbkur4-noop.image?width=1220&height=735)

If you want to learn more about how to use the Frame Debugger window, read this [documentation](https://docs.unity3d.com/2020.3/Documentation/Manual/FrameDebugger.html) on Unity website.


# --- END: View draw calls.md ---



# --- BEGIN: View overdraw.md ---

Overdraw seriously affects the GPU performance of mobile games. You can view overdraw so as to optimize your applications accordingly in time. Follow the steps below to view overdraw:

1. Open your project in Unity Editor.
2. Click **Scene**.
3. Expand the drop-down menu under the **Scene** tab.
4. From the **Miscellaneous** list, select **Overdraw**.
   Overdrawn areas are marked by semi-transparent colors forming a "heat map". The most saturated areas represent the most overdrawn areas in a scene.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/1f5a87dd0cff4bf3bdb6f8e558056ffd~tplv-em5hxbkur4-noop.image?width=2009&height=1070)


# --- END: View overdraw.md ---



# --- BEGIN: XR Profiling Toolkit.md ---

The XR Profiling Toolkit Unity package is an automated and customizable graphics profiling tool for evaluating the performance of XR applications running on headset devices. The core framework of the toolkit involves automated test scripting, graphics feature toggling, profiling data export, and report generation for in-depth performance analysis and comparison. 
You can easily integrate this tool into your existing XR projects via the Unity Package Manager. In addition, we provide open-source high-quality VR and MR sample scenes to demonstrate the toolkit's usages and capabilities.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dec7dd7a83d34790b9b292222c857fd8~tplv-goo7wpa0wc-image.image" width="600px" />

XR Profiling Toolkit VR and MR sample scenes

## **Use cases**

* **Cross-Vendor Evaluation:** The XR Profiling Toolkit enables developers to assess the hardware capabilities of various XR headsets and easily draw comparisons between two testing results, providing a clear understanding of the performance budget across different hardware platforms.
* **Graphics Content Optimization:** The XR Profiling Toolkit helps developers make informed decisions about their graphics content, rendering features, and visual quality achievable on different headsets, assisting content creation optimization and resource planning for XR devices.
* **Sample Scene and Testing:** The XR Profiling Toolkit provides high-quality VR and MR art scenes as a reference for developers. This sample also serves as a testbed to help reproduce performance or functional issues when troubleshooting.

## **Using the XR Profiling Toolkit Project**
You can get the XR Profiling Toolkit and the sample scenes from [Unity Asset Store](https://assetstore.unity.com/packages/tools/utilities/xr-profiling-toolkit-311263), or from our [GitHub repository](https://github.com/Pico-Developer/XR-Profiling-Toolkit/).
The project includes source code scripts, art assets, and other resources, all under the MIT License. You can also find and install the app's apk file that we built from the project in the Releases section.
## Setup
### Supported Devices

* PICO 4 series, including PICO 4 Ultra
* PICO Neo 3 series
* Meta Quest 3
* Meta Quest 2

### Development Environment

* PICO SDK version: 3.1.2
   * included in the project and imported from the downloaded file
   * Note that there may be conflicting guids with other providers when you import the PICO SDK from the git url. This is a known issue and will be fixed in a future update.
* Meta XR All-in-One SDK version: 72.0.0
   * Included in the project and installed via the Unity Package Manager
* Unity version: 2022.3.23f1 LTS
* Graphics API: Vulkan
* Target architecture: ARM64
* Windows or Mac host
   * [Android Debug Bridge](https://developer.android.com/tools/adb) installed
   * Python version: 3.7.17 (pip version: 23.0.1)

### Cross-Vendor Build
If you want to build the Unity project yourself, you will need to set the build target to Android and configure the XR Plug-in provider.
The project is developed to support cross-vendor builds and testing. When targeting a specific device such as PICO and Quest, select the corresponding **Plug-in Providers** in **Project Settings -> XR Plug-in Management**. We recommend using the settings provided in the project for optimized performance and functionalities.
Notice that you will need to uncheck the previous platform when switching and deploying to other platforms.
If you are interested in cross-vendor deployment in your own project and extending the platforms currently provided in the sample project, check out the **PlatformSwitcher.cs** script and the **XR Origin** setup in the scene.
### XR Feature Settings
The XR Feature Settings object can be found in **Packages/XR Profiling Toolkit/Settings/XRFeatureSettings**. Once set, the settings will be applied to **all** **scenes**.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a51bcf2fba94c7db2a3e590562d5fb9~tplv-goo7wpa0wc-image.image" width="600px" />

* **Incompatible Features**: features that are not compatible with each other. Incompatible features can't be enabled simultaneously, such as Foveated Fixed Rendering (FFR) and Adaptive Resolution. By default, none are in the list.
* **Foveation Level**: level of foveated rendering. Recommend medium level for a balance of quality and performance
* **MSAA Samples**: number of samples for [MSAA](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@15.0/manual/anti-aliasing.html#multisample-anti-aliasing-msaa). 4x is recommended.
* **Feature Status In Manual Mode**: Sets which features to turn on when in Manual Mode. In Manual Mode, users can explore the scene and interact with objects. It is recommended that both MSAA and FFR should be turned on.
* **Target Resolution**: the eye buffer resolution at which the scene will be rendered.
   * On different platforms, the width or the height of the eye buffer may not match exactly, but the total number of pixels should be close. 
   * The given value is for mainstream devices. Value can be set higher for advanced devices.

## Sample Scene
You can import the sample scene from **Windows->Package Manager->XR Profiling Toolkit->Samples->Cyber Alley VR Sample Scene**. In this VR sample scene, users can interact with interactable objects, teleport to viewpoints, and explore various rendering optimization features.
### Main Menu
Use the controller to select a sample scene in the main menu interface. Two sample scenes are available now. 
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53da9098852c4b81942fa2a27249c9ed~tplv-goo7wpa0wc-image.image" width="600px" />

Choose test scene in the main menu

### VR Sample Scene - Cyber Alley
The Cyber Alley scene is a showcase scene that evaluates the performance of a well-made VR scene. It features various graphics enhancement features, a dynamic particle system, and performance evaluation and debugging tools. On PICO 4, it runs consistently at 72 frames per second (FPS), which is the default maximum FPS. In the project settings, we lock it to be 72 FPS for performance reasons, such as protecting overburn, and recommend doing so. If you don't want to lock the FPS, you can change the setting in **Assets -> XR -> Settings -> PXR_Settings**.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5215da9c39554a3da133df12a17eaa54~tplv-goo7wpa0wc-image.image" width="600px" />

XR Profiling Toolkit VR Sample Scene - Cyber Alley

#### Controls




![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56a86bcd53c24cb78bb2129882b272f3~tplv-goo7wpa0wc-image.image)
PICO 4 controller input mapping. Other XR controllers share similar controls.

Control tooltips are also displayed on the controller model when running the scene. See the right image.




![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/142a576057e74721851a03e451fce4e7~tplv-goo7wpa0wc-image.image)
Button hints and tooltips on the controller models

* **Toggle UI Menu:** A/X or Menu Button
* **Interact with Object or UI:** Trigger
* **Teleport:** Thumbstick forward to activate, release to select target and teleport
* **Snap Turn:** Thumbstick left or right




#### Teleportation Points
There are 5 teleportation points in the scene, and they will be visible when teleportation is activated by the user. When a teleportation point is selected by hovering, its visual effect will change. Teleporation will take place when releasing the thumbstick with a target selected.
Note that the player may not keep their original orientation after teleportation. This is designed to orient users to look at specific areas in the scene.

#### UI Menu
There are two tabs in the UI menu: Settings and User Guide.




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00b0afdc09034ebead1db90036046778~tplv-goo7wpa0wc-image.image" width="924px" />

Settings menu

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6504c337abf40a79de57fb93f8972ad~tplv-goo7wpa0wc-image.image" width="1615px" />

Debug View




**Settings**

* ##### Graphics
   It is expected to see noticeable visual changes when each of the settings is toggled.
* ##### Debug View
   The Tile Visualizer is used to visualize the Fragment Density Map (FDM) pattern when FFR is turned on. The green area indicates the full resolution. When FFR is turned on, there should be some yellow (1/2 resolution) and orange (1/4 resolution) tiles in the peripheral region of the view.
   Tile patterns vary across platforms and also change when MSAA is turned on and off.
* ##### Misc
   Mute - mute scene audio. Useful to mute the sound when testing to not get disturbed.







<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e11912e08104379bfefc821bed9dbf1~tplv-goo7wpa0wc-image.image" width="926px" />

User Guide Menu




**User Guide**
Instructions about how to interact with the scene. 




#### Dynamic Particles
The particle emitter is highlighted in the scene with an outlining effect.
When hovering, the highlighting effect will be off, and a pop-up will prompt users to change particle mode by interacting with the emitter.
#### Modes

* **Off**: no particle
* **Particle system**: orange smoke
* **VFX graph**: purple smoke

* Notice that the default VFX graph renderer block is not compatible with Multiview. We overcame this by using a custom shader graph for particle rendering. To adjust the effect yourself, you will need to [enable shader graph for VFX graph](https://docs.unity3d.com/Packages/com.unity.visualeffectgraph@14.0/manual/sg-working-with.html).
* GPU load will change when switching between modes, and it will likely cause some frame drops. It should be running at full frame rate once stabilized.

### MR Sample Scene - Relic
The Relic scene is a showcase scene that evaluates the performance of an MR scene with the real-world environment displayed in the passthrough. It features various graphics enhancement features, a spatial prop system using spatial anchors, and performance evaluation and debugging tools. 
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9855c0ea2c8f439a98f18392d34abcbb~tplv-goo7wpa0wc-image.image" width="600px" />

XR Profiling Toolkit MR Sample Scene

#### Controls

* **Toggle UI Menu:** A/X or Menu Button
* **Interact with UI:** Trigger
* **Place spatial props:** Trigger
* **Delete spatial props:** B/Y
* **Cancel selected spatial props:** Grip

#### UI Menu
There are two tabs in the UI menu: Settings and Props.




<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3521320dee1461b9b2f93a0216e2f02~tplv-goo7wpa0wc-image.image" width="556px" />

Graphics Settings Menu




**Settings**

* ##### Graphics
   It is expected to see noticeable visual changes when each of the settings is toggled.
* ##### LOD Level
   The relic items in the demo scene have already been configured with 3 levels of LOD.You can test the LOD changes by moving the observation position in the space. Alternatively, you can click a button to change the LOD levels of all items at once.
* **Misc**
   Mute - mute scene audio. Useful to mute the sound when testing to not get disturbed.







<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ef4df53120b454aa9ac85a407beadcc~tplv-goo7wpa0wc-image.image" width="602px" />

Props Settings Menu




**Props**
You can follow the guidance on the Props menu to freely create spatial anchor objects in MR for performance testing.




#### Spatial Prop Settings
The demo scenario provides three basic spatial object models. You can also import your own scenarios or models for performance testing through the following configurations.
You can find the setting file under "Demo Sample Scenes/RelicMRSampleScene/Settings.
#### MR Asset Settings Guide

* **Main Test Prefab** : It will be created after the scene is calibrated and entered. It will attempt to be created on the calibrated object labeled "Table". If there is no object of this type, it will be attempted to be created directly in front of you. If his value is NULL, no object will be created.
* **Id2Prefab** : Here are examples of three objects. You can also try to configure your own models in this table. Later, you'll be able to find them in the **Props** menu of the scene, create them freely in space, and conduct performance tests.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5147d506783b4e6c920e48430bff9fc3~tplv-goo7wpa0wc-image.image" width="600px" />

* The object should attempt the `XR Simple Interactable` and `Collider` scripts for UI Selecting. 

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1e4635ef73441e7b37cd79a9119d0cc~tplv-goo7wpa0wc-image.image" width="400px" />

## Automated Test
The scene can be run automatically with a pre-configured command sequence (see Command Queue below), and a performance report showing the test results will be generated. 
This generated report helps developers evaluate scene complexities, identify performance hotspots, and verify performance optimization and regression.
The MR Scene's Automated Test can only be run on PICO4 Ultra or Meta Quest 3 devices.

### Command Queue
Command Queue is used to store scene automation sequences. Whenever running a profiling session, a serialized Command Queue needs to be specified to define how the session should be run. For the convenience of saving and debugging by yourself, we recommend clicking **XR Profiling Toolkit -> Shortcut -> Copy Scriptfolder To Assets**, which moves the demo script from the Package folder to the asset folder, then you can find the demo script in **Assets\XRProfilingToolkit\Editor\ProfilingToolScripts.**
####  Create and Edit a Command Queue
To create a Command Queue in Unity Editor, right-click on the Project window and select **Create-> XRProfilingToolkit -> Command Queue.**
The following section contains instructions for command queue configurations. Once configured, click the **Save to File** button to save the current Command Queue to a JSON file on disk for later use.
You can find three sample Command Queue assets by default in **Package\XR Profiling Toolkit\ Editor\ProfilingToolScripts\SampleCommandQueues**.
If you click the shortcut menu **XR Profiling Toolkit -> Shortcut -> Copy ProfilingToolScripts folder To Assets** these sample Command Queue assets will be copied to the Assets folder in **Assets\XRProfilingToolkit\Editor\ ProfilingToolScripts\SampleCommandQueues** for ease of use.
Likewise, you can find three Command Queue samples JSON files saved in **Package\XR Profiling Toolkit\Editor\ProfilingToolScripts\AutomationScripts** or **Assets\XRProfilingToolkit\Editor\ ProfilingToolScripts\AutomationScripts**.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/115e869e00ab4a6bbd85ac323c0fa566~tplv-goo7wpa0wc-image.image" width="500px" />

A Command Queue Example

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8388a46f0214a8bb33bc3eba1edcb37~tplv-goo7wpa0wc-image.image" width="600px" />

Sample Command Queues

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59db68a919f446b087a30d12a567a5d8~tplv-goo7wpa0wc-image.image" width="600px" />

Profiling Tool Scripts. We recommend copying the files from the Packages folder to the Assets folder for ease of use.

#### Configurations

1. **Id**: used to identify the command queue. Only profiling sessions running with the same command queue should be compared to ensure the scene has been run in the same way.
   1. **Version**: id should end with [semantic version](https://semver.org/) X.Y.Z. Whenever the command queue is saved, patch version (Z) will be bumped automatically. Major (X) and minor (Y) versions will need to be bumped manually.
2. **Stop Time**: after the specified number of seconds, the whole command queue will be stopped, and any pending commands will not run.
3. **Commands**: list of scene automation commands. Scene Automation Command can be added to the list and command type can be specified with the dropdown list.

The following basic commands are supported by default for any test scene:

1. **CommandMove**: move to the target position at the specified speed.
2. **CommandPause**: pause the whole command queue when this command is reached. Any subsequent commands will not run.
3. **CommandWait:** wait for a certain period before the next command.
   1. **DurationInSec (float):** seconds to wait
4. **CommandScreenCapture**: capture screenshot, screen record, rendering stage, or draw call. This works with the Python script. The command prints out an adb log with the Python script monitoring logcat. When the screen capture log is printed, the Python script calls the corresponding service to capture it.
   1. **Type (enum)**: type of capture. Including CaptureScreen, StartScreenRecord, EndScreenRecord, CaptureRenderingStage, CaptureDrawCall. The last two options capture detailed GPU metrics and are only recommended if you know how to read them.
   2. **Context (string):** context of the capture. This can be any metadata associated with the capture. Captures with the same context will be grouped together in the report.

The following basic commands are supported in conjunction with components in any scene:

1. **CommandLoadLevel**: load a specific level with the **SceneLoader.Prefab**, you can find it at **XR Profiling ToolKit->Shortcuts**
   1. **Level Index (int)**: which level to load, starting from 0. 0 indicates the 1st profiling scene.
2. **CommandToggleFeature**: toggle the scene features with the **FeatureManager.Prefab**, you can find it at **XR Profiling ToolKit->Shortcuts**
   1. **Feature (enum)**: includes the following rendering features: FFR (fixed foveated rendering, Med Level), MSAA (4x), [Dynamic Resolution](https://developer.oculus.com/documentation/unity/dynamic-resolution-unity/) (Meta) or [Adaptive Resolution](https://developer.picoxr.com/document/unity/adaptive-resolution/) (PICO).
   2. **Enabled (bool)**: turn on or off the feature

The following examples of expandable commands are supported in the Cyber Alley scene according to their specific logic. You can try to expand your own commands on your own project:

1. **CommandSetDynamicMode**: set the dynamic mode of the scene. Scene 1 has a dynamic particle system
   1. **Mode (int)**: mode of dynamic system. In Scene 1 (Cyber Alley), 0: no effect, 1: using particle system, 2 - using vfx graph
2. **CommandTeleport**: teleport to a target teleportation anchor location
   1. **TargetId (int)**: index of the teleportation anchor, ranging from 0 to 4 available targets in the scene. Check **TeleportAnchors_Scene1** in **CyberAlley** for teleportation locations and their corresponding index.

The following examples of expandable commands are supported in the Relic scene according to their specific logic. You can try to expand your own commands on your own project:

1. **CommandCreateSpaceItem**: set the dynamic mode of the scene. Scene 1 has a dynamic particle system
   1. Position X/Y/Z **(float)**
   2. Rotation X/Y/Z/W**(float)**
   3. Scale X/Y/Z**(float)**
   4. Item Id: The item Id in "**MR Asset Settings**" ->"**Id2Prefab**"->"ID",You can find the setting guide in *MR Asset Settings Guide*.
2. **CommandSetLODLevel**: set the LOD level of the scene Objects
   1. level **(int)**: value of the LOD level, ranging from 0 to 2 available targets in the relic scene..
3. **CommandWaitForSceneCapture**: wait for the Scene Capture finished

### Device Profiling Tool Window
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50d3a3649d3a4b68bd907c5dc0e516f3~tplv-goo7wpa0wc-image.image" width="450px" />

#### Requirements for Profiling Sessions

* Host machine, Windows or Mac, with [adb](https://developer.android.com/tools/adb) installed
* Headset connected to the host machine, listed in `adb devices`
* Python version: 3.7 or later

#### Running a Session

1. Choose a **CommandQueue JSON path** by clicking Browse to select a JSON file we saved in command queue, or copying the full path to the JSON object we saved in command queue and paste it into the command text.
2. Choose a **Profiling Data Output Path** by clicking Browse to select a directory to output file, or copying the directory path and paste it into the command text.
3. Click **Run Automation** button and then you will see logs printed out in the terminal. Once completed, you will find a new folder containing metrics and screenshots captured during the session at Output Path.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/877eec1adccf4c3fb72e0b9a1f4279b8~tplv-goo7wpa0wc-image.image" width="389px" />

4. If the **Run Automation** button doesn't work, you can also click the **Copy Run Automation Command** button and try it on a command line terminal.

### Result Analysis
Once we have the session data, we can then generate reports to visualize the performance analysis of the profiling sessions.
#### Requirements

* Python version: 3.7 or later
* Python dependencies installed
   * Click the **Set Up Analysis Tool Environment** button and wait for completion.
   * If the **Set Up Analysis Tool Environment** button doesn't work, you can try to open a command line terminal, locate the Package's Profilting ToolScripts folder in **Package\XR Profiling Toolkit\Editor\ProfilingToolScripts\**, and run `pip install -r requirements.txt` command to manually run the command.

#### Metrics Configuration
There are three .schema files in JSON format under the ProfilingToolScripts **** folder defining which metrics should be displayed in the profiling report

* pxr_metrics.schema: basic performance metrics for PICO
* ovr_metrics.schema: counterpart of basic performance metrics on Quest
* pil_output.schema: advanced cross-platform GPU metrics

Each schema file contains a list of available metrics along with their descriptions (either a website link or in the file itself). Following is an example of a metric:
```JSON
  {
    "enabled": 1, // whether the metric should be displayed in the report, 0: disabled, 1: enabled
    "name": "% Time Shading Fragments", // name of the metric shown in the report
    "description": "Percentage of time spent shading fragments. Formula: Time spent on shading fragments / Total time spent on shading.", // description of the metric shown in the report
    "template": "{time_shading_fragments_percentage.value:f}" // data template, do not modify!
  },
```

#### Performing Analysis
There are two ways to analyze the performance of profiling sessions
##### **Generate Analysis Report**
 The result of a single session will be displayed on a local webpage.

1. Choose a **Profiling Data Directory** by clicking Browse to selecting a folder generated from running a session in *Running a session*, or copying the full path to the folder we saved in *Running a session* and paste it into the command text.
2. Click **Generate Analysis Report** button and then there will be an **analyze_report** folder generated in the **Profiling Data Directory**.The local webpage will show out.You can also open it in the **analyze_report** folder by clicking index.html later.
3. If the **Generate Analysis Report** button doesn't work, you can also click the **Copy Generate Analysis Command** button and try it on a command line terminal

##### **Generate Comparison Report**
 The results of two sessions will be compared and displayed on the same local webpage.

1. Choose a **Comparison Profiling Data Directory** by clicking Browse to selecting a folder generated from running a session in *Running a session*, or copying the full path to the folder we saved in *Running a session* and paste it into the command text.It will be compared with the Profiling Data Path we chose .
2. Click **Generate Comparison Report** button and then there will be a **comparison_report_{benchmark_session_directory_1}_{benchmark_session_directory_2}** folder generated in the **Profiling Data Directory**.The local webpage will show out.You can also open it in the **comparison_report_{benchmark_session_directory_1}_{benchmark_session_directory_2}** folder by clicking index.html later.
3. If the **Generate Comparison Report** button doesn't work, you can also click the **Copy Generate Comparison Command** button and try it on a command line terminal.

### Reading the Report
#### Header and Device Specification
Showing the session name, automation command queue id along with the hardware spec, rendering configurations of the device.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52254e64e9bd4657a2414af22a410b1a~tplv-goo7wpa0wc-image.image" width="3352px" />

#### Metrics
Displaying metric data plotted on graphs
Tabs on the left switch among available metrics configured in *Metrics Configuration*. Metrics name and session average are displayed on the tab.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2dc6accef1a2441ab53396c9f23e093a~tplv-goo7wpa0wc-image.image" width="1704px" />

#### **Screen Captures**
Displays captured screenshots. Captures with the same context will be grouped together. As shown below, two images are displayed side by side for comparison. The left one is the baseline, with the least number of rendering features turned on, while the right one with some additional features turned on.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc669a7f11654639a5a36ed0f2ff6b67~tplv-goo7wpa0wc-image.image" width="3190px" />

For the comparison report, the report differs in the following ways.

* Since two sessions may run on different devices, device specs of individual sessions are displayed side by side.
* If the same metric data is available from both sessions, they will be plotted on the same graph. The session average of both sessions will be displayed on the tab.
* Screen captures will be displayed side by side only if they share the same context and rendering feature status.

## Porting XR Profiling Toolkit to Another Project
To port the XR Profiling Toolkit to other Unity projects, follow these minimal steps:

1. Import the **XR Profiling ToolKit** package by **Window->Package Manager-> Add package from disk.** Or import from Unity Asset Store.
2. Go to the Unity editor menu, click and run **XR Profiling ToolKit->Shortcuts->Validate Provider Plugin (Meta\PICO):**
   * Note that running this menu command will automatically check other XR SDKs, specifically, from Meta and PICO, in the existing project, and feature-flag the code needed to support respective platforms.
3. Add the **CommandRunner.prefab** to the Scene by clicking **Add CommandRunner To Scene** button:
   * In the scene where you want to run the profiling, create an empty GameObject and attach the `CommandRunner.cs` script.
4. **Set up Command Queue:**
   * Follow the *Automated Test* section to create a command queue in your Unity project. Note that only a limited set of commands is supported, as some commands have dependencies on other systems. However, you can create new command types that suit your project’s needs by using the existing commands as a reference. See more details in *Configurations*.
5. **Build and deploy the project:**
   * Build and deploy your Unity project to install the apk file on your device. Then, you can follow the *Automated Test* section to run a profiling session and generate performance reports.

## Editor Menu Description
Below is a table detailing the Unity Editor Menu of the toolkit and the description for reference.
| **Editor Menu** | **Description** |
| --- | --- |
| Device Profiling Tool Window | The main Unity Editor Window interface for device profiling |
| ShortCuts->Add CommandRunner To Scene | The core prefab for running automatically with a pre-configured command sequence |
| ShortCuts->Validate Provider Plugin (Meta\PICO) | Switching and deploying to other platforms |
| ShortCuts->Add SceneLoader To Scene | Add the core prefab for using the **CommandLoadLevel** command |
| ShortCuts->Add FeatureManager To Scene | Add the core prefab for using the **CommandToggleFeature** command |
| ShortCuts->Copy ProfilingToolScripts folder To Assets | Useful shortcut to copy the profiling tool scripts and files from the Package folder to the Assets folder for ease of use |


# --- END: XR Profiling Toolkit.md ---

