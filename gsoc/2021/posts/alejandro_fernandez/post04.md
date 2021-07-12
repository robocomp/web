# Setting the environment for LearnBlock and first steps to build the component

_9 July, 2021_

## Introduction

After selecting the possible models for the component we need to start building the component, but is necessary setting an environment with RoboComp and LearnBlock and familiarizing myself with it.

## Environment setting

Firstly, I installed [RoboComp](https://github.com/robocomp/robocomp) following the instructions of the repository. The process was longer than I expected, but was more or less easy.
After that, I started to install [LearnBlock](https://github.com/robocomp/LearnBlock) in the same way as RoboComp and in this case it wasn´t so easy. I have some problems relate to the version of PySide, I solved these problems changing the requirements.txt, concretely putting PySide2 instead of PySide.


But the greatest problem was about dlib library that it wasn´t capable of installing, so finally my tutors suggested to not install this library as is only use in one component.

## Creating the structure of the project

For creating the structure of the project, I followed the component **emotionrecognition2** as has points in common with this new component.

```bash
.
├── etc/
├── src/
├── steps-for-integrate.md
└── models/
    ├── model_centernet.tflite
    ├── model_efficientdet.tflite
    └── model_ssd.tflite 
```

The directory etc will contain the config files of Ice, src all the code of the project including the csdl and idsl files and models the converted models of Tensorflow Lite of the previous post. Meanwhile, the file steps-for-integrate-md will specify the step to integrate the model in LearnBlock.

## Doing the .csdl and .idsl files.

Each component has two files csdl and idsl files to work properly in LearnBlock, they contain the information relate to the input and output of the component, the interface, etc.

### DetectComponent.idsl

    module detectionComponent
    {
        struct SPrediction
        {
            int x;
            int y;
            int w;
            int h;
            string class;
        };

        sequence<SPrediction> Predictions;

        sequence<byte> ImgType;

        struct TImage
        {
            int width;
            int height;
            int depth;
            ImgType image;
        };

        interface detectionComponent
        {
            Predictions processImage(TImage frame);
        };
    };
 
### DetectComponent.cdsl
 
    import "detectionComponent.idsl";

    Component DetectionComponent{
        Communications
        {
            implements detectionComponent;
        };
        language Python;
    };

__Alejandro Fernández Camello__
