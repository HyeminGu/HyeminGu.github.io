---
layout: post
title: RA ch6 Multiple Regression 1
date: 2020-07-05 11:12:00-0400
description: Lecture note chapter 6 for regression analysis taught by Hyemin Gu in 2020
tags: statistics lecture_note tutorial
categories: teaching regression_analysis
---
# Ch 6: Multiple Regression 1
## Outline
1. General regression models
    * types of general regression models
    * simple regression model
    * normal error regression model
    * Fitted values and residuals
2. ANOVA approach
    * ANOVA results
    * F-test
    * coefficient of multiple determination
3. Inference
    * inference on parameters
    * mean response of $$Y_h$$
    * a new observation $$Y_{h,new}$$

---

## 1. General regression models
### types of general regression models
* $$p-1$$ predictor variables <br>ex) $$Y_i =  \beta_0 + \beta_1 X_{1i} + \beta_2 X_{2i} + \epsilon_i$$
* qualitative predictor variables $$\rightarrow$$ Ch 8<br>ex) Male/Female 
* polynomial regression <br>ex) $$Y_i = \beta_0 + \beta_1 X_i + \beta_2 X_i^2 + \epsilon_i$$
* transformed variables <br>ex) $$Y_i^\ast = log Y_i = \beta_0 + \beta_1 X_i + \epsilon_i$$
* interaction effects <br>ex) $$Y_i =  \beta_0 + \beta_1 X_{1i} + \beta_2 X_{2i} + \beta_3 X_{1i}X_{2i} + \epsilon_i$$

From now on, we increase the number of predictor variables to $$p-1$$. To rewrite linear regression model with $$p-1$$ predictor variables into matrix form, we need to define several terms such as:
* $$Y = (Y_1, Y_2, \cdots, Y_n)^t$$, size = $$n \times 1$$
* $$X = \newline(1, X_{11}, X_{12}, \cdots, X_{1,p-1} ;  1, X_{21}, X_{22}, \cdots, X_{2,p-1} ; \cdots ; 1, X_{n1}, X_{n2}, \cdots, X_{n,p-1})$$, size =  $$n \times p$$
* $$\beta = (\beta_0, \beta_1, \beta_2, \cdots, \beta_{p-1})^t$$, size =  $$p \times 1$$ 
* $$\epsilon = (\epsilon_1, \epsilon_2, \cdots, \epsilon_n)^t$$, size =  $$n \times 1$$

### simple regression model
$$Y = X\beta + \epsilon$$, $$E(\epsilon) = 0$$, $$\sigma^2(\epsilon) = \sigma^2 I \in \mathbb{R}^n$$
LSE: minimizer of $$Q = (Y-X\beta)^t(Y-X\beta) = \epsilon^t \epsilon$$
$$b = (X^tX)^{-1}X^tY$$

### normal error regression model
Add an assumption that $$Y \sim N(X\beta, \sigma^2 I)$$.
MLE: maximizer of $$L(\beta, \sigma^2) = \frac{1}{(2\pi \sigma^2)^{\frac{n}{2}}} exp \left(-\frac{1}{2\sigma^2} (Y-X\beta)^t(Y-X\beta)\right)$$
$$\hat{\beta} = (X^tX)^{-1}X^tY$$

### Fitted values and residuals
$$\hat{Y} = (\hat{Y_1}, \hat{Y_2}, \cdots, \hat{Y_n})^t = Xb = X(X^tX)^{-1}X^tY = HY$$, where **$$H = X(X^tX)^{-1}X^t$$ (Hat matrix)**.
* $$E(\hat{Y}) = E(Y)$$
* $$\sigma^2(\hat{Y}) = \sigma^2 H$$ <br>
$$e = Y-\hat{Y} = Y - Xb = Y - HY = (I-H)Y$$
* $$E(e) = 0$$
* $$\sigma^2(e) = \sigma^2(I-H)$$

## 2. ANOVA approach
### ANOVA results

