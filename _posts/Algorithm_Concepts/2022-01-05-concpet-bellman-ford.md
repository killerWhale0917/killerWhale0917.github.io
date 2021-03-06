---
title:  "벨만-포드(Bellman-Ford)의 최단 경로 알고리즘"
excerpt: "음의 사이클이 있는 그래프의 판단과, 해당 그래프의 최단경로를 구해주는 알고리즘인 벨만-포드 알고리즘"

categories:
  - concept
tags:
  - [그래프, 벨만-포드]

toc: true
toc_sticky: true
 
date: 2022-01-05
last_modified_at: 2022-01-05
---
📌 **알립니다!**<br>
이번에 작성되는 글은 **구종만, 『알고리즘 문제해결 전략2』, 인사이트(2012)**를 읽고 정리하는 글입니다.<br>
30장. 최단 경로 알고리즘 - 벨만-포드의 최단 경로 알고리즘<br>
더 자세한 관련 문제와의 설명은 책에 더 상세하게 설명되어 있습니다.
{: .notice--info}

# Dijkstra VS Bellman-Ford
**다익스트라 알고리즘**은 한 시작점에서 다른 모든 정점까지의 최단 거리를 구하는 알고리즘이며, 그 시간복잡도는 <u>우선순위 큐를 사용하고 중복 원소를 큐에 넣지 않도록 하면</u> \\(O(\|V\|lg\|V\|)\\)가 된다. 이번에 알아볼 **벨만-포드 알고리즘**도 한 시작점에서 다른 모든 정점까지의 최단 거리를 구하는 알고리즘인데, 시간복잡도는 \\(O(\|V\|\|E\|)\\)이다. 알고리즘을 수행하는데 시간이 더 오래걸리지만, 이렇게 유명하고 많이 사용되는 이유는 무엇일까?

다익스트라 알고리즘에서는 한 가지 전제조건이 필요하였다.
> 음의 가중치를 가진 간선이 존재하면 안된다.

그렇기 때문에 **음수 간선이 있는 그래프**의 경우 그 정당성이 보장되지 못하였다.

# 벨만-포드 알고리즘
이번, 벨만-포드 알고리즘에서는 음의 가중치를 간선이 존재해도 되고, 그래프에서 어떤 사이클의 가중치의 총 합이 음수가 되는 것(=음수 사이클)도 발견해 낼 수 있는 알고리즘이다. 벨만-포드 알고리즘의 큰 동작 방식은 시작점에서 각 정점까지 가는 최단 거리의 상한을 적당히 예측한 뒤, 예측값과 실제 최단거리 사이의 오차를 반복적으로 줄여나간다.

실제로, 다양한 문제에서 음의 사이클이 존재하는 문제에서 자주 사용되는 알고리즘인데 음수 사이클의 표현을 하기 위해 시간여행, 터널과 같은 표현을 자주 사용하기도 한다.

## 벨만-포드의 동작 과정
알고리즘이 시작할 때는, 다익스트라 알고리즘과 비슷하게 그래프의 구조에 대해서 아는것이 존재하지 않다. 시작점(거리 0)을 제외한 모든 정점까지의 거리는 `INF`로 초기화 한다. 벨만-포드 알고리즘은 최종 최단거리 dist값을 실제 최단 거리와 가깝게 만들기 위해서 최단 거리의 특성을 이용한다.

### 최단 거리의 특성
출발점이 \\(u\\)이고, 도착점이 \\(v\\)이며, 가중치가 \\(w\\)인 간선에 대해 다음 조건은 항상 참이다.

\\[
    \text{dist}[v] \le \text{dist}[u] + w
\\]

위와 반대로, dist[u] + w < dist[v] 인 상황을 생각해보면, 정점 v까지의 최단거리보다 더 짧다는 의미이기 때문에 그 값을 업데이트 할 수 있다. 이렇게 dist값을 업데이트 하는 과정을 **완화한다**고 말한다. 벨만-포드 알고리즘은 이와 같은 와화 과정을 모든 간선에 대해 반복적으로 실행한다.

## 종료 조건과 정당성의 증명
하지만, 이러한 확인 과정이나 완화과정을 몇 번이나 거쳐야하는지 아직 결정하지 않았다. 어떤 그래프가 하나 주어졌다고 했을 때, 그 그래프에서 시작점으로 부터 가장 멀리 있는 정점까지 도착하기 위해서는 최대 \|V\| - 1개의 간선을 거쳐야만 한다. 아래의 그래프를 살펴보자

