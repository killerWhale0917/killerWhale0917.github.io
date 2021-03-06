---
title:  "딥러닝에 대한 소개"
excerpt: "딥러닝과 헷갈리기 쉬운 AI와 Machine Learning 사이의 관계에 대해서 설명하고 딥러닝의 기본 구성 요소에 대해서 설명합니다."

categories:
  - DLBasic
tags:
  - [AI, Naver, BoostCamp]
toc: true
toc_sticky: true
 
date: 2022-02-01
last_modified_at: 2022-06-17 00:00:00
---
📌 **알립니다!**<br>
이번에 작성되는 글은 **네이버 부스트캠프 AI Tech**를 수강하며 정리하는 글입니다.<br>
여기서 존재하는 강의 자료의 출처는 네이버 부스트코스/캠프에게 있습니다.
{: .notice--info}

# Introduction

이번에 처음으로 딥러닝을 공부하게 되면서 인공지능이라는 것이 어떻게 학습하는지 어째서 사람보다 더 좋은 판단을 내릴 수 있는지가 많이 궁금해졌습니다. 딥러닝에 대해서 찾아보면 **인공지능, 딥러닝, 머신러닝**에 대한 용어들이 자주 등장하는데, 이들이 서로 어떤 관계를 맺고 있는지 살펴보고 딥러닝을 연구하는 좋은 사람이 되기 위해서는 어떤 능력들이 필요한지 살펴봅시다.

이번 글부터, 순서대로 딥러닝에 대한 기초 이론들을 간단하게 살펴볼 예정입니다. 글 내용 중에서 틀린 부분이 있다면 언제든지 댓글이나 issue로 말씀해주시면 바로 수정하도록 하겠습니다.

## 🌟 좋은 딥러너가 되기 위한 자격

