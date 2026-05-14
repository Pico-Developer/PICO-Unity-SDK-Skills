# Core Features

## Table of Contents
- Body Tracking
- Controller & HMD input mapping
- Enable interaction between the controller ray and a canvas
- Eye Tracked Foveated Rendering
- Eye Tracking
- Face Tracking
- Fixed Foveated Rendering
- Focus Awareness
- Haptic Feedback
- Interaction Pack overview
- Mixed Reality Capture
- MR Safeguard
- PICO Haptic Editor
- PXR_Hand Pose Generator script
- PXR_Hand Pose script
- Sense Pack overview
- Shared Spatial Anchor
- Spatial Anchor
- Spatial Audio
- Spatial Mesh
- Use hand tracking
- Video Seethrough

---



# --- BEGIN: Body Tracking.md ---

Body Tracking is a motion capture technology used to collect information about the user's body position and movements, and convert this information into reproducible pose data. Body Tracking enables users to run, kick, step, lie down, twist the waist, and more, in XR scenes, enriching your app's user experience.
PICO's Body Tracking feature needs to work with PICO Motion Trackers. PICO Motion Trackers can obtain information about the user's body position and movements. Body Tracking APIs will convert this information into pose data for multiple body joints, which can be used as input for your app.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb790438b29a494aba7ab4dc78ad8bcf~tplv-goo7wpa0wc-image.image" width="408px" />

## Body Tracking modes
The SDK provides two Body Tracking modes: half-body tracking and full-body tracking. Below are detailed descriptions:
| **Mode** | **Description** |
| --- | --- |
| Half-body tracking | This mode outputs the position and pose information of 14 (No.0 -13) human body joints, and provides foot stepping data. |
| Full-body tracking | This mode outputs the position and pose information of 24 human body joints, and provides foot stepping data. |
## Development environment

* PICO device models: PICO 4 series, PICO 4 Ultra series
* PICO device's system version: 5.13.0 or later
* PICO Motion Tracker (Official)

## Prerequisites

* Have added the XR Origin object.
* Have added the PXR_Manager (Script) component to the XR Origin object.

## Integrate the Body Tracking feature
### **Step 1: Enable the Body Tracking capability for your app**
On the **PXR_Manager (Script)** panel of the **Inspector** window, check the **Body Tracking** checkbox to enable the Body Tracking capability for your app. Then you can call Body Tracking APIs to integrate this feature into your app.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be0697de3d3b401da64b05c4df2ab82a~tplv-goo7wpa0wc-image.image" width="450px" />

### Step 2: Retrieve the information of PICO Motion Trackers
PICO Motion Trackers must be used in conjunction with the PICO Motion Tracker app. To ensure that your app can receive body movement data from motion trackers, users need to pair (connect) motion trackers with the PICO Motion Tracker app and to calibrate their body positioning using this app. You can use APIs to obtain the connection and calibration state of motion trackers.
| **API** | **Description** |
| --- | --- |
| GetBodyTrackingSupported | Gets whether the current PICO headset supports Body Tracking. |
| GetBodyTrackingState | Gets the connection state of currently connected motion trackers. |
| StartMotionTrackerCalibApp（***Deprecated API***: OpenFitnessBandCalibrationAPP） | Launches the PICO Motion Tracker app to perform calibration. <br>  <br> * For Motion Tracker (Official), "single-glance calibration" will be performed. When a user has a glance at the PICO Motion Tracker on their lower legs, calibration is completed. <br> * For Motion Tracker (Beta), the user needs to follow the instructions on the home of the PICO Motion Tracker app to complete calibration. |
**Note**
To ensure the accuracy of body tracking data, it is recommended to listen to the change of the calibration state. Once the body tracking data is not accurate enough for use, you need to immediately guide the user to re-calibrate.

### Step 3: Start the Body Tracking feature
Once the PICO Motion Trackers have connected to the PICO Motion Tracker app, the user has completed the calibration, the motion trackers have normal battery levels, and the tracking mode has been set to Body Tracking, you can then start the Body Tracking feature in your app using the following APIs:
| **API** | **Description** |
| --- | --- |
| StartBodyTracking | Start body tracking. |
In `StartBodyTracking`, you need to specify the body tracking mode:  `BODY_JOINT_SET_BODY_START_WITHOUT_ARM` (half-body tracking); `BODY_JOINT_SET_BODY_FULL_START` (full-body tracking).
Below is the code sample:
```C#
// Set bone lengths
BodyTrackingBoneLength boneLength = new BodyTrackingBoneLength();
// Start full-body tracking
int ret = PXR_MotionTracking.StartBodyTracking(BodyJointSet.BODY_JOINT_SET_BODY_FULL_START,boneLength);
```

### **Step 4: Retrieve pose data for different body joints**
Call `GetBodyTrackingData` to retrieve the position and orientation data of various body joints, which can be used as input for your app.
```C#
public class PXR_BodyTrackingBlock : MonoBehaviour
{
    public Transform skeletonJoints;
    public bool showCube = true;
    public float zDistance = 0;

    private bool supportedBT = false;
    private bool updateBT = true;

    private BodyTrackingGetDataInfo bdi = new BodyTrackingGetDataInfo();
    private BodyTrackingData bd = new BodyTrackingData();
    private Transform[] boneMapping = new Transform[(int)BodyTrackerRole.ROLE_NUM];
    BodyTrackingStatus bs = new BodyTrackingStatus();
    bool istracking = false;
    // Start is called before the first frame update
    void Start()
    {
        skeletonJoints.transform.localPosition += new Vector3(0, 0, zDistance);
        InitializeSkeletonJoints();
        StartBodyTracking();
    }

    // Update is called once per frame
    void Update()
    {
      

#if UNITY_ANDROID
        // Update bodytracking pose.
        if (updateBT )
        {
            PXR_MotionTracking.GetBodyTrackingState(ref istracking, ref bs);

            // If not calibrated, invoked system motion tracker app for calibration.
            if (bs.stateCode!=BodyTrackingStatusCode.BT_VALID)
            {
                return;
            }
            // Get the position and orientation data of each body node.
            int ret = PXR_MotionTracking.GetBodyTrackingData(ref bdi, ref bd);

            // if the return is successful
            if (ret == 0)
            {
                for (int i = 0; i < (int)BodyTrackerRole.ROLE_NUM; i++)
                {
                    var bone = boneMapping[i];
                    if (bone != null)
                    {
                        bone.transform.localPosition = new Vector3((float)bd.roleDatas[i].localPose.PosX, (float)bd.roleDatas[i].localPose.PosY, (float)bd.roleDatas[i].localPose.PosZ);
                        bone.transform.localRotation = new Quaternion((float)bd.roleDatas[i].localPose.RotQx, (float)bd.roleDatas[i].localPose.RotQy, (float)bd.roleDatas[i].localPose.RotQz, (float)bd.roleDatas[i].localPose.RotQw);
                    }
                }
            }
        }

#endif
    }

    public void StartBodyTracking()
    {
        // Query whether the current device supports human body tracking.
        PXR_MotionTracking.GetBodyTrackingSupported(ref supportedBT);
        if (!supportedBT)
        {
            return;
        }
        BodyTrackingBoneLength bones = new BodyTrackingBoneLength();

        // Start BodyTracking
        PXR_MotionTracking.StartBodyTracking(BodyJointSet.BODY_JOINT_SET_BODY_FULL_START, bones);
        
        PXR_MotionTracking.GetBodyTrackingState(ref istracking, ref bs);

        // If not calibrated, invoked system motion tracker app for calibration.
        if (bs.stateCode!=BodyTrackingStatusCode.BT_VALID)
        {
            if (bs.message==BodyTrackingMessage.BT_MESSAGE_TRACKER_NOT_CALIBRATED||bs.message==BodyTrackingMessage.BT_MESSAGE_UNKNOWN)
            {
                PXR_MotionTracking.StartMotionTrackerCalibApp();
            }
        }
        
        skeletonJoints.gameObject.SetActive(true);
        updateBT = true;
    }

    private void OnDestroy()
    {
        int ret = PXR_MotionTracking.StopBodyTracking();
        updateBT = false;
    }

    public void InitializeSkeletonJoints()
    {
        Queue<Transform> nodes = new Queue<Transform>();
        nodes.Enqueue(skeletonJoints);
        while (nodes.Count > 0)
        {
            Transform next = nodes.Dequeue();
            for (int i = 0; i < next.childCount; ++i)
            {
                nodes.Enqueue(next.GetChild(i));
            }

            ProcessJoint(next);
        }
    }

    void ProcessJoint(Transform joint)
    {
        int index = GetJointIndex(joint.name);
        if (index >= 0 && index < (int)BodyTrackerRole.ROLE_NUM)
        {
            boneMapping[index] = joint;
            Transform cubeT = joint.Find("Cube");
            if (cubeT)
            {
                cubeT.gameObject.SetActive(showCube);
            }
        }
        else
        {
            Debug.LogWarning($"{joint.name} was not found.");
        }
    }

    // Returns the integer value corresponding to the JointIndices enum value passed in as a string
    int GetJointIndex(string jointName)
    {
        BodyTrackerRole val;
        if (Enum.TryParse(jointName, out val))
        {
            return (int)val;
        }
        return -1;
    }
}
```

### Step 5: Stop the Body Tracking feature
When the Body Tracking feature is no longer needed in the scene or the user exits your app, call `StopBodyTracking` to stop body tracking.
```C#
int ret = PXR_MotionTracking.StopBodyTracking();
```

## Animate avatars
In social applications, if you need to render avatars, you can either create avatars totally by yourself or use the PICO Unity Avatar SDK to facilitate the process. The PICO Unity Avatar SDK provides a highly customizable avatar solution and a variety of features to help you create vivid avatars in your apps, improving users' interaction experience. Combining the Body Tracking feature of the PICO Unity Integration SDK, you can animate avatrss within your apps. Refer to [PICO Unity Avatar SDK's documentation](https://developer-cn.picoxr.com/document/unity-avatar/body-tracking/) for detailed instructions.
## Body joints reference
PICO SDK's Body Tracking feature supports tracking 24 human body joints as shown below.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41c2c2ee630c4962b1a973e458be5608~tplv-goo7wpa0wc-image.image" width="600px" />

Below are the descriptions of related concepts:
| **Concept** | **Description** |
| --- | --- |
| Coordinate  | Body joint data uses the same global coordinate system as the HMD data  |
| Root joint  | 0 (Pelvis)  |
| Parent/child joint  | Joints numbered from 1 to 23. Parent joints are located near the root joint, while the child joints are located near the end of the limbs.  |
| Bone  <br>   | A bone is a rigid part between two joints, and its pose is stored in the parent joint which is located near the root joint. For example, the pose of the bone of the lower leg is stored in the knee joint.  <br> More examples:  <br>  <br> * Joint 4 (LEFT_KNEE): It stores the location information of the left knee joint and the pose of the bone of the left lower leg.  <br> * Joint 7 (LEFT_ANKLE): It stores the location information of the left ankle joint and the pose of the bone of the left foot.  |
The following is the BodyTrackerRole enumeration. Each value corresponds to a joint presented in the above reference image.
```C#
public enum BodyTrackerRole
    {
        Pelvis = 0, 
        LEFT_HIP = 1, 
        RIGHT_HIP = 2, 
        SPINE1 = 3,  
        LEFT_KNEE = 4,  
        RIGHT_KNEE = 5, 
        SPINE2 = 6,  
        LEFT_ANKLE = 7, 
        RIGHT_ANKLE = 8,  
        SPINE3 = 9,  
        LEFT_FOOT = 10, 
        RIGHT_FOOT = 11,
        NECK = 12,  
        LEFT_COLLAR = 13,  
        RIGHT_COLLAR = 14, 
        HEAD = 15, 
        LEFT_SHOULDER = 16, 
        RIGHT_SHOULDER = 17, 
        LEFT_ELBOW = 18,
        RIGHT_ELBOW = 19,  
        LEFT_WRIST = 20,  
        RIGHT_WRIST = 21,  
        LEFT_HAND = 22,  
        RIGHT_HAND = 23  
    }
```

## API reference
For more details on Body Tracking APIs, such as parameter descriptions and returns, refer to the [API reference](/reference/unity/client-api/PXR_MotionTracking/).
## Creative Commons license
The body tracking solution of this Service ("PICO Motion Tracking Service"), is adapted from ["SMPL-Body](https://smpl.is.tue.mpg.de/bodylicense.html)" by Max Planck Society e.V used under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/). This Service is licensed under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/) by Hainan Chuangjianweilai Technology Co., Ltd.


# --- END: Body Tracking.md ---



# --- BEGIN: Controller & HMD input mapping.md ---

Controllers and HMDs are the major tools that users use to interact with the virtual world. Through performing controller/HMD actions, users are enabled for various operations within your apps. For example, they can press the Back button to exit the current scene or app, press the Confirm button to make a setup, etc. Every controller/HMD action will be mapped to an input event. The PICO Unity Integration SDK uses Unity's official keycodes for input event mapping.
## Controller mapping
PICO controllers buttons use the keycodes provided by the Unity XR Input System.
### PICO 4 Ultra
The following figures display the buttons on each controller:
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25088a9bfdc9471ba3c7ea0d62cc508e~tplv-goo7wpa0wc-image.image" width="700px" />

