## 위상 정렬 (Topological Sort)

### 위상정렬?

**순서가 정해져있는 작업**을 차례로 수행해야 할 때 그 순서를 결정해 주기 위해 사용하는 알고리즘.

### 그게 무슨소리죠?

예를 들어, A~H 까지의 작업이 있고, 이 작업들이 아래 그래프와 같은 순서대로 진행되어야 한다고 합시다.

![](https://user-images.githubusercontent.com/40164248/103175018-4a1d3380-48aa-11eb-86a1-3a5c3cb49b79.png)

위 그래프는 A는 B,C보다 먼저, C는 D보다 먼저, D는 B보다 번저 수행되어야 한다는 것을 의미합니다.

이 때, A~H의 작업을 모두 우선순위를 지키면서 수행할 수 있는지, 있다면 어떤 순서로 수행해야 하는지 알아내는 것이 위상 정렬입니다. 위 그림의 경우에는 `A -> C -> D -> B` 순서대로 수행하면 가능한 것을 직관적으로 알 수 있습니다.

<br>

### 좀더 알고리즘적인 정의

위상 정렬을 다시한번 정의하면, 

* **DAG(Directed Acyclic Graph)** 에서 정점들을 간선의 방향성을 거스르지 않도록 나열하는 알고리즘

이라고 할 수 있습니다. 따라서 뒤에서도 언급되지만 유향 그래프에서 cycle이 존재한다면 위상정렬이 불가능합니다.

<br>

### 알고리즘

* DFS + Stack
* Queue + indegree(진입 차수)

보통 위의 두 가지 방법을 가장 많이 쓰는데, Queue를 사용하는 방법이 좀더 구현이 간결하고 활용도가 높아 Queue를 사용한 방법을 소개하도록 하겠습니다.

![](https://user-images.githubusercontent.com/40164248/103175052-8355a380-48aa-11eb-94fb-1259ab2483a2.png)

다음과 같이 그래프가 주어졌다고 합시다. 이 때 가장 먼저 진입점을 찾아야 합니다.

진입점을 찾기 위해 모든 노드의 indegree(진입 차수 - 자신에게 들어오는 방향인 간선의 수)를 구하고, indegree가 0인 노드를 찾습니다. 여기에선 A가 됩니다. 

진입점이 된 A 노드를 queue에 넣습니다.

![](https://user-images.githubusercontent.com/40164248/103175149-23abc800-48ab-11eb-9aa9-11ab8990a6dd.png)

그리고 queue의 제일 아래에 있는 A를 빼낸 뒤, A에서 나가는 모든 간선을 제거합니다.

![](https://user-images.githubusercontent.com/40164248/103175180-6f5e7180-48ab-11eb-9d91-d13b7b0a0ab6.png)

이제부터는 반복입니다. 마찬가지로 이 상태에서 indegree가 0인 노드인 C를 queue에 넣습니다.

![](https://user-images.githubusercontent.com/40164248/103175181-6ff70800-48ab-11eb-9a7e-7f0d4ac4c93f.png)

queue에서 C를 pop한 뒤 C에서 나가는 간선을 제거하고, indegree가 0인노드 F를 queue에 넣습니다.

![](https://user-images.githubusercontent.com/40164248/103175182-708f9e80-48ab-11eb-8880-b7a837f085ca.png)

이런식으로 반복하면 아래와 같이 됩니다.

![](https://user-images.githubusercontent.com/40164248/103175183-71283500-48ab-11eb-9e1b-be605d9ad6bd.png)

![](https://user-images.githubusercontent.com/40164248/103175186-71c0cb80-48ab-11eb-8e83-fcc3d805d6c4.png)

![](https://user-images.githubusercontent.com/40164248/103175188-71c0cb80-48ab-11eb-9bb5-6c18f62f0d79.png)

* 결과적으로 queue에서 pop된 순서대로 모아진 `A->C->F->B->D->E`가 정답이 됩니다. 

* 눈치채셨겠지만 정답이 반드시 하나는 아닙니다. `A->C->F->B->E->D`도 가능한걸 쉽게 알수 있죠.

* 또, 중요한 것이 있는데, cycle이 존재해서 위상정렬이 불가능 한 경우에는 중간에 indegree가 0인 노드가 없는 때가 반드시 생깁니다. 이를 이용해서 위상정렬 가능 여부도 판단할 수 있습니다.
  * cycle을 이루는 노드만 남았다면, 서로 물고 물려 indegree가 0인 노드가 존재하지 않게 됩니다.

* 시간복잡도는 O(V+E) 입니다. (V: 정점의 개수, E: 간선의 개수)
  * 기본적으로 모든 노드를 탐색해야 하고, 각 노드마다 간선을 모두 제거해야 하기 때문입니다.



### 구현

Python으로 위의 과정을 구현하면 다음과 같습니다.

```python
from collections import deque


def topological_sort(graph: dict, indegrees: dict):
    queue = deque()
    result = []
    keys = list(indegrees.keys())
    num_of_nodes = len(keys)

    while len(result) < num_of_nodes:
        for key in keys:
            if ind[key] == 0:
                queue.append(key)
                keys.remove(key)

        if len(queue) == 0:
            return ['Impossible']

        popped_node = queue.popleft()
        result.append(popped_node)
        edges_to_delete = graph[popped_node]
        for edge in edges_to_delete:
            indegrees[edge] -= 1

    return result


# graph는 모두 입력받았고, 입력 과정에서 indegree도 체크했다고 가정
g = {'A': ['B', 'C'], 'B': ['D', 'E'], 'C': ['E', 'F'], 'D': [], 'E': [], 'F': ['B']}
ind = {'A': 0, 'B': 2, 'C': 1, 'D': 1, 'E': 2, 'F': 1}

print(topological_sort(g, ind))

```

