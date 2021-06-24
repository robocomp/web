# GSoC'21 RoboComp project: Improvement of a Social Navigation component

19th June, 2021

## About me

I have always been fascinated by the idea of bringing an otherwise inanimate and unintelligent system to life by adding an electronic brain. If machines could be endowed with humans’ ability to adapt and learn quickly, the resultant products could be used to perform any activity by using human-like intelligence but circumventing their low physical and mental resilience. To learn to program such intelligent robots, I pursued Computer Science as my undergraduate degree at BITS Pilani (Goa). Since then, I have focused my academic research at the intersection of Human Psychology, Cognitive Neuroscience and Robotics.


## About the Project

Mobile robots that come across people on a daily basis must react to them in a socially appropriate way. While conventional control algorithms treat all sensor readings as objects, they fail to capture the underlying behavior of such entities. In order to achieve this goal, one cannot really rely on hand-engineered heuristics for path planning algorithms. With the advent of Machine Learning, one can learn such heuristics in a data driven way. Social Navigation Graph Neural Network - 1D (SNGNN-1D) is one such Graph Neural Network based Machine Learning algorithm which evaluates the static scenes generated randomly from the point of view of the robot. It makes use of human labeled trajectory data, a score between 0 and 100 that demonstrates how good the robot’s position is with respect to its surroundings. This score, for every state in the room, is used to generate a heat map that is used by the A* algorithm to plan a path to the goal position. The problem with this approach is that it is computationally expensive. Also, SNGNN has been trained using static scenes and does not factor in dynamic settings like walking humans, which is a very common scenario in a social setting. A more cost effective way to carry out this task would be to train a policy for a robot to reach the goal. In such cases, Reinforcement Learning is a promising pursuit. However, it is difficult to structure a reward function for complex environments (social settings). In this case, one can make use of SNGNN-1D as a reward function because it scores the robot’s presence in the room with respect to its surroundings.