You can pass a static property in [InputDevice.TryGetFeatureValue](https://docs.unity3d.com/ScriptReference/XR.InputDevice.TryGetFeatureValue.html) to get the activation status of a specified button. The table below describes the mappings between buttons and static properties:
| **Button** | **Static Properties** <br> ***Note***: For detailed descriptions, refer to the table for PICO Neo3. |
| --- | --- |
| Menu | [CommonUsages.menuButton](https://docs.unity3d.com/cn/2021.2/ScriptReference/XR.CommonUsages-menuButton.html) |
| Trigger | * [CommonUsages.triggerButton](https://docs.unity.cn/2019.1/Documentation/ScriptReference/XR.CommonUsages-triggerButton.html) <br> * [CommonUsages.trigger](https://docs.unity3d.com/ScriptReference/XR.CommonUsages-trigger.html) |
| Grip | * [CommonUsages.gripButton](https://docs.unity3d.com/cn/2020.3/ScriptReference/XR.CommonUsages-gripButton.html) <br> * [CommonUsages.grip](https://docs.unity3d.com/ScriptReference/XR.CommonUsages-grip.html) |
| Capture | N/A |
| Thumbstick | * [CommonUsages.primary2DAxisClick](https://docs.unity3d.com/cn/2019.4/ScriptReference/XR.CommonUsages-primary2DAxisClick.html) <br> * [CommonUsages.primary2DAxis](https://docs.unity3d.com/ScriptReference/XR.CommonUsages-primary2DAxis.html) |
| X/A | [CommonUsages.primaryButton](https://docs.unity3d.com/cn/2021.1/ScriptReference/XR.CommonUsages-primaryButton.html) |
| Y/B | [CommonUsages.secondaryButton](https://docs.unity3d.com/cn/2020.2/ScriptReference/XR.CommonUsages-secondaryButton.html) |
### PICO 4
The following figures display the buttons on each controller:
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/7243d25c977f4852872588b8950b4cd5~tplv-em5hxbkur4-noop.image?width=1554&height=819" width="526px" />

<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/b13044b36a5546e2a1e7dd3ce8611fee~tplv-em5hxbkur4-noop.image?width=2868&height=1958" width="440px" />

The table below describes the mappings between PICO 4 controller buttons and Unity XR keycodes (for detailed descriptions, refer to the table for PICO Neo3):
| **Button** | **Unity XR Keycode** |
| --- | --- |
| Menu | [CommonUsages.menuButton](https://docs.unity3d.com/cn/2021.2/ScriptReference/XR.CommonUsages-menuButton.html) |
| Trigger | * [CommonUsages.triggerButton](https://docs.unity.cn/2019.1/Documentation/ScriptReference/XR.CommonUsages-triggerButton.html) <br> * [CommonUsages.trigger](https://docs.unity3d.com/ScriptReference/XR.CommonUsages-trigger.html) |
| Grip | * [CommonUsages.gripButton](https://docs.unity3d.com/cn/2020.3/ScriptReference/XR.CommonUsages-gripButton.html) <br> * [CommonUsages.grip](https://docs.unity3d.com/ScriptReference/XR.CommonUsages-grip.html) |
| Capture | N/A <br> ***Note***: If you have enabled [content protection](/13136/en_content-protection) for your app, users are unable to capture or record the screen in your app. |
| Thumbstick | * [CommonUsages.primary2DAxisClick](https://docs.unity3d.com/cn/2019.4/ScriptReference/XR.CommonUsages-primary2DAxisClick.html) <br> * [CommonUsages.primary2DAxis](https://docs.unity3d.com/ScriptReference/XR.CommonUsages-primary2DAxis.html) |
| X/A | [CommonUsages.primaryButton](https://docs.unity3d.com/cn/2021.1/ScriptReference/XR.CommonUsages-primaryButton.html) |
| Y/B | [CommonUsages.secondaryButton](https://docs.unity3d.com/cn/2020.2/ScriptReference/XR.CommonUsages-secondaryButton.html) |
### PICO Neo3
The following figures display the buttons on each controller:
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/a8ed19ad61e444ef8bb3d5e1a579bd95~tplv-em5hxbkur4-noop.image?width=1399&height=1029" width="502px" />

<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/2fa716c744a44803862d5eb3acd922fa~tplv-em5hxbkur4-noop.image?width=2650&height=1718" width="426px" />

The table below describes the mappings between PICO Neo3 controller buttons and Unity XR keycodes:
| **Button** | **Unity Keys** |
| --- | --- |
| Menu | [CommonUsages.menuButton](https://docs.unity3d.com/2021.2/Documentation/ScriptReference/XR.CommonUsages-menuButton.html): represents whether the Menu button has been activated (pressed). |
| Trigger | * [CommonUsages.triggerButton](https://docs.unity.cn/2019.1/Documentation/ScriptReference/XR.CommonUsages-triggerButton.html): represents whether the Trigger button has been activated (pressed). <br> * [CommonUsages.trigger](https://docs.unity3d.com/ScriptReference/XR.CommonUsages-trigger.html): represents the degree to which the Trigger button was pressed. For example, in an archery game, it represents how full the bow has been drawn. |
| Grip | * [CommonUsages.gripButton](https://docs.unity3d.com/2020.3/Documentation/ScriptReference/XR.CommonUsages-gripButton.html): represents whether the Grip button has been activated (pressed). <br> * [CommonUsages.grip](https://docs.unity3d.com/ScriptReference/XR.CommonUsages-grip.html): represents the degree to which the Grip button was pressed. For example, in an archery game, it represents how full the bow has been drawn. |
| Thumbstick | * [CommonUsages.primary2DAxisClick](https://docs.unity3d.com/2019.4/Documentation/ScriptReference/XR.CommonUsages-primary2DAxisClick.html): represents whether the Thumbstick has been activated (pressed). <br> * [CommonUsages.primary2DAxis](https://docs.unity3d.com/ScriptReference/XR.CommonUsages-primary2DAxis.html): represents whether the Thumbstick has been moved upward, downward, leftward, or rightward. |
| X/A | [CommonUsages.primaryButton](https://docs.unity3d.com/2021.1/Documentation/ScriptReference/XR.CommonUsages-primaryButton.html): represents whether the X/A button has been activated (pressed). |
| Y/B | [CommonUsages.secondaryButton](https://docs.unity3d.com/2020.2/Documentation/ScriptReference/XR.CommonUsages-secondaryButton.html): represents whether the Y/B button has been activated (pressed). |
### Retrieve InputDevice for controllers
Retrieve `InputDevice` for controllers using [InputDevices.GetDeviceAtXRNode](https://docs.unity3d.com/ScriptReference/XR.InputDevices.GetDeviceAtXRNode.html).
```C#
// Retrieve InputDevice for the left controller
var leftHandDevice = UnityEngine.XR.InputDevices.GetDeviceAtXRNode(UnityEngine.XR.XRNode.LeftHand);
```

### Retrieve button input values
Retrieve the input values of physical controller buttons by specifying corresponding keycodes in [InputDevice.TryGetFeatureValue](https://docs.unity3d.com/ScriptReference/XR.InputDevice.TryGetFeatureValue.html). Below is an example API call:
```C#
// Gets whether the Trigger button has been pressed
bool triggerValue;
if (device.TryGetFeatureValue(UnityEngine.XR.CommonUsages.triggerButton, out triggerValue) && triggerValue)
{
    Debug.Log("Trigger button is pressed.");
}
```

## HMD mapping
### PICO 4 Ultra
The following figure displays the buttons on the HMD:
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/580f606faf354d088322adc6aa2911a7~tplv-goo7wpa0wc-image.image" width="500px" />

The table below describes the mapping between HMD buttons and Android keys:
| **Button** | **Static Properties** | **Remarks** |
| --- | --- | --- |
| Volume Up | [VOLUME_UP](https://source.android.com/docs/core/interaction/input/key-layout-files#system-controls) | A system-level Android key. Not open for modification. |
| Volume Down | [VOLUME_DOWN](https://source.android.com/docs/core/interaction/input/key-layout-files#system-controls) | A system-level Android key. Not open for modification. |
### PICO 4
The following figure displays the buttons on the HMD:
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/5c0be10cef3f4a15be675a3fcaef84a7~tplv-em5hxbkur4-noop.image?width=3160&height=1926" width="546px" />

The table below describes the mapping between HMD buttons and Android keys:
| **Button** | **Android Key** | **Remarks** |
| --- | --- | --- |
| Volume Up | [VOLUME_UP](https://source.android.com/docs/core/interaction/input/key-layout-files#system-controls) | A system-level Android key. Not open for modification. |
| Volume Down | [VOLUME_DOWN](https://source.android.com/docs/core/interaction/input/key-layout-files#system-controls) | A system-level Android key. Not open for modification. |
### PICO Neo3
The following figures display the buttons on the HMD:
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e94db38d5d8d42bc81f2c4e781a1aff9~tplv-em5hxbkur4-noop.image?width=2866&height=1848" width="524px" />

<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/5985097f3f48403ea90a5f44d3554e06~tplv-em5hxbkur4-noop.image?width=2202&height=1352" width="370px" />

The table below describes the mapping between HMD buttons and Unity/Android keys:
| **Button** | **Key** | **Remarks** |
| --- | --- | --- |
| Back | [KeyCode.Escape](https://docs.unity3d.com/ScriptReference/KeyCode.Escape.html) | N/A |
| Confirm | [KeyCode.JoystickButton0](https://docs.unity3d.com/ScriptReference/KeyCode.JoystickButton0.html) | N/A |
| Home | [KeyCode.Home](https://docs.unity3d.com/ScriptReference/KeyCode.Home.html) | A system-level key. Not open for modification. |
| Volume Up | [VOLUME_UP](https://source.android.com/docs/core/interaction/input/key-layout-files#system-controls) | A system-level Android key. Not open for modification. |
| Volume Down | [VOLUME_DOWN](https://source.android.com/docs/core/interaction/input/key-layout-files#system-controls) | A system-level Android key. Not open for modification. |
In the new Unity Input System, querying `KeyCode.JoystickButton0` will report errors and the Confirm key is unable to be identified. To solve this issue, follow the steps below to use the old Unity Input System:

1. Go to **Edit** > **Project Settings** > **Player** > **Other Settings** > **Configuration**.
2. Set **Active Input Handling*** to **Both** or **Input Manager (Old)**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/b1f3288ed9d849bc993d52bd0d755b2d~tplv-em5hxbkur4-noop.image?width=1401&height=994)

## Add controller models
The PICO Unity Integration SDK packages a pair of controller models that you can access from **Packages/PICO Integration/Assets/Resources/Prefabs**. Based on the device model that users use, the shapes of these two models will change accordingly in the app.
You can also use custom controller models, such as pistols, bows, and wands, that best suit your apps to bring users with a more immersive app experience.
## (Recommended) Upgrade the XR Interaction Toolkit
It is recommended that you upgrade the XR Interaction Toolkit to 2.1.1 or above to use the latest Unity Input System. For how to make an upgrade, refer to the [Quickstart](/en_create-an-xr-scene#782faf9d) guide. For more information about the XR Interaction Toolkit, refer to [Unity's official article](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@2.1/manual/index.html).
## Learn more

* To learn more about Unity XR input, refer to [this article](https://docs.unity3d.com/Manual/xr_input.html).
* To learn other keycodes provided by the Unity XR Input System, refer to [this article](https://docs.unity3d.com/ScriptReference/XR.CommonUsages.html).


# --- END: Controller & HMD input mapping.md ---



# --- BEGIN: Enable interaction between the controller ray and a canvas.md ---

All UI elements should be inside a canvas. This article introduces how to create a canvas and to enable interaction between the controller ray and the canvas.
## Procedure

1. Open your project in Unity Editor.
2. In the **Hierarchy** window, click **+** > **XR** > **UI** **Canvas**.
   A Canvas object is added to the scene.
3. Select **Canvas**.
   The components and scripts for configuring the Canvas object are displayed in the **Inspector** window.
4. In the **Canvas** pane, set **Render Mode** to **World Space**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/ca586c2e8faf464b95939b0c7e0309d1~tplv-em5hxbkur4-noop.image?width=699&height=351)
5. In the **Rect Transform** pane, edit the position and scale of Canvas, making sure that it can be captured by the camera.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/1bbaeec65dd9453b813f8ae28af9bca9~tplv-em5hxbkur4-noop.image?width=701&height=464)
6. Click **Add Component** at the bottom of the **Inspector** window.
7. Add the **Tracked Device Graphic Raycaster** script to Canvas and configure parameters as needed.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/1c26c81dfe754c96812192dd87c1c9e5~tplv-em5hxbkur4-noop.image?width=858&height=288)
8. In the **Hierarchy** window, select **XR** **Origin**.
9. Expand **XR** Origin and select **LeftHand Controller**.
   The components and scripts for configuring the LeftHand Controller are displayed in the **Inspector** window.
10. In the **XR** **Ray Interactor** pane, edit **Max Raycast Distance** according to actual needs, making sure that this value is **larger** that the distance between the UI and the camera.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/7295e56e14124d449591585d55ea7656~tplv-em5hxbkur4-noop.image?width=858&height=637)
11. Configure **RightHand Controller** with the same steps as above.

## Learn more
For more information about Canvas, see [Unity official documentation](https://docs.unity3d.com/2020.1/Documentation/Manual/UICanvas.html).


# --- END: Enable interaction between the controller ray and a canvas.md ---



# --- BEGIN: Eye Tracked Foveated Rendering.md ---

Eye Tracked Foveated Rendering (ETFR) renders the image at full resolution in the area of the eye's gaze point, while rendering the peripheral area at a lower resolution. As the eye moves, the area rendered at full resolution changes accordingly. You can use ETFR to reduce the device's GPU load during the app's runtime. 
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75cbfb4abfee4d3c8664cc47c43a896b~tplv-goo7wpa0wc-image.image" width="500px" />

## Requirements

* PICO device models: ETFR only supports devices with eye tracking cameras, including PICO Neo3 Pro Eye, PICO 4 Pro, and PICO 4 Enterprise
* PICO device's system version: 5.7.0 or later

## Different levels of ETFR
The SDK provides four levels of ETFR: low, med, high, and top high. The high and top high levels bring the same effect. The following image shows to what degree the resolution is affected for different ETFR levels.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a455aa1eb4741feacb314eecea12735~tplv-goo7wpa0wc-image.image)
## ETFR vs FFR
Compared to fixed foveated rendering (FFR), ETFR can track the user's actual gaze point in real-time, allowing for greater reduction in resolution around the eye's peripheral area. FFR cannot track the user's gaze point and assumes that the user is predominantly looking at the center of the screen. Consequently, FFR takes a more conservative approach when reducing the resolution around the peripheral area. Therefore, using ETFR can bring more GPU savings for your app than FFR.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7066d2eaa2ed4b0588e1658adff9d143~tplv-goo7wpa0wc-image.image)
The following table compares GPU-related metrics between top-high level ETFR and top-high level FFR. The statistics are sourced from PICO's internal test, so they may be different from the statistics you get from actual use.
|  | **ETFR** | **FFR** |
| --- | --- | --- |
| **GPU occupation (%)** | 91.94 | 95.33 |
| **GPU frequency (MHz)** | 587 | 587 |
| **FPS** | 71.79 | 68.09 |
## Limitations
ETFR and FFR are mutually exclusive. Therefore, you can only enable one of the two modes for your app.
## Enable eye tracked foveated rendering
After enabling ETFR, relevant permission will be automatically added to the AndroidManifest.xml file.

1. Add **XR Origin** to the scene.
2. Add the **PXR_Manager** script to **XR Origin**.
3. On the **PXR_Manager (Script)** pane, complete the following:
   1. Set **Foveated Rendering Mode** to **Eye Tracking Foveation Rendering**.
   2. Set a **Foveated Rendering Level**.
      If you select Low, Med, High, or Top High, the Subsampling checkbox will appear.
      | **Level** | **Description** |
      | --- | --- |
      | None | To disable ETFR. |
      | Low | Less foveation (higher periphery visual fidelity, lower performance) |
      | Med | Medium foveation (medium periphery visual fidelity, medium performance) |
      | High  | High or top high foveation (lower periphery visual fidelity, higher performance) |
      | Top High |  |
   3. (Optional) Check the **Subsampling** checkbox.
      Subsampling is a rendering optimization technique that works in conjunction with foveated rendering. When enabled, the eye textures are laid out using subsampling to eliminate visual artifacts caused by low-resolution areas at the edges of the field of view in FFR, which improves app performance. This also results in smoother transitions when users move, reducing motion sickness.

      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7409fe23dd1b451abfc69c8305c0c8c5~tplv-goo7wpa0wc-image.image)

## Change the foveated rendering level
Call `SetFoveationLevel` to dynamically change the foveated rendering level.
```C#
// With FFR enabled, dynamically change its foveated rendering level
PXR_FoveationRendering.SetFoveationLevel(FoveationLevel.High, false);

// With ETFR enabled, dynamically change its foveated rendering level
PXR_FoveationRendering.SetFoveationLevel(FoveationLevel.High, true);
```

## Change the foveated rendering mode
**Change from ETFR to FFR:**

1. Call `SetFoveationLevel` and set the `FoveationLevel` parameter to `None`. This disables the current foveated rendering mode and level.
2. Call `SetFoveationLevel` again, set the `isETFR` parameter to `false` and specify a desired FFR level in the `FoveationLevel` parameter.

```C#
// Change from ETFR to FFR
PXR_FoveationRendering.SetFoveationLevel(FoveationLevel.None, true);
PXR_FoveationRendering.SetFoveationLevel(FoveationLevel.High, false);
```

**Change from FFR to ETFR:**

1. Call `SetFoveationLevel` and set the `FoveationLevel` parameter to `None`. This disables the current foveated rendering mode and level.
2. Call `SetFoveationLevel` again, set the `isETFR` parameter to `true` and specify a desired ETFR level in the `FoveationLevel` parameter.
   The second call may fail to be executed and, if so, call `SetFoveationLevel` a third time, set the `isETFR` parameter to `true`, and specify a desired ETFR level in the `FoveationLevel` parameter.

```C#
// Change from FFR to ETFR       
PXR_FoveationRendering.SetFoveationLevel(FoveationLevel.None, false);
PXR_FoveationRendering.SetFoveationLevel(FoveationLevel.High, true);
```

## Declare permission in AndroidManifest.xml
After enabling eye tracking for your app, the SDK automatically declares the following metadata and permission in the AndroidManifest.xml file:

* <meta-data android:name="picovr.software.eye_tracking" android:value="1"/>
* <uses-permission android:name="com.picovr.permission.EYE_TRACKING" />

Do not edit the permission declaration content if not needed. If you would like to customize the AndroidManifest.xml file, add permission declarations corresponding to the SDK features enabled for your app.
## Log analysis
After completing ETFR-related settings, the system generates the following logs:
```Plain Text
I [PxrUnity]: PicoVRSystem Pxr_SetEyeFoveationLevelEnable bSupported :true, level :3., result :0
I [PxrUnity]: PicoVRSystem Pxr_SetEyeFoveationLevelEnable bEnable :false, result :0.
I [PxrUnity]: PicoVRSystem Pxr_SetEyeFoveationLevelEnable m_RecreatingEyeTextures true. result :0
```

Below are log descriptions:
| **Row No.** | **Description** |
| --- | --- |
| 1 | * "bSupported" is used to determine if the device supports eye tracking: true (support): false (not support) <br> * "level" indicates the foveated rendering level: -1 (disabled), 0 (low), 1 (med), 2 (high), 3 (top high) <br> * "result" indicates the result of API call: 0 indicates success and other values indicate failure |
| 2 | * "bEnable" is used to determine if ETFR is enabled: true (enabled), false (disabled) <br> * "result" indicates the result of API call: 0 indicates success and other values indicate failure |
| 3 | * "m_RecreatingEyeTextures" indicates whether it is necessary to recreate eye textures: true (necessary), false (not necessary) <br> * "result" indicates the result of API call: 0 indicates success and other values indicate failure |
## API reference
Below are foveated rendering APIs. For details on parameters, returns, and more, refer to the [API reference](/reference/unity/client-api/PXR_FoveationRendering/).
| **API** | **Description** |
| --- | --- |
| `SetFoveationLevel` | Switch to a new foveated rendering mode or set a new foveated rendering level. |
| `GetFoveationLevel` | Get the current foveated rendering level. |
| `SetFoveationParameters` | Set foveated rendering-related parameters. |


# --- END: Eye Tracked Foveated Rendering.md ---



# --- BEGIN: Eye Tracking.md ---

Eye tracking is a sensor technology that enables a device to track a user's gaze in real time. Eye tracking converts a user's eye movements into data streams that contain the pupil distance, gaze vector, and gaze point as a device's input. The device then decodes the data to display to the user what the eyes are capturing in real time. 
Eye tracking enables smoother scene movement, reducing the potential dizziness users feel while using VR apps. 
## Requirements
The following are the requirements for eye-tracking-related features.
Eye tracking APIs are refactored in SDK v2.3.0. It is recommended that you upgrade the SDK to 2.3.0 or later versions, and upgrade the PICO device's system to 5.7.0 or later version to use the latest eye tracking APIs.

| **Feature** | **PICO device system version** | **PICO device** |
| --- | --- | --- |
| Eye tracking | 5.4.0 or later | Devices with eye tracking cameras, including PICO Neo3 Pro Eye, PICO 4 Pro, and PICO 4 Enterprise |
| Eye Tracking Calibration | 5.5.0 or later <br>  |  |
## Enable eye tracking and eye tracking calibration for your app

1. Open an existing scene or create a new scene in the Unity Editor.
2. In the **Hierarchy** window, click **+** > **XR** > **XR Origin (VR)**.
   The XR Origin is added to the scene. If you have not upgraded the XR Interaction Toolkit, only XR Rig will be available. Refer to the [Quickstart](/13136/en_create-an-xr-scene#782faf9d) guide for how to upgrade the XR Interaction Toolkit.
3. Select **XR Origin**.
   The **Inspector** window displays the components and scripts added to the XR Origin.
4. Click **Add Component** at the bottom of the **Inspector** window, and then add the **PXR_Manager** script to XR Origin.
5. Check the **Eye Tracking** checkbox.
   Once checked, the **Eye Tracking Calibration** checkbox appears.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f31cde68d974beeb3ff7ca91d80ed0a~tplv-goo7wpa0wc-image.image)
6. (Optional) Check the **Eye Tracking Calibration** checkbox.
   Once enabled, your app can activate the eye tracking calibration function provided by the PICO system.

## (Optional) Enable eye tracking for your device and complete eye tracking calibration

1. Turn on your VR headset.
2. Go to **Settings** > **LAB** > **Eye Tracking**.
3. Toggle the **Eye Tracking** switch.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65969db2343a449a83d61910dba863d4~tplv-goo7wpa0wc-image.image)
   The **Calibrate Eye Tracking** tab **** appears below.
4. Click **Calibrate Eye Tracking** > **Start Calibration**.
5. Follow the prompts to complete the calibration.

## Call eye tracking APIs
Call eye tracking APIs according to actual needs. 
### Query if the device supports eye tracking
Only devices with eye tracking cameras, including PICO Neo3 Pro Eye, PICO 4 Pro, and PICO 4 Enterprise, support eye tracking. Call `GetEyeTrackingSupported` to query if the current device supports eye tracking. 
### Dynamically start/stop eye tracking
Call `StartEyeTracking` and `StopEyeTracking` to dynamically start or stop eye tracking. Currently, only the binocular-tracking mode (`PXR_ETM_BOTH`) is supported. After `StartEyeTracking` is called, the system will apply for the eye tracking permission from the user through a pop-up window.
### Get the state of eye tracking
Call `GetEyeTrackingState` to get the state of eye tracking, including the information about whether eye tracking is working properly, the eye tracking mode in use, and a tracking state code.
### Get eye tracking data
Call `GetEyeTrackingData` to get eye tracking data, including the positions and orientations of both eyes. To get eye tracking data, you must call `StartEyeTracking` before calling `GetEyeTrackingData`.
### Code sample
Below is the code sample:
```C#
    private bool support = false;
    private EyeTrackingMode[] eyeTrackingModes;
 
    // Start is called before the first frame update
    void Start()
    {
        // Query if the current device supports eye tracking
        int supportModesCount = 0;
        PXR_MotionTracking.GetEyeTrackingSupported(ref support, ref supportModesCount, ref eyeTrackingModes);
        if (support)
        {
            // Start eye tracking 
            EyeTrackingStartInfo eyeTrackingStartInfo = new EyeTrackingStartInfo();
            eyeTrackingStartInfo.needCalibration = 1;
            eyeTrackingStartInfo.mode = EyeTrackingMode.PXR_ETM_BOTH;
            PXR_MotionTracking.StartEyeTracking(ref eyeTrackingStartInfo);
        }
    }
 
    // Update is called once per frame
    void Update()
    {
        if (support)
        {
            // Get the status of eye tracking
            bool tracking = false;
            EyeTrackingState eyeTrackingState = new EyeTrackingState();
            PXR_MotionTracking.GetEyeTrackingState(ref tracking, ref eyeTrackingState);
 
            // Get eye tracking data
            EyeTrackingDataGetInfo info = new EyeTrackingDataGetInfo();
            info.displayTime = 0;
            info.flags = EyeTrackingDataGetFlags.PXR_EYE_DEFAULT
            | EyeTrackingDataGetFlags.PXR_EYE_POSITION
            | EyeTrackingDataGetFlags.PXR_EYE_ORIENTATION;
            EyeTrackingData eyeTrackingData = new EyeTrackingData();
            PXR_MotionTracking.GetEyeTrackingData(ref info, ref eyeTrackingData);
        }
    }
 
    private void OnDisable()
    {
        if (support)
        {
            // Stop eye tracking
            EyeTrackingStopInfo eyeTrackingStopInfo = new EyeTrackingStopInfo();
            PXR_MotionTracking.StopEyeTracking(ref eyeTrackingStopInfo);
        }
    }
```

## App manifest
After enabling eye tracking for your app, the SDK automatically declares the corresponding permission in the AndroidManifest.xml file:

* <meta-data android:name="picovr.software.eye_tracking" android:value="1" />
* <uses-permission android:name="com.picovr.permission.EYE_TRACKING" />

Do not edit the permission declaration content if not needed. If you would like to customize the AndroidManifest.xml file, add permission declarations corresponding to the SDK features enabled for your app.
## API list
The following table lists the new eye tracking APIs provided in PXR_MotionTracking. These APIs are supported by SDK v2.3.0 or later versions. For details on parameters and returns, refer to the [PXR_MotionTracking API reference](/reference/unity/client-api/PXR_MotionTracking/). For details on deprecated eye tracking APIs, refer to the [PXR_EyeTracking API reference](/reference/unity/client-api/PXR_EyeTracking/).
| **API** | **Description** |
| --- | --- |
| `GetEyeTrackingSupported` | Get whether the current device supports eye tracking. |
| `StartEyeTracking` | Start eye tracking. |
| `StopEyeTracking` | Stops eye tracking. |
| `GetEyeTrackingState` | Get the state of eye tracking. |
| `GetEyeTrackingData` | Get eye tracking data. |
| `GetEyeOpenness` | Get the openness of both eyes. Only supported by PICO 4 Enterprise. |
| `GetEyePupilInfo` | Get the positions and diameters of the pupils of both eyes. Only supported by PICO 4 Enterprise. |
| `GetPerEyePose` | Get the pose data of the left and right eyes. Only supported by PICO 4 Enterprise. |
| `GetEyeBlink` | Get the blink data of the left and right eyes. Only supported by PICO 4 Enterprise. |


# --- END: Eye Tracking.md ---



# --- BEGIN: Face Tracking.md ---

Facial expressions are important representations of feelings, emotions, etc., especially for social interactions. In virtual scenes, facial expressions are no less important. A virtual face that is able to give accurate and vivid expressions simultaneously with users' expressive facial movements can make your app more interactive and immersive.
Each PICO 4 Pro HMD is equipped with a face tracking camera that detects and captures users' facial movements. The face tracking APIs convert captured data into blendshapes and pass them to the app for implementing face tracking. The face tracking APIs provide a set of 52 blendshapes and 20 visemes covering eye, lip, tongue, nose, cheek, brow, and jaw movements, enabling the virtual face to smile, blink, frown, etc.
## Expected effect
In the following video, the avatar moves the eyes, blinks, and opens the mouth corresponding to the user's facial movements.

         <video src=https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c3ae03f14d549bf80dc57a44a1db26b~tplv-goo7wpa0wc-image.image></video>

## Learn different face tracking modes
| **Mode** | **Description** | **Use the face tracking camera?** | **Use** **the microphone?** | **Related Facial Parts** | **Required Material** | **Remarks** |
| --- | --- | --- | --- | --- | --- | --- |
| Face Only | To track the user's face only. This mode is image-driven. | Yes | No | The whole face, including the tongue and eyeballs. | An ARKit head model. | This mode uses blend shapes numbered from 0 to 51. <br> Due to the angle limitations of the facial tracking camera, it is less sensitive in detecting subtle movements of the mouth. |
| Lipsync Only | To track the user's lips only. This mode is audio-driven, which can solely rely on the input from the microphone to drive the lip model to do relevant actions. | No | Yes | Lips, eyes, and eyebrows. | An ARKit head model or a lip model that supports viseme. | This mode only uses voice to drive the movement of the lips and adds random animations for blinking and raising eyebrows. <br> You can use blend shapes numbered from 0 to 51 to drive the ARKit head model or use blend shapes numbered from 52 to 71 to drive the viseme lip model. |
| Hybrid (Viseme) | To enable both face tracking and lipsync. This mode tracks the user's face and lips. The output format of the lip data is viseme. | Yes | Yes | The whole face, including the tongue and eyeballs. | An ARKit head model and a lip model that supports viseme. <br> For lip movements, you need to make lip animations for the ARKit model and make viseme animations as well. | This mode uses all 71 blend shapes, of which the blend shapes numbered from 52 to 71 are used to drive the viseme material. <br> This mode uses the face tracking camera and microphone to drive facial movements. Compared to the Hybrid (Blendshape) mode, this mode provides more precise mouth movements but increases art design costs. |
| Hybrid (Blendshape) | To enable both face tracking and lipsync. This mode tracks the user's face and lips. The output format of the lip data is blend shape. <br>  | Yes | Yes | The whole face, including the tongue and eyeballs. | An ARKit head model. | This mode uses blend shapes numbered from 0 to 51. <br> This mode uses the face tracking camera and microphone to drive facial movements, which is well-suited for materials that do not have viseme animations created as the algorithm internally integrates the output of visemes into the results of the first 52 blend shapes. |
## Requirements

* PICO device models:
   | **Mode** | **Device Model Requirement** |
   | --- | --- |
   | Lipsync Only | PICO Neo3 and PICO 4 series. |
   | Face Only / Hybrid (Viseme) / Hybrid (Blendshape) | PICO 4 Pro and PICO 4 Enterprise. |
* PICO device's system version: 5.7.0 or later

## Enable face tracking
### For app
Use the following steps to enable the face tracking capability for your app:

1. In the Unity Editor, create a scene or open an existing one.
2. In the **Hierarchy** window, add an **XR Origin** to the scene. Skip this step if there is already one in the scene.
3. Select **XR Origin**.
   The components and scripts for configuring XR Origin are then displayed in the Inspector window.
4. Click **Add Component** at the bottom of the Inspector window and add the **PXR_Manager** script to XR Origin.
5. Select a **Face Tracking Mode**. 
   * The PXR_Manager (Script) pane only provides the Hybrid option. Once selected, Hybrid (Viseme) mode is enabled by default. If you want to use the Hybrid (Blendshapes) mode, you need to call `StartFaceTracking` and specify `mode` to `PXR_FTM_FACE_LIPS_VIS` for the  `startInfo` parameter.
   * The Hybrid mode enables the optimal face tracking effect while resulting in the highest CPU usage. You can set different face tracking modes for different scenes according to actual needs, thereby bringing down CPU usage and enhancing app performance. For example, you can select the Face Only mode for audio-free scenes and the Lipsync Only mode for audio-only scenes.

   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6f4f3f541834791bfc51b19ee7abffe~tplv-goo7wpa0wc-image.image)

### (Optional) For device
Use the following steps to enable the face tracking capability for your device:

1. Turn on your PICO VR headset.
2. Go to **Settings** > **LAB** > **Face Tracking**.
3. Toggle the **Face Tracking** switch.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed837d7f944a444186c5edf200d769cb~tplv-goo7wpa0wc-image.image)

## Complete player settings
To improve the performance of face tracking, allow the use of C++ code in the project.

1. Go to **Edit** > **Project Settings** > **Player** > **Other Settings**.
2. Check the **Allow 'unsafe' Code** checkbox.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ae421e0aa1840a9afaa2b980101d9d0~tplv-goo7wpa0wc-image.image)

## Call face tracking APIs
Call desired face tracking APIs according to actual needs.
### Want face tracking for the current app
Before calling all other face tracking APIs, call `WantFaceTrackingService` to want face tracking for the current app.
### Query if the device supports face tracking
Call `GetFaceTrackingSupported` to query if the current device supports face tracking, which returns an array of face tracking modes the device supports and the specific modes supported.
### Dynamically start/stop face tracking

* Call `StartFaceTracking` to specify the wanted face tracking mode and start face tracking. After this API is called, the system will apply for the face tracking permission from the user through a pop-up window.
* Call `StopFaceTracking` to stop face tracking. If you set `pause` to `0` in `FaceTrackingStopInfo`, face tracking will be paused instead of being stopped.

### Switch face tracking modes
If you want to switch face tracking modes, you can first call `StopFaceTracking`, and then call `StartFaceTracking`. To switch modes quickly, you can set `pause` to `0` in `FaceTrackingStopInfo` when calling `StopFaceTracking`, which pauses face tracking instead of stopping it. Then you can call `StartFaceTracking` to select a new mode. This method reduces the time required for the startup and shutdown of face tracking, enabling faster acquisition of face tracking data.
```C#
FaceTrackingStopInfo info  = new FaceTrackingStopInfo();
info.pause = 0;
trackingState = (TrackingStateCode)PXR_MotionTracking.StopFaceTracking(ref info);
FaceTrackingStartInfo info = new FaceTrackingStartInfo();
info.mode = FaceTrackingSupportedMode.PXR_FTM_FACE_LIPS_VIS;
trackingState = (TrackingStateCode)PXR_MotionTracking.StartFaceTracking(ref info);
```

### Get the state of face tracking
Call `GetFaceTrackingState` to get the state of eye tracking, including the information about whether face tracking is working properly, the face tracking mode in use, and a tracking state code.
### Get face tracking data
Call `GetFaceTrackingData` to get face tracking data. The returns of the request includes an array with a fixed length of 72, which corresponds to the 52 blend shapes and 20 visemes. Refer to the "[Blend shape & Viseme reference](#78a6eddc)" section for details. Before calling `GetFaceTrackingData`, you must call `StartFaceTracking` to start face tracking first.
### Code sample
Below is the complete code sample:
```C#
private FaceTrackingMode[] supportedModes = { };
private FaceTrackingMode supportedMode;
private bool supported = false;
private int modeCount = 0;

void Start()
{
    // Query if the current device supports face tracking
    int ret = PXR_MotionTracking.GetFaceTrackingSupported(ref supported, ref modeCount, ref supportedModes);

    if (supported)
    {
        // Start face tracking
        FaceTrackingStartInfo info = new FaceTrackingStartInfo();
        info.mode = FaceTrackingMode.PXR_FTM_FACE;
        PXR_MotionTracking.StartFaceTracking(ref info);
    }

}

void Update()
{
    if (supported)
    {
        // Get the status of face tracking
        bool tracking = false;
        FaceTrackingState faceTrackingState = new FaceTrackingState();
        PXR_MotionTracking.GetFaceTrackingState(ref tracking, ref faceTrackingState);

        // Get face tracking data
        FaceTrackingDataGetInfo info = new FaceTrackingDataGetInfo();
        info.displayTime = 0;
        info.flags = FaceTrackingDataGetFlags.PXR_FACE_DEFAULT;
        FaceTrackingData faceTrackingData = new FaceTrackingData();
        PXR_MotionTracking.GetFaceTrackingData(ref info, ref faceTrackingData);
    }
}

private void OnDisable()
{
    if (supported)
    {
        // Stop face tracking
        FaceTrackingStopInfo info = new FaceTrackingStopInfo();
        PXR_MotionTracking.StopFaceTracking(ref info);
    }
}
```

## App manifest
Based on the face tracking mode you enable for your app, the SDK automatically declares corresponding permissions in the AndroidManifest.xml file. Do not edit the permission declaration content if not necessary. If you would like to customize the AndroidManifest.xml file, add permission declarations corresponding to the SDK features you enable for your app.
| **Mode** | **Manifest** |
| --- | --- |
| Hybrid | <meta-data android:name="picovr.software.face_tracking" android:value="false/true" /> <br> <uses-permission android:name="com.picovr.permission.FACE_TRACKING" /> <br> <uses-permission android:name="android.permission.RECORD_AUDIO" /> |
| Face Only | <meta-data android:name="picovr.software.face_tracking" android:value="false/true" /> <br> <uses-permission android:name="com.picovr.permission.FACE_TRACKING" /> |
| Lipsync Only | <meta-data android:name="picovr.software.face_tracking" android:value="false/true" /> <br> <uses-permission android:name="android.permission.RECORD_AUDIO" /> |
## Blend shape & Viseme reference
### `BlendShapeIndex` enum
```C#
enum BlendShapeIndex {
    EyeLookDown_L=0,
    NoseSneer_L=1,
    EyeLookIn_L=2,
    BrowInnerUp=3,
    BrowDown_R=4,
    MouthClose=5,
    MouthLowerDown_R=6,
    JawOpen=7,
    MouthUpperUp_R=8,
    MouthShrugUpper=9,
    MouthFunnel=10,
    EyeLookIn_R=11,
    EyeLookDown_R=12,
    NoseSneer_R=13,
    MouthRollUpper=14,
    JawRight=15,
    BrowDown_L=16,
    MouthShrugLower=17,
    MouthRollLower=18,
    MouthSmile_L=19,
    MouthPress_L=20,
    MouthSmile_R=21,
    MouthPress_R=22,
    MouthDimple_R=23,
    MouthLeft=24,
    JawForward=25,
    EyeSquint_L=26,
    MouthFrown_L=27,
    EyeBlink_L=28,
    CheekSquint_L=29,
    BrowOuterUp_L=30,
    EyeLookUp_L=31,
    JawLeft=32,
    MouthStretch_L=33,
    MouthPucker=34,
    EyeLookUp_R=35,
    BrowOuterUp_R=36,
    CheekSquint_R=37,
    EyeBlink_R=38,
    MouthUpperUp_L=39,
    MouthFrown_R=40,
    EyeSquint_R=41,
    MouthStretch_R=42,
    CheekPuff=43,
    EyeLookOut_L=44,
    EyeLookOut_R=45,
    EyeWide_R=46,
    EyeWide_L=47,
    MouthRight=48,
    MouthDimple_L=49,
    MouthLowerDown_L=50,
    TongueOut=51，
    PP=52，
    CH=53，
    o=54,
    O=55,
    I=56,
    u=57,
    RR=58,
    XX=59,
    aa=60,
    i=61,
    FF=62,
    U=63,
    TH=64,
    kk=65,
    SS=66,
    e=67,
    DD=68,
    E=69,
    nn=70,
    sil=71
};
```

### Blend shapes
The 52 blend shapes describe the movements of facial features. The following table describes the `BlendShapeIndex` enums numbered 0 to 51. The blend shapes listed below are arranged by the order of data output.
| **Index** | **Blend Shape** | **Reference Image** | **Description** | **"Hybrid" Mode** | **"Face Only" Mode** | **"Lipsync Only" Mode** |
| --- | --- | --- | --- | --- | --- | --- |
| 0 | `EyeLookDown_L` <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47e8093f3e4f4ac8b910eba5aef3947b~tplv-goo7wpa0wc-image.image) | The movement of the left eyelids consistent with a downward gaze. You need to make both the eyelid and eyeball move downward. | Valid, available to ARKit face. | Valid, available to ARKit face. <br>  | Returns 0 by default. |
| 1 | `NoseSneer_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/921fa02fffca4a3881870a18668a6511~tplv-goo7wpa0wc-image.image) | The raising of the left side of the nose around the nostril. You can add some skin folds at the root of the nose to make the expression more vivid. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 2 | `EyeLookIn_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddbe84532f25492f8f887b211f510399~tplv-goo7wpa0wc-image.image) | The movement of the left eyelids consistent with a rightward gaze. You need to deal with both the eyelid and eyeball. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 3 | `BrowInnerUp` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8dce821ba2ce49459019318950ac46de~tplv-goo7wpa0wc-image.image) | The upward movement of the inner portion of both eyebrows. You can add some skin folds at the brow bone and forehead to make the expression more vivid. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 4 | `BrowDown_R` <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd75537b57394c2fb880dce531c23691~tplv-goo7wpa0wc-image.image) | The downward movement of the outer portion of the right eyebrow. You can add some skin folds to make the express | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 5 | `MouthClose` <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7df0ac5e17a9452e8a2b23e365e5cc14~tplv-goo7wpa0wc-image.image) | The closure of the lips independent of jaw position.You need to use this with `MouthClose`. When the coefficients of `JawOpen` and `mouthClose` are the same, there should be no gap between the upper and lower lips. <br>  | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 6 | `MouthLowerDown_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb1273d45907479280b8d9f7ebbd8f53~tplv-goo7wpa0wc-image.image) | The downward movement of the lower lip on the right side. When `MouthLowerDown_L` and `MouthLowerDown_R` are both activated to `1.0`, the whole lip, including the middle part, moves downward together. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 7 | `JawOpen` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/652d1dbfb3204acab844e5a9e693a124~tplv-goo7wpa0wc-image.image) | The opening of the lower jaw.  | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 8 | `MouthUpperUp_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06dbbe0a5a3847d198f084a2f57e6149~tplv-goo7wpa0wc-image.image) | The upward movement of the upper lip on the right side. When `MouthUpperUp_L` and `MouthUpperUp_R` are both activated to `1.0`, the whole lip, including the middle area, moves upward. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 9 | `MouthShrugUpper` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fb3f9b1eff04a869a2391941fcd2bb4~tplv-goo7wpa0wc-image.image) | The outward movement of the upper lip. When `MouthShrugUpper` and `MouthShrugLower` are both activated to `1.0`, the lips are tightly closed and lifted upward, with no gap between them. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 10 | `MouthFunnel` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24541eacb3eb487dbbf28d2107a68775~tplv-goo7wpa0wc-image.image) | The contraction of both lips into an open shape. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 11 | `EyeLookIn_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf9bc09b1ecf409a874328c8d55ef01c~tplv-goo7wpa0wc-image.image) | The movement of the right eyelids consistent with a leftward gaze. You need to deal with both the eyelid and eyeball. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 12 | `EyeLookDown_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db5dc548f84249649be2db5db94dd907~tplv-goo7wpa0wc-image.image) | The movement of the right eyelids consistent with a downward gaze. You need to make both the eyelid and eyeball move downward. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 13 | `NoseSneer_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f00c17307fb4ac3be85aedcd97c957d~tplv-goo7wpa0wc-image.image) | The raising of the right side of the nose around the nostril. You can add some skin folds at the root of the nose to make the expression more vivid. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 14 | `MouthRollUpper` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0974e01805df4b59b0c26645db0c8740~tplv-goo7wpa0wc-image.image) | The movement of the upper lip toward the inside of the mouth. When `MouthRollUpper` and `MouthRollLower` are both activated to 1.0, the lips are completely pursed and the upper and lower lips cannot be seen. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 15 | `JawRight` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15e76fa0fd764c40b86777811f93a8fc~tplv-goo7wpa0wc-image.image) | The rightward movement of the lower jaw. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 16 | `BrowDown_L` <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7ca11b99a2c4c859ffeb71452e1745d~tplv-goo7wpa0wc-image.image) | The downward movement of the outer portion of the left eyebrow. You can add some skin folds to make the expression more vivid. <br>  | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 17 | `MouthShrugLower` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d309fbf355b4a209a65d88f28dc0bb7~tplv-goo7wpa0wc-image.image) | The outward movement of the lower lip. When `MouthShrugUpper` and `MouthShrugLower` are both activated to `1.0`, the lips are tightly closed and lifted upward, with no gap between them. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 18 | `MouthRollLower` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69eb937843f7413c8fd83f5a2e5fba37~tplv-goo7wpa0wc-image.image) | The movement of the lower lip toward the inside of the mouth. When `MouthRollUpper` and `MouthRollLower` are both activated to 1.0, the lips are completely pursed and the upper and lower lips cannot be seen. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 19 | `MouthSmile_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccd846ad1e2d4ab0961b6301f68960ff~tplv-goo7wpa0wc-image.image) | The upward movement of the left corner of the mouth. You need to make the left cheek move upward. When `MouthSmile_L` and `MouthSmile_R` are both activated to `1.0`, the middle area should not remain fixed, with the overall mouth looking like smiling. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 20 | `MouthPress_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbbf3ea25cc74d418bd1a476b05bf53e~tplv-goo7wpa0wc-image.image) | The upward compression of the lower lip on the left side. No need to make the cheek move. When `MouthPress_L` and `MouthPress_R` are both activated to `1.0`, the middle part should be fixed at the original position and you need to see if the mouth looks natural. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 21 | `MouthSmile_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9156965fc8324da6ba17ca7f1352b78b~tplv-goo7wpa0wc-image.image) | The upward movement of the right corner of the mouth. You need to make the right cheek move upward. When `MouthSmile_L` and `MouthSmile_R` are both activated to `1.0`, the middle area should not remain fixed, with the overall mouth looking like smiling. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 22 | `MouthPress_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6feabed473b4326b1c86d19ad51f031~tplv-goo7wpa0wc-image.image) | The upward compression of the lower lip on the right side. No need to make the cheek move. When `MouthPress_L` and `MouthPress_R` are both activated to `1.0`, the middle part should be fixed at the original position and you need to see if the mouth looks natural. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 23 | `MouthDimple_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/279234ad5ca843119a2dcf9c15abea31~tplv-goo7wpa0wc-image.image) | The backward movement of the right corner of the mouth. When activated to `1.0` with `MouthDimple_`, the whole lips should be tightened but not smiling, and you should see if the lips look natural. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 24 | `MouthLeft` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea73442605d5462da533a6c41e362737~tplv-goo7wpa0wc-image.image) | The leftward movement of both lips together. You also need to make the left cheek move upward to make the mouth look crooked. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 25 | `JawForward` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0be80124fb234548ab74c2f27b3d4d82~tplv-goo7wpa0wc-image.image) | The forward movement of the lower jaw. <br>  | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 26 | `EyeSquint_L` <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edb9852380da4195bc14e601da7fc0ce~tplv-goo7wpa0wc-image.image) | The contraction of the face around the left eye. <br>  | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 27 | `MouthFrown_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b37c6bdb47344f7e94b2c11696f3a80e~tplv-goo7wpa0wc-image.image) | The downward movement of the left corner of the mouth. The left cheek should also move downward. When both `MouthFrown_L` and `MouthFrown_R` are activated to `1.0`, both the left and right corners of the lips should move downward naturally. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 28 | `EyeBlink_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc8f4009514842478e9bfeb1c043cec2~tplv-goo7wpa0wc-image.image) | The closure of the eyelids over the left eye. Recommend making the left eye completely closed when `EyeBlink_L` is activated to `0.8`. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 29 | `CheekSquint_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57dd569c45034476927e242784720b58~tplv-goo7wpa0wc-image.image) | The upward movement of the cheek around and below the left eye, which is usually used to make a smiling expression. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 30 | `BrowOuterUp_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d9965412d8e46869f97616c40bc3d13~tplv-goo7wpa0wc-image.image) | The upward movement of the outer portion of the left eyebrow. You can add some skin folds at the brow bone and forehead to make the expression more vivid. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 31 | `EyeLookUp_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95ed200fb0e2400d97f0ba38051efdab~tplv-goo7wpa0wc-image.image) | The movement of the left eyelids consistent with an upward gaze. You need to make both the eyelid and eyeball move upward. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 32 | `JawLeft` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b0b823c5a454919a1f539d5ffcc05d3~tplv-goo7wpa0wc-image.image) | The leftward movement of the lower jaw. Do not make it a crooked mouth. <br>  | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 33 | `MouthStretch_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd731acb656147ee9b6867ea1ea149af~tplv-goo7wpa0wc-image.image) | The leftward movement of the left corner of the mouth. You need to make the left cheek move downward so that the moth stretches wider. When `MouthStretch_L` and `MouthStretch_R` are both activated to 1.0, you need to see if the mouth looks natural. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 34 | `MouthPucker` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f15b915a0c4644c480daa40ef9f86f40~tplv-goo7wpa0wc-image.image) | The contraction and compression of both closed lips. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 35 | `EyeLookUp_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f71b1b2b0b94d5ca01252aae0b5bbc4~tplv-goo7wpa0wc-image.image) | The movement of the right eyelids consistent with an upward gaze. You need to make both the eyelid and eyeball move upward. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 36 | `BrowOuterUp_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e44f5ca1271146d1a03aa2f7482c0d80~tplv-goo7wpa0wc-image.image) | The upward movement of the outer portion of the right eyebrow. You can add some skin folds at the brow bone and forehead to make the expression more vivid. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 37 | `CheekSquint_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b2b278167e9486d8c1ef764ef35a461~tplv-goo7wpa0wc-image.image) | The upward movement of the cheek around and below the right eye, which is usually used to make a smiling expression. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 38 | `EyeBlink_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18443a1aeb754f3a8ca835588940c43c~tplv-goo7wpa0wc-image.image) | The closure of the eyelids over the right eye. Recommend making the right eye completely closed when `EyeBlink_R` is activated to `0.8`. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 39 | `MouthUpperUp_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/032bbf3a65a444a88a568db582b6f876~tplv-goo7wpa0wc-image.image) | The upward movement of the upper lip on the left side. When `MouthUpperUp_L` and `MouthUpperUp_R` are both activated to `1.0`, the whole lip, including the middle area, moves upward. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 40 | `MouthFrown_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1ddd05903f0452594c388424b069968~tplv-goo7wpa0wc-image.image) | The downward movement of the right corner of the mouth. The right cheek should also move downward. When both `MouthFrown_L` and `MouthFrown_R` are activated to `1.0`, both the left and right corners of the lips should move downward naturally. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 41 | `EyeSquint_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4daac66d3300477d941092529b6e6b21~tplv-goo7wpa0wc-image.image) | The contraction of the face around the right eye. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 42 | `MouthStretch_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27b06227a5be4008b7eca90bfe9eb7f3~tplv-goo7wpa0wc-image.image) | The rightward movement of the right corner of the mouth. You need to make the right cheek move downward so that the moth stretches wider. When `MouthStretch_L` and `MouthStretch_R` are both activated to 1.0, you need to see if the mouth looks natural. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 43 | `CheekPuff` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74d24d02274a4f96b58975a171c918e5~tplv-goo7wpa0wc-image.image) | The outward movement of both cheeks. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 44 | `EyeLookOut_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecc83b53e81f4040b4378db68fc67487~tplv-goo7wpa0wc-image.image) | The movement of the left eyelids consistent with a leftward gaze. You need to deal with both the eyelid and eyeball. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 45 | `EyeLookOut_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed71923c14d34789b990f3723037aade~tplv-goo7wpa0wc-image.image) | The movement of the right eyelids consistent with a rightward gaze. You need to deal with both the eyelid and eyeball. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 46 | `EyeWide_R` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/472ea42877a04545a4a94e3e90cd0677~tplv-goo7wpa0wc-image.image) | The widening of the eyelids around the right eye. If you want to appear surprised, you can expose the whole eye and part of the sclera of the eye. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 47 | `EyeWide_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1f3e4a2447b44fab3c60610d45ea736~tplv-goo7wpa0wc-image.image) | The widening of the eyelids around the left eye. If you want to appear surprised, you can expose the whole eye and part of the sclera of the eye. <br>  | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
| 48 | `MouthRight` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bdb5f9544164c6b8158f076e7b1d28e~tplv-goo7wpa0wc-image.image) | The rightward movement of both lips together. You also need to make the right cheek move upward to make the mouth look crooked. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 49 | `MouthDimple_L` <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/101ec2dac69f4a0f9b5aa9982b75d0da~tplv-goo7wpa0wc-image.image) | The backward movement of the left corner of the mouth. When activated to `1.0` with `MouthDimple_`, the whole lips should be tightened but not smiling, and you should see if the lips look natural. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 50 | `MouthLowerDown_L` | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88b5faffbf7c4f61867357dcf1177a48~tplv-goo7wpa0wc-image.image) | The downward movement of the lower lip on the left side. When `MouthLowerDown_L` and `MouthLowerDown_R` are both activated to `1.0`, the whole lip, including the middle part, moves downward together. | Valid, available to ARKit face. | Valid, available to ARKit face. | Valid, available to ARKit face. |
| 51 | `TongueOut` | / | The extension of the tongue. | Valid, available to ARKit face. | Valid, available to ARKit face. | Returns 0 by default. |
### Visemes
PICO's Lipsync capability maps human speech to a set of mouth shapes using visemes. Visemes are visual analogs of phonemes that are used to simulate natural mouth movements. Each viseme depicts the mouth shape for a specific set of phonemes. The following table describes the `BlendShapeIndex` enums numbered 52 to 71. The blend shapes listed below are arranged by the order of data output.
| **No.** | **Viseme ID** | **Phonemes (Chinese)** | **Phonemes (English)** | **Reference Image** | **"Hybrid" Mode** | **"Face Only" Mode** | **"Lipsync Only" Mode** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 52 | PP | `p`, `b`, `m` <br> e.g., 坡，波，末 <br>  | `p`, `b`, `m` <br> e.g., pat, bat, mat <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7eb1b561fd0489290fd207305b8ee0c~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 53 | CH | `zh`, `ch`, `sh` <br> e.g., 知，吃，事 | `dZ`, `tS`, `S` <br> e.g., join, chip, ship <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f009c0f6a90c492889b4d63c21208fed~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 54 <br>  | o <br>  | `o` <br> e.g., 破，喔 <br>  | `aw` <br> e.g., law <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a52094167172422483671731d9c58188~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 55 | O | `ou`, `ao` <br> e.g., 走，好 | `ow` <br> e.g., how <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f781a2ecf924bfba1dbf2cbd88fe58f~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 56 | I | `i` (back) (ai, ei, ui, etc.） <br> e.g., 海，黑，灰 | `ih` (stressed) <br> e.g., lip <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f3603d1e49f492d8f697ea398856943~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 57 <br>  | u | `ü` <br> e.g., 绿 | - | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e7ce2e1e2f74fefabff3c8011793870~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 58 | RR | `r` <br> e.g., 日 | `r` <br> e.g., room | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/858569555afe49f1ba22895f7d20472c~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 59 | XX | `j`, `q`, `x`, `y` <br> e.g., 及，期，戏，宜 | `jh` <br> e.g., year <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad992f88787d408e80a36f88e0a28426~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 60 | aa | `a` <br> e.g., 那 | `ɑː` <br> e.g., car | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd8dd579e2924b18beb36dada414636b~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 61 <br>  | i <br>  | `i` (front) (ie, in, ian, etc.)  <br> e.g., 列，林，连 <br>  | `ih` (unstressed) <br> e.g., lip <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae0bc637334f4a3cbb6c7fe964900922~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 62 | FF | `f` <br> e.g., 发，佛 | `f`, `v` <br> e.g., for, vow | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e22166f98e5d4b9ab6740a5bc948fcd8~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 63 | U | `u`, `w` <br> e.g., 露，舞 | `ou` <br> e.g., book | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bec63836bc64ff0bb171876f5aa3e04~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 64 | TH | `th` <br>  | `th` <br> e.g., think, that | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/977d6ef68ded46b2a619e2d629056f77~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 65 | kk | `g`, `k`, `h` <br> e.g., 歌，可，河 <br>  | `g`, `h`, `k` <br> e.g., good, who, cool | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46e309d679ca4c69a02714ff92dd48c9~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 66 | SS | `z`, `c`, `s` <br> e.g., 思，紫 | `z`, `s` <br> e.g., zoo, see | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76b9d772fef342f7b57ebbde3e9ed97e~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 67 <br>  | e <br>  | `e` <br> e.g., 么，呢 | - | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b0954f2b04d468cbd9736a8b9ad1f39~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 68 | DD | `d`, `t` <br> e.g., 得，特 | `d`, `t` <br> e.g., doll, tall | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59a2454484c74c8bac6f2d983ed90ebb~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 69 | E | `ie`, `ei` <br>  | `e` <br> e.g., bed | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f0542d004d14c73bdd8ee91ca96185a~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 70 | nn | `n`, `l` <br> e.g., 呢，乐 | `n`, `l` <br> e.g., not, lot | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83475127cc1e41f19495fd0e9b4cf92b~tplv-goo7wpa0wc-image.image) | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
| 71 | sil | - | - | - | Valid, available to Viseme mouth shape. | Returns 0 by default. | Valid, available to Viseme mouth shape. |
## API reference
The following table lists the newly designed face tracking APIs in PXR_MotionTracking, which are available in SDK 2.3.0 or later versions. For details on parameters, returns, and more, refer to the [PXR_MotionTracking API reference](/reference/unity/client-api/PXR_MotionTracking/).
| **API** | **Description** |
| --- | --- |
| `WantFaceTrackingService` | Want the face tracking service for the current app. |
| `GetFaceTrackingSupported` | Get whether the current device supports face tracking. |
| `StartFaceTracking` | Start face tracking. |
| `StopFaceTracking` | Stop face tracking. |
| `GetFaceTrackingState` | Get the state of face tracking. |
| `GetFaceTrackingData` | Get face tracking data. |
The following table lists the face tracking APIs provided in PXR_System, which are available in SDK 2.1.4 or later versions. For details on parameters, returns, and more, refer to the [PXR_System API reference](/reference/unity/client-api/PXR_System/?v=3.0.0).
| **API** | **Description** |
| --- | --- |
| `EnableFaceTracking` | Enable/disable face tracking. |
| `EnableLipSync` | Enable/disable lipsync. |
| `GetFaceTrackingData` | Get face tracking data. |
| `SetFaceTrackingStatus` | Switch the face tracking mode. |


# --- END: Face Tracking.md ---



# --- BEGIN: Fixed Foveated Rendering.md ---

In the human visual system, the eyes provide both the foveal and peripheral visions. The foveal vision is optimized for presenting highly detailed and accurate objects, whereas the peripheral vision is optimized for organizing the broad spatial scene, which gives rise to the foveated rendering system that is widely applied in VR apps.
Foveated rendering provides full resolution in the central field of view and lowers the resolution in the peripheral field of view (outside of the gaze point), which dramatically reduces computational complexity and therefore improves app performance. 
For **** fixed foveated rendering, the gaze point is fixed in the center of view and the resolution decreases from the center to the peripheral area.
## About subsampling
Starting from version 2.1.5, the SDK supports subsampling, a rendering optimization technique that works in conjunction with foveated rendering. When enabled, the eye textures are laid out using subsampling to eliminate visual artifacts caused by low-resolution areas at the edges of the field of view in FFR, which improves app performance. This also results in smoother transitions when users move, reducing motion sickness.
## How foveated rendering affects resolution
The PICO Unity Integration SDK provides four levels of foveated rendering: Low, Med, High, and Top High. The following figures demonstrate to what degree the resolution is affected.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e70a94748da45f3b421630a00942116~tplv-goo7wpa0wc-image.image)
## Expected effect
The rendering effects of low, med, and high-level fixed foveated rendering are as shown below:
| **Low** | **Med** | **High & Top High** |
| --- | --- | --- |
|    ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/1e9698d0df2b4cef9e0e39fe75811fc3~tplv-em5hxbkur4-noop.image?width=295&height=324) |    ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/ea708df9467145ca8b658757953f7701~tplv-em5hxbkur4-noop.image?width=295&height=325) |    ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/12ca4310894e4ef6a3e9a647b05c34ec~tplv-em5hxbkur4-noop.image?width=295&height=321) |
## Set a foveated rendering level

1. Open an existing scene or create a new scene in the Unity Editor.
2. In the **Hierarchy** window, click **+** > **XR** > **XR Origin (VR)** to add the XR Origin.
3. Select **XR Origin**.
   The Inspector window displays the components and scripts added to XR Origin.
4. Click **Add Component** at the bottom of the **Inspector** window, then add the **PXR_Manager** script to XR Origin.
5. Complete the following steps on the **PXR_Manager (Script)** pane.
   1. Set **Foveated Rendering Mode** to **Fixed Foveated Rendering**.
   2. Select a **Foveated Rendering Level**.
      'None' indicates disable fixed foveated rendering. If you select 'Low', 'Med', 'High', or 'Top High', the 'Subsampling' checkbox will appear.
   3. (Recommended) Check the **Subsampling** checkbox to enable subsampling.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3999fb533d71450e8de91f207bc8707f~tplv-goo7wpa0wc-image.image)

## Known issues

* If you use the Universal Render Pipeline (URP) in your project and you enable fixed foveated rendering, fixed foveated rendering may not work.
   * **Cause 1**: At present, fixed foveated rendering is tied to the eye buffer. However, with the introduction of intermediate texture in URP, graphics will be rendered to the intermediate texture first, instead of the eye buffer, which causes fixed foveated rendering to fail.
      **Solution**: Disable post-processing, HDR, and the renderer feature that uses the intermediate texture.
   * **Cause 2**: In URP 10.10.1, the behavior of setting a camera's **Clear Flags** has changed. Specifically, if you choose **Skybox**, the Invalidate setting for Color Attachment will be lost, which will cause the failure of fixed foveated rendering.
      This issue may also exist in versions later than 10.10.1, and what happens in your actual use shall prevail.

      **Solution**: As shown in the figure below, comment out the `CameraClearFlags.Skybox` part in the `GetCameraClearFlag` method of `ScriptableRenderer`, thereby making it return `ClearFlag.All` as well.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9807f4ab1c6d4902898fff8e1bf2123f~tplv-goo7wpa0wc-image.image)
* If you use the Built-in Render Pipeline, you will also need to disable post-processing, otherwise fixed foveated rendering will not work.
* If your project uses OpenGLES graphics API, Gamma color space, and fixed foveated rendering at the same time, subsampling cannot be enabled.

## API reference
You can call foveated rendering APIs to get or set foveated rendering levels and customize foveated rendering parameters. Below is the API list, for details on parameters and returns, refer to the [API reference](/reference/unity/client-api/PXR_FoveationRendering/).
| **API** | **Description** |
| --- | --- |
| SetFoveationLevel | Set a foveated rendering level for the current app. |
| GetFoveationLevel | Get the foveated rendering level of the current app. |
| (Deprecated) SetFoveationParameters | Set foveated rendering parameters for the current app. |


# --- END: Fixed Foveated Rendering.md ---



# --- BEGIN: Focus Awareness.md ---

Focus awareness allows the system UI to be displayed as an overlay on top of a scene. Therefore, players can access the system UI without exiting the current application to have an uninterrupted immersive XR experience.
## Notes

* Only events are provided. No API.
* If you do not enable this feature for your app, 4 controller models may overlap on the screen when users click the Home button.

## Focus events
The focus events are described as follows:
| **Event** | **Description** |
| --- | --- |
| PXR_Plugin.System.FocusStateLost | This event indicates that the application has lost input focus. <br> For example, if a player presses the **Home** button on the controller while an application is running, the system UI will show up, causing the application to lose focus. At this time, the developer can pause the application, and disable this player's input capability (e.g., the controller) or notify other online players that this player is not focusing on the current application. |
| PXR_Plugin.System.FocusStateAcquired | This event indicates that the application has acquired input focus. <br> When the system UI is closed by a player, this event will be triggered. At this time, the developer can continue the application and re-enable this player's input capability. |


# --- END: Focus Awareness.md ---



# --- BEGIN: Haptic Feedback.md ---

PICO 4 controllers are equipped with broadband linear motors. Together with the SDK's capability, they enable haptic feedback that is demonstrated through controller vibrations. The frequency of vibration is between 50 and 500Hz, which makes it possible to simulate most haptic output in the real world, thereby giving users a wonderful haptic experience.
## Non-buffered haptics
Non-buffered haptics are usually triggered by events and provide relatively simple effects. You can set vibration properties to achieve desired haptic effects.
### Supported devices
PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series.
### Enable haptics
You can call `SendHapticImpulse` (formerly `SetControllerVibrationEvent` or `SetControllerVibration`) to set up non-buffered haptics for controllers, including setting which controller to vibration, the vibration strength (amplitude), frequency, and duration. The valid vibration frequency ranges from 50 to 500Hz. The higher the frequency, the subtler the vibration. You can set a vibration amplitude from 0 to 1. The higher the value, the stronger the vibration. Below is an example of API call:
```C#
//To enable non-buffered haptics for the right controller, set the amplitude to 0.5, the duration to 500ms, and the frequency to 100Hz
PXR_Input.SendHapticImpulse(VibrateType.RightController, 0.5f, 500, 100) 
```

To stop vibration, call this API again and set both `amplitude` and `duration` to `0`.
### Tips for use
Recommended frequencies vary by event type. In general, use low frequencies to indicate soft-body collisions and high frequencies for rigid-body collisions. Below are detailed instructions.
| **Event Type** | **Recommended Frequency** |
| --- | --- |
| Playing drums, playing basketball | Low frequency, which is between 50 and 100Hz. |
| Shooting, playing ping pong | Intermediate frequency, which is about 170Hz. |
| Stone collision | High frequency, which is about 300Hz. |
## Buffered haptics
With buffered haptics, your app sends a buffer of haptic data (audio data) to specified controller(s) to trigger haptic feedback. Buffered haptics are usually used in music games or any scenes that are integrated sound effects. When there is a change in sound properties such as volume, pitch, and rhythm, the controller(s) can provide haptics to notify users.
### Supported device
PICO 4 series and PICO 4 Ultra series.
### Important notes

* Buffered haptics support the following audio formats: MP3, WAV, and OGG.
* Buffered haptics do not support setting vibration durations. The duration is determined by the duration of the audio file.

### Enable haptics
**Buffered** **haptics** are triggered by the haptic data (audio data) from audio files or PICO haptic files (.phf). The haptics for the left and right controllers are controlled by the left and right channels separately. You can choose to enable vibration for one or both controllers and set the vibration parameters, including amplitude, channel inversion, cache type, etc. Channel inversion is controlled by the `channelFlip` parameter. When enabled, the audio data from the left (right) channel will be used as the source data for the right (left) controller.
Each haptic has a source ID as its unique identifier which is returned by the `sourceID` parameter. You need to define `sourceID` in your code so as to retrieve haptics' source IDs for further operations, such as updating, stopping, pausing, or resuming specified haptics. Use the following APIs to enable buffered haptics:
| **API** | **Description** | **Remarks** |
| --- | --- | --- |
| `SendHapticBuffer` (formerly `StartControllerVCMotor`) | Enable haptic feedback for specified controller(s). The haptic data comes from the audio file stored in the AudioClip component in the Unity Engine. | The algorithm calculates vibration amplitudes and frequencies based on the sound properties such as the pitch and volume of the audio stream. |
| `SendHapticBuffer` (formerly `StartVibrateBySharem`) | Enable PCM haptic effect for specified controller(s). The PCM data is converted from the audio file stored in the AudioClip component in the Unity Engine. | Pulse-code modulation (PCM) samples, quantizes, and encodes continuously changing analog signals to create digital signals, which enables high-fidelity haptic effects. |
| `SendHapticBuffer` (formerly `StartVibrateByPHF`) | Enable haptic feedback for specified controller(s). The haptic data comes from the PICO haptic file (.phf). | PICO Haptic File (.phf) is a highly customizable haptic data file format developed by PICO. |
| `StartHapticBuffer` (formerly `StartVibrateByCache`) | Start a specified haptic. The haptic should have cached data. | If you select "cache and stop vibrating" (`CacheNoVibrate`) when using the above APIs, you need to call this API to start a specified haptic feedback after data caching. <br> ***Note***: If you consecutively call this API, the haptic data generated by the previous call will be overwritten by the latter one. |
Below are example API calls:
```C#
// Use the audio file to enable haptic feedback for the right controller, disable channel inversion, and let it cache while stopping vibration.
PXR_Input.SendHapticBuffer(PXR_Input.VibrateType.RightController, audioClip, PXR_Input.ChannelFlip.No, ref sourceid, PXR_Input.CacheType.CacheNoVibrate);

