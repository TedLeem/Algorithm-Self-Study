# Ways to check Cyclic
해당 그래프가 순환그래프인지를 확인하는 알고리즘 여러가지를 확인해보자.

## 1. Disjoint Set의 Union-Find 
조건: 자신을 가리키는 Vertex는 없어야 한다. 무방향그래프이어야 한다. 

1. 서로 다른 집합(Disjoint set)의 __루트노드__ 를 비교한다.__(반드시 두 노드의 루트노드들을 비교해야한다.)__
2. 두 루트노드가 같다면 합쳤을때 순환그래프를 형성하게 된다.
3. 두 류투노드가 다르다면 두 집합을 합쳐도 순환그래프를 형성하지 않는다.
4. 두 루트노드를 합칠 때, 어떤 노드를 루트로 할 지의 기준은 루트노드의 값으로 결정한다. 여기서는 작은 값.  
 
#### 시간복잡도 : logN (이진트리여서)

```python
def find(self, vertex_name):
        if self.parent[vertex_name]!= vertex_name:
            return self.find(self.parent[vertex_name])
        else:
            return self.parent[vertex_name]
    

def is_cycle(self, vertex_from_name, vertex_to_name):

        root_from = self.find(vertex_from_name)
        root_to = self.find(vertex_to_name)

        if root_from != root_to:
            # union할 집합의 부모가 루트노드가 다르다면 합쳐도 순환하지않음을 의미
            if root_from > root_to:
                self.parent[root_from] = root_to
            else:
                self.parent[root_to] = root_from
            return False
        else:
            return True

```

## 2. DFS 
```python
def dfs_cycle(self,cur_vertex_name, pre_vertex_name, visitied,check):
        #현재 dfs단계와, 이전노드의 정보
        ls = self.vertices[cur_vertex_name]
        # 현재 vertex의 연결된 리스트
        
        for i in ls :
            vertex_name = i[0]
            if vertex_name == pre_vertex_name :
                # 다음 노드가 이전노드에서 온 노드를 찾았거나, 
                continue
            if visitied[vertex_name] == True:
                # 이미 방문한 노드라면 
                check[0] = True
                # 재귀는 반드시 End Condition using check wheter non-promising node             
                return
            visitied[vertex_name] = True
            self.dfs_cycle(vertex_name,cur_vertex_name,visitied,check)
            
def is_cycle(self, vertex_init_name):
        visitied = {}
        init = 0
        check = [False]

        for i in self.vertices.keys():
            visitied[i] = False     
            #방문배열 초기화
        
        visitied[vertex_init_name]=True
        # dfs시작 vertex 정해주기 
        self.dfs_cycle(vertex_init_name, vertex_init_name, visitied,check)
        if check[0] == True:
            return True
        else :
            return False 


```
