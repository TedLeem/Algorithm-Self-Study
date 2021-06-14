# Radix sort(Most efficient String sort Algorithm)
Key - Indexed Counting Algorithm   
=> key를 통해 본인이 들어갈 index(key에 해당하는 value)를 알아내는 알고리즘
1. 각 문자의 빈도수를 {문자 : 빈도수} 형태로 저장한다. (이때 주의해야할점은 맨 앞에 한 칸은 0으로 해주고 한칸씩 밀려서 저장하게끔 한다.)
2. {문자: 빈도수} 배열을 {문자: 정렬된 배열에서 문자의 인덱스}로 바꿔주는데 정렬된 배열의 인덱스는 그 전까지 문자의 빈도수를 순차적으로 더해줌으로서 얻을 수 있다.
3. 다시 원래 배열에 복사한다.

```python
Let 'A' is a array we want to sort.
'A' has size N , consist of  R character.
for i in range(N):
  cnt[ a[i] + 1 ] +=1
for i in range(R):
  cnt[i+1] = cnt[i]
for i in range(N):
  aux[cnt[a[i]]++] = a[i]
for i in range(N):
  a[i] = aux[i]

```

## MSD(Most Significant Digits)
가변 문자일일 경우? => MSD이용하되  
마지막에 우선순위가 낮은 '\n'을 추가하여 정렬 적용
### Resource
Time Complexitiy: O(WN) W는 문자열의 길이   
Space Complexity: O(R+ N)

### 단점
1. O(n) 추가 공간
2. O(DR) 추가공간 => count 저장배열
3. 무분별한 메모리접근 => 캐시 비효율
  
따라서 Radix sort의 장점과 Quick sort의 장점을 결합한 알고리즘이 있는데 그게 바로 3way radix quick sort이다.
# 3-way radix quick sort
https://www.geeksforgeeks.org/3-way-radix-quicksort-in-java/
