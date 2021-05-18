# 문제모음
https://www.acmicpc.net/step/34

## 핵심
M길이의 수열을 생성한다고 치자.(abc)   
다음 i,j를 생각하여 트리를 만들자.  
i는 트리의 깊이, 순열의 index를 가리킴 
j는 순열의 i인덱스에 들어갈 숫자를 가리킴
백트래킹을 이용하면 된다.  

### Non promising node 확인 조건
1. 방문여부
2. 방문여부 + 오른차순인지 (j+1 > stringLs[i-1] )
3. 없음
4. 오름차순인지


## N과 M(1)
```python
import sys
from types import TracebackType

N,M = map(int,sys.stdin.readline().split())
stringLs = [0]*M
visited = [False]*N


def dfs(i):
    if i== M:
        print(*stringLs)
        return
    
    for j in range(N):
        if visited[j] == False:
            stringLs[i]= j+1
            visited[j]= True
            dfs(i+1)
            visited[j] = False

dfs(0)
            
```

## N과 M(2)
```python
import sys
from types import TracebackType

N,M = map(int,sys.stdin.readline().split())
stringLs = [0]*M
visited = [False]*N


def dfs(i):
    if i== M:
        print(*stringLs)
        return
    
    for j in range(N):
        if visited[j] == False:
            if i ==0 :
                stringLs[i]= j+1
                visited[j]= True
                dfs(i+1)
                visited[j] = False
            
            elif i>0:
                if j+1 > stringLs[i-1]:                
                    stringLs[i]= j+1
                    visited[j]= True
                    dfs(i+1)
                    visited[j] = False

dfs(0)
```
### 간결코드
```
def dfs(i, num):
    if i== M:
        print(*stringLs)
        return
    
    for j in range(num, N):
    # 그전 녀썩 보다 큰 숫자들부터 반복문 시작 
        if visited[j] == False:
          stringLs[i]= j+1
          visited[j]= True
          dfs(i+1, j+1)
          visited[j] = False
```

## N과 M(3)
```python
import sys
from types import TracebackType

N,M = map(int,sys.stdin.readline().split())
stringLs = [0]*M

def dfs(i):
    if i== M:
        print(*stringLs)
        return
    
    for j in range(N):       
        stringLs[i]= j+1    
        dfs(i+1)
        

# i는 트리의 깊이, 순열의 자리 
# j는 순열의 자리에 들어갈 숫자 
# ls

dfs(0)
            
```
## N과 M(4)
```python
import sys
from types import TracebackType

N,M = map(int,sys.stdin.readline().split())
stringLs = [0]*M
visited = [False]*N


def dfs(i):
    if i== M:
        print(*stringLs)
        return
    
    for j in range(N):
        if i==0:
            stringLs[i]= j+1
            dfs(i+1)
            
        else:
             if j+1 >= stringLs[i-1]:
                stringLs[i]= j+1
                dfs(i+1)
                
dfs(0)        
```

### Other method to solve permutation
```python
def permutation(lst):
  
    # If lst is empty then there are no permutations
    if len(lst) == 0:
        return []
  
    # If there is only one element in lst then, only
    # one permuatation is possible
    if len(lst) == 1:
        return [lst]
  
    # Find the permutations for lst if there are
    # more than 1 characters
  
    l = [] # empty list that will store current permutation
  
    # Iterate the input(lst) and calculate the permutation
    for i in range(len(lst)):
       m = lst[i]
  
       # Extract lst[i] or m from the list.  remLst is
       # remaining list
       remLst = lst[:i] + lst[i+1:]
  
       # Generating all permutations where m is first
       # element
       for p in permutation(remLst):
           l.append([m] + p)
    return l
  
  
# Driver program to test above function
data = list('123')
for p in permutation(data):
    print p****
```
