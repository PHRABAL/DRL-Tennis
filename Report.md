# DRL - Multi-Agent DDPG Algorithm - Tennis Collaboration

### Model Architecture
The Udacity provided DDPG code in PyTorch was adapted to employ two agents acting independently, but with a shared experience buffer. Each agent has its own set of deep neural networks (local and target actors and critics), each with two hidden layers of 256-128 nodes, with ReLU activation functions on the hidden layers and tanh on the output layers. The agents shared one experience memory buffer.

### Hyperparameters
A learning rate of 1e-3 on each DNN and batch size of 128 were used along with replay buffer size of 1e6, gamma .99 and Tau of 6e-2. Each agent took one step, then learned once, then repeated. After optimizing these hyperparameters, the agents were learning and achieving the desired goal of a 0.5 average reward. However, the agents took several hundred episodes to gain traction and start playing effectively. I determined that the exploitation-exploration balance needed further work to have the agents learn faster.

### Exploitation vs. Exploration

When training agents to succeed in an environment where the rules, boundaries and outcomes are completely unknown, it's extremely important to strike the right balance between having the agent explore the environment to learn how it's shaped and exploit what's learned to achieve the highest possible reward. If the agent doesn't explore enough, it might not find the optimal actions to take. If the agent explores too long, it will be slow to achieve the desired reward. 

In the Unity Tennis environment, I found that early exploration is extremely important and taking a wide variety of random actions accelerates learning. However, I also found that allowing the agents to keep experimenting/exploring too far into the simulation hurts long term learning performance.

### Exploratory Boost

To address this balance, I created the Exploratory Boost method. The approach essentially sets aside achieving rewards by the agent for a fixed period of time in the beginning of training in favor of wild, broad exploration of the environment. Then, at an optimal time determined through tuning, all exploration is cut off in favor of exploiting what has been experienced thus far with an all out pursuit of maximum reward. My approach discards the conventional deep reinforcement learning approach which slowly shifts agents from exploring to exploiting over time and, instead, focuses mainly on one task (exploration), then only the other (exploitation.)

Below are two graphs showing the improved performance of Exploratory Boost. Each had identical hyperparameters, except the noise (exploration) settings. <strong>Notice that in addition to faster overall convergence to the goal, Exploratory Boost also results in far fewer outlier rewards at the low end (blue that's below the yellow trend line.) The agents are experiencing far fewer poor performing episodes. They are more consistent in reaching a decent reward each time. This indicates Exploratory Boost has resulted in a higher quality of learning.</strong>

<img src="Noise_decay_method_versus_Exploratory_Boost.png">

<i>LEFT: Best result from using the traditional slow transition from explore to exploit (559 episodes.) RIGHT: Best result from Exploratory Boost approach (384 episodes.)</i>

I used Ornstein-Uhlenbeck noise with parameters of 0.13 theta and 0.2 sigma. I implemented a noise volume of 6 at the start of training, which mulitplied the OU noise output by 6, resulting in heavy noise and a wide variety of exploratory actions for the first 250 episodes. I then reduced the noise to zero thereafter.

### Results and Future Work

Utilizing the MADDPG algorithm with the above hyperparameters and Exploratory Boost the agents achieved the average score of 0.5 in 384 episodes.

For the objective of this project, the model produced a satisfactory result. However, as noted by Udacity in its own training and similarly found in my training, the agents are not stable or reliable on-goingly. If you allow them to continue playing, they vary considerable episode to episode in the reward attained. This may be partially due to the not truly cooperative play environment noted in the Overview, but it is also worth exploring what other model structure could result in consistent, on-going success of these agents.
