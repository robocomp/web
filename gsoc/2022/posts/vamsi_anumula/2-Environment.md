# GSoC'22 RoboComp project: Reinforcement Learning for pick and place operations

30th June 2022

## Environment 
The aim of the project is to make a Open AI Gym wrapper for the exisiting robotic arm model in CoppeliaSim. The gym wrapper creation eases the process of training our agent. The currently available library implementations of state-of-the-art Deep RL algos require the custom environment to follow this gym.Env structure. A standard wrapper has been built until now. Curently, the task is for the robot arm to reach the object, grasp it and lift to a desired height. 

# Environment Description

## State Space

A 26 dimensional continuous state space is considered, comprising of:

|        Info                           |  Dimensions |
| -------------------------             |  ---|
| Block pose: 3 coords+ 4 quarternions  |  7  |
| Gripper tip position corods           |  3  |
| Relative position of block w.r.t tip  |  3  |
| Left grip force sensor                |  3  |
| Right grip force sensor               |  3  |
| Left finger force sensor              |  3  |
| Right grip force sensor               |  3  |
| Gripper info                          |  1  |

## Action space

5 dimensional action space in either discrete or continuous setting.

|        Info               |  Discrete  |  Continuous |
| ------------------------- |  ---       |  ---   |
| Move arm in x-direction   |  {-1,0,1}  |[-1,1]  |
| Move arm in y-direction   |  {-1,0,1}  |[-1,1]  |
| Move arm in z-direction   |  {-1,0,1}  |[-1,1]  |
| Move wrist                |  {-1,0,1}  |[-1,1]  |
| Open/Close the gripper    |  {-1,0,1}  |[-1,1], but will berounded off to {-1,0,1}  |

## Reward

The goal is for the arm to grasp the object and pick it to a certain height. The objct will only be able to achieve the desired height only if the arm was able to successfully grip it. So, the reward function will be a gradually decreasing negative score proprtional to absolute deviation from the current object height to the desired height, in range of [-1,0] and once the desired height is acheived, a positive scoreof +10 is awarded.
Huge penalty of -100 is awarded in case of an invalid state/collision.

## Algorithms

For continuous action space, Soft Actor Critic(SAC) is considered and Deep Q Network is considered for the discrete setting. 

## Training process objectives
- Train the agent using existing imlementations of SAC, DQN using Stablebaselines3 library.
- Continuously modify environment to fix bugs encountered during training process.
- Experiment and investigate agent performace with different reward fucntions
- Carry out hyperparameter tuning to achieve the desired goal

# Further steps

## Goal Environment for goal-conditioning with HER

Since, the task of pick and place is quite complex, we want to use to leverage the idea of goal-conditioning. With goal-conditioning, each episode is considering as a success by treating the achieved terminal state as a virtual goal state. Hindsight Experience Replay(HER) is used to achieved the goal conditioning for our agent. In order to use HER, our environment need to be modified into a gym.goalEnv structure, where the observation space consists of state, achieved goal and desired goal, and the reward for each time step will be computed based on this structure. This goal env will be created and tested. Any off-policy algorithm like SAC, DQN then can be used along with HER to achieve a more robust and sample efficient training of the agent.

...

__Vamsi Anumula__
