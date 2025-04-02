---
title: 'Federated Learning Algorithms'
date: 2025-04-02
permalink: /posts/2025/04/federated-learning-algorithms/
tags:
  - Federated Learning
---

This blog introduces some basic federated learning algorithms.

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

$$F_k(w)=\frac{1}{n_k}\sum_{i \in \mathcal{P}_k} f_i(w)$$

$$g_k = \nabla F_k(w_t)$$

The central server then aggregates these gradients and applies the update.

$$w_{t+1} \leftarrow w_t - \eta \sum_{k=1}^{K} \frac{n_k}{n} g_k$$

FedAvg
======

Now let's make a small change to the update step above.

$$\forall k, \quad w_{t+1}^{k} \leftarrow w_t - \eta g_k$$

$$w_{t+1} \leftarrow \sum_{k=1}^{K} \frac{n_k}{n} w_{t+1}^{k}$$

Now, each client locally takes one step of GD on the current model using its local data, and the server then takes a weighted average of the resulting models. This way we can add more computation to each client by iterating the local update multiple times before averaging. In practice, major speedups are obtained when computation on each client is improved, once a minimum level of parallelism over clients is achieved.

The amount of computation is controlled by three parameters $$C$$, $$E$$, $$B$$. Setting $$B=\infty$$ and $$E=1$$ makes this the FedSGD algorithm.
