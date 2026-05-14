# Graphics and Rendering

## Table of Contents
- Adaptive Resolution
- Anti-Aliasing
- Application SpaceWarp
- Buffer Discards Optimization
- Composition layer parameters
- Display Refresh Rate
- Enable supersampling, sharpening, and super resolution for composition layers
- General procedure for using compositor layers
- Late Latching
- Multiview Rendering
- Render Viewport Scaling
- Sharpening
- Super Resolution
- Universal Render Pipeline
- Use Blurred Quad layers
- Use EAC layers
- Use Equirect layers
- What's the maximum number of VR compositor layers supported_

---



# --- BEGIN: Adaptive Resolution.md ---

Adaptive resolution automatically adjusts the screen resolution based on the device's GPU workload, ensuring that the app can run at a stable frame rate. You can achieve higher image quality with increased resolution when GPU workload is low. Applications also achieve a more stable framerate when GPU workload is high by automatically decreasing resolution. You can enable adaptive resolution for your app, set a desired resolution bound and power consumption mode.
## Requirements

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series
* PICO device's system version: 5.7.0 or later

## Enable adaptive resolution

1. Open a scene or create a new scene in the Unity Editor.
2. In the **Hierarchy** window, click **+** > **XR** > **XR Origin (VR)** to add **XR Origin**.
3. Select the main camera object in the scene.
4. In the **Inspector** window, click the **Add Component** button, and add the **PXR_Manager** script to the main camera object.
5. On the **PXR_Manager (Script)** pane, check the **Adaptive Resolution** checkbox.
   The pane shows adaptive resolution-related fields.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59edd27e89b04b99a9c98e99db329e1c~tplv-goo7wpa0wc-image.image)
6. Set a resolution bound:
   1. In the **Min Adaptive Resolution Scale** field, set the minimum rendering resolution for the app, ranging from 0.7 to 1.3, with a default value of 0.7.
   2. In the **Max Adaptive Resolution Scale** field, set the maximum rendering resolution for the app, ranging from 0.7 to 1.3, with a default value of 1.26.
   The default resolution is 1504x1504. To calculate the adaptive resolution, multiply 1504 by the resolution scale you set. For example, 1504 multiplied by 0.7 is approximately 1100, 1504 multiplied by 1.26 is approximately 1900.

7. Select a **Power Setting** mode to optimize for higher resolution vs. lower power consumption.
   | **Option** | **Description** |
   | --- | --- |
   | HIGH_QUALITY | Optimizes for higher resolution, which in turn increases power consumption. |
   | BALANCED | Balances resolution with power consumption. |
   | BATTERY_SAVING | Optimizes for power consumption, which in turn decreases resolution. |

## Demo
The AdaptiveResolution demo shows the change of resolution with the change of GPU load. For more information, refer to the "[Adaptive resolution demo](/en_adaptive-resolution-demo)" article.
## About render viewport scaling
Render viewport scale controls the proportion of the allocated eye texture that should be used for rendering. The larger the scale, the more proportion of eye texture will be used for rendering, resulting in a better image quality. Render viewport scale can be modified at runtime without reallocating eye textures. Therefore, modifying the render viewport scale can dynamically change the eye render resolution. For more information, refer to the "[Render viewport scaling](/en_render-viewport-scaling)" guide.
## Known issues
When using URP with Adaptive Resolution, the URP’s pipelineAsset.renderScale will overwrite the max adaptive resolution scale. This issue will be fixed in a future version of the SDK.


# --- END: Adaptive Resolution.md ---



# --- BEGIN: Anti-Aliasing.md ---

The edges of objects in low-resolution scenes usually appear jagged, which can cause visual discomfort and lead to an unpleasant app experience. You can use the multisampling anti-aliasing (MSAA) feature to smooth the jagged edges of objects. MSAA samples the jagged areas and then surrounds them with intermediate shades of color, thereby making the lines appear much smoother. A higher MSAA level enhances the image quality while causing a decline in app performance. 
## Different MSAA levels
From left to right: none, 2x MSAA, 4x MSAA, 8x MSAA.
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e65f94a747dd4c75974452ba87c2e87f~tplv-em5hxbkur4-noop.image?width=1566&height=417)
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e48fc1b0b818404fbef4410b0c5df64a~tplv-em5hxbkur4-noop.image?width=1554&height=414)
## Use the recommended MASS level
Currently, the default recommended MASS level is **4x** which you can use in your project. 

1. Open your project in the Unity Editor.
2. In the **Hierarchy** window, click **+** > **XR** > **XR Origin (VR)**.
3. Select **XR Origin**.
   The scripts and components mounted by the XR Origin are then displayed in the Inspector window.
4. Click **Add Component** at the bottom of the **Inspector** window.
5. Search for the **PXR_Manager** script and double click to add it.
   The PXR_Manager pane appears as below:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/aa17c3d5aeed480e9cea960d5bf51ef4~tplv-em5hxbkur4-noop.image?width=856&height=308)
6. Check **Use Recommended MSAA**. This is typically the default setting.

## Use other MSAA levels
If you do not want to use the recommended MSAA level, you can set another level. 

1. In the **PXR_Manager** pane, uncheck **Use Recommended MSAA**.
2. From the top menu bar, select **Edit** > **Project Settings**.
   The Project Settings window appears.
3. From the left navigation pane, select **Quality**.
4. Under **Rendering** , set **Anti Aliasing**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/b5f26306d87447b08195729a55681e84~tplv-em5hxbkur4-noop.image?width=1423&height=987)


# --- END: Anti-Aliasing.md ---



# --- BEGIN: Application SpaceWarp.md ---

Application SpaceWarp (AppSW) can greatly bring down rendering latency and therefore enhance app performance by unleashing extra computational power for your app.
## Tech overview
Using AppSW, PICO apps are capable of rendering images at half the screen's actual refresh rate without lowering the image quality. For example, your app renders images at 36 FPS but can still result in an output of 72 FPS to the display. To achieve this effect, the app needs to provide the motion vector buffer and the depth buffer in addition to the eye buffer for frame synthesis.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/300ff2f1423e46f2a6f571b3bf15f150~tplv-goo7wpa0wc-image.image" width="546px" />

Below are the descriptions of the aforementioned key concepts:
| **Concept** | **Description** |
| --- | --- |
| Eye buffer | In the process of 3D graphic rendering on VR devices, the eye buffer plays an intermediary role. As the system renders the standard view of each eye into the eye buffer, it can then provide the eye buffer as a rendering texture to the ATW thread for distortion and sampling.  |
| Motion vector buffer | Motion vectors record the velocity of each moving pixel, which is used to track the amount of movement of pixels in both the screen space and the depth buffer, helping predict where the pixel is in the near future. |
| Depth buffer | The depth buffer records the distance between each pixel and the rendering camera, which can be used to perform reprojection to reduce HMD latency. |
| Frame synthesis | A process of synthesizing new frames using the rendered buffers, which is done by the PICO system. |
## Requirements
Make sure to meet the following development environment requirements before using AppSW:

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series
* PICO device's system version: 5.4.0 or later
* Unity Editor: 2021 LTS or later (Unity 2021 is recommended, as there may be compatibility issues with Unity 2022 and 2023 when using AppSW)

For Unity 6 or a higher version, the following requirements should also be met:

* URP: 17.0.3 or later
* Render Graph: **Compatibility Mode (Render Graph Disabled)** is enabled
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1852a67a0632443b910b81949b37909b~tplv-goo7wpa0wc-image.image)

## Use AppSW
### Step 1: Set the rendering mode
Go to **Edit** > **Project Settings** > **XR Plug-in Management** > **PICO**, then set **Stereo Rendering Mode** to **Multiview**.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a310d74cec145aeb013d22ef0f928ce~tplv-goo7wpa0wc-image.image)
### Step 2: Import the URP that generates the motion vector
Use the following steps to import the URP that can generate the motion vector in your project.

1. Clone the [Unity-Graphics](https://github.com/Pico-Developer/Unity-Graphics/tree/AppSpacewarpForUnity) repository.
2. Use command `git checkout “AppSpacewarpForUnity”` to check out the target branch.
3. Open your project in the Unity Editor.
4. Go to **Window** > **Package Manager** > **+** > **Add package from disk**, and import the three **package.json** files provided in the following three folders into your project. 
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1200ca4e72a34a6c996b762d0ab5023a~tplv-goo7wpa0wc-image.image)
   Once imported, the Core RP Library, Shader Graph, and Universal RP appear under the Custom directory in the Package Manager.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/907fe177612d45c2b84550f306f51f6b~tplv-goo7wpa0wc-image.image)
   | **Resource** | **Description** |
   | --- | --- |
   | Core RP Library | SRP Core contains reusable code, including boilerplate code for working with platform-specific graphics APIs, utility functions for common rendering operations, and shader libraries. If you are going to create a custom SRP from scratch or customize a prebuilt SRP, using SRP Core can save you time. |
   | Shader Graph | The Shader Graph package adds a visual shader-editing tool to the Unity Editor. You can use this tool to create shaders in a visual way instead of writing code. You can use this resource if you want to edit shaders.  |
   | Universal RP | The Universal Render Pipeline (URP) is a prebuilt Scriptable Render Pipeline made by Unity. You can use the URP to quickly and easily create optimized graphics. |