// Use PCM data to enable haptic feedback for the left controller, enable channel inversion, and don't cache.
PXR_Input.SendHapticBuffer(PXR_Input.VibrateType.LeftController, pcmData, buffersize, frequency, channelMask, PXR_Input.channelFlip.Yes, ref sourceId, CacheType.DontCache)

// Use the PHF file to enable haptic feedback for both controller, disable channel inversion, and use the standard amplitude.
PXR_Input.SendHapticBuffer(PXR_Input.VibrateType.BothController, phf_text, PXR_Input.ChannelFlip.No, 1, ref sourceid);
```

### Update haptic settings
You can call `UpdateHapticBuffer` (formerly `UpdateVibrateParams`) to update settings, including the vibrating controller, channel inversion, and vibration amplitude, for a specified haptic. The target haptic is specified by the `sourceID` parameter. Below is an example API call:
```C#
PXR_Input.UpdateHapticBuffer(sourceid, PXR_Input.VibrateType.LeftController, PXR_Input.ChannelFlip.No, 2);
```

### Stop/pause/resume haptics
You can call the following APIs to control target haptics that are specified by the `sourceID` parameter.
| **API** | **Description** | **Remarks** |
| --- | --- | --- |
| `StopHapticBuffer` (formerly `StopControllerVCMotor`) | Stops a specified buffered haptic. | If a haptic has cached data, you can choose whether to clear the data. By default, the cached data is reserved. |
| `PauseHapticBuffer` (formerly `PauseVibrate`) | Pauses a specified buffered haptic. | If you want to resume a paused haptic, call `ResumeHapticBuffer`. |
| `ResumeHapticBuffer` (formerly `ResumeVibrate`) | Resumes a paused haptic. | / |
Below are example API calls:
```C#
// Stop a buffered haptic
PXR_Input.StopHapticBuffer(sourceid);

// Pause a buffered haptic
PXR_Input.PauseHapticBuffer(sourceid);

