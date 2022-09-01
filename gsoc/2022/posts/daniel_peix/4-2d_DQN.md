# Post 4: 2D DQN
The goal described in this post consist on the implementation of the DQN algorithm just for 2 dimensions.

## Basics: Why only two dimensions?
By using two dimensions, we can propose an easy situation to solve. Although it is a simple solution, the state space to explore is big enough to check if the environmrnt is working as it should be, and also see if the model converges or not.

## Adapting the environment
This section descibes all the changes perfomrmed on the environment, in order to support a 2-dimensional training process, and also minor changes to improve it. 

### Spaces and observation

#### Action space
With two dimensions in our environment, x-axis and y-axis movements are required. The last layer of the DQN's neural network has a size equal to the number of possible actions to be taken in the environment. In this case, there are tree different values for each action (-1, 0 or 1), and there are two actions (x-axis and y-axis), so the size of the NN's output will be 9 (3 ^ 2 = 9). Also the step function has been modified in order to be able to perform both movements.

#### State space
In order to support two dimensions, the spaces.py file needs to be modified. To simplify this changes, a parameter has been added to de constructor, so when changing the number of dimensions used in the training process is needed, the only change that needs to be performed is this parameter, in DQN.py. 

#### Observation's shape
In this case, the size of the observation will be just two: signed x-axis and y-axis distances. With this new data, we know enough information to manage the movement in two dimensions.

### Spaces' creation and observation's shape
The space has been modified in order to have only 2 dimensions, x-axix and y-axis, also the action space is just movements in those axis. The observation's shape consists in just two values: signed distance on both x-axis and y-axis. This two values give the information needed to calculate a decent reward.

### Adjusting the reward function
The reward function is one of the most important aspects of a Reinforcement Learning environment. A well planed reward function will bring nice results to the training processes, but a mediocre reward function will only bring poor results during the training process.

In order to create a decent reward function, the 2d distance is used. With two thresholds, the environment can check is the gripper is above te cube, far away from it or any other possible situation. Depending on which situation is taking place, the reward wil be different.

## Results
TODO: YouTube links

__Daniel Peix del Río__
