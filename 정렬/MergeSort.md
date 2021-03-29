# MergeSort
## 1. Top Down Approach
오랜만에 병합정렬 코드 짜봐서 은근 헷갈렸다..
## 핵심

## 실수했던 부분.
1. merge함수 while문 탈출조건을 or 말고 and로했었어야함
2. merge함수의 index를 0이아니라 left로 해줘야함
3. 처음에 mergesort호출할떄 mergesort(arr,0,len(arr)-1), 마지막이 배열의 크기가아니라 배열의 마지막인덱스로해주어야함, merge할떄 마지막까지 포함해서
## 흐름
1. 두개의 배열로 쭉 쪼갬 배열의 길이가 하나될때까지
2. 합침 
3. 합칠때, 각각의 원소를 비교, 이때 새로운 배열생성하므로 공간이 필요(auxilary space)
```python
def merge(arr, left, mid, right):

    size1 = mid-left +1
    size2 = right-mid

    leftArr = [0]*size1
    rightArr = [0]*size2

    #temp는 arr원소 참조의 목적용
    temp = left
    for i in range(size1):
        leftArr[i] = arr[temp]
        temp+=1
        #왼쪽배열 초기화
    for i in range(size2):

        rightArr[i] = arr[temp]
        temp+=1
        #오른쪽배열 초기화

    index = left
    index1= 0
    index2 =0
    
    #왼쪽과 오른쪽배열의 원소를 하나씩 비교해나가면서 합치기
    #둘중의 하나의 배열이라도 배열의 크기를 벗어나는 값을 참조하면 벗어나기
    while (index1 < size1 and index2 < size2 ):
        if leftArr[index1] <= rightArr[index2]:
            arr[index] = leftArr[index1]
            index1+=1
        else:
            arr[index] = rightArr[index2]
            index2+=1
        index+=1
    
    if index1 < size1:
        #왼쪽배열이 아직 다 참조되지않았다면
        for i in range(index1,size1):
            arr[index] = leftArr[i]
            index +=1
    if index2 < size2:
        #오른쪽 배열이 아직 다 참조되지않았다면
        for i in range(index2,size2):
            arr[index] = rightArr[i]
            index +=1

def mergesort(arr,left,right):
    #탈출조건
    if left >= right:
        return
    mid = (left+right)//2
    #divide left 
    mergesort(arr,left,mid)
    mergesort(arr,mid+1,right)
    merge(arr, left,mid,right)
    #divide right

```

## 2. Bottom-up Approach