// Resume a paused buffered haptic
PXR_Input.ResumeHapticBuffer(sourceid);
```

## API reference
For more information about APIs, such as the descriptions of input parameters and returns, refer to the [API reference](/reference/unity/client-api/PXR_Input/).


# --- END: Haptic Feedback.md ---



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



# --- BEGIN: Mixed Reality Capture.md ---

Mixed Reality Capture (MRC) enables the blend of physical and virtual worlds. With mixed reality capture, real-world people can replace avatars to appear in virtual scenes.
MRC can greatly empower the creation of VR videos. Users can record mixed reality videos to mark down their interactions with the virtual world and share videos on social platforms. In addition, with the continuous development of the MRC technology, MRC can bring us immersive and unique experiences in more and more scenarios such as education, recreation, and meetings.
## Expected effect
Below is what a mixed reality video looks like:
<video src=https://sf3-cdn-tos.huoshanstatic.com/obj/vcloud/1f989c1e0ca0aeea795c6c109319d6bd-.mp4></video>
## Requirements

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series
* PICO device's system version: 4.7.0 or later

## Important note
When using MRC, make sure that the tag of the main XR camera in the scene has been set to **MainCamera**. If you change the XR camera, make sure to set the new XR camera's tag to **MainCamera**; otherwise, MRC will not work.
## Enable MRC for your app
You can enable the mixed reality capture capability for your app. Below are the steps to follow:

1. In the Unity Editor, open an existing scene or create a new one.
2. In the **Hierarchy** window, add **XR Origin** to the scene. Skip this step if there is already one in the scene.
   If you have not upgraded the XR Interaction Toolkit to the latest version, the object name will be XR Rig. Refer to the [Quickstart](/13136/en_create-an-xr-scene#782faf9d) guide for how to upgrade the XR Interaction Toolkit.
3. Set the **Tag** of the main XR camera (generally the Main Camera under XR Origin) to **MainCamera**. This is typically the default setting.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d884d4c595874f718d374aeea4db630a~tplv-goo7wpa0wc-image.image)
4. Select **XR** **Origin** and add the **PXR_Manager** script to it.
5. Check the **MRC** checkbox. This is typically the default setting.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30b234950ea6423bb6adfd3ab375456a~tplv-goo7wpa0wc-image.image)
   The ""true" in XR Origin" information appears in the `openMRC` field, indicating that the MRC capability has been enabled for your app. You can check this by opening the PXR_Manager.cs file in a code editor.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b12c1133b9a94a95acda7c39627715e9~tplv-goo7wpa0wc-image.image)
6. Configure MRC-related parameters.
   | **Parameter** | **Description** |
   | --- | --- |
   | foreground Layer Masks | Select the layer(s) for foreground camera recording. The selected layer(s) will be displayed in front of the user in the video. |
   | back Layer Masks | Select the layer(s) for rear view camera recording. The selected layer(s) will be displayed behind the user in the video. |
7. Go to **Edit** > **Project Settings** > **Player** > **Other Settings**, set **Color Space*** to **Linear**. 
   When using the MRC feature, if you set the graphics API as Vulkan and the color space as Gamma at the same time in your Unity project, it can lead to a significant drop in frame rates. Therefore, if you are using the Vulkan graphics API, it is essential to complete this step; otherwise, you can skip it.

## Log analytics
You can refer to the following logs to determine whether MRC has been enabled.
MRC disabled:
```Plain Text
117602: 04-19 15:06:28.058 21630  3841 I Unity   : PXR MRC Awake openMRC = False ,MRCInitSucceed = False.
```

MRC enabled:
```Plain Text
167204: 04-19 14:56:18.797  5650 31586 I Unity   : PXR MRC Awake openMRC = True ,MRCInitSucceed = False.
167541: 04-19 14:56:18.813  5650 31586 I Unity   : PXR MRC cameraDataLength: 10
167598: 04-19 14:56:18.826  5650 31586 I Unity   : PXR MRC cameraData: 0: 1920
167607: 04-19 14:56:18.826  5650 31586 I Unity   : PXR MRC cameraData: 1: 1080
167616: 04-19 14:56:18.826  5650 31586 I Unity   : PXR MRC cameraData: 2: 38.50488
167625: 04-19 14:56:18.826  5650 31586 I Unity   : PXR MRC cameraData: 3: 0.4115266
167634: 04-19 14:56:18.827  5650 31586 I Unity   : PXR MRC cameraData: 4: 0.4536189
167643: 04-19 14:56:18.827  5650 31586 I Unity   : PXR MRC cameraData: 5: -0.5702769
167652: 04-19 14:56:18.827  5650 31586 I Unity   : PXR MRC cameraData: 6: -0.02062303
167661: 04-19 14:56:18.827  5650 31586 I Unity   : PXR MRC cameraData: 7: 0.7954143
167670: 04-19 14:56:18.828  5650 31586 I Unity   : PXR MRC cameraData: 8: 0.005452859
167680: 04-19 14:56:18.828  5650 31586 I Unity   : PXR MRC cameraData: 9: 0.6056905
167816: 04-19 14:56:18.839  5650 31586 I Unity   : PXR MRC Init Succeed.
169180: 04-19 14:56:19.013  5650 31586 I Unity   : PXR MRC Pxr_GetMrcLayerImage createMRCOverlaySucceed : true.
169273: 04-19 14:56:19.029  5650 31586 I Unity   : PXR MRC Camera created. mrcPlay is true.
77087: 04-19 14:56:20.793  5650 31586 I Unity   : PXR MRC Pxr_GetMrcY+:0.1921037
```

## Test and debug
You can test if your app's MRC capability works well using a mobile phone and a PICO device.
### Before you begin
Before debugging, do the following:

* Prepare the following devices and accessories:
   * A PICO device (Neo3 or later).
   * A mobile phone. For iPhone, the system version should be iOS12 or later. For Android phones, there is no system version requirement. It is recommended to use a phone that boasts superior performance whenever possible.
   * A tripod for placing your mobile phone.
* Install the "PICO VR" app on your mobile phone.
* Install the "Mixed Reality Capture" app on the PICO device.
* Connect your mobile phone and PICO device to the same WLAN.
* Log in to your PICO device and the "PICO VR" app with the same PICO user account.

### Procudure
Follow the steps below to debug MRC for your app:

1. Install your app on the PICO device.
2. Place the tripod in an appropriate position and place the mobile phone on it. Make sure that the phone's rear cameras are facing you.
3. Put on the headset and launch the "Mixed Reality Capture" app.
4. Follow the on-screen instructions to complete setups and then record mixed reality videos.

## Troubleshooting
### The video is in first-person view
If the recorded video is in first-person view, it indicates that MRC has not taken effect. Below are possible causes and troubleshooting methods:
| **Cause** | **Troubleshooting Method** |
| --- | --- |
| The MRC checkbox is not checked on the PXR_Manager (Script) pane <br>  | For SDK v2.1.3 and v2.1.4, check if the log includes `Pxr_GetMrcY`. If not, it indicates that MRC is not enabled. <br> For SDK v2.1.5 and later versions, check out the log to see if `openMRC` is `False`. If not, it indicates that MRC is not enabled. <br> ```C# <br> // The log for SDK v2.1.5 and later versions <br> I Unity   : PXR MRC Awake openMRC = False,MRCInitSucceed = False.   <br> ``` <br>  |
| The MRC process is blocked | If there are errors in the lifecycle of the `MonoBehaviour` class, it will block the lifecycle of the PXR_Manager.cs file. Consequently, MRC-related codes cannot be executed, blocking the MRC process. |
| Abnormal calibration data interrupts the initialization process | Check out the log to see if there is abnormal calibration data. If there is, it indicates that the issue is caused by the calibration app instead of the SDK. <br> ```C# <br> I Unity   : PXR MRC  Abnormal calibration data  <br> ``` <br>  <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68238e4f2fd1455c9a65262e48729bbd~tplv-goo7wpa0wc-image.image) |
| The URP configuration file is not set <br>  | 1. Firstly, check out the log to see if MRC is successfully initialized. <br> 2. Then, launch the app and set `loglevel=8` to see if the APIs in `OnPreRenderCallBack` and `OnPostRenderCallBack` are executed at every frame. <br>    ```C# <br>     // The command for setting loglevel=8  <br>     adb shell am broadcast -a android.intent.action.loglevel_refresh --ei "plugin_loglevel" 8 --ei "xrUnityLogLevel" 8 <br>    ``` <br>  <br>  <br> If MRC has been initialized successfully but the process is being blocked, resulting in the failure of the monitored `Camera` event to proceed, it is because the URP configuration file is not set, causing the callback functions `OnPreRenderCallBack` and `OnPostRenderCallBack` in the PXR_Manager.cs file to not be executed. |
### The virtual scene is too small
The position value of the third-person camera written in the XML file is incorrect. 

* `cameraData：3`: camera's position on the X axis (unit: meter)
* `cameraData：4`: camera's position on the Y axis (unit: meter)
* `cameraData：5`: camera's position on the Z axis (unit: meter)

You can determine if the above three values are accurate according to the mobile phone's position relative to the HMD's position. In the following example, the value of `cameraData：5` is `24.7`, indicating that the mobile phone is located 24.7 meters directly in front of the HMD, which significantly exceeds the distance between the phone and the HMD during normal recording, causing the virtual scene to be too small.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b7f679c0c98475d80643356ffa72ccd~tplv-goo7wpa0wc-image.image" width="500px" />


# --- END: Mixed Reality Capture.md ---



# --- BEGIN: MR Safeguard.md ---

When the distance between the objects in the virtual scene and the PICO headset or controllers is within a certain range, the virtual scene will become semi-transparent, revealing the real-world scene. While ensuring user safety, the MR Safeguard capability can maximize the immersive experience for your app.
## Tech summary
When the detection ball surrounding the headset or controller collides with the mesh in the space, the real-world environment becomes visible.
| **Device** | **Detection Ball Radius** | **Expertec Effect** |
| --- | --- | --- |
| HMD | 20cm | The overall physical environment becomes visible. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2d13556a4fb4595b3624d1237ae30dc~tplv-goo7wpa0wc-image.image) |
| Controllers | 10cm | A circular area with the center at the centroid of the detection ball and a radius equal to the ball's radius becomes visible. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15c54288237042afa48733b449de5169~tplv-goo7wpa0wc-image.image) |
## Why do we need MR safeguard？
In the brand-new MR app experience, users can see the real environment around them and can freely choose to interact with the real environment and with virtual objects or virtual environments according to their current needs.
The traditional VR safety boundary can no longer meet the expectations of users for a good experience in this situation for the following reasons:

* It restricts the user's range of movement;
* It displays a fence when the user approaches the boundary;
* Once the user steps out of the boundary, they can no longer interact with the virtual content in the app.

Therefore, PICO proposes a new MR safeguard system, aiming to provide users with a more natural, friendly, and comfortable MR system experience while ensuring their safety:

* Users can move around in the real environment without the display of safety boundaries;
* Users can interact with both real objects and virtual objects or virtual environments;
* The system will only alert users when they approach obstacles with the view obscured by virtual objects or virtual environments.

## What types of apps can use MR safeguard?
MR Safeguard mode is still experimental, and currently, it can only be applied for use if the following conditions are met:

* The seethrough feature must be enabled throughout the process, allowing users to view the real world without any obstacles.
* There should be no long-term, large-scale virtual scene that blocks the user's view, and the core scenes should all adopt the MR experience.
* The main interaction of the app does not involve running, quick movements, or other intense actions.

For the following special cases, MR Safeguard mode can also be requested, but it requires clear safety warnings and user agreement for interaction, along with necessary protective measures tailored to the app experience:

* Virtual experience that replaces the surface of real objects. It is recommended to use semi-transparent effects in this type of experience. This allows users to see the actual environment and make informed decisions. Adequate safety measures should also be in place to protect users. If the user moves more than about one meter, it is recommended to make all displayed content semi-transparent, and restore the virtual experience when the user stays in place.
* Brief appearances of VR scenes within the app, such as the main interface, settings, pause, transition, and other non-core app scenes. The app should try to avoid such experiences as much as possible, and if it cannot be avoided, there must be sufficient measures to ensure user safety. If the user moves more than about one meter, it is recommended to make all displayed content semi-transparent, and restore the virtual experience when the user stays in place.
* Actions such as punching and kicking should only be performed in place, and there must be sufficient safety measures and reminders to ensure user safety. If the user moves more than about one meter, it is recommended to make all displayed content semi-transparent, and restore the virtual experience when the user stays in place.

The final decision on whether to use MR Safeguard mode will be based on the results of the app review.
## Development environment

* PICO device models: PICO 4 series, PICO 4 Ultra series
* PICO device's system version: 5.15.0 or later

## Enable the MR Safeguard capability for your app
### Prerequisites

* Have added the XR Origin object and added the PXR_Manager (Script) component to it.
* Have set up the Spatial Mesh feature for your app. The Spatial Mesh feature enables the system to scan the physical environment and generate meshes as obstacles in the space. For detailed instructions, refer to [this article](/en_spatial-mesh).

### Procedure
On the **PXR_Manager (Script)** panel of the **Inspector** window, check the **MR Safeguard** checkbox.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c17c1d5795a402eac0393c1d5354310~tplv-goo7wpa0wc-image.image" width="450px" />

The MR Safeguard capability is enabled, and the SDK automatically writes the following metadata to the app's AndroidManifest.xml file.
```XML
<meta-data android:name="enable_mr_safeguard" android:value="1" > </meta-data>
```


# --- END: MR Safeguard.md ---



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



# --- BEGIN: PXR_Hand Pose Generator script.md ---

The SDK uses shapes, bones and transforms and the components of hand poses. You can set up these components to create general hand poses.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ed90aadb3bd4344a7b9f278410bcade~tplv-goo7wpa0wc-image.image" width="500px" />

The PXR_Hand Pose Generator script is made up of the Hand Pose Config field, Shapes, Bones, and Transform components. You can use it to generate hand poses by setting shapes, bones, and transforms. Additionally, you can set the hold duration and margin to make hand poses smoothly switch from one to another.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45e16f7ebd744c9dbac83ba54880eceb~tplv-goo7wpa0wc-image.image" width="400px" />

## Basic concepts
### Hand pose config file
"Hand Pose Config" is used to create a hand pose configuration file that stores a hand pose's shape, bone, and transform settings.
### Margin
When transitioning between state A and state B, data jitter may occur due to errors in both the user's finger shape and the algorithm's recognition capability. Specifically, when the user's finger shape approaches the critical point between states A and B, unexpected jitter may occur during the transition between the two states.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cc2861a6b92459491b544c23934cb7c~tplv-goo7wpa0wc-image.image" width="450px" />

To resolve this issue, you can set a margin for each finger shape to make the transition smoother. Once set, the margin will be calculated into the transition process when transitioning from state A to state B or vice versa.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7dee4a49d9eb43608f724dce2c121907~tplv-goo7wpa0wc-image.image" width="450px" />

### Hold Duration
"Hold Duration" is the time during which the current state is maintained before switching to a new state. This prevents rapid flickering of the hand model at the edge when switching between different states.
## Prefab for visualized hand pose editing
The HandPoseGenerator prefab is located in the Package\PICO Integration\Assets\Resources\Prefabs directory. You can use the HandPoseGenerator prefab to create a hand pose configuration file by configuring Shapes, Bones, and Transform, and then attach the file to the PXR_Hand Pose script of either the prefab or another GameObject for use. You can view the visualization of shapes, bones, and transform settings in the Unity Editor's Inspector window when creating hand poses using this prefab.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed59a8e4bade4206b858533ec8f54ce6~tplv-goo7wpa0wc-image.image" width="400px" />

| **Default UI** | **Shapes Visualization** | **Transform Visualization** |
| --- | --- | --- |
| ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea2d59170bd341f990535361199347fd~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2b9670eff334140b890a224c454c430~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebc3872f69754bb884cef0ebe6dba760~tplv-goo7wpa0wc-image.image) |
## Shapes
The Shapes component is used to define finger shapes. You can use it to define the shape of each finger, the allowed angle error (margin) during shape recognition, and set the duration for which the current shape should be maintained when switching to a new shape (hold duration).
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56ab9e0ad46249be91d0ccac7d8ee6a2~tplv-goo7wpa0wc-image.image" width="400px" />

### Available finger shapes
Finger shapes include flexion, curl, and abduction.
| **Flexion** | **Curl** | **Abduction** |
| --- | --- | --- |
| Flexion of metacarpal joints | Curl of distal joints | Abduction between fingers |
| ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8885b2fa4a6347eea19b5ad349440775~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06246609a1144985b5aeb02e82e7863d~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25cee98434244b7f939664c2e3458d37~tplv-goo7wpa0wc-image.image) |
### Different states of finger shapes
Finger shapes support four states: any, open, and close.
| **State** | **Description** |
| --- | --- |
| Any | The finger shape can be in any state, which will not affect hand pose recognition. |
| Open | Used to set the degree at which a finger extends or opens. |
| Close | Used to set the degree at which the finger curls or closes. |
Below are schematic diagrams that show the five fingers in the shape of flexion, curl, and abduction. Each diagram illustrates the degree at which the finger opens and closes.
**Flexion**
| **Thumb** |  | **Index/Middle/Ring/Little Finger** |  |
| --- | --- | --- | --- |
| Open ( θ > 155° ) |  Close（ θ < 120° ） | Open ( θ > 144° ) | Close ( θ < 126° ) |
| ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60e4c99283864e9881e19ce9d53beb62~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/822ff3a8d7d240629fdb0b75364ead80~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7625cb14ae141a08888d7e5e6d5d3db~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72907f4c1fd34790b427be4e1b64b025~tplv-goo7wpa0wc-image.image) |
**Curl**
| **Thumb** |  | **Index/Middle/Ring/Little Finger** |  |
| --- | --- | --- | --- |
| Open ( θ > 90° ) | Close ( θ < 90° ) | Open ( θ > 107° ） | Close ( θ < 73° ) |
| ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb9c82b84dcc4ebd8ce1f8db7a7cc379~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b705c970586a467a890e27d6b3db1fb4~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/872116e1a57246469e879bb073fa8746~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0365f3ace3e745f79821c60bf1b27d62~tplv-goo7wpa0wc-image.image) |
**Abduction**
The content describes the abduction between two fingers, starting from the thumb and moving sequentially to the next finger. Specifically, it refers to the opening degree between the thumb and index finger, index and middle finger, middle and ring finger, and ring and little finger. Notably, **there is no individual abduction setting for the little finger**.
| **Thumb** |  | **Index/Middle/Ring/Little Finger** |  |
| --- | --- | --- | --- |
| Open ( θ > 13° ) | Close ( θ < 13° ) | Open ( θ > 10° ) | Close ( θ < 10°) |
| ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b98fb27fcb0d443d98a99629d7f8af20~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf0f22e34bca45009f3abdf600d34371~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c1373af96ce4a88958d2bf0674136be~tplv-goo7wpa0wc-image.image) | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5aba1bb2fd634ddb8eedbf73d1e9bfc0~tplv-goo7wpa0wc-image.image) |
### Shape exclusivity
If you set both the flexion and abduction shapes for a finger and set the state of the flexion shape to "any", the abduction shapes will take effect but the flexion shape will not.
### Margin for shapes
Margin is used to calculate a range within which a shape is valid and recognized. You can set a margin for a finger shape after setting the shape's state to "Open" or "Close".
**When is the finger shape valid/invalid?**
| ###### **Flexion & Curl** | ###### **Abduction** |
| --- | --- |
| **Valid:** <br> When the finger's actual flexion/curl degree is within [(Min.Range - Margin), (Max.Range + Margin)], the finger shape will be recognized. <br> **Invalid:** <br> When the finger's actual flexion/curl degree is smaller than (Min.Range - Margin) or bigger than (Max.Range + Margin), the finger shape will not be recognized. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/022517af2b474aeb9e74f69f4f8768cd~tplv-goo7wpa0wc-image.image) | **Valid:** <br> When the finger's actual abduction degree is within [(Min.Range - Margin/2), (Max.Range + Margin/2)], the finger shape will be recognized. <br> **Invalid:** <br> When the finger's actual abduction degree is smaller than (Min.Range - Margin/2) or bigger than (Max.Range + Margin/2), the finger shape will not be recognized. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe5f43dceaf74b0494baa16f3fc8364d~tplv-goo7wpa0wc-image.image) |
**How to set a margin for flexion, curl, and abduction?**
| ###### **Flexion & Curl** | ###### **Abduction** |
| --- | --- |
| Use the SDK's default range by setting Flexion/Curl's state to "Open" or "Close", then adjust the margin. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b4f36919a9c4e549f3b582703d07183~tplv-goo7wpa0wc-image.image) | Abduction uses the SDK's default recognition range and you can customize a margin for it. When the finger's abduction degree falls outside the range, it enters another state, and vice versa. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/786741097ac3452495b2503c74be22f2~tplv-goo7wpa0wc-image.image) |
### Visualizations
When creating hand poses using the HandPoseGenerator prefab, the colors of the joints will change according to the shape and state you set for fingers.
**Flexion:**
| **Any** | **Open** | **Close** |
| --- | --- | --- |
| All hand joints are gray. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a70de4d5af491db1cc4afe0232af5a~tplv-goo7wpa0wc-image.image) | The proximal joints become purple. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5cbefb755dc443ab8baca67cda7b584~tplv-goo7wpa0wc-image.image) | The proximal joints become purple. <br> Thumb: <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/586f8d4f294c4dd8a532fa2adf84ac36~tplv-goo7wpa0wc-image.image) <br> Index, middle, ring, and little fingers: <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ee264294d7b46f78635a2ebe1b70638~tplv-goo7wpa0wc-image.image) |
**Curl:**
| **Any** | **Open** | **Close** |
| --- | --- | --- |
| All hand joints are gray. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a70de4d5af491db1cc4afe0232af5a~tplv-goo7wpa0wc-image.image) | The tip, distal, and intermediate joints become purple. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/232bd4d519da4400a3c0465b741e6b83~tplv-goo7wpa0wc-image.image) | The tip, distal, and intermediate joints become purple. <br> Thumb: <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad8584aad80e4452bc08172229190f57~tplv-goo7wpa0wc-image.image) <br> Index, middle, ring, and little fingers: <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0749fa6ef114847af929f8363578dab~tplv-goo7wpa0wc-image.image) |
**Abduction:**
| **Any** | **Open** | **Close** |
| --- | --- | --- |
| The edge areas of all fingers are not highlighted. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a70de4d5af491db1cc4afe0232af5a~tplv-goo7wpa0wc-image.image) | The edge areas of all fingers are highlighted. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a88b1f23f115435fbcb62f5aaf963091~tplv-goo7wpa0wc-image.image) | The edge areas between two fingers are highlighted. <br> Thumb: <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e43e4c32d5d493baecc3112406169ca~tplv-goo7wpa0wc-image.image) <br> Index, middle, ring, and little fingers: <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3ef5643316045f0ad2dead5db76f65f~tplv-goo7wpa0wc-image.image) |
## Bones
The Bones component is used to define inter-joint relations, i.e., the distance between two hand joints. If it is not possible to define a hand pose using only the Shapes component, use the Bones component together.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3715b43512a746689558517e36a5d15e~tplv-goo7wpa0wc-image.image" width="400px" />

For example, making the tips of the thumb and index finger touch can help create the "Okay" pose.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a531da37d7bb41ba9782fe94c3fd4d0e~tplv-goo7wpa0wc-image.image" width="300px" />

### Distance
"Distance" (meter) is used to set a physical distance between two hand joints. When the actual distance between two joints is the "Distance" you set, the inter-joint relation is triggered.
### Margin for bones
Margin (unit: meter) is used to calculate the distance range within which an inter-joint relation is triggered. When the actual distance between two joints is within [(Distance - Margin/2), (Distance + Margin/2)], the relation is presented, otherwise not presented. You can set a margin to make the transitions of inter-joint relations smoother. 
## Transform
You can use the Transform component to define the orientation of hands by setting the "Track Axis", ”Track Target", "Angle Threshold", and "Margin".
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1d4fa6932f54df9ab69909de5d8cbc5~tplv-goo7wpa0wc-image.image" width="400px" />

### Track Axis
"Track Axis" is used to define the axis reference for hand tracking.
| **Option** | **Description** | **Visualization** |
| --- | --- | --- |
| Fingers | Four fingers extend as the main axis. | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c09a05d0b6284781b71b2713b87b1dc3~tplv-goo7wpa0wc-image.image) |
| Palm | The palm extends as the main axis. | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cd1eb66b72b4d34a861f91704061717~tplv-goo7wpa0wc-image.image) |
| Thumb | The thumb extends as the main axis. | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bdefae5297d493f8a03fc74cedf87af~tplv-goo7wpa0wc-image.image) |
### Track Target
Track Target is used to define the orientation of the Track Axis.
| **Option** | **Description** | **Visualization** |
| --- | --- | --- |
| Towards Face  | The Track Axis **faces towards the face**. <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68a73837408a47bbafb0192ecbbc6a9d~tplv-goo7wpa0wc-image.image) |
| Away From Face | The Track Axis **faces away from the face**.  <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7de4e3e440ca42afb528b09387fe6ae3~tplv-goo7wpa0wc-image.image) |
| World Up | The Track Axis **faces upwards**. | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6864020846ae453c9f8532167bf2e146~tplv-goo7wpa0wc-image.image) |
| World Down | The Track Axis **faces downwards**. <br>  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47f3e5786b894edb968e36012e40c164~tplv-goo7wpa0wc-image.image) |
### Angle Threshold & Margin
When the hand's angle is within [(Angle Threshold - Margin/2), (Angle Threshold + Margin/2)], the hand's orientation you set is valid; otherwise, the orientation is invalid.
### Visualizations of Track Axis & Track Target
The following table provides the visualized illustrations of different Track Aaxis and Track Target settings.
| **Track Axis** | **Track Target** | **Visualization** |
| --- | --- | --- |
| Fingers <br>  | Towards Face  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1935b2d222624cb9930b68043299e04d~tplv-goo7wpa0wc-image.image) |
|  | Away From Face | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b9e70058145424d9cbe9020d1266d92~tplv-goo7wpa0wc-image.image) |
|  | World Up | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61431b4981d84829954f84c33c33f729~tplv-goo7wpa0wc-image.image) |
|  | World Down | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e4ad4a77ba3497798c3579b982d067b~tplv-goo7wpa0wc-image.image) |
| Palm <br>  | Towards Face  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c73d716101a04a46a8b17e0e3e10c027~tplv-goo7wpa0wc-image.image) |
|  | Away From Face | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8695ba17890943cc81c0501ab1f764ab~tplv-goo7wpa0wc-image.image) |
|  | World Up | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dab27fda51cf4e3991e9c8f894acb301~tplv-goo7wpa0wc-image.image) |
|  | World Down | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/314c5b35cdd64fc892a1c8744e7f8f88~tplv-goo7wpa0wc-image.image) |
| Thumb | Towards Face  | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54caae9cbe004c398f5dc82189bc81f0~tplv-goo7wpa0wc-image.image) |
|  | Away From Face | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dcbfff5434bf4b068c54d4065c6912c1~tplv-goo7wpa0wc-image.image) |
|  | World Up | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5e584fa4cc746c3adbf44cf74105bc2~tplv-goo7wpa0wc-image.image) |
|  | World Down | ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13e41186c04e40e0aa540a43e33d8547~tplv-goo7wpa0wc-image.image) |


# --- END: PXR_Hand Pose Generator script.md ---



# --- BEGIN: PXR_Hand Pose script.md ---

The PXR_Hand Pose script is for setting up hand pose events. You can use it to select the hand to be tracked ("Track Type"), add the hand pose configuration file generated by the PXR_Hand Pose Generator script, and create events to be triggered by the hand pose.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6817a10b9a354ab1acc6f070225316c7~tplv-goo7wpa0wc-image.image" width="400px" />

## Track Type
"Track Type" is used to define the hand to be tracked:

* Any: To track any hand detected by the device.
* Left: To track the left hand.
* Right: To track the right hand.

## Config
"Config" is used to store the hand pose configuration file generated by PXR_Hand Pose Generator (Script).
## Hand pose event
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/893cad027c0d4e99b6fec5070dfc2f9e~tplv-goo7wpa0wc-image.image" width="400px" />

Different types of hand pose event:
| **Event Type** | **When is the event triggered?** |
| --- | --- |
| Hand Pose Start | This event is triggered when the hand pose starts. |
| Hand Pose Update | The event is triggered at every frame during the hand pose and provides the duration of the pose in milliseconds. |
| Hand Pose End | This event is triggered when the hand pose ends. |
Click **+**, add the object with the bound script to the **None (Object)** area, and then control the scope of UnityEvent callback. The options are as follows:
| **Option** | **Description** |
| --- | --- |
| Off | Callback is not issued. |
| Editor And Runtime | Callback is always issued. |
| Runtime Only | Callback is only issued in the Runtime and Editor playmode. |


# --- END: PXR_Hand Pose script.md ---



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



# --- BEGIN: Shared Spatial Anchor.md ---

Within the same physical space, the Shared Spatial Anchors feature allows users to share scene content when experiencing the same app.
When a local spatial anchor is uploaded to PICO's cloud, it becomes a shared spatial anchor. The user creating the anchor can share the anchor's UUID with other users within the app. Other users can then download and use the shared spatial anchor after obtaining its UUID.
## Development environment

* PICO device models: PICO 4 series, PICO 4 Ultra series
* PICO device's system version: 5.15.0 or later

## Important note
Users are required to log in to their PICO devices to use shared spatial anchors.
## Prerequisites

