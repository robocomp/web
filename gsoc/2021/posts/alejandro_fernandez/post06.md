# Creating the component and adding an extra test

_26 July, 2021_

## Introduction

The goal of the previous week was to create the component, that has been done easily using the (robocomp)[https://github.com/robocomp/robocomp] command robocompdsl and having a good reference in emotionrecognition2 component previously create made things easier.

## Creating the component

Firstly, I need to locate the interface that I have previously created in my robocomp installiation in the directory interfaces/IDSLs, also I have done some changes in the interfaces to modify and get the threshold (if the confidence of the prediction is lower than the threshold it will not be included in the predictions) and change the string class in Sprediction to label as class is a keyword in Python. So the final code of the interface will be like that:

  module DetectionComponent
  {
      struct SPrediction
      {
          int x;
          int y;
          int w;
          int h;
          string label;
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

      interface DetectionComponent
      {
          Predictions processImage(TImage frame);
          void setThreshold(float threshold);
          float getThreshold();
       };
  };

## Results

### SSD MobileNet

The results of this model are pretty decent respect to the requirements needed

![](images/test_detect_ssd.jpg)

### Efficient Det

As in the last model the results are good

![](images/test_detect_efficient.jpg)

### CenterNet 

In this case, the results do not reach the expectatives. For a minimum score of 0.3 all predictions are below this score so I reduce the minimum to 0.12 and the results do not make sense.

![](images/test_detect_centernet.jpg)

I tried converting the model another time to check if the fault was about a bad conversion from the original model, but the results did not improve.

### Conclusion

After these evaluations we can conclude that SSD MobileNet and Efficient Det are the best options, meanwhile CenterNet does not work properly converted to tflite in this case. I think that the predictions of Efficient Det are a tiny better compared with SSD Mobile, so Efficient Det will be the model used in the component.

__Alejandro Fernández Camello__

