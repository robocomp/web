# Final testing and improvements

_5 August, 2021_

## Introduction

The goal of this week was to ensure that the component works properly, for that I created a program that connect to this distributed component and execute some operations using it. 
These things appear more or less easy, but I had a lot of problems connecting the program to the proxy of the component.

## Testing the component

Using [Ice](https://github.com/zeroc-ice/ice) a distributed framework based in RPC we can provide the components an easily interaction with other components for that reason is used in RoboComp and LearnBlock.
So I write the following program using Ice to interact with the component:

    import Ice
    import sys
    import time
    import numpy as np
    import subprocess

    import cv2

    Ice.loadSlice("-I ./src/ --all ./DetectionComponent.ice")

    from RoboCompDetectionComponent import *

    def connectComponent(ic, stringProxy, _class, tries=4):

        i = 0
        while True:
            try:
                i += 1
                print(f"Try {i}")
                basePrx = ic.stringToProxy(stringProxy)
                proxy = _class.checkedCast(basePrx)
                print("Connection Successful:", stringProxy)
                break
            except Ice.Exception as e:
                if i is tries:
                    print("Cannot connect to the proxy:", stringProxy)
                    return None
                else:
                    time.sleep(1.5)
        return proxy


    if __name__ == "__main__":
        # Initialize the communicator of Ice
        ic = Ice.initialize(sys.argv)

        # Connecting to the component in the port 10010 of localhost
        component_proxy = connectComponent(ic, "detectioncomponent:tcp -h localhost -p 10010", DetectionComponentPrx,10)

        # Test the setter and getter of the threshold of the component
        print(component_proxy.getThreshold())
        component_proxy.setThreshold(0.1)
        print(component_proxy.getThreshold())
        component_proxy.setThreshold(0.3)

        # Test the processing of the image by the component

        # Prepare the image for the component
        img = cv2.imread("../test/test.jpg")
        img = cv2.cvtColor(img, cv2.COLOR_RGB2BGR)
        img = cv2.resize(img,(448,448))

        # Create the input of the component according to the interface
        frame = TImage()
        frame.width = img.shape[0]
        frame.height = img.shape[1]
        frame.depth = img.shape[2]
        frame.image = bytes(img)

        # Get the predictions of the component
        predictions = component_proxy.processImage(frame)

        # Print the predictions
        for pred in predictions:
            print(f"Box location=({pred.x},{pred.y}),Width={pred.w},Height={pred.h},Label={pred.label}")

        # Destroy the communicator to ensure the program finishes properly
        ic.destroy()

The program basically executes all the operations defined by the interface that I have previously prepared, for the thereshold there is a getter and a setter so
we can check if they work. Finally, tests the principal operation of the component that given an image as an input return a list with the boxes and labels predicted for that image. Reads an image locate in the test directory and returns its prediction, the image has as attributes the width, height, depth and a sequence of bytes that contains the proper image. The greater problem that appear was related to connecting to the proxy of the component, I finally I discover that the thread of the component finished with the program so in the end of the program I create a infinite loop that only finished when the user press Control+c in the terminal.

### Improvements and conclusion

After the testing, appeared some errors that needed to be solved, but no one of them was important. The component does not stand out for being fast, but as I can only test it an environment with a CPU I expect that the perfomance will dramatically increase using a GPU. After that, I only need to prepare the pull request for the official repository of LearnBlock from my fork. I added a directory call Detect with the files needed from the model to work properly, also I need to add the interfaces in IDSL and Ice format.

__Alejandro Fernández Camello__

