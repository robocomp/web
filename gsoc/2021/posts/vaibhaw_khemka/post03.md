## ARCHITECTURE OF MobDepth:
<img src="assets/Mobdepth.jpg">

* Input - Camera Frame (480,640,3) , Output - Depth Map (240,320,1)
* **Design Choices:** <br />
  1. Real-Time Estimation - As the model needs to predict in real time, thus a light-weight architecture is required. <br />
     As *MobileNet* uses least Number of Parameters without compromising on the Generalization, Thus it is used as Encoder.<br />
     
     ![Pre-Trained-Models_Parameters](https://user-images.githubusercontent.com/46538042/125079484-4e3fce80-e0e1-11eb-80b2-e2898996054f.png) <br />
  2. Generalization and High-Quality Depth Map - *MobileNet* is Pre-trained on ImageNet Dataset and including *Skip-Connections* make it more generalizable, removing the problem of Vanashing Gradient.  
## SOME MORE RESULTS (on MobDepth(with Skip-Connections)):
a) Fig-1 <br />
![MobDepthwithskip_result1](https://user-images.githubusercontent.com/46538042/125090541-1179d480-e0ed-11eb-9f7c-ac104e6f716a.png)
b) Fig-2 <br />
![MobDepthwithskip_result2](https://user-images.githubusercontent.com/46538042/125090613-26eefe80-e0ed-11eb-98f3-0959d9a43dad.png)

## AUGMENTATION OF SIMULATOR DATA (coppeliaSim):
* To integrate the component with robocomp, model should give high quality depth map on Simulator data as well, obained using coppeliaSim. Thus, NYU dataset is Augmented with Simulator Data.

* Process of Data Collection of Simulator Data can be found in [Data-Collector](https://github.com/robocomp/grasping/tree/master/data-collector)

## FINE-TUNING USING COLLECTED SIMULATOR DATA:
* The Pre-Trained Model ("MobDepth (with Skip-Connections)") is trained further on collected simulator data to give high quality depth map in simulated world.

## RESULTS BEFORE AND AFTER FINE-TUNING:
a) Fig-1 <br />
![Before_Fine-Tuning1](https://user-images.githubusercontent.com/46538042/125087934-92839c80-e0ea-11eb-9aa6-8469804482d7.png)
![After_Fine-Tuning1](https://user-images.githubusercontent.com/46538042/125087929-90b9d900-e0ea-11eb-8f46-6e4a276785c2.png)

b) Fig-2 <br />
![Before Fine-Tuning2](https://user-images.githubusercontent.com/46538042/125088053-afb86b00-e0ea-11eb-9613-407b64aa1a5f.png)
![After Fine-Tuning2](https://user-images.githubusercontent.com/46538042/125088045-adeea780-e0ea-11eb-9b9c-3e58aa109fee.png)


     

