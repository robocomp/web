# Post 7: Conclusions and improvements

## Conclusions
Throughout this project, I have expanded my knowledge of reinforcement learning. It was a field of which I only knew some very basic concepts, so I have learned quite a few things that I did not know before. 

I have also understood the functioning of the two algorithms used: the Q algorithm and DQN. 

The most important conclusion I draw from this whole project is that the reward function is the most important part of the training process. With a reward function that is able to describe the policy or behavior that the robot has to learn, you will surely always get the desired results or, at least, results with a fairly high quality. Conversely, a poorly designed reward function will prevent good results from being obtained during the training process.

## Improvements
During training and as detailed in the post "4D DNQ", the computer suffers a lot because CoppeliaSim uses a large part of the RAM memory, and can even clog the computer. 

In order to solve this problem, one idea would be to store every thousand episodes the target neural network in a file and load it in the next episode. Even if the training is paused when restarting CoppeliaSim is needed, the neural network will not start from scratch, but will have the values it had before restarting the simulator. 

__Daniel Peix del Río__
