---
layout: post
title: RA ch1 Linear Regression with One Predictor Variable
date: 2020-06-30 11:12:00-0400
description: Lecture note chapter 1 for regression analysis taught by Hyemin Gu in 2020
tags: statistics lecture_note tutorial
categories: teaching regression_analysis
---

# Ch 1: Linear Regression with One Predictor Variable

## Outline

1. Simple Regression Model

   - Formulation by Least Square Estimation
   - Gauss-Markov theorem
   - Properties of linear regression model
   - Estimation of $$\sigma^2 = Var(E)$$

2. Normal Error Regression Model
   - Formulation by Maximum Likelihood Estimation
   - Advantages of Normal error regression model

---

## 1. Simple Regression Model

### Formulation by Least Square Estimation

Let $$Y$$ be dependent / response variable, and $$X$$ be independent / explanatory / predictor variable.
Given $$n$$ paired data $$(X_i, Y_i), i=1, \cdots, n$$,
we want to find a **linear function** $$f(x) = \beta_0 + \beta_1 x$$ s.t.

$$Y_i = \beta_0 + \beta_1 X_i + \epsilon_i, i=1, \cdots, n$$

where $$\epsilon_i$$ stands for the error between the function value $$f(X_i)$$ and the response $$Y_i$$, $$E(\epsilon_i)=0$$, $$Var(\epsilon_i)=\sigma^2$$, $$\epsilon_i \perp \epsilon_j$$ for $$i\neq j$$.

There are various ways to draw a line which crosses the data points $$(X_i, Y_i), i=1, \cdots, n$$. Among them, it is reasonable to select one with the **least sum of squared errors** $$\sum_i \epsilon_i^2$$.

Define a function $$Q$$ parametrized by $$\beta_0, \beta_1$$,

$$Q = Q(\beta_0, \beta_1) = \sum_i (Y_i - \beta_0 - \beta_1 X_i)^2 = \sum_i \epsilon_i^2$$

<U>Note</U>

- $$Q$$ is convex.
- Every convex function has a global minimum.
- $$Q$$ is differentiable over $$\beta_0, \beta_1$$.

By differentiating the function $$Q$$ over $$\beta_0, \beta_1$$, find a critical point $$(b_0, b_1)$$ by setting each partial derivative = 0.

$$\frac{\partial Q}{\partial \beta_0} = -2 \sum_i (Y_i - \beta_0 - \beta_1 X_i) = 0$$

$$\frac{\partial Q}{\partial \beta_1} = -2 \sum_i X_i (Y_i - \beta_0 - \beta_1 X_i) = 0$$

The solution for the above simultaneous equations is

$$b_0 = E(Y) - b_1 E(X)$$

$$b_1 = \frac{E[(X_i-E(X))(Y_i-E(Y))]}{\sum_i (X_i - E(X))^2} = \frac{Cov(X, Y)}{Var(X)}$$

> <U>Proof</U>
>
> 1. $$n \beta_0 = \sum_i (Y_i - \beta_1 X_i)$$
> 2. $$\sum_i X_i (Y_i - \beta_0 - \beta_1 X_i) = \sum_i (X_i - E(X))(Y_i - \beta_0 - \beta_1 X_i)$$
>    $$ = \sum_i (X_i - E(X))(Y_i - E(Y) + \beta_1 E(X) - \beta_1 X_i)$$

<U>Remark</U>

1. Once a dataset $$(X_i, Y_i), i=1, \cdots, n$$ is given, $$X_i$$s are known constants. Also, $$E(Y_i) = \beta_0 + \beta_1 X_i$$s are considered as constants.
2. The error term $$\epsilon_i$$ is a random variable.
3. $$Y_i$$ is the sum of the constant $$\beta_0 + \beta_1 X_i$$ and random $$\epsilon_i$$. Therefore, $$Y_i$$ is also a random variable.
4. Since $$E(\epsilon_i)=0$$, </br>$$E(Y_i)=E(\beta_0 + \beta_1 X_i + \epsilon_i) = \beta_0 + \beta_1 X_i$$, and </br>$$Var(Y_i) = Var(\epsilon_i)=\sigma^2$$.

### Gauss Markov theorem

<U>Statement</U>
Under the regression model, the least square estimators of regression coefficients $$b_0, b_1$$ are

1. unbiased (i.e. $$E(b_0)=\beta_0, E(b_1)=\beta_1$$) and
2. having minimum variance among all unbiased linear estimators. (i.e. $$Var(b_i) \leq Var(b_i^*), i=0, 1$$, $$b_i^*$$ unbiased, linear)

Shortly, it is said that "$$b_0, b_1$$ are BLUE(best linear unbiased estimator) of $$\beta_0, \beta_1$$, respectively.

