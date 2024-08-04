---
layout: post
title: RA ch9 Model selection and validation
date: 2020-07-08 11:12:00-0400
description: Lecture note chapter 9 for regression analysis taught by Hyemin Gu in 2020
tags: statistics lecture_note tutorial
categories: teaching regression_analysis
---

# Ch 9: Model selection and validation

When we have $$p-1$$ predictor varaibles, we can construct $$2^{p-1}$$ different linear models by choosing the parameters to use. Complex models could reduce sum squared error $$SSE$$ significantly, but it may cause overfitting, lacking adaptability to unseen cases. Therefore, when we choose a model, we need to consider 2 conditions below at the same time.

- causing small error which can be estimated by $$SSE$$
- simple enough to perform well with new data

This chapter focuses on introducing several criteria to choose a good linear regression model. Some could be only used(or has proved) in linear regression, while others are used in general models.

## Outline

1. Criteria for model selection
   - coefficient of multiple determination, $$R_p^2$$
   - adjusted coefficient of multiple determination, $$R_{a,p}^2$$
   - Mallow's $$C_p$$
   - $$AIC_p$$ and $$BIC_p$$
   - Prediction sum of squares, $$PRESS_p$$
2. Model validation

---

## 1. Criteria for model selection

Criteria for model selection below a model with

- small $$SSE$$
- small number of parameters $$p$$.

### coefficient of multiple determination, $$R_p^2$$

$$R_p^2 = 1 - \frac{SSE_p}{SSTO}$$

Larger is better.
It can be used in general models.
drawback: always find the most complex model

### adjusted coefficient of multiple determination, $$R_{a,p}^2$$

$$R_{a,p}^2= 1 - \frac{SSE_p/(n-p)}{SSTO/(n-1)}$$

adjusted version of $$R^2$$
Larger is better.
It can be used in general models.

### Mallow's $$C_p$$

Consider the sum of square of model error to the mean response $$\sum_i (\hat{Y_i} - E(Y_i))^2$$. It could be divided into two components.

- $$\sum_i (\hat{Y_i} - E(\hat{Y_i}))^2 = \sum_i \sigma_i^2(\hat{Y_i})$$ : **random error** caused by random noise (cannot be handled by the model itself.)
- $$\sum_i (E(\hat{Y_i}) - E(Y_i))^2$$ : **bias** of the model

We have a criterion measure **$$\Gamma_p = \frac{1}{\sigma^2} \sum_{i=1}^n  (\hat{Y_i} - E(Y_i))^2 = \sum_i \sigma_i^2(\hat{Y_i}) + \sum_i (E(\hat{Y_i}) - E(Y_i))^2$$**. But there are some problems:

1. We are not aware of $$\sigma^2$$ in general.
2. We cannot obtain $$E(Y_i)$$.

Let us have the full model with $$P-1$$ predictor variables, and each model that we want to assess has $$p-1$$ predictor variables.

