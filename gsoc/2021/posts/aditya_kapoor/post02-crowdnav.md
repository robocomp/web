# Integrating CrowdNav environment setup in webots

## Introduction
We are currently implementing baselines and drawing inspiration from prior work done in Reinforcement Learning based Social Navigation frameworks. 
[Crowd-Robot Interaction:Crowd-aware Robot Navigation with Attention-based Deep Reinforcement Learning](https://arxiv.org/pdf/1809.08835.pdf) is one such simple framework that we are using as a test bed to develop our own social navigation algorithm.

## Setup 1
The objective of the agent (robot ) is to maximise rewards and it does that by avoiding collision and getting to its goal position. Along with the robot, there is one more entity in the room, that is humans.
The humans are randomly positioned on a circle of radius 4 meters and their target (goal) position is in diametrically opposite direction on the same circle. Random pertubation is added to the (x,y) coordinates of both starting and goal positions of the humans.
Now the robot, aka, agent has to learn to get to its goal position and also avoid collisions with the humans who will also be moving and are not mindful of the robot in its way. The paper makes use of this simple setup in both training and evaluating the performance of the algorithm


https://user-images.githubusercontent.com/39992294/125636861-9d9ef782-f3df-4c90-988f-3da763863c4d.mp4


## Setup 2
Here too, the objective of the robot is the same. However, the configuration of the humans in the environment is different. Instead of placing them in a circle of confined radius, in this setup we place them in a square/ rectangular setting. The goal positions of the human is on the other side of the quadrilateral.

https://user-images.githubusercontent.com/39992294/125636816-086e9128-91e3-4072-89ef-7a3feaab00e2.mp4

## Setup 3
As the objective of the robot is the same, the humans are placed randomly in the environment and they have random goal positions that they move towards.

### Note: In all the settings, once the human reaches its goal position, the human becomes static. The policy or the movement of the humans is precomputed and there is no learning involved there. However, the robot is learning with experience using the baselines that we have developed over the course time.
