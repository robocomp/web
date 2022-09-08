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

During our testing in phase-1, I observed that if the target is given inside an
occupied cell, the MPC tries to move towards it as one of the cost function of
the MPC is to minimize the distance between the robot position and the goal
position. This often leads to the robot crashing as it reeached near the
obstacle. To fix this issue I first checked if the target and all it's
neighbouring cells are unoccupied. If even one of the neighbouring 16 cells of
the target is occupied, I consider the target to be inside a occupied cell and
move the target to the nearest free cell available. 

The following code snippet is taking care of this:

```C++
if(neighboors_16(target).size()<16){
      std::optional<QPointF> new_target = closest_free(target_);
      target = pointToKey(new_target->x(), new_target->y());
      std::cout<<"OCCUPIED"<<std::endl;
 }
```
In the video [ [Target in obstacle] ]( https://youtu.be/mq_63IHb0MQ ), you can
see how the robot performs when the target is given in an obstacle. Before
fixing this issue, the robot used to crash but now the robot no longer crashes.
It goes near the obstacle and stops. [ [Pull Request #379] ](
https://github.com/robocomp/robocomp/pull/379 ) 

## Contribution 2: Passing through narrow corridors

Another problem I found during my phase-1 testing period was that with the
euclidean distance obstacle avoidance constraints, the robot can't pass through
narrow corridors. The below image shows that the occupied cells in the map are
marked overconservatively. In the image, the green lines represent the actual
obstacle boundaries.

![](assets/narrow_corridor.png)

Because of this overconstrained representation of the obstacles, the MPC was
unable to come up with a feasible trajectory that can take the robot across the
corridors. Currently this was happening because given an occupied cell, all it's
16 neighbouring cells were also marked as obstacles. I fixed this my marking the
8 neighbouring cells as obstacles instead of 16. 

The below code snippet does is taking care of this:

```C++
for (auto &&[k, v]: iter::filterfalse([](auto v) { return std::get<1>(v).free; }, fmap))
{
    v.cost = 100;
    v.tile->setBrush(occ_brush);
    for (auto neighs = neighboors_8(k); auto &&[kk, vv]: neighs)
    {
        fmap.at(kk).cost = 100;
        fmap.at(kk).tile->setBrush(occ_brush);
    }
}
```

In the video [ [Passing through narrow corridors] ](
https://youtu.be/1x6ngcrBRds ), you can see that the robot can now pass through
the narrow corridors with the euclidean distance obstacle avoidance constraints.
We can also observe that the obstacles are now represented in a much less
conservative way.
[ [Pull Rrequest #379] ]( https://github.com/robocomp/robocomp/pull/379 ) 

## Contribution 3: Reformulating the obstacle avoidance constraints as freeballs

Suppose we have N obstacles and we are planning for T timesteps into the
future. Using the euclidean distance obstacle avoidance constraints, for each
timestep we will have a constraint for each of the N obstacles such that the
distance between the robot and the obstacle is greater than the sum of the
radius. Therefore for T timesteps, we will have N\*T constraints. This is a lot
of constraints and will slow down the computation time. To overcome this , we
use the freeballs algorithm as mentioned in the paper [ [An NMPC Approach using
Convex Inner Approximations for Online Motion Planning with Guaranteed Collision
Avoidance] ]( https://arxiv.org/abs/1909.08267 )  to avoid obstacles. In this
approach, we first take an initial guess for T centerpoints and and optimize for
them using a gradient based update rule such that the center points are furthest
away from the closest obstacle at that timestep. Now for each free ball we draw
a circle such that it's radius is the distance to the closest obstalce. If the
distance is above a certain threshold, we take a maximum circle radius defined
by the user. Once we have the center points and the radius, we add a constraint
to the MPC formualtion such that the robot always stays inside the circle. With
this approach, we only have T constraints and because of the decrease in the
number of constraints the computation time also decreases a lot. 

However this approach is very dependent on the value of the weight variables.
That is why to improve this, I added the feature that we will do a line search
for the weight variables and whichever weight will lead to a trajectory that is
furthest away from all the obstacles will be selected. In my experimentation, I
observed that we can only search for 3 weight variables after which the
computation time increases too much to operate safely in the environment.

In the video [ [Free Balls obstacle avoidance with automatic weights tuning] ](
https://youtu.be/BvM0eflDXGI ), the robot uses the freeballs algorith, with the
automatic weight search to navigate in the environment with narrow corridors.
[ [Pull Request #9] ]( https://github.com/robocomp/optimizer/pull/9 ) 


