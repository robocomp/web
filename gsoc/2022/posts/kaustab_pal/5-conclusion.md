# GSoC'22 RoboComp project: Model Predictive Control for obstacle avoidance 

08 September 2022

## Detailed report

While the above contributions explain my GSoC'22 work, you can find a more
detailed explanation along with mathematical explanations here: [ [GSoC'22
Project Report] ]( https://kaustabpal.github.io/gsoc_22_report ) 

## Future scope

While the free balls algorithm works really well in complex environment, there
are much to be explored on how we can speed up the computation time to compute
the trajectories more efficiently. One approach would be to comne up with better
ways to initialize the optimizer. Another approach can be to make the trajectory
optimization formulation differentiable. Having a differentiable formulation
will enable us to integrate the trajectory computation with the perception
system in an end to end manner.


