# HuffMan Coding
## Problem
데이터를 전송하기 위해 데이터(문자열-> 2진 인코딩)를 압축한다고 하자.   
어떻게 하면 정보의 손실 없이 가장 적은 비트의 길이로 데이터를 압축할 것인가?   
이 문제의 가장 중요한 keyPoint는 다음 두가지이다.

### 1. 각 문자의 인코딩된 비트는 prefix-free code이어야 한다.
prefix(접두어)는 어떤 단어(어근)의 앞에 붙어 뜻을 첨가하여 하나의 다른 단어를 이루는 말을 이룬다. 
그렇다면 prefix-free code란 해당 binary code에 다른 문자를 표현하는 binarycode가 포함되지 않는 코드를 말한다.   
인코딩할떄 반드시 prefix code를 사용해야 하는 이유는 디코딩 하는 과정에서 Ambiguity해지기 때문이다.  

>ex: Suppose U = {A,B,C,D} is encoded using variable-length code {0,01,10,1} what is 001 an encoding of?   
AB,AAD 등으로 디코딩이 가능하므로 Ambiguity하다고 한다.   
이 문제는 binary tree를 통해 표현하면 간단해진다. 
각 문자들이 tree의 leafnode들이라면, 해당 트리는 반드시 prefix-freecode를 만족하게 된다.    
반대로 말하면, tree를 생성했을때, 모든 문자에 대해 어느 하나의 문자라도 트리의 leaf node로 구성되어있지 않고 어떤 leafnode의 parent node로 구성되어있다면 그건 prefix-free code를 만족하지 않는다. 
자세한건 (binary prefix-tree)를 찾아봐라.   

### 2. 가장 적은 길이의 binarycode로 인코딩 해야 한다.
이제 두 번째 조건을 만족하는 binary prefix tree를 만들어야 한다. 각 문자의 길이를 어떤걸 제일 짧게 하면 좋을까?    
#### 그렇다. 가장 자주사용되는 문자를 가장 짧은 비트로 표현해야 좋다.    
이 점을 이용하면 우리가 트리를 생성할때, frequency(자주사용하는횟수)가 낮은 문자일수록 가장 깊은 level에 위치시켜야 함을 알 수 있다.   
그렇다면 트리가 완성되었을 때, 다음을 알 수 있다. 
#### k번쨰 level에 위치해있는 문자의 인코딩된 binarycode의 길이는 k이다. 

## 구현
자, 이제 구현을 해보자.   
이 문제를 구현하기 위한 자료구조는 MinHeap을 사용할 것이다.  
heap은 가장 우선순위가 높은 노드를 반환해준다. (가장 freq이 낮은 두 노드의 값을 뽑을 거임)   
힙 트리생성 시간복잡도 : O(NlogN) => (데이터개수:N  X 추가: logN)  
### prefix-free-tree 생성
1. 각 문자에 대하여 leaf 노드를 만든 뒤 해당 노드들을 이용하여 최소힙을 만든다. (이때 노드는 freq,char의 데이터로 구성됌)
2. 힙에서 두개의 노드를 꺼낸 뒤 두개 노드의 freq을 합한 값을 이용하여 새로운 노드를 만든다. 
3. 해당 노드의 leftChild 노드(더 작은녀석)와 rightChild 노드에 각각 힙에서 꺼낸 두 노드로 순서대로 연결한다. 합해진 값을 가진 노드는 다시 힙에 추가한다.
4. 힙에 노드가 하나가 남겨질때까지 2,3과정을 반복한다.

``` c
struct MinHeapNode* buildHuffmanTree(char data[], int freq[], int size){

    struct MinHeap * minHeap = createAndBuildMinHeap(data,freq,size);

    while (!isSizeOne(minHeap)){
        struct MinHeapNode * leftNode = extractMin(minHeap);
        struct MinHeapNode * rightNode = extractMin(minHeap);

        struct MinHeapNode * top = MinHeapNode('$',leftNode->freq + rightNode->freq);
        top->left = leftNode;
        top->right = rightNode;
        insertMinHeap(top);
    }
    
    return extractMin(minHeap);

}


```

### 코드 읽기
전위순회(preorder traversal) 방법을 이용하여 트리를 읽어내려가면 해당 문자에 대한 인코딩된 binarycode를 확인할 수 있다.   
