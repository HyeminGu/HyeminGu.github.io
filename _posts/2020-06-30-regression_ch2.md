---
layout: post
title: RA ch2 Review of Mathematical Statistics
date: 2020-07-01 11:12:00-0400
description: Lecture note chapter 2 for regression analysis taught by Hyemin Gu in 2020
tags: statistics lecture_note
categories: teaching regression_analysis
---

# CH 2: Review of Mathematical Statistics

## Outline

1. Probabilistic distributions
   - special distributions
   - normal distribution
   - T distribution, F distribution
2. Statistical inference
   - statistical estimation
   - statistical hypothesis test
   - inference for population mean
   - inference for population variance
3. Correlation analysis
   - correlation
   - statistical inference on $$\rho$$

---

## 1. Probabilistic distributions

### special distributions

| Discrete          | $$P(X = k)$$             | Continuous  | $$P(a \leq X \leq b)$$    |
| :---------------- | ------------------------ | :---------- | ------------------------- |
| binomial          | $$B(n, p)$$              | gamma       | $$\Gamma(\alpha, \beta)$$ |
| poisson           | $$\mathcal{P}(\lambda)$$ | normal      | $$N(\mu, \sigma^2)$$      |
| negative binomial | $$Nb(\alpha, p)$$        | Exponential | $$Exp(\lambda)$$          |
| geometric         | $$G(p)$$                 | chi-square  | $$\chi^2(n)$$             |
|                   |                          | beta        | $$Beta(\alpha, \beta)$$   |
|                   |                          | T           | $$t(n)$$                  |
|                   |                          | F           | $$F(m, n)$$               |

<U>Note</U> 각 pdf를 암기하는 것보다 각 분포가 이산/연속인지, 매개변수가 무엇이며 어떤 의미인지, 각 분포의 성질을 아는 것이 중요

### normal distribution

normal 분포의 경우 pdf를 기억해둘 필요가 있다.

**standard normal distribution (표준정규분포)** - $$X \sim N(0, 1)$$
pdf : $$f(x) = \frac{1}{\sqrt{2\pi}} e^{-\frac{x^2}{2}}, x \in \mathbb{R}$$
where 0 is the mean and 1 is the variance of the distribution.

**General normal distribution** - $$Y \sim N(\mu, \sigma^2)$$
$$Y = \mu + \sigma X, \sigma>0$$
pdf : $$g(y) = \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{(y-\mu)^2}{2\sigma^2}}, y \in \mathbb{R}$$
where $$\mu$$ is the mean and $$\sigma^2$$ is the variance of the distribution.

properties of normal distribution

1. If $$X_i \sim N(\mu_i, \sigma_i^2)$$ independent for $$i=1,2,\cdots, n$$, then
   (a) $$Y = \sum_{i=1}^n a_i X_i \sim N(\sum_i a_i \mu_i, \sum_i a_i^2 \sigma_i^2)$$ </br>cf) $$X \sim N(\mu, \sigma^2) \Rightarrow aX + b \sim N(a\mu + b, a^2\sigma^2)$$ for constant $$a, b$$
   (b) $$V = \sum_{i=1}^n \left( \frac{X_i - \mu_i}{\sigma_i} \right)^2 = \sum_{i=1}^n z_i^2 \sim \chi^2(n)$$

### T distribution, F distribution

**T distribution**
Let $$Z \sim N(0, 1), V \sim \chi^2(n)$$ are independent
Define $$T = \frac{Z}{\sqrt{V/n}} \sim t(n)$$

**F distribution**
Let $$U \sim \chi^2(m), V \sim \chi^2(n)$$ are independent
Define $$W = \frac{U/m}{V/n} \sim F(m, n)$$

properties

1. $$T^2 = \frac{z^1/1}{V/n} \sim F(1, n)$$
2. $$W \sim F(n, m) \Rightarrow 1/W \sim F(m,n)$$

<U>Theorem</U> (Student)
$$X_1, \cdots, X_n \sim N(\mu, \sigma^2)$$ i.i.d.

Define **sample mean** $$\bar{X} = \frac{1}{n} \sum_{i=1}^n X_i$$,
and **sample variance** $$s^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \bar{X})^2$$.

(a) $$\bar{X} \sim N(\mu, \frac{\sigma^2}{n})$$

(b) $$(n-1) s^2/\sigma^2 = \sum_{i=1}^n \frac{(X_i - \bar{X})^2}{\sigma^2} \sim \chi^2(n-1)$$

(c) $$\bar{X}$$ and $$s^2$$ are independent

(d) $$T = \frac{\bar{X} - \mu}{s/\sqrt{n}} \sim t(n-1)$$

