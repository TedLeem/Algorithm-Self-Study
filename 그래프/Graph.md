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
