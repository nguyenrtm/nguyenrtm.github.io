---
title: 'Differential Privacy'
date: 2025-04-09
permalink: /posts/2025/04/differential-privacy/
tags:
  - Differential Privacy
---

This blog introduces Differential Privacy.

Differential Privacy (DP) is a strong privacy notion that upper bounds the amount of influence an individual in a private dataset has on the output of an algorithm. In the context of machine learning, this means reducing memorization of each individual and forcing the model to learn features that are shared amongst the population.

Definition
======
Let $$\epsilon > 0$$ and $$\delta \in [0,1]$$. A randomized algorithm $$A : \mathcal{D} \rightarrow \mathcal{R}$$ satisfies $$(\epsilon, \delta)$$-DP if for any pair of adjacent datasets $$D, D' \in \mathcal{D}$$ that differ exactly in a single data sample, and for all sets $$\mathcal{R} \subseteq \mathcal{R}$$ it holds that

$$\Pr[A(D) \in \mathcal{R}] \leq e^{\epsilon} \Pr[A(D') \in \mathcal{R}] + \delta$$

The privacy parmeters $$\epsilon, \delta$$ can be interpreted as: $$\epsilon$$ upper bounds the privacy loss, and $$\delta$$ is the probability that this guarantee does not hold.