<U>Proof</U> go to [link](https://drive.google.com/file/d/19612eTUYLQTYB2lD9_atC_nFeF5wQXqL/view?usp=sharing)

### Properties of linear regression model

<U>Notations</U>
Observation : $$Y = \beta_0 + \beta_1 X + \epsilon$$
Real line : $$E(Y) = \beta_0 + \beta_1 X$$ (unknown)
Fitted line : $$\hat{Y} = b_0 + b_1 X$$ (known)

residual : $$e_i = Y - \hat{Y}$$ (known)
error : $$\epsilon_i = Y - E(Y)$$ (unknown)

1. $$\sum_i e_i = 0$$
   > $$\because \sum_i (Y_i - \hat{Y_i}) = \sum_i (Y_i - b_0 - b_1 X_i) = 0$$ by the choice of $$b_0, b_1$$
2. $$\sum_i e_i^2$$ is the minimum
3. $$\sum_i Y_i = \sum_i \hat{Y_i}$$
4. $$\sum_i X_i e_i = 0$$ (residual $$e$$ is orthogonal to $$X$$)
   > $$\because \sum_i X_i e_i = \sum_i (X_i - \bar{X}) e_i = \sum_i (X_i - \bar{X}) (Y_i - (\bar{Y} + b_1 (X_i - \bar{X}) ))$$ > $$= \sum_i (X_i - \bar{X}) (Y_i - \bar{Y}) - b_1 \sum_i (X_i - \bar{X})^2$$ > $$= \sum_i (X_i - \bar{X}) (Y_i - \bar{Y}) - \frac{\sum_i (X_i - \bar{X}) (Y_i - \bar{Y})}{\sum_i (X_i - \bar{X})^2} \sum_i (X_i - \bar{X})^2 = 0$$
5. $$\sum_i \hat{Y_i}e_i = 0$$ (residual $$e$$ is orthogonal to the fitted line $$\hat{Y}$$)
6. $$\hat{Y_i} = b_0 + b_1 X_i$$ (regression line passes through $$(\bar{X},\bar{Y})$$)
   > $$\because \hat{Y_i} = \bar{Y} + b_1(X_i - \bar{X})$$

### Estimation of $$\sigma^2 = Var(E)$$

$$e_i = Y_i - \hat{Y_i}$$
Define $$SSE$$ (Sum of Squared Error) $$= \sum_i (Y_i -  \hat{Y_i})^2 = \sum_i e_i^2$$
$$s^2 = MSE$$ (Mean Square Error) $$= \frac{SSE}{n-2} = \sum_i \frac{(Y_i -  \hat{Y_i})^2}{n-2} = \sum_i \frac{e_i^2}{n-2}$$ ($$n-2$$ is the **degree of freedom, df** of the model)

<U>Observation</U>

- $$E(MSE) = \sigma^2$$ ($$s^2$$ is an unbiased estimator of $$\sigma^2$$)
- $$Var(\epsilon_i) = \frac{\sum_i \epsilon_i^2}{n}$$

## 2. Normal Error Regression Model

### Formulation by Maximum Likelihood Estimation

Assuming a normal distribution to the error terms $$\epsilon_i$$, we can estimate $$Var(\epsilon_i) = \sigma^2$$ as well as $$\beta_0, \beta_1$$.

Now the formulation is given as
$$Y_i = \beta_0 + \beta_1 X_i + \epsilon_i$$
where $$\epsilon_i \sim N(0, \sigma^2), \epsilon_i \perp \epsilon_j$$ for $$i \neq j$$, (pdf of $$\epsilon_i$$) $$= \frac{1}{\sqrt{2\pi}\sigma} exp \left(-\frac{\epsilon_i^2}{2 \sigma^2}\right)$$

We estimate $$\beta_0, \beta_1$$ and $$\sigma^2$$ from **Maximum Likelihood Estimation**.
Since $$E(Y_i) = \beta_0 + \beta_1 X_i$$ and $$Var(Y_i) = \sigma^2$$,
pdf of $$Y_i$$ is given as $$f_i = \frac{1}{\sqrt{2\pi}\sigma} exp \left(-\frac{(Y_i - \beta_0 - \beta_1 X_i)^2}{2 \sigma^2}\right)$$.

Using the i.i.d. condition of variables $$Y_i$$ and $$Y_j$$, the **likelihood function, $$L$$** is given as

$$L(\beta_0, \beta_1, \sigma^2) = \Pi_i f_i = \frac{1}{(\sqrt{2\pi}\sigma)^n} exp(-\sum_i \frac{(Y_i - \beta_0 - \beta_1 X_i)^2}{2 \sigma^2})$$

We maximize $$L$$ or $$log L$$ by calcuating the critical point.
Then the estimators obtained by maximizing likelihood are given as

$$\hat{\beta_0} = b_0 = \bar{Y} - b_1 \bar{X}$$

$$\hat{\beta_1} = b_1 = \frac{\sum_i (X_i-\bar{X})(Y_i - \bar{Y})}{\sum_i (X_i-\bar{X})^2}$$

(same as LSE)

$$\hat{\sigma^2} = \frac{\sum_i (Y_i - \hat{\beta_0} - \hat{\beta_1} X_i)^2}{n} = \frac{\sum_i (Y_i - \hat{Y_i})^2}{n}$$

cf) $$MSE = s^2 = \frac{\sum_i (Y_i - \hat{Y_i})^2}{n-2}$$ is an unbiased estimator of $$\sigma^2$$.
$$\hat{\sigma^2}$$ is not an unbiased estimator of $$\sigma^2$$.

### Advantages of Normal error regression model

By introducing normal distribution on the error $$\epsilon_i$$, we could obtain an estimator of $$\sigma^2$$. Also, in the following chapter, we could find out this normality condition enables to calculate confidence intervals to several variables in the linear regression model.

---

Here is the [jupyter notebook script](https://github.com/HyeminGu/Regression_R_tutorials/blob/main/Regression_1_Simple_Linear_Regression.ipynb) to run several practice codes using R.
