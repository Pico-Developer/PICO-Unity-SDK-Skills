# SecureMR Guide

This guide is self-contained. Use it when the user asks about SecureMR, SecureMR privacy, tensors, operators, pipelines, QNN model integration, VST inference, readback tensors, dynamic textures, pipeline synchronization, or SecureMR troubleshooting.

## What SecureMR is

SecureMR lets an app delegate mixed-reality algorithms to an isolated service. The app works with handles to secure resources instead of directly reading all sensitive environment data. SecureMR is mainly for PICO XR mode on supported devices such as PICO 4 Ultra-class hardware.

Use SecureMR when the user needs privacy-preserving MR algorithms, camera-derived inference, object detection/segmentation pipelines, or model-assisted scene understanding. Do not recommend it for simple Passthrough display or normal UI overlays.

## Core concepts

| Concept | Meaning | Practical implication |
| --- | --- | --- |
| Tensor | A chunk of data stored inside the SecureMR service. The app receives a handle. | Define shape, channel, data type, and usage carefully. Shape mismatches are a common failure source. |
| Operator | A node that consumes operand tensors and writes result tensors. | Operators implement model inference, pre/post-processing, rendering, tracking, and other algorithm steps. |
| Pipeline | A computation graph made of tensors and operators. | Pipelines run when submitted. Avoid uncontrolled per-frame queue buildup. |
| Global tensor | Tensor shared across pipelines. | Required for some cross-pipeline data and conditions; use placeholder mapping for thread safety. |
| Run handle | Reference returned by a scheduled pipeline execution. | Can be used as a wait-for dependency for future submissions. |

## Device and setup checklist

1. Confirm device and OS support. Use a PICO 4 Ultra-class target when SecureMR is required.
2. Use PICO XR mode; do not assume Unity OpenXR or PICO Spatial support.
3. Configure Video Seethrough / VST if the algorithm uses camera-derived input.
4. Enable SecureMR in `PXR_Manager` where applicable.
5. Prepare model packages and resources before creating operators that depend on them.
6. Add privacy/review language explaining what data is processed and why.
7. Test on physical device; SecureMR behavior cannot be validated fully in the editor.

## Typical pipeline architecture

Example: VST image -> model inference -> render result.

1. Create a pipeline.
2. Create a `RectifiedVstAccessOperator` to output a rectified VST image tensor.
3. Create a `RunModelInferenceOperator` configured with a model binary, often converted/profiled with QNN tooling.
4. Bind the VST tensor as an operand to the inference operator.
5. Create result tensors for labels, confidence, masks, boxes, points, or other model outputs.
6. Add post-processing operators if needed: matrix algebra, sorting, NMS, assignment, slicing, or CPU operators provided by PICO.
7. Add MR rendering operators if needed: render text, render glTF, update materials/textures, track objects, or visualize outputs.
8. Submit the pipeline at a controlled rate and use wait-for dependencies when required.

Pseudo-code structure:

```csharp
// Names are illustrative. Match exact class names and generic parameters to the SDK version in use.
var pipeline = secureMRProvider.CreatePipeline();

var vstTensor = pipeline.CreateTensor<byte, Color>(shape, initialData);
var labelTensor = pipeline.CreateTensor<int, Scalar>(labelShape, initialLabelData);
var confidenceTensor = pipeline.CreateTensor<float, Scalar>(confidenceShape, initialConfidenceData);

var vstOperator = pipeline.CreateOperator<RectifiedVstAccessOperator>();
vstOperator.SetResult("vst", vstTensor);

var inference = pipeline.CreateOperator<RunModelInferenceOperator>();
inference.SetOperand("input", vstTensor);
inference.SetResult("label", labelTensor);
inference.SetResult("confidence", confidenceTensor);

var render = pipeline.CreateOperator<RenderTextOperator>();
render.SetOperand("label", labelTensor);
render.SetOperand("confidence", confidenceTensor);

var runHandle = pipeline.Submit(waitFor: previousRunHandle, condition: null);
previousRunHandle = runHandle;
```

