# Coverting the models to Tensorflow Lite

_5 July, 2021_

## Introduction

The goal is to convert the following models to the tflite format that is more suitable for low computational environments:

- **SSD MobileNet v2 320x320**
- **CenterNet MobileNetV2 FPN 512x512**
- **EfficientDet D0 512x512**

As is said in the previous post the only two models that can be converted are **SSD MobileNet**(using standard Tensorflow Lite) and **EfficientDet**(using Tensorflow Lite Model Maker), but in the zip file of CenterNet MobileNet appeared a tflite file of the model.

## SSD MobileNet

I followed this [tutorial](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/running_on_mobile_tf2.md).

Firstly, I needed to convert the model to an inference graph of tflite that can be done with this command in the directory research/object_detection in the repository:

    python object_detection/export_tflite_graph_tf2.py --pipeline_config_path=object_detection/ssd_mobilenet/pipeline.config 
    --trained_checkpoint_dir=object_detection/ssd_mobilenet/checkpoint --output_directory=object_detection/models_tflite/ssd_mobilenet

After that, we can pass to the last part to create the tflite model with all necessary metadata. For that, I wrote a tiny script of Python with the information provided by the tutorial, this script is located in the following directory research/object_detection/models_tflite/ssd_mobilenet.

    import tensorflow as tf
    from tflite_support.metadata_writers import object_detector
    from tflite_support.metadata_writers import writer_utils

    if __name__ == "__main__":
        _TFLITE_MODEL_PATH = "model_ssd.tflite"
        _TFLITE_LABEL_PATH = "../../data/mscoco_label_map.pbtxt"
        _SAVED_MODEL_PATH = "saved_model"

        converter = tf.lite.TFLiteConverter.from_saved_model(_SAVED_MODEL_PATH)
        converter.optimizations = [tf.lite.Optimize.DEFAULT]
        tflite_model = converter.convert()

        with open(_TFLITE_MODEL_PATH, 'wb') as f:
            f.write(tflite_model)

        writer = object_detector.MetadataWriter.create_for_inference(
            writer_utils.load_file(_TFLITE_MODEL_PATH), input_norm_mean=[0],
            input_norm_std=[255], label_file_paths=[_TFLITE_LABEL_PATH])
        writer_utils.save_file(writer.populate(), _TFLITE_MODEL_PATH)
 
The difference respect to the tutorial are that as that I use dynamic quantization I only need to pass to the optimizations the default optimization.
 
# EfficientDet

Firstly, I though about creating a script and following this [tutorial](https://www.tensorflow.org/lite/tutorials/model_maker_object_detection), but I wasn´t capable of configure Google Cloud so I finally decided using the [Google Colab notebook](https://colab.research.google.com/github/tensorflow/tensorflow/blob/master/tensorflow/lite/g3doc/tutorials/model_maker_object_detection.ipynb) provided by the same tutorial. I only needed to do a small change in the line with object_detector.create adding to the parameters **do_train=False** for skipping the train as the model is pretrained with the dataset that we are using and if I train the model will modified for adapting to the training dataset.

__Alejandro Fernández Camello__

