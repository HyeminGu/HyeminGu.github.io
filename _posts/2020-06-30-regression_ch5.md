---
layout: post
title: RA ch5 Matrix Approaches to Simple Linear Regression
date: 2020-07-04 11:12:00-0400
description: Lecture note chapter 4 for regression analysis taught by Hyemin Gu in 2020
tags: statistics lecture_note
categories: teaching regression_analysis
---

# Ch 5: Matrix Approaches to Simple Linear Regression

Linear functions can be written by matrix operations such as addition and multiplication. Now, we move on to formulation of linear regression into matrices. Knowledge of linear algebra provides lots of intuition to interpret linear regression models. Also, it is easier to describe the calculations using matrices, even in the generalized settings. Therefore, we briefly review useful concepts in linear algebra, and then describe the simple linear regression model into matrix form.

## Outline

1. Review of linear algebra
   - Linear indep:endency and rank
   - quadratic form
   - projection(idempotent) matrix
2. Simple linear regression into matrix form
   - notations
   - simple linear regression
   - ANOVA results
   - a sketch to generalized settings

---

## 1. Review of linear algebra

### Linear independency and rank

**Linear independency** among a set of vectors $$\{ v_1, v_2, \cdots, v_n \}$$ is defined as any linear combination leading to the zero vector $$c_1v_1 + c_2v_2 + \cdots + c_nv_n=0$$ implies $$c_1=c_2=\cdots=c_n=0$$. We can also consider the linear independency among row/column vectors in a square matrix $$M \in \mathbb{R}^{n,n}$$ where $$M = [v_1 v_2 \cdots v_n]$$. About linear independency, the following are equivalent:

1. $$\{v_1, v_2, \cdots, v_n\}$$ is linearly independent.
2. $$Mx=b$$ is consistent for any $$b$$. (nonsingular)
3. $$Mx=b$$ has the unique solution.
4. $$Mx=0$$ has only a trivial solution (zero vector). $$\iff$$ Nullspace of $$M$$ is trivial.
5. $$det(M)\neq0$$
6. Eigenvalues of $$M$$ are nonzero.
7. $$M$$ is invertible.

For a square matrix $$M$$, **rank** is the number of linearly independent rows/columns of $$M$$. Rank cannot exceed the dimension of the vector space (Since $$M$$ is a mapping (function) which maps a vector in $$\mathbb{R}^n$$ to $$\mathbb{R}^n$$, the dimension of the vector space is $$n$$.) If rank equals $$n$$, we say the matrix $$M$$ is full-rank, and otherwise, rank-deficient.

What about a general matrix $$M\in \mathbb{R}^{m,n}$$? In this case, rank is defined as the same way as above. But in the case of overdetermined system $$m > n$$, rank is up to $$min(m,n)=n$$, so we may not have an exact solution. Also, $$M^tM \in \mathbb{R}^{n,n}$$ could be full-rank only if all the columns were independent(rank equals to $$n$$.), whereas $$MM^t \in \mathbb{R}^{m,m}$$ never becomes full-rank.

### quadratic form

Let $$x = (x_1 x_2 \cdots x_n)$$ be a vector with $$n$$ entries/variables, and $$A$$ be a $$n$$ by $$n$$ square matrix. **$$x^tAx$$** is called a quadratic form of $$x$$ with respect to $$A$$ because it represents _any quadratic function_ of variable $$x$$.
$$$$x^tAx = a*{11}x_1^2 + (a*{12} + a*{21})x_1x_2 + (a*{13} + a*{31})x_1x_3 + \cdots + a*{nn}x_n^2$$$$

Moreover, if $$A$$ is positive definite ($$x^tAx > 0$$ except for $$x=0$$ $$\iff$$ Eigenvalues of $$A$$ are all positive), the quadratic form is a convex function(볼록함수), which has a global minimum.

### projection(idempotent) matrix

A matrix $$H$$ is said to be **idempotent** if it satisfies $$H^2=H$$. Another name of such $$H$$ is projection matrix. Several peroperties of idempotent matrices are:

1. Any eigenvalue of an idempotent matrix is 1 or 0.
2. Trace(sum of diagonal entries) of an idempotent matrix becomes its rank.
3. If $$H$$ is idempotent, then $$I-H$$ is also idempotent. <br>(Moreover, it decomposes the vector space $$\mathbb{R}^n$$ into 2 spaces as $$\mathbb{R}^n = range(H) \oplus range(I-H)$$ where $$\oplus$$ denotes direct sum. $$\iff$$ <br>$$range(H)=null(I-H), range(I-H)=null(H)$$. This concept is different from orthogonality. Orthogonality is a stronger condition.)
4. Any projection matrix except for $$I$$ is rank-deficient (not invertible).

When an idempotent matrix $$H$$ also satisfies $$H=H^t$$ (symmetric) then it is called an **orthogonal projection matrix**. For any matrix $$X$$, $$X(X^tX)^{-1}X^t$$ is an orthogonal projection, and it projects a vector into range space (column space) of $$X$$.

<U>Remark</U> A matrix $$U\in \mathbb{R}^{n,n}$$ satisfying $$U^tU=UU^t=I$$ is called an orthogonal matrix. This means $$U$$ is invertible with its inverse $$U^t$$. Be careful that orthogonal projection matrix is not an orthogonal matrix!

## 2. Simple linear regression into matrix form

### notations

Response variable $$Y = (Y_1, Y_2, \cdots, Y_n)^t$$
Design matrix $$X = \newline(1, X_{11}; 1, X_{21}; \vdots ~~ \vdots; 1, X_{n1})$$
Coefficient vector $$\beta = (\beta_1, \beta_2, \cdots, \beta_n)^t$$
Error vector $$\epsilon = (\epsilon_1, \epsilon_2, \cdots, \epsilon_n)^t$$

$$E(Y) = (E(Y_1), E(Y_2), \cdots, E(Y_n))^t = X\beta$$

$$\sigma^2(Y) = E[ (Y-E(Y))(Y-E(Y))^t ]$$

$$E(\epsilon) = 0$$

$$\sigma^2(\epsilon) = \sigma^2 I$$

$$1 = (1, \cdots, 1)^t$$ (one-vector)
$$J$$ : A matrix whose entries are all 1 (one-matrix)

<U>Note</U>

- $$Y^tY = \sum_i Y_i^2$$
- $$X^tY = (\sum_i Y_i \sum_i X_iY_i)^t$$
- $$X^tX = (n, \sum_i X_i; \sum_i X_i, \sum_i X_i^2)$$
- $$(X^tX)^{-1} = (\frac{\sum_i X_i^2}{n\sum_i(X_i-\bar{X})^2} , \frac{-\sum_i X_i}{n\sum_i(X_i-\bar{X})^2}; \frac{-\sum_i X_i}{n\sum_i(X_i-\bar{X})^2}, \frac{n}{n\sum_i(X_i-\bar{X})^2})$$ <br> $$= \frac{1}{\sigma^2} (\sigma^2(b_0), \sigma(b_0,b_1); \sigma(b_0,b_1) ,\sigma^2(b_1))$$

<U>Note</U>
$$A$$ : a constant matrix, $$Y$$ : a random variable, and $$W = AY$$
Then, $$E(A) = A$$,
$$E(W) = E(AY) = AE(Y)$$,
$$\sigma^2(W) = \sigma^2(AY) = A \sigma^2(Y) A^t$$

### simple linear regression

$$Y = X\beta + \epsilon$$, $$E(\epsilon) = 0$$, $$\sigma^2(\epsilon) = \sigma^2 I$$

**Least square method, regression coefficients $$b$$**
Let $$b$$ be a solution to the system below.

1. $$nb_0 + b_1 \sum_i X_i = \sum_i Y_i$$
2. $$b_0 \sum_i X_i + b_1 \sum_i X_i^2 = \sum_i X_i Y_i$$

This can be written as
$$(n, \sum_i X_i; \sum_i X_i, \sum_i X_i^2)(b_0, b_1)^t = (\sum_i Y_i \sum_i X_iY_i)^t$$
i.e. **$$X^tXb = X^tY$$**
$$\Rightarrow$$ **$$b = (X^tX)^{-1}X^tY$$** where $$X^tX$$ is assumed to be full-rank (rank=2 in this case)

properties of $$b$$

