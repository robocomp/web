**Hello**, you might be aware of my project if you have read my previous post. For the first timers, I would again state the task of my project. My aim would be to integrate the Morse which stands for Modular Open Robot Simulation Engine with RoboComp. Morse is a generic simulator for academic robots that focuses on realistic 3D simulation. The simulator that  we have now in RoboComp is RCIS, therefore the idea of my project is to use the features of Morse in RoboComp for improved simulation.

----------

## How will the project be implemented
**The project** will be done by creating either three components implementing OmniRobot, RGBDBus and JointMotor interfaces or creating one single component that implement all of the above. Then this component will be simulated by Morse by adding necessary code required for the simulation.Then the interaction with these simulation will be done through other interfaces. 

-------
## Current Status
**Now**, I will tell you about the work done soo far and what were the difficulties that were faced while working. But before that I would like to thank my both mentors **Luis sir and Pablo sir**, for being very supportive and understanding mentor and being available all the time whenever I needed them.

The current repository which contains the work done so far is available [here](https://github.com/piyushpilaniya/Gsoc-2018).
I started my work by understanding How Morse works and simulated a few robots using Morse. The tutorials present on the Open Robot's website ([Click here to see](https://www.openrobots.org/morse/doc/stable/tutorials.html)) were a great help in achieving that. I then implemented a omni directional component simulated in Morse. Now I am advancing towards implementing RGBD and laser components along with that omni directional component. The problem faced by me was that Morse has very few predefined robots, sensors and actuators and it does not have one for omni platform. So that was a big problem. Although I got a little help from Morse and simulated the component.

