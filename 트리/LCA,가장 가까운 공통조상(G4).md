## 가장 가까운 공통 조상
https://www.acmicpc.net/problem/3584

## 문제풀이
1. 트리의 표현
기존에는 부모가 자식노드의 정보를 가졌다면, 이 문제는 자식을 통해 부모를 찾아야하므로 자식이 부모의 노드를 저장하는 방식으로 트리를 표현해야한다.  
2. 공통 조상을 찾기 위해서는 두 노드의 깊이를 같게해야한다. 같은 깊이라고 가정한 뒤, 두 노드의 부모값을 비교하면서 같은 부모를 쭉 찾아나가면 된다.  
3. 노드의 깊이는 루트노드까지 부모를 찾는 횟수를 통해 구한다. 
4. 루느노드를 제외한 자식은 반드시 하나의 부모노드를 가진다. => 루트노드는 초기값을 가진다.

## 코드
```python
import sys

def getDepth(node):
    count=0
    
    while tree[node] != 0 :
        node = tree[node]
        count+=1
    
    return count

tree = {}
T = int(input())
result = []

for i in range(T):
    N = int(input())

    for i in range(1,N+1):
        tree[i] = 0

    for i in range(N-1):
        parent, child = map(int,sys.stdin.readline().split())
        tree[child] = parent
    
    a,b = map(int,sys.stdin.readline().split())

    aDepth = getDepth(a)
    bDepth = getDepth(b)

    while aDepth != bDepth:
        if aDepth > bDepth:
            a = tree[a]
            aDepth-=1
        else:
            b = tree[b]
            bDepth -=1
    
    while a!= b:
        a= tree[a]
        b= tree[b]
    result.append(a)

for ans in result:
    print(ans)


```

이 알고리즘의 문제점 O(N)

## 더나은 알고리즘 O(logN)
나중에 필요할 떄 공부
https://www.crocus.co.kr/660
