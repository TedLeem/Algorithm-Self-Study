https://www.acmicpc.net/problem/5430

```python
import sys
from collections import deque

class NewArray:
    def __init__(self, ls) -> None:
        self.queue = deque(ls)
        self.pointer = True
        self.check = True
    def R(self):
        self.pointer = not(self.pointer)
    def D(self):
        if self.pointer == True:
            # 앞에를 가리키고 있다.
            self.queue.popleft()
        else:
            # 뒤를 가리킴
            self.queue.pop()
    def print(self):
        
        tempStr = ''
        
        tempStr += '['
        
        if self.pointer == True:
            # 앞에를 가리키고 있다.
            for i in range(len(self.queue)):
                if i == len(self.queue) -1 :
                    tempStr += str(self.queue[i])
                    # print(self.queue[i],end='')
                    break
                tempStr += str(self.queue[i])
                tempStr += ','
                # print(self.queue[i], end=',')

        else:
            for i in range(len(self.queue)-1,-1,-1):
                if i == 0 :
                    tempStr += str(self.queue[i])
                    # print(self.queue[i],end='')
                    break
                tempStr += str(self.queue[i])
                tempStr += ','
                # print(self.queue[i], end=',')
        tempStr += ']'
    
        return tempStr


T = int(input())
resultArr= []
for i in range(T):
    functionStr = sys.stdin.readline().rstrip()
    N = int(input())
    tempStr = sys.stdin.readline().rstrip()
    if N == 0:
        arr = []
        # print('error')
        # continue
    else:
        arr = list(map(int,tempStr[1:len(tempStr)-1].split(',')))

    newArr = NewArray(arr)    
    
    for i in range(len(functionStr)):
        if functionStr[i] == 'R':
            newArr.R()
        else:
            if len(newArr.queue) == 0:
                resultArr.append('error')
                newArr.check = False
                break
            newArr.D()
    if newArr.check == True:
        resultArr.append(newArr.print())

for i in resultArr:
    print(i)

```
