# Shortest Path
문제  
최단경로: https://www.acmicpc.net/problem/1753

## 1. 디익스트라 알고리즘
핵심: 가야할 edge를 선택할때 __그 순간에__ weight이 가장 작은 간선을 선택하는(Greedy) 선택을 한다. 
1. 방문하지 않는 노드중 가장 dist[v]값이 작은 노드(v)를 선택한다. 
2. 선택한 노드의 연결된 간선들중 방문하지 않은 노드(w)와 연결된 간선(e: v->w)을 모두 추가한다.
3. 만약 ( dist[v] + edge.weight > dist[w])이면 weight을 업데이트 한다.
4. 마지막에 백트랙킹을 통해 shortest path를 구한다.



### 의문점 
위의 2번쨰 순서에서 선택한 노드의 연결된 간선들중 __방문하지 않은 노드(w)__ 와 연결된 간선(e: v->w)를 추가한다고 했는데
이미 한 번 방문한 노드여도 상관 없지 않나..?
## 2. Bellman-Ford Algorithm
