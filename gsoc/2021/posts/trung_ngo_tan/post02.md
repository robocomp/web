# GSoC'21 RoboComp project: Sign language recognition

25th June 2021

## Introduction
The inference directly from Python for Pytorch models usually performs poorly. This is a common issue when inference deep learning model by Pytorch. Besides, the slow also comes from the characteristic of Python language is an interpreted programming language. 

Transferring all Python code to C++ is a feasible approach. However, developers have to deal with the complexity of the C++ program and may increase
time consumption. In this project, to deal with both mentioned issues, I apply some techniques:
* Almost process is on Python, except post-processing code in c++ (heavy computation).
* Inference via TensorRT and ONNX.

## Post-processing code C++:
To match joints of multiple skeletons, the predicted joints have to be post-processed [1]. 
However, this step is quite complex and may slow down the whole process. We can implement this part in C++ and call these functions in Python.
As implemented in https://github.com/Daniil-Osokin/lightweight-human-pose-estimation-3d-demo.pytorch, we reuse their post-processing code in our project. 

In this code, they use PythonObject to wrap the C++ function. Please check the tutorial for other approaches: https://github.com/Daniil-Osokin/lightweight-human-pose-estimation-3d-demo.pytorch

## Inference via TensorRT and ONNX: 

ONNX: "..ONNX provides an open-source format for AI models, both deep learning and traditional ML. It defines an extensible computation graph model, as well as definitions of built-in operators and standard data types. ...
 ..ONNX is widely supported and can be found in many frameworks, tools, and hardware. Enabling interoperability between different frameworks and streamlining the path from research to production helps increase the speed of innovation in the AI community..."
 [Github link](https://github.com/onnx/onnx)

TensorRT: "... includes a deep learning inference optimizer and runtime that delivers low latency and high throughput for deep learning inference applications...". This framework is optimized for inference deep learning model on Nividia GPU. 
 [Main page](https://developer.nvidia.com/tensorrt)

In this project, I apply both ONNX and TensorRT for comparison. The Pose detection model firstly transforms to the ONNX model. Then this ONNX model is built to TensorRT model. 
In the below table, they are performances (in FPS) of my model.

| Model                                                 | PYTORCH     |     ONNX    |    TensorRT |
| ----------------------------------------------------- | ----------  | ----------  | ----------  |
| + Optical flow algorithm -  Hand joints detection     | ~ 50        |    x        |     x       |
| - Optical flow algorithm -  Hand joints detection     | ~ 26        |    x        |     x       |
| + Optical flow algorithm + Hand joints detection      | ~ 22        | ~ 29        | ~ 34        |
| - Optical flow algorithm +  Hand joints detection     | ~ 14        | ~ 22        | ~ 30        |

We can see that with the support of ONNX and TensorRT, model's inference speed is double. Because this is the FPS for the whole detection process (deep learning model inference + post-process code), the x2 speed up can not demonstrate full power of ONNX and TensorRT. 


Reference:

1. Zhe Cao and Gines Hidalgo and Tomas Simon and Shih-En Wei and Yaser Sheikh "OpenPose: Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields", 2019, https://arxiv.org/abs/1812.08008

 