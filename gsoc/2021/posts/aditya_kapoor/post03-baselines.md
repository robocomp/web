# Baselines implemented

## Reinforcement Learning
Reinforcement Learning has four essential elements:

  1) Agent. The program you train, with the aim of doing a job you specify.
  2) Environment. The world, real or virtual, in which the agent performs actions.
  3) Action. A move made by the agent, which causes a status change in the environment.
  4) Rewards. The evaluation of an action, which can be positive or negative.
![Environment_Agent](https://user-images.githubusercontent.com/39992294/125690449-89d90615-3722-405c-8833-324e1dbeeb09.png)


## Neural Network Architecture

### Graph Attention Network
We are using Graph Neural Networks as our barebones to facilitate Deep side of the RL algorithm. Every entity in the room or the environment represents a node of a graph structure that has its own set of features, called as node feature vectors.
These features can comprise of their position coordinates, velocity etc. 

![GraphAttentionNet](https://user-images.githubusercontent.com/39992294/125680613-7c033c6e-c90f-436f-bc53-31eeeb95b856.png)

As a result the entire environment can be represented as one huge graph that has information needed to solve the environment, that is, it comprises of the global state of the environment that can be used to reconstruct the scene.

To visualise how a Graph Neural Network (GNN) works, one can imagine that every node has its own Neural Network with shared weights/ parameters across each node. There is one catch here, that is after every layer of the Neural Network, there is an aggregation step.
For Graph Attention Networks (GAT), this aggregation turns into a weighted aggregation. Each node assigns an attention weight to its incoming edges and multiplies each of the neighboring node's feature vector with this attention weight and sums them to get a single aggregated feature vector.
The weights are computed using the node feature vectors of each node based on some kind of similarity measure or pattern matching, depending on the type of Attention Mechanism is being used.

These final feature vectors are then either averaged (average across all nodes) or anyone of the final feature vector of a node is passed through a MLP to get the Policy or Value or both (depending on the RL algorithm).


## Deep Q Learning (DQN) and its variants

### DQN
The objective of the agent in the environment is to maximize rewards across an episode. The cummulative reward that an agent gets after an episode terminates is called returns. 
The Q Network is used to estimate the State-Action Values for all possible actions given a state, that represents the average return an agent gets on successful termination of the episode given a state-action pair. Once the Q-network becomes accurate on its prediction, the optimal policy would be to greedily choose a transition that 
yields the best state-action value and DQN exactly makes use of this Policy.

![DQN](https://user-images.githubusercontent.com/39992294/125689696-654f2bdc-1aa5-42d5-b526-36cb0a0e1c3b.png)

### DDQN
Double DQN is used to address the moving target problem in DQNs. In this, there are 2 copies of the DQN, one is trained using the Buffer and the other is updated after regular intervals. The target value is calculated using the second copy of the DQN.
![DoubleDQN](https://user-images.githubusercontent.com/39992294/125689835-28b161d3-7821-496d-9e54-4b76f6c45a42.png)


### Dueling DQN
Dueling DQN is a variant of the DQN that stabilises training by addressing the problem of over estimation of state-action values of predicted by DQN. 
![DuelingDQN](https://user-images.githubusercontent.com/39992294/125689871-b373f4dc-7ec3-46c4-be00-327169eacb85.jpeg)


### PER
Prioritized Exprience Replay is a variant of a Replay Buffer that tries to improve the convergence of the DQN by learning from the most erroneous samples. It samples the trajectories that led to a huge error.
![PER](https://user-images.githubusercontent.com/39992294/125689908-24e54fc4-aa58-45c6-a690-8f059a00df0b.png)


## Advantage Actor Critic (A2C)
The actor critic algorithm consists of two networks (the actor and the critic) working together to solve a particular problem. At a high level, the Advantage Function calculates the agent’s TD Error or Prediction Error. The actor network chooses an action at each time step and the critic network evaluates the quality or the Q-value of a given input state. As the critic network learns which states are better or worse, the actor uses this information to teach the agent to seek out good states and avoid bad states.
![A2C](https://user-images.githubusercontent.com/39992294/125689939-c5a93efe-cdc9-4377-afba-f129e22eca12.jpg)

