# Post 2: Environment and algorithms
The goals detailed in this post consist on the implementation of an environment which is able tu support RL training processes, and also some RL
algorithms will be implemented in order to test them.

## Environment

### Gym Interface
An enviromnment able to support RL processes, must implement a set of methods, known as OpenAI Gym interface: open(), close(), reset(), step() and
render(). In order to implement these methods, I am going to use the ZMQ Remote API, available since CoppeliaSim v4.3 was released. It allows to
manage all the data available in a simulation, and also makes possible to control the simultion itself (start, end, reset, load a scene, change
the speed, ...).

### Implementation
Apart from using the ZMQ API, it is neccessary to make the code easy to mantain, clear and clean. All the implemented code has been organized in
different files according to its functionality.

### Improvements
When I tested the environmnt it worked to slow, so i decided to take some time references and find the bottleneck of the code. The issue was that
the ZMQ API script calls were too slow, so I decided to gather them and reimplement the code in irder to reduce the calls as much as possible.

## Algorithms
Once the environment is ready, it is time to develop some algorithms to test it and see some results. In this post, only and introduction will be
shown.

### Q learning
It is an algorithm based on dynamic programming and Bellman's equation (Q stands for 'Quality'). The main idea of Q learning is hto have an
mxn-sized table (m: number of states, n: number of actions), and the content of thet table will be values that indicate how god or bad is the
action in a certain state. The learning process consists on filling the Q table with the appropriate values, using the Bellman's equation. This
algorithm considers a discrete space os states, as well as a discrete space of actions, as both are needed as indexes to access the Q table. 
To test this algorithm, only 2 dimensions has been considered (x-axix and y-axix movements).

### DQN
It is kind a continuous version of Q learning. Intead of using the Q table (which needs a discrete state space) it uses a neural network (NN), that
offers the advantage of using a continuous space state. The NN takes as input the state (continuous values) extracted from the environment, and the output
consists in the most suitable action to be performed in that state. The NN funcions the same way as the Q table did.

__Daniel Peix del Río__
