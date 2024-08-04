---
layout: post
title: Data-dependent Kernel Support Vector Machine classifiers in Reproducing Kernel Hilbert Space
date: 2021-05-30 17:39:00
description: This is a 2021 Spring Project paper for the ST - Math Foundations of Probabilistic Artificial Intelligence II class.
tags: machine_learning presentation
categories: machine_learning class_project
---

**Abstract**
Support Vector Machine (SVM) provides a linear classifier for binary classification problems. Complex decision boundaries in the input feature space are handled by nonlinear kernels to the SVM. Theories in Reproducing Kernel Hilbert Spaces (RKHS) state that, given a kernel $$\mathcal{K}$$ and a set of $$M$$ given data $$(x_i,y_i)$$, for $$i=1,\cdots,M$$, a SVM classifier function can be written as $$f(x) =\alpha_0 + \sum_{i=1}^M \alpha_i \mathcal{K}(x, x_i)$$ for some coefficients $$\alpha_i$$s. Also, applying conformal transforms to a positive definite kernel  produces another positive definite kernel which are in more complexity. Hence, in case that well-known kernels fail given the current training data, a new kernel can be tried by optimizing the coefficients of a conformal kernel in the way to maximize the ratio "(Between-class error)/(Within-class error)" of the training data. Here, data-dependent kernel SVM is applied to an application of classifying tumor/tumor-free organs from gene expression data and compared its classification performance with other well-known kernels.

[View file](../../../assets/pdf/project_paper_math_found_of_ai.pdf) 
