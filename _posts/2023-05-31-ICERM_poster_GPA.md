---
layout: post
title: Lipschitz Regularized Gradient Flows and Latent Generative Particles
date: 2023-05-31 17:39:00
description: This is a poster for Optimal Transport in Data Science - ICERM 2023.
tags: machine_learning presentation
categories: generative_modeling gradient_flow particle_transport optimal_transport poseter machine_learning
---

**Abstract**
We constructed gradient flows which minimize Lipschitz regularized f-divergences which are written in variational formulation. Variational formulation enables to approximate a function of likelihood ratio dP/dQ between two empirical distributions obtained from samples. In case of KL-divergence, this function is the log likelihood ratio. We allow flexibility in choosing f depending on the probability distribution to learn, so that heavy-tailed distributions can be fitted using alpha divergences, instead of the KL divergence. On the other hand, Lipschitz regularization leads to the f-divergences bounded even between non-absolutely continuous distributions.
In terms of the transport equation of probability distributions in the Wasserstein space, the gradient flow evolves the empirical distribution in direction of the gradients of the function of likelihood ratio that are learned from data. This function is parametrized by neural networks, and its gradients give us the particle dynamics. Hence we transport the particles through the ODEs and generate more samples from the particles trajectory.
Moreover, in order to reduce the dimensions, we developed our particle transportation algorithm in latent spaces and applied to high dimensional problems such as image generation and gene expression data merging.

[View poster](/assets/pdf/icerm_2023_poster_hyemin.pdf)
