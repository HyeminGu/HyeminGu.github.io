---
layout: post
title: Lipschitz-Regularized Gradient Flows and Latent Generative Particles
date: 2024-10-21 17:39:00
description: This is a poster for SIAM Mathematics of Data Science 2024.
tags: machine_learning presentation
categories: generative_modeling gradient_flow particle_transport optimal_transport poseter machine_learning
---

**Abstract**
We developed a generative particle algorithm(GPA) that solves particle systems for Wasserstein gradient flows minimizing a regularized variant of f-divergences which are called Lipschitz regularized f-divergences. The Lipschitz regularized f-divergence is formulated as an f-divergence infimally convolved with Wasserstein-1 proximal, forming a robust framework. In our algorithm the f-divergence is estimated only using samples by solving its dual formulation in a space of Lipschitz continuous neural network functions. The optimizer function equals the first variation of the Lipschitz regularized f-divergence, and therefore its gradient produces a vector field for particle dynamics. Lipschitz regularization imposes a speed limit on the vector field and enhances stability of the dynamics. We also show that a specific selection of f enables stable generation of heavy-tailed data distributions. As a generative model, GPA excels in generating samples from scarce target data and is scalable to high-dimensional problems such as MNIST image generation. Since GPA offers the freedom to select the initial distribution, we show an application of GPA to gene expression data integration.

[View poster](/assets/pdf/siam_mds_2024-poster.pdf)
