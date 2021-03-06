---
title:  "신경망과 오차를 계산하는 손실함수"
excerpt: "퍼셉트론과 신경망의 개념이 어떻게 다른지, 신경망의 결과를 평가할 수 있는 손실함수인 평균 절댓값 오차(MAE), 오차제곱합(SSE), 평균 제곱 오차(MSE), 평균 제곱근 편차(RMSE), 크로스 엔트로피(+엔트로피와 쿨백-라이블러 발산)에 대해서 설명합니다."

categories:
  - DLBasic
tags:
  - [AI, Naver, BoostCamp, Math]
toc: true
toc_sticky: true
 
date: 2022-02-04
last_modified_at: 2022-06-17 02:00:00
---

![image](https://user-images.githubusercontent.com/91870042/174445155-a8ae761d-bd66-42dc-a7cd-959acf784e8e.png){: .align-center width="100%"}

# 신경망

[Deep Learning Basic의 2번째 게시물](https://killerwhale0917.github.io/dlbasic/DLBasic-2-MLP/)에서는 신경망의 기본이 되는 다층퍼셉트론에 대해서 살펴보았고, [3번째 게시물](https://killerwhale0917.github.io/dlbasic/DLBasic-3-activation-function/)에서는 활성함수에 대해서 알아보았습니다. 이제 신경망을 이해할 준비는 모두 완료되었습니다. 신경망이 다층퍼셉트론과 다른 것은 사실 하나 밖에 없습니다. 다층퍼셉트론은 활성함수로 step function, 계단함수를 사용하여 0 또는 1의 값만 전달한다는 것이고, 신경망은 sigmoid, ReLU와 같은 함수를 사용하여 실수값을 전달하게 됩니다.

![image](https://user-images.githubusercontent.com/91870042/174444064-42701f7c-43ba-4e0a-b566-0b633ea0b442.png){: .align-center width="100%"}

이제 퍼셉트론에서 시작하여 신경망의 구조를 모두 살펴보았습니다! 그렇다면 만들어진 신경망이 얼마나 우리가 만든 문제를 잘 맞추는지 평가하기 위한 도구가 필요합니다. 바로 이 도구가 `손실함수(loss function)`입니다.(목적함수 라고 불리는 경우도 있습니다). 바로 밑에서는 손실함수의 종류에 대해서 살펴보겠습니다.

<br>

# loss function

손실함수에 대해서 설명하기 위해 하나의 흔한 문제를 가져오겠습니다. 선형회귀 문제로 2차원 좌표평면 공간에 흩뿌려진 점들을 가장 잘 대표하는 직선을 찾는 문제입니다. 그림으로 표현하면 아래와 같이 나타내볼 수 있습니다.

![image](https://user-images.githubusercontent.com/91870042/174445475-f82c439e-b86d-452d-9930-c4b21b5719a1.png){: .align-center width="50%"}

어떻게 학습을 잘 시켜서 위와 같이 점들을 대표하는 빨간 직선을 만들었다고 합시다. 그렇다면 이 직선이 얼마나 잘 그어진 것인지 평가할 명확한 기준이 필요합니다. 간단하게 생각해보면 각 점들이 직선에서 얼마나 떨어져있는지 거리의 평균으로 평가를 해볼 수 있습니다.

$$
\text{loss} = \frac{1}{n}\sum_{i=1}^{n} | f(x_i) - y_i |
$$

- $\text{loss}$ : 손실함수의 결과값인 오차
- $n$ : 좌표평면에 있는 파란색 점들의 수
- $f$ : 회귀선인 빨간 직선
- $x_i$ : $i$ 번째 점의 x 절편
- $y_i$ : $i$ 번째 점의 y 절편

위에서 정의한 식이 손실함수이며, 문제나 상황에 맞게 손실함수를 선택할 수 있습니다. 위의 식은 실제로도 사용되는 손실함수로서 `평균 절대값 오차 (Mean Absolute Error, MAE)`라고 합니다. 이제부터는 MAE 이외에 자주 사용되는 손실함수의 종류에 대해서 살펴보겠습니다.

<br>

## 🐥 평균 제곱 오차

평균 제곱 오차보다 MSE 또는 Mean Squared Error로 잘 알려진 유명한 손실함수입니다. 위의 MAE와 다른 점은 절댓값 대신에 제곱을 해주었다는 것입니다. MAE는 모든 오차제곱합을 더해주는 손실함수인 **오차제곱합(SSE)**의 한계를 극복한 함수입니다. 단 하나의 튀는 값으로 인해서 전체 오류값이 올라가는 것을 방지해줄 수 있다는 것이 장점입니다.

$$
\text{loss} = \frac{1}{n}\sum_{i=1}^{n} (y_i - \hat{y_i})^2
$$

- $n$ : 데이터의 수
- $y_i$ : 실제 정답
- $\hat{y_i}$ : 예측값

이 MSE는 연속형 데이터를 사용한 회귀분석에서 자주 사용됩니다. 위에서 살펴본 선형회귀 문제에서도 단 하나의 큰 오류가 존재하더라도 평균을 사용하여 전체적인 오류를 파악할 수 있도록 도와줄 수 있기 때문에 MSE를 사용하게 됩니다. 모든 지점에서 미분이 가능하다는 장점이 존재합니다!

반대로, 단점도 있습니다. 예측값과 실제값의 차이를 제곱하기 때문에 값이 매우 커질 수 있는 단점을 갖습니다. 이는 방대한 데이터셋을 가진 딥러닝에서는 연산량을 크게 증가시킬 수 있는 요인이 되기도 합니다. 또한 제곱 연산으로 인해 오차의 값이 0과 1사이의 실수 값을 갖는다면 더 작게, 1이상이라면 더 크게 반영되는 왜곡이 존재합니다.

<br>

## 🐤 평균 제곱근 편차

평균 제곱근 편차(Rooted Mean Squared Error, RMSE)는 위의 MSE에 루트를 씌워준 형태입니다.

$$
\text{loss} = \sqrt{\frac{1}{n}\sum_{i=1}^{n} (y_i - \hat{y_i})^2}
$$

- $n$ : 데이터의 수
- $y_i$ : 실제 정답
- $\hat{y_i}$ : 예측값

평균을 취한 MSE에 대해 다시 루트를 취해주기 때문에 값의 왜곡을 줄일 수 있는 장점이 있습니다. 이는 추가로 딥러닝의 큰 데이터셋에 대해 오차를 계산할 때 값이 매우 커지는 것을 방지해줄 수 있는 역할을 해줄 수도 있습니다. 하지만 단점으로 루트를 취하기 때문에 그래프가 미분 불가능한 지점을 갖게 됩니다.

<br>

## 🐣 크로스 엔트로피

실제로 많이 사용되는 손실함수인 `크로스 엔트로피(Cross Entropy, CE)`입니다. 개인적으로 처음에 개념적인 이해가 어려웠던 함수입니다. 말만 봐도 어려운 크로스 엔트로피에 대해서 알기 전에는 엔트로피에 대한 개념을 이해하고 있어야 합니다.

### ✅ 정보량과 엔트로피

![image](https://user-images.githubusercontent.com/91870042/174448730-00419612-84fe-459d-9b2f-3c41e4132b1c.png){: .align-center width="40%"}

많은 곳에서 엔트로피는 **불확실성** 이라고 표현합니다. 이때의 불확실성은 우리가 예측하고자 하는 사건에 대한 불확실성이며 해당 사건이 발생하기 어려움을 의미합니다. 예를 들어 2개의 게임을 한다고 가정합시다. 하나는 동전을 던져 앞면/뒷면을 예측하는 게임이고 다른 하나는 주사위를 굴려 어떤 수의 눈금이 나올지 예측하는 게임입니다. 당연히 주사위를 굴려서 눈금을 맞추는 게임이 어려우며, 불확실성이 크다고 할 수 있습니다.

- 주사위 게임 : 불확실성이 높다 = 엔트로피 값이 크다.
- 동전 게임 : 불확실성이 낮다 = 엔트로피 값이 낮다.

조금더 생각해보면, 엔트로피 값은 확률값의 역수라고 생각할 수 있습니다. 주사위 게임의 확률역수는 6이며, 동전게임의 확률역수는 2입니다. 이런 개념이 ***정보량**을 계산하는 수식에 그대로 적용되어 있습니다.

$$
I(X) = \lg \frac{1}{P(X)}
$$

- $I$ : 정보량
- $\lg$ : $\log_2$


**정보량**<br>
정보량은 해당 사건을 특정짓기 까지 필요한 비트의 수라고 볼 수 있습니다. 동전 던지기의 경우 단 1개의 비트(1과 0)을 사용하여 앞면과 뒷면을 구분지을 수 있습니다. 반면에 주사위는 사건이 총 6개 이며 각각을 구분짓기 위해서는 최소 3개의 비트가 필요합니다. 바로 이 3이라는 값이 정보량이라고 볼 수 있습니다. 현재는 정수단위로 나누어서 정보량을 표현하였지만, $\log_2$를 사용하여 실수단위의 정확한 정보량을 계산하는 것이 가능합니다.
{: .notice--success}

그런데 지금은 모든 사건의 등장확률이 같은 경우를 다뤘습니다. 하지만 실제 현실은 다릅니다. 각 사건이 발생활 확률이 다르기 때문에 발생활률도 함께 고려한 entropy 계산식이 필요합니다. 이런 경우, 위의 정보량을 계산하는 수식에 **각 사건의 등장확률을 곱하여 표현**해볼 수 있습니다. 또한 지금까지 정보량의 단위가 1비트였다면 자연상수 $e$ 가 단위인 `내트`로 계산해보겠습니다.

$$
H_p[X] = \mathbb{E}[I(X)] = -\sum_{i=1}^{n}p(x_i)\ln(p(x_i))
$$

- $H[X]$ : 계산된 엔트로피 값
- $\mathbb{E}$ : 기댓값
- $p(x_i)$ : 사건 $x_i$가 등장할 확률

엔트로피를 구하는 식에 로그가 사용되는 이유는 정보량의 계산만을 위한 것은 아닙니다. 정보량은 0보다 크고, 특정 사건의 발생확률이 100%인 것은 정보량이 0이어야 합니다. 또한 독립적인 두 사건의 정보량의 합은 각 사건의 합과 동일해야 합니다. 이 모든 성질을 만족하는 것이 로그이기에 엔트로피의 개념에서 로그가 사용되는 것입니다.

이렇게 짧게 엔트로피와 정보량의 개념에 대해서 알아보았습니다. 이제 본론인 크로스 엔트로피에 대해서 알아봅시다! 😅

---

크로스 엔트로피는 2개의 확률 분포에 대해서 사건 $X$가 갖는 정보량이라고 정의합니다. 서로 다른 두 확률분포를 사용하기에 "크로스" 엔트로피라고 합니다. 수식은 엔트로피와 유사하지만, 2개의 확률분포가 등장한다는 것에 차이를 둘 수 있습니다.

$$
H_{p,q}(X) = -\sum_{i=1}^{n}p(x_i)\ln(q(x_i))
$$

- $p$ : 실제 확률 분포
- $q$ : 신경망을 통해서 예측된 확률 분포

예를 들어, 정사면체의 조금 신기한 주사위가 있다고 가정합시다. 이 신기한 주사위는 각 눈금이 나올 확률이 1은 10%, 2는 20%, 3은 30%, 4는 40%로 일반적인 주사위와는 다릅니다. 하지만, 우리는 이 주사위의 각 눈금이 나올 확률이 모두 25%라고 예측하였다고 합시다. 이 경우, 엔트로피와 크로스 엔트로피를 계산하면 다음과 같습니다.

$$ 
\begin{aligned}
    \text{entropy} &= -[0.1\ln(0.1) + 0.2\ln(0.2) + 0.3\ln(0.3) + 0.4\ln(0.4)] = 1.279 \\
    \text{cross entropy} &= -[0.1\ln(0.25) + 0.2\lg(0.25) + 0.3\lg(0.25) + 0.4\lg(0.25)] = 1.386
\end{aligned}
$$

> *그래서 cross entropy 를 계산하는 것이 실제값과 예측값간의 오차를 어떻게 계산한다는 것인가?*

### ✅ 쿨백-라이블러 발산
이 질문에 답하기 위해서는 `쿨백-라이블러 발산(KL-Divergence)`라는 개념을 이해하고 있어야 합니다. 지금 당장 쿨백-라이블러 발산에 대해서 자세하게 소개하지는 않지만 한줄로 말하자면 **두 확률분포의 차이를 계산하는 방법**이라고 할 수 있습니다. 이산확률 변수일 때의 쿨백-라이블러 발산의 식은 다음과 같습니다.

$$
\begin{aligned}
D_{KL}(P\|Q) &= \sum_{i=1}^{n}P(i)\log\frac{P(i)}{Q(i)}\\
& = -\sum_{i=1}^{n}P(i)\log Q(i) -(-\sum_{i=1}^{n}P(i)\log P(i))\\
& = H(P, Q) - H(P)
\end{aligned}
$$

어디서 많이 본 식이 쿨백-라이블러 발산에 포함되어 있습니다. 바로 엔트로피의 개념과 크로스 엔트로피의 개념이 모두 들어가있습니다. 두 확률분포가 유사하려면 KL발산 값이 작아야 하며 그렇기 위해서는 먼저 앞에오는 크로스 엔트로피의 값이 작아져야만 합니다. 따라서, 손실함수인 크로스 엔트로피를 통해 확률분포가 비슷해지는 방향으로 학습을 하도록 유도할 수 있습니다!!

<br>

이렇게 해서 손실함수의 개념과 그 종류에 대해서 살펴보았습니다. 특히 크로스 엔트로피의 경우 필요한 선수 지식이 많아 꽤 복잡하게 많이 느껴졌습니다. 하지만 많이 사용되는 손실함수이며, 마찬가지로 그 변형이 많아 확실한 이해를 하는 것이 중요합니다. 다음은 딥러닝의 학습 방법론인 **경사하강법**에 대해서 알아보겠습니다🔥

<br>

# References

[🎨 헤더 이미지 소스](https://www.analyticsvidhya.com/blog/2019/08/detailed-guide-7-loss-functions-machine-learning-python-code/)

[🌏 만년필잉크의 데이터 분석 지식 저장소 : 딥러닝-5.3. 손실함수(4)-교차 엔트로피 오차(CEE)](https://gooopy.tistory.com/63?category=824281)

[🌏 Deep Play : Cross-entropy의 이해: 정보이론과의 관계](https://3months.tistory.com/436)

[🌏 위키백과 : 쿨백-라이블러 발산](https://ko.wikipedia.org/wiki/%EC%BF%A8%EB%B0%B1-%EB%9D%BC%EC%9D%B4%EB%B8%94%EB%9F%AC_%EB%B0%9C%EC%82%B0)