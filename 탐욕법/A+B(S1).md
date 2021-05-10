# 문제
https://www.acmicpc.net/problem/16953

## 핵심
1. B에서 A로 바꾸어나간다.(A<B이면 계속) 마지막 숫자가 무었이냐에 따라 계산을 다르게 한다.
   1일때 = B = B//10 
   짝수일때 => B = B//2
   1을 제외한 홀수일때 => 반복문을 빠져나와 A와 B를 비교한다.
   
~~2. 주의해야할 점이 문제에서 정답(최소 바꾼 횟수)에 +1을 더해서 출력하고 정답이 없을경우 -1으로 출력하라 하였다. 즉, count가 0이면 -1을 출력해줘야 한다.  
   ex: A= 1 B=1 , Ans = -1~~
   
## 내코드
```python
import sys

ls = list(map(int,sys.stdin.readline().split()))
A , B = ls[0], ls[1]
count =0 
def lastOne(num):
    num = num%10
    if num == 1:
        return 1
    elif num % 2 ==0 :
        return 2
    else:
        return -1

while A < B  :
    val = lastOne(B)
    if val == 1:
        B = B// 10 
    elif val == 2:
        B = B//2 
    else:
        break
    count +=1


if A == B:
    print(count+1)
else:
    print(-1)
```
## 다른풀이 : A에서 B로 순차적으로 해나가는방법도 있다. 
