---
title:  "[Recommender System] 협업필터링 개요"
excerpt: "다른 유저의 정보를 이용해서 추천을 진행하는 협업필터링과 이웃기반 협업필터링인 NBCF에 대해서 알아보자"

categories:
  - RecSys
tags:
  - [AI, Naver, BoostCamp, Recommender System]
toc: true
toc_sticky: true
use_math: true

date: 2022-03-14 05:00:00
last_modified_at: 2022-03-14 05:00:00
---
📌 **알립니다!**<br>
이번에 작성되는 글은 **네이버 부스트캠프 AI Tech**를 수강하며 정리하는 글입니다.<br>
여기서 존재하는 강의 자료의 출처는 네이버 부스트코스/캠프에게 있습니다.
{: .notice--info}

# Collaborative Filtering

![image](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Collaborative_filtering.gif/300px-Collaborative_filtering.gif){: .align-center width="50%"}
<p align="center"><i>Process of Collaborative Filtering from wikipedia</i></p>

## CF 문제 정의

**협업필터링**(Collaborative Filtering, CF)는 많은 유저들로부터 얻은 기호정보를 이용해서 유저의 관심사를 자동으로 예측하는 방법이다. 협업은 **다수의 의견을 사용해서 추천**을 하기 때문에 붙여지게 되었다.

협업필터링은 *"많은 유저와 아이템 정보가 있을수록 협업의 효과는 커지고 추천은 정확하게 이루어질 것이다"* 라는 가정으로부터 시작되었고, 최종목적은 **유저 $u$ 가 아이템 $i$ 에 부여할 평점을 예측하는 것**이다.

협업필터링이 이루어지는 과정을 살펴보자.

1. 주어진 데이터를 활용해서 **유저-아이템 행렬**을 생성한다.
2. 유사도 평가 기준을 정해서 유저-유저, 아이템-아이템의 유사도를 측정한다.
3. 주어진 평점과 유사도를 사용해서 행렬의 비어있는 값인 평점정보를 예측한다.

## CF 원리

유저A와 비슷한 취향을 가진 유저 B는 선호하는 아이템이 비슷하다고 생각해볼 수 있다. 반대로 유저A 가 선호하지 않는 아이템도 유저B 도 선호하지 않을 것이다. 이런 협업필터링은 TF-IDF와 달리 **아이템의 특징을 전혀 활용하지 않음에도, 좋은 추천 성능을 보인다**.

## CF의 분류

### NBCF: Neighborhood-based CF

- [User-based NBCF](#user-based-cf)
- [Item-based NBCF](#item-based-cf)

### MBCF: Model-based CF

- [Non-parametric (KNN, SVD)](https://killerwhale0917.github.io/recsys/boostcamp-recsys-knncf/)
- [Matrix Factorization](https://killerwhale0917.github.io/recsys/boostcamp-recsys-svdmf/)
- [Deep Learning](https://killerwhale0917.github.io/recsys/boostcamp-recsys-dlmlp/)

### Hybrid CF

- Content-based Recommendation과 CF의 결합

<br/>

# Neighborhood-based CF

## User-based CF

**유저 기반의 협업필터링**(UBCF)는 두 유저가 얼마나 유사한 아이템을 선호하는지의 정보를 사용한다. UBCF는 먼저 유저간의 유사도를 구하고 타겟 유저와 유사도가 높은 유저들이 선호하는 아이템을 추천한다. 유사도를 구하는 4가지 방법은 [여기](https://killerwhale0917.github.io/recsys/boostcamp-recsys-knncf/#similarity-measure)에 작성되어 있다.

아래의 예시에서는 유저A와 유저B가 비슷한 취향을 갖기 때문에 유저B의 스타워즈에 대한 선호도는 유저A와 비슷하게 높을 것이라고 예측해볼 수 있다.

![image](https://user-images.githubusercontent.com/91870042/158013811-0a94588e-b2b4-45a5-a2fe-f5aef0f5c40d.png){: .align-center width="90%"}

## Item-based CF

**아이템 기반의 협업필터링**(IBCF)는 두 아이템이 유저들로부터 얼마나 유사한 평점을 받았는지를 사용한다. 두 아이템간의 유사도를 구하고 타겟 아이템과 유사도가 높은 아이템중 선호도가 큰 아이템을 추천한다.

아래의 예시에서는 <스타워즈>가 <아이언맨>, <헐크>와 유사도가 높은 것을 알 수 있다. 반대로 <비포선라이즈>, <노팅힐>은 <스타워즈>와의 유사도가 낮다. 따라서 유저B의 <스타워즈>에 대한 평점은 <아이언맨>, <헐크>와 비슷하게 높을 것이라고 예측할 수 있다.

![image](https://user-images.githubusercontent.com/91870042/158014038-07d5914d-0fa5-4979-9170-491354f58686.png){: .align-center width="90%"}

## NBCF

UBCF, IBCF인 이웃기반 협업필터링 (NBCF)의 최종목적은 **유저 $u$ 가 아이템 $i$ 에 부여할 평점을 예측**하는 것이며 특징은 다음과 같다.

- 구현이 간단하고 이해가 쉽다.
- **아이템이나 유저가 계속 늘어날 경우, 확장성이 떨어진다**. [Scalability]
- **주어진 평점, 선호도 데이터가 적을 경우 성능이 저하된다**. [Sparsity]

위에서 말한 Scalability와 Sparsity는 Matrix Factorization으로 문제를 해결할 수 있다.

### Sparsity

사실, 유저-아이템 행렬의 대부분의 원소는 그 값이 비어있다. 그 이유는 모든 사용자가 아이템에 대해서 평가를 진행하지 않기 때문이며, 이러한 행렬을 희소행렬이라고 부른다.

NBCF를 적용하기 위해서는 비어있는 정도(`Sparse ratio`)가 99.5%를 넘지 않는 것이 좋다. 이보다 더 큰 값을 갖는 경우에는 `Matrix Factorization`을 사용해야 한다.
