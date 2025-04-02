---
title: 'Federated Learning'
date: 2025-04-02
permalink: /posts/2025/04/federated-learning/
tags:
  - Federated Learning
---

FedSGD
======

As a baseline, Federated Learning (FL) training algorithm is based on Stochastic Gradient Descent (SGD). SGD can be applied naively to the federated optimization problem, where a single batch gradient calculation is done per round of communications.

Definition of terms:
- $$w_t$$: Model weights on communication round $$t$$.
- $$w_t^k$$: Model weights on communication round $$t$$ on client $$k$$.
- $$C$$: Fraction of clients performing computations in each round.
- $$E$$: Number of training passes each client makes over its local dataset on each round.
- $$B$$: The local minibatch size used for client updates.
- $$\eta$$: Learning rate
- $$\mathcal{P}_k$$: Set of data points on client $$k$$.
- $$n_k$$: Number of data points on client $$k$$.
- $$f_i(w)$$ - Loss $$l(x_i,y_i;w)$$: loss on example $$(x_i,y_i)$$ with model parameters $$w$$.

For FedSGD, $$C = 1$$. This corresponds to a full-batch (non-stochastic) GD. For the current global model $$w_t$$, the average gradient on its global model is calculated for each client $$k$$.

