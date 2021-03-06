---
title:  "[Recommender System] Word2Vec, Item2Vec"
excerpt: "아이템을 벡터로 표현하는 방법(Word2Vec)을 추천시스템에 적용한 Item2Vec에 대해서 알아보자"

categories:
  - RecSys
tags:
  - [AI, Naver, BoostCamp, Recommender System]
toc: true
toc_sticky: true
use_math: true
 
date: 2022-03-14 10:00:00
last_modified_at: 2022-03-14 10:00:00
---
📌 **알립니다!**<br>
이번에 작성되는 글은 **네이버 부스트캠프 AI Tech**를 수강하며 정리하는 글입니다.<br>
여기서 존재하는 강의 자료의 출처는 네이버 부스트코스/캠프에게 있습니다.
{: .notice--info}

# Word2Vec

임베딩과 워드 임베딩에 대해서 이해하고, 워드 임베딩의 대표적인 방법론인 `Word2Vec`에 대해서 알아보자

## 개요

### 임베딩

**임베딩**(Embedding)은 주어진 데이터를 낮은 차원의 벡터로 만들어서 표현하는 방법을 말한다. 이 벡터를 표현하는 방법에는 `Sparse Representation`과 `Dense Representation` 2가지 방법이 존재한다.

- **Sparse Representation**  
    임베딩한 벡터의 차원 수를 아이템 전체 가짓수와 동일하게 표현하는 것을 말한다. 임베딩된 벡터는 이진값으로만 구성되어 있으며, 특정 아이템에 해당하는 index만 1로 표현한다. 단점으로는 아이템의 개수가 많아질 수록 벡터의 크기가 너무 커져서 차원이 낭비되는 문제가 있다.  
    Ex. 면도기 = [0, 0, 0, ... , 1, 0], 가위 = [0, 1, 0, ... , 0, 0]

- **Dense Representation**  
    임베딩한 벡터의 차원 수가 아이템의 전체 가지수보다 훨씬 작게 만들어서 표현하는 것을 말한다. 벡터에 표현되는 값을 이진값으로 나타낼 수도 있지만, 주로 실수값으로 이루어진 벡터로 표현을 한다.  
    Ex. 면도기 = [0.2, 1.4, -0.4, 1.2, 0.3], 가위 = [-0.1, 0.5, 1.1, -1.0, 0.4]

### 워드 임베딩

워드 임베딩은 텍스트 분석을 위해서 **단어를 벡터로 표현하는 방법**을 말한다. 단어를 벡터로 표현하게 되면, 단어간의 유사도를 구하는 것이 가능해진다. 또한 비슷한 의미를 가진 단어일 수록 임베딩 공간에서는 서로 가깝게 위치하게 된다.

이렇게 단어를 임베딩으로 표현하기 위해서는 변환을 해주는 학습 모델이 필요해진다. MF도 유저와 아이템의 임베딩으로 볼 수 있고, 데이터로 부터 학습한 행렬이 임베딩이 되는 것이다.

### Word2Vec