* The XR Origin object has been added to your Unity project.
* The PXR_Manager (Script) component has been added to the XR Origin object.
* The Video Seethrough feature has been set up for your app. For more information, refer to [this article](/en_seethrough).
* The app's ID has been added to your Unity project. For more information, refer to [this article](/document/unity/complete-project-settings/#dcd5e00a). 
*  The PICO Platform Services has been initialized. For more information, refer to [this article](/document/unity/initialization/#4d3c337f). 
* `GetLoggedInUser` or `GetAccessToken` have been called in the code to retrieve the user's PICO account information, so as to trigger login notification for the user. For more information, refer to [this article](/document/unity/accounts-and-friends/#ecbd97a8). 

## Implementation process

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3NjdweCIgaGVpZ2h0PSIzNTNweCIgdmlld0JveD0iLTAuNSAtMC41IDc2NyAzNTMiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDIgMzIyIEMgMiAzMDQgMiAyOTUgMjIgMjk1IEMgOC42NyAyOTUgOC42NyAyNzcgMjIgMjc3IEMgMzUuMzMgMjc3IDM1LjMzIDI5NSAyMiAyOTUgQyA0MiAyOTUgNDIgMzA0IDQyIDMyMiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTEgMzA0LjE5IEwgMTMzLjYzIDMwNC4xOSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDEzOC44OCAzMDQuMTkgTCAxMzEuODggMzA3LjY5IEwgMTMzLjYzIDMwNC4xOSBMIDEzMS44OCAzMDAuNjkgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI3MSIgeT0iMjc3IiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjg3cHg7IG1hcmdpbi1sZWZ0OiA3MnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5Mb2dpbjwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjE0MSIgeT0iMjgyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQ1IiByeD0iNi43NSIgcnk9IjYuNzUiIGZpbGw9IiNlMWQ1ZTciIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMwNXB4OyBtYXJnaW4tbGVmdDogMTQycHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRldmljZSBBPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMDEiIHk9IjEyMiIgd2lkdGg9IjIwMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjZDRlMWY1IiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNDJweDsgbWFyZ2luLWxlZnQ6IDEwMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2IHN0eWxlPSJjb2xvcjpyZ2IoMzEsIDM1LCA0MSkiPjxwPjxmb250PjxzcGFuPjwvc3Bhbj48L2ZvbnQ+PC9wPjxkaXYgc3R5bGU9ImZvbnQtd2VpZ2h0Om5vcm1hbDtjb2xvcjpyZ2IoMzEsIDM1LCA0MSkiPjxwPjxmb250PjxzcGFuPjwvc3Bhbj48L2ZvbnQ+PC9wPjxkaXYgc3R5bGU9ImZvbnQtd2VpZ2h0Om5vcm1hbDtjb2xvcjpyZ2IoMzEsIDM1LCA0MSkiPjxwPjxmb250IHN0eWxlPSJmb250LXNpemU6MTRweCI+VXBsb2FkU3BhdGlhbEFuY2hvckFzeW5jPC9mb250PjwvcD48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjYxIDMwNC41IEwgMzI0LjYzIDMwNC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzI5Ljg4IDMwNC41IEwgMzIyLjg4IDMwOCBMIDMyNC42MyAzMDQuNSBMIDMyMi44OCAzMDEgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZWxsaXBzZSBjeD0iMzc2IiBjeT0iMzA0LjUiIHJ4PSI0NSIgcnk9IjI3LjUiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMiwzKSIgb3BhY2l0eT0iMC4yNSIvPjxlbGxpcHNlIGN4PSIzNzYiIGN5PSIzMDQuNSIgcng9IjQ1IiByeT0iMjcuNSIgZmlsbD0iI2E5YzRlYiIgc3Ryb2tlPSIjZmZmZmZmIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMDVweDsgbWFyZ2luLWxlZnQ6IDMzMnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BbmNob3IgVVVJRDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NTIgMjgyIEwgNTUyIDE3MS4zNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU1MiAxNjYuMTIgTCA1NTUuNSAxNzMuMTIgTCA1NTIgMTcxLjM3IEwgNTQ4LjUgMTczLjEyIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNDkyIiB5PSIyODIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDUiIHJ4PSI2Ljc1IiByeT0iNi43NSIgZmlsbD0iI2UxZDVlNyIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzA1cHg7IG1hcmdpbi1sZWZ0OiA0OTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGV2aWNlIEI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDIxIDMwNC41IEwgNDg1LjYzIDMwNC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDkwLjg4IDMwNC41IEwgNDgzLjg4IDMwOCBMIDQ4NS42MyAzMDQuNSBMIDQ4My44OCAzMDEgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDcxMiAzMjMuMjUgQyA3MTIgMzA0LjI1IDcxMiAyOTQuNzUgNzMyIDI5NC43NSBDIDcxOC42NyAyOTQuNzUgNzE4LjY3IDI3NS43NSA3MzIgMjc1Ljc1IEMgNzQ1LjMzIDI3NS43NSA3NDUuMzMgMjk0Ljc1IDczMiAyOTQuNzUgQyA3NTIgMjk0Ljc1IDc1MiAzMDQuMjUgNzUyIDMyMy4yNSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNzAyIDMwNCBMIDYxOC4zNyAzMDQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2MTMuMTIgMzA0IEwgNjIwLjEyIDMwMC41IEwgNjE4LjM3IDMwNCBMIDYyMC4xMiAzMDcuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjY0MiIgeT0iMjY5LjUiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyODBweDsgbWFyZ2luLWxlZnQ6IDY0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5Mb2dpbjwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIiIHk9IjMyNyIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIsMykiIG9wYWNpdHk9IjAuMjUiLz48cmVjdCB4PSIyIiB5PSIzMjciIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMzdweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VXNlciBBPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3MTIiIHk9IjMyOS41IiB3aWR0aD0iNTAiIGhlaWdodD0iMTUiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMiwzKSIgb3BhY2l0eT0iMC4yNSIvPjxyZWN0IHg9IjcxMiIgeT0iMzI5LjUiIHdpZHRoPSI1MCIgaGVpZ2h0PSIxNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMzdweDsgbWFyZ2luLWxlZnQ6IDcxM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Vc2VyIELCoMKgPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0MjIiIHk9IjEyMiIgd2lkdGg9IjI0MCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjZDRlMWY1IiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNDJweDsgbWFyZ2luLWxlZnQ6IDQyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2IHN0eWxlPSJjb2xvcjpyZ2IoMzEsIDM1LCA0MSkiPjxwPjxmb250IHN0eWxlPSJmb250LXNpemU6MTJweCI+PHNwYW4+PC9zcGFuPjwvZm9udD48L3A+PGRpdiBzdHlsZT0iZm9udC13ZWlnaHQ6bm9ybWFsO2NvbG9yOnJnYigzMSwgMzUsIDQxKSI+PHA+PHNwYW4+PC9zcGFuPjwvcD48ZGl2IHN0eWxlPSJmb250LXNpemU6MjRweDtmb250LXdlaWdodDpub3JtYWw7Y29sb3I6cmdiYSgzMSwzNSw0MSwxLjAwMDAwMCkiPjxwIHN0eWxlPSJmb250LXNpemU6MTNweCI+RG93bmxvYWRTaGFyZWRTcGF0aWFsQW5jaG9yQXN5bmM8L3A+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDMzNiAxOS41IEMgMzEyIDE5LjUgMzA2IDM3IDMyNS4yIDQwLjUgQyAzMDYgNDguMiAzMjcuNiA2NSAzNDMuMiA1OCBDIDM1NCA3MiAzOTAgNzIgNDAyIDU4IEMgNDI2IDU4IDQyNiA0NCA0MTEgMzcgQyA0MjYgMjMgNDAyIDkgMzgxIDE2IEMgMzY2IDUuNSAzNDIgNS41IDMzNiAxOS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgyLDMpIiBvcGFjaXR5PSIwLjI1Ii8+PHBhdGggZD0iTSAzMzYgMTkuNSBDIDMxMiAxOS41IDMwNiAzNyAzMjUuMiA0MC41IEMgMzA2IDQ4LjIgMzI3LjYgNjUgMzQzLjIgNTggQyAzNTQgNzIgMzkwIDcyIDQwMiA1OCBDIDQyNiA1OCA0MjYgNDQgNDExIDM3IEMgNDI2IDIzIDQwMiA5IDM4MSAxNiBDIDM2NiA1LjUgMzQyIDUuNSAzMzYgMTkuNSBaIiBmaWxsPSIjYzNhYmQwIiBzdHJva2U9IiNmZmZmZmYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM3cHg7IG1hcmdpbi1sZWZ0OiAzMDdweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UElDTyBDbG91ZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyMDEgMTIyIFEgMjEyIDQyIDMwOS42IDQ1LjcyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzE0Ljg0IDQ1LjkyIEwgMzA3LjcxIDQ5LjE1IEwgMzA5LjYgNDUuNzIgTCAzMDcuOTggNDIuMTUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDIwMSAyODIgTCAyMDEgMTY4LjM3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjAxIDE2My4xMiBMIDIwNC41IDE3MC4xMiBMIDIwMSAxNjguMzcgTCAxOTcuNSAxNzAuMTIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDU1Mi4wOCAxMjIgUSA1MzIgNDIgNDI3LjIxIDQwLjkyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDIxLjk2IDQwLjg2IEwgNDI4Ljk5IDM3LjQzIEwgNDI3LjIxIDQwLjkyIEwgNDI4LjkyIDQ0LjQzIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAzNDIgMTkyIEwgMzQyIDEzMiBRIDM0MiAxMjIgMzQyIDExMiBMIDM0MiA2MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDMxMiAxOTIgTCAzNDIgMTkyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxyZWN0IHg9IjI2MSIgeT0iMTgyIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTkycHg7IG1hcmdpbi1sZWZ0OiAyNjJweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+U3VjY2VzczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyNTIgMTkyIEwgMjMyIDE5MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIzMiAxOTIgTCAyMzEuMDcgMjc1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjMxLjAxIDI4MC44OCBMIDIyNy41OSAyNzMuODQgTCAyMzEuMDcgMjc1LjYzIEwgMjM0LjU5IDI3My45MiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDAyIDE5MiBMIDQwMiAxMzIgUSA0MDIgMTIyIDQwMiAxMTIgTCA0MDIgNjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDIgMTkxLjU1IEwgNDMyIDE5MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cmVjdCB4PSI0NDIiIHk9IjE4MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE5MnB4OyBtYXJnaW4tbGVmdDogNDQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlN1Y2Nlc3M8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTIyIDE5MiBMIDQ5MiAxOTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1MjIgMTkyIEwgNTIyIDI3NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDUyMiAyODAuODggTCA1MTguNSAyNzMuODggTCA1MjIgMjc1LjYzIEwgNTI1LjUgMjczLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PC9nPjwvc3ZnPg==" from="flow-chart" payload="{&quot;data&quot;:{&quot;mxGraphModel&quot;:{&quot;dx&quot;:&quot;919&quot;,&quot;dy&quot;:&quot;532&quot;,&quot;grid&quot;:&quot;1&quot;,&quot;gridSize&quot;:&quot;10&quot;,&quot;guides&quot;:&quot;1&quot;,&quot;tooltips&quot;:&quot;1&quot;,&quot;connect&quot;:&quot;1&quot;,&quot;arrows&quot;:&quot;1&quot;,&quot;fold&quot;:&quot;1&quot;,&quot;page&quot;:&quot;1&quot;,&quot;pageScale&quot;:&quot;1&quot;,&quot;pageWidth&quot;:&quot;827&quot;,&quot;pageHeight&quot;:&quot;1169&quot;},&quot;mxCellMap&quot;:{&quot;K7dyDj5E&quot;:{&quot;id&quot;:&quot;K7dyDj5E&quot;},&quot;GVuv594V&quot;:{&quot;id&quot;:&quot;GVuv594V&quot;,&quot;parent&quot;:&quot;K7dyDj5E&quot;},&quot;uCdE579D&quot;:{&quot;id&quot;:&quot;uCdE579D&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;shape=actor;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;User&quot;,&quot;diagramCategory&quot;:&quot;advanced&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;505&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;45&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;QSjQqMd0&quot;:{&quot;id&quot;:&quot;QSjQqMd0&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;89&quot;,&quot;y&quot;:&quot;532.19&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;178&quot;,&quot;y&quot;:&quot;532.19&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;ic3T8fIx&quot;:{&quot;id&quot;:&quot;ic3T8fIx&quot;,&quot;value&quot;:&quot;<b>Login</b>&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;109&quot;,&quot;y&quot;:&quot;505&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;DDZLX8TX&quot;:{&quot;id&quot;:&quot;DDZLX8TX&quot;,&quot;value&quot;:&quot;Device A&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#E1D5E7;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;179&quot;,&quot;y&quot;:&quot;510&quot;,&quot;width&quot;:&quot;120&quot;,&quot;height&quot;:&quot;45&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;krtJJLOR&quot;:{&quot;id&quot;:&quot;krtJJLOR&quot;,&quot;value&quot;:&quot;<p><font></font></p><p><font></font></p><p><font style=\&quot;font-size:14px\&quot;>UploadSpatialAnchorAsync</font></p>&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#D4E1F5;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;139&quot;,&quot;y&quot;:&quot;350&quot;,&quot;width&quot;:&quot;200&quot;,&quot;height&quot;:&quot;40&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;8xgSpw2k&quot;:{&quot;id&quot;:&quot;8xgSpw2k&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;source&quot;:&quot;DDZLX8TX&quot;,&quot;target&quot;:&quot;uR1AoHhJ&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;309&quot;,&quot;y&quot;:&quot;540&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;359&quot;,&quot;y&quot;:&quot;525&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;uR1AoHhJ&quot;:{&quot;id&quot;:&quot;uR1AoHhJ&quot;,&quot;value&quot;:&quot;Anchor UUID&quot;,&quot;style&quot;:&quot;ellipse;whiteSpace=wrap;html=1;fillColor=#A9C4EB;strokeColor=#FFFFFF;shadow=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;oval&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;369&quot;,&quot;y&quot;:&quot;505&quot;,&quot;width&quot;:&quot;90&quot;,&quot;height&quot;:&quot;55&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;P43WZxMB&quot;:{&quot;id&quot;:&quot;P43WZxMB&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;source&quot;:&quot;taldf7FZ&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;-0-mxGeometry&quot;:{&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;590&quot;,&quot;y&quot;:&quot;393&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;taldf7FZ&quot;:{&quot;id&quot;:&quot;taldf7FZ&quot;,&quot;value&quot;:&quot;Device B&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#E1D5E7;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;530&quot;,&quot;y&quot;:&quot;510&quot;,&quot;width&quot;:&quot;120&quot;,&quot;height&quot;:&quot;45&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;9GGdyVMj&quot;:{&quot;id&quot;:&quot;9GGdyVMj&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;entryX=0;entryY=0.5;entryDx=0;entryDy=0;exitX=1;exitY=0.5;exitDx=0;exitDy=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;source&quot;:&quot;uR1AoHhJ&quot;,&quot;target&quot;:&quot;taldf7FZ&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;470&quot;,&quot;y&quot;:&quot;525&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;489&quot;,&quot;y&quot;:&quot;525&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;MJmHHGhv&quot;:{&quot;id&quot;:&quot;MJmHHGhv&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;shape=actor;whiteSpace=wrap;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;User&quot;,&quot;diagramCategory&quot;:&quot;advanced&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;750&quot;,&quot;y&quot;:&quot;503.75&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;47.5&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;2kE6FlgZ&quot;:{&quot;id&quot;:&quot;2kE6FlgZ&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;740&quot;,&quot;y&quot;:&quot;532&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;650&quot;,&quot;y&quot;:&quot;532&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;apViNVL9&quot;:{&quot;id&quot;:&quot;apViNVL9&quot;,&quot;value&quot;:&quot;<b>Login</b>&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;680&quot;,&quot;y&quot;:&quot;497.5&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;2YPqai1A&quot;:{&quot;id&quot;:&quot;2YPqai1A&quot;,&quot;value&quot;:&quot;User A&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;shadow=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;40&quot;,&quot;y&quot;:&quot;555&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;6OekUJzD&quot;:{&quot;id&quot;:&quot;6OekUJzD&quot;,&quot;value&quot;:&quot;User B  &quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;shadow=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;750&quot;,&quot;y&quot;:&quot;557.5&quot;,&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;15&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;huZAoh7E&quot;:{&quot;id&quot;:&quot;huZAoh7E&quot;,&quot;value&quot;:&quot;<p><font style=\&quot;font-size:12px\&quot;></font></p><p></p><p style=\&quot;font-size:13px\&quot;>DownloadSharedSpatialAnchorAsync</p>&quot;,&quot;style&quot;:&quot;rounded=1;whiteSpace=wrap;html=1;fillColor=#D4E1F5;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;RoundedRectangle&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;460&quot;,&quot;y&quot;:&quot;350&quot;,&quot;width&quot;:&quot;240&quot;,&quot;height&quot;:&quot;40&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;gUo2fH0e&quot;:{&quot;id&quot;:&quot;gUo2fH0e&quot;,&quot;value&quot;:&quot;PICO Cloud&quot;,&quot;style&quot;:&quot;ellipse;shape=cloud;whiteSpace=wrap;html=1;shadow=1;strokeColor=#FFFFFF;fillColor=#C3ABD0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;Cloud&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;344&quot;,&quot;y&quot;:&quot;230&quot;,&quot;width&quot;:&quot;120&quot;,&quot;height&quot;:&quot;70&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;oI1emR6N&quot;:{&quot;id&quot;:&quot;oI1emR6N&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;curved=1;endArrow=classic;html=1;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=0.083;entryY=0.628;entryDx=0;entryDy=0;entryPerimeter=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;source&quot;:&quot;krtJJLOR&quot;,&quot;target&quot;:&quot;gUo2fH0e&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;curved&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;239&quot;,&quot;y&quot;:&quot;330&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;340&quot;,&quot;y&quot;:&quot;280&quot;,&quot;as&quot;:&quot;targetPoint&quot;},&quot;-2-Array&quot;:{&quot;as&quot;:&quot;points&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;250&quot;,&quot;y&quot;:&quot;270&quot;}}}},&quot;hk0efbnw&quot;:{&quot;id&quot;:&quot;hk0efbnw&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=0.5;entryY=1;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;source&quot;:&quot;DDZLX8TX&quot;,&quot;target&quot;:&quot;krtJJLOR&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;239&quot;,&quot;y&quot;:&quot;450&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;239&quot;,&quot;y&quot;:&quot;410&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;NJ7rKLmb&quot;:{&quot;id&quot;:&quot;NJ7rKLmb&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;curved=1;endArrow=classic;html=1;entryX=0.957;entryY=0.555;entryDx=0;entryDy=0;entryPerimeter=0;exitX=0.542;exitY=0;exitDx=0;exitDy=0;exitPerimeter=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;source&quot;:&quot;huZAoh7E&quot;,&quot;target&quot;:&quot;gUo2fH0e&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;curved&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;540&quot;,&quot;y&quot;:&quot;300&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;450&quot;,&quot;y&quot;:&quot;240&quot;,&quot;as&quot;:&quot;targetPoint&quot;},&quot;-2-Array&quot;:{&quot;as&quot;:&quot;points&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;570&quot;,&quot;y&quot;:&quot;270&quot;}}}},&quot;oB135IOO&quot;:{&quot;id&quot;:&quot;oB135IOO&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=none;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;straight&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;380&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;380&quot;,&quot;y&quot;:&quot;290&quot;,&quot;as&quot;:&quot;targetPoint&quot;},&quot;-2-Array&quot;:{&quot;as&quot;:&quot;points&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;380&quot;,&quot;y&quot;:&quot;350&quot;}}}},&quot;7FJJKQ7r&quot;:{&quot;id&quot;:&quot;7FJJKQ7r&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=none;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;straight&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;350&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;380&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;wVM1Osjy&quot;:{&quot;id&quot;:&quot;wVM1Osjy&quot;,&quot;value&quot;:&quot;Success&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;299&quot;,&quot;y&quot;:&quot;410&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;V0PnwqqG&quot;:{&quot;id&quot;:&quot;V0PnwqqG&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=none;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;straight&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;290&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;270&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;1BxRPvjV&quot;:{&quot;id&quot;:&quot;1BxRPvjV&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;entryX=0.75;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;target&quot;:&quot;DDZLX8TX&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;270&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;270&quot;,&quot;y&quot;:&quot;495&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;J6ub0PQy&quot;:{&quot;id&quot;:&quot;J6ub0PQy&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=none;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;straight&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;440&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;440&quot;,&quot;y&quot;:&quot;290&quot;,&quot;as&quot;:&quot;targetPoint&quot;},&quot;-2-Array&quot;:{&quot;as&quot;:&quot;points&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;440&quot;,&quot;y&quot;:&quot;350&quot;}}}},&quot;IRtWg6s9&quot;:{&quot;id&quot;:&quot;IRtWg6s9&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=none;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;straight&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;440&quot;,&quot;y&quot;:&quot;419.55&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;470&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;IzUBm2lj&quot;:{&quot;id&quot;:&quot;IzUBm2lj&quot;,&quot;value&quot;:&quot;Success&quot;,&quot;style&quot;:&quot;text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;vertex&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;text&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;x&quot;:&quot;480&quot;,&quot;y&quot;:&quot;410&quot;,&quot;width&quot;:&quot;40&quot;,&quot;height&quot;:&quot;20&quot;,&quot;as&quot;:&quot;geometry&quot;}},&quot;Y4AaJwse&quot;:{&quot;id&quot;:&quot;Y4AaJwse&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=none;html=1;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;straight&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;560&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;530&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}},&quot;LJULH8aM&quot;:{&quot;id&quot;:&quot;LJULH8aM&quot;,&quot;value&quot;:&quot;&quot;,&quot;style&quot;:&quot;endArrow=classic;html=1;entryX=0.25;entryY=0;entryDx=0;entryDy=0;&quot;,&quot;parent&quot;:&quot;GVuv594V&quot;,&quot;target&quot;:&quot;taldf7FZ&quot;,&quot;edge&quot;:&quot;1&quot;,&quot;diagramName&quot;:&quot;DirectionalConnector&quot;,&quot;diagramCategory&quot;:&quot;general&quot;,&quot;-0-mxGeometry&quot;:{&quot;width&quot;:&quot;50&quot;,&quot;height&quot;:&quot;50&quot;,&quot;relative&quot;:&quot;1&quot;,&quot;as&quot;:&quot;geometry&quot;,&quot;-0-mxPoint&quot;:{&quot;x&quot;:&quot;560&quot;,&quot;y&quot;:&quot;420&quot;,&quot;as&quot;:&quot;sourcePoint&quot;},&quot;-1-mxPoint&quot;:{&quot;x&quot;:&quot;560&quot;,&quot;y&quot;:&quot;495&quot;,&quot;as&quot;:&quot;targetPoint&quot;}}}},&quot;mxCellList&quot;:[&quot;K7dyDj5E&quot;,&quot;GVuv594V&quot;,&quot;uCdE579D&quot;,&quot;QSjQqMd0&quot;,&quot;ic3T8fIx&quot;,&quot;DDZLX8TX&quot;,&quot;krtJJLOR&quot;,&quot;8xgSpw2k&quot;,&quot;uR1AoHhJ&quot;,&quot;P43WZxMB&quot;,&quot;taldf7FZ&quot;,&quot;9GGdyVMj&quot;,&quot;MJmHHGhv&quot;,&quot;2kE6FlgZ&quot;,&quot;apViNVL9&quot;,&quot;2YPqai1A&quot;,&quot;6OekUJzD&quot;,&quot;huZAoh7E&quot;,&quot;gUo2fH0e&quot;,&quot;oI1emR6N&quot;,&quot;hk0efbnw&quot;,&quot;NJ7rKLmb&quot;,&quot;oB135IOO&quot;,&quot;7FJJKQ7r&quot;,&quot;wVM1Osjy&quot;,&quot;V0PnwqqG&quot;,&quot;1BxRPvjV&quot;,&quot;J6ub0PQy&quot;,&quot;IRtWg6s9&quot;,&quot;IzUBm2lj&quot;,&quot;Y4AaJwse&quot;,&quot;LJULH8aM&quot;]},&quot;lastEditTime&quot;:0,&quot;snapshot&quot;:&quot;&quot;}" />

The following is an overview of the integration process for the Shared Spatial Anchor feature, with more details provided in the text below.

1. Enable the Shared Spatial Anchor capability for your app in the Unity editor.
2. Use the RoomService, MatchmakingService, and NetworkingService APIs of the PICO SDK to create a [multiplayer](/en_matchmaking) environment. Users can then send messages within the room to share the UUIDs of shared spatial anchors. You can also use the [Photon Unity Networking](https://doc.photonengine.com/pun/current/getting-started/pun-intro) framework to implement the sharing of anchor UUID.
3. Call `CreateSpatialAnchorAsync` to create a general spatial anchor in the current room, then call `PersistSpatialAnchorAsync` to persist the spatial anchor into the PICO device's local disk. For more details, refer to the "[Spatial Anchor](/en_spatial-anchors)" article.
4. Call `UploadSpatialAnchorAsync` to upload the general spatial anchor to PICO's cloud.
5. Use the `NetworkingService` APIs of the PICO SDK or Photon Unity Networking to allow users to share the UUIDs of shared spatial anchors.
6. Call `DownloadSharedSpatialAnchorAsync` to download the shared spatial anchor.
7. Call `QuerySpatialAnchorAsync` to load the downloaded shared spatial anchor in the scene.

## Enable the Shared Spatial Anchor capability for your app
On the **PXR_Manager (Script)** panel of the **Inspector** window, check the **Shared Spatial Anchor** checkbox to enable the Shared Spatial Anchor capability for your app. Then, you can call Shared Spatial Anchor APIs to implement this feature in your app.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a220ed5e4db6407dbfc31e84be18e0bb~tplv-goo7wpa0wc-image.image" width="500px" />

## Upload spatial anchors to PICO's cloud
Your app's users can upload spatial anchors to PICO's cloud through the `UploadSpatialAnchorAsync` API. Once uploaded, the user can share the UUID of this shared spatial anchor to other users, and other users can then download this anchor.
```C#
async Task<(PxrResult result, Guid uuid)> UploadSpatialAnchorAsync(ulong anchorHandle)
```

To know the upload progress while uploading a spatial anchor to PICO's cloud, use the `UploadSpatialAnchorWithProgressAsync `API.
```C#
public static async Task<(PxrResult result, Guid uuid)> UploadSpatialAnchorWithProgressAsync(ulong anchorHandle, Action<int> progressUpdated, CancellationToken token = default)
```

You can record the UUID of a spatial anchor when the user uploads it, so that you can subsequently share the anchor's UUID directly over the network, without the need to upload the anchor again.
## Share shared spatial anchors to others
You can use the RoomService, MatchmakingService, and NetworkingService APIs of the PICO SDK to create a [multiplayer](/matchmaking) environment and enable users to share the UUIDs of anchors or you can use the [Photon Unity Networking](https://doc.photonengine.com/pun/current/getting-started/pun-intro) framework to implement this experience.
It is recommended to add relevant instructions to guide the user. In a multiplayer game, it is suggested that the anchor creator should carefully observe the environment around the anchor after creating it, and then share the anchor, to ensure that the anchor can be successfully recognized and located later.
## Download shared spatial anchors
After other users get the UUID of the shared spatial anchor, they can download the anchor through `DownloadSharedSpatialAnchorAsync`. After the anchor is downloaded, the app can implement custom logic to obtain the pose data of the anchor, but cannot persist or unpersist the anchor.
```C#
async Task<PxrResult> DownloadSharedSpatialAnchorAsync(Guid uuid)
```

To know the download progress while downloading a shared spatial anchor, use the `DownloadSharedSpatialAnchorWithProgressAsync` API.
```C#
public static async Task<PxrResult> DownloadSharedSpatialAnchorWithProgressAsync(Guid uuid, Action<int> progressUpdated, CancellationToken token = default)
```

## Load shared spatial anchors
After other users download the shared spatial anchor, they can load that anchor in the scene through `QuerySpatialAnchorAsync`.
```C#
async Task<(PxrResult result, List<ulong> anchorHandleList)> QuerySpatialAnchorAsync(Guid[] uuids = null)
```

It is recommended to add relevant instructions to guide the user. In a multiplayer game, if the users receiving the anchor fail to recognize the anchor, they should go to the vicinity of the anchor or the location previously observed by the anchor sharer, and then closely observe the surrounding environment, so as to increase the success rate of recognizing and retrieving the anchor.
## Unpersist shared spatial anchors
After a user uploads a general spatial anchor to PICO's cloud, the user cannot actively unpersist that anchor. PICO will automatically unpersist anchors that have been inactive (i.e. no client requests for that anchor) for 7 days, starting from the last time the anchor is active. After deletion, other users who have obtained that shared spatial anchor will no longer be able to use it.
Additionally, after a user uploads an anchor to PICO's cloud, even if the user unpersists the anchor from the app's memory or the PICO device's local disk, other users can still continue to use that shared spatial anchor.
## Code sample
The following file contains a code sample for your reference. This sample demonstrates how to use the PICO SDK's RoomService, MatchmakingService, and NetworkingService to share anchor UUIDs and shows how to use the Shared Spatial Anchor APIs.
<a href="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a74b70ba7e84a29ac3fa5cbdee38b43~tplv-goo7wpa0wc-image.image" filename="SharedSpatialAnchor.cs" download>SharedSpatialAnchor.cs</a>
## API reference
For more details on Shared Spatial Anchor APIs, such as parameter descriptions and returns, refer to the [API reference](/reference/unity/client-api/PXR_MixedReality/).


# --- END: Shared Spatial Anchor.md ---



# --- BEGIN: Spatial Anchor.md ---

Spatial anchors can anchor the positions in the virtual environment to the positions in the real environment. After placing and saving spatial anchors, when the user returns to the locations where these anchors were placed, the system can retrieve them and return them to the app.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0374e600877d4bf093ade417d2dd1fdd~tplv-goo7wpa0wc-image.image" width="600px" />

## Basic concepts
| **Name** | **Description** |
| --- | --- |
| UUID | UUID (Universally Unique Identifier) is the unique identifier for spatial anchor, which is assigned when the anchor is created, and can be used to load specific anchors. |
| Handle | Through handles, you can associate anchors in app's memory with those persisted into the PICO device's local disk. When destroying, storing, or deleting anchors, as well as retrieving an anchor's UUID and real-time location, you need to specify the anchor using its handle. The handle is not permanent; it will change after the app is restarted. |
## Feature refactoring info
Starting from version 3.0.0, PICO refactorred the Spatial Anchors feature. Refer to the "[Compatibility & porting guide for MR features](/en_compatibility-and-porting-guide-for-mr-features)" article for details.
## Development environment

* PICO device models: PICO 4 series, PICO 4 Ultra series
* PICO device's system version: 5.14.0 or later

## Prerequisites

* The XR Origin object has been added to the scene.
* The PXR_Manager (Script) component has been added to the XR Origin object.
* The Video Seethrough feature has been set up for your app. For detailed instructions, refer to "[Video Seethrough](/en_seethrough)" article 

## Enable the Spatial Anchor capability for your app
On the **PXR_Manager (Script)** panel of the **Inspector** window, check the **Spatial Anchor** checkbox to enable the Spatial Anchor capability for your app. Then you can call Spatial Anchor APIs to implement this feature in your app.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/029b4769ffb544f09627e3d7ea2c0357~tplv-goo7wpa0wc-image.image" width="500px" />

## Start/stop the Spatial Anchor feature
Before calling other Spatial Anchor APIs, call `StartSenseDataProvider` to start the Spatial Anchor feature in your apps. When all spatial-anchor-related operations are done, call `StopSenseDataProvider` to stop this feature. You need to specify the spatial anchor data provider, which is `SpatialAnchor`, in these two API calls.
```C#
// Start the Spatial Anchor feature
async Task<PxrResult> StartSenseDataProvider(PxrSenseDataProviderType type)

// Stop the Spatial Anchor feature
PxrResult StopSenseDataProvider(PxrSenseDataProviderType type)
```

## Get the state of spatial anchor data provider
This is an optional API. If you do not store the state of spatial anchor data provider when calling `StartSenseDataProvider`, you can call `GetSenseDataProviderState` to check if the data provider has successfully started.
```C#
PxrResult GetSenseDataProviderState(PxrSenseDataProviderType type,out PxrSenseDataProviderState state)
```

## Manage spatial anchors
You can use APIs to manage spatial anchors in the scene, including creating, persisting, loading spatial anchors, and more. In addition to calling APIs, you can also manage spatial anchors more conveniently through the PXR_Spatial Anchor (Script) component. For more information, refer to the "About the PXR_Spatial Anchor (Script) component" section.
### Create spatial anchors
Call `CreateSpatialAnchorAsync` to create a spatial anchor in the app's memory. The request returns the UUID and handle of the created anchor. You can also use the SpatialAnchor prefab to create anchors more conveniently. For more information, refer to the "About the SpatialAnchor Prefab" section.
After creating a spatial anchor, if you do not persist the anchor, it will be destroyed when you exit the app. If you want the app to always be able to retrieve the created anchors, you need to persist the anchors into the PICO device's local disk.
```C#
async Task<(PxrResult result,ulong anchorHandle,Guid uuid)> CreateSpatialAnchorAsync(Vector3 position, Quaternion rotation)
```

It is recommended to design your app to provide a good interaction experience between the anchors and the user. For example, try to place the anchors within a 3-meter range of the user's HMD. After placing an anchor, if your app wants to accurately retrieve it, the user needs to look around and move around the anchor's location.
After placing anchors, your app can observe and map the area within a 3-meter range centered on the user. The area range within which the anchor can be retrieved is related to the area range within which the user looks around after placing the anchor, with a maximum radius of 5 meters. If there are no other anchors in a location beyond the 5-meter radius, the anchor may not be retrievable.
### Persist spatial anchors
Call `PersistSpatialAnchorAsync` to persist a spatial anchor into the PICO device's local disk. After saving the anchor, you can retrieve it when the user enters the same space multiple times using the same PICO device. You can use the anchor for a long time, and can also continue to call corresponding APIs to query and load the anchor even after it has been destroyed in your app's memory.
```C#
async Task<PxrResult> PersistSpatialAnchorAsync(ulong anchorHandle)
```

### Load spatial anchors
After successfully creating a spatial anchor, each anchor will be assigned a unique UUID. You can pass a list of UUIDs in `QuerySpatialAnchorAsync` to load the specified anchors from the PICO device's local disk or the app's memory. Before calling `QuerySpatialAnchorAsync`, you need to call `GetAnchorUuid` to get the UUIDs of anchors. If you do not pass any UUIDs in the request, it will return all available anchors.
**Note**

* Only supports loading anchors created by the current app.
* `QuerySpatialAnchorAsync` can only be called once at a time. The next call must wait until the current one completes.

```C#
async Task<(PxrResult result, List<ulong> anchorHandleList)> QuerySpatialAnchorAsync(Guid[] uuids = null)
```

If the user has previously placed an anchor, but can no longer retrieve information about that anchor, you can guide the user back to the location where the anchor was last placed. If the user does not need to retrieve the previous anchor, or wants to place a new anchor in a different location, you can let the user place interactive objects again or capture the current space, and experience your app in the new location.
### Get the UUIDs of spatial anchors
Call `GetAnchorUuid` to get the UUID of a spatial anchor. You can use the returned UUID to load a specific anchor.
```C#
PxrResult GetAnchorUuid(ulong anchorHandle, out Guid uuid)
```

### Locate spatial anchors
Call `LocateAnchor` to allow your app to obtain the real-time location of a spatial anchor, with the purpose of ensuring that the anchor is anchored in a fixed position in the real world. If you do not get the location of the anchor, when the user moves in the scene, the location of the anchor may shift. 
The frequency for calling this API can be determined by yourself according to actual needs, and it is recommended to call it about once per second, with a maximum of once per frame.
```C#
PxrResult LocateAnchor(ulong anchorHandle, out Vector3 position, out Quaternion rotation)
```

### Destroy spatial anchors
Call `DestroyAnchor` to destroy a spatial anchor from the app's memory. If you destroy the anchor immediately after creating it, you will not be able to retrieve that anchor. However, if you create an anchor and then persist it into the PICO device's local disk, even after destroying the anchor, you can still query and load that anchor.
```C#
PxrResult DestroyAnchor(ulong anchorHandle)
```

### Unpersist spatial anchors
Call `UnPersistSpatialAnchorAsync` to unpersist a spatial anchor from the PICO device's local disk. After deletion, the anchor can no longer be queried and loaded.
After a user deletes a virtual object, it is recommended to promptly unpersist the associated anchor. It is also recommended to unpersist anchors that have not been used for a long time to free up system resources.
`UnPersistSpatialAnchorAsync` can only be called once at a time. The next call must wait until the current one completes.

```C#
async Task<PxrResult> UnPersistSpatialAnchorAsync(ulong anchorHandle)
```

The anchors in app's memory and the PICO device's local disk are associated through `anchorHandle`, which acts as a reference to the anchors persisted into the PICO device's local disk. When you call `DestroyAnchor` first, `anchorHandle` is deleted, and you will no longer be able to reference the anchor in the PICO device's local disk. Subsequently, when you call `UnPersistSpatialAnchorAsync` to unpersist a specific anchor, the system will be unable to locate that anchor. In this case, please call `UnPersistSpatialAnchorAsync` first, and then call `DestroyAnchor`.
### About the SpatialAnchorDataUpdated event
Receiving the `SpatialAnchorDataUpdated` event indicates that new spatial anchors have been discovered. You can manage these new anchors as needed, including persisting, loading, destroying, or unpersisting them, as well as retrieving their UUIDs or real-time locations.
When the number of anchors decreases, the system will not push this event. For example, as the user walks around, the system continues to discover new anchors; however, old anchors that were previously discovered will not be automatically deleted as the user moves away.
## About the PXR_Spatial Anchor (Script) component
The PXR_Spatial Anchor (Script) component is for conducting automated control over spatial anchors. It is designed to facilitate the management of a spatial anchor's lifecycle by simplifying tasks such as creating, updating, and persisting spatial anchors.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/203dc01a79c04b9dbf5ddd3cb4b1c4d7~tplv-goo7wpa0wc-image.image" width="450px" />

After adding the PXR_Spatial Anchor (Script) component to a GameObject, the SDK will automatically create an anchor based on the object's Transform and continuously update the anchor's pose. You can manage the anchor through this component. Below is a code sample:
```C#
IEnumerator CreateSpatialAnchor()
{
    // Create a new GameObject
    GameObject object = new GameObject();
    // Add the PXR_Spatial Anchor (Script) component to this GameObject
    var anchor = object.AddComponent<PXR_SpatialAnchor>();
    
    // Wait until this anchor is created
    yield return new WaitUntil(() => anchor.Created);
}

// Get this anchor's UUID
var uuid = anchor.uuid;
// Get this anchor's handle
var handle = anchor.handle;

// Persist this anchor
await anchor.PersistAsync();
// Unpersist this anchor
await anchor.UnPersistAsync();

// Destroy this GameObject so as to destroy the anchor created based on this GameObject
Destroy(object);
```

You can use `QuerySpatialAnchorObjectsAsync` to query the list of GameObjects that have the  PXR_Spatial Anchor (Script) component added to them.
```C#
public static async Task<(PxrResult result, List<GameObject> spatialAnchorObjects)> QuerySpatialAnchorObjectsAsync(Guid[] uuids = null, CancellationToken token = default)
```

## About the SpatialAnchor prefab
The SDK provides a spatial anchor prefab (SpatialAnchor.prefab) in the /Assets/Resources/Prefabs directory. This prefab comes with the PXR_Spatial Anchor (Script) component attached by default, completing the creation process.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d75bcc8fede3456cacf095ddb6b34d85~tplv-goo7wpa0wc-image.image" width="450px" />

You can either drag it directly into the scene for use or instantiate it through code, as shown below:
```C#
// Create a new anchor object and use the specified anchorPrefab to instantiate it
GameObject anchorObject = Instantiate(anchorPrefab);

// Get the PXR_Spatial Anchor (Script) component from the instantiated anchor object and manage the anchor (including deletion, persistence, and unpersistence) using this component
var anchor = anchorObject.GetComponent<PXR_SpatialAnchor>();
```

## Code samples
### Code sample 1
This code sample demonstrates how to create, persist, destroy, and unpersist spatial anchors, as well as how to interact with users through an UI.
```C#
using System;
using UnityEngine;
using UnityEngine.UI;
using System.Collections.Generic;
using Unity.XR.PXR;
using UnityEngine.XR;
using UnityEngine.XR.Interaction.Toolkit;
using System.Threading.Tasks;

// Ensure this script is attached to a GameObject with XRSimpleInteractable component
[RequireComponent(typeof(XRSimpleInteractable))]
public class PXRSample_SpatialAnchor : MonoBehaviour
{
    // XR base interactable object
    private XRBaseInteractable interactable;

    // Anchor handle, uniquely identifies a spatial anchor
    [HideInInspector]
    public ulong anchorHandle;

    // UI text to display the anchor ID
    [SerializeField]
    private Text anchorID;

    // GameObject for the saved icon
    [SerializeField]
    private GameObject savedIcon;

    // UI canvas
    [SerializeField]
    private GameObject uiCanvas;

    // UI buttons
    [SerializeField] private Button btnPersist;        // Button to persist the anchor
    [SerializeField] private Button btnDestroyAnchor;  // Button to destroy the anchor
    [SerializeField] private Button btnDeleteAnchor;   // Button to delete the anchor

    private void Awake()
    {
        // Initialize by hiding the UI canvas
        uiCanvas.SetActive(false);
        // Set the canvas to use the main camera
        uiCanvas.GetComponent<Canvas>().worldCamera = Camera.main;

        // Add click event listeners to the buttons
        btnPersist.onClick.AddListener(OnBtnPressedPersist);
        btnDestroyAnchor.onClick.AddListener(OnBtnPressedDestroy);
        btnDeleteAnchor.onClick.AddListener(OnBtnPressedUnPersist);
    }

    protected void OnEnable()
    {
        // Get the XRBaseInteractable component and add event listeners
        interactable = GetComponent<XRBaseInteractable>();
        interactable.firstHoverEntered.AddListener(OnFirstHoverEntered);
        interactable.lastHoverExited.AddListener(OnLastHoverExited);
        interactable.firstSelectEntered.AddListener(OnFirstSelectEntered);
        interactable.lastSelectExited.AddListener(OnLastSelectExited);
    }

    protected void OnDisable()
    {
        // Cleanup operations can be performed here (currently not implemented)
    }

    private void Start()
    {
        // Initialization operations can be performed here (currently not implemented)
    }

    private void Update()
    {
        // If the UI canvas is active, make it always face the camera
        if (uiCanvas.activeSelf)
        {
            uiCanvas.transform.LookAt(new Vector3(uiCanvas.transform.position.x * 2 - Camera.main.transform.position.x, 
                                                  uiCanvas.transform.position.y * 2 - Camera.main.transform.position.y, 
                                                  uiCanvas.transform.position.z * 2 - Camera.main.transform.position.z), 
                                                  Vector3.up);
        }
    }

    private void LateUpdate()
    {
        // Attempt to locate the spatial anchor
        var result = PXR_MixedReality.LocateAnchor(anchorHandle, out var position, out var rotation);
        if (result == PxrResult.SUCCESS)
        {
            // If successful, update the position and rotation of the current object
            transform.position = position;
            transform.rotation = rotation;
        }
        else
        {
            // Log the result of locating the anchor
            PXRSample_SpatialAnchorManager.Instance.SetLogInfo("LocateSpatialAnchor:" + result.ToString());
        }
    }

    // Handle the first hover enter event
    protected virtual void OnFirstHoverEntered(HoverEnterEventArgs args) => UpdateColor();

    // Handle the last hover exit event
    protected virtual void OnLastHoverExited(HoverExitEventArgs args) => UpdateColor();

    // Handle the first select enter event
    protected virtual void OnFirstSelectEntered(SelectEnterEventArgs args) => UpdateCanvas();

    // Handle the last select exit event
    protected virtual void OnLastSelectExited(SelectExitEventArgs args) => UpdateCanvas();

    // Update the object's color to indicate hover state
    protected void UpdateColor()
    {
        if (interactable.isHovered)
        {
            foreach (var renderer in GetComponentsInChildren<Renderer>())
            {
                // If hovered, set emission color to yellow
                renderer.material.SetColor("_EmissionColor", Color.yellow);
            }
        }
        else
        {
            foreach (var renderer in GetComponentsInChildren<Renderer>())
            {
                // If not hovered, clear emission color
                renderer.material.SetColor("_EmissionColor", Color.clear);
            }
        }
    }

    // Update the display state of the UI canvas
    protected void UpdateCanvas()
    {
        uiCanvas.SetActive(interactable.isSelected);
    }

    // Button event handler to persist the anchor
    private async void OnBtnPressedPersist()
    {
        var result = await PXR_MixedReality.PersistSpatialAnchorAsync(anchorHandle);
        PXRSample_SpatialAnchorManager.Instance.SetLogInfo("PersistSpatialAnchorAsync:" + result.ToString());
        if (result == PxrResult.SUCCESS)
        {
            // If successful, show the saved icon
            ShowSaveIcon();
        }
    }

    // Button event handler to destroy the anchor
    private void OnBtnPressedDestroy()
    {
        PXRSample_SpatialAnchorManager.Instance.DestroySpatialAnchor(anchorHandle);
    }

    // Button event handler to delete the anchor
    private async void OnBtnPressedUnPersist()
    {
        var result = await PXR_MixedReality.UnPersistSpatialAnchorAsync(anchorHandle);
        PXRSample_SpatialAnchorManager.Instance.SetLogInfo("UnPersistSpatialAnchorAsync:" + result.ToString());
        if (result == PxrResult.SUCCESS)
        {
            // If successful, first destroy the anchor
            OnBtnPressedDestroy();
        }
    }

    // Set the anchor handle and update the UI display
    public void SetAnchorHandle(ulong handle)
    {
        anchorHandle = handle;
        anchorID.text = "ID: " + anchorHandle;
    }

    // Show the saved icon
    public void ShowSaveIcon()
    {
        savedIcon.SetActive(true);
    }
}
```

### Code sample 2
The following code sample defines a class named `PXRSample_SpatialAnchorManager`, which is responsible for managing the creation, loading, and destruction of spatial anchors. This class is a MonoBehaviour in Unity and can be attached to a GameObject.
```C#
using System;
using System.Collections; 
using System.Collections.Generic; 
using System.Linq;
using System.Runtime.InteropServices;
using System.Threading.Tasks;
using UnityEngine.UI; 
using Unity.XR.PXR;
using UnityEngine; 
using UnityEngine.XR; 
using UnityEngine.XR.Interaction.Toolkit; 

// Define the Spatial Anchor Manager class
public class PXRSample_SpatialAnchorManager : MonoBehaviour
{
    // Singleton instance
    private static PXRSample_SpatialAnchorManager instance = null;

    // Singleton property
    public static PXRSample_SpatialAnchorManager Instance
    {
        get
        {
            // If instance is null, find it in the scene
            if (instance == null)
            {
                instance = FindObjectOfType<PXRSample_SpatialAnchorManager>();
            }
            return instance; // Return the instance
        }
    }

    public GameObject anchorPrefab; // Anchor prefab
    private bool isCreateAnchorMode = false; // Flag for anchor creation mode
    public Dictionary<ulong, PXRSample_SpatialAnchor> anchorList = new Dictionary<ulong, PXRSample_SpatialAnchor>(); // Dictionary to store anchors
    public Dictionary<ulong, ulong> persistTaskList = new Dictionary<ulong, ulong>(); // Persistent task list
    public Dictionary<ulong, ulong> unPersistTaskList = new Dictionary<ulong, ulong>(); // Non-persistent task list
    private InputDevice rightController; // Right hand controller
    [SerializeField] private GameObject anchorPreview; // Anchor preview object
    [SerializeField] private GameObject menuPanel; // Menu panel
    [SerializeField] private Button btnCreateAnchor; // Button to create anchor
    [SerializeField] private Button btnLoadAnchors; // Button to load anchors

    private bool btnAClick = false; // A button click state
    private bool aLock = false; // A button lock state
    private bool btnAState = false; // A button current state
    private bool gripButton = false; // Grip button state

    public Text tipsText; // Tips text display
    private int maxLogCount = 5; // Maximum number of log entries
    private Queue<string> logQueue = new Queue<string>(); // Queue for logs

    // Initialization
    void Start()
    {
        PXR_Manager.EnableVideoSeeThrough = true; // Enable video see-through

        StartSpatialAnchorProvider(); // Start the spatial anchor provider

        // Add button click event listeners
        btnCreateAnchor.onClick.AddListener(OnBtnPressedCreateAnchor);
        btnLoadAnchors.onClick.AddListener(OnBtnPressedLoadAllAnchors);

        // Show buttons
        btnCreateAnchor.gameObject.SetActive(true);
        btnLoadAnchors.gameObject.SetActive(true);

        // Get the right hand controller
        rightController = InputDevices.GetDeviceAtXRNode(XRNode.RightHand);
    }

    // Asynchronously start the spatial anchor provider
    private async void StartSpatialAnchorProvider()
    {
        var result = await PXR_MixedReality.StartSenseDataProvider(PxrSenseDataProviderType.SpatialAnchor); // Start spatial anchor data provider
        SetLogInfo("StartSenseDataProvider:" + result); // Log the result
        if (result == PxrResult.SUCCESS) // If successful
        {
            var result2 = await PXR_MixedReality.QuerySpatialAnchorAsync(); // Query spatial anchors
            SetLogInfo("LoadSpatialAnchorAsync:" + result2.result.ToString() + result2.anchorHandleList.Count); // Log the result
            if (result2.result == PxrResult.SUCCESS) // If query successful
            {
                // Iterate through anchor handle list
                foreach (var key in result2.anchorHandleList)
                {
                    if (!anchorList.ContainsKey(key)) // If the anchor is not in the list
                    {
                        GameObject anchorObject = Instantiate(anchorPrefab); // Instantiate the anchor prefab
                        PXRSample_SpatialAnchor anchor = anchorObject.GetComponent<PXRSample_SpatialAnchor>(); // Get the anchor component
                        anchor.SetAnchorHandle(key); // Set the anchor handle

                        // Locate the anchor
                        PXR_MixedReality.LocateAnchor(key, out var position, out var orientation);
                        anchor.transform.position = position; // Set anchor position
                        anchor.transform.rotation = orientation; // Set anchor rotation
                        anchorList.Add(key, anchor); // Add to the anchor list
                        anchorList[key].ShowSaveIcon(); // Show save icon
                    }
                }
            }
        }
    }

    // Register event when enabled
    void OnEnable()
    {
        PXR_Manager.SpatialAnchorDataUpdated += SpatialAnchorDataUpdated; // Register anchor data update event
    }

    // Unregister event when disabled
    void OnDisable()
    {
        PXR_Manager.SpatialAnchorDataUpdated -= SpatialAnchorDataUpdated; // Unregister anchor data update event
    }

    // Update is called once per frame
    void Update()
    {
        ProcessKeyEvent(); // Process key events
        
        menuPanel.SetActive(gripButton); // Show menu panel based on grip button state

        // If in create anchor mode and button is clicked
        if (isCreateAnchorMode && btnAClick)
        {
            CreateSpatialAnchor(anchorPreview.transform); // Create spatial anchor
        }
    }

    // Process key events
    private void ProcessKeyEvent()
    {
        rightController.TryGetFeatureValue(CommonUsages.primaryButton, out btnAState); // Get A button state
        if (btnAState && !aLock) // If A button is pressed and not locked
        {
            btnAClick = true; // Set click state
            aLock = true; // Lock the button
        }
        else
        {
            btnAClick = false; // Reset click state
        }
        if (!btnAState) // If A button is not pressed
        {
            btnAClick = false; // Reset click state
            aLock = false; // Unlock the button
        }

        // Get left hand grip button state
        InputDevices.GetDeviceAtXRNode(XRNode.LeftHand).TryGetFeatureValue(CommonUsages.gripButton, out gripButton);
    }

    // Anchor data updated event
    private void SpatialAnchorDataUpdated()
    {
        SetLogInfo("SpatialAnchorDataUpdated:"); // Log update
        OnBtnPressedLoadAllAnchors(); // Load all anchors
    }

    // Create anchor button event
    private void OnBtnPressedCreateAnchor()
    {
        isCreateAnchorMode = !isCreateAnchorMode; // Toggle anchor creation mode
        if (isCreateAnchorMode) // If entering create mode
        {
            btnCreateAnchor.transform.Find("Text").GetComponent<Text>().text = "CancelCreate"; // Update button text
            anchorPreview.SetActive(true); // Show anchor preview
        }
        else // If exiting create mode
        {
            btnCreateAnchor.transform.Find("Text").GetComponent<Text>().text = "CreateAnchor"; // Restore button text
            anchorPreview.SetActive(false); // Hide anchor preview
        }
    }

    // Asynchronously load all anchors
    private async void OnBtnPressedLoadAllAnchors()
    {
        var result = await PXR_MixedReality.QuerySpatialAnchorAsync(); // Query all spatial anchors
        SetLogInfo("LoadSpatialAnchorAsync:" + result.result.ToString() + result.anchorHandleList.Count); // Log the result
        if (result.result == PxrResult.SUCCESS) // If successful
        {
            foreach (var key in result.anchorHandleList) // Iterate through anchor handles
            {
                if (!anchorList.ContainsKey(key)) // If the anchor is not in the list
                {
                    GameObject anchorObject = Instantiate(anchorPrefab); // Instantiate the anchor prefab
                    PXRSample_SpatialAnchor anchor = anchorObject.GetComponent<PXRSample_SpatialAnchor>(); // Get the anchor component
                    anchor.SetAnchorHandle(key); // Set the anchor handle

                    // Locate the anchor
                    PXR_MixedReality.LocateAnchor(key, out var position, out var orientation);
                    anchor.transform.position = position; // Set position
                    anchor.transform.rotation = orientation; // Set rotation
                    anchorList.Add(key, anchor); // Add to the anchor list
                    anchorList[key].ShowSaveIcon(); // Show save icon
                }
            }
        }
    }

    // Asynchronously create a spatial anchor
    private async void CreateSpatialAnchor(Transform transform)
    {
        var result = await PXR_MixedReality.CreateSpatialAnchorAsync(transform.position, transform.rotation); // Create anchor
        SetLogInfo("CreateSpatialAnchorAsync:" + result.ToString()); // Log the result
        if (result.result == PxrResult.SUCCESS) // If successful
        {
            GameObject anchorObject = Instantiate(anchorPrefab); // Instantiate the anchor prefab
            PXRSample_SpatialAnchor anchor = anchorObject.GetComponent<PXRSample_SpatialAnchor>(); // Get the anchor component
            if (anchor == null) // If the anchor component doesn't exist
            {
                anchor = anchorObject.AddComponent<PXRSample_SpatialAnchor>(); // Add the anchor component
            }
            anchor.SetAnchorHandle(result.anchorHandle); // Set the anchor handle

            anchorList.Add(result.anchorHandle, anchor); // Add to the anchor list

            // Get the anchor's UUID
            var result1 = PXR_MixedReality.GetAnchorUuid(result.anchorHandle, out var uuid);
            SetLogInfo("GetUuid:" + result1.ToString() + "  " + (result.uuid.Equals(uuid)) + "Uuid:" + uuid); // Log UUID information
        }
    }

    // Destroy a spatial anchor
    public void DestroySpatialAnchor(ulong anchorHandle)
    {
        var result = PXR_MixedReality.DestroyAnchor(anchorHandle); // Destroy the anchor
        SetLogInfo("DestroySpatialAnchor:" + result.ToString()); // Log the result
        if (result == PxrResult.SUCCESS) // If successful
        {
            if (anchorList.ContainsKey(anchorHandle)) // If the anchor is in the list
            {
                Destroy(anchorList[anchorHandle].gameObject); // Destroy the anchor object
                anchorList.Remove(anchorHandle); // Remove from the list
            }
        }
    }

    // Set log information
    public void SetLogInfo(string log)
    {
        if (logQueue.Count >= maxLogCount) // If the log queue reaches maximum entries
        {
            logQueue.Dequeue(); // Remove the oldest log
        }
        logQueue.Enqueue(log); // Add the new log

        Debug.Log("PXRSample_SpatialAnchorManager" + log); // Output to console
        
        tipsText.text = string.Join("\n", logQueue.ToArray()); // Update tips text with logs
    }
}
```

## API reference
For more details on Spatial Anchor APIs, such as parameter descriptions and returns, refer to the [API reference](/reference/unity/client-api/PXR_MixedReality/).


# --- END: Spatial Anchor.md ---



# --- BEGIN: Spatial Audio.md ---

Compared with traditional stereo audio rendering, spatial audio rendering spatializes sounds to a greater extent by covering audio sources from all directions in a space, including those on the horizontal plane and above and below listeners. In addition, spatial audio rendering enables listeners to perceive a more realistic change in sound. For example, when a listener gets closer to the audio source, the sound gets louder.
## Development environment

* PICO device models: PICO Neo3, PICO 4, and PICO 4 Ultra series
* PICO device's system version: 5.11.0 or later
* Unity version: The PICO Spatial Audio Renderer supports the following Unity versions:
   * 2021.1.9f1c1
   * 2020.3.21f1 LTS
   If you successfully use the PICO Spatial Audio Renderer in other Unity versions, please let us know. Thank you.

## SpatialAudio folder overview
After importing the Pico Unity Integration SDK into your project, you can access the SpatialAudio folder under the Packages/Pico Integration directory. The table below illustrates what the folder contains.
| **Sub-folder** | **Content** |
| --- | --- |
| Plugins | Stores the dynamic libraries for all supported hardware platforms. You can delete unnecessary libraries if needed. |
| Prefabs | Stores prefabs. |
| Runtime | Stores the original C# scripts required for using spatial audio rendering, including: <br> Basic scripts: <br>  <br> * PXR_Audio_Spatializer_Context.cs <br> * PXR_Audio_Spatializer_Audio Source.cs <br> * PXR_Audio_Spatializer_Ambisonic Source.cs <br> * PXR_Audio_Spatializer_Audio Listener.cs <br>  <br> Utility scripts: <br>  <br> * PXR_Audio_Spatializer_API.cs <br> * PXR_Audio_Spatializer_Types.cs <br>  <br> Environmental acoustics simulation scripts: <br>  <br> * PXR_Audio_Spatializer_Scene Geometry.cs <br> * PXR_Audio_Spatializer_Scene Material.cs |
| Samples | Stores sample audio clips which you can try or use. |
## Learn about components
### PXR_Audio_Spatializer_Audio Source
The PXR_Audio_Spatializer_Audio Source component is used to set audio source-related parameters, including basic parameters, attenuation-related parameters, and directivity-related parameters.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/454cb25405854e19a2f38964f47dcda3~tplv-goo7wpa0wc-image.image" width="400px" />

Below are parameter descriptions of basic parameters:
| **Parameter** | **Description** |
| --- | --- |
| Source Gain (dB) | For setting the gain of audio source (unit: dB). |
| Reflection Gain (dB) | For setting the gain of the reflected sound from the sound source (unity: dB). |
| Source Size (meters) | For setting the radius of audio source (unit: meter). |
| Enable Doppler | Sets whether the source simulates the Doppler effect. <br>  <br> * When enabled, the realism of the direct and reflected sound of the source improves, but the CPU usage for the audio thread increases slightly. <br> * When disabled, realism decreases slightly, but CPU usage is significantly reduced. |
Below are the descriptions of attenuation-related parameters:
| **Parameter** | **Description** |
| --- | --- |
| Source Attenuation Mode | Sets how the volume of an audio source attenuates with distance change. Available options are: <br>  <br> * **None**: the volume of an audio source will not attenuate with distance change. <br> * **Fixed**: Fix the volume of an audio source so that it will not attenuate with distance change; <br> * **Inverse Square**: The volume of an audio source is inversely proportional to the square of the distance between the source and the listener. <br> * **Custom** (do not use this option) |
| Min Attenuation Distance | Sets the minimum distance from which the volume of an audio source starts attenuating. When the distance between the audio source and the listener is below the minimum attenuation distance, the volume will not attenuate with distance change. In other words, attenuation will be 0dB. <br> ***Note***: The value set for Min Attenuation Distance should NOT be greater than that for Max Attenuation Distance. Otherwise, the volume attenuation curve will be rather abnormal. |
| Max Attenuation Distance | Sets the maximum distance from which the volume of an audio source stops attenuating. When the distance between the audio source and the listener is beyond the maximum attenuation distance, the volume will not attenuate with distance change. <br> ***Note***: The value set for Max Attenuation Distance must be greater than that for Min Attenuation Distance. Otherwise, the volume attenuation curve will be rather abnormal. |
In reality, the energy of sound waves emitted by a sound source spreads in a non-isotropic manner, and it is represented by a polar coordinate system that is related to the angle of sound wave emission. This representation is known as the directivity (Polar Pattern) of the sound source. The origin of the polar coordinate system is located at the sound source, with the 0-degree direction aligned with the direction of the sound source. 
Below are the descriptions of directivity-related parameters:
| **Parameter** | **Description** |
| --- | --- |
| Alpha | This parameter determines the shape of polar pattern, which includes omnidirectional, cardioid, figure-8, as well as all intermediate shapes. The following diagram illustrates the impact of the 'alpha' value on the polar pattern when the 'order' is set to '1'. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97039fcb522f42e4b8ff5cd93f25fad8~tplv-goo7wpa0wc-image.image) |
| Order | The parameter determines the sharpeness of polar pattern. The following diagram illustrates the impact of the 'order' value on the polar pattern when the 'alpha' value is set to '0.5'. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cbec494628f4a858f8b7857c5f40f3b~tplv-goo7wpa0wc-image.image) |
### PXR_Audio_Spatializer_Audio Listener
The PXR_Audio_Spatializer_Audio Listener is used to specify the result of spatial audio rendering, which refers to the output mode of binaural audio signals.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b3e869d8abb4cc5a0fea712cc6938c8~tplv-goo7wpa0wc-image.image" width="450px" />

Below are the descriptions of the available values for the Output Method parameter:
| **Value** | **Description** |
| --- | --- |
| On Audio Filter Read | To output spatial audio signals in the `OnAudioFilterRead` callback of the PXR_Audio_Spatializer_Audio Listener component and directly superimpose the spatial audio signal onto Unity's final output signal. This is how the PICO Audio Spatial plugin often processes audio signals. |
| Pico Audio Router | To simultaneously output spatial audio signals in all Pico Audio Router plugins (as shown in the figure below) of the Unity Audio Mixer. This output method is designed to facilitate independent volume processing and post-processing of spatial audio for developers. <br> ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9da50a2ab027439fa4d569484e90e03f~tplv-goo7wpa0wc-image.image) |
The SampleScene_output_to_mixer demo incorporates Unity Audio Mixer and some interesting post-processing effects. You can find this demo under the /SpatialAudio/Samples directory.
### PXR_Audio_Spatializer_Context
The PXR_Audio_Spatializer_Context component is used to set rendering qualities. Below are parameters descriptions:
| **Parameter** | **Description** |
| --- | --- |
| Spatializer Api Impl | For setting the audio backend. You can select **Unity** or **Wwise**. |
| Rendering Quality | For setting audio rendering quality. |
| Late Init Event | For defining a set of events that takes place after spatial audio renderer initialization but before audio processing. It is set as empty by default. |
## Set up different spatial audio rendering modes
### Free field
A free field is a sound field that only simulates the location of the audio source while ignoring all environmental acoustic phenomena such as reflection sounds. Below are the steps to set up a free field:

1. Open your project in the Unity Editor.
2. From the top menu bar, select **GameObject** > **3D Object** to create an object (object 1) in the scene.
3. In the **Hierarchy** window, select **object 1**.
   The components for configuring object 1 are then displayed in the Inspector window.
4. Click **Add Component** at the bottom of the **Inspector** window.
5. Add the **PXR_Audio_Spatializer_Context (Script)** component to object 1.
6. Configuring **Rendering Quality** as needed.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/18bdae42e85244fdb85f2bd175c15637~tplv-em5hxbkur4-noop.image?width=819&height=135)
7. Create another object (object 2). For a better visual effect, creating a **sphere** is recommended.
8. Add the **PXR_Audio_Spatializer_Audio Source (Script)** component to object 2. After that:
   * The **Audio Source** component is then automatically added to object 2. It is recommended that you keep **Spatial Blend** as **0**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/a2a02db68e454a268c05027ddb04c201~tplv-em5hxbkur4-noop.image?width=815&height=775)
   * The **Scene** view then displays the following:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/842b8cecd21b497d880a4988f7faffb4~tplv-em5hxbkur4-noop.image?width=1206&height=634)
9. Find the object where the **Audio Listener** component is added. It is typically the **Main Camera**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f35cd8cfc81d4fde8b52d5bb988b6937~tplv-em5hxbkur4-noop.image?width=812&height=42)
10. Select this object.
11. Click **Add Component** at the bottom of the **Inspector** window.
12. Add the **PXR_Audio_Spatializer_Audio Listener (Script)** component to this object.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/066c4a3f62a1448386c51d0c77d7bf1f~tplv-em5hxbkur4-noop.image?width=812&height=102)

At this point, you have accessed the PICO Spatial Audio Renderer into your project. Next, you need to spatialize audio signals through the following steps:

1. Select a testing file and import it into your project.
2. Find the **Audio Source** component on the audio source.
3. In **AudioClip** , select an audio clip.
4. Check **Play On Awake**.
   The Audio Source component starts as soon as the audio source object is enabled.
5. Check **Loop**.
   The audio clip replays after it finishes.
6. Play the audio clip.
   You will hear spatialized sounds.

### Environmental acoustic simulation
Real-time environmental acoustic simulation is a core feature the PICO Spatial Audio Renderer provides. It can simulate many acoustic phenomena such as reflection sounds and occlusion. This part walks you through the steps to set up environmental acoustic simulation:

1. In your virtual scene, import or create an environment model.
2. In the environment model object that you want for environmental acoustic simulation, add the **PXR_Audio_Spatializer_SceneGeometry (Script)** component to it. 
   Once added, the **PXR_Audio_Spatializer_SceneMaterial (Script)** component will be automatically added.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca06823d152e46b588693abe6dcccc43~tplv-goo7wpa0wc-image.image)
3. In the **PXR_Audio_Spatializer_SceneGeometry (Script)** panel, configure the following parameters as needed:
   | **Parameter** | **Description** |
   | --- | --- |
   | Include Children | To determine whether this acoustic geometry includes its child objects. |
   | Visualize Mesh In Editor | To use a white frame to visualize the object associated with this acoustic geometry. This parameter only works in Unity Editor and will not affect play mode or build. |
   | Static mesh backing utilities | The tool for baking static meshes. <br>  <br> * Layer: specify the layer of the to-be-baked mesh in this parameter <br> * Bake: click this button to start baking the mesh <br> * Clear: click this button to delete the baked mesh |
   | Baked Static Mesh | The baked mesh will be presented here. |
4. In the **PXR_Audio_Spatializer_SceneMaterial (Script)** panel, configure the following parameters as needed:
   **Note**
   You can totally configure these parameters by yourself, or you can use PICO's preset materials and edit these parameters for them as needed.

   | **Parameter** | **Description** |
   | --- | --- |
   | Material Preset | Includes PICO's predefined settings for the Absorption, Scattering, and Transmission parameters. <br> If you want to customize the above parameters, select "Custom". If you want to use predefined settings, select the target option from the list. |
   | Absorption band XXXX Hz | The amount of sound energy absorbed by the acoustic material. |
   | Scattering | Defines the amount of sound energy scattered by this acoustic material.  <br> In an environment with a high scattering rate, the reflection sounds you hear would be more like reverbs; while in an environment with a low scattering rate, the reflection sounds you hear would be more like distinctive echoes. In short: <br>  <br> * The higher the scattering rate, the louder the reverb and the lower the echoes. <br> * The lower the scattering rate, the lower the reverb and the louder the echoes. |
   | Transmission | Defines the amount of sound energy that can be transmitted through this acoustic material. The higher the transmission rate, the stronger the sound transmitted through this acoustic material and vice versa. <br> ***Note***: Materials with a higher scattering rate will have a lower transmission rate. |

### Ambisonics
Ambisonics is a full-sphere surround sound effect that covers audio sources on the horizontal plane and below and above the listener, thereby giving the listener a highly immersive audio experience. The PICO Spatial Audio Renderer can auralize first-order Ambix-formatted ambisonic signals. Below are the steps to set up ambisonics:

1. Open your project in the Unity Editor.
2. From the top menu bar, select **Edit** > **Project Settings**.
   The Project Settings window appears.
3. From the left navigation bar, select **Audio**.
   The Audio pane appears on the right.
4. Set **Ambisonic Decoder Plugin** as **Pico Ambisonic Decoder**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/3bf12e4845db4401b79a253d6219fdec~tplv-em5hxbkur4-noop.image?width=1394&height=1002)
5. In the **Project** window, right-click the **Asset** folder.
6. From the shortcut menu, select **Create** > **Audio Mixer** to create an audio mixer as the ambisonic rendering bus.
7. (Optional) Rename the audio mixer as, for example, Ambisonics_bus.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/52eecd7710704a969564a96cbfb78997~tplv-em5hxbkur4-noop.image?width=1197&height=456)
8. Click the **arrow** icon on the right side of **Ambisonics_bus**.
   The following menu appears:
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/b4435d2596b64329bb80f4ee7f72873b~tplv-em5hxbkur4-noop.image?width=1191&height=454)
9. Click **Master**.
   The parameters you can configure for the Master channel appear in the Inspector window.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/494f10d9df6c4e64b0fdce2baf37e667~tplv-em5hxbkur4-noop.image?width=848&height=428)
