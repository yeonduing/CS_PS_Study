## The Floyd-Warshall Algorithm

* 모든 정점 쌍에 대해 둘 사이의 최단 거리를 구하는 알고리즘
    * Dijkstra/Bellman-Ford 를 반복해서 구할 수도 있음

* 경유점 : 두 정점 u와 v를 잇는 어떤 경로가 있다고 가정할 때, u와 v 사이에 있는 다른 정점

![](https://i.imgur.com/0z4TJTm.png)

```
1. 경유점 k를 제외한 S - {k} 노드 중 서로 다른 노드 U, V 선택 (S = 정점 집합일 때 k, U, V ∈ S)
2. U → k → V의 비용 확인 후 최단거리 갱신
```

![](https://i.imgur.com/sI4GOyq.png)

### 직접 해보기

다음과 같은 그래프가 주어졌다고 해보자. <br>
Floyd-Warshall 알고리즘은 Dijkstra와 다르게 모든 그래프의 모든 정점 쌍의 최단 거리를 저장해야하므로 **2차원 배열**이 필요하다 <br>
초기화 할 때에는
1. if from == to, then 0
2. if edge(from, to) == value then value, else infinity

![](https://i.imgur.com/khUGC2k.png)

초기화가 완료되었으면 모든 정점들을 '경유점'으로 만들어 가며 2차원 배열을 갱신해나간다.<br>
아래와 같이 A가 경유점이 되었다면, 나머지 정점쌍에 대해 거리를 비교하며 표를 갱신할 수 있다.<br>
예를 들어 기존 BD간 거리는 정의되어 있지 않아 infinity였는데 A를 경유하면서 거리가 9로 짧아졌으므로 갱신한다.

![](https://i.imgur.com/ZPGr5Wu.png)

![](https://i.imgur.com/oMKyOmv.png)

![](https://i.imgur.com/KrmM80L.png)

![](https://i.imgur.com/b8PjrIp.png)

위 과정을 보면 모든 정점에 대해 경유점을 선택하고 모든 시작점과 끝점을 선택하는 과정에서 3중 for문이 도는 것을 알 수 있다.<br>
이를 코드로 작성해보면 아래와 같다.

```swift
graph = [[Int]]()

func floydWarshall() {
   for k in 0..<n {
      for from in 0..<n {
         for to in 0..<n {
            graph[from][to] = min(graph[from][k] + graph[k][to], graph[from][to])
         }
      }
   }
}

```
가장 충실하게 짜여진 코드지만 문제에 따라 최적화의 필요는 있다.<br>
* 실제 from 노드에서 경유 노드로 간선이 있는지 확인
* Undirected Graph라면 대각선 상위로만 적용


### 시간 복잡도

노드의 개수가 N개 일 때 한 노드마다 O(N²)의 연산을 수행하므로 O(N³)

### 문제를 뽀샤버려라

* 백준 다익스트라 모음 : [열로가쑈](https://solved.ac/problems/tags/floyd_warshall)
* 프로그래머스 : 순위(49191)
