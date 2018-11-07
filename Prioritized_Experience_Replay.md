## Prioritized Experience Replay

<a href="../MADDPG_PER.ipynb">MADDPG_PER.ipynb</a> implements the same Unity Tennis environment, but with Prioritized Experience Replay instead of a standard replay buffer. PER provides the agents with experiences to learn from based on how important they are to the learning process. 

Experiences that have the greatest loss (divergence) from the current network predictions are fed more often during training. This gives the agents an opportunity to maximize their learning time by using experiences where they were the most inaccurate.

PER is based on <a href="https://arxiv.org/abs/1511.05952">this research paper</a>.

Parameters Alpha and Beta control to what degree PER is used versus randomly selected experiences and the importance given to them when updating network weights.
