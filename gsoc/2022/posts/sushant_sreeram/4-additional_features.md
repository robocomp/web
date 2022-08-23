# Additional Features


## SNGNN reward function
    
SNGNN is a graph neural network that was trained on social scenarios from the SocNav dataset. A graph neural network is just another neural network. But instead of data such as images, this network takes in a graph data structure as an input. Graph neural networks have started gaining more attention, because it is very simple to model problems as a graph. The paper [Graph Neural Networks for for Human-aware Social
Navigation](https://arxiv.org/pdf/1909.09003.pdf) describes how a scenario is converted to a graph. Once the current environmental scene is converted to a graph, the SNGNN network would output a score that depicts whether the robot causes any discomfort to the humans, or not. There is an additional output that the network outputs that shows how well the robot is travelling to reach its goal.

## Manual Control

A manual controlling script has been written to control the robot using a keyboard. The code has been written using Python's Pygame library. This is very helpful when we want to observe the rewards / observations from a specific positon. And who doesn't have fun just roaming around with the robot in the environment!

## Custom Environment Checks

Since the environment is constantly under improvement, changes can break the whole code, and this is very undesirable. In order to prevent this from happening, a few tests were written using Pytest. These tests would check whether the observations are correct, if the shapes of the observation space, action space match the shape that the environment outputs, and a few other small checks. 