### Step 3: Enable the URP
To enable the URP you just imported, you need to complete the following tasks, including creating the URP asset, adding the URP asset to graphics settings, disabling HDR, and upgrading project materials. For detailed instructions, refer to [this article](/13136/en_universal-render-pipeline).
### Step 4: Replace shaders
Replace the default shaders of dynamic objects in the scene with URP shaders that can generate motion vectors. You can use the standard URP shader provided by the Unity-Graphics repository, which is "com.unity.render-pipelines.universal/Shaders/Lit.shader", or refer to that shader for modification.
### Step 5: Set Graphics API to Vulkan
Before enabling AppSW for your app, you need to complete Player settings. Below are the steps to follow:

1. Go to **Edit** > **Project Settings** > **Player** > **Other Settings** > **Rendering**.
2. In **Graphics API**, add **Vulkan** and move it up to the top of the list.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/427bc427ab9c4b04b9182d0f3de190be~tplv-goo7wpa0wc-image.image)

### Step 6: Enable AppSW for your app
After completing Player settings, use the following steps to enable AppSW for your app:

1. Go to **Edit** > **Project Settings** > **XR Plug-in Management** > **PICO** > **Android Settings**.
2. Check **Application SpaceWarp**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/477389269b1f49ab82f7ce18e425048c~tplv-goo7wpa0wc-image.image)
3. Add **XR Origin** to the scene and then add the **PXR_Manager** script to XR Origin. Skip this step if you have done it before.
4. Create a new script and call `PXR_Manager.Instance.SetSpaceWarp` in the `Start` section.
   Enable AppSW:
   ```C#
   void Start()
   {
       PXR_Manager.Instance.SetSpaceWarp(true);
   }
   ```

   Disable AppSW:
   ```C#
   void Start()
   {
       PXR_Manager.Instance.SetSpaceWarp(false);
   }
   ```

5. Add the script to the scene. For example, you can add the script to XR Origin.

### Step 7: Check AppSW status
You can check your app's current frame rate and whether AppSW is successfully enabled or not through PxrMetric log output. Below is an example log:
```Plain Text
xxx/com.pico.xxx I/PxrMetric: FPS=36/72,MTP=40.60ms,AppSW=on,FrmEarly=0,FrmLate=0,FrmCpu=2.33ms,FrmGpu=7.16ms,FrmTime=9.50ms,VsyncDelay=1,GPU=43%/441Mhz,GPUTemp=55.2C,LayerCnt=3
```

## Compositor layer AppSW
If you would like to deal with in-app UIs with independently-rendered compositor layers, you can enable AppSW to make the layers' movements smoother, and this effect is not limited by the framerate. In addition, as these layers are independently displayed, you can set them to be transparent for handling transparent UIs.
## Troubleshooting
You may come across the following rendering issues when using AppSW:

* If the scene's background is very simple and clean, and contains elements such as straight lines, grids, etc., AppSW may cause graphic distortion such as distorted straight lines as shown below. To resolve distortion, you can keep debugging and adjusting the background accordingly until reaching the desired effect.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eefc9056106e416fb48fb5a9457ed789~tplv-goo7wpa0wc-image.image" width="216px" />

* If the scene contains objects that rotate at high speeds, distortion artifacts may appear around the objects when AppSW is enabled. You can mitigate this issue by reducing the objects' rotation speeds.
* Using AppSW and [Optimize Buffer Discards](/en_/optimize-buffer-discards) together can cause screen tearing. This is because AppSW needs to process the depth buffer, and when Optimize Buffer Discards is enabled, the contents of the depth buffer will be discarded.

## FAQs

* **Do I have to enable late latching while using AppSW?**
   Late latching can reduce latency. It is recommended that you enable late latching for your app while using AppSW, but this is not a required option.
* **Does AppSW support OpenXR development?**
   Yes.
* **Do I need to always enable AppSW for my app?**
   Not necessarily. You can enable or disable AppSW for your app at any time according to actual needs.

## Known issue
Using AppSW and [content protection](/13136/content-protection) together will cause screen jitter and screen ghosting.
## Recommended content
**Late latching** is a technique that reduces the **motion-to-photon latency** (MTP latancy). During the image transmission process, late latching can remove 1 frame of latency in HMD and controller poses. Therefore, if you want to improve rendering quality and reduce as much latency as possible at the same time, you can enable late latching for your app. For more information on late latching, refer to [this article](/13136/en_late-latching).


# --- END: Application SpaceWarp.md ---



# --- BEGIN: Buffer Discards Optimization.md ---

Buffer Discards Optimization is a technique used to improve app performance. If enabled, the depth buffer contents are discarded instead of being resolved, and the MSAA color buffer is resolved instead of being stored after rendering.
## Requirements

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series
* PICO device's system version: 5.3.0 or later
* Graphics API: Vulkan

## Enable buffer discards optimization

1. In the Unity Editor, open an existing scene or create a new scene.
2. Go to **Edit** > **Project** **Settings** > **XR Plug-in Management** > **PICO** > **Android settings**.
3. Check the **Optimize Buffer Discards (Vulkan)** checkbox.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99c081545ace44e2a7ab70f54cbee7fc~tplv-goo7wpa0wc-image.image)


# --- END: Buffer Discards Optimization.md ---



# --- BEGIN: Composition layer parameters.md ---

The PXR_Composition Layer component is used to configure compositor layer-related parameters. The PXR_Manager component also provides some compositor layer-related parameters.
## Parameters in the PXR_Composition Layer component
### Type
The SDK provides two types of compositor layers: Overlay and Underlay. Below are detailed descriptions:
| **Type** | **Description** |
| --- | --- |
| Overlay | The overlay texture is displayed in front of the eye buffer.  <br> If you want to use overlay textures, pay attention to the following:  <br>  <br> * If you would like to customize "Source Rects" and "Destination Rects" related parameters in "Texture Rects", make sure that the values of the "X", "Y", "W", and "H" parameters are within the following required ranges: <br>    * X: [0,1) <br>    * Y: [0,1) <br>    * W: (0,1] <br>    * H: (0,1] <br> * If you set the Shape parameter to Equirect, pay attention to the following: <br>    * The "Radius" parameter is used to specify the radius of a cylinder. When set to 0 or positive infinity (1.0f/0.0f), it represents an infinitely large radius. When the spherical radius is infinitely large, its visual effect is similar to the skybox in an empty scene. <br>    * The "X" parameter under "Destination Rects" is useless. The "W" parameter is mapped to the central angle and is symmetric with respect to the center point coordinates (0, 0). |
| Underlay | Underlay textures are displayed behind the eye buffer. <br> Underlay textures rely on the alpha channel of the rendering target. After all the objects have been drawn behind the eye buffer, you need to hollow out an area on the eye buffer to display the Underlay textures behind it. You can go to Packages/PICO Integration/Assets/Resources/Shader to get the `PXR_SDK / PXR_UnderlayHole` script or write your own shaders to hollow out an area. <br> ***Note***: If you are using the Universal Render Pipeline (URP) in your project, and you need to use underlay layers at the same time, you must disable HDR. Otherwise, the underlay layers will not work. |
### Shape
The SDK provides five shapes of compositor layers: quad, cylinder, equirect, cubemap, and equi-angular cubemap. Below are detailed descriptions:
| **Shape** | **Description** |
| --- | --- |
| Quad | A flat texture with four vertices, which is normally used to display text or information. |
| Cylinder | A texture with cylindrical curves, which is normally used to display curved UI. If you use this shape: <br>  <br> * The center of the Transform component is the center of the cylinder. The scale of the Transform component is the scale of the cylinder, and the Transform component's scales for the cylinder are all global scales. Specifically, X is the radius of the cylinder, Y is the height of the cylinder, and X/Z is the arc length of the cylinder. <br> * When using the Cylinder texture, you must put the camera inside the inscribed sphere of the cylinder. Then you can adjust the distance between the camera and the sphere as overlay textures will not be displayed if the camera is too close to the surface of the inscribed sphere. |
| Equirect | Sphere texture, which is normally used to display 180/360 panoramic images or videos. |
| Cubemap | A cubemap consists of six square textures that represent the reflections on an environment. The six square textures form the faces of an imaginary cube that surrounds an object, and each face represents the view along a specific direction of the world axes, including up, down, left, right, front, and back. |
| Equi-Angular Cubemap | Equi-Angular Cubemap (EAC) is a projection technique used to display 360-degree panoramic images or videos. It is a hybrid of two other projection techniques: the equidistant projection and the cubemap projection. EAC supports 180-degree projection. <br> In an EAC projection, the 360-degree panorama is first divided into six cube faces, then equidistant projection is used to map the pixels from each cube face onto a sphere. This creates a seamless panoramic image that can be viewed from any angle. |
| Blurred Quad | Blurred quad layers are used to render spatial pictures or spatial videos. |
### Depth
The **Depth** parameter determines the order of layer composition. The layer with a smaller depth is composited in front of the layer with a larger depth. For example, the depth of a scene with multiple overlays and underlays can be as follows:
`[Camera](Overlay)2/1/0[EyeBuffer]0/1/2(Underlay)`
### Texture type
The SDK provides three texture types: External Surface, Dynamic Texture, and Static Texture. Below are detailed descriptions:
| **Type** | **Description** |
| --- | --- |
| External Surface | A layer's texture will be obtained from an external Android surface, for example, the video texture from an Android player. The texture from the external Android surface will be directly rendered to the VR compositor layer. The object created is `public IntPtr externalAndroidSurfaceObject = IntPtr.Zero;`, which can be found in the PXR_OverLay.cs file. <br> If you want to improve video quality, external surfaces are recommended. |
| Dynamic Texture | If you want to render dynamic content to the layer, in other words, to refresh the texture at each frame, you can use dynamic layers. For example, if you want to generate RenderTexture images with normal cameras, you need to use dynamic textures. |
| Static Texture | You can use static texture to render static content, such as a painting in the gallery. |
### Texture
The **Texture** parameter is used to specify the textures to be displayed through the left and right eyes perspectively.
You must specify the same texture with the same height and width for the left-eye and right-eye cameras. However, if you want to display 3D effects, you can specify two different textures.

