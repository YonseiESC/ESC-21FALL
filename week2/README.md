## ๐ป Programming HW description ๐ป

์์ํ๊ธฐ ์ ์ `hw1.Rmd` ํ์ผ๊ณผ `home1-part1-data.R`, `home1-part2.data.R` ๋ฐ์ดํฐ๋ฅผ ๋ค์ด๋ฐ์์ ๊ฐ์ working directory์ ์์น์์ผ์ฃผ์ธ์.

์ด description๊ณผ Rmd ํ์ผ์ ํจ๊ป ์ฝ์ด๊ฐ๋ฉด์ `# TODO` ๋ผ๊ณ  ๋ ๋ถ๋ถ์ ์ฑ์์ ๋ธํธ๋ถ์ ์์ฑํด๋ด์๋ค.

(โ๏ธreference : University of Washington STAT435 Intro to Statistical Learning HW1)

๐ ์ผํ ๋ณด๋ฉด ๋ฌธ์ ๊ฐ ๊ต์ฅํ ๋ง์๋ณด์ด์ง๋ง ๋ง์ `#TODO` ๋ผ๊ณ  ๋์ด์๋ ๋ถ๋ถ์ ๊ทธ๋ฆฌ ๋ง์ง ์์ต๋๋ค! ๊ฒ๋จน์ง ๋ง์ธ์:)

๐์ ๊ฐ ํ๋ ์์ (๋ง์  ๋ชป๋ฐ์..)๋ฅผ ๋ณํํ ๊ฒ์ด๊ธฐ ๋๋ฌธ์ ์ผ๋ง๋ ์ง ๋ ๋์ ๋ฐฉ๋ฒ์ด ์์ ์ ์์ต๋๋ค. Rmd ํ์ผ๊ณผ ์ด description์ ๊ฐ์ด๋๋ผ์ธ์ด๊ณ  ๋ณธ์ธ์ด ๋ ํจ์จ์ ์ธ ๋ฐฉ์์ด๋ ๋ค๋ฅธ ๋ฐฉ์์ผ๋ก ์ง๊ณ  ์ถ๋ค๋ฉด ์ผ๋ง๋ ์ง ๊ฐ๋ฅํฉ๋๋ค!

๐์์๋ต์์ ์์์ผ์ ์๋ก๋ํ๊ฒ ์ต๋๋ค!

### Part 1. Implement and experience KDE on your own!

๋จผ์  ๊ฐ๋จํ ์๋ฎฌ๋ ์ด์๋ ๋ฐ์ดํฐ๋ฅผ ์์ฑํฉ๋๋ค. sin(x) ํจ์์ Gaussian noise๋ฅผ ๋ํ ๋ฐ์ดํฐ๋ฅผ ์์ฑํฉ๋๋ค.

**(a)** R์ ๋ด์ฅ๋ ํจ์์ธ `ksmooth` ๊ฐ ์ด๋ป๊ฒ ์๋ํ๋์ง ๋ด์๋ค! Gaussian kernel์ ์ฌ์ฉํ  ๋์ Uniform kernel (box kernel)์ ์ฌ์ฉํ  ๋ ์ด๋ป๊ฒ ๋ค๋ฅผ๊น์? ๊ฒฝ์ฐ์ ๋ฐ๋ผ bandwidth๋ฅผ ์ค์ด๋ฉด uniform kernel๊ฐ ๋๊ธฐ๋ ํ์๋ ๋ณผ ์ ์์ต๋๋ค.

**(b)** ์ด์   ์ง์  kernel smoothingํ๋ ํจ์๋ฅผ ๋ค์๊ณผ ๊ฐ์ด ๊ตฌํํด๋ด์๋ค. 

`ksmooth.train(x.train, y.train, bandwidth=0.5)` with output `x.train`, `yhat.train` (`x.train` ์ ์ ๋ ฌ๋์ง ์์๋ค๊ณ  ๊ฐ์ ํฉ๋๋ค.)

์ธ์๋ ๋ฐฐ์ ๋ Nadaraya-Watson average์ Gaussian kernel์ ์ด์ฉํ๋ฉด ๋ฉ๋๋ค.

์ค์ฌ์ ๊ธฐ์ค์ผ๋ก quartile (75%)์ ํด๋นํ๋ density๊ฐ +/- 0.25*bandwidth ๋ด์ ๋ค์ด์ค๋๋ก scaling ํด์ค๋๋ค. (์ด๊ฑด ๋์ด์์)

**(c)** (a)์์ `ksmooth` ๋ฅผ ์ด์ฉํด์ ํผํํ๋ $\hat{f}$ ๊ณผ ์ฌ๋ฌ๋ถ์ `ksmooth.train` ์ ์ด์ฉํด ํผํํ ๊ฒ์ด ๋น์ทํ์ง ์๊ฐํํด์ ๋น๊ตํด๋ด์๋ค!

