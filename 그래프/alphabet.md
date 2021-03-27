# 알파벳

# 코드
```python
import sys
import string

max = 0 
# 최대값

def dfs(i,j,count):

    global max
    # max라는 전역변수를 사용하겠다는 의미 근데 이거 재귀라서 매번 키워드가 적용되는데 괜찬흐려나>>

    hashArr[graph[i][j]] = True
    # check[i][j] = True
    count +=1 
    # res = max(count+1,res)
    if max < count:
        max = count
    
        # print(graph[i][j],end=' ')
    
    if i+1 <N  and not hashArr[graph[i+1][j]]   :
        # 주의해야할점은 범위 체크를 반드시 먼저해야함 
        # 안그러면 범위를 벗어난 배열의 값을 참조하여 index out of range 에러가 남
        # 즉 조건문에 순서에 주의하자 
        dfs(i+1,j,count) 
        # 아래쪽
    if j+1 < M  and not hashArr[graph[i][j+1]] :
        dfs(i,j+1,count) 
        # 오른쪽
    if i-1 >= 0  and not hashArr[graph[i-1][j]] :
        dfs(i-1,j,count) 
        # 위쪽
    if j-1 >= 0  and not hashArr[graph[i][j-1]] :
        dfs(i,j-1,count) 
        # 왼쪽
    hashArr[graph[i][j]] = False
    # 나올떄 False


N ,M= map(int,sys.stdin.readline().split(" "))
# graph = [[0]* M for x in range(N)]
if N==0 or M ==0 :
    print(0)
else:    
    graph = [[0]* (M+1) for x in range(N+1)]
    check = [[False]* M for x in range(N)]

    for i in range(N):
        graph[i] = list(sys.stdin.readline().replace('\n',''))
        # 문자열 한 글자씩 리스트로 바로 반환

    hashArr = dict()
    alpahbet = list(string.ascii_uppercase)

    for i in alpahbet:
        hashArr[i] = False
        # 해쉬딕셔너리에 알파벳 추가 
    dfs(0,0,0)
    print(max)
```

# 고칠수있는점
1. 배열의 범위를 주의했어야함  
0~N-1,  0~M-1 까지인데 나는 1부터 설정해서 계속 못돌았우... (범위 설정할때는 항상 양끝이 어떤 값을 지니는지 생각)
2. 리팩토링
  ```python
   res = max(count+1,res)
   # 아래를 위 한문장으로 쓸 수 있음
   count +=1 
    if max < count:
        max = count
   
  ```
3. 잘알려진 풀이법
``` python
dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]


def DFS(x, y, ans):
    global answer

    answer = max(ans, answer)

    # 좌우상화 다 확인한다
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]

        # index 벗어나지 않는지 체크하고, 새로운 칸이 중복되는 알파벳인지 체크한다
        if ((0 <= nx < R) and (0 <= ny < C)) and (board[nx][ny] not in passed):
            passed.append(board[nx][ny])
            DFS(nx, ny, ans+1)
            passed.remove(board[nx][ny])
```