### Radius
When you set the **Shape** parameter to **Equirect**, you need to specify the cylinder's radius through the **Radius** parameter.
### Texture Rects
After checking the **Texture Rects** checkbox, you can continue to configure Source Rects and Destination Rects related parameters.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adb1fee141454aed913634c58ee15049~tplv-goo7wpa0wc-image.image)
#### Source Rects
In the **Source Rects** parameter, customize the texture to be rendered on the object's surface. Below are available options:
| **Option** | **Description** |
| --- | --- |
| Mono Scopic | If you want to display two different textures on the left-eye and right-eye cameras respectively, you can select this option. |
| Stereo Scopic | Vertically split the image from the center. The left part will be displayed on the left-eye camera, and the right part will be displayed on the right-eye camera. <br> ***Note***: It is recommended that you specify the same texture with the same height and width for the left-eye and right-eye cameras. Otherwise, the left-eye and right-eye textures can be too different and lead to discomfort. |
| Custom | You can set which area of the texture is to be rendered on the object's surface. Specifically: <br>  <br>    * **X** and **Y** are for setting an origin on the texture where the rendering area starts <br>    * **W** is for setting the width of the texture area <br>    * **H** is for setting the height of the texture area <br>  <br> For example, if you set both **X** and **Y** to **0.5** and set both **W** and **H** to **0.5**, the rendering area starts from the center of the texture and 1/4 upper-right area of the texture will be rendered on the object's surface. |
#### Destination Rects
In the **Destination Rects** parameter, set which area of the object's surface is to be covered by the texture. Below are available options:
| **Option** | **Description** |
| --- | --- |
| Default | Keep the original size of the object's surface. |
| Custom | You can set which area of the object's surface is to be covered by the texture: <br>  <br>    * **X** and **Y** are for setting the origin on the object's surface where the to-be-rendered area starts. <br>    * **W** is for setting the width of the to-be-rendered area. <br>    * **H** is for setting the height of the to-be-rendered area. <br>  <br> For example, if you set both **X** and **Y** to **0.5** and set both **W** and **H** to **0.5** for the texture in **Source Rects**, and set both **X** and **Y** to **0.5** and set both **W** and **H** to **1** here, 1/4 upper-right area of the object's surface will be covered by1/4 upper-right area of the texture. |
### Layer Blend
**Layer Blend** is used to set the color and alpha value for the source and destination layers.
Layer blending can blend the colors of the source layer and the destination layer, which is often used to render transparent or semi-transparent objects. By default, compositor layers are blended from back to front. If there are layers 1, 2, 3, and 4 in the scene, the layers will be blended in the following order:

1. Layers 4 and 3 are blended to generate destination layer 1. Layer 2 becomes the source layer.
2. Destination layer 1 is blended with layer 2 to generate destination layer 2. Layer 1 becomes the source layer.
3. Destination layer 2 is blended with layer 1.

![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/7e27cc19105d42dab1248c646227f391~tplv-em5hxbkur4-noop.image?width=789&height=237)
Below are parameter descriptions:
| **Parameter** | **Description** |
| --- | --- |
| Src Color | For setting the color value of the source layer. |
| Dst Color | For setting the color value of the destination layer. |
| Src Alpha | For setting the alpha value of the source layer. |
| Dst Alpha | For setting the alpha value of the destination layer. |
* The final color = (srcColor × LayerBlend.srcColor) + (dstColor × dst.layerBlend)
* The final alpha = (srcColor × LayerBlend.srcAlpha) + (dstColor × dst.dstAlpha)

### Override Color Scale
If you want to globally override the layer's color settings, check the **Override Color Scale** checkbox and configure the following parameters:
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/91818027d8204541bca2999dbba5ff10~tplv-em5hxbkur4-noop.image?width=792&height=152)
Below are parameter descriptions:
| **Parameter** | **Description** |
| --- | --- |
| Scale | Set the color scale. |
| Offset | Set the color offset. |
X, Y, Z, and W respectively correspond to the R, G, B, and A of the color channel. The final color=(original color×scale)+offset.

### More about external surfaces
When using external surfaces, you can configure the following parameters if needed:
![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/b03f027082464f7c815cbc932e89d986~tplv-em5hxbkur4-noop.image?width=783&height=104)
Below are parameter descriptions:
| **Parameter** | **Description** |
| --- | --- |
| DRM | For protecting the copyright of external textures. Once enabled, external surfaces will become black when users capture or record the screen. |
| 3D Surface Type | For determining how to display the texture: <br>  <br> * **Single**: The complete image will be displayed on both the left-eye and right-eye cameras. <br> * **Left Right**: The image will be vertically split from the center. The left part will be displayed on the left-eye camera, and the right part will be displayed on the right-eye camera. <br> * **Top Bottom**: The image will be horizontally split from the center. The top part will be displayed on the left-eye camera, and the bottom part will be displayed on the right-eye camera. |
## Parameters in the PXR_Manager component
### Use Premultiplied Alpha
Enable the premultiplied alpha effect to multiply the RGB color channels by the alpha value, that is, `(R×A, G×A, B×A)`. This is recommended for the following scenarios:

*  UI interfaces with transparency or particle effects。
*  Materials using alpha blending or content with frequent transparency blending。

###  Layer Blend
**Layer Blend** is used to set the color and alpha value for the source and destination layers.
Layer blending can blend the colors of the source layer and the destination layer, which is often used to render transparent or semi-transparent objects. By default, compositor layers are blended from back to front. If there are layers 1, 2, 3, and 4 in the scene, the layers will be blended in the following order:

1. Layers 4 and 3 are blended to generate destination layer 1. Layer 2 becomes the source layer.
2. Destination layer 1 is blended with layer 2 to generate destination layer 2. Layer 1 becomes the source layer.
3. Destination layer 2 is blended with layer 1.

![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/7e27cc19105d42dab1248c646227f391~tplv-em5hxbkur4-noop.image?width=789&height=237)
Below are parameter descriptions:
| **Parameter** | **Description** |
| --- | --- |
| Src Color | For setting the color value of the source layer. |
| Dst Color | For setting the color value of the destination layer. |
| Src Alpha | For setting the alpha value of the source layer. |
| Dst Alpha | For setting the alpha value of the destination layer. |
* The final color = (srcColor × LayerBlend.srcColor) + (dstColor × dst.layerBlend)
* The final alpha = (srcColor × LayerBlend.srcAlpha) + (dstColor × dst.dstAlpha)


