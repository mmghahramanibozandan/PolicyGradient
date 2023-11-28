# Policy Gradient
To maximize the performance measure $J(\theta)$ that depends on the policy parameter $\theta \in \Theta$, a standard approach is to improve the policy by following the gradient ascent:

$$ \theta_{t+1} = \theta_t + \alpha\widehat{\nabla J(\theta_t)} $$

where $\alpha$ is the learning rate. But how do we copmute $\widehat{\nabla J(\theta_t)}$?

It turns out that:

$$ \nabla J(\theta_t) \propto \mathbb{E}_\pi[G_t \nabla\log(\pi(a\vert s, \theta))] $$

hence every sample of that quantity yields an unbiased estimate for the gradient!

The update becomes:

$$ \theta_{t+1} = \theta_t + \alpha G_t \nabla\log(\pi(a\vert s, \theta)) $$

Method: **REINFORCE**

Game: **Short Corridor**

### Short corridor with switched actions

It is a gridworld environment with only 4 states and 2 actions:


1. The leftmost state is the _starting state_ (i.e. every episode always begins in this state). Two actions are available:
    - _left_: no movement
    - _right_: move to the right (i.e. in the second state)


2. The second state has the same actions but with opposite outcomes:
    - _left_: move to the right (i.e. in the third state)
    - _right_: move to the left (i.e. in the first state)


3. The third state is similar to the first, except that it is not a starting state. Again the actions are:
    - _left_: move to the left (i.e. in the second state)
    - _right_: move to the right (i.e. in the fourth state)


4. The fourth state is the _goal state_, in which the episode ends.

The reward is simply -1 for each transition (apart from the last one leading to the fourth state), therefore the aim
will be to minimize the number of transitions in order to reach the goal state.

The environment is implemented through a standard `step` function, with a specific
label for the actions. The function does not return the next state but only updates its value as an inner variable
of the class.
![img](https://github.com/mmghahramanibozandan/PolicyGradient/blob/main/img/download2.png)
![img](https://github.com/mmghahramanibozandan/PolicyGradient/blob/main/img/download3.png)
