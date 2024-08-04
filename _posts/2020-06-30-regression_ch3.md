---
layout: post
title: RA ch3 Inferences in Regression and Correlation Analysis
date: 2020-07-02 11:12:00-0400
description: Lecture note chapter 3 for regression analysis taught by Hyemin Gu in 2020
tags: statistics lecture_note tutorial
categories: teaching regression_analysis
---

# Ch 3: Inferences in Regression and Correlation Analysis

In Ch 1, **normal error regression model** ($$Y_i = \beta_0 + \beta_1 X_i + \epsilon_i$$ where $$\epsilon_i \sim N(0, \sigma^2), \epsilon_i \perp \epsilon_j$$ for $$i \neq j$$) is introduced by adding an assumption that each error term follows normal distribution.

From a good property of normal distribution (_Summation of random variables also follows normal distribution where each of them follows normal distribution._ ), we could notice that the response $$Y_i$$, and coefficients $$\beta_0$$, $$\beta_1$$ follow normal distribution. This allows statistical tests for these random variables.

## Outline

1. Inference of variables of interest
   - inference of $$\beta_1$$
   - inference of $$\beta_0$$
   - interval estimation of $$\hat{Y_h} = b_0 + b_1 X_h$$
   - prediction of $$Y_{h,new} = \beta_0 + \beta_1 X_h + \epsilon_{h,new}$$
2. ANOVA apporach to regression
   - ANOVA table
   - F-test
   - measure of linear association

---

## 1. Inference of variables of interest

From now on, we assume that all the linear regression model below refer to normal error regresion model.

### inference of $$\beta_1$$

To see if $$Y$$ is linear to $$X$$, apply a test if the slope of the regression line is zero or not.
$$H_0: \beta_1=0$$, $$H_1: \beta_1 \neq 0$$
estimator of $$\beta_1$$:

$$b_1 = \frac{\sum_i (X_i-\bar{X})(Y_i-\bar{Y})}{\sum_i (X_i-\bar{X})^2}$$

where $$E(b_1) = \beta_1$$, and $$\sigma^2(b_1) = Var(b_1) = \frac{\sigma^2}{\sum (X_i -\bar{X})^2}$$

> <U>Proof</U> > $$b_1$$ is an unbiased estimator of $$\beta_1$$.
> We use the fact that $$\beta_1$$ is linear to $$Y_i$$'s.
> $$b_1 = \sum_i c_i Y_i$$, where $$c_i = \frac{X_i - \bar{X}}{\sum_i (X_i - \bar{X})^2}$$.
> Since $$Y_i$$'s are independent to each other,
> $$\sigma^2(b_1) = \sum_i c_i^2 Var(Y_i) = \sigma^2 \sum_i c_i^2 = \sigma^2 \sum_i [\frac{X_i - \bar{X}}{\sum_i (X_i - \bar{X})^2}]^2 = \frac{\sigma^2}{\sum_i (X_i - \bar{X})^2}$$

Therefore, it is derived that **$$b_1 \sim N(\beta_1, \frac{\sigma^2}{\sum (X_i - \bar{X})^2})$$** under the normal error regression model.
Here, $$\sigma^2$$ is typically unknown, and so it is estimated by $$s^2 = MSE = SSE/(n-2)$$. We write $$s^2(b_1) = \frac{s^2}{\sum (X_i - \bar{X})^2}$$.
Recall that $$\frac{(n-2)s^2}{\sigma^2} \sim \chi^2(n-2)$$. This implies that

$$\frac{b_1 - \beta_1}{s(b_1)} \sim t(n-2)$$

**$$1-\alpha$$ confidence interval for $$\beta_1$$**
$$b_1 \pm s(b_1) t(1-\alpha/2, n-2)$$

**2-sided test**
test statistic $$t^\ast = \frac{b_1-0}{s(b_1)}$$
If $$\mid t^\ast\mid \leq t(1-\alpha/2, n-2)$$, conclude $$H_0$$, otherwise, $$H_1$$.

### inference of $$\beta_0$$

We can also check if the intercept of the regression line is zero or not.
$$H_0: \beta_0=0$$, $$H_1: \beta_0 \neq 0$$
estimator of $$\beta_0$$: $$$$b_0 = \bar{Y} - b_1 \bar{X}$$$$
where $$E(b_0) = \beta_0$$, and $$\sigma^2(b_0) = Var(b_0) = \sigma^2[\frac{1}{n} + \frac{\bar{X}^2}{\sum (X_i -\bar{X})^2}]$$