# --- END: Composition layer parameters.md ---



# --- BEGIN: Display Refresh Rate.md ---

Display refresh rates control the times that a headset's screen refreshes per second and therefore affect the quality of the image displayed to users. A higher refresh rate enables better image quality. In general, the display refresh rate should be 75 Hz or higher, thereby making human eyes unlikely to feel screen flickering.
## Considerations

* ***Low*** display refresh rates may cause frame drops, display lag, screen tearing, latency, and more other problems, which hugely affects the app experience.
   The default display refresh rate for PICO apps is 72 Hz. Yon can set a higher refresh rate for your app if needed. For example, racing games usually require high display refresh rates to ensure screen smoothness.
* ***High*** display refresh rates may affect your app's performance. Therefore, if you want to set a high display refresh rate for your app, you must ensure that it is able to sustain that rate. In the debugging process, you can use relevant tools to monitor your app's performance at the high display refresh rate and make in-time adjustments if necessary. See [this article](/13136/en_performance-monitoring-and-analysis) for details.
* ***High*** display refresh rates may reduce the life of the device.

## Set a display refresh rate

1. Open your project in the Unity Editor.
2. From the top menu bar, select **Edit** > **Project Settings**.
3. In the **Project Settings** window, click **PICO** > **Android settings icon**.
4. Set **Display Refresh Rates**.
   | **Refresh Rate** | **Description** |
   | --- | --- |
   | Default | Default refresh rate, which is 72 Hz. <br> ***Note***: The default refresh rate might change with SDK version upgrade. |
   | Refresh Rate 72 | 72 Hz. |
   | Refresh Rate 90 | (Recommended) 90 Hz. |
   | Refresh Rate 120 | 120 Hz. |
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c1024126be364de490831c44a2ea3b74~tplv-em5hxbkur4-noop.image?width=1401&height=1002)


# --- END: Display Refresh Rate.md ---



# --- BEGIN: Enable supersampling, sharpening, and super resolution for composition layers.md ---

Using Supersampling, Sharpening, and Super Resolution can optimize the rendering effect of composition layers. You can set up them as needed.
## Limitations

* For a composition layer, you can only enable one of the Supersampling, Sharpening, or Super Resolution capabilities for it. 
* When dynamically setting composition layers, if you enable Supersampling, Sharpening, and Super Resolution for a layer simultaneously, only Supersampling will take effect.

## Supersampling
Supersampling supports sampling data at a higher resolution than that of your PICO device, which helps reduce jagged edges in images. You can use the following steps to enable Supersampling for a composition layer:

1. Open your project in the Unity Editor.
2. In the **Hierarchy** window, add an empty object.
3. In the **Inspector** window, add the **PXR_Composition Layer (Script)** component to the empty object.
4. On the **PXR_Composition Layer (Script)** panel, select the **Supersampling Mode**.
   Below are the available options:
   | **Mode** | **Description** |
   | --- | --- |
   | None | Disable the Supersampling mode. |
   | Normal | Normal mode.  <br> In this mode,  supersampling a pixel requires sampling its 2 surrounding pixels, resulting in a total of 3 sampling operations. Compared to the Quality mode, this mode has lower power consumption but a reduced sharpening effect. |
   | Quality | High-quality mode. <br> In this mode, supersampling a pixel requires sampling its 4 surrounding pixels, resulting in a total of 5 sampling operations. Compared to the Normal mode, this mode has a better sharpening effect but a higher power consumption. |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5596b7e8ac844e9095cbbf3fda25b3a9~tplv-goo7wpa0wc-image.image)
5. Select the **Supersampling Enhance Mode** to further improve the subsampling effect.
   * Supersampling Enhance Mode is available only if Supersampling Mode is set to Normal or Quality.
   * This parameter is not available for Blurred Quad layers.

   Below are the available options:
   | **Mode** | **Description** |
   | --- | --- |
   | None  | Do not enable supersampling enhancement. |
   | Fixed Foveated  | Fixed-foveated supersampling. When this mode is enabled, the app only supersamples the pixels in the user's central gaze area while leaving the pixels in the surrounding regions unsupersampled. |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/139cb775b9254595a88d70c531c5869f~tplv-goo7wpa0wc-image.image)

## Sharpening
Sharpening is an image processing technique that enhances high-frequency information within an image, improves the edges and contours of the image.
### Tech summary
PICO SDK's sharpening capability is built on a differentiation-based spatial filtering algorithm. This algorithm determines the degree of sharpening for a given pixel based on the color contrast between the given pixel and its surrounding pixels. In general, the smaller the color difference between the given pixel and its surrounding pixels, the smaller the sharpening degree, and vice versa. The following image illustrates the contrast before and after applying sharpening.
### Considerations

* Sharpening increases the number of samplings and computational workload, which may lead to an increase in GPU power consumption.
* Sharpening could potentially make image noise or moiré patterns more pronounced.

### Enabel Sharpening for a composition layer

1. Open your project in the Unity Editor.
2. In the **Hierarchy** window, add an empty object.
3. In the **Inspector** window, add the **PXR_Composition Layer (Script)** component to the empty object.
4. On the **PXR_Composition Layer (Script)** panel, select the **Sharpening Mode**.
   Below are the available options:
   | **Mode** | **Description** |
   | --- | --- |
   | None | Do not enable sharpening. |
   | Normal | Normal sharpening.  <br> In this mode, sharpening a pixel requires sampling its 2 surrounding pixels, resulting in a total of 3 sampling operations. Compared to the Quality mode, this mode has lower power consumption but a reduced sharpening effect. |
   | Quality | High-quality sharpening. <br> In this mode, sharpening a pixel requires sampling its 4 surrounding pixels, resulting in a total of 5 sampling operations. Compared to the Normal mode, this mode has a better sharpening effect but a higher power consumption. |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c4b9cace3ec4cda802ecb937671c67e~tplv-goo7wpa0wc-image.image)
5. Select the **Sharpening Enhance Mode** to further enhance the effectiveness of sharpening.
   * Sharpening Enhance Mode is available only if Sharpening Mode is set to Normal or Quality. 
   * This parameter is not available for Blurred Quad layers.

   Below are the available options:
   | **Mode** | **Desciption** |
   | --- | --- |
   | None | Do not enable sharpening enhancement. |
   | Fixed Foveated | Fixed foveated sharpening. When this mode is enabled, the app only sharpens the pixels in the user's central gaze area while leaving the pixels in the surrounding regions unsharpened. |
   | Self Adaptive | Self-adaptive sharpening. When this mode is enabled, the app only sharpens the pixels with color contrast exceeding a certain threshold in the area, thereby reducing the number of pixels to sharpen and lowering power consumption. |
   | Both | To simultaneously enable fixed foveated sharpening and self-adaptive sharpening. |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7c1bfc9ad8e43ffb7a6ce2a627067ea~tplv-goo7wpa0wc-image.image)

## Super Resolution
Super resolution refers to the technique of enhancing the resolution of an image from low-resolution (LR) to high-resolution (HR). It uses some specific algorithms that leverages known image information to retrieve and supplement image details and additional data, enhancing image clarity for your app.
### Recommendations
Take PICO 4 series devices as an example. They have a screen display resolution of 4320 × 2160 pixels, but to balance power consumption and performance, the default rendering resolution (eye buffer) is set to 1504 x 1504 pixels. As a result, your app typically renders at a resolution lower than the device's native resolution. In situations with constrained performance, enabling super resolution can deliver an improved visual experience to users.
However, it is not advisable to enable super resolution when your app's actual rendering resolution is already lower than the default rendering resolution, as using super resolution at this time can make image noise more pronounced. Furthermore, as the eye buffer resolution gradually approaches the device screen's native display resolution, the effectiveness of super resolution will gradually diminish.
Compared to directly increasing the eye buffer resolution, the GPU resources consumed by super resolution are relatively fixed. In scenarios with lower GPU loads, you may choose to directly increase the Eye Buffer resolution. Still, in scenarios with heavier GPU loads, it is recommended to use super resolution to more reasonably allocate GPU resources.
### Considerations 
Super resolution increases the GPU load on the compositor service. Enabling super resolution for three or more layers may result in resource constraints on the compositor service, leading to screen tearing. Therefore, the SDK automatically disables super resolution when the GPU load is excessive and re-enables it once the GPU load returns to normal.
### Enable Super Resolution for a composition layer

1. Open your project in the Unity Editor.
2. In the **Hierarchy** window, add an empty object.
3. In the **Inspector** window, add the **PXR_Composition Layer (Script)** component to the empty object.
4. On the **PXR_Composition Layer (Script)** panel, check the **Super Resolution** checkbox.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/308ce38c07b543c2b726d3b168f9f91d~tplv-goo7wpa0wc-image.image)


