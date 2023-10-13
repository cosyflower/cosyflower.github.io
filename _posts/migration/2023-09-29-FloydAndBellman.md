---
layout: single
title: "Floyd And Bellman"
categories:
    - wootaecourse # category 일치했는지 확인하기 
tags:
    - ['Off The Record'] # tag도 마찬가지로 같이 띄울 수 있다 
toc: "true"
toc_sticky: "true"

date: 2023-09-29
last_modified_at: 2023-09-29
published: true # true로 변경하면 노출할 수 있음 

#toc: 목차 보이기 
#toc_sticky: 자동 스크롤 가능 
#date: 포스팅한 날자 
#last_modified_at: 마지막 수정 일자 

#bundle exec jekyll serve - test 하는 방법 
#published: true
#br : 개행하기 
#hr : 개행 줄이 같이 출력되는 상황 
---
# [플로이드 와샬, 벨만 포드]

#23.09.29 #하루10분 #아침10분


> 최소 신장 트리와 연관있는 남은 알고리즘까지 추가로 학습해보자 (플로이드 와샬, 그리고 벨만 포드) 

### 벨만 포드 알고리즘
그래프 최단 경로를 구하는 알고리즘(하나의 시작점에서 진행하는 형태) - 최단 거리 
음수 사이클 X - 음수 간선 허용한다
<!-- ![](image.png) -->

출발지 한 곳을 정해서 진행하는 것은 다익스트라와 공통점이다

### 벨만-포드 알고리즘
최단 거리를 기록하는 1차원 배열을 선언(정점의 개수 크기의 1차원 배열을 선언)
출발점은 당연하게 0 으로 나머지는 INF로 설정(update 하기 위함) 
<!-- ![](image%202.png) -->

### 기본적으로 vertex, edge 모두 포함해야 한다
<!-- ![](image%203.png) -->
시작점을 기준으로 향하는 정점의 거리를 먼저 확인한다
update 가능한지를 각각 확인해본다 

update 된 정점들을 출발점으로 간선 정보를 확인해서 거리 배열을 다시 update 한다 
연결된 간선 정보를 모두 확인하면서 update 한다

최종적으로 distance 배열에 INF 정보가 없다면, 전체적으로 한 번 더 살펴보게 된다 
<br>
`음수 사이클이 존재하는지도 확인해볼 것`
## 벨만 포드 알고리즘의 구현

-> 전체 정점의 개수, 전체 간선의 개수, 마지막으로 시작점에 관련 정보를 전달해야 한다
-> 정점의 개수 * 간선의 개수 의 시간 복잡도를 가지고 있다
-> 간선을 전체적으로 확인한다. 각 정점 별로 확인하면서 진행한다 

기존에 설정한 Integer.MAX_VALUE가 아닌 정점을 탐색해 가면서 update 하는 방향이라고 생각하면 되겠다 
나오는 정점의 거리 배열이 초기화된 상태라면 살펴볼 이유가 없다(아무것도 도달한 것도 없으며, 혹은 해당 간선을 아직 탐색하지 않은 상황이라고 할 수 있겠다

마지막으로는 음수 사이클의 존재 여부를 확인하게 된다. 최종적으로 간선을 조회하면서 마찬가지로 Integer.MAX_VALUE가 존재하는지 혹은 더 최소값을 유지하고 있는지를 확인하면 되겠다 

```java
public static boolean bellmanFord(int vertexCount, int edgeCount, int startPoint) {
    // 시작점을 기준으로 0 나머지 거리는 최대로 저장을 미리 해둔 상황이다
    distance = new int[vertexCount + 1];
    Arrays.fill(distance, Integer.MAX_VALUE);
    distance[startPoint] = 0;

    // 각각의 정점에서 확인하기
    for (int i = 0; i < vertexCount; i++) {
        // 전체 간선 파악하기
        for (int j = 0; j < edgeCount; j++) {
            Edge currentEdge = edges.get(j);
            if (distance[currentEdge.getV()] != Integer.MAX_VALUE &&
                    distance[currentEdge.getW()] > currentEdge.getV() + currentEdge.getWeight()) {
                distance[currentEdge.getW()] = currentEdge.getV() + currentEdge.getWeight();
            }
        }
    } // 전체 간선 * 전체 정점의 크기로 Loop을 진행하게 된다

    // 음수 가중치를 확인해야 한다
    for (int i = 0; i < edgeCount; i++) {
        Edge findMinusEdge = edges.get(i);
        if (distance[findMinusEdge.getW()] > distance[findMinusEdge.getV()] + findMinusEdge.getWeight()) {
            System.out.println("음수 사이클이 존재합니다");
            return false;
        }
    }

    return true;
}
```

---
## 플로이드 와샬 알고리즘
모든 정점 간 최소 거리를 구할 수 있는 알고리즘이다
마찬가지로 음수 가중치는 허용하지만 음수 사이클을 허용하지는 않는다 
시간 복잡도는 n^3 형태를 가지고 있다 
<!-- ![](image%204.png) -->

플로이드 와샬 알고리즘은 중간 경유지라는 개념이 하나 더 들어간 형태가 되겠다
i에서 j까지 이동하려고 할 때 중간 경유지 k가 들어가게 되면서
graph[i to j] = graph[i to k] + graph[k to j] 형태의 값으로 만들 수 있다 

추가적으로 그래프 관련 정보를 이중 행렬로 표현하고 있다 
graph [ 시작점 ] [ 종점 ] = 거리 (가중치) 


### 각각의 정점을 ‘경유’하며 진행되는 경우를 생각하자
중간 경유지의 개념으로 생각하며, 해당 정점을 시작으로 혹은 종점으로 진행되는 경우에는 배제하고 진행한다
코드의 구현은 상대적으로 쉬우나 경유지 -> 시작점 -> 종점을 전체적으로 조회하며 진행되는 개념이기 때문에 기본적으로 시간 복잡도의 크기가 클 수 밖에 없다 

-> 각각의 정점이 경유지가 되는 경우를 고려해서 최소값을 비교해 나가면 되겠다 
-> 이중 행렬로 정보를 기입하는 이유를 충분히 알 수 있었다
-> 시작점이 고정된 것이 아니라 특정 정점에서 다른 정점까지의 최소 거리를 모두 구할 수 있다는 장점을 가지고 있음 

---
## 추가적으로 Djikstra의 경로 복원 방법에 대해서 알아보자 
중간 중간 update 될 때 중간 경유지가 어디 인지를 계속해서 반영한다고 생각하면 되겠다 
값이 update 되었다는 것은 해당 경로가 최소 경로임을 확인할 수 있다. 어떤 정점을 경유해서 진행되었는지 확인할 수 있는 셈이라고 할 수 있겠다 