## 💻 Programming HW description 💻

시작하기 전에 `hw1.Rmd` 파일과 `home1-part1-data.R`, `home1-part2.data.R` 데이터를 다운받아서 같은 working directory에 위치시켜주세요.

이 description과 Rmd 파일을 함께 읽어가면서 `# TODO` 라고 된 부분을 채워서 노트북을 완성해봅시다.

(✏️reference : University of Washington STAT435 Intro to Statistical Learning HW1)

📍 얼핏 보면 문제가 굉장히 많아보이지만 막상 `#TODO` 라고 되어있는 부분은 그리 많지 않습니다! 겁먹지 마세요:)

📍제가 했던 숙제(만점 못받음..)를 변형한 것이기 때문에 얼마든지 더 나은 방법이 있을 수 있습니다. Rmd 파일과 이 description은 가이드라인이고 본인이 더 효율적인 방식이나 다른 방식으로 짜고 싶다면 얼마든지 가능합니다!

📍예시답안은 수요일에 업로드하겠습니다!

### Part 1. Implement and experience KDE on your own!

먼저 간단히 시뮬레이션된 데이터를 생성합니다. sin(x) 함수에 Gaussian noise를 더한 데이터를 생성합니다.

**(a)** R에 내장된 함수인 `ksmooth` 가 어떻게 작동하는지 봅시다! Gaussian kernel을 사용할 때와 Uniform kernel (box kernel)을 사용할 때 어떻게 다를까요? 경우에 따라 bandwidth를 줄이면 uniform kernel가 끊기는 현상도 볼 수 있습니다.

**(b)** 이젠 직접 kernel smoothing하는 함수를 다음과 같이 구현해봅시다. 

`ksmooth.train(x.train, y.train, bandwidth=0.5)` with output `x.train`, `yhat.train` (`x.train` 은 정렬되지 않았다고 가정합니다.)

세션때 배웠던 Nadaraya-Watson average와 Gaussian kernel을 이용하면 됩니다.

중심을 기준으로 quartile (75%)에 해당하는 density가 +/- 0.25*bandwidth 내에 들어오도록 scaling 해줍니다. (이건 되어있음)

**(c)** (a)에서 `ksmooth` 를 이용해서 피팅했던 $\hat{f}$ 과 여러분의 `ksmooth.train` 을 이용해 피팅한 것이 비슷한지 시각화해서 비교해봅시다!

**(d)** ISLR의 Wage dataset을 불러옵니다. (`home1-part1-data.R`)

(원래는 `ksmooth.predict` 도 구현하여 test set에서도 evaluation을 해야 하지만 이 과정에서 interpolation을 해야 하는 등 번거로워지기 때문에 이번엔 train data만 사용합니다!)

데이터의 scatterplot을 그려보고 구현한 함수로 피팅했을 때 어떻게 함수가 추정되는지 확인해봅시다.

그런 뒤 bandwidth가 1, ..., 10까지로 늘어남에 따라 training error는 어떻게 변하는지 봅시다.



### Part 2. Optimal Bandwidth

이번에는 bandwidth에 따른 bias-variance tradeoff를 봅시다.

Training sample $(x_1, y_1), ..., (x_n, y_n)$.

Predictor values $x_1, ..., x_n$ are considered fixed (not random).

Response values $y_i=f(x_i)+\epsilon_i$, with $\epsilon_1, ..., \epsilon_n$ independent, $E(\epsilon_i)=0, Var(\epsilon_i)=\sigma^2$

Define $\textbf{y}=(y_1, ..., y_n), \textbf{f}=(f(x_1), ..., f(x_n))$, etc.

$K_\lambda(x)$ : Kernel with bandwidth parameter $\lambda$ controlling the amount of smoothing.

Define $\textbf{W}$ : n x n weight matrix with $\textbf{W}_{i,j}=\dfrac{K_\lambda(x_i-x_j)}  {\sum_j K_\lambda(x_i=x_j)}$ 

Then $\hat{f}=Wy$.

**(a)** 위의 specification에 따라서 W를 만들고 (Part1에서와 거의 동일합니다!) `sigma=seq(from=0.01, to=2, by=0.01)` 에 따라서 variance, bias^2, sum(MSE)를 저장합니다. 

**(b)** (a)의 결과를 보고 optimal한 lambda값 (이 경우엔 $\sigma$)을 찾아서 $\hat{f}$ 를 구하고 주어진 $f$와 비교해봅시다.

**(c)** simulated data에 대해서 bandwidth에 따라 fitted line이 어떻게 변화하는지 관찰하고 (a)의 결과와 비교해서 설명해보세요!