# --- END: Enable supersampling, sharpening, and super resolution for composition layers.md ---



# --- BEGIN: General procedure for using compositor layers.md ---

This part walks you through how to add a world-locked or head-locked Quad layer. The layer type referenced here is **Overlay**.
### Expected effects

* **World-locked layers**
   In general, compositor layers are world-locked. No matter how the HMD moves, the layer is fixed in its given position in this world.
   <video src=https://sf3-cdn-tos.huoshanstatic.com/obj/vcloud/b62da208791e641b2e40ee79f29f1b67-.mp4></video>
* **Head-locked layers**
   A head-locked layer moves with the HMD. To make this happen, you need to add a layer as the child of the camera.
   <video src=https://sf6-cdn-tos.huoshanstatic.com/obj/vcloud/ef26264b0d092af8d892a1bd65cd554a-.mp4></video>

### Use world-locked layers
**Firstly**, add an XR Origin and add the PXR_Manager script to it. Below are the steps to follow:

1. Open your project in the Unity Editor.
2. In the **Hierarchy** window, click **+** > **XR** > **XR Origin (VR)**.
   The XR Origin is then added to the scene. The Main Camera under it becomes the camera for capturing the content by default. If you have not upgraded the XR Interaction Toolkit to the latest version, the object name will be XR Rig. Refer to the [Quickstart](/13136/en_create-an-xr-scene#782faf9d) guide for how to upgrade the XR Interaction Toolkit.
3. Select the **Main Camera** under XR Origin/Camera Offset.
4. In the **Inspector** window, set **Tag** to **MainCamera**. This is typically the default setting.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/278cbc3c20bb4c718625f4c0bdd1a5de~tplv-em5hxbkur4-noop.image?width=718&height=147)
5. Delete the **Main Camera**, which is added by default after creating the project.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e6282694d3634fb6aac2b3652e5a14bd~tplv-em5hxbkur4-noop.image?width=598&height=436)
6. Select **XR Origin**.
   The scripts and components for configuring the XR Origin are then displayed in the Inspector window.
7. Click **Add Component** at the bottom of the **Inspector** window.
8. Search for the **PXR_Manager** script and double-click to add it.

**Secondly**, add a 3D object and add the PXR_Composition Layer script to it. This script is used to configure layer settings. Below are the steps to follow:

1. From the top menu bar, select **GameObject** > **3D Object**.
2. Create a 3D object, for example, Cube.
3. Adjust the cube's position to make it visible to the camera.
4. In the **Hierarchy** window, select this 3D object.
   The scripts and components for configuring this 3D object are then displayed in the Inspector window.
5. Click **Add Component** at the bottom of the **Inspector** window.
6. Search for the **PXR_Over Lay** script and double-click to add it.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/7ceba2035cc1404eb9e59f51b2220683~tplv-em5hxbkur4-noop.image?width=813&height=600)

**Thirdly**, configure basic layer settings. Below are the steps to follow:

1. Set **Type** to **Overlay**.
2. Set **Shape** to **Quad**.
3. Set **Depth** to **0**.

**Finally**, select a texture type and configure parameters:

1. Set **Texture Type** to **Dynamic Texture** or **Static Texture**.
   The **PXR_Composition Layer (Script)** panel is changed to the following:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e10f14f6c50c4398814a8a48fe33638f~tplv-em5hxbkur4-noop.image?width=813&height=730)
2. In the **Texture** parameter, select a texture to be displayed on the left-eye and right-eye cameras.
   You have completed basic layer settings. You can then run the scene on your PICO VR headset to experience the expected effect. If you have further needs, you can proceed with the following steps:
3. (Optional) Check the **Texture Rects** checkbox and configure Source Rects and Destination Rects related parameters.
4. (Optional) Check the **Layer Blend** checkbox, then set the color and alpha value for the source and destination layers.
5. (Optional) If you want to globally override the layer's color settings, check the **Override Color Scale** checkbox and configure related parameters.

### Use head-locked layers

1. In the **Hierarchy** window, expand **XR Origin** (or XR Rig) > **Camera Offset**.
2. Right-click **Main Camera** and add a 3D object (for example, a cube) to it.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/45e0142a583f42c5bd8e3a6cf1612e94~tplv-em5hxbkur4-noop.image?width=598&height=433)
3. Adjust the cube's position to make it visible to the camera.
4. Select **Cube**.
5. Click **Add Component** at the bottom of the **Inspector** window.
6. Search for the **PXR_Compostion Layer** script and double-click to add it.
7. Configure basic layer settings and set the texture.


# --- END: General procedure for using compositor layers.md ---



# --- BEGIN: Late Latching.md ---

**Late latching** is a technique that reduces the **motion-to-photon latency** (MTP latency). MTP latency refers to the entire duration from the time the user starts moving to the corresponding image changes to be mapped on the display. During the image transmission process, late latching can remove 1 frame of latency in HMD and controller poses. Therefore, if you want to improve rendering quality and reduce as much latency as possible at the same time, you can enable late latching for your app.
## Requirements

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series
* PICO device's system version: 5.6.0 or later

## Tech summary
Late latching reduces MTP latency by providing the GPU with the HMD and controller motion inputs at the very last moment before the start of rendering.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9250796dad664807a5cba91012e8312a~tplv-goo7wpa0wc-image.image" width="390px" />

## Benefits
Late latching can bring your app the following improvements:

* Reduce direction prediction latency, thereby mitigating the shadows caused by direction distortion.
* Reduce position prediction latency, thereby mitigating the shake of nearby objects.
* Make the controllers' movements more precise.

## Use late latching
### Before you begin
Complete the following tasks before enabling late latching for your app.

* Enable multiview rendering. See [this article](/13136/en_multiview-rendering) for detailed instructions.
* Since late latching only supports the Vulkan graphics API, you need to go to **Edit** > **Project Settings** > **Player** > **Android Settings** > **Other Settings** > **Graphics API**, add **Vulkan**, and move it up to the top.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdb2997b188247c7a19ad70a4699c955~tplv-goo7wpa0wc-image.image)

### Enable late latching
Use the following steps to enable late latching for your app.

1. Create a scene or open an existing scene in the Unity Editor.
2. In the **Hierarchy** window, add the **XR Origin** (or XR Rig) to the scene. Skip this step if there is already one in the scene.
3. Select the **XR Origin**.
4. In the **Inspector** window, click **Add Component** at the bottom and add the **PXR_Manager** script to the XR Origin.
5. In the **PXR_Manager (Script)** pane, check the **Use Late Latching** checkbox.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e2c0bf1b3a545cd8d6cfc417c816491~tplv-goo7wpa0wc-image.image)
   The PXR_Late Latching (Script) component is automatically added to the Main Camera object.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/449fce23f99f4e0882489c8b88f49ac5~tplv-goo7wpa0wc-image.image)
   Meanwhile, the Late Latching Debug checkbox appears under the Use Late Latching checkbox. For more information on late latching debugging, refer to the "[Debug late latching](/en_late-latching#22a8d235)" section.

## Debug late latching
The Late Latching Debug mode enables you to check if late latching is working properly for your app. You can use these logs to check if late latching is working properly for your app.
### Requirements

* SDK: 2.2.0 or later
* Unity Editor: 2021.3.19f or later, and currently does not support Unity 2022

### Important note
The Late Latching Debug mode only supports [development builds](https://docs.unity3d.com/2021.2/Documentation/Manual/UnityCloudBuildDevelopmentBuilds.html).
### Steps

1. Check the **Late Latching Debug** checkbox.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bbd766d20954024bbf651dc497ad0d3~tplv-goo7wpa0wc-image.image)
2. Go to **File** > **Build Settings** and check the **Development Build** checkbox.
3. Build the project into an APK file and run it on your PICO device.
4. Use the `adb logcat -s Unity` command to capture logs.
   Example logs:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f580bc8a0fe4af5ab2f33419d6ae69a~tplv-goo7wpa0wc-image.image)

## Known issue
Using late latching and compositor layers (overlay/underlay) together will make these layers jitter.
## Recommended content
For apps that require low latency, you can use late latching and application spacewarp (AppSW) together. AppSW enables apps to render graphics at a refresh rate that is half of the actual screen refresh rate. If you want to know more about AppSW, you can refer to [this article](/13136/en_application-spacewarp).


# --- END: Late Latching.md ---



# --- BEGIN: Multiview Rendering.md ---

