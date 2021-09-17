[TOC]

# SVM의 비유적 이해

| SVM                  | 남북한 경계선          |
| :------------------- | :--------------------- |
| Hyperplane           | 군사분계선 (MDL)       |
| Slab                 | DMZ                    |
| Boundary of the slab | 북방한계선, 남방한계선 |
| Margin               | 2km                    |
| Support vector       | GOP                    |
| Slack variables      | GP                     |
| ξ (xi)               | "봐주는 거리"          |



<img src="https://i.loli.net/2021/09/14/v1h2Koaw5CQkEMH.png" alt="1535780677" style="zoom:67%;" />



# SVM의 수학적 이해

## Optimal Separating Hyperplanes (Xβ)

**Perspective M**

![image-20210914004916690](https://i.loli.net/2021/09/14/njrCX8usFWfZvdq.png)



**Perspective β**
$$
\max_{\beta,\beta_0}\:M \\
subject\:to\:\frac{1}{||\beta||}y_i(x_i^T\beta+\beta_0) \geq M
$$
$$
\max_{\beta,\beta_0}\:M \\
subject\:to\:y_i(x_i^T\beta+\beta_0) \geq 1
$$

$$
\min_{\beta,\beta_0}\:\frac{1}{2}||\beta||^2 \\
subject\:to\:y_i(x_i^T\beta+\beta_0) \geq 1
$$

※ 현재까지 모든 수식은 동일한 식이다!

Lagrange primal function:![image-20210914010124090](https://i.loli.net/2021/09/14/TNQ1ROU7Jsi5xVI.png)

![image-20210914010308007](https://i.loli.net/2021/09/14/pXQNsRIUZoCm8PO.png)

After substitution, we obtain the Lagrangian Wolfe dual objective function:

![image-20210914010528699](https://i.loli.net/2021/09/14/7VpSbZQXeAHOBfF.png)

Additional Karush-Kuhn-Tucker condition:![image-20210914010703807](https://i.loli.net/2021/09/14/jEv7yMgwCHRI8bp.png)

Parameter α:

![image-20210914011030038](https://i.loli.net/2021/09/14/2hirUeRj6aCMmg9.png)

α contains the information of whether we concern the variable or not!

## Slack Variables 의 등장

![image-20210914012448320](https://i.loli.net/2021/09/14/z5u2msBIbqjQ9iT.png)

**Perspective M**
$$
\max_{\beta,\beta_0,||\beta||=1} M \\
subject\:to\:y_i(x_i^T\beta+\beta_0) \geq M - \xi_i, \\
\xi_i \geq 0, \sum_{i=1}^{N}\xi_i \leq constant
$$

**Perspective β**
$$
\min_{\beta,\beta_0}\:\frac{1}{2}||\beta||^2 \\
subject\:to\:y_i(x_i^T\beta+\beta_0) \geq 1-\xi_i, \\
\xi \geq 0, \sum\xi_i \leq constant'
$$
Lagrange function for the last constraint only:

![image-20210914160934521](https://i.loli.net/2021/09/14/mrjxfnSD4cAOL1V.png)

Lagrange primal function:

![image-20210914012838306](https://i.loli.net/2021/09/14/ZD8fjxRQ6snLrHv.png)

![image-20210914013042339](https://i.loli.net/2021/09/14/DIwSaXTVmjshUCH.png)

After substitution, we obtain the Lagrangian Wolfe dual objective function:

![image-20210914013132181](https://i.loli.net/2021/09/14/9fLoezjSxvC3U4c.png)

The followings are constraints:
$$
0 \leq \alpha_i \leq C, \\
\sum_{i=1}^N\alpha_iy_i = 0, \\
\alpha_i[y_i(x_i\beta + \beta_0) - (1 - \xi_i)] = 0, \\
\mu_i\xi_i = 0, \\
y_i(x_i^T\beta + \beta_0) - (1-\xi_i) \geq 0
$$
Q. α의 특징은? C의 특징은?



# Kernel

사고실험: 일직선 위의 분류분석

$$
◆─◆─◆─◆─◆─△─△─△─△─△─△─◆─◆─◆─◆─◆─◆
$$
Transformation: x → h(x)

![image-20210914014257954](https://i.loli.net/2021/09/14/NwfX7DIZMJnPkKF.png)

![image-20210914014729009](https://i.loli.net/2021/09/14/GwNjXLFdtgqi91Q.png)



Kernel function: K(x, x')

![image-20210914015634006](https://i.loli.net/2021/09/14/vl3wVO6MPFjSqNe.png)

Candidates:

![image-20210914015706560](https://i.loli.net/2021/09/14/vpHOTCWQKh7kRg8.png)

Example: d=2

![image-20210914015758177](https://i.loli.net/2021/09/14/6hLwFvtb9SknENg.png)

The kernel property of the support vector machine is not unique!

![image-20210914184149879](https://i.loli.net/2021/09/14/VhP9b8fEecGzyQw.png)



# SVM과 차원의 저주

## 사고실험 1

$$
A. △─△─△─△─△─△─△─△─◆─◆─◆─◆─◆─◆─◆─◆─◆
$$

$$
B. ◆─◆─◆─◆─◆─△─△─△─△─△─△─◆─◆─◆─◆─◆─◆
$$

어느 것이 분류가 더 쉬운가?

→ 인간에게는 쉽지만, 컴퓨터에게는 까다로운 질문.

빠르고 (computational) 정확한 (reduced test error) 모델을 찾는 것이 컴퓨터의 목표이다.



## 사고실험 2

<img src="https://i.loli.net/2021/09/14/TCAZgKUL6EkSyGD.png" alt="image-20210914023104760" style="zoom:67%;" />

느리더라도 고차원의 성능이 좋지 않나?

→ 그렇지 않다. 오히려 training data 내 노이즈의 영향을 크게 받는 과적합 문제가 발생할 수 있다.



## 사고실험 3

C, the cost of slack variables.
$$
△─△─△─△─△─◆─△─△─◆─◆─◆─◆─◆─◆─◆─◆
$$
C가 작다면?

- 하나를 slack variable로 처리하고 중간에서 자르면 된다!
- high bias, low variance
- underfitting

C가 크다면?

- 복잡한 kernel 을 이용해서 margin을 확보해야 한다.
- low bias, high variance
- overfitting



# Loss + Penalty

Recall:
$$
\min_{\beta,\beta_0}\:\frac{1}{2}||\beta||^2 \\
subject\:to\:y_i(x_i^T\beta+\beta_0) \geq 1-\xi_i, \\
\xi \geq 0, \sum\xi_i \leq constant'
$$
Rephrase:
$$
\min_{\beta,\beta_0}\:\frac{1}{2}||\beta||^2 \\
subject\:to\:[1-y_i(x_i^T\beta+\beta_0)]_{+} \leq \xi_i, \\
\sum\xi_i \leq constant'
$$
Rephrase:
$$
\min_{\beta,\beta_0}\:\frac{1}{2}||\beta||^2 \\
subject\:to\:\sum_{i=1}^N[1-y_i(x_i^T\beta+\beta_0)]_{+} \leq constant'
$$
Final optimization problem:
$$
\min_{\beta,\beta_0}\:\frac{1}{2}||\beta||^2 + C\sum_{i=1}^N\Big[1-y_if(x_i)\Big]_{+}
$$
Which is equivalent to:

![image-20210914160533474](https://i.loli.net/2021/09/14/KUWpoi3tfL8sP9Q.png)

→ **Loss + Penalty** form!

Compare it with:

![image-20210914160924243](https://i.loli.net/2021/09/14/mrjxfnSD4cAOL1V.png)

→ The solutions are equal when C = 1/λ.



## Loss

<img src="https://i.loli.net/2021/09/14/PMFv29oizSbNIRc.png" alt="image-20210914183850989" style="zoom:67%;" />

![image-20210914154154490](https://i.loli.net/2021/09/14/cP9NhdoVnl3r4mu.png)
$$
Risk\:function\:R[y,f(x)] = E_y\Big[L[y,f(x)]\Big]
$$


## Penalty

Ridge Regression:
$$
L(\beta) = \min_{\beta}\sum_{i=1}(y_i-\hat{y}_i)^2 + \lambda ||\beta||^2
$$
Compare it with SVM:

![image-20210914160533474](https://i.loli.net/2021/09/14/KUWpoi3tfL8sP9Q.png)

→ Loss function 만 다르고 같은 R2 penalty 를 공유한다!

- Ridge Regession: Squared Error
  - LDA also uses squared error but without the penalty term.

- SVM: SVM Hinge Loss



## SVM & Logistic Regression

Again the **loss functions** are different!

- SVM: SVM Hinge Loss
- Logistic Regression: Binomial Deviance, the negative (−) binomial log-likelihood loss function



Logistic Regression:
$$
Pr(Y=1|x)=\frac{1}{1+e^{-f(x)}} \\
Pr(Y=0|x)=\frac{1}{1+e^{f(x)}}
$$

$$
Y_{new}=2(Y-0.5),\:Y\in\{0,1\} \\
so\:that\:Y_{new} \in \{-1,1\}
$$

$$
Pr(Y_{new}=1|x) = \frac{1}{1+e^{-f(x)}} \\
Pr(Y_{new}=-1|x)=\frac{1}{1+e^{f(x)}}
$$

Binomial likelihood:
$$
Pr(Y=1|x)^Y\times Pr(Y=1|x)^{1-Y}
$$
Loss = Negative(−) binomial log-likelihood:
$$
\begin{align}
Loss &= -Y\:\log Pr(Y=1|x)-(1-Y)\log Pr(Y=0|x) \\
&= -\frac{Y_{new}+1}{2}\log Pr(Y_{new}=1|x)-\frac{1-Y_{new}}{2}\log Pr(Y_{new}=-1|x) \\
&= -\frac{Y_{new}+1}{2}\log \frac{1}{1+e^{-f(x)}} -\frac{1-Y_{new}}{2}\log \frac{1}{1+e^{f(x)}} \\
&=\frac{Y_{new}+1}{2}\log ({1+e^{-f(x)}}) +\frac{1-Y_{new}}{2}\log (1+e^{f(x)}) \\
&= \log(1+e^{-Y\cdot f(x)}) \because Y\in\{-1,1\}

\end{align}
$$
Risk minimizer f:

![image-20210914181649092](https://i.loli.net/2021/09/14/mwjVTHbIOgfnPus.png)

![image-20210914181708905](https://i.loli.net/2021/09/14/sWiEt14UqC6Y9y2.png)

**Rule of Thumb**

- Use SVM when the classes are well separated!
- Use logistic regression in more overlapping regimes.



# Path Algorithm for Parameters

![image-20210916061212327](https://i.loli.net/2021/09/16/xl97PErzis8eagb.png)

![image-20210914160533474](https://i.loli.net/2021/09/14/KUWpoi3tfL8sP9Q.png)

The corresponding solution:

![image-20210916055459124](https://i.loli.net/2021/09/16/iHlGySAK3R4nrJV.png)

- α's all lie in [0, 1]
  - α = 0 ← yf > 1: the observations are correctly classified outside their margins.
  - α = 1 ← yf < 1: the observations inside their margins.
  - α = 0.XX ← yf = 1: the observations sitting on their margins.

- λ is large → ∥β∥ is small → M = 1 / ∥β∥ is large → The margin is wide.
- We decrease λ from an initial large value.
  - Some observations inside the margin comes out. (α = 1 → α = 0)
  - Meanwhile it smoothly changes the α on the margins. α(λ)