- To settle for 1, we use $$MSE_{full} = MSE(X_1, X_2, \cdots, X_{P-1})$$ ($$MSE$$ of the full model) rather than $$\sigma^2$$.
- To resolve 2, we use the formula $$E(SSE_p) = \sum_i (E(\hat{Y_i}) - E(Y_i))^2 + (n-p)\sigma^2$$. (You may prove this using the fact that $$Tr(Var(\hat{Y}) = Tr(\sigma^2H) = p\sigma^2$$.) <br>Therefore, $$\Gamma_p = \frac{1}{\sigma^2} [E(SSE_p) - (n-2p)\sigma^2 ]$$.
  > $$\because \Gamma_p \sigma^2 = \sum_i (E(\hat{Y_i}) - E(Y_i))^2 + (n-p)\sigma^2 - (n-p)\sigma^2 + \sum_i \sigma_i^2(\hat{Y_i})$$
  > Since $$\sigma_i^2(\hat{Y_i}) = p\sigma^2$$, $$\Gamma_p = E(SSE_p) - (n-2p)\sigma^2$$.

Now we substitute $$\Gamma_p = \frac{1}{\sigma^2} [E(SSE_p) - (n-2p)\sigma^2 ]$$ with
**$$C_p = \frac{SSE_p}{MSE_{full}} - (n-2p)$$**.

Note that when there is no bias in the model with $$p-1$$ predictor variables, then $$\Gamma_p = p$$.

> $$\because \frac{1}{\sigma^2}\sum_i \sigma^2(\hat{Y_i})^2 = \frac{1}{\sigma^2} p \sigma^2 = p$$.

By the way, $$C_p$$ (an estimator of $$\Gamma_p$$) becomes $$p$$ when it is the full model.

> $$\because \frac{SSE_p}{MSE_p} - (n-2p) = n-p - (n-2p) = p$$.

Therefore, Smaller $$C_p$$ near $$p$$ is better.
$$C_p$$ formula is unique for assessing regression model. For other models, you should analyze $$\Gamma_p$$ for their situation.

### $$AIC_p$$ and $$BIC_p$$

$$AIC_p = n log(SSE_p) - n log(n) + 2p$$
$$BIC_p = n log(SSE_p) - n log(n) + [log(n)]p$$ where $$[k]$$ stands for the largest integer which does not exceed $$k$$

Smaller is better.
It is a simple criterion.

<U>Note</U> $$BIC_p$$ is more sensitive to $$p$$ (penalize more to large $$p$$). To be exact, if $$n\geq 8$$, then $$AIC_p \leq BIC_p$$.

### Prediction sum of squares, $$PRESS_p$$

$$PRESS_p$$ doesn't penalize a model with many predictor variables. Instead, it directly calculate prediction error to unseen data.
$$PRESS_p = \sum_i (Y_i - \hat{Y_{i(i)}})^2$$
where $$\hat{Y_{i(i)}}$$ denotes $$i$$th fitted value using a fitted line constructed without $$(X_i, Y_i)$$ data.

Smaller is better.
It can be used in general models.
However if the number of predictior variables are large, the computation is heavy. Therefore, we don't go through all the candidate models, but use _stepwise selection method_.

**stepwise selection method**
Stepwise selection method is a greedy approach to solve an optimization problem. At each stage, it calculates criterion function values of all the states that could be reached in one step. It chooses a path to the best state for each step.

- It doesn't guarantee obtaining the global optimum.
- But it is the easiest approach to handle(computationally or make an algorithm to solve) optimization problems.
- It significantly reduces the computational load.
- And it gives a quite reasonable solution in a limited time.

Here, we could use forward/backward/both stepwise method which has a computational complexity of $$\omicron(p^2)$$.
Ex) forward method
We start from a model with largest T-value $$t^\ast = \frac{b_k}{s(b_k)}$$. Then add variable with largest $$PRESS_p$$. Repeat this adding process until there is no significant change.

<U>Remark</U> Generally, computing $$PRESS_p$$ is costly. However, when it comes to assessing a linear regression model, we have a good formula to compute this deleted residual $$Y_i - \hat{Y_{i(i)}}$$. It is going to be introduced in the next chapter.

## 2. Model validation

To find a model which performs well in prediction, we check a candidate model against independent data which is unseen, uncorrelated but from the same population. The steps are

1. divide a given dataset into 2 non-overlapping sets <br>training data : validation data = 7:3 or 6:4
2. make a model using training data $$(X_t, Y_t)$$ and obtain parameters $$\hat{\beta_t} = (X_t^tX_t)^{-1}X_t^tY_t$$
3. calculate the mean squared prediction error

$$MSPR = \frac{\sum_{i=1}^{n^\ast} (Y_{i,new}-\hat{Y_i})^2}{n^\ast}$$

where $$n^\ast$$ = number of validation data, and $$\hat{Y_i} = X_{i,new}^t\hat{\beta_t}$$.
For a properly trained model, $$MSPR > MSE$$. But if $$MSPR \gg MSE$$, the model is invalid (lack of prediction ability).

---

Here is the [jupyter notebook script](https://github.com/HyeminGu/Regression_R_tutorials/blob/main/Regression_5_Variable_Selection_in_Multiple_Regression.ipynb) to run several practice codes using R.