Multiview rendering was formerly known as Single Pass Stereo rendering.
Multiview rendering allows a camera to render both the left-eye and right-eye images at nearly the same time. More specifically, the objects will be rendered to the left eye texture once first, and then be automatically duplicated to the right eye texture with proper parameter modifications. Using Multiview rendering can reduce by half the use of draw calls and occlusion culling, and therefore reduces CPU usage. In this regard, Multiview rendering is strongly recommended for CPU-bound applications.
## Normal rendering vs Multiview rendering
| **Normal rendering** | **Multiview rendering** |
| --- | --- |
| The left-eye image on the left, the right-eye image on the right. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0fedd8ed8cb439da64e2a4fb5a31a85~tplv-goo7wpa0wc-image.image) | The left-eye and right-eye images are packed together. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/451a081641864924b1495c4b2083e009~tplv-goo7wpa0wc-image.image) |
> Image credit: Unity

## Important note
If you use post processing after enabling multiview rendering, it will cause performance overhead and affect the app's frame rate.
## Enable Multiview rendering

1. Open your project in Unity Editor.
2. On the top menu bar, select **Edit** > **Project Settings**.
3. In the **Project Settings** window, click **PICO** > **Android settings icon**.
4. Set **Stereo Rendering Mode** to **Multiview**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/40ebfe45bc964349b5b9569e0724118b~tplv-em5hxbkur4-noop.image?width=1401&height=1002)

## See also
Learn more about Single Pass Stereo rendering and XR SDK Display subsystem from Unity's official documentation：

* [Single Pass Stereo rendering](https://docs.unity3d.com/Manual/SinglePassStereoRendering.html)
* [XR SDK Display subsystem](https://docs.unity3d.com/Manual/xrsdk-display.html)


# --- END: Multiview Rendering.md ---



# --- BEGIN: Render Viewport Scaling.md ---

Render viewport scale controls the proportion of the allocated eye texture that should be used for rendering. The larger the scale, the more proportion of eye texture will be used for rendering, resulting in a better image quality. Render viewport scale can be modified at runtime without reallocating eye textures. Therefore, modifying the render viewport scale can dynamically change the eye render resolution.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac41718b74b946e9b9d34a3af92ef986~tplv-goo7wpa0wc-image.image" width="500px" />

## Requirements

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series
* PICO device's system version: 5.6.0 or later

## Preview the effect
In the following example, the render viewport scale is decreased from 1.0 to 0.1 first and then brought back to 1.0. We can observe that the image status transitions from clear to blurry and then back to clear.

      <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f32ddbc878aa4abcaceb7a8f7c4cb971~tplv-goo7wpa0wc-image.image></video>

## Important notes

* While a camera is being rendered, it is impossible to modify the render viewport scale. In the event that an attempt is made to change the scale during camera rendering, the request will be disregarded and an error message will be logged. If the value is modified during gameplay updates, it will not become effective until the next frame.
* A larger render viewport scale brings a higher image quality, while also increases latency and therefore app performance. It is recommended to adjust the render viewport scale according to actual needs.

## Modify the render viewport scale
You can modify the render viewport scale by editing the value in `XR.XRSettings.renderViewportScale`. The default value is 1 and the valid value ranges from 0.0 to 1.0. Below is an example script:
```C#
using UnityEngine;
public class RenderVSTest : MonoBehaviour
{
        float eyeTextureScale = 1.2f;
        
        void Start()
        {
                UnityEngine.XR.XRSettings.eyeTextureResolutionScale = eyeTextureScale;
                UnityEngine.XR.XRSettings.renderViewportScale = 1.0f;
        }

        private void Update()
        {
                UnityEngine.XR.XRSettings.renderViewportScale = 0.58f + 0.42f * (Mathf.Cos(Time.time));
                Debug.Log("Current renderViewportScale: " + UnityEngine.XR.XRSettings.renderViewportScale);
        }
}
```

## Learn more

* [Unity's instructions on render viewport scaling](https://docs.unity3d.com/ScriptReference/XR.XRSettings-renderViewportScale.html).
* You can also change the eye render resolution by modifying the eye buffer resolution, which is a costly operation compared with render viewport scaling. Refer to [this article](/en_modify-eye-texture-resolution) for detailed instructions.


# --- END: Render Viewport Scaling.md ---



# --- BEGIN: Sharpening.md ---

Sharpening is an image processing technique that enhances high-frequency information within an image, improves the edges and contours of the image.
## Tech summary
PICO SDK's sharpening capability is built on a differentiation-based spatial filtering algorithm. This algorithm determines the degree of sharpening for a given pixel based on the color contrast between the given pixel and its surrounding pixels. In general, the smaller the color difference between the given pixel and its surrounding pixels, the smaller the sharpening degree, and vice versa. The following image illustrates the contrast before and after applying sharpening.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcb9973fb51c4015a8fa03644563fa9c~tplv-goo7wpa0wc-image.image" width="350px" />

The sharpening effect for text is shown as follows:
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/946cd81b63d0415c9a7508baf3c3401c~tplv-goo7wpa0wc-image.image" width="350px" />

## Requirements

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series
* PICO device's system version: 5.8.0 or later

## Important notes

* Sharpening increases the number of samplings and computational workload, which may lead to an increase in GPU power consumption.
* Sharpening could potentially make image noise or moiré patterns more pronounced.
* Sharpening and super resolution cannot be simultaneously enabled within the same eye buffer. If you enable both of them, the SDK will only activate super resolution.
* Currently, simultaneously enabling sharpening and subsampling is not supported.

## Enable the Sharpening mode in Unity

1. Open your project in the Unity Editor.
2. In the **Hierarchy** window, add the XR Origin object.
3. Select **XR Origin**, then add the **PXR_Manger** script to it in the **Inspector** window.
4. On the **PXR_Manager (Script)** pane, set the **Sharpening Mode** parameter.
   If you are unable to select sharpening mode, uncheck the **Super Resolution** checkbox and try again.

   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/383a9a2319b94dab8ec44f10eb670d0e~tplv-goo7wpa0wc-image.image)
   The options are described below:
   | **Mode** | **Desciption** |
   | --- | --- |
   | None | Do not enable sharpening. |
   | Normal | Normal sharpening.  <br> In this mode, sharpening a pixel requires sampling its 2 surrounding pixels, resulting in a total of 3 sampling operations. Compared to the Quality mode, this mode has lower power consumption but a reduced sharpening effect. |
   | Quality | High-quality sharpening. <br> In this mode, sharpening a pixel requires sampling its 4 surrounding pixels, resulting in a total of 5 sampling operations. Compared to the Normal mode, this mode has a better sharpening effect but a higher power consumption. |
5. Set the **Sharpening Enhance Mode** parameter to further enhance the effectiveness of sharpening.
   Sharpening enhancement mode is only available to the **Normal** and **Quality** sharpening modes.

   The options are described below:
   | **Mode** | **Desciption** |
   | --- | --- |
   | None | Do not enable sharpening enhancement. |
   | Fixed Foveated | Fixed foveated sharpening. When this mode is enabled, the app only sharpens the pixels in the user's central gaze area while leaving the pixels in the surrounding regions unsharpened. |
   | Self Adaptive | Self-adaptive sharpening. When this mode is enabled, the app only sharpens the pixels with color contrast exceeding a certain threshold in the area, thereby reducing the number of pixels to sharpen and lowering power consumption. |
   | Both | To simultaneously enable fixed foveated sharpening and self-adaptive sharpening. |

## Use API to dynamically enable/disable the Sharpening mode
Call `UPxr_SetSuperResolutionOrSharpening`to dynamically enable or disable the Sharpening mode during your app's runtime.
```C#
public static void UPxr_SetSuperResolutionOrSharpening(SuperResolutionOrSharpeningType type);
```

Below are the values of the `SuperResolutionOrSharpeningType` enum:
```C#
public enum SuperResolutionOrSharpeningType
{        
    None， // Disablt both the Super Resolution and Sharpning modes
    SuperResolution, 
    NormalSharpening,  // Sharpening mode of the Normal level（others will be automatically set to None）
    NormalSharpeningAndFixedFoveated, // Sharpening mode of the Normal + FixedFoveated level（others will be automatically set to None）
    NormalSharpeningAndSelfAdaptive, // Sharpening mode of the Normal + SelfAdaptive level（others will be automatically set to None）
    NormalSharpeningAndFixedFoveatedAndSelfAdaptive, // Sharpening mode of the Normal + FixedFoveated + SelfAdaptive level（others will be automatically set to None）
    QualitySharpening, // Sharpening mode of the Quality level（others will be automatically set to None）
    QualitySharpeningAndFixedFoveated, // Sharpening mode of the Quality + FixedFoveated level（others will be automatically set to None）
    QualitySharpeningAndSelfAdaptive, // Sharpening mode of the Quality + SelfAdaptive level（others will be automatically set to None）
    QualitySharpeningAndFixedFoveatedAndSelfAdaptive,// Sharpening mode of the Quality + FixedFoveated + SelfAdaptive level（others will be automatically set to None）
}
```

Below is the code sample:
```C#
// Enable the Sharpening mode of the Normal level
PXR_Plugin.Render.UPxr_SetSuperResolutionOrSharpening(SuperResolutionOrSharpeningType.NormalSharpening); 

// Enable the Sharpening mode of the Normal + FixedFoveated level
PXR_Plugin.Render.UPxr_SetSuperResolutionOrSharpening(SuperResolutionOrSharpeningType.NormalSharpeningAndFixedFoveated);

// Disable the Super Resolution and Sharpening modes
PXR_Plugin.Render.UPxr_SetSuperResolutionOrSharpening(SuperResolutionOrSharpeningType.None);
```

## Best practice
When using sharpening, it is recommended to enable both the fixed foveated sharpening mode and the self-adaptive sharpening mode. 
The following two images show the pixel areas sharpened when only the fixed foveated sharpening mode is enabled and when both the fixed foveated sharpening mode and the self-adaptive sharpening mode are enabled. The sharpened areas are marked by red color.
By comparing them, it can be observed that enabling both modes at the same time can significantly reduce power consumption while maintaining good visual quality.
| Only fixed foveated sharpening mode is enabled. | Both the fixed foveated sharpening mode and the self-adaptive sharpening mode are enabled. |
| --- | --- |
| ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf92d5cf5ba64518aac8a00dbd5717cd~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/941fe6da718746f781d4998f2f29a824~tplv-goo7wpa0wc-image.image) |
## About super resolution
Both sharpening and super resolution can improve image clarity, but they work differently. Sharpening enhances the high-frequency information within an image, but it only amplifies high-frequency components already present in the image. Super resolution estimates and supplements image details that are not shown in the original image. To learn more about super resolution, refer to the "[Super resolution](/en_super-resolution)" guide.


# --- END: Sharpening.md ---



# --- BEGIN: Super Resolution.md ---

Super resolution refers to the technique of enhancing the resolution of an image from low-resolution (LR) to high-resolution (HR). It uses some specific algorithms that leverages known image information to retrieve and supplement image details and additional data, enhancing image clarity for your app.
## Requirements

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series
* PICO device's system version: 5.8.0 or later

## Recommendations
Take PICO 4 series devices as an example. They have a screen display resolution of 4320 × 2160 pixels, but to balance power consumption and performance, the default rendering resolution (eye buffer) is set to 1504 x 1504 pixels. As a result, your app typically renders at a resolution lower than the device's native resolution. In situations with constrained performance, enabling super resolution can deliver an improved visual experience to users.
However, it is not advisable to enable super resolution when your app's actual rendering resolution is already lower than the default rendering resolution, as using super resolution at this time can make image noise more pronounced. Furthermore, as the eye buffer resolution gradually approaches the device screen's native display resolution, the effectiveness of super resolution will gradually diminish.
Compared to directly increasing the eye buffer resolution, the GPU resources consumed by super resolution are relatively fixed. In scenarios with lower GPU loads, you may choose to directly increase the Eye Buffer resolution. Still, in scenarios with heavier GPU loads, it is recommended to use super resolution to more reasonably allocate GPU resources.
## Considerations

* Super resolution increases the GPU load on the compositor service. Enabling super resolution for three or more layers may result in resource constraints on the compositor service, leading to screen tearing. Therefore, the SDK automatically disables super resolution when the GPU load is excessive and re-enables it once the GPU load returns to normal.
* Super resolution and sharpening cannot be simultaneously enabled within the same eye buffer. If you enable both of them, the SDK will only activate super resolution.
* Currently, super resolution only applies to the rendering resolution (eye buffer) and does not support compositor layers.
* Currently, simultaneously enabling super resolution and subsampling is not supported.

## Enable the Super Resolution mode in Unity

1. Open your project in the Unity Editor.
2. In the **Hierarchy** window, add the XR Origin object.
3. Select **XR Origin**, then add the **PXR_Manager** script to it in the **Inspector** window.
4. On the **PXR_Manager (Script)** pane, check the **Super Resolution** checkbox.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd39096ed7cc4466bd97beae64a16183~tplv-goo7wpa0wc-image.image)