| name | formula | df | mean square |
| :---:| :---:   |:---:| :---:      |
|$$SSTO$$| $$Y^tY - \frac{1}{n}Y^tJY$$ | $$n-1$$| |
|$$SSE$$ | $$Y^tY - Y^tHY$$ | $$n-p$$ | $$MSE = \frac{SSE}{n-p}$$ |
|$$SSR$$ | $$Y^tHY - \frac{1}{n}Y^tJY$$ | $$p-1$$ | $$MSR = \frac{SSR}{p-1}$$ |

$$E(MSE) = \sigma^2$$
$$E(MSR) = \sigma^2 + \alpha$$, $$\alpha \geq 0$$

### F-test
**$$H_0 : \beta_1 = \beta_2 = \cdots = \beta_{p-1} = 0$$**
test statistics: $$F^\ast = \frac{MSR}{MSE} \sim F(p-1, n-p)$$ under $$H_0$$ by Cochran's theorem

### coefficient of multiple determination
$$R^2 = \frac{SSR}{SSTO} = 1- \frac{SSE}{SSTO}$$, $$0 \leq R \leq 1$$
If it is near 1, there is a strong linear relationship between $$X$$ and $$Y$$.
If it is near 0, all $$b_k=0, \forall k=1,2,\cdots, p-1$$

**Adjusted $$R^2$$**
$$R_a^2 = 1- \frac{SSE/(n-p)}{SSTO/(n-1)}$$
: to avoid deciding the most complex model with largest number of variables

## 3. Inference
### inference on parameters
$$E(b) = \beta$$ (unbiased)
$$\sigma^2(b) = \sigma^2 (X^tX)^{-1}$$, size: $$p \times p$$
Needs an assumption that $$b \sim MVN(\beta, \sigma^2 (X^tX)^{-1})$$ $$MVN$$: multi-variate normal distribution

$$s^2(b) = MSE(X^tX)^{-1}$$
For the normal error regression model, $$\frac{b_k -\beta_k}{s(b_k)} \sim t(n-p), k=0,1, \cdots, p-1$$

**$$1-\alpha$$ confidential limits for single $$\beta_k$$** 
$$b_k \pm t(1-\alpha/2, n-p)s(b_k)$$

**T-test**
$$H_0 : \beta_k = 0$$, test statistic: $$t^\ast = \frac{b_k}{s(b_k)}$$

### mean response of $$Y_h$$
$$X_h = (1, X_{h1}, X_{h2}, \cdots, X_{hn})^t$$
$$\hat{Y_h} = X_h^tb$$
$$\sigma^2(\hat{Y_h}) = \sigma^2(X_hb) = X_h^t \sigma^2(X^tX)^{-1} X_h = X_h^t \sigma^2(b) X_h$$
$$s^2(\hat{Y_h}) = s^2(X_hb) = MSE X_h^t (X^tX)^{-1} X_h = X_h^t s^2(b) X_h$$

**$$1-\alpha$$ confidential limits for $$E(Y_h)$$** 
$$\hat{Y_h} \pm t(1-\alpha/2, n-p)s(\hat{Y_h})$$

### a new observation $$Y_{h,new}$$
$$X_h = (1, X_{h1}, X_{h2}, \cdots, X_{hn})^t$$

**$$1-\alpha$$ confidential limits for $$Y_{h,new}$$** 
$$\hat{Y_h} \pm t(1-\alpha/2, n-p)s(pred)$$
$$s^2(pred) = MSE + s^2(\hat{Y_{h,new}}) = MSE (1 + X_h^t (X^tX)^{-1} X_h)$$

---
We've generalized linear regression model with one predictor variable to multi-variable. Many things were analogous to one variable case, but we could notice that tests for the coefficients were restricted. Next time, we introduce extra sum of squares to ease this restriction.

---
Here is the [jupyter notebook script](https://github.com/HyeminGu/Regression_R_tutorials/blob/main/Regression_3_Multiple_Linear_Regression.ipynb) to run several practice codes using R.
