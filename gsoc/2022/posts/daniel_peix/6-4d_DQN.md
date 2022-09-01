 # Post 6: 4D DQN
The goal described in this post consist on the adjusting of the current code to fit one more dimension: closing and oppening the gripper.

## Basics: Why is the gripper movement added?
After seen the results of the 3-dimensional training, the 3D positioning seems to be successfull, so improving the environment in order to fit the fourth dimension seems to be the next step. This brings us the possibility of grasping the cube whtn the gripper has reached its 3D pose.

## Adapting the environment
This section descibes all the changes perfomrmed on the environment, in order to support a 4-dimensional training process and be able to process all the new information taken from the environment. 

### Spaces and observation

#### Action space
By adding the fourth dimension to our environment, the gripper movements are required. To support this, the action space must be upgraded in order to support that movement. The last layer of the DQN's neural network has a size equal to the number of possible actions to be taken in the environment. In this case, there are tree different values for each action (-1, 0 or 1), and there are four actions (x-axis, y-axis, z-axis and gripper), so the size of the NN's output will be 27 (3 ^ 4 = 81). Also the step function has been modified in order to be able to perform gripper's movements.

#### State space
With the fourth dimension added, the state space's size increases. In order to add this new dimension to our environment, we only need to change the value of the constructor's parameter, in DQN.py file.

#### Observation's shape
In this case, the size of the observation needs to change. As we are now using the gripper, we need a way of detecting when the cube has been grasped. In order to achieve this, is mandatory to extract more information from the environment. Seven different data will be returned in the observation array: signed x-axis, y-axis and z-axis distance, the information from the two sersors placed on the gripper's 'fingers' and the information from the two sersors placed on the gripper's 'hand'. With this new data, we know enough information to be able to deteect collisions and manage the movement in three dimensions.

### Adjusting the reward function
This reward function is quite similar to the 3-dimensional one, just adding the griper's 'hand' info. The data which is used in this new reward function is: 2D distance, 3D distance, the gripper's 'fingers' data and the gripper's 'hand' data.

## Results
TODO: YouTube links

__Daniel Peix del Río__
