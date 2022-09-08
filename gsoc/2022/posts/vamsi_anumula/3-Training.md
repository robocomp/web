
# GSoC'22 RoboComp project: Reinforcement Learning for pick and place operations

8th September 2022

## Training Objective
The goal of the current phase is for the robot arm to reach the block, grasp it and lift it to a desired height above ground.

## Reward

The agent will get rewarded as follows:

|        State                           |  Reward | Terminal? |
| -------------------------             |  ---|   ----   |
| Arm is far way from the block         |  -100  |  Yes  |
| Collision detected                        |  -100  |  Yes  |
| Grasp detected and dh>0                 |  1000\*dh_norm | No |
| Goal height reached                 |  10,000 | Yes |

### Notation
dh:= change in object height from ground \
dh_norm:= Normailzed dh

*\*The reward structure is subject to change*

## Algorithms

Soft Actor Critic (SAC) is chosen for training in continuous action space setting.

## Trained agent demo

*TODO*

## Reward curve

*TODO: Will be added once hyperparameter tuning is done.*

## Futher Steps
 - The next step would be train the arm to place the block at desired position after grasping, by modifying rewards.
 - Modify exisitng env to support Goal Conditioning and train the arm using SAC, along with HindSight Experience Replay(HER) replay buffer to achieve a more robust and sample efficient training of the agent.