## Tensor design rules

SecureMR tensors are defined by:

- Shape: dimensions such as `[height, width]` or model-specific dimensions.
- Channel: number of channels, not always a normal shape dimension.
- Data type: `UInt8`, `Int8`, `UInt16`, `Int16`, `Int32`, `Float32`, `Float64`, etc.
- Usage: `Matrix`, `Scalar`, `Timestamp`, `Color`, `Point`, `Slice`, or `Gltf` where applicable.

Important rules:

- A 1-channel tensor with shape `[1024, 1024, 3]` is different from a 3-channel tensor with shape `[1024, 1024]`.
- Timestamp usage has strict channel/type/shape constraints.
- Color tensors require RGB/RGBA-style channel counts and integral types.
- Point tensors require 2 or 3 channels.
- glTF tensors are handles to renderable assets and may have special lifecycle constraints.
- Apps usually cannot read secure tensor contents directly. Use supported readback mechanisms only when the SDK and privacy model allow it.

## Operators

Operators are created in a pipeline and connected with operands/results:

```csharp
var op = currentPipeline.CreateOperator<ArithmeticComposeOperator>();
op.SetOperand("operand0", operand0);
op.SetOperand("operand1", operand1);
op.SetResult("result", resultTensor);
```

Operator families include:

- VST access and rectification operators.
- QNN / model inference operators.
- CPU operators for pre/post-processing.
- MR rendering operators for text, glTF, textures, materials, and visual overlays.

## Pipeline execution and synchronization

- Operators in a pipeline execute in the order they are added.
- Pipeline submission schedules one execution and returns a run handle.
- Use `wait-for` when one execution must happen after another.
- Use `condition` with a global tensor to discard execution when the condition is zero.
- Multiple executions of the same pipeline do not run concurrently.
- Global tensor reads/writes are synchronized to avoid conflicting access.
- The SDK may queue submissions; if a previous execution has not finished, uncontrolled per-frame submission can increase latency. Control execution frequency based on measured model/pipeline time.

## QNN model workflow

When using ML inference:

1. Train or export the model from PyTorch, TensorFlow, ONNX, or another supported source.
2. Convert and profile it using Qualcomm Neural Network tooling required by the SDK path.
3. Package model binaries/resources with the Unity app.
4. Verify input tensor shape/channel/type exactly match the model input.
5. Verify output tensors match model output shape/type.
6. Use device-side logs to distinguish model load failure from tensor/operator binding failure.

## Common errors

| Error / symptom | Likely cause | Fix |
| --- | --- | --- |
| `INVALID PARAMETER` | Tensor shape/channel/type does not match operator/model expectation, or output size mismatch. | Print every tensor's shape/channel/type/usage and compare to operator/model specification. |
| `HANDLE NOT INITIALIZED` | Tensor/operator/pipeline handle was not created, was destroyed, or wrong ID was used. | Verify creation order, registered tensors, pipeline IDs, and lifecycle cleanup. |
| Inference output is all zeros | Model input not fed, condition tensor zero, incorrect tensor mapping, or model preprocessing mismatch. | Validate VST/input tensor, placeholder mapping, model normalization, and run condition. |
| Pipeline latency grows | Submitting every frame while previous runs are queued. | Submit at controlled frequency or use wait-for and measured execution time. |
| Rendered output missing | MR render operator not connected, glTF tensor lifecycle wrong, or VST/SecureMR not enabled. | Validate render tensors/operators and PXR Manager feature toggles. |
| Cannot inspect tensor data | SecureMR intentionally hides tensor content. | Use supported Readback tensor or debug operators only when allowed. |

## SecureMR answer pattern

For user questions, include:

1. Device/mode support check.
2. VST/SecureMR setup and privacy boundary.
3. Tensor/operator/pipeline design.
4. Model conversion/package notes if ML is involved.
5. Execution/synchronization strategy.
6. Debugging plan with tensor shape, operator bindings, pipeline IDs, and adb/PXR logs.
