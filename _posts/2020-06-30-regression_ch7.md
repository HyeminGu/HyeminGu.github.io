---
layout: post
title: RA ch7 Multiple Regression 2
date: 2020-07-06 11:12:00-0400
description: Lecture note chapter 7 for regression analysis taught by Hyemin Gu in 2020
tags: statistics lecture_note
categories: teaching regression_analysis
---

# Ch 7: Multiple Regression 2

In Ch 6, we've seen linear regression model with multiple variables. To resolve the limitation for testing regression coefficients, we introduce a new concept, **extra sum of squares**.

## Outline

1. Extra sum of squares
   - definition
   - application 1 : Tests
   - application 2 : coefficient of partial determination
2. Standardized multiple regression model
   - correlation transformation and standardized regression model
   - multicollinearity issue

---

## 1. Extra sum of squares

### definition

<U>Recall</U>

- $$SSTO$$ can be divided into $$SSE$$ and $$SSR$$.
- When we add prediction variables to the regression model, $$SSE$$ gets decreased, while $$SSR$$ gets increased.

Using the above concept, define **extra sum of squares**

$$SSR(X_2 \mid X_1) = SSE(X_1) - SSE(X_1, X_2)$$,

the marginal explanation ability by adding $$X_2$$ into the model containing $$X_1$$. $$SSR(X_2 \mid X_1) = SSR(X_1, X_2) - SSR(X_1)$$ results in the same value..

### application : Tests

**Test whether a single $$\beta_k=0$$**

$$H_0: \beta_3 = 0$$

Full model) $$Y_i = \beta_0 + \beta_1 X_{i1} + \beta_2 X_{i2} + \beta_3 X_{i3} + \epsilon_i$$

Reduced model) $$Y_i = \beta_0 + \beta_1 X_{i1} + \beta_2 X_{i2} + \epsilon_i^\ast$$

test statistic:
$$\frac{(SSE(R)-SSE(F))/(df_f - df_r)}{SSE(F)/df_f}$$<br> $$ = \frac{(SSE(X_1,X_2)-SSE(X_1,X_2,X_3))/(n-3 - (n-4))}{SSE(X_1,X_2,X_3)/(n-4)} = \frac{SSR(X_3|X_1,X_2)/1}{SSE(X_1,X_2,X_3)/(n-4)} = \frac{MSR(X_3|X_1,X_2)}{MSE(X_1,X_2,X_3)} \sim F(1,n-4)$$

**Test whether several $$\beta_k=0$$**

$$H_0: \beta_2 = \beta_3 = 0$$

Full model) $$Y_i = \beta_0 + \beta_1 X_{i1} + \beta_2 X_{i2} + \beta_3 X_{i3} + \epsilon_i$$

Reduced model) $$Y_i = \beta_0 + \beta_1 X_{i1} + \epsilon_i^\ast$$

test statistic:
$$\frac{(SSE(X_1)-SSE(X_1,X_2,X_3))/(n-2 - (n-4))}{SSE(X_1,X_2,X_3)/(n-4)}$$<br>
$$ = \frac{SSR(X_2, X_3|X_1)/2}{SSE(X_1,X_2,X_3)/(n-4)} \newline = \frac{MSR(X_2,X_3|X_1)}{MSE(X_1,X_2,X_3)} \sim F(2,n-4)$$

**Test whether the slopes of $$x_k$$ and $$x_l$$ are the same**

$$H_0: \beta_2 = \beta_3 = \beta_c$$

Full model) $$Y_i = \beta_0 + \beta_1 X_{i1} + \beta_2 X_{i2} + \beta_3 X_{i3} + \epsilon_i^\ast$$

Reduced model) $$Y_i = \beta_0 + \beta_c (X_{i1} + X_{i2}) + \beta_3 X_{i3} + \epsilon_i$$
Consider $$X_{i1} + X_{i2}$$ as a new variable.

