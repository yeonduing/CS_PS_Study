# ***Union-find***

### ***disjoint set(서로소 집합)***

공통원소가 없는 두 집합을 의미한다. 
집합 {1,2}와 {3,4}는 서로소 관계이다.

###### 서로소 집합 "자료구조"란

서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조 <br>
서로소 집합 자료구조는 **union과 find 2개의 연산으로 조작 가능**<br>
***union***은 2개의 서로소 집합을 하나로 합치는 연산<br>
***find***는 특정한 원소가 속한 집합이 어떤 집합인지 알려주는 연산 

<br>

### ***Disjoint set***은 ***Graph*** 로 표현이 가능하다.
집합의 원소들은 그래프의 ***Vertex or Node***로 표현되고
union 연산은 ***Edge***로 표현된다. 

- union 1 3 연산이라면<br>
  1과 3이라는 노드가 있고, 1과 3이 간선 하나로 연결된 상태로 표현할 수 있겠다.<br>
  union는 a노드와 b노드 그룹을 합치는 연산이라고 생각하면 되겠다. <br>
- find는 x노드가 어느 그룹에 속해 있는지 하는지 알아오는 연산

<br>


### 서로소 집합 알고리즘
- 서로소 집합을 다루는 방식
- 연산을 효과적으로 수행하기 위해 **부모테이블**을 가지고 있어야 한다.
- 그룹의 **최상위 노드는 부모 노드를 자기 자신**으로 한다.

<br>

1. ***Parent table Init***<br>
   처음에 모든 노드(원소)는 자기자신을 가리키도록 만든다.
   ```Python
   v, e = map(int, input().split())   # 정점의 개수 v와 간선의 개수 e를 입력
   parent = [0] * (v + 1)             # 1번 노드부터 시작한다고 가정
   
   for i in range(1, v + 1):
      parent[i] = i                   # 우선, 자기 자신을 가리키도록 초기화
   ```
2. ***Union*** <br>
   union a b의 경우, b의 부모를 a로 갱신시켜주면 된다.
   ```Python
   def union_parent(a,b):
     a = find_parent(a)
     b = find_parent(b)
     
     if a < b: parent[b] = a          # 합쳐줄 때, 어느 것을 부모로 할지 
     else : parent[a] = b             # 일관적인 로직을 두기 위해, 작은 번호로 합침
   ```
3. ***Find***<br>
   find를 통해 어느 그룹인지 알아오려면, 나의 부모의 부모 ~~ 부모를 타고 올라가서 최상위 노드가 누구인지 알아와야 한다.<br>
   부모테이블을 계속 타고 올라가, 최상위 노드를 알아온다. <br>
   최상위 노드를 한 번 알아왔으면, 내 부모노드를 최상위 노드로 갱신한다. 이걸로 연산 횟수가 줄어든다. **"경로 압축"**
   ```Python
   def find_parent(x):
     if parent[x] != x:               
       parent[x] = find_parent(parent[x]) 
     return parent[x]
   ```
    - union할때마다 속한 것들을 모두 바꿔줄 수도 있지만, 지금 건드리는 것만 바꿔서 쓸데없는 연산을 줄일 수도 있지
     
<br>
<br>

# ***Kruskal Algorithm***<br>
최소 비용 신장 트리 (***MST***)를 만드는 알고리즘 <br>
정점만 있는 그래프에서, 가중치가 작은 간선들을 그래프에 포함시키는 알고리즘으로 일종의 ***Greedy***라고 할 수 있다.<br>
(대신 MST 정의에 따라, ***Cycle***이 발생하지 않는 간선만 추가)<br>
> ***SPANNING TREE***: 신장트리는 모든 노드를 포함하면서, 사이클이 없는 부분 그래프다.<br>
> ***MST***: 한 그래프에는 여러개의 신장트리가 존재할 수 있는데, 그 중 간선의 합이 가장  작은 신장트리를 말한다.

<br>

### ***Logic***
1. 간선을 모두 정렬 
2. 가중치가 작은 간선을 순서대로 선택하면서 연결
3. 연결할 때 ***Cycle***이 발생하지 않도록 해야 함

### ***Cycle*** 여부를 판단하기 위해, ***union-find***를 사용한다.
```python=
for edge in edges:
    cost, a, b = edge
    
    if find_parent(a) != find_parent(b): #find는 최상위 노드를 가져온다.
        union_parent(a, b)               #최상위 노드가 같을 때, 두개의 간선을 추가하
        result += cost
```
***`line 4`***<br>
정점 a와 정점 b를 잇는 간선이 추가되었을 경우, Cycle이 생기는지 판단하기 위해서<br>
두 정점이 속한 그룹의 최상위 노드가 같은지 확인한다.<br>
최상위 노드가 같다는 것은 **이미 두 노드가 신장트리에 포함되어 있음을 의미**<br>
신장 트리에 포함되어 있는 정점 a와 정점 b를 잇는 간선을 추가해버리면 Cycle이 발생 <br>

***`line 5`***<br>
따라서, 최상위 노드가 다른 경우에, **아직 신장트리에 포함되지 않았단 뜻**이므로<br>
해당 간선을 추가하는 ***union_parent***를 수행한다.<br>

<br>
<br>

# ***Python Example***
최소 신장 트리를 만드는데 필요한 비용을 계산해라.
정점은 1번부터 주어진다.

```python=
# init
v, e = map(int, input().split())
parent = [0] * (v+1)
edges = []
result = 0

# 자기 자신을 가리키도록 초기화
for i in range(1, v+1): parent[i] = i

# input edges
for _ in range(e):
    a, b, cost = map(int, input().split())
  
    #cost 기준으로 내장 정렬함수 돌리려고 cost를 먼저 삽입
    edges.append((cost,a,b))  
edges.sort()


# Kruskal
for edge in edges:
    cost, a, b = edge
  
    if find_parent(a) != find_parent(b):
        union_parent(a,b)
        result += result

print(result)
```

###### Union & Find
```python=
def find_parent(x):
    if parent[x] != x : 
        parent[x] = find_parent(parent[x])
    return parent[x]
  
def union_parent(a,b):
    a = find_parent(a)
    b = find_parent(b)
    
    if a < b: parent[b] = a
    else : parent[a] = b

```
