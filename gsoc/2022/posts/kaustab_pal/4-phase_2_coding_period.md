# GSoC'22 RoboComp project: Model Predictive Control for obstacle avoidance 

08 September 2022

## Phase 2

The phase 2 started from July 25th. The plans for phase 2 are:
1. Introduce a feature where if the target is given inside an obstacle, the
   target will automatically be moved to the nearest unoccupied cell.
2. We discoreved a problem where the agent is unable to pass through narrow
   corridors. This bug needs to be fixed.
3. Re-formulating the obstacle avoidance constraints as free-balls [ [Paper] ](
   https://arxiv.org/abs/1909.08267 ) and implement that as a constraint in the
   MPC.

## Contribution 1: Move target if it is in occupied cell

During our testing in phase-1, we observed that if the target is given inside an
occupied cell, the MPC tries to move towards it as one of the cost function of
the MPC is to minimize the distance between the robot position and the goal
position. This often lead to the robot crashing as it reeached near the
obstacle. To fix this issue we added a check such that if the target of the MPC
is inside an occupied cell inside a occupancy grid map, we move the target to
the nearest free cell such that all the 16 neighbouring cells of the target are
also unoccupied.

The following code snippet is taking care of this:

```
if(neighboors_16(target).size()<16){
        std::optional<QPointF> new_target = closest_free(target_);
        target = pointToKey(new_target->x(), new_target->y());
        std::cout<<"OCCUPIED"<<std::endl;
    }
```

[ [Target in obstacle] ]( https://youtu.be/mq_63IHb0MQ ) 

[ [Passing through narrow corridors] ]( https://youtu.be/1x6ngcrBRds ) 