## Use the API to dynamically enable/disable the Super Resolution mode
Call `UPxr_SetSuperResolutionOrSharpening`to dynamically enable or disable the Super Resolution mode during your app's runtime.
```C#
public static void UPxr_SetSuperResolutionOrSharpening(SuperResolutionOrSharpeningType type);
```

Below are the values of the `SuperResolutionOrSharpeningType` enum:
```C#
public enum SuperResolutionOrSharpeningType
{        
    None， // Dsiable both the Super Resolution and Sharpening modes 
    SuperResolution,  // Enable the Super Resolution mode (others will be set to None)
    NormalSharpening,  
    NormalSharpeningAndFixedFoveated, 
    NormalSharpeningAndSelfAdaptive, 
    NormalSharpeningAndFixedFoveatedAndSelfAdaptive, 
    QualitySharpening, 
    QualitySharpeningAndFixedFoveated,
    QualitySharpeningAndSelfAdaptive,
    QualitySharpeningAndFixedFoveatedAndSelfAdaptive,
}
```

Below is the code sample:
```C#
// Enable the Super Resolution mode
PXR_Plugin.Render.UPxr_SetSuperResolutionOrSharpening(SuperResolutionOrSharpeningType.SuperResolution); 

// Disable both the Super Resolution and Sharpening modes
PXR_Plugin.Render.UPxr_SetSuperResolutionOrSharpening(SuperResolutionOrSharpeningType.None);
```

## Best practice
Super resolution is one of the methods for improving image clarity. You can also set the Multisampling Anti-Aliasing (MSAA) for your project while using super resolution to provide users with even better visual quality. For detailed instructions, refer to the "[Anti-aliasing](/en_anti-aliasing)" guide.
## About sharpening
Both super resolution and sharpening can improve image clarity, but they work differently. Super resolution estimates and supplements image details that are not shown in the original image, while sharpening enhances the high-frequency information within an image, but it only amplifies high-frequency components already present in the image. To learn more about sharpening, refer to the "[Sharpening](/sharpening)" guide.


# --- END: Super Resolution.md ---



# --- BEGIN: Universal Render Pipeline.md ---

This page takes **Unity 2020.3.30f1** as an example to walk you through how to use the Universal Render Pipeline (URP).
URP is a prebuilt Scriptable Render Pipeline made by Unity. URP offers developer-friendly rendering workflows to let you create optimized graphics easily. See the [documentation](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@10.3/manual/index.html) on Unity website for more details.
## Install URP
Follow the steps below to install URP:

1. Open your project in Unity Editor.
2. From the top menu bar, select **Window** > **Package Manager**.
   The **Package Manager** pop-up window appears.
3. Set the **Packages** filer to **Unity Registry**.
4. Select **Universal RP**.
5. Click **Install**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/b597f279b2324a9589e42cdd1a353ae6~tplv-em5hxbkur4-noop.image?width=1600&height=1135)

## Use URP
To use URP, you need to create a URP asset, add the URP asset to graphics settings, disable HDR for the URP asset, and upgrade materials for your project.
### Create a URP asset
Follow the steps below to create a URP asset.

1. Under the **Project** tab, select an existing folder from the **Assets** directory, or create a new folder in the **Assets** directory and select it.
2. From the top menu bar, select **Assets** > **Create** > **Rendering** > **Universal Render Pipeline** > **Pipeline Asset (Forward Renderer)**.
   The URP asset is created in the selected folder.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c6e95f18d3a94dcdb9f7c1458d25e8d6~tplv-em5hxbkur4-noop.image?width=1867&height=542)

### Add the URP asset to graphics settings
If you do not add the URP asset to graphics settings, Unity will still use the Built-in render pipeline. Follow the step below to add the URP asset to graphics setting.

1. From the top menu bar, select **Edit** > **Project Settings**.
   The **Project Settings** pop-up window appears.
2. From the left navigation pane, select **Graphics**.
   The **Graphics** pane appears on the right side of the window.
3. In the **Scriptable Render Pipeline Settings** field, add the URP asset you created earlier.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/299179d06378427097e1e64ef44f0b0c~tplv-em5hxbkur4-noop.image?width=1424&height=987)

### Disable HDR
Follow the steps below to disable HDR for the URP asset.

