# QuickSort
## 코드
## QuickSort Code
```python
def QuickSort(ls, l,r):
    if n == 1:
        return
    pivot = ChoosePivot(A,n)
    Partition(A,l,r)
    Recursively sort 1st part of the array
    Recursively sort 2nd part of the array

```
## Partition code
### 2way
```python
def Partition_2way(A,l,r):
    p= A[l]
    i = l
    for j= l+1 to r:
        if A[j] <p :
            swap(A[j],A[i])
            i+=1
    swap(A[l],A[i])
```
### 3way
```python
def Partition_3way(A,l,r):
    p= A[l]
    i = l, h = l
    # i is the index where the smaller value comparing with p will be loocated
    # h is the index where the same value as p will be located. 
    for j = i+1 to r:
        if A[j] < p :
            swap(A[i],A[j])
            # if there is at least one value in this list eqaul to p , A[i] is same value as p. Suppose p1
            # therefore p1(A[i]) will be swapped with A[j]
            # so we have to locate p1 back to the original space in if statment
            if i!= h:
                # condition 'i!=h' means that there is currently at least one value in this list equal to p.
                swap(A[h],A[j])                
            i+=1
            h+=1
            #Since smaller value is swapped to the new position , move index i,h
        elif A[j] == p:
            swap(A[h], A[j])
            h+=1
            # Since same value is swapped to the new postition , move index h only
        
    swap(A[l],A[i])
    # swap p to it's positinon
```

#### 
