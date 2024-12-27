---
layout: post
title: Policy Gradient, TRPO, PPO, DPO
date: 2024-12-24 10:14:00-0400
description: Things I learned recently about advanced Policy Gradient Methods.
tags: RL, LLM
categories: Machine Learning
giscus_comments: true
related_posts: false
---


## Prereqs
<!-- {:data-toc-text="Prereqs"} -->

We assume prerequisite knowledge in Reinforcement Learning definitions (MDPs, etc.), some Calculus, and some Linear Algebra.

## Policy Gradient

Let $\theta$ be the parameters for a policy $\pi_\theta$.  Consider a trajectory $\tau = s_1,a_1,s_2,a_2,...,s_T,a_T$ and the trajectory distribution 

$$ p_\theta(s_1,a_1,s_2,a_2,...,s_T,a_T) = p(s_1) \prod_{t=1}^T\pi_\theta(a_t|s_t) p(s_{t+1}|s_t,a_t).$$

We can think this as probability of taking the trajectory $\tau$ under the policy $\pi_\theta$ and the transition function $p(s_{t+1}|s_t,a_t)$. On the RHS, $p(s_1)$ is the probability begin the trajectory at $s_1$, $\pi_\theta(a_t|s_t)$ is the probability that our policy takes action $a_t$ in state $s_t$, and $p(s_{t+1}|s_t,a_t)$ is the probability the enviornemnt transitions to $s_{t+1}$ when in state $s_t$ and taking action $a_t.$

Let $r: \mathcal{S} \times \mathcal{A} \rightarrow \mathbb{R}$ be a reward function that takes in a state and a action and ouputs the reward. The goal in RL is to maximize reward, so we are looking for the optimal parameter $\theta^*$ such that 

$$\theta^* = \text{argmax}_\theta \mathbb{E}_{(s,a)\sim p_\theta(s,a)}\left[\sum_{t=1}^T r(s_t,a_t)\right]. $$ 

Let $J(\theta) = \mathbb{E}_{(s,a)\sim p_\theta(s,a)}\left[\sum_{t=1}^T r(s_t,a_t)\right]$ be our objective function that we want to maximize. To make the notation cleaner, we introduce the return function $R$ so that $R(\tau) = \sum_{t=1}^T r(s_t,a_t)$. Then 

$$J(\theta) = \int p_\theta(\tau) R(\tau) d\tau.$$

To optimize $J(\theta)$, we would like to use a first-order (gradient) method, so let's calculate $\nabla_\theta J(\theta).$

$$
\begin{aligned}
    \nabla_\theta J(\theta) & = \int \nabla_\theta p_\theta(\tau) R(\tau) d\tau\\
    & = \int p_\theta(\tau) \frac{\nabla_\theta p_\theta(\tau)}{p_\theta(\tau)} R(\tau) d\tau \quad \text{(multiply and divide by $p_\theta(\tau)$)}\\
    & = \int p_\theta(\tau) \nabla_\theta \log (p_\theta(\tau)) R(\tau) d\tau \quad \text{(by derivative of log)} \\
    & = \mathbb{E}_{\tau \sim p_\theta(\tau)}[\nabla_\theta \log (p_\theta(\tau)) R(\tau)]
\end{aligned}
$$
Let's now expand $\nabla_\theta \log p_\theta(\tau)$. 

$$
\begin{aligned}
    \nabla_\theta \log p_\theta(\tau) & = \nabla_\theta (\log p(s_1) + \sum_{t=1}^T (\log \pi_\theta(a_t|s_t) + \log p(s_{t+1}|s_t,a_t))) \quad \text{(by log rule)}\\
    & = \sum_{t=1}^T \nabla_\theta \log \pi_\theta(a_t|s_t) \quad \text{(only terms that are function of $\theta$)}
\end{aligned}
$$

Substituting this into $J(\theta)$, we have 

$$
    \nabla_\theta J(\theta) = \mathbb{E}_{\tau \sim p_\theta(\tau)} \left[ \left( \sum_{t=1}^T \nabla \log\pi_\theta (a_t|s_t) \right) \left(\sum_{t=1}^T r(s_t,a_t)\right)   \right],
$$

We can estimate this value by sampling $N$ trajectories. Then we would have
$$
    \nabla_\theta J(\theta) \approx \frac{1}{N} \sum_{i=1}^N \left( \sum_{t=1}^T \nabla \log\pi_\theta (a_{i,t}|s_{i,t}) \right) \left(\sum_{t=1}^T r(s_{i,t},a_{i,t})\right).
$$ 

With the estimate of $\nabla_\theta J(\theta),$ we can gradient ascent by 
$$\theta \leftarrow \theta + \alpha \nabla J(\theta)$$ 
with step size $\alpha$. This is the REINFORCE algorithm (Williams 1992). Sample trajectories, estimate the gradient using the trajectories, update $\theta$. 

This algorithm will work in theory, but there are many improvements that we can make to reduce variance. 

### Rewards To Go
We can reformulate $\nabla_\theta J(\theta)$ as 

$$
    \nabla_\theta J(\theta) \approx \frac{1}{N} \sum_{i=1}^N  \sum_{t=1}^T \nabla \log\pi_\theta (a_{i,t}|s_{i,t})  \left(\sum_{t'=1}^T r(s_{i,t'},a_{i,t'})\right).
$$ 

Notice that at time step $t$, we are still summing over all rewards from time steps $t' < t.$ These rewards should not 


### Trust Region Policy Optimization


{:data-toc-text="Customizing"}


### Proximal Policy Optimization


### Direct Preference Optimization

