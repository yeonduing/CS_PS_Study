
# Shortest Path Algorithm

![](https://i.imgur.com/b5TMCYb.jpg)

(뭐 대충 중요하다는 내용ㅎ)

최단 경로 문제를 풀 때 가장 많이 언급되고 활용되는 삼대장

* 다익스트라
* 벨만포드
* 플로이드

상황에 맞게 위의 알고리즘들을 적용해야하는데 이 때 몇가지를 고려해보면 좋다.
문제를 그래프화 시킬 수 있게되었다면 이제 다음을 생각해 볼 차례다.

1. **가중치**가 있는가? : 가중치가 없다면 BFS로 해결 가능
2. **음수간선**이 있는가? : weight에 음수 값이 있다면 벨만포드
3. **단일 시작점**을 갖는가? : 단일 시작점이 주어진다면 다익스트라, 모든 정점들의 쌍에 대한 경로 값을 알고 싶다면 플로이드

## The Dijkstra's Algorithm

* 다익스트라 : 단일 시작점 최단 경로 알고리즘으로, 시작 정점 s에서부터 다른 정점들까지의 최단 거리를 계산
* BFS의 연장선상에서 고안 된 알고리즘이라 매우 형태가 유사
    * 차이점 : Dijkstra는 Priority Queue를 사용한다는 점
    * 특정 노드의 이웃(neighbor)을 살피지만, 시작점 부터의 거리가 가장 짧은 것 부터 살피는 특징을 갖고 있음

### 직접 해보기

다음과 같은 그래프가 주어졌다고 생각해보자. 다익스트라를 활용하여 해당 문제를 풀 경우 오른쪽 표와 같이 **방문 여부**, **시작점부터의 거리**, 그리고 **경로에 놓인 노드** 들에 대한 정보를 트래킹 할 수 있게끔 구현한다고 생각하면 쉽다(?증말?)

![](https://i.imgur.com/0dtDFdP.png)

3가지 질문에 대한 답을 하며 알고리즘을 익히고, 3가지 질문에 대한 답을 구현해내면 다익스트라 완성.

```
질문 1. 다음에 어떤 노드를 꺼내지?
답 1. 방문하지 않은 노드 중 시작점에서부터의 거리가 가장 짧은 것!

질문 2. 노드를 꺼낸 다음에는 뭘 하면 되지?
답 2. 이웃을 봐야지!

질문 3. 이웃들의 경로는 언제 업데이트 해?
답 3. 새로운 경로 < 기존 경로일 때 업데이트 하는거야!
```

문제의 조건에 정점 A가 source임이 주어졌을 때, 우측의 표는 아래 그림과 같이 **초기화** 할 수 있다. 

![](https://i.imgur.com/WAIh3iH.png)


 ```
 방문하지 않은 노드 중 시작점에서부터 거리가 가장 짧은 노드 = A
 ```
 - A 방문 = true로 변경하고 A의 이웃을 살펴보면 B와 D가 있다
 - B와 D는 모두 새로운 경로가 현재 경로보다 작으므로 시작점부터의 거리 및 최단 경로에 놓인 노드를 업데이트 한다

 ![](https://i.imgur.com/baMovLh.png)

 ```
 방문하지 않은 노드 중 시작점에서부터 거리가 가장 짧은 노드 = D
 ```
 - D 방문 = true로 변경하고 D의 이웃을 살펴보면 (A), B, E가 있다
 - B의 현재 경로 거리가 3인 반면 새로운 거리는 5라 그대로 둔다.
 - E는 새로운 경로가 현재 경로보다 작으므로 시작점부터의 거리 및 최단 경로에 놓인 노드를 업데이트 한다

 ![](https://i.imgur.com/aQx2VcF.png)
 
 이러한 방식으로 비교하고, 선택하며 과정을 이어나가면 된다.
 
![](https://i.imgur.com/Xy9IzBF.png)

![](https://i.imgur.com/NcBLGvb.png)

![](https://i.imgur.com/tIbkawr.png)

* 만약 특정 도착지가 주어졌다면 중간에 break하고 나올 수도 있었겠지?

### Pseudo Code로 맛보기

```
function Dijkstra (Graph: g, source: s) :
     create vertex set Q // 미방문 노드가 모여있을 Q

     // 초기화 진행 중 삐비빕...
     for each vertex v in Graph g: 
          distance[v] = ∞
          prev[v] = undefined
          add v to Q
     distance[s] = 0

     while Q is not empty:
          // 살펴 볼 노드는 미방문 & 거리가 가장 짧아야 함
          u = vertex in Q with min distance[u]
          remove u from Q

          // 거리 계산해보고 필요 시 업데이트
          for each neighbor v of u:
               new_distance  = distance[u] + weight(u, v)
               if new_distance < distance[v] :
                    distance[v] = new_distance
                    prev[v] = u

```

### 시간복잡도

* 다익스트라 알고리즘의 시간복잡도에 관여하는 요소는 총 2가지가 있다
    * Edge 검사
    * Priority Queue에 삽입/삭제

* 각 정점은 정확히 한 번 방문하기 때문에 모든 Edge는 한 번씩 검사 = O( |E| )
* 우선순위 큐에 추가되는 원소의 최대 수 = O( |E| )
  우선순위 큐에서 삽입/삭제에 걸리는 시간 = O( lg|E| )
  = O( |E| lg|E| )
  
* 두 요소의 합 = O( |E| lg|E| )
    * BUT |E| < V² 이므로 최종적으로 시간복잡도는 **O ( |E| lg|V| )** 로 나타낼 수 있다


### 문제를 뽀샤버려라

* 백준 다익스트라 모음 : [열로가쑈](https://solved.ac/problems/tags/dijkstra)
* 프로그래머스 : 배달(12978), 가장 먼 노드(49189)
* 알고스팟 : 신호 라우팅(ROUTING), 소방차(FIRETRUCKS), 철인 N종 경기(NHTHLON)