![image](https://user-images.githubusercontent.com/91870042/174116005-e82c3d06-0112-489b-984e-3a69547ed743.png)


- Implementation Skills (Tensorflow, Pytorch)
- Math Skills
- Knowing a lot of recent Papers

좋은 딥러닝 연구가가 되기 위해서는 위의 3가지 요소가 많이 강조됩니다. 첫 번째로 딥러닝을 구현할 구현능력이 중요합니다. 최신의 연구동향이 나와 있는 논문을 읽고 해당 논문에 나온 딥러닝 구조를 딥러닝 프레임워크인 Tensorflow나 PyTorch를 사용해서 코드로 작성하는 것은 어렵지만 중요한 능력입니다.

다음으로는 딥러닝의 이론들이 선형대수학의 행렬 또는 미분을 사용한 연산이 매우 많이 등장하기 때문에 이와 관련된 수학적 지식이 필요하며 확률론에 기반을 둔 이론들도 많이 등장합니다. 따라서 이 2가지 수학적 지식에 대해서 깊은 이해가 있을수록 딥러닝에 대한 이해가 쉬워질 수 있습니다.

마지막으로 최신의 연구 동향을 얻기 위해서 많은 논문을 읽고 또 알고 있는 것이 중요합니다. 딥러닝이 등장한 지 오랜 시간이 흐르지 않았음에도 정말 빠른 발전들을 이루고 있습니다. 지금 이 시간에도 딥러닝의 발전은 빠른 속도로 이루어지고 있기 때문에 이 경향을 가장 쉽게 알 수 있는 논문들을 읽는 것이 중요합니다.

## 🔗 AI, ML, Deep Learning의 관계
![image](https://user-images.githubusercontent.com/91870042/144704573-50928379-2c3a-435a-9f71-338be2efc9a9.png){: .align-center width="100%"}

인공지능(AI)와 머신러닝(ML), 딥러닝(DL)과의 관계는 위의 그림으로 한 번에 나타내 볼 수 있습니다. 이 각각에 대해서 자세히 설명하면 다음과 같습니다.

1. Artificial Intelligence: 사람의 지능을 모방하는 것
2. Machine Learning: 데이터를 통해 학습시키는 것
3. Deep Learning: 머신러닝 중에서 사람의 뇌를 모방한 신경망(Neural Network) 모델을 사용해 학습하는 세부적인 분야

## 🎯 딥러닝의 기본 요소

이번에는 딥러닝을 구성하는 기본 요소에 대해서 알아봅시다. 딥러닝의 상위 개념인 머신러닝은 데이터를 기반으로 하여 학습시키는 것을 의미합니다. 마찬가지로 딥러닝 역시 `데이터`를 사용하여 학습을 진행합니다. 이제 이 데이터를 학습시킬만한 구조가 필요합니다. 이러한 구조를 `모델` 이라고 하며 모델에 따라서 학습을 잘하여 성능이 좋게 나올 수도 있으며 특정 데이터에 맞는 모델이 있을 수도 있습니다. 

이제 모델이 학습한 결과를 평가할만한 존재가 필요하며 그때 사용되는 것이 `손실함수`입니다. 손실함수는 현재 모델이 실제 정답과 얼마만큼의 오차를 두고 있는지 말을 합니다. 마지막으로 여기서 구한 오차를 사용하여 학습을 최적화시키는 `최적화 알고리즘`이 필요합니다. 간단하게 설명한 4가지의 구성요소를 통해서 딥러닝은 학습을 하게 됩니다. 아래에서 더 자세히 말씀드리겠습니다.

### Data

> "The data that the model can learn from"

데이터는 모델을 학습하는 데 필요한 것이라고 할 수 있습니다. 예를 들어서 개와 고양이를 분류하는 문제에 대해서는 개와 고양이의 수많은 사진들이 필요합니다. 이렇듯 데이터는 풀고자 하는 문제에 의존하게 됩니다. 특히 AI를 사용한 분야 중 CV(Computer Vision)에서는 풀고자 하는 문제에 대한 분류를 다음과 같이 5가지로 나누어볼 수 있습니다.
    
![image](https://user-images.githubusercontent.com/91870042/144704834-e01eec9f-ec99-4cc8-a8c8-62e41472eddd.png){: .align-center width="100%"}

- `Classification`: 주어진 데이터에 대해서 분류하는 문제 (개와 고양이 분류)
- `Semantic Segmentations`: 한 이미지에 대해서 픽셀로 분석하는 문제 (각 부분이 어떤 클래스에 속하는지 판단)
- `Detection`: 한 이미지 내에서 특정 사물에 대한 경계박스를 찾는 문제
- `Pose Estimation`: 사람의 행동이 주어졌을 때, 그 사람이 움직이는 정보를 Skeleton정보로 바꾸는 문제
- `Visual QnA`: 어떤 사진이 주어지고, 그 사진에 대한 질문이 주어졌을 때 답을 말하는 문제

이렇듯 특정 문제를 풀기 위한 AI를 학습시키기 위해서는 이 문제를 해결하기에 가장 좋은 관련된 데이터를 입력으로 넣어주는 것이 중요합니다. 예로, 야구게임 경기 예측문제에 대한 입력으로 야구경기 데이터가 아닌, 사용자의 쇼핑 이력 데이터를 준다면 제대로 학습을 진행할 수 없습니다.

### Model

> "The model how to transform the data"

모델은 위에서 말한 수많은 데이터를 이용해서 학습하는 데 필요한 것입니다. 예로, 이미지를 라벨로 바꾸어주는 문제를 생각해봅시다. 어떤 사물의 사진을 줬을 때, 그 사진의 제목을 설정해주는 신경망 구조가 모델입니다.

모델은 같은 데이터를 주더라도 모델에 따라서 더 좋은 결과, 나쁜 결과가 나올 수 있어 좋은 모델의 선택이 필요합니다. 하지만 단순히 성능을 비교해서 판단하기보다는 근거를 가지고 올바른 모델을 선택하는 것이 중요합니다.

![image](https://user-images.githubusercontent.com/91870042/144704950-a55c4c49-6bca-46a7-9ed1-bcfe91971561.png){: .align-center width="100%"}

### Loss Function

> "The loss function that quantifies the badness of the model"

손실함수는 어떤 모델을 통해서 나온 결과 값과 실제 값이 얼마나 유사한지 판단하는 기준입니다. 반대로 말하면 그 모델이 얼마나 안 좋은지 판단해볼 수도 있습니다. 다시 말해 손실함수는 그 모델이 얼마나 좋은 모델인지 나쁜 모델인지 판단하는 척도가 됩니다.

문제 유형에 따라서 자주 사용하는 손실함수가 있지만, 반드시 그 문제에는 해당 손실함수를 사용해야 한다는 것은 아닙니다. 주어진 문제의 상황에 맞는 손실함수를 사용하는 것이 모델을 올바르게 학습하는 데 중요합니다.

- Regression Task(회귀 문제): `MSE` loss function(Mean Squared Error)
- Classification Task(분류 문제): `CE`(Cross Entropy Loss)
- Probabilistic Task(확률 문제): `MLE`(=MSE, Maximum Likelihood Estimation)

왜 이 각각의 문제들이 저런 손실함수가 사용되는지, 그리고 이 손실함수들은 각각 무엇을 말하는지는 이후에 따로 정리하여 설명드리도록 하겠습니다.

### Optimization Algorithm

> "The algorithm to adjust the parameters to minimize loss"

딥러닝에 사용되는 여러 개의 숫자 값들을 이용하고, 이 값들 간의 행렬연산 또는 다른 수학적 연산을 통해서 결과를 예측하는데 이바지합니다. 이런 값들을 **파라미터**라고 부르며 이 값들을 문제를 잘 맞추도록 설정하는 것이 반드시 필요합니다.

최적화 알고리즘 또는 Optimizer는 손실함수를 통해 얻어낸 값(오차)을 최대한 줄이기 위해서 사용됩니다. 알고리즘에 따라 빠르게 오차를 줄여나갈 수도 있고, 천천히 줄여나갈 수 있습니다. 한정된 자원과 시간 속에서 빠른 학습속도와 높은 학습성능은 딥러닝의 학습에서 정말 중요한 요소 중 하나입니다. 그렇기에 각 문제에 맞는 최적화 방법을 선택해야 하며, 최적화 알고리즘들이 어떠한 방식으로 진행되는지 파악하는 것이 중요합니다.

대표적으로 사용되는 Optimizer에는 다음 개념들이 있습니다. 일단 한 번 이런 이름이 있구나 정도로만 이해하고 넘어가셔도 좋습니다😊 이후에 최적화 알고리즘에 대해서 자세하게 설명하겠습니다.

- SGD
- Momentum
- NAG
- Adagrad
- Adadelta
- Rmsprop
- Adam

아래의 영상은 딥러닝의 학습 과정을 그림으로 표현한 것입니다. 각 그래프는 손실함수를 좌표평면에 표현한 모습이며 손실함수의 값을 줄여야 하기 때문에 낮은 방향으로 진행되는 것이 최적화가 진행된다고 이해할 수 있습니다. 아래에서는 예시로 **Adadelta, NAG** 가 빠른 속도로 최적화를 진행하는 모습을 보이고 있습니다.

![optim_algs](https://user-images.githubusercontent.com/91870042/152749857-2dbc6550-1906-4226-abe4-5dd6030a3659.gif){: width="49%"} ![optim_algs2](https://user-images.githubusercontent.com/91870042/152749846-be0675a3-7194-462a-8973-75042d2a392b.gif){: width="49%"}

## 🚀 References

[🌏 Deep Learning, Historical Review](https://gngsn.tistory.com/103)
