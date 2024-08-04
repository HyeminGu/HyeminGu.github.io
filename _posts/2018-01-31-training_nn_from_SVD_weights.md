---
layout: post
title: Training a 2 layer Neural Network using SVD-generated weights
date: 2018-01-31 17:39:00
description: This is a poster for Joint Mathematics Meetings 2018.
tags: machine_learning presentation
categories: neural_network poseter machine_learning
---

**Abstract**
The objective of this study is to figure out a good initial weight for training a 2 layered neural network aimed at MNIST handwritten digit recognition. Conventionally, initial weights are set up with random values near zero. This made hard to understand where the weights converge. This study is going to introduce a deterministic weight initialization method based on the training dataset. By applying singular value decomposition on the training set, principal components are obtained. These principal components are going to be used for the first layer’s weight. Then we find the relevant weight for the second layer. At the end, the performance of 2 neural networks constructed by random weight initialization and the new pc weight initialization is going to be compared.

[View poster](/assets/pdf/jmm_2018-poster.pdf) 