> <U>proof</U>
> (b) $$\sum_{i=1}^n \frac{(X_i - \mu)^2}{\sigma^2} = \sum_{i=1}^n \frac{(X_i - \bar{X})^2}{\sigma^2} + \sum_{i=1}^n \frac{(\bar{X} - \mu)^2}{\sigma^2}$$ > $$\sum_{i=1}^n \frac{(\bar{X} - \mu)^2}{\sigma^2} = \frac{(\bar{X} - \mu)^2}{(\sigma/\sqrt{n})^2}$$
> First term follows $$\chi^2(n)$$, and third term follows $$\chi^2(1)$$. Due to the additivity in chi-square distribution, (b) follows.
>
> (d) $$T = \frac{\bar{X}-\mu}{s/\sqrt{n}} = \frac{(\bar{X}-\mu)/(\sigma/\sqrt{n})}{\sqrt{s^2/\sigma^2}} = \frac{z}{\sqrt{U/(n-1)}} \sim t(n-1)$$

<U>Note</U> $$n$$이 커지면 T 분포는 표준정규분포와 유사하게 됨. 일반적으로 T 분포는 표준정규분포보다 두꺼운 꼬리를 가짐.

## 2. Statistical inference

$$X$$가 어떤 분포를 따른다고 하자. 이때 해당 분포의 상방 백분위수 ($$100*(1- \alpha)$$ 백분위수)를 $$x_\alpha = P(X \leq x) = \alpha$$ 를 만족하는 $$x$$값이라고 정의하자.

### statistical estimation(통계적 추정)

모수에 대한 추측값 (점추정, point estimation) 또는 오차의 한계(구간추정, interval estimation)를 제시한다.

ex) (point estimation) $$E(\bar{X}) = \mu, Var(\bar{X}) = \frac{\sigma^2}{n}, E(s^2) = \sigma^2$$
ex) (interval estimation)
$$X_i \sim N(\mu, \sigma^2)$$이고 모분산 $$\sigma^2$$을 알 때 평균 $$\mu$$의 구간추정
$$z = \frac{\bar{X}-\mu}{\sigma/\sqrt{n}} \sim N(0,1)$$
$$P(-z_{\alpha/2} \leq \frac{\bar{X}-\mu}{\sigma/\sqrt{n}} \leq z_{\alpha/2}) = 1-\alpha$$
따라서, $$\mu$$의 $$100*(1- \alpha)$$ 신뢰구간 : $$(\bar{X}-z_{\alpha/2} * \sigma/\sqrt{n}, \bar{X}+z_{\alpha/2} * \sigma/\sqrt{n})$$
오차의 한계 : $$z_{\alpha/2} * \sigma/\sqrt{n}$$
신뢰수준 : $$100*(1- \alpha)$$

### statistical hypothesis test

**가설, hypothesis**

- 귀무가설, Null hypothesis, $$H_0$$ : 효과가 없다, 차이가 없다, 서로 다르지 않다는 주장
- 대립가설, Alternative hypothesis, $$H_1$$ : 효과가 있다, 차이가 있다, 서로 다르다는 주장
  - 양측가설, 2-sided hypothesis : $$\theta \neq \theta_0$$
  - 단측가설, 1-sided hypothesis : $$\theta > \theta_0$$ or $$\theta < \theta_0$$

**가설 검정, test of statistical hypothesis**
귀무/대립가설을 설정하고, 얻어진 자료를 근거로 어느 가설이 더 타당한지 판단

**유의성 검정, test of statistical significance**
얻어진 자료보다 더 극단적인 자료가 얻어질 가능성을 계산하여, 이를 근거로 주어진 가설의 유효성 판단

**유의확률, p-value**
$$H_0$$이 참이라는 가정 하에, 현재와 같거나 더 극단적인 자료가 얻어질 확률
i.e. 귀무가설을 기각할 경우 저지르게 될 오류의 최대 확률
p-value가 크다 $$\Longleftrightarrow$$ 귀무가설이 참이라는 가정 하에서 귀무가설을 기각하는 오류를 낼 확률이 높다 $$\Longleftrightarrow$$ 귀무가설이 참일 확률이 높다

**유의수준, $$\alpha$$**
귀무가설의 기각에 대한 기준 확률 (p-value가 큰지 작은지를 판단하는 기준)
p-value $$> \alpha \Rightarrow$$ 귀무가설을 채택
p-value $$< \alpha \Rightarrow$$ 귀무가설을 기각

**기각역**
귀무가설을 기각시키는 검정통계량의 관측값의 영역 $$P(\bar{x} \leq x) | \mu = \mu_0) \leq \alpha$$인 $$x$$ 값

**통계적 유의성**
유의확률 (p-value)이 유의수준($$\alpha$$) 이하이면 검사결과가 유의수준 $$\alpha$$에서 통계적으로 유의하다고 할 수 있다

**유의성 검정의 단계**

1. 가설 설정 ex) $$H_0 : \mu = \mu_0$$ $$H_1 : \mu > \mu$$
2. 유의수준 지정 ex) $$\alpha = 0.05$$
3. 검정통계량 결정 ex) $$z = \frac{\bar{X}-\mu_0}{\sigma/\sqrt{n}} \sim N(0, 1)$$ under $$H_0$$
4. p-value 계산 ex) $$z_0 = \frac{\bar{x}-\mu_0}{\sigma/ \sqrt{n}} \Rightarrow p = P(z > z_0 \mid H_0)$$
5. 유의수준과 비교 ex) $$p < \alpha$$
6. 유의성 판단 ex) $$H_0$$ 기각