![image](https://user-images.githubusercontent.com/91870042/148185753-d4d28a1c-c3da-4833-8f18-52f3f24eff9d.png){: .align-center}

가장 왼쪽에 있는 정점으로 부터, 가장 오른쪽에 있는 정점으로 이동하기 위해서는 4번을 이동해야 한다. 이는 정점의수-1개인 5개보다 작은 값이다. 그러면 이번에는 5번의 간선을 지나는 그래프를 보자.

![image](https://user-images.githubusercontent.com/91870042/148186093-acd95973-9060-4ced-bb94-42aaef19bde7.png){: .align-center}

이 그래프에서는 시작점에서 마지막 점으로 이동하기 까지, \|V\| - 1개의 간선을 거쳐야만 한다. 그렇기 때문에, 최대 완화과정을 \|V\| - 1번 진행하면 모든 정점까지의 최단 거리를 얻어낼 수 있음을 알아낼 수 있다. 하지만, 음수 사이클이 존재하는 그래프에서는 음수 사이클을 많이 돌면 돌수록 그 값이 `-INF`로 작아지기 때문에 그 다음에도 완화가 이루어질 수 있다. 바로 이부분을 벨만-포드 알고리즘에서 사용한다.

## 음수 사이클의 판정
처음에 벨만-포드 알고리즘은 다익스트라 알고리즘과 다르게, 음수인 간선이 존재하여도, 음수 사이클이 존재하여도 판단할 수 있다고 했었다. 벨만-포드 알고리즘이 음수 사이클을 찾아내는 방법은 다음과 같다. 

\|V\| - 1번의 완화 과정을 거치고, 그 다음 \|V\|번째의 완화에서도 값의 업데이트가 이루어진다면, 그래프 내에 음수 사이클이 존재한다고 말할 수 있다. \|V\| - 1번의 완화과정을 거치면, 모든 정점에 대해서 최단 거리를 알아내야 정상이지만, 한 번더 값의 업데이트가 일어났다는 것은 음수 사이클이 있을 때만 가능하기 때문이다. 이는 다음 수식으로도 설명할 수 있다.

![image](https://user-images.githubusercontent.com/91870042/148186927-2849161a-0775-4c64-bea2-27ca6a83039a.png){: .align-center}

위와 같은 그래프가 있을 때, 다음 3가지 부등식이 성립한다.

\begin{aligned}
\left\\{\begin{matrix}
\text{dist}[1] \le \text{dist}[3] + 10 \\\\\\
\text{dist}[2] \le \text{dist}[1] + 10 \\\\\\
\text{dist}[3] \le \text{dist}[2] - 21
\end{matrix}\right.
\end{aligned}

위의 식에서 좌변끼리, 우변끼리 모두 더하면 아래와 같은 결과가 나오며, 다시 정리하면 가장 아래의 수식이 나온다.
\\[
    \text{dist}[1] + \text{dist}[2] + \text{dist}[3] \le \text{dist}[1] + \text{dist}[2] + \text{dist}[3] - 1 \\\\\\
\\]

\\[
    0 \le -1
\\]

너무나 당연하게 위의 식은 모순이기 때문에, 음수사이클이 존재하는 그래프에서는 \|V\|번째의 완화에서 3개의 간선 중에서 하나는 항상 완화가 성공한다는 사실을 알 수 있다.

## 구현
~~~cpp
int V; // 그래프에 존재하는 정점의 수
vector<pii> adj[MAX]; // 간선을 표현하는 인접리스트

vector<int> bellmanFord(int src) {
    vector<int> dist(MAX, INF); // 각 정점까지의 최단거리를 저장. (초기: INF)
    dist[src] = 0; // 시작점의 거리는 0으로 설정
    bool hasNegCycle = false; // 음수사이클 존재 여부

    // 음수사이클의 판정을 위해서 V번의 완화를 시도하고,
    // 마지막 완화에서 성공한다면, 음수사이클이 존재하는 것이다.
    for (int i = 0; i < V; ++i) {

        // 존재하는 모든 간선에 대해서 검사한다.
        for (int here = 0; here < V; ++here) {
            for (pii there : adj[here]) {
                int node = there.first;
                int cost = there.second;

                // (here, there) 간선을 따라서 완화를 시도한다.
                if (dist[there] > dist[here] + cost && dist[here] != INF) {
                    dist[there] = dist[here] + cost;

                    // 마지막 V번째 완화에서 성공한 경우 = 음수 사이클이 존재한다.
                    if (i == V - 1) hasNegCycle = true;
                }
            }
        }
    }

    if (hasNegCycle) return vector<int> ();
    else return dist;
}
~~~

## 시간복잡도
벨만-포드 알고리즘의 수행시간은 모든 간선을 검사하는 중첩 반복문에 의해서 지배된다. 첫번재 for문은 V번 수행이 되고, 안에 2개의 for문은 모든 간선에 대해서 검사하는 부분이기 때문에 E번 수행된다. 따라서 벨만-포드 알고리즘의 최종 시간복잡도는 \\(O(\|V\|\|E\|)\\)이다.

## 실제 경로 계산하기
벨만-포드 알고리즘을 수행하는 과정에서 각 정점을 마지막으로 완화시킨 간선들을 모으면, **스패닝 트리**를 얻을 수 있다. 이 <u>스패닝 트리에 존재하는 간선은 최단 경로 위에 있기 때문에</u>, 각 정점에서 부터 스패닝 트리의 루트인 시작점 까지 거슬러 올라가는 경로는 항상 시작점에서 해당 경로까지의 최단경로가 된다.