- $$E(b) = \beta$$
  > $$E(b) = E[(X^tX)^{-1}X^tY] = (X^tX)^{-1}X^tE(Y) = (X^tX)^{-1}X^tX\beta = \beta$$
- $$\sigma^2(b) = \sigma^2(X^tX)^{-1}$$

**Objective function, $$Q$$**
$$Q = \sum_i \left(Y_i - (\beta_0 + \beta_1 X_i)\right)^2 = (Y-X\beta)^t(Y-X\beta) = Y^tY - 2\beta^tX^tY +\beta^tX^tX\beta$$
$$Q$$ is a quadratic function of variable $$\beta$$. Note that the term $$Y^tY = Y^tIY$$ is a quadratic form and since $$I$$ is positive definite, $$Q$$ has a global minimum. We can find a solution by finding a critical point.
$$b$$ is a solution of $$\frac{\partial Q}{\partial \beta} = -2 X^tY + 2X^tX\beta = 0$$

**Regression line, $$\hat{Y}$$**
**$$\hat{Y}$$** $$ = (\hat{Y_1}, \hat{Y_2}, \cdots, \hat{Y_n})^t = Xb = $$ **$$X(X^tX)^{-1}X^tY = HY$$**, where **$$H = X(X^tX)^{-1}X^t$$ (Hat matrix)**.

Properties of hat matrix $$H$$

- $$H^2 = H$$ (idempotent), $$H^t = H$$ $$\Rightarrow$$ Orthogonal projection matrix
  We can interpret the regression line $$\hat{Y}$$ as an orthogonal projection of $$Y$$ onto the range space of $$X$$, $$Range(X)$$.
- $$Tr(H) = rank(H) = 2$$

**Residuals, $$e$$**
$$e = Y-\hat{Y} = Y - Xb = Y - HY = (I-H)Y$$

Property of the residual $$e$$

- Since $$H$$ is an orthogonal projection matrix, so is $$I-H$$. We can interpret the residual $$e$$ as an orthogonal projection of $$Y$$ onto the space orthogonal to $$Range(X)$$. $$e \perp X$$, $$e \perp \hat{Y}$$.
- $$E(e) = 0$$
  > $$\because E(e) = E[(I-H)Y] = (I-H) E(Y) = (I-H)X\beta$$ > $$= X\beta - X(X^tX)^{-1}X^tX\beta = 0$$
- $$\sigma^2(e) = \sigma^2(I-H)$$
  > $$\because \sigma^2(e) = \sigma^2[(I-H)Y] = (I-H)\sigma^2(Y)(I-H)^t$$ > $$= (I-H)\sigma^2I(I-H) = \sigma^2(I-H)^2I = \sigma^2(I-H)$$

**Mean response of $$\hat{Y_h}$$**
$$\hat{Y_h} = X_h^tb$$
$$\sigma^2(\hat{Y_h}) = \sigma^2(X_hb) = \sigma^2 [\frac{1}{n} + \frac{X_h-\bar{X})^2}{\sum_i(X_i-\bar{X})^2} ]$$

> $$\sigma^2(X_hb) = X_h^t \sigma^2(b) X_h = X_h^t \sigma^2(X^tX)^{-1} X_h = \sigma^2 [\frac{1}{n} + \frac{X_h-\bar{X})^2}{\sum_i(X_i-\bar{X})^2}]$$

### ANOVA results

- $$SSTO = \sum_i (Y_i - \bar{Y})^2 = \sum_i Y_i^2 - \frac{(\sum_i Y_i)^2}{n} = Y^tY - \frac{1}{n}Y^tJY$$
- $$SSE = \sum_i e_i^2 = [(I-H)Y]^t[(I-H)Y] = Y^t(I-H)Y = Y^tY - Y^tHY$$
- $$SSR = SSTO-SSE = Y^tHY - \frac{1}{n}Y^tJY$$

### a sketch to generalized settings

- In application, we use normal error regression model by assuming normal distribution to errors. Also, there is an explicit formula to write normal distribution of the error in matrix form.
- By moving on to matrix formulation, we can generalize the current regression model with one prediction variable to multiple variables. In most cases, the difference is just adding more variables to the design matrix $$X$$ and coeffient $$\beta$$ and $$b$$. When we use normal error regression model for multiple regression, we have MANOVA analogous to ANOVA.