test statistic:
$$\frac{SSR(X_1+X_2|X_3)/1}{SSE(X_1,X_2,X_3)/(n-4)} \newline = \frac{MSR(X_1+X_2|X_3)}{MSE(X_1,X_2,X_3)} \sim F(1,n-4)$$

### application 2 : coefficient of partial determination

We can also calculate $$R^2$$ which accounts for marginal contribution of $$X_2$$ given that $$X_1$$ is in the model.
$$R_{2|1}^2 = \frac{SSR(X_2|/X_1)}{SSE(X_1)}$$
$$0 \leq R_{2|1}^2 \leq 1$$ and large value implies large contribution.

## 2. Standardized multiple regression model

When the predictor variables are not scaled properly, it leads to $$det(X^tX) \approx 0$$, which means there is multicollinearity between predictor variables. There is a cure for this problem.

### correlation transformation and standardized regression model

**correlation transform**
$$n$$ : number of observations
We use standardized variables $$\frac{Y-\bar{Y}}{s_Y}$$ and $$\frac{X_{ik}-\bar{X_k}}{s_{X_k}}$$.

When we use $$Y_i^\ast$$ and $$X_{ik}^\ast$$ as simple functions of $$\frac{Y-\bar{Y}}{s_Y}$$ and $$\frac{X_{ik}-\bar{X_k}}{s_{X_k}}$$, respectively,
$$Y_i^\ast = \frac{1}{\sqrt{n-1}} \frac{Y_i-\bar{Y}}{s_Y} = \frac{Y_i-\bar{Y}}{\sqrt{\sum_i (Y_i -\bar{Y})^2}}$$ where $$s_Y^2 = \frac{\sum_i (Y_i -\bar{Y})^2}{n-1}$$
$$Y_{ik}^\ast = \frac{1}{\sqrt{n-1}} \frac{X_{ik}-\bar{X_k}}{s_{X_k}} = \frac{X_{ik}-\bar{X_k}}{\sqrt{\sum_i (X_{ik} -\bar{X_k})^2}}$$ where $${s_{X_k}}^2 = \frac{\sum_i (X_{ik} -\bar{X_k})^2}{n-1}$$

**standardized regression model**
$$Y_i^\ast = \beta_1^\ast X_{i1}^\ast + \cdots + \beta_{p-1}^\ast X_{i,p-1}^\ast + \epsilon_i^\ast$$

<U>Note</U>

- $$\beta_0^\ast = 0$$
- $$\beta_0 = \bar{Y} - \beta_1 \bar{X_1} - \cdots - \beta_{p-1} \bar{X_{p-1}}$$
- $$\beta_k = \frac{s_Y}{s_{X_k}} \beta_k^\ast, k=1,2,\cdots, p-1$$

**Property of correlation matrix of $$X$$ variables**
Let $$corr(X_i,X_j) = r_{ij}$$.

$$(X^\ast)^t X^\ast = r_{XX}$$
$$r_{XX}b^\ast = r_{YX}$$ $$\Rightarrow b^\ast = \frac{r_{YX}}{r_{XX}}$$

### multicollinearity issue

Why do we need to avoid multicollinearity among variables?

> When we solve normal equation $$X^tX b = X^tY$$, the $$det(X^tX) \approx 0$$ condition makes the system highly singular. This leads to high round-off error while computation, resulting in severe error in $$b$$.

How to know if the predictor variables are correlated among themselves?

> 1. uncorrelated $$X_1$$ and $$X_2$$ > $$r_{12}^2=0$$ > $$SSR(X_1|X_2) = SSR(X_1)$$ or $$SSR(X_2|X_1) = SSR(X_2)$$
> 2. perfectly correlated $$X_1$$ and $$X_2$$ > $$r_{12}^2=1$$ > $$(X^tX)^{-1}$$ Does not exist. $$\Rightarrow$$ infinitely many regression lines
> 3. general effects of multicollinearity ($$0 < r_{12}^2 < 1$$)
>    $$r_{12}^2 \approx 1 \Rightarrow$$ increase of explanation ability is not significant.