> <U>Proof</U> > $$b_0$$ is an unbiased estimator of $$\beta_0$$.
>
> We use the fact that $$\beta_0$$ is linear to $$Y_i$$'s.
> $$b_0 = \sum_i d_i Y_i$$, where $$d_i = \frac{1}{n} - c_i \bar{X}$$, $$c_i = \frac{X_i - \bar{X}}{\sum_i (X_i - \bar{X})^2}$$.
> Similar to the case of $$\sigma^2(b_1)$$,
> $$\sigma^2(b_0) = \sigma^2 \sum_i d_i^2 = \sigma^2 \sum_i [\frac{1}{n} - c_i \bar{X}]^2 = \sigma^2 [\frac{1}{n} + \frac{\bar{X}^2}{\sum_i (X_i - \bar{X})^2}]$$

Therefore, it is derived that **$$b_0 \sim N\left(\beta_0, \sigma^2[\frac{1}{n} + \frac{\bar{X}^2}{\sum (X_i -\bar{X})^2}]\right)$$** under the normal error regression model.
Here, we substitue $$\sigma^2$$ by $$MSE$$ and write $$s^2(b_0) = s^2[\frac{1}{n} + \frac{\bar{X}^2}{\sum (X_i -\bar{X})^2}]$$.
Recall that $$\frac{(n-2)s^2}{\sigma^2} \sim \chi^2(n-2)$$. This implies that $$$$\frac{b_0 - \beta_0}{s(b_0)} \sim t(n-2)$$$$

**$$1-\alpha$$ confidence interval for $$\beta_0$$**
$$b_0 \pm s(b_0) t(1-\alpha/2, n-2)$$

**2-sided test**
test statistic $$t^\ast = \frac{b_0 - 0}{s(b_0)}$$
If $$\mid t^\ast\mid \leq t(1-\alpha/2, n-2)$$, conclude $$H_0$$, otherwise, $$H_1$$.

### interval estimation of $$\hat{Y_h} = b_0 + b_1 X_h$$

Here, we have a known level $$X_h$$, and the goal is to estimate the mean response $$\hat{Y_h}$$.

We have $$E(\hat{Y_h}) = E(Y_h) = \beta_0 + \beta_1 X_h$$, and $$\sigma^2(\hat{Y_h}) = \sigma^2 [\frac{1}{n} + \frac{(X_h - \bar{X})^2}{\sum_i (X_i - \bar{X})^2} ]$$.

> <U>Proof</U> > $$\sigma^2(\hat{Y_h}) = \sigma^2(b_0 + b_1 X_h) = \sigma^2 (\bar{Y} - b_1 (X_h - \bar{X}))$$
> Since $$\bar{Y} \perp b_1$$,
> $$\sigma^2 (\bar{Y} - b_1 (X_h - \bar{X})) = \sigma^2 (\bar{Y}) + \sigma^2(b_1 (X_h-\bar{X}))$$ > $$= \frac{\sigma^2}{n} + \frac{\sigma^2}{\sum_i (X_i - \bar{X})^2}(X_h - \bar{X})^2 = \sigma^2 [\frac{1}{n} + \frac{(X_h - \bar{X})^2}{\sum_i (X_i - \bar{X})^2}]$$

<U>Note</U> The variance of $$\hat{Y_h}$$ increases if $$X_h$$ is far from $$\bar{X}$$.

We conclude that **$$\hat{Y_h} \sim N\left(\beta_0 + \beta_1 X_h, [\frac{1}{n} + \frac{(X_h - \bar{X})^2}{\sum_i (X_i - \bar{X})^2} ]\right)$$**.
Confidence interval and stastistical test follows.

### prediction of $$Y_{h,new} = \beta_0 + \beta_1 X_h + \epsilon_{h,new}$$

Here, we have an unknown data $$(X_h, Y_{h,new})$$, which is expected to be came out from the regression model. The goal is to predict the confidence interval for the new data $$(X_h, Y_{h,new})$$. The new data could be written as $$Y_{h,new} = \beta_0 + \beta_1 X_h + \epsilon_{h,new}$$ where $$\epsilon_{h,new} \sim N(0, \sigma^2)$$.

**When the parameters $$(\beta_0, \beta_1, \sigma^2)$$ are known**
we can obtain the mean $$E(Y_{h,new})$$. This makes it easy to find out $$Y_{h,new} \sim N(E(Y_{h,new}), \sigma^2)$$. The confidence interval is given as **$$E(Y_{h,new}) \pm z(1-\alpha/2)\sigma$$**.

**When the parameters are unknown**
we cannot access the mean $$E(Y_{h,new})$$, and use the regression function value $$\hat{Y_{h,new}}$$ as an alternative. Also, we cannot be certain of the location of the distribution of $$Y$$. The prediction limits for $$Y_{h,new}$$ in this case must take account of two elements,

1. variation in possible location of the distribution of $$Y$$
2. variation within the probability distribution of $$Y$$.

<U>Note</U> $$s^2(pred) = MSE + s^2(\hat{Y_{h,new}})$$