10. Click **Add Effect**.
11. Select **Pico Ambisonic Renderer** from the menu.
   The ambisonic renderer is then added to the Master channel.
12. Create an object in the scene.
13. Add the **PXR_Audio_Spatializer_Ambisonic Source** component to this object.
   The Audio Source component is then automatically added to this object as well.
14. In the **Audio Source** pane, set **Output** as **Master (Ambisonic_bus)**.

At this point, you have set up ambisonics. You can then try it through the following steps:

1. In the **Project** window, go to **Packages** > **Pico Integration** > **SpatialAudio** > **Samples** > **Audio**.
   You will enter the Audio folder.
2. Find the **loop_FOA_48k** audio clip.
3. In the **Hierarchy** window, select the object you created earlier.
4. In the **Audio Source** pane, set **AudioClip** to **loop_FOA_48k** for this object. You can do this through either of the following ways:
   * Click the **circle** icon in the **AudioClip** parameter and select the target audio clip in the pop-up window.
   OR
   * Drag the target audio clip to the **AudioClip** parameter.
   If you want to use external audio clips, make sure that:
   
      * The audio clip is first-order Ambix-formatted.
      * The **Ambisonic** option is checked for the audio clip.

5. Check **Play On Awake** and **Loop**.
6. Play the audio clip.
   You can hear a music piece placed in front of the listener. The music piece moves in the following trajectory:
   1. Moves horizontally and clockwise around the listener for one cycle.
   2. Moves vertically around the listener for one cycle (upwards first and then moves downwards).

