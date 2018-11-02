<img src="https://user-images.githubusercontent.com/10624937/42135623-e770e354-7d12-11e8-998d-29fc74429ca2.gif">

# DRL - Multi-Agent DDPG Algorithm - Tennis Collaboration

## Overview
Using the Unity agent/environment "Tennis", this deep reinforcement learning task trains two AI agents to play tennis with each other in a cooperative way. The agents are rewarded for keeping the ball in play as long as possible. The task is considered solved when the average reward of the winning agent each episode hits 0.5 over 100 consecutive episodes.

The agents receive feedback in the form of a reward after taking each action. They decide whether to move their rackets forward or backward and at what velocity. They also can decide to jump. A +0.1 reward is given if the agent hits the ball over the net and a -0.01 penalty if they miss the ball or hit it out of bounds. The algorithm provides to each agent the velocity and position of both agents and the ball, but only tells each agent their own reward, not the reward of the other agent.

## MADDPG Algorithm
As seen in the code, the MADDPG algorithm is used to train the two agents. MADDPG is a multi-agent variant of DDPG, a model-free, off-policy, policy gradient-based algorithm that uses two separate deep neural networks (one actor, one critic) to both explore the stocastic environment and, separately, learn the best policy to achieve maximum reward. DDPG has been shown to be quite effective at continuous control tasks and here the multi-agent version is applied to this continuous control task.

## Collaboration ... Sort Of
The environment and use of the Mutli-Agent Deep Deterministic Policy Gradient (MADDPG) algorithm results in an unusual structure of game play. The agents are not incentivized to perform better than their opponent, so it is not competitive. However, the agents do not formulate a shared strategy to keep the ball in play for as long as possible, so it is not a true cooperative effort either. Each agent acts independently, without coordinating their actions, but their individual goals are such that it results in cooperative play. When one agent successfully keeps the ball in play, the other agent benefits by having the opportunity to increase its reward by also keeping the ball in play.

At first the agents randomly take actions and record the feedback, Eventually they begin to take those experiences and learn from them using separate deep neural networks under the MADDPG algorithm.

The attached code written in Python, using PyTorch and presented in a Jupyter Notebook, demonstrates how the agents learn and eventually achieve the average score of 0.5 in 384 episodes. The attached <a href="Report.md">Report</a> describes the algorithm and methodology in detail, including the introduction of Exploratory Boost.

## Setup Instructions

To reproduce this model on a Mac, clone the <a href="https://github.com/udacity/deep-reinforcement-learning">Udacity DRLND repo</a>, then place the tennis.app.zip file in the p3_collab-compet folder. Also place the Juputer notebook there and run it.
