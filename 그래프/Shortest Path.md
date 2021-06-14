# Shortest Path
문제  
최단경로: https://www.acmicpc.net/problem/1753

## 1. 디익스트라 알고리즘
핵심: 가야할 edge를 선택할때 __그 순간에__ weight이 가장 작은 간선을 선택하는(Greedy) 선택을 한다.   
방문한 노드들의 집합을 S, 아직 방문하지 않은 노드들의 집합을 U라하자.   
1. U에서 dist[v]값이 가장 작은 노드(v)를 선택하여 S에 추가한다. 
2. 선택한 노드(현재 S)와 연결된 노드들 중에 U에 있고 가중치의 값이 (e: v->w)( dist[v] + edge.weight > dist[w])이면 weight을 업데이트 한다.
위를 반복한다.
Prim 알고리즘과 매우 비슷한 문제이며, 마찬가지로 Indexed Priority Queue를 사용한다.   


### 의문점 
위의 2번쨰 순서에서 선택한 노드의 연결된 간선들중 __방문하지 않은 노드(w)__ 와 연결된 간선(e: v->w)를 추가한다고 했는데
이미 한 번 방문한 노드여도 상관 없지 않나..?
노드가 방문으로 표시되는 즉시 해당 노드의 거리 값이 소스에서 가장 짧다는 보장을 제공므로 방문한 노드에 대해서는 다시 방문할 필요가 없어진다.   


## 2. Bellman-Ford Algorithm

### 궁금한점 꼭 V-1번을 돌려야 하나?
```python

def dijkstra(v, k, g):
    dist = [INF] * v
    dist[k - 1] = 0
    q = []
    heappush(q, [0, k-1])

    while q:
        cost, pos = heappop(q)

        for p, c in g[pos]:
            c += cost
            if c < dist[p]:
                dist[p] = c
                heappush(q, [c, p])
    return dist


V, E = map(int, r().split())
K = int(r())
graph = [[] for _ in range(V)]
for _ in range(E):
    u, v, w = map(int, r().split())
    graph[u-1].append([v-1, w])

for d in dijkstra(V, K, graph):
    print(d if d != INF else "INF")

```
이 코드는 디익스트라가 해결하지 못하는 음수 가중치값이 존재하는 경우에 대해 해결해준다. 
벨만포드 문제에 대해서도 다 해결해줄 것인가???????   

