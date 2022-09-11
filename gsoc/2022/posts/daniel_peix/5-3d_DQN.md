# Post 5: 3D DQN
The goal described in this post consist on the adjusting of the current code to fit one more dimension.

## Basics: Why three dimensions?
After seen the results of the 2-dimensional training, improving the environment in order to fit 3 dimensions seems to be the next step. This brings as lot of new information to the observation and state, so the reward function will be more difficult to adjust in order to obtain decent results.

## Adapting the environment
This section descibes all the changes perfomrmed on the environment, in order to support a 3-dimensional training process and be able to process all the new information taken from the environment. 

### Spaces and observation

#### Action space
By adding the third dimension to our environment, the z-axis movements are required. To support this, the action space must be upgraded in order to support that movement. The last layer of the DQN's neural network has a size equal to the number of possible actions to be taken in the environment. In this case, there are tree different values for each action (-1, 0 or 1), and there are also three actions (x-axis, y-axis and z-axis), so the size of the NN's output will be 27 (3 ^ 3 = 27). Also the step function has been modified in order to be able to perform z-axis movements.

#### State space
With the third dimension added, the state space's size increases. In order to add this new dimension to our environment, we only need to change the value of the constructor's parameter, in DQN.py file.

#### Observation's shape
In this case, the size of the observation needs to change. As we are using 3 dimensions, we need a way of detecting collisions. In order to achieve this, is mandatory to extract more information from the environment. Five different data will be returned in the observation array: signed x-axis, y-axis and z-axis distance, and the information from the two sersors placed on the gripper's 'fingers'. With this new data, we know enough information to be able to deteect collisions and manage the movement in three dimensions.

### Adjusting the reward function
This reward function is not as trivial as the one done for two dimensions. In this case, there is more information available from the environment, so the reward function might be a little more complicated. The data which is used in this new reward function is: 2D distance, 3D distance and the gripper's 'fingers' data. Using two values for the distance (2D and 3D) allows us to give more importance to the 2D distance over the 3D one, because is crucial to be first above the cube.

## Results
Start of the training: https://youtu.be/zBbi9Xjelkg
End of the training: https://youtu.be/T5mk46UGFe8

__Daniel Peix del Río__
