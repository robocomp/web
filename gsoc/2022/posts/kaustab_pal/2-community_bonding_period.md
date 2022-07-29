# GSoC'22 RoboComp project: Model Predictive Control for obstacle avoidance 

30th June 2022

## Community bonding period 

The community bonding period lasted from May 20th to June 12th. This period was
mainly used to get familiar with my mentors, establishing communication channels
and understanding coding and documentation styles. 

I spent this period getting familiar with two components in the optimizer repo.
One of them is the **comp-casadi-cpp** and the other being **local_grid**. 

The **comp-casadi-cpp** component had the free balls MPC implementation and the
**local_grid** component has an implementation where a local grid is created
when a target is set and a path is calculated to the target from the robot's
current position. After that we can either follow the path using a *standard
MPC* or the *Carrot Chasing algorithm*.

### The Carrot chasing algorithm

Given a path, the carrot chasing algorithm simply moves the robot to the next
point in the path orienting the robot to follow the path accordingly. 

### Standard MPC

In the standard MPC, given a target, we use a cost function to optimize for the
controls that takes the agent closer to the target. The optimization problem
also has certain constraints like bounds on the controls, the dynamics model
constraint, acceleration constraints and obstacle avoidance constraints. 

### The Free-Balls MPC

This is the same as the standard MPC but the obstacles avoidance constraints has
been  modified to make the computation faster. In this formulation we first find
the centers and radius of freeballs that determine the occupied space and then
the MPC calculates the trajectories such that the trajectory points lie as close
to the free ball centers as possible. 

## Conclusion of Community Bonding Period

The community bonding period ended with me getting a good understanding of the
codes and the algorithms. For the phase 1 plan, we decided review, test and
correct the existing MPC algorithm. 
