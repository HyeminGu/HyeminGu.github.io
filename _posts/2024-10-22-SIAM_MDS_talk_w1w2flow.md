---
layout: post
title: Wasserstein Proximals Stabilize Training of Generative Models and Learn Manifolds
date: 2024-10-22 09:30:00
description: This is a talk slide for SIAM Mathematics of Data Science 2024.
tags: machine_learning presentation
categories: generative_modeling gradient_flow particle_transport optimal_transport poseter machine_learning
---

**Abstract**
In this talk, I will delve into the crucial role of Wasserstein proximals in enhancing the training of generative models. When generative models learn data distributions, they typically encounter two primary challenges: training instability and effectively representing low dimensional manifolds in high dimensional spaces. By reformulating the learning losses of generators as Mean Field Game(MFG) problems, we show that traditional approaches like Normalizing Flows (NFs) and generative adversarial networks (GANs) are ill-posed. This inadequacy leads to training instability for NFs and GANs. However, advanced models that incorporate the Wasserstein-2 proximal through a running cost have proven to be effective at mitigating this issue. On the other hand, capturing low dimensional structure in high dimensional spaces is related to the numerical tractability of the terminal condition in the mean-field game. Unlike NFs, f-GANs address this challenge by introducing Wasserstein-1 proximal in the loss function. Wasserstein proximals offer a mathematical insight into generative model training techniques, and guide a more robust and efficient training approach for generator models. We demonstrate the use of Wasserstein proximal methods to stabilize the training of flow-based generative models.

[View poster](/assets/pdf/w1w2flow_presentation_split.pdf)
