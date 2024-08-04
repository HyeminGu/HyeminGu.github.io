---
layout: post
title: RA ch4 Diagnostics and Remedial Measures
date: 2020-07-03 11:12:00-0400
description: Lecture note chapter 4 for regression analysis taught by Hyemin Gu in 2020
tags: statistics lecture_note
categories: teaching regression_analysis
---

# Ch 4: Diagnostics and Remedial Measures

**Checklist to see if the linear model is appropriate**

1. linearity
2. homogeneity (constant variance)
3. independency
4. normality
5. outliers
6. omission of other predictor variables

We can observe above properties from visual methods. Now, we are going to find which plots are relevant to check these properties. Moreover, we learn how could we revise the components in a model when there is some disparity between the real data and the requirements.

<U>Notation</U>

- residual $$e_i=Y_i - \hat{Y_i}$$
- mean of residuals $$\bar{e} = \frac{\sum_i e_i}{n} = 0$$
- variance of residualss $$s^2 = \frac{\sum_i e_i^2}{n-2} = \frac{SSE}{n-2} = MSE$$
- semi-studentized residual $$e_i^\ast = \frac{e_i-\bar{e}}{\sqrt{MSE}} = \frac{e_i}{\sqrt{MSE}}$$

## Outline

1. Graphical diagnostics
   - linearity
   - homogeneity
   - independency
   - normality
   - outliers
   - omission of other important predictors
2. Transformation of variables
   - Case 1: constant variance, but not-normal
   - Case 2: nonconstant variance and not-normal

---

## 1. Graphical diagnostics

First, we identify useful plots.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/regression/useful_plots.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
useful plots for diagnostics
</div>

### linearity

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/regression/linearity.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
linearity
</div>
You can see a certain pattern. So, nonlinear!

### homogeneity

The errors should have the constant variance. i.e. $$\sigma^2(\epsilon_i) = const$$.
But if it isn't, then you can also see the nonhomogeneous residuals.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/regression/homogeneity.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
homogeneity
</div>

### independency

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/regression/independency.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
independency
</div>
If $$corr(e_i,e_j) \neq 0$$, then we can sse some systematic patterns.

### normality

You can check for the distribution by plotting a box plot, histogram, or Stem-and-Leaf plot. Or you can draw a **normal Probability Plot**.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/regression/normality.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
normality
</div>

### outliers

You can draw a **semi-standardized residual plot** to figure out outliers.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/regression/outlier.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
outlier
</div>

### omission of other important predictors

If some important predictors are omitted, the residuals may not be close to 0.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/regression/omission_of_predictor_variables.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
omission of predictor variables
</div>

## 2. Transformation of variables

The basic idea is to linearize the variables by seeking the behavior of the error term.

### Case 1: constant variance, but not-normal

Transform $$X$$. Define a new variable as $$X^\prime = f(X)$$ where $$f(\cdot)$$ is a nonlinear function of $$X$$, which could linearize the response $$Y$$. Then use $$X^\prime$$ instead of $$X$$ in the linear model.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/regression/transformX.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
transform X
</div>

### Case 2: nonconstant variance and not-normal

Transform $$Y$$. Define a new variable as $$Y^\prime = g(Y)$$ where $$g(\cdot)$$ is a nonlinear function of $$Y$$, which could linearize the response $$Y^\prime = f(X)$$. Then use $$Y\prime$$ instead of $$Y$$ in the linear model. Transformation of $$Y$$ modifies the variance of the responses, therefore right transformation could enable the data to have homogeneity.

Cf) Box-Cox transformation
Transform $$Y$$ by $$Y^\prime = Y^\lambda$$ and identify the optimal $$\lambda \in \mathbb{R}$$ by MLE or Least squares.