1. Go to the folder where the URP asset is located.
2. Click **Universal Render Pipeline Asset**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/be1fe3cf283c419793997044a97374bc~tplv-em5hxbkur4-noop.image?width=1841&height=542)
3. Under the **Inspector** tab, expand the **Quality** list.
4. Disable **HDR**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/2a76fba256ad4549bea21492ee4ffb39~tplv-em5hxbkur4-noop.image?width=685&height=547)

### Upgrade project materials
Follow the steps below to upgrade your project's materials to URP materials.

1. From the top menu bar, select **Edit** > **Render Pipeline** > **Universal Render Pipeline** > **Upgrade Project Materials to UniversalRP Materials**.
   The **Material Upgrader** pop-up window appears.
2. Read the instructions on the pop-up window.
3. Click **Proceed**.
   The materials used in your project are upgraded to URP materials.

## Known issues
Before Unity fixes the following issues, please use the Universal Render Pipeline carefully.

* For Unity 2021 or later, setting MSAA while using the Universal Render Pipeline will cause a drop in frame rate.
* For Unity 2020 or later, compared with OpenGLES, adding Vulkan to Graphics API can cause low frame rate, high memory and GPU usage.
* Using Vulkan, URP, and HDR at the same time will cause the underlay layers and VST layer fail to be displayed.
* For Unity 2021 or later, enabling Screen Space Ambient Occlusion (SSAO) in URP Renderer will cause low frame rate, high memory and GPU usage.
* For Unity 2022 and above, if you are using OpenGLES and MultiView in your project and have added the Universal Render Pipeline but are not using it, you should actively remove the URP package, remove the current light and add a new one. Otherwise, the app may crash during runtime.
* If you use Unity6, URP, OpenGL, Multi-pass, and MSAA (not in Disabled state) simultaneously, it will cause the content of the Eye Buffer to fail to render. Changing any of the above configurations will resolve this issue.


# --- END: Universal Render Pipeline.md ---



# --- BEGIN: Use Blurred Quad layers.md ---

Blurred Quad layers are used to render spatial pictures and spatial videos.
To use this shape of layer, you need to set the **Shape** parameter to **Blurred Quad** in the **PXR_Compostion Layer** component, set the **Texture Type** parameter to **External Surface** (only supported currently), and then set up Blurred Quad layer-exclusive parameters.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66a8e3e4f07a4900aa70a013bfd237e7~tplv-goo7wpa0wc-image.image" width="450px" />

Below are details about Blurred Quad layer-exclusive parameters.
| **Parameter** | **Description** |
| --- | --- |
| Mode | This parameter determines how spatial pictures and spatial videos are displayed in the scene. <br>  <br> * Small Window: open a small window to display the picture or video in the scene. The texture is 0.5-meter behind the picture or video. <br>  <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cb47926ff3f4a91b7cb0402429c540f~tplv-goo7wpa0wc-image.image) <br>  <br> * Immersion: compared with Small Window mode, Immersion mode provides a larger window, no longer obscures the textures, and features the frosted glass effect that softly blends outward. <br>  <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5d2f31a532b45ce94f90010e87cad44~tplv-goo7wpa0wc-image.image) |
| Scale | This is used to reduce parallax and assess whether the subject is too close or if the parallax is too large. If the parallax is excessive, the overall scale of the image during playback will be reduced, and a horizontal shift will be applied to the left and right eye images to lower the parallax and improve image fusion. The value range is [0.0, +∞] and should be adjusted based on window size. It is recommended to use 0.5 for Small Window mode and 1.0 for Immersion mode. |
| Shift  | This is used to apply a horizontal shift to the left and right eye images, reducing parallax to improve image fusion. The offset direction for the left and right eyes is opposite. The specified Shift value is applied to the left eye, while the right eye uses the opposite Shift value (i.e., -Shift). The value range is [-1, 1], and the default value is 0.01. |
| FOV | The vertical field of view (FOV) for user-captured pictures or videos. The value range is [0, 180], and the default value is 70. If the picture or video contains a FOV value or if the actual FOV is known, that value should be used; otherwise, it is recommended to set it to 61.05. <br> ***Note***: This parameter sets the vertical angle, not the radians. At runtime, the vertical FOV will be calculated based on this setting and the texture's width and height. |
| IPD | The interpupillary distance (IPD) of the camera used to capture pictures or videos. The value range is [0.05, 0.07], and the default value is 0.064. |
In addition to setting parameters in the **PXR_Overlay (Script)** component within the Unity Editor, you can also directly modify the values in the PXR_Overlay.cs file (as shown below). Changes made here will take effect every frame.
```C#
#region Blurred Quad
public BlurredQuadMode blurredQuadMode = BlurredQuadMode.SmallWindow;

public float blurredQuadScale = 0.5f;
public float blurredQuadShift = 0.01f;
public float blurredQuadFOV = 70.0f;
public float blurredQuadIPD = 0.064f;
#endregion
```


# --- END: Use Blurred Quad layers.md ---



# --- BEGIN: Use EAC layers.md ---

Equi-Angular Cubemap (EAC) is a projection technique used to display 180 or 360 degree panoramic images or videos. It is a hybrid of two other projection techniques: the equidistant projection and the cubemap projection.
The SDK provides four EAC modes. After setting the **Shape** parameter to **Eac** in **Overlay Settings**, you can then select the type of EAC layer in the **Model Type** parameter.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee612849cc7042129209acf78b6d22a4~tplv-goo7wpa0wc-image.image" width="400px" />

Below are the descriptions of the four EAC modes:
| **Mode** | **Description** | **Layout of faces** |
| --- | --- | --- |
| EAC 360 | Horizontal 360° × Vertical 360° panoramic video. | The layout of the 6 faces of the 360° EAC layer is as follows. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad73871b762e47c8b001fa519d0ce3d6~tplv-goo7wpa0wc-image.image) |
| EAC 360 View Port | In addition to Horizontal 360° × Vertical 360° panoramic video, it supports viewport offset. |  |
| EAC 180 | Horizontal 180° × Vertical 180° video. | The layout of the 5 faces of the 180° EAC layer is as follows. Among them, the left, right, bottom, and top faces only have their front halves displayed. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5bf93ab34364d7daac7b122754a9f13~tplv-goo7wpa0wc-image.image) |
| EAC 180 View Port | In addition to Horizontal 180° × Vertical 180° video, it supports viewport offset. |  |
Below are the descriptions of EAC-related parameters:
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59092c21e3d24b3b9c89193e176c0fe0~tplv-goo7wpa0wc-image.image)
| **Parameter** | **Description** | **Remarks** |
| --- | --- | --- |
| Offset Pos Left | The translation of viewport when mapping the texture of the left eye. | Only applicable to the following EAC modes: <br>  <br> * Eac 180 View Port <br> * Eac 360 View Port |
| Offset Pos Right | The translation of viewport when mapping the texture of the right eye. |  |
| Offset Rot Left | The rotation of viewport when mapping the texture of the left eye. |  |
| Offset Rot Right | The rotation of viewport when mapping the texture of the right eye. |  |
| Overlap Factor | Overlap coefficient, indicating the proportion of expansion for each face. The sampling formula in the compositor is as follows: Texcoord = arctan(position/overlapFactor) | - <br>  |
##


# --- END: Use EAC layers.md ---



# --- BEGIN: Use Equirect layers.md ---

Equirect layers are sphere textures, which are normally used to display 180/360 panoramic images or videos. Below are the steps to add an Equirect layer:

1. Add an XR Origin and 3D object, then respectively add the PXR_Manager script and the PXR_Composition Layer script to them. 
2. In the **PXR_Over Lay** pane, do the following:
   1. Select a **Type**.
   2. Set the **Shape** to **Equirect**.
   3. Set the **Depth** if needed.
   4. Select a **Texture Type**.
   5. Specify a 360 panoramic texture in **Texture**.
3. Set **Texture Rects**, **Layer Blend**, and **Override Color Scale** for the layer. 
4. Run the scene on your PICO VR headset. Below is the expected effect:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f000a15fe57e4881ae4b9cbda2cfa5c1~tplv-em5hxbkur4-noop.image?width=935&height=523)


# --- END: Use Equirect layers.md ---



# --- BEGIN: What's the maximum number of VR compositor layers supported_.md ---

For now, a single scene supports no more than **15** VR compositor layers, and the exceeded layers will not be displayed. Moreover, a single scene only supports one Equirect layer and one Cylinder layer. To maintain good performance, it is recommended that you add no more than **4** compositor layers to a single scene. For more information about VR compositor layers, see [this article](/13136/en_vr-compositor-layers).


# --- END: What's the maximum number of VR compositor layers supported_.md ---

