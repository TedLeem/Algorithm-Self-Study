# Implemntation of Graph using python
We have to define __Vertex and Graph__ class first.   
Vertex 
- Node 
- Neighbors[nodes connecting with edges, weights of edge]
Graph is represented with dictionary.   
### Vertex 
```python
class Vertex:
    def __init__(self, vertex):
        self.name = vertex
        self.neighbors = []
        # (노드이름 , 간선가중치)
        

    def add_neighbor(self, neighbor, weight):
        if isinstance(neighbor, Vertex):
            if neighbor.name not in self.neighbors:
                self.neighbors.append((neighbor.name,weight))
                neighbor.neighbors.append((self.name,weight))
                
                #self.neighbors = sorted(self.neighbors) //정렬해줘야하나?
                #neighbor.neighbors = sorted(neighbor.neighbors)
        else:
            return False
        
    def add_neighbors(self, neighbors):
        for neighbor in neighbors:
            self.add_neighbor(self,neighbor[0],neighbor[1])
            
        
    def __repr__(self):
        return str(self.neighbors))
```
### Graph
```python
class Graph:
    def __init__(self):
        self.vertices = {}
    
    def add_vertex(self, vertex):
        if isinstance(vertex, Vertex):
            self.vertices[vertex.name] = vertex.neighbors

            
    def add_vertices(self, vertices):
        for vertex in vertices:
            if isinstance(vertex, Vertex):
                self.vertices[vertex.name] = vertex.neighbors
            
    def add_edge(self, vertex_from, vertex_to,weight ):
    
        vertex_from = Vertex(vertex_from)
        vertex_to = Vertex(vertex_to)
        
        vertex_from.add_neighbor(vertex_to,weight)
        if isinstance(vertex_from, Vertex) and isinstance(vertex_to, Vertex):
            self.vertices[vertex_from.name] = vertex_from.neighbors
            self.vertices[vertex_to.name] = vertex_to.neighbors


    def add_edges(self, edges):
        for edge in edges:
            self.add_edge(edge[0],edge[1])  
    # def __repr__(self):
         
    #     if len(self.vertices) >= 1:
    #             ls = [str(key) + ":" + str(self.vertices[key]) for key in self.vertices.keys()]  
    #     else:
    #         ls = dict()
    #     print(ls)

```

### Application
first init Vertex and make a graph using created vertexes.  
code will be customized depending on problems.

```python
V,E = map(int,sys.stdin.readline().split())
graph = Graph()
for i in range(E):
    vertex_from , vertex_to, weight = map(int,sys.stdin.readline().split())
    graph.add_edge(vertex_from,vertex_to,weight)


```


## 1. Undirect Graph
### 1. Adjacency Linked list
```python

```

### 2. Adjacency Matrix
```python

```

## 2. Direct Graph
### 1. Dicitionary 

## 3.트리와 그래프의 관계  
만일 그래프에 단 하나의 사이클도 없다면, 해당 그래프는 ‘트리’ 라고 부른다.
이는 그래프가 마치 하나의 정점에서 출발해 피어난 나무 모양과도 같음에 붙여진 이름이다.
그래프는 항상 루트를 기준으로 다시 그릴 수 있기 때문에, 루트가 고정되지 않는 한 어떤 정점이 ‘위에’ 있는지 판정할 수는 없다.
하지만 루트가 고정된다면, 우리는 정점 간에 ‘부모’ 와 ‘자식’ 의 관계를 정의할 수가 있다.
트리에는 몇 가지 중요한 성질이 있는데, 그 중 두 가지만 추려보자면 아래와 같다.

임의의 두 정점 U와 V에 대해, U에서 V로 가는 최단경로는 유일하다.
아무 정점이나 잡고 부모와의 연결을 끊었을 때, 해당 정점과 그 자식들, 그 자식들의 자식들… 로 이루어진 부분그래프는 트리가 된다.
둘 모두 직관적이며 자명한 사실이므로 증명은 생략한다. 두 번째 성질에서, 끊어진 부분그래프로 만들어진 트리를 ‘서브트리’ 라고 부른다. 트리에서의 간선의 개수는 항상 정점의 수 - 1이라는 것은 익히 알려진 사실이며, 증명 또한 어렵지 않으므로 설명을 생략한다.

## Most Popular Problems using Graph
1. Path: Finding a path between two nodes
2. Shortest Path: Finding the shortest path between two nodes 
3. Cycle : Is there a Cycle (a cycle is a non-empty path from a node to itself)
4. Euler tour : Is there a cycle that uses each edge exactly once?
5. Hamilton tour: Is there a cycle that usese each vertex exactly once?
6. Connectivity : Is there a way to connect all of vertices?
7. MST(Miniumn Spanning Tree): What is the best way to connect all of the vertices?
8. Biconnectivity: Is there a vertex whose removal disconnects the graph?
9. Bipartite : Can you divide the vertices into two bipartite groups such that every edge has one vertex from each group?
10. Planarity : Can you draw the graph in the plane with no crossing edge?
11. Graph isomorphism : Do two adjacency lists represent the same graph?
12. ...

I will continously update the solution per each problem.