**(d)** ISLR์ Wage dataset์ ๋ถ๋ฌ์ต๋๋ค. (`home1-part1-data.R`)

(์๋๋ `ksmooth.predict` ๋ ๊ตฌํํ์ฌ test set์์๋ evaluation์ ํด์ผ ํ์ง๋ง ์ด ๊ณผ์ ์์ interpolation์ ํด์ผ ํ๋ ๋ฑ ๋ฒ๊ฑฐ๋ก์์ง๊ธฐ ๋๋ฌธ์ ์ด๋ฒ์ train data๋ง ์ฌ์ฉํฉ๋๋ค!)

๋ฐ์ดํฐ์ scatterplot์ ๊ทธ๋ ค๋ณด๊ณ  ๊ตฌํํ ํจ์๋ก ํผํํ์ ๋ ์ด๋ป๊ฒ ํจ์๊ฐ ์ถ์ ๋๋์ง ํ์ธํด๋ด์๋ค.

๊ทธ๋ฐ ๋ค bandwidth๊ฐ 1, ..., 10๊น์ง๋ก ๋์ด๋จ์ ๋ฐ๋ผ training error๋ ์ด๋ป๊ฒ ๋ณํ๋์ง ๋ด์๋ค.



### Part 2. Optimal Bandwidth

์ด๋ฒ์๋ bandwidth์ ๋ฐ๋ฅธ bias-variance tradeoff๋ฅผ ๋ด์๋ค.

Training sample $(x_1, y_1), ..., (x_n, y_n)$.

Predictor values $x_1, ..., x_n$ are considered fixed (not random).

Response values $y_i=f(x_i)+\epsilon_i$, with $\epsilon_1, ..., \epsilon_n$ independent, $E(\epsilon_i)=0, Var(\epsilon_i)=\sigma^2$

Define $\textbf{y}=(y_1, ..., y_n), \textbf{f}=(f(x_1), ..., f(x_n))$, etc.

$K_\lambda(x)$ : Kernel with bandwidth parameter $\lambda$ controlling the amount of smoothing.

Define $\textbf{W}$ : n x n weight matrix with $\textbf{W}_{i,j}=\dfrac{K_\lambda(x_i-x_j)}  {\sum_j K_\lambda(x_i=x_j)}$ 

Then $\hat{f}=Wy$.

**(a)** ์์ specification์ ๋ฐ๋ผ์ W๋ฅผ ๋ง๋ค๊ณ  (Part1์์์ ๊ฑฐ์ ๋์ผํฉ๋๋ค!) `sigma=seq(from=0.01, to=2, by=0.01)` ์ ๋ฐ๋ผ์ variance, bias^2, sum(MSE)๋ฅผ ์ ์ฅํฉ๋๋ค. 

**(b)** (a)์ ๊ฒฐ๊ณผ๋ฅผ ๋ณด๊ณ  optimalํ lambda๊ฐ (์ด ๊ฒฝ์ฐ์ $\sigma$)์ ์ฐพ์์ $\hat{f}$ ๋ฅผ ๊ตฌํ๊ณ  ์ฃผ์ด์ง $f$์ ๋น๊ตํด๋ด์๋ค.

**(c)** simulated data์ ๋ํด์ bandwidth์ ๋ฐ๋ผ fitted line์ด ์ด๋ป๊ฒ ๋ณํํ๋์ง ๊ด์ฐฐํ๊ณ  (a)์ ๊ฒฐ๊ณผ์ ๋น๊ตํด์ ์ค๋ชํด๋ณด์ธ์!

## ESL exercise 6.8

๋ฌธ์ ์์ ์ค๋ชํด์ฃผ๋ฏ์ด Joint ๋ถํฌ๊ฐ ๋ gaussian kernel์ ๊ณฑ ํํ๋ก ํํ๋๋ค๋ ๊ฒ์ ์ด์ฉํด์ x๊ฐ given์ผ ๋ y์ ์กฐ๊ฑด๋ถ ๋ถํฌ์ ํ๊ท ์ ๊ณ์ฐํด๋ณด์ธ์.

๊ณ์ฐ ํ์ ๊ฒฐ๊ณผ๊ฐ Nadaraya-Watson estimator์ ๊ฐ์ ํํ๋ฅผ ๊ฐ์ต๋๋ค.

classification์ ๊ฒฝ์ฐ์๋, y์ kernel์ gaussian์ด ์๋๋ผ ํด๋น class๋ฉด 1, ๊ทธ๋ ์ง ์์ผ๋ฉด 0์ด ๋๋ ํจ์๋ก ๋ฐ๊พธ๊ณ  ์์ ๊ฐ์ ๊ณผ์ ์ ๋ฐ๋ณตํ๋ฉด ๋ฉ๋๋ค. 