의미: 귀무가설의 반증은 모수의 추정값이 귀무가설 하에서 대립가설 방향으로 멀리 떨어질수록 강함

### inference for population mean

$$X_i, i=1, \cdots, n$$ are $$n$$ observations from a population.

1. Assuming that $$X_i \sim N(\mu, \sigma^2)$$
   1. when $$\sigma^2$$ is known : $$z = \frac{\bar{X}-\mu}{\sigma/\sqrt{n}} \sim N(0,1)$$
   2. when $$\sigma^2$$ is unknown : $$t = \frac{\bar{X}-\mu}{s/\sqrt{n}} \sim t(n-1)$$
2. Assuming that $$X_i \sim i.i.d.(\mu, \sigma^2)$$
   1. if $$n$$ is large enough
      - when $$\sigma^2$$ is known : $$z = \frac{\bar{X}-\mu}{\sigma/\sqrt{n}} \sim N(0,1)$$
      - when $$\sigma^2$$ is unknown : $$s^2 \rightarrow \sigma^2$$, $$z = \frac{\bar{X}-\mu}{\sigma/\sqrt{n}} \sim N(0,1)$$
   2. if $$n$$ is not large enough and the distribution is far from normal distribution : Non-parametric method

### inference for population variance

Case 1) Estimating the population variance
where $$X_i \sim N(\mu, \sigma^2)$$, i.i.d. $$i=1, \cdots, n$$
$$\frac{n-1}{\sigma^2}s^2 \sim \chi^2(n-1)$$ where $$s^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \bar{X})^2$$
**point estimation of $$\sigma^2$$** : $$\hat{\sigma^2} = s^2$$
**interval estimation of $$\sigma^2$$** : $$(\frac{(n-1) s^2}{\chi_{\alpha/2}^2(n-1)}, \frac{(n-1) s^2}{\chi_{1-\alpha/2}^2(n-1)})$$

Case 2) Comparing the two population variances
where $$X_i \sim N(\mu_1, \sigma_1^2)$$, i.i.d. $$i=1, \cdots, n_1$$ independent from $$Y_i \sim N(\mu_2, \sigma_2^2)$$, i.i.d. $$i=1, \cdots, n_2$$
$$F = \frac{s_1^2/\sigma_1^2}{s_2^2/\sigma_2^2} \sim F(n_1-1, n_2-1)$$
**interval estimation of $$\frac{\sigma_1^2}{\sigma_2^2}$$** :
$$(\frac{s_1^2}{s_2^2 F_{\alpha/2}(n_1-1, n_2-1)}, \frac{s_1^2}{s_2^2 F_{1-\alpha/2}(n_1-1, n_2-1)}) \iff (\frac{s_1^2 F_{1-\alpha/2}(n_1-1, n_2-1)}{s_2^2}, \frac{s_1^2 F_{\alpha/2}(n_1-1, n_2-1)}{s_2^2})$$

## 3. Correlation analysis

### correlation

The correlation between two random variables $$X$$ and $$Y$$ is defined as
$$$$\rho = corr(X, Y) = \frac{cov(X, Y)}{\sqrt{Var(X)Var(Y)}}$$$$

<U>properties</U>

1. $$-1 \leq \rho \leq 1$$
2. measures the intensity of linearity
3. $$\mid \rho \mid \approx 1 \Rightarrow$$ high linear relationship

### statistical inference on $$\rho$$

Let $$S_{xx} = \sum_{i=1}^{n} (x_i - \bar{x})^2$$,
$$S_{yy} = \sum_{i=1}^{n} (y_i - \bar{y})^2$$, and
$$S_{xy} = \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})$$.

**Statistical test on $$\rho$$**
$$H_0 : \rho = 0$$
test statistic : $$T = \sqrt{n-2} \frac{r}{\sqrt{1-r^2}} \sim t(n-2)$$ under $$H_0$$
where $$r^2 = \frac{SSR}{SSTO} = \frac{S_{xy}^2/S_{xx}}{S_{yy}} = (\frac{S_{xy}}{\sqrt{S_{xx}} \sqrt{S_{yy}}})^2$$

> <U>proof</U>
> Note that $$SSR = \sum_{i=1}^n (\hat{Y_i} - \bar{Y})^2 = \beta_1^2 \sum_{i=1}^n (X_i - \bar{X})^2$$.
> $$T = \sqrt{n-2} \frac{r}{\sqrt{1-r^2}} = \frac{\sqrt{SSR}}{\sqrt{MSE}} \sim t(n-2)$$ $$\because T^2 \sim F(1, n-2)$$

If $$H_0$$ is rejected, it is said that there is a linear relationship between $$X$$ and $$Y$$ within the possibility of $$\alpha$$.

<U>Note</U> $$H_0$$ is more likely to be dismissed when $$n$$ is large or $$\mid r\mid$$ is large.
