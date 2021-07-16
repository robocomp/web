# GSoC'21 RoboComp project: Deep Reinforcement Learning for precise robot grasping and object manipulation

14th July, 2021

## Brief on work done in first phase

In the first phase, the initial couple of weeks were spent on the intensive shortlisting from the literature review and finding out of the feasibility of various works in our scenario. Eventually I chose
 [VPG-Toolbox](https://github.com/andyzeng/visual-pushing-grasping).
 
Which is a toolbox used extensively for Deep reinforcement learning in manipulators for grasping.


## About the toolbox

The vpg-toolbox is used to teach manipulators how to plan complementary pushing and grasping actions for manipulation. vpg uses an intel realsense camera to gain the RGB-D images.

vpg uses two FCN's to determine the best push and grasp. based on the RGB-D of the cluttered environment.

![](assets/vpg1.jpg)

## Tasks seen
To implement vpg onto the robocomp's ice framework I first had to translate the remoteAPI used to a PyRep component for better integration further down the line.

For this I used the UR5 PyRep example and the scene file from vpg-toolbox's repository.

Next, I had to implement the perception module to pass the RGB-D feed to the DRL module.

Note: These modules haven't yet been implemented into robocomp's ICE.

## Tasks ahead
- To complete the pipeline in robocomp's ICE.
- Replace the UR5 with kinova gen 3 and retrain the DRL model.

**Additionally**

- Use DSR as the primary middleware. 

## References

> [Learning Synergies between Pushing and Grasping
with Self-supervised Deep Reinforcement Learning](https://arxiv.org/pdf/1803.09956.pdf)

**Pawan Wadhwani**
