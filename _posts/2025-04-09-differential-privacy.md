---
title: 'Differential Privacy'
date: 2025-04-09
permalink: /posts/2025/04/differential-privacy/
tags:
  - Differential Privacy
---

This blog introduces Differential Privacy.

Differential Privacy (DP) is a strong privacy notion that upper bounds the amount of influence an individual in a private dataset has on the output of an algorithm. In the context of machine learning, this means reducing memorization of each individual and forcing the model to learn features that are shared amongst the population.

Differential Privacy
======
Let $$\epsilon > 0$$ and $$\delta \in [0,1]$$. A randomized algorithm $$M : \mathcal{D} \rightarrow \mathcal{R}$$ satisfies $$(\epsilon, \delta)$$-DP if for any pair of adjacent datasets $$D, D' \in \mathcal{D}$$ that differ exactly in a single data sample, and for all sets $$\mathcal{R} \subseteq \mathcal{R}$$ it holds that

$$\Pr[M(D) \in \mathcal{R}] \leq e^{\epsilon} \Pr[M(D') \in \mathcal{R}] + \delta$$

The privacy parameters $$\epsilon, \delta$$ can be interpreted as: $$\epsilon$$ upper bounds the privacy loss, and $$\delta$$ is the probability that this guarantee does not hold. We say that the mechanism $$M$$ is $$(\epsilon, \delta)$$-differentially private. In short, we can understand this as: the probability distribution of the output remains nearly unchanged whether an individual's data is included or excluded.

Composition of Privacy Budgets
======

If we have a mechanism $$M_1$$ that has a budget of $$\epsilon_1$$, and another mechanism $$M_2$$ that has budget $$\epsilon_2$$, the overall budget we need is at most $$\epsilon_1 + \epsilon_2$$. This occurs because the probabilities are multiplicative.

$$e^{\epsilon_1}*e^{\epsilon_2} = e^{\epsilon_1+\epsilon_2}$$

And it turns out this also follows for $$(\epsilon, \delta)$$-differentially privacy, i.e. the overall mechanism ($$M_1$$ followed by $$M_2$$) is $$(\epsilon_1+\epsilon_2, \delta_1+\delta_2)$$ differentially private.

This budget is a loose upper bound and with careful analysis we can prove tighter bounds.


Deep Learning with Differential Privacy (DP-SGD)
======

DP-SGD proposes a modification to stochastic gradient descent algorithm to make it differentially-private: i.e., differentially-private stochastic gradient descent (DP-SGD).

Intuitively, through DP-SGD we bound the amount of information the parameters have about the data. So no matter how many times we use the model parameters to produce outputs, we can't leak any more information than this bound.

The alternative would be to train the model normally and then add noise to its outputs. However, the privacy loss would be accumulated every time we queried the model, so you'd have to add noise proportional to the number of queries.
