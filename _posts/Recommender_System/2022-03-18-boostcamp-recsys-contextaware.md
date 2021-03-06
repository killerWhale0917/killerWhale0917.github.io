---
title:  "[Recommender System] Context-aware Recommendation 개요"
excerpt: "컨텍스트 기반 추천시스템이 무엇이고, 어떤 데이터를 사용하는지 그 개요에 대해서 살펴보자"

categories:
  - RecSys
tags:
  - [AI, Naver, BoostCamp, Recommender System]
toc: true
toc_sticky: true
use_math: true

date: 2022-03-18 00:00:00
last_modified_at: 2022-03-18 00:00:00
---
📌 **알립니다!**<br>
이번에 작성되는 글은 **네이버 부스트캠프 AI Tech**를 수강하며 정리하는 글입니다.<br>
여기서 존재하는 강의 자료의 출처는 네이버 부스트코스/캠프에게 있습니다.
{: .notice--info}

# Context-aware Recommendation

컨텍스트를 기반으로 한 추천이 기존에 다루었던 협업필터링과 어떻게 다른지 살펴보고, 컨텍스트 기반 추천이 어떻게 발전되었는지 간단하게 살펴보자.

기존 추천시스템에서는 다음 3가지 정보를 사용해서 추천을 진행하였다.

- 유저 관련 정보
- 아이템 관련 정보
- 유저-아이템 상호작용 정보

Matrix Factorization은 유저와 아이템의 상호작용 정보를 2차원 행렬로 표현했는데, 이 행렬에 사용되는 정보는 유저의 ID, 아이템의 ID, 그리고 유저와 아이템의 상호작용 정보였다. 이렇게 되면 유저나 아이템이 갖는 고유한 특징들을 모두 예측에 사용하지 않게 된다.

그래서 컨텍스트 기반 추천시스템은 유저와 아이템 간의 상호작용 뿐만아니라, 아이템이나 유저가 갖는 컨텍스트(맥락)정보도 함께 반영하고자 하였다.

## 활용 예시

**Click-Through Rate(CTR) Prediction**

CTR예측은 유저가 주어진 아이템을 클릭할 확률을 예측하는 문제이다. 예측하는 값은 **[클릭한다, 클릭하지 않는다]** 2가지 이므로 이진 분류문제에 해당한다. 그래서 클릭할 확률을 예측하기 위해서는 값을 확률로 바꿔주는 과정이 필요하다. 모델에서 출력한 실수 값을 시그모이드 함수에 통과시켜서 [0, 1] 사이의 값으로 만들었다.

CTR예측은 주로 광고분야에서 많이 사용된다. 그 이유는 광고 추천을 잘하는 것은 곧 수익으로 다가오기 때문이다. 컨텍스트 기반 추천시스템을 사용할 때는 광고가 노출된 상황의 다양한 유저와 광고, 컨텍스트 피처를 모델의 입력변수로 넣어주었다. 

컨텍스트 기반 추천시스템은 유저 ID가 존재하지 않는 데이터도 다른 유저나 컨텍스트 피처를 사용해서 예측하는 것을 가능하게 해주었다. 실제로 현업에서는 유저 ID를 피처로 사용하지 않는 경우가 많다고 한다.

**이진 분류 문제 - 로지스틱 회귀**

먼저 <로지스틱 회귀를 사용한 기본 모형> 에 대해 살펴보자.
    
$$
logit(P(y=1\mid x)) = \left( w_0 + \sum_{i=1}^{n}w_ix_i \right), \quad w_i\in\R
$$
    
추천 시스템에서는 상호작용 정보를 입력으로 사용하는 것이 중요한데, 위의 수식은 상호작용 정보를 입력으로 사용할 수 가 없었다. 그래서 변수간의 상호작용을 고려한 Polynomial Model이 고안되었다.

입력변수간의 상호작용을 고려한 <Polynomial Model>
    
$$
logit(P(y=1\mid x))=\left(w_0+\sum_{i=1}^{n}w_ix_i+\sum_{i=1}^{n}\sum_{j=i+1}^{n}w_{ij}x_ix_j \right), \quad w_i, w_{ij}\in\R
$$

기존의 입력변수 하나 $x_i$ 만 고려하던 것에 비해 입력변수 2개 $x_, x_j$ 에 대해서 상호작용 정보를 학습할 수 있도록 추가로 구성하였다. 이렇게 Polynomial Model은 강제로 상호작용 정보를 학습할 수 있도록 만들었지만, 학습에 필요한 파라미터의 수가 급격하게 증가하게 되는 단점이 있다. 그래서 이 문제를 해결하기 위해 FM과 FFM이 고안되었다.

## 컨텍스트 기반 추천시스템이 사용하는 데이터

입력데이터(feature)는 하나의 벡터로 표현하기 위해서 임베딩 과정을 거친다. 이때 2가지 방법으로 표현할 수 있는데 하나는 Sparse한 방법, 다른 하나는 Dense한 방법이다. 데이터(feature)를 임베딩 벡터를 표현하기 전에 어떤 데이터가 있는지 간단히 알아보자.

- Dense Feature: 벡터로 표현했을 때, 비교적 작은 공간에 밀집되어 분포하는 수치형 변수
    - ex. 유저-아이템 평점, 기온, 시간
- Sparse Feature: 벡터로 표현했을 때, 비교적 넓은 공간에 분포하는 범주형 변수
    - ex. 유저ID, 아이템ID, 요일, 분류, 키워드, 태그

CTR 예측문제에서 사용되는 데이터를 구성하는 요소는 대부분 Sparse Feature이다. 이 feature들을 원핫 인코딩으로 진행하기에는 차원의 개수만큼 벡터의 크기가 커지기 때문에 파라미터의 수가 너무 커질 수 있는 단점이 존재한다. 그렇기 때문에 feature 임베딩 과정을 거쳐서 Dense 한 값을 만들어서 예측해야 한다. (Item2Vec, Latent Dirichle Allocation, BERT)

## 컨텍스트 기반 추천시스템의 발전과정

- ~1990 : 로지스틱 회귀, 서포트 벡터 머신
-  1999 : Matrix Factorization 의 출현
-  2008 : Context-aware Recommendation 이라는 개념의 출현
-  2010 : Factorization Machine의 출현
-  2016 : Field-arae Factorization Machine 의 출현