### Mixed reality spatial audio
This mode is only supported by PICO 4 Ultra series devices.

PICO 4 Ultra series devices support real-time dynamic scanning of real-world scenes and convert the scene content into spatial meshes. The PICO Spatial Audio Plugin combines this capability with spatial audio rendering, allowing virtual sound sources to interact with the user's real environment, producing the following effects:

* Virtual sound waves reflect off the surfaces of the real environment (i.e., the surface of the real-time spatial meshes).
* Virtual sound waves experience volume attenuation as they pass through the surfaces of the real world (i.e., the real-time spatial meshes).

Use the following steps to set up spatial audio for mixed reality scenes:

1. On the **PXR_Manager (Script)** component panel, check the **Spatial Mesh** checkbox to enable the [Spatial Mesh](/en_spatial-mesh) capability and then select a desired LOD.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d97869805aa340f0bc0809a5b2a81331~tplv-goo7wpa0wc-image.image)
2. Add the **PXR_Spatial Mesh Manager (Script)** component to any GameObject in the scene, and then add any prefab with the MeshFilter in **Mesh Prefab** (you can refer to the prefab provided in /SpatialAudio/Samples/Resources/MeshPrefab as needed).
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29ee44272f8d42be8fa4e6b1a70251f8~tplv-goo7wpa0wc-image.image)
3. Add the **PXR_Audio_Spatializer_MR Scene Geometry Manager** component to any GameObject in the scene.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/180dac61a2a6470884235e4c26b47c2d~tplv-goo7wpa0wc-image.image)

> You can refer to PICO's sample scene in /SpatialAudio/Samples/SpatialMesh_with_SpatialAudio.unity as needed.

### Important notes for macOS developers
If you are using the macOS operating system, due to the Gatekeeper mechanism, the system will prevent loading of spatial audio dynamic libraries. Therefore, you may see the following warning messages:
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38d454ea97c34b62bd42cb09a2f85428~tplv-goo7wpa0wc-image.image)
When seeing the above warning messages, use the following steps to solve them:

1. Go to **System Preferences** > **Security & Privacy**.
   You will see the following information in the Security & Privacy window: “libPicoAmbisonicDecoder.dylib” (or ”libPicoSpatializer.dylib“) was blocked from use because it is not from an identified developer.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f569ce5ee7c0421486d3b7f6c78156b1~tplv-goo7wpa0wc-image.image)
2. Click the **Allow Anyway** button next to the information.
   If the system still prompts the above warning messages, click **OK** on the pop-up window.

3. Restart your Unity project.
   If Unity or macOS do not report these warning messages anymore, the Pico Spatial Audio Renderer is successfully installed in your Unity project.

## Functions
The PICO Spatial Audio Renderer provides functions that you can call to customize your own acoustic scenes.
### PXR_Audio_Spatializer_Audio Source
| **Function** | **Description** |
| --- | --- |
| `Resume` | Resumes the audio source. |
| `SetGainDB` | Sets the gain of the audio source (unit: dB). |
| `GetGainDB` | Gets the gain of the audio source (unit: dB). |
| `SetReflectionGainDB` | Sets the reflection gain of the audio source (unit: dB). |
| `GetReflectionGainDB` | Gets the reflection gain of the audio source (unit: dB). |
| `SetSize` | Sets the radius of the audio source (unit: meter). |
| `GetSize` | Gets the radius of the audio source (unit: meter). |
| `SetDopplerStatus` | Sets whether to enable the Doppler effect when running the audio source. <br> ***Note***: If the **Enable Doppler** option is not enabled during building, this function will be invalid. |
| `GetDopplerStatus` | Gets whether to enable the Doppler effect when running the audio source. |
| `GetAttenuationMode` | Gets the attenuation mode of the audio source. |
| `SetMinAttenuationRange` | Sets the minimum distance from which the volume of an audio source starts attenuating. When the distance between the audio source and the listener is below the minimum attenuation distance, the volume will not attenuate with distance change, in other words, attenuation will be 0dB. <br> ***Note***: The value set for Min Attenuation Distance should NOT be greater than that for Max Attenuation Distance. |
| `GetMinAttenuationRange` | Gets the minimum distance from which the volume of an audio source starts attenuating. |
| `SetMaxAttenuationRange` | Sets the maximum distance from which the volume of an audio source stops attenuating. When the distance between the audio source and the listener is beyond the maximum attenuation distance, the volume will not attenuate with distance change. <br> ***Note***: The value set for Max Attenuation Distance must be greater than that for Min Attenuation Distance. |
| `GetMaxAttenuationRange` | Gets the maximum distance from which the volume of an audio source stops attenuating. |
| `SetDirectivity` | Sets the polar pattern of the audio source. <br>  <br> * alpha: the shape of polar pattern. <br> * order: the sharpeness of polar pattern. |
### PXR_Audio_Spatializer_Ambisonic Source
`Resume()`: Resumes the audio source.
### PXR_Audio_Spatializer_Context
`SetRenderingQuality(PXR_Audio.Spatializer.RenderingMode quality)`: Sets the spatial audio rendering quality.
## Tips
### About Unity settings
By default, after modifying the C# code, the Unity Editor will immediately start compilation even if the audio is playing. For PICO's spatial audio rendering feature, if the above-mentioned situation takes place, the Unity Editor will crash. Therefore, it is recommended that you modify Unity settings to avoid this issue. Below are the steps to follow:

1. From the top menu bar, select **Edit** > **Preferences**.
   The Preferences window appears.
2. From the left navigation pane, select **General**.
3. Set **Script Changes While Playing** to **Recompile After Finished Player** or **Stop Playing And Compile**.
   ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/090c4fbe9ebb457d95c382863bcce873~tplv-em5hxbkur4-noop.image?width=1280&height=993)

### About the number of audio sources
Environmental acoustic simulation and Doppler effect simulation can cause a large CPU load. Therefore, when using environmental acoustic simulation, make sure that the number of audio sources that are being played concurrently and have Doppler effect simulation on is within 20.
### About the Doppler effect
If the Doppler effect is enabled for the audio source, the direct sounds and reflection sounds from the audio source will be more realistic while bringing up CPU consumption at the same time, and vice versa.
If you want to achieve the Doppler effect while keeping the CPU and memory usage low, try the following method:

1. Choose some audio sources with an acceptable but slightly less realistic sound.
2. Uncheck the **Enable Doppler** option for the audio source.
3. Set **Spatial Blend** to **1**.
   In this case, the audio signal will be reconverted to mono format when routed into the audio renderer without being spatialized. This uses Unity's own Doppler effect while not using Unity's directional spatialization algorithm, thus striking a balance between sound quality and performance when there is a large number of sound sources.

### Best practices for environmental acoustic simulation

* For scene objects made of different materials, their meshes need to be segmented. After that, by attaching the PXR_Audio_Spatializer_SceneMaterial component to their respective GameObjects, it is easier to set independent acoustic materials for them, thereby more accurately simulating the environmental sound.
* When using environmental acoustic simulation, if the listener and sound source are separated by complex scene geometry and there is a high-order reflection path between them, you might be unable to hear reflection sounds. This rarely happens if you use the latest Pico Spatializer plugin.
   If you come across this problem, it is recommended to upgrade the Pico Spatializer plugin to the latest version first. If the problem still exists after that, try the following solutions:
   * Avoid this issue through gameplay design. Simply do not let players be able to go to places where errors can occur.
   * Separate the mesh into multiple GameObjects, and only add the **PXR_Audio_Spatializer_Scene Geometry** component to large walls instead of small objects with detailed geometries such as tables and columns.
   * If the problem still exists, add some **Pico Sound Reflection Object** to places where you want sounds to be reflected. You can find Pico Sound Reflection Object **** under the /Pico Spatial Audio/Prefabs directory.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf59151406fc4abe8896728d62110cb2~tplv-goo7wpa0wc-image.image)

## Sample
The PICOSpatialAudioSample demonstrates the spatial audio functionality provided by the PICO Unity Integration SDK. Within this sample, you can configure spatial audio parameters, move around the scene, and play audio sources. For more details, refer to the "[Spatial audio sample](/en_spatial-audio-sample)" article.
## Known issue
For macOS users, if you run any samples from /Packages/Pico Integration/SpatialAudio/Samples in the Unity Editor and press any keyboard key, you might hear some beeping sound. This is caused by a known Unity bug that can be fixed by Unity only. You can click [here](https://issuetracker.unity3d.com/issues/macos-funk-error-sound-plays-when-pressing-any-non-shortcut-key-in-play-mode) to discuss this issue in Unity Community.


# --- END: Spatial Audio.md ---



# --- BEGIN: Spatial Mesh.md ---

The Spatial Mesh feature can dynamically scan the real-world scene in real-time, and then convert the contents of the scene into spatial meshes.
## About spatial meshes
Spatial meshes represents the information of the surface of a space. When the app starts mesh scanning, a lot of triangle meshes will be gradually generated for the space the user has looked around. The spatial mesh data also includes information such as the mesh bounding box and semantic classifications.




![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d42488e2e5844125a52e8ebcb2545327~tplv-goo7wpa0wc-image.image)




![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d91072977c64c509bd289d95f3822fd~tplv-goo7wpa0wc-image.image)




![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e18c04049594f72a2217ebd15cfe067~tplv-goo7wpa0wc-image.image)




Spatial meshes are primarily the representation of the physical environment in a mixed reality scene. By reconstructing the physical environment into spatial meshes, it becomes easier to enable interactions between virtual and real-world objects. For example, a virtual ball hitting a real-world wall can be made to bounce back. Additionally, by working with depth sensing technology, it is possible to achieve occlusion between virtual and real-world objects.
You can obtain spatial meshes' vertex, index, and semantic information in real time through the SDK, and you can set different LODs (level of detail) to acquire meshes with varying levels of detail according to your needs. Additionally, you can also use the built-in mesh renderer component in the SDK to visualize meshes.
## Tech summary
After creating the spatial mesh provider, PICO device will scan the current space. As the user moves in the current space, the algorithm continuously perceives the depth and semantic information in front of the user's field of view in real-time and integrates this information into spatial meshes. If the scanned area within the field of view changes, the spatial meshes are updated accordingly to maintain consistency with the real-world environment.
Currently, when reading meshes in real time, only the mesh information within a radius of approximately 5 meters centered on the user's HMD is loaded. If the app needs to record mesh information over a larger area, it needs to store the corresponding data.
## Recommendations
It is recommended to use spatial meshes based on actual needs to reduce system overhead. If your app requires the complete mesh information of a space, it is recommended to first guide the user to look around the space, so that the entire space can be fully scanned. After generating the corresponding spatial mesh data, the user can then continue to experience the rest of the app.
If you do not need to update the information of spatial meshes in real time after creating them, it is recommended to store the current mesh data and continue using it, while also turning off the spatial mesh provider to reduce resource usage. Additionally, you can consider using a lower LOD to reduce the number of meshes.
## Development environment

* PICO device models: PICO 4 series, PICO 4 Ultra series
* PICO device's system version: 5.14.0 or later

## Enable the Spatial Mesh capability for your app
Before using spatial mesh data, you need to enable the Spatial Mesh capability for your app in the Unity Editor.

1. Add the **XR Origin** object and add the **PXR_Manager (Script)** component to it.
2. On the **PXR_Manager (Script)** panel of the **Inspector** window, check the **Spatial Mesh** checkbox.
3. Set the **LOD** parameter according to actual needs. 
   LOD affects the number and accuracy of spatial meshes: the lower the level, the fewer triangles there are per unit surface area, resulting in a corresponding decrease in accuracy.
   | **LOD**  | **Number of Meshes** |
   | --- | --- |
   | High | 250 triangle meshes per square meter.  |
   | Medium | 125 triangle meshes per square meter. |
   | Low | 80 triangle meshes per square meter. |
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c97aed86a8741c9a483a7237e0846fb~tplv-goo7wpa0wc-image.image)

## Set up spatial meshes
You can use the PXR_Spatial Mesh Manager (Script) component provided by the SDK to display spatial meshes. If you use this approach, you can directly add the PXR_Spatial Mesh Manager (Script) component to the desired GameObject, and then add the mesh prefab to display the spatial mesh. In addition, you can configure callback functions for spatial meshes and customize the colors of spatial meshes.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4a1e4838ddb47849a149e76e9942dd0~tplv-goo7wpa0wc-image.image" width="450px" />

### **Configure the spatial mesh prefab**
The **Mesh Prefab** parameter is used to configure the spatial mesh prefab. This prefab must contain at least the **Mesh Filter** component. If you want to display the scanned mesh, it should also include the **Mesh Renderer** component, as shown below:
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a57bd6d20a14ceb9749482d23a52a99~tplv-goo7wpa0wc-image.image" width="500px" />

