# Post 3: DQN
The goals detailed in this post consist on the implementation of the DQN algorithm and also a collision detection system.

## DQN

### Basics
This is a Reinforcement Learning algorithm that consist on using a Neural Netwrk to store the mapping between the states of the environment and the actions to perform. 

### Integration
In this case, I took as a base an existing implementation of DQN, and then adapt it to the current environment, implemented previously. The main issue faced during this process was the sizes of te tensors using in the Neural Network, because the implementation taken was prepared for images, so I had to reimplement it and adapt the batch sizes in order to fix the environment.

## Collisions
Once DQN has been successfully integrated with the environment, tis time to solve a big problem: collisions. In CoppeliaSim, collisions can deform the elements of the simulation, and also break them.

In order to avoid this, is mandatory to implement a collision detection system.

### Updating from 2D to 3D
First of all, we will force the collisions by extending the training to 3 dimensions. By doing that, the gripper is more likely to crash either into the table or the cube. So, changes in the environment are needed, as well as adapting the input sizes of the neural network used for DQN.

### Detect and react to collisions
Then, in the reward function, it is needed to collect the data from the force sensors which are in the 'fingers' of the arm's gripper, and fix a threshold that allow us to detect a collision. 

If a collision is detected, that current episode must end, with a negative reward, and a normal reset of the environment will occur when starting the next episode, as usual.

__Daniel Peix del Río__