![image](https://user-images.githubusercontent.com/91870042/158574760-4637d174-13d9-4269-ad3b-2f4acc9bc8ae.png){: .align-center width="90%"}

Word2Vec은 단어를 임베딩 공간의 벡터로 변환해주는 모델 중 하나이며 신경망을 기반으로 하고 있다. 대량의 문서를 벡터공간에 투영시켜 보면 위의 사진과 같이 비슷한 의미간의 변화는 이동한 모습이 비슷한 것을 알 수 있다.

임베딩 공간에 표현된 벡터는 압축된 형태의 많은 의미를 갖는 Dense Representated Vector로 표현이 되며 모델의 구조가 단순하기 때문에 효율적이고 빠른 학습이 가능하다. 이 신경망을 학습하는 방법에는 `CBOW`, `Skip-Gram`, `Skip-Gram with Negative Sampling` 이 있다.

## Word2Vec 학습방법

### CBOW

**Continuous Bag Of Words(CBOW)**는 주변에 있는 단어들을 사용해서 중앙에 있는 단어를 예측하는 방법이다. 이 주변 단어를 정의하기 위해서 중심단어로 부터 얼마나 떨어져 있는 단어들을 사용할 것인지 정하는 길이 $n$ 을 정의해야한다. 이 값을 윈도우 크기라고 하며, $n$ 일 때는 실제 예측을 하기 위해서 사용되는 단어는 $2n$ 개가 된다.

예시로, 다음과 같은 문장이 있다고 해보자

> The quick brown fox jumps over the lazy dog.

여기서 단어 `fox`를 예측하고 싶다고 하고 윈도우의 크기를 $2$ 라고 가정한다면, 학습에 사용하는 주변단어는 `quick`, `brown`, `jumps`, `over`이 된다.

![image](https://user-images.githubusercontent.com/91870042/158574947-6012199c-7380-4b46-a0f1-96f326eee245.png){: .align-center width="90%"}

모델에서 이 주변단어를 사용해서 중앙 단어인 `fox`를 예측하는 과정을 정말 간단하게 나타내면 다음과 같다.

![image](https://user-images.githubusercontent.com/91870042/158575105-d83997c5-df32-4f3e-b91c-baad8ef7b9f9.png){: .align-center}

입력으로 주변단어들을 받아서 Dense한 벡터로 임베딩하고, 이 임베딩 벡터들을 사용해서 중심 단어를 예측하는 것이다. 이 간단한 모델에서 사용할 파라미터는 총 2개로, 주변단어를 임베딩 벡터로 변환시켜주는 행렬과, 임베딩 벡터를 단어로 바꾸어주는 행렬이다.

![image](https://user-images.githubusercontent.com/91870042/158575275-e310fb9b-91fc-434d-a220-97438e2f60cd.png){: .align-center width="90%"}

이번에는 입력으로 2개의 단어가 들어왔다고 가정하고 그린 CBOW 학습방법이다. 그림에 있는 파라미터는 각각 다음 의미를 갖는다. 2개의 가중치 행렬이 여기서 학습이 되는 파라미터이다.

- $V$ : 단어의 총 개수, $M$ : 임베딩 벡터의 사이즈
- **$W_{V\times M}$:** $V$ 개의 단어를 $M$ 차원의 벡터로 바꾸어주는 matrix
- **$W'_{M\times V}$:** $M$ 차원의 벡터를 $V$ 개의 단어로 바꾸어주는 matrix

이 모델을 살펴보면 주변 단어가 Sparse Representation 된 원핫벡터가 임베딩 행렬( $W_{V\times M}$ )을 거쳐서 Dense Representated Vector 로 나타낼 수 있다. 주변단어가 4개인 경우, Projection Layer에는 총 4개의 임베딩된 벡터( $V$ )가 모이게 된다. 

![image](https://user-images.githubusercontent.com/91870042/158575430-27795c04-adeb-408d-b130-10b8fe59f26a.png){: .align-center}

모여진 4개의 벡터는 평균을 구해서 하나의 벡터로 다시 만든다. 이 새롭게 생긴 벡터는 다시 임베딩 과정을 거쳐 새로운 하나의 벡터( $z$ ) 를 만든다.

![image](https://user-images.githubusercontent.com/91870042/158575609-e9983c8e-9571-4024-8b6f-c4ba6c8ba277.png){: .align-center}

Projection Layer에서 출력층으로 나온 행렬을 $z$ 라고 했을 때, 어떤 단어에 속할 확률이 높은지를 알아내기 위해서 `softmax()`를 사용한다. 그리고, 그 결과를 실제 정답값과의 오차를 **cross entropy**를 사용해서 계산하며 학습에 사용된 파라미터들을 업데이트한다.  
이렇게 하여 Continuous Bag Of Words(CBOW)에 대해서 알아보았다.

### Skip-Gram

Skip-Gram은 방금 알아본 CBOW와 반대로 **입력과 출력과정이 거꾸로 구성**되어 있다. CBOW는 주변단어로 부터 중앙단어를 예측했던 것에 비해서 **Skip-Gram은 중앙단어를 사용해서 주변단어를 예측하도록 만들었다**. 

![image](https://user-images.githubusercontent.com/91870042/158575833-fe5fc5d4-9d29-4fa0-a108-85b3db420b73.png){: .align-center width="70%"}

하나의 벡터만 Projection Layer에 전달되기 때문에 CBOW처럼 임베딩된 벡터들의 평균을 구하는 과정이 존재하지 않는다. 일반적으로 CBOW보다는 Skip-Gram의 성능이 더 좋다고 알려져 있다. 여기서 말하는 성능은 loss값을 말하는 것이 아닌, 임베딩 공간에 표현되는 성능을 의미한다.

### Skip-Gram with Negative Sampling

![image](https://user-images.githubusercontent.com/91870042/158575985-8e9ba462-29a1-4bc2-b992-a5baba2910e4.png){: .align-center}

**Skip-Gram with Negative Sampling(SGNS)**는 Skip-Gram의 입력과 레이블을 모두 입력으로 사용하고 주변에 그 단어가 있다면 1, 없다면 0으로 나타내는 이진 분류 문제로 바꾸었다.

![image](https://user-images.githubusercontent.com/91870042/158576055-176eecbf-3199-4ba7-b601-3ddf236fc70e.png){: .align-center}

여기서 Negative Sampling 이라고 부르는 이유에 대해서 알아보자. 조금만 생각을 해보면 Skip Gram에서 입력과 레이블을 한 쌍으로 하는 입력이라고 하면 SGNS에서 그 레이블 값은 항상 1일 수 밖에 없다.

그렇기 때문에 강제로 주변단어 이외의 다른 단어들을 가져와서 사용해야 한다. 이 과정을 Negative Sampling이라고 부른다. 이때 가져올 단어들의 개수 즉, Negative Sampling을 진행할 횟수는 하이퍼 파라미터로 직접 지정해줘야 한다. 보통 학습데이터가 적은경우 5~20, 많은 경우는 2~5가 적당하다.

![image](https://user-images.githubusercontent.com/91870042/158576282-a0b8c715-8ad6-41e8-8977-7eb564a38ab5.png){: .align-center}

학습과정을 살펴보면, 이전에는 입력으로 주어진 단어들을 동일한 행렬을 사용해서 임베딩 벡터로 변환했던 것에 비해, **SGNS는 중심단어와 주변단어가 서로 다른 행렬을 사용해서 임베딩**한다.

![image](https://user-images.githubusercontent.com/91870042/158576359-eae338b8-1a18-403a-8548-ec7ce62db70d.png){: .align-center width="90%"}

이후에는 두 임베딩된 벡터를 내적을 하면 하나의 스칼라 값을 얻게 되고, 이 값은 `sigmoid()`를 거쳐서 0~1 사이의 값으로 매핑된 결과를 낸다. 이 결과와 실제 레이블간의 error를 cross-entropy를 사용해 계산한다. 이 error는 임베딩 과정에서 사용된 두 행렬을 모두 업데이트 한다.

최종 생성된 워드 임베딩이 2개이기 때문에 선택적으로 하나만 사용하거나 두 matrix의 평균값으로 사용한다. 이 때 생성된 2개의 행렬의 성능차이는 크게 나지 않는다.

<br/>

# Item2Vec

![image](https://user-images.githubusercontent.com/91870042/158576457-ca771678-7ab0-4c15-aa6c-2c98ba3a35a0.png){: .align-center width="90%"}

Word2Vec의 아이디어를 추천시스템에 그대로 적용시킨 Item2Vec에 대해서 알아보자. Item2Vec은 SGNS의 영감을 받아 아이템 기반 협업필터링에 적용시킨 논문이다. 단어가 아닌 추천시스템에 사용되는 아이템을 입력으로 사용하여 임베딩을 하였다.

**유저가 소비한 아이템 리스트를 문장으로, 아이템을 단어로 가정하여 Word2Vec을 사용**하는 것이다. Item2Vec은 유저-아이템 관계를 사용하지 않기 때문에 유저의 식별없이 세션 단위로도 데이터를 생성하는 것이 가능하다.

그래서 결과적으로는 SGNS 기반의 Word2Vec을 사용해서 아이템을 벡터화 하는 것이 이 논문의 목표이다. 참고로 SVD기반의 MF를 사용한 Item Based Collaborative Filtering(IBCF)보다는 Word2Vec이 더 높은 성능과 양질의 추천 결과를 제공한다.

## Item2Vec 상세

입력으로 아이템 집합이 필요하기 때문에 유저 혹은 세션별로 소비한 아이템 리스트를 생성한다. 이렇게 리스트로 생성하는 과정을 거치면서 아이템에 대한 공간적, 시간적 정보는 사라지게 되며 집합안에 존재하는 아이템은 서로 유사하다고 가정한다.

공간적 정보가 사라졌기 때문에 아이템간의 순서가 존재하지 않는다. 리스트 안에 있는 모든 아이템에 대해서 모두 Positive Sampling이 될 수 밖에 없는 것이다. 그렇기 때문에 기존의 Skip-Gram에서 사용한 앞뒤 단어의 개념이 사라졌기 때문에 Item2Vec에서는 같은 집합 내에 존재하는 모든 단어쌍을 학습에 사용한다.

$$ \frac{1}{K}\sum_{i=1}^{K}\sum_{\underset{j\ne 0}{-n\le j \le n }}\log p(w_{i+j}\mid w_i) \qquad \text{(skip-gram)}$$

$$ \frac{1}{K}\sum_{i=1}^{K}\sum_{j\ne i}^{K}\log p(w_j\mid w_i)\qquad \text{(Item2Vec)} $$

## Item2Vec vs. Single Vector Decomposition (MF)

![image](https://user-images.githubusercontent.com/91870042/158576527-9bc29b5a-6b48-4462-ab3c-73f090a20439.png){: .align-center width="90%"}

두 모델을 `t-SNE`를 사용해 임베딩한 결과를 시각화해보면, 비슷한 카테고리에 대해서 Item2Vec의 임베딩 성능이 더 우수한 것을 알 수 있다. 비슷한 색을 갖는 것들이 하나의 카테고리에 속하는 것인데 Item2Vec의 군집화가 더 잘된 것을 알 수 있다.

## Item2Vec의 활용 사례

- 아프리카 TV의 Live2Vec
- Spotify의 Song2Vec
- Criteo의 Meta-Prod2Vec