Confidence interval and stastistical test follows.

## 2. ANOVA apporach to regression

Once a regression line $$\hat{Y}$$ is obtained, we have the formula:
$$$$\sum_i(Y_i - \bar{Y})^2 = \sum_i(Y_i - \hat{Y_i})^2 + \sum_i(\hat{Y_i} - \bar{Y})^2$$$$

<U>Notation</U>

- Sum of Square TOtal $$SSTO = \sum_i(Y_i - \bar{Y})^2$$ : <br>$$\ell_2$$ or Euclidean distance between each response $$Y_i$$ and the sample mean $$\bar{Y}$$, 평균값과의 차이
- Sum of Squared Error $$SSE = \sum_i(Y_i - \hat{Y_i})^2$$ : <br>$$\ell_2$$ distance between the response $$Y_i$$ and the regression line $$\hat{Y_i}$$, regression curve와의 차이/regression curve로 설명되지 않는 부분
- Sum of Square Regression $$SSR = \sum_i(\hat{Y_i} - \bar{Y})^2$$ :<br>평균값 fitting 대비 regression line fitting이 얻은 설명력<br>cf) $$SSR = b_1^2 \sum_i(\hat{X_i} - \bar{X})^2$$

<U>Note</U> $$Y - \hat{Y} \perp \hat{Y} - \bar{Y}$$

### ANOVA table

|     | SS                                | df      | MS            | E(MS)                                         |
| --- | --------------------------------- | ------- | ------------- | --------------------------------------------- |
| R   | $$\sum_i(\hat{Y_i} - \bar{Y})^2$$ | 1       | $$SSR$$       | $$\sigma^2 + \beta_1^2\sum_i(X_i-\bar{X})^2$$ |
| E   | $$\sum_i(Y_i - \hat{Y_i})^2$$     | $$n-2$$ | $$SSR/(n-2)$$ | $$\sigma^2$$                                  |
| TO  | $$\sum_i(Y_i - \bar{Y})^2$$       | $$n-1$$ |               |                                               |

### F-test

We've seen applying T-test to see if there is a linear relationship between $$X$$ and $$Y$$. There is another way using F-test.

$$H_0: \beta_1=0$$, $$H_1: \beta_1 \neq 0$$
test statistic: $$F^\ast = \frac{MSR}{MSE} = \frac{SSR/1}{SSE/(n-2)} \sim F(1, n-2)$$
If $$F^\ast \leq F(1-\alpha, 1, n-2)$$, conclude $$H_0$$, otherwise, conclude $$H_1$$.

<U>Note</U>

- F-test is one-tailed.
- $$F^\ast = \frac{SSR/1}{SSE/(n-2)} = \frac{b_1^2 \sum_i(X_i -\bar{X})^2}{MSE}$$ <br>Recall that $$s^2(b_1) = \frac{MSE}{\sum_i(X_i-\bar{X})^2}$$ <br>$$\therefore F^\ast = \left(T^\ast\right)^2$$

### measure of linear association

We introduce one more approach to confirm the linearity.

**coefficient of determination (결정계수)**
$$R^2 = \frac{SSR}{SSTO} = 1- \frac{SSE}{SSTO}$$, $$0\leq R^2 \leq 1$$
If $$R^2 \approx 1$$, we can say there is a strong linear relationship between $$X$$ and $$Y$$.
cf) Coefficient of correlation $$r$$ (상관계수) has the relationship $$r^2 = R^2$$. The difference is $$r$$ has a sign. This could be calculated.

However, the population correlation coefficient remains unknown. Therefore it is estimated by $$r$$. In a normal correlation model,
MLE of $$\rho_{xy}$$ : $$r_{xy} = \frac{\sum_i (X_i-\bar{X})(Y_i-\bar{Y})}{\sqrt{\sum_i(X_i-\bar{X})^2 \sum_j (Y_j-\bar{Y})^j}}$$

$$H_0 : \rho_{xy} = 0$$
test statistic: $$t^\ast = \frac{r}{\sqrt{1-r^2}} sqrt{n-2}$$

If $$\mid t^\ast\mid \leq t(1-\alpha/2, n-2)$$, conclude $$H_0$$, otherwise, $$H_1$$.

---

Once we construct a model, we should make sure that it is valid. We've seen methods from statistical inference up to now. But there are more intuitive ways using visual plots. Next time, we will find which plots are useful to check the validity of a model.

---

Here are the jupyter notebook scripts [verification of linear model ($$R^2$$, inference on variables)](https://github.com/HyeminGu/Regression_R_tutorials/blob/main/Regression_2_Verification_of_Linear_Regression.ipynb) and [prediction](https://github.com/HyeminGu/Regression_R_tutorials/blob/main/Regression_4_Prediciton.ipynb) to run several practice codes using R.