### Configure Unity Event callback functions
The SDK provides [Unity Events](https://docs.unity.cn/cn/2021.1/Manual/UnityEvents.html) on top of the existing spatial mesh events (Action). With UnityEvent, user-driven callbacks can persist from edit time to runtime without additional programming or script configuration. You can configure callback functions for the following Unity Events:

* **On Spatial Mesh Added (Guid, GameObject)**: Triggered when a new spatial mesh is detected and added to the scene.
* **On Spatial Mesh Updated (Guid, GameObject)**: Triggered when an existing spatial mesh is updated (for example, when its shape or position changes).
* **On Spatial Mesh Removed (Guid, GameObject)**: Triggered when a spatial mesh is removed.

### Configure the color of a spatial mesh
In the Custom Mesh Color section, you can configure custom colors for spatial meshes of various semantics, enriching the visual effects of the scene.
## Manage the lifecycle of spatial mesh provider
If you have used the PXR_Spatial Mesh Manager (Script) component, you can listen to the following events to get mesh handling results.
```C#
// Guid is the unique identifier for a mesh object; GameObject is the instance of the mesh object
public static Action<Guid, GameObject> MeshAdded; // the drawing of new meshes has been complete
public static Action<Guid, GameObject> MeshUpdated; // the drawing of updated meshed has been complete
public static Action<Guid> MeshRemoved; // the removal of disappeared mesh has been complete
```

If you want to create your own logic to control the display and hiding of spatial meshes, you can listen to the `SpatialMeshDataUpdated` event to get notified when spatial mesh data is updatde. This event receives the `PxrSpatialMeshInfo` struct, which contains the updated spatial mesh data. The object that subscribes to this event can perform corresponding operations, such as updating the UI or re-rendering the scene, after receiving the updated spatial mesh data.
```C#
var subsystem = XRGeneralSettings.Instance.Manager.ActiveLoaderAs<PXR_Loader>().meshSubsystem;

// Start mesh scanning
subsystem.Start();

// Stop mesh scanning
subsystem.Stop();

Action<List<PxrSpatialMeshInfo>> SpatialMeshDataUpdated;

public struct PxrSpatialMeshInfo
{
    public Guid uuid; // the unique identifier of spatial mesh
    public MeshChangeState state; // the current state of the mesh
    public Vector3 position; // the position of the mesh
    public Quaternion rotation; // the rotation of the mesh
    public ushort[] indices; // the indice array of the mesh
    public Vector3[] vertices; // the vertice array of the mesh
    public PxrSemanticLabel[] labels; // the semantic label array of the mesh
}

public enum MeshChangeState
{
    Added, // a new mesh
    Updated, // the mesh has been updated
    Removed, // the mesh has been removed
    Unchanged, // the mesh remains unchanged
}
```

Below is the code sample:
```C#
// Handles the changes to the spatial mesh, including adding, updating, and removing meshes
void SpatialMeshDataUpdated(List<PxrSpatialMeshInfo> meshInfos)
{
    // Iterate through the list of mesh info objects
    for (int i = 0; i < meshInfos.Count; i++)
    {
        // Get the current mesh info object
        PxrSpatialMeshInfo meshInfo = meshInfos[i];

        // Handle the different states of spatial meshes
        switch (meshInfo.state)
        {
            // If the mesh was newly added
            case MeshChangeState.Added:
                {
                    // Add the mesh info to the list of meshes needing to be drawn
                    spatialMeshNeedingDraw.Add(meshInfo.uuid, meshInfo);
                }
                break;
            // If the mesh was updated
            case MeshChangeState.Updated:
                {
                    // If the mesh is not in the list of meshes needing to be drawn, add it
                    if (!spatialMeshNeedingDraw.ContainsKey(meshInfo.uuid))
                    {
                        spatialMeshNeedingDraw.Add(meshInfo.uuid, meshInfo);
                    }
                    // Otherwise, update the existing mesh info
                    else
                    {
                        spatialMeshNeedingDraw[meshInfo.uuid] = meshInfo;
                    }
                }
                break;
            // If the mesh was removed
            case MeshChangeState.Removed:
                {
                    // Remove the mesh info from the list of meshes needing to be drawn
                    spatialMeshNeedingDraw.Remove(meshInfo.uuid);

                    // Get the game object associated with the removed mesh
                    GameObject removedGo;
                    if (meshIDToGameobject.TryGetValue(meshInfo.uuid, out removedGo))
                    {
                        // If the object pool has space, deactivate the game object and add it to the pool
                        if (meshObjectsPool.Count < objectPoolMaxSize)
                        {
                            removedGo.SetActive(false);
                            meshObjectsPool.Enqueue(removedGo);
                        }
                        // Otherwise, destroy the game object
                        else
                        {
                            Destroy(removedGo);
                        }
                        // Remove the mesh ID to game object mapping
                        meshIDToGameobject.Remove(meshInfo.uuid);
                    }
                }
                break;
            // If the mesh was unchanged
            case MeshChangeState.Unchanged:
                {
                    // Remove the mesh info from the list of meshes needing to be drawn
                    spatialMeshNeedingDraw.Remove(meshInfo.uuid);
                }
                break;
            // If the mesh state is invalid
            default:
                throw new ArgumentOutOfRangeException();
        }
    }
}
```


# --- END: Spatial Mesh.md ---



# --- BEGIN: Use hand tracking.md ---

Hand tracking enables the user's hand movements as input for PICO devices. After enabling hand tracking, the PICO system will track the real-time position of 26 joints on the user's hands. When using hands as the primary input source for an app, different hand poses can trigger different events. For example, when the fingertips of the thumb and index finger are pinched together, it enables the ray pointer which functions similarly to the controller ray. Users can use the ray pointer to click, select, and drag objects. You can create different hand poses, such as poke, pinch, and grip, for your app using the hand pose generator, and configure different events for different hand poses to enhance user-app interaction.
## Requirements

* PICO device models: PICO Neo3 series, PICO 4 series, and PICO 4 Ultra series (self-adaptive hand models only support PICO 4 Ultra series)
* PICO device's system version: 5.11.0 or later

## Hand joint conventions
PICO SDK's hand tracking feature follows the hand joint conventions outlined by OpenXR and supports the 26 hand joints listed below.
![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96389e811e5041c6b690f66d37c71889~tplv-goo7wpa0wc-image.image)
| ##### **Value** | ##### **Joint Name** | ##### **Description** | ##### **Corresponding OpenXR Enum** |
| --- | --- | --- | --- |
| 0 | Palm | The central point in the palm. | XR_HAND_JOINT_PALM_EXT |
| 1 | Wrist | The joint of the wrist. | XR_HAND_JOINT_WRIST_EXT |
| 2 | Thumb_metacarpal | The metacarpal joint of the thumb. | XR_HAND_JOINT_THUMB_METACARPAL_EXT |
| 3 | Thumb_proximal | The proximal joint of the thumb. | XR_HAND_JOINT_THUMB_PROXIMAL_EXT |
| 4 | Thumb_distal | The distal joint of the thumb. | XR_HAND_JOINT_THUMB_DISTAL_EXT |
| 5 | Thumb_tip | The fingertip of the thumb. | XR_HAND_JOINT_THUMB_TIP_EXT |
| 6 | Index_metacarpal | The metacarpal joint of the index finger. | XR_HAND_JOINT_INDEX_METACARPAL_EXT |
| 7 | Index_proximal | The proximal joint of the index finger. | XR_HAND_JOINT_INDEX_PROXIMAL_EXT |
| 8 | Index_intermediate | The intermediate joint of the index finger. | XR_HAND_JOINT_INDEX_INTERMEDIATE_EXT |
| 9 | Index_distal | The distal joint of the index finger. | XR_HAND_JOINT_INDEX_DISTAL_EXT |
| 10 | Index_tip | The fingertip of the index finger. | XR_HAND_JOINT_INDEX_TIP_EXT |
| 11 | Middle_metacarpal | The metacarpal joint of the middle finger. | XR_HAND_JOINT_MIDDLE_METACARPAL_EXT |
| 12 | Middle_proximal | The proximal joint of the middle finger. | XR_HAND_JOINT_MIDDLE_PROXIMAL_EXT |
| 13 | Middle_intermediate | The intermediate joint of the middle finger. | XR_HAND_JOINT_MIDDLE_INTERMEDIATE_EXT |
| 14 | Middle_distal | The distal joint of the middle finger. | XR_HAND_JOINT_MIDDLE_DISTAL_EXT |
| 15 | Middle_tip | The fingertip of the middle finger. | XR_HAND_JOINT_MIDDLE_TIP_EXT |
| 16 | Ring_metacarpal | The metacarpal joint of the ring finger. | XR_HAND_JOINT_RING_METACARPAL_EXT |
| 17 | Ring_proximal | The proximal joint of the ring finger. | XR_HAND_JOINT_RING_PROXIMAL_EXT |
| 18 | Ring_intermediate | The intermediate joint of the ring finger. | XR_HAND_JOINT_RING_INTERMEDIATE_EXT |
| 19 | Ring_distal | The distal joint of the ring finger. | XR_HAND_JOINT_RING_DISTAL_EXT |
| 20 | Ring_tip | The fingertip of the ring finger. | XR_HAND_JOINT_RING_TIP_EXT |
| 21 | Little_metacarpal | The metacarpal joint of the little finger. | XR_HAND_JOINT_LITTLE_METACARPAL_EXT |
| 22 | Little_proximal | The proximal joint of the little finger. | XR_HAND_JOINT_LITTLE_PROXIMAL_EXT |
| 23 | Little_intermediate | The intermediate joint of the little finger. | XR_HAND_JOINT_LITTLE_INTERMEDIATE_EXT |
| 24 | Little_distal | The distal joint of the little finger. | XR_HAND_JOINT_LITTLE_DISTAL_EXT |
| 25 | Little_tip | The fingertip of the little finger. | XR_HAND_JOINT_LITTLE_TIP_EXT |
```C++
// Provided by XR_EXT_hand_tracking
typedef enum XrHandJointEXT {
    XR_HAND_JOINT_PALM_EXT = 0,
    XR_HAND_JOINT_WRIST_EXT = 1,
    XR_HAND_JOINT_THUMB_METACARPAL_EXT = 2,
    XR_HAND_JOINT_THUMB_PROXIMAL_EXT = 3,
    XR_HAND_JOINT_THUMB_DISTAL_EXT = 4,
    XR_HAND_JOINT_THUMB_TIP_EXT = 5,
    XR_HAND_JOINT_INDEX_METACARPAL_EXT = 6,
    XR_HAND_JOINT_INDEX_PROXIMAL_EXT = 7,
    XR_HAND_JOINT_INDEX_INTERMEDIATE_EXT = 8,
    XR_HAND_JOINT_INDEX_DISTAL_EXT = 9,
    XR_HAND_JOINT_INDEX_TIP_EXT = 10,
    XR_HAND_JOINT_MIDDLE_METACARPAL_EXT = 11,
    XR_HAND_JOINT_MIDDLE_PROXIMAL_EXT = 12,
    XR_HAND_JOINT_MIDDLE_INTERMEDIATE_EXT = 13,
    XR_HAND_JOINT_MIDDLE_DISTAL_EXT = 14,
    XR_HAND_JOINT_MIDDLE_TIP_EXT = 15,
    XR_HAND_JOINT_RING_METACARPAL_EXT = 16,
    XR_HAND_JOINT_RING_PROXIMAL_EXT = 17,
    XR_HAND_JOINT_RING_INTERMEDIATE_EXT = 18,
    XR_HAND_JOINT_RING_DISTAL_EXT = 19,
    XR_HAND_JOINT_RING_TIP_EXT = 20,
    XR_HAND_JOINT_LITTLE_METACARPAL_EXT = 21,
    XR_HAND_JOINT_LITTLE_PROXIMAL_EXT = 22,
    XR_HAND_JOINT_LITTLE_INTERMEDIATE_EXT = 23,
    XR_HAND_JOINT_LITTLE_DISTAL_EXT = 24,
    XR_HAND_JOINT_LITTLE_TIP_EXT = 25,
    XR_HAND_JOINT_MAX_ENUM_EXT = 0x7FFFFFFF
} XrHandJointEXT;
```

## PICO hand model prefabs
The SDK provides two standard hand model prefabs: HandLeft and HandRight. Each model consists of 1209 vertices, 1198 quadrilateral faces, and 2414 triangular faces.
You can get the prefabs in Packages > PICO Integration > Assets > Resources > Prefabs. The prefabs have bound hand joints according to the OpenXR conventions, and have bound the ray pose (Ray Pose) and ray model (Default Ray) as well.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21d1c8a644674db1bd69c15824c02ecc~tplv-goo7wpa0wc-image.image" width="600px" />

## Enable hand tracking
If you only want to make your app recognize users' hand poses, enable the hand tracking capability for your app.
### Step 1: Complete basic setups

1. [Import the required version of SDK](/en_import-the-sdk)
2. [Complete project settings](/en_complete-project-settings)
3. [Upgrade the XR Interaction Toolkit](/en_create-an-xr-scene#782faf9d)

### Step 2: Set up hand models (using PICO hand model prefabs)
The SDK provides [standard hand model prefabs](#0409d0e8). You can directly use them with default settings in your app or customize their settings by binding desired hand joints, ray pose, and ray model according to actual needs. 

1. Under the **XR Origin** directory, delete **LeftHand Controller** and **RightHand Controller**.
   If you do not delete these two controller models, they will coexist with the hand prefabs when running the scene on your headset.

2. In the **Project** window, go to **Packages** > **PICO Integration** > **Assets** > **Resources** > **Prefabs**.
   You will see the HandLeft and HandRight prefabs.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56af9bae27e540d8b8a559086fcab246~tplv-goo7wpa0wc-image.image)
3. In the **Hierarchy** window, drag **HandLeft** and move it to the **XR Origin** directory. The prefab should be placed at the same level as **Main Camera** under the directory.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/071ad655fa5e431ab3605168f237ae9d~tplv-goo7wpa0wc-image.image)
4. Select **HandLeft**.
   The components and scripts for configuring the HandLeft prefab are then displayed in the Inspector window, including the PXR_Hand script whose UI appears as below:
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80ebd4393712479cb58c998b6a269825~tplv-goo7wpa0wc-image.image)
5. (Optional) Click the **Circle** icon in each hand joint parameter and bind a desired joint.
   By default, hand prefabs have been bound with joints based on the bone structure of real physical hands. If you need to customize the settings, make sure to follow the bone structure of real hands.

6. (Option) Modify the **Ray Pose** and **Default Ray** parameters. The **RayPose (Transform)**, which is the SDK's default ray pose template, and the default ray model **DefaultRay** have been bound by default.
7. Set up **HandRight** through the same steps as above.

### Step 3: Enable hand tracking for your app

1. Open an existing scene or create a new scene in the Unity Editor.
2. In the **Hierarchy** window, click **+** > **XR** > **XR Origin (VR)**.
   XR Origin is added to the scene.
3. Select **XR Origin** and add the **PXR_Manager** script to it in the **Inspector** window.
4. Check the **Hand Tracking** checkbox.
   The **Hand Tracking Support** parameter appears.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/062bf07a43924b4b826ab9371cd62a55~tplv-goo7wpa0wc-image.image)
5. In the **Hand Tracking Support** parameter, select the interaction mode. Below are available options:
   * **Controller And Hands**: Automatically switch between controllers and hand poses for user-app interaction. When the user puts down the controllers and the device recognizes hand poses, it uses hand poses for interaction; when the user picks up the controllers, it switches back to controllers for interaction.
   * **Hands Only**: Only use hand poses for user-app interaction.

### Step 4: Enable hand tracking for your PICO device




1. Turn on your PICO device.
2. Go to **Settings** > **LAB** > **Hand Tracking**.
3. Toggle the **Hand Tracking** switch.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1394d204385245a0859130ed4fbb7662~tplv-goo7wpa0wc-image.image)




1. Turn on your PICO device.
2. Go to **Control Center** > **Settings** > **Interaction**.
3. Set **Interaction Controls** to **Auto Switch between Hands & Controllers**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45bdb141d45247e59d914af297057e4d~tplv-goo7wpa0wc-image.image)



## Self-adaptive hand models
PICO's official hand models are self-adaptive. Their size can dynamically change to match the size of the user's real hands.
To enable this feature, check the **Adaptive Hand Model (PICO)** checkbox on the **PXR_Manager (Script)** component. After enabling this feature, the SDK automatically writes the following metadata into the app's AndroidManifest.xml file.
```XML
<meta-data android:name="Enable_AdaptiveHandModel" android:value="1" />
```

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/960d2a8a678c473ba2d96dab4aa141bd~tplv-goo7wpa0wc-image.image" width="500px" />

If you are using custom hand models, you need to call `GetHandScale` to retrieve the size of the user's hands, then dynamically adjust the size of hand models in the scene. Below is the code sample for using `GetHandScale`:
```C#
 float scale = 0; // the scaling ratio for custom hand models
 PXR_HandTracking.GetHandScale(handType,ref scale);
```

## High-frequency tracking (60Hz)
The device supports tracking users' hands at 60Hz to capture much faster hand movements. This improves the accuracy of hand tracking data and brings users a more natural and smooth interaction experience.
Typically, the default hand tracking mode already achieves a good balance between tracking accuracy and speed. The high-frequency tracking mode will incur higher performance overhead while further improves tracking accuracy. If your app type (e.g., fitness, music/dance) requires tracking faster hand movements, you can enable the high-frequency tracking mode. Before enabling it, it's recommended to first test whether the default hand tracking mode can meet your expected tracking performance.
On the **PXR_Manager (Script)** panel, check the **High Frequency Tracking (60Hz)** checkbox to enable high-frequency hand tracking. 
High-frequency tracking mode cannot be disabled during runtime once enabled.

<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c289b3ee732479381d6e5cfe95d7c95~tplv-goo7wpa0wc-image.image" width="500px" />

Once enabled, SDK automatically writes the following metadata to the app's AndoridManifest.xml file:
```XML
<meta-data android:name="Hand_Tracking_HighFrequency" android:value="1" />
```

## About the InputDeviceChanged event
When the input source has changed, you will receive the `PXR_Plugin.System.InputDeviceChanged` event. The event returns one of the following values indicating the current input source: `0` (HMD), `1` (Controllers), `2` (Hands). For example, when the input source has changed from controllers to hands, the event returns `2`, indicating that the current input source is hands.
## About Unity's XR Hands package
The PICO Unity Integration SDK supports Unity's official XR Hands package. This package defines a set of API that allows you to access hand tracking data from devices that support hand tracking.
For how to customize hand poses using Unity's XR Hand package, refer to [Unity's official documentation](https://docs.unity3d.com/Packages/com.unity.xr.hands@1.4/manual/gestures/custom-gestures.html).
## API reference
For details about Hand Tracking APIs, refer to the [API reference](/reference/unity/client-api/PXR_HandTracking/).


# --- END: Use hand tracking.md ---



# --- BEGIN: Video Seethrough.md ---

The Video Seethrough feature enables the vision to cross the boundary between the physical and virtual environments. It uses HMD cameras and image processing algorithms to capture and approximate what users would see if they could directly look through the display of the HMD. This finally enables the blend of the real-world scene and the virtual scene to create a mixed-reality scene.
The PICO system directly processes the video seethrough images, so the app is unable to access any images or videos of users' surroundings.
<img src="https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/8b0fabfb331c4ca0a54bfaeb9d4b61ff~tplv-em5hxbkur4-noop.image?width=868&height=572" width="446px" />

## Expected effect
Video seethough enables the physical environment to become a scene's background image upon which the virtual objects are overlayed. This is also known as "seethrough AR". 

      <video src=https://sf1-cdn-tos.huoshanstatic.com/obj/vcloud/8480f6b065c76c96c81ee67729890e24-.mp4></video>

## Key concepts
| **Name** | **Description** |
| --- | --- |
| Render Target | Render target is a surface where the graphics APIs draw contents. |
| Overlay | One type of compositor layer, which is displayed in front of the app's layer. |
| App layer | The app layer is drawn by the Unity engine. The layer's resolution is usually lower than the screen's resolution. |
| Underlay | One type of compositor layer, which is displayed behind the app's layer. |
| Compositor | An SDK-level capability. The compositor combines images generated by different apps/services into one layer and then renders them to the left and right-eye cameras for display. |
## Tech details
For the composition of mixed reality scenes, the app does not directly render the image onto the HMD's screen. Instead, it first renders the image into a render target. Afterwards, the compositor service combines other layers and outputs the final image onto the screen. The layer rendering order is as follows: VST layer, underlay layer, app layer, and overlay layer, in a front-to-back sequence.
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d026a86a7824c3c9ed4485fab094b7d~tplv-goo7wpa0wc-image.image" width="500px" />

| **Layer Name** | **Description** |
| --- | --- |
| Seethrough layer | The VST layer is located at the bottom of the composited image and is the first layer to be rendered. The VST layer's data is generated by the runtime and cannot be accessed by the app. |
| Underlay layer | The underlay layer is generated by the app and is positioned as the penultimate layer in the composited image. |
| App layer <br>  | The app layer is drawn by the Unity engine, and its resolution is usually lower than that of the screen. This results in a decrease in image clarity, especially for UI elements. You can improve the resolution and address the issue of low UI element clarity by increasing the value of `eyebufferScale`. However, this will also come with a higher performance cost. For UI elements with fixed sizes, you can use underlay or overlay layers to resolve the clarity issue. <br> To make sure that the content of the underlay layer can be displayed on the screen through the app layer, you need to create a "hole" at the corresponding position of the underlay layer on the app layer. This means that an appropriate transparency should be set for the Alpha channel of the app layer at the corresponding position based on the content of the underlay layer.  |
| Overlay layer | The overlay layer is the last layer to be rendered and is positioned as the topmost layer among all the layers. As a result, the overlay layer obscures all other layers. The overlay layer is typically in the shape of a circle or is a render texture generated by the Unity engine. The app directly sends the overlay layer to the compositor service for compositing. During the compositing process, the compositor service does not perform any scaling or stretching on the overlay layer, ensuring the clarity of the image is maintained. |
## Requirements

* PICO device models: PICO 4 Ultra series (to use this functionality on PICO 4 series devices, you need to use SDK [3.1.0](https://github.com/Pico-Developer/PICO-Unity-Integration-SDK/tree/3.1.0) or earlier versions)
* PICO device's system version: 5.14.0 or later

## Important notes

* When using video seethrough, all post-processing capabilities in the scene must be disabled, otherwise video seethrough will not work. 
* If you are using Vulkan and the render pipeline (Universal Render Pipeline or Built-in Render Pipeline) in your project, you need to disable HDR, otherwise video seethrough will not work. 
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43e97d637b0b40fa81c793cc3a2cee6e~tplv-goo7wpa0wc-image.image)

## Set up video seethrough for your app

1. Add **XR Origin** to the scene and mount the **PXR_Manager** script to it. Refer to the [Quickstart](/13136/en_create-an-xr-scene) guide for detailed instructions. You can skip this step if you have already done so.
2. On the **PXR_Manager (script)** pane, check the **Video Seethrough** checkbox.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cfa690e4ff942a78ec2a4379e2cd754~tplv-goo7wpa0wc-image.image)
3. Select the main camera (usually named **Main Camera**) in the scene.
4. On the **Camera** pane, complete the following settings for the main camera:
   1. Set **Clear Flags** to **Solid Color**.
      This setting enables the camera to clear the color value of each pixel before rendering each frame and then implements the color value (the background color you will set next) that needs to be rendered.
      ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/d2b26af7836742eba19da5f90200ddbd~tplv-em5hxbkur4-noop.image?width=794&height=131)
   2. In **Background**, click the color bar to open the **Color** window, then set the values of **R**, **G**, **B**, and **A** to **0** or simply set **Hexadecimal** to **000000**.
      The scene's background color is set to black, and the alpha channel is set to be completely transparent.
      ![Image](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e5594ceef1ef4fab9e6b2ef0ad410141~tplv-em5hxbkur4-noop.image?width=466&height=1005)
5. Open the PXR_Manager.cs script or any script created by you in a code editor, use the `Unity.XR.PXR` namespace, and use the `PXR_Manager.EnableVideoSeeThrough` variable to enable video seethrough. Once video seethrough is enabled, it works throughout the lifecycle of the app.
   The `PXR_Manager.EnableVideoSeeThrough` variable takes some time to make video seethrough work or stop working. In this case, if you need to get the current precise status of the Video Seethrough feature, you can listen for the `VstDisplayStatusChanged` event.

   Below is the code sample:
   ```C#
   // Enable video seethrough
   PXR_Manager.EnableVideoSeeThrough = true;
   
   // Disable video seethrough
   PXR_Manager.EnableVideoSeeThrough = false;
   
   // Listen for the status of the Video Seethrough feature
   PXR_Manager.VstDisplayStatusChanged += VstDisplayStatusChanged;
   private void VstDisplayStatusChanged(PxrVstStatus status)
   {
       switch (status)
       {
           case PxrVstStatus.Disabled: 
               break;
           case PxrVstStatus.Enabling:.
               break;
           case PxrVstStatus.Enabled: 
               break;
           case PxrVstStatus.Disabling: 
               break;
       }
   }
   ```

## Set up video seethrough effects
You can enrich your app's visual experience by setting up video seethrough effects.
### Method 1: set video seethtough effect parameters
Before the compositor service begins to work, you can perform post-processing on the seethrough layer, such as adjusting the color and adding special effects, to create different visual effects. Currently, you can modify four parameters for the seethrough layer, which are contrast, saturation, brightness, and color temperature.

1. Refer to the "Set up video seethrough for your app" section to enable video seethrough for your app.
2. Use the following APIs to set video seethrough effect parameters.
   | **API** | **Description** |
   | --- | --- |
   | EnableVideoSeeThroughEffect | Enable or disable video seethrough effect. |
   | SetVideoSeeThroughEffect | Set video seethrough effect-related parameters, including the contract, saturation, brightness, and color temperature. |

Below is the code sample:
```C#
// Firsly, enable video seethrough
PXR_Manager.EnableVideoSeeThrough = true

// Listen for the status of the Video Seethrough feature
PXR_Manager.VstDisplayStatusChanged += VstDisplayStatusChanged;
private void VstDisplayStatusChanged(PxrVstStatus status)
{
    switch (status)
    {
        case PxrVstStatus.Disabled:
            break;
        case PxrVstStatus.Enabling:
            break;
        case PxrVstStatus.Enabled:
            break;
        case PxrVstStatus.Disabling:
            break;
    }
}

// Then, enable video seethrough effect
PXR_MixedReality.EnableVideoSeeThroughEffect(true);

// Finally, set video seethrough effect parameters, including contrast, saturation, brightness, and color temperature (you need to set desired values for the 'value' and 'duration' parameters)
PXR_MixedReality.SetVideoSeeThroughEffect(PxrLayerEffect.Colortemp, 10, 0);
PXR_MixedReality.SetVideoSeeThroughEffect(PxrLayerEffect.Brightness, 40, 10);
PXR_MixedReality.SetVideoSeeThroughEffect(PxrLayerEffect.Saturation, -5, 0);
PXR_MixedReality.SetVideoSeeThroughEffect(PxrLayerEffect.Contrast, 1, 5);
```

### Method 2: set up the LUT texture
LUT, or Look-Up Table, is a technique used for remapping colors. It is primarily utilized for adjusting image styles and adding filters in post-processing effects. You can use LUTs to set video seethrough effects.
To correctly obtain the corresponding RGBA values, the imported LUT texture must be converted to the RGBA32 format. Therefore, you need to convert the LUT texture format first, and then call APIs to set the LUT. The steps are as follows:

1. Import the LUT texture into your Unity project.
   The size of the LUT texture should not exceed 512*512.

   The following neutral LUT texture is compatible with the PICO Unity Integration SDK.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32289908077b4f32845a8907a62e9092~tplv-goo7wpa0wc-image.image)
2. In the **Project** window, double-click the LUT texture.
3. In the **Inspector** window, complete the following:
   1. Expand the **Advanced** settings list and check the **Read/Write** checkbox.
   2. Go to the **Android settings** section, check the **Override For Android** checkbox, and set the **Format** parameter to **RGBA 32 bit**.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e547c5a4c6034e7abdb2aeb2952b8eb0~tplv-goo7wpa0wc-image.image)
4. In the lower-right corner, click the **Apply** button.
5. Refer to the "Set up video seethrough for your app" section to enable video seethrough for your app.
6. Call `SetVideoSeeThroughLut` to set the LUT. Below is the code sample:
   ```C#
   // Firsly, enable video seethrough
   PXR_Manager.EnableVideoSeeThrough = true
   
   // Listen for the status of the Video Seethrough feature
   PXR_Manager.VstDisplayStatusChanged += VstDisplayStatusChanged;
   private void VstDisplayStatusChanged(PxrVstStatus status)
   {
       switch (status)
       {
           case PxrVstStatus.Disabled:
               break;
           case PxrVstStatus.Enabling:
               break;
           case PxrVstStatus.Enabled:
               break;
           case PxrVstStatus.Disabling:
               break;
       }
   }
   
   // Then, enable video seethrough effect
   PXR_MixedReality.EnableVideoSeeThroughEffect(true);
    
   // Finally, set the LUT (you need to pass the actual number of rows and columns in the LUT texture)
   PXR_MixedReality.SetVideoSeeThroughLut(lutTex1, 8, 8);
   ```

## API reference
For more details on video seethrough APIs, refer to the [API reference](/reference/unity/client-api/PXR_MixedReality/).


# --- END: Video Seethrough.md ---

