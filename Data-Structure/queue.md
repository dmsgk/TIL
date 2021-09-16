## 1.0. Queue

- FIFO(First in, first out)의 자료구조
- Queue의 종류
  - 선형 큐
  - 원형 큐(Circular queue)

## 1.1. 선형 큐

- BFS 구현에 사용된다.
- 캐싱 처리에 구현
- 선형 큐는 데이터를 집어넣는 Enqueue 기능과 데이터를 내보내는 Dequeue 기능을 제공
- 데이터가 들어오는 부분을 rear, 나가는 부분을 front라고 한다.

### Enqueue

데이터를 넣어주는 기능을 수행. 마지막 데이터의 위치가 변하므로 **rear**이 **-1**만큼 이동한다.

![img](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/152a69e7-c10a-4a2a-a57b-5c518691f92b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210916%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210916T023631Z&X-Amz-Expires=86400&X-Amz-Signature=5e0a73438723b32c29e0ebe32189fd94a03288e498caf7ae6c2d7d0c239efb9e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

### Dequeue

데이터를 내보내는 기능을 수행. 맨 앞에 있는 데이터가 바뀌므로 **front**가 +1만큼 이동한다.

![img](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c3259ed3-9775-4e43-b6d0-5ed1069fb9fe/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210916%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210916T023707Z&X-Amz-Expires=86400&X-Amz-Signature=36cac39d62649c974d0309a7afc6c5a1ad6d3f49de479ce4aee2b7ee731d9451&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

### 선형 큐의 단점

- 일반적인 선형 큐는 rear이 마지막 index를 가르키면서 데이터의 삽입이 이루어진다. 문제는 rear이 배열의 마지막 인덱스를 가르키게 되면 앞에 남아있는 (삽입 중간에 Dequeue 되어 비어있는 공간) 공간을 활용 할 수 없게 된다. 이 방식을 해결하기 위해서는 Dequeue를 할때 front를 고정 시킨 채 뒤에 남아있는 데이터를 앞으로 한 칸씩 당기거나 원형 큐를 사용해야 한다.

  ![img](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c3ab6b0a-19ed-4660-87e0-d7c3174aa440/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210916%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210916T023733Z&X-Amz-Expires=86400&X-Amz-Signature=a1ba0a4aa8497b9ddaa593968a5e7aa2079be9695c489bf7efe34e9aad37c3e9&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

### 파이썬에서 큐 사용하기 - `from collections import deque`

- collections 모듈을 활용한 deque로 `popleft()`와 `appendleft()`를 사용한다.

```python
from collections import deque 

queue = deque()
queue.append(1)
queue.append(2)
queue.popleft() # 1
queue.popleft() # 2
```



## 1.2. 원형 큐

큐 앞의 공간을 활용할 수 있어, 기존 선형 큐의 단점을 보완할 수 있다.

### 파이썬으로 원형 큐 구현하기

**Class생성, init**

```python
MAX_QSIZE = 10
class CircularQueue :
    def __init__(self):
        self.front = 0
        self.rear = 0
        self.items = [None] * MAX_QSIZE
```

MAX_QSIZE를 사용하여 원형 큐의 크기를 지정해준다.이후에 원형 큐 클레스를 작성하고 `__init__`메소드를 사용해서 원형큐에 필요한 front와 rear을 선언해준다. item은 파이썬의 list를 사용하여 None으로 큐의 크기만큼 만들어준다.

**isEmpty**

```python
def isEmpty(self):
        return self.front == self.rear
```

큐가 비었는지 확인한다 **.front와 rear가 같은 위치를 가르키고 있다면** 큐가 비어있는 것이다.

**isFull**

```python
def isFull(self):
        return self.front == (self.rear+1)%MAX_QSIZE
```

큐가 꽉 찼는지 판단한다.

![https://media.vlpt.us/images/changyeonyoo/post/fb7fe30d-49c5-4328-8e75-69276768ef37/image.png](https://media.vlpt.us/images/changyeonyoo/post/fb7fe30d-49c5-4328-8e75-69276768ef37/image.png)

이처럼 rear가 가르키는 인덱스의 다음 인덱스를 front가 가르키고 있다면 원형 큐는 꽉 찼다고 말한다.큐의 크기와 나머지 연산을 사용해서 rear가 가르키고 있는 인덱스를 찾아서 판단한다.

**clear**

```python
def clear(self):
        self.front = self.rear
```

큐를 초기화 하기 위해서는 front를 rear가 가르키고 있는 인덱스로 가게해서 원형 큐의 초기상태를 만들어준다.

**enqueue**

```python
def enqueue(self, item):
        if not self.isFull():
            self.rear = (self.rear + 1) % MAX_QSIZE
            self.items[self.rear] = item
```

원형 큐에 데이터를 삽입하기 전에 큐가 포화상태인지 먼저 판단한다.포화상태가 아니라면 rear를 한칸 옮기고 rear가르키고 있는 인덱스에 값을 저장한다.

**dequeue**

```python
def dequeue(self):
        if not self.isEmpty():
            self.front = (self.front+1) % MAX_QSIZE
            return self.items[self.front]
```

원형 큐에서 데이터를 지우기 위해서는 먼저 큐가 비어있는지 판단한다.큐가 비어있지 않다면 front를 옮겨줌으로써 큐 안에 있는 데이터를 지운다.이후 비어지는 데이터를 반환한다.

**peek**

```python
def peek(self):
        if not self.isEmpty():
            return self.items[(self.front+1)%MAX_QSIZE]
```

원형큐가 비어있는지 먼저 판단하고 front의 다음 인덱스 안에 있는 값을 반환한다.큐 크기와 나머지 연산을 사용해 인덱스를 계산할 수 있다.

**전체 코드**

```python
MAX_QSIZE = 10
class CircularQueue :
    def __init__(self):
        self.front = 0
        self.rear = 0
        self.items = [None] * MAX_QSIZE

    def isEmpty(self):
        return self.front == self.rear

    def isFull(self):
        return self.front == (self.rear+1)%MAX_QSIZE

    def clear(self):
        self.front = self.rear

    def __len__(self):
        return (self.rear - self.front + MAX_QSIZE) % MAX_QSIZE

    def enqueue(self, item):
        if not self.isFull():
            self.rear = (self.rear + 1) % MAX_QSIZE
            self.items[self.rear] = item

    def dequeue(self):
        if not self.isEmpty():
            self.front = (self.front+1) % MAX_QSIZE
            return self.items[self.front]

    def peek(self):
        if not self.isEmpty():
            return self.items[(self.front+1)%MAX_QSIZE]

    def print(self):
        out = []
        if self.front < self.rear:
            out = self.items[self.front+1:self.rear+1]
        else:
            out = self.items[self.front+1:MAX_QSIZE] + self.items[0:self.rear+1]

        print("[f=%s, r=%d] ==> "%(self.front, self.rear), out)

class CircularDeque(CircularQueue):

    def __init__(self):
        super().__init__()

    def addRear (self, item):
        self.enqueue(item)

    def deleteFront (self):
        return self.dequeue()

    def getFront(self):
        return self.peek()

    def addFront(self, item):
        if not self.isFull():
            self.items[self.front] = item
            self.front = (self.front - 1 + MAX_QSIZE) % MAX_QSIZE

    def deleteRear(self):
        if not self.isEmpty():
            item = self.items[self.rear]
            self.rear = (self.rear - 1 + MAX_QSIZE) % MAX_QSIZE
            return item

    def getRear(self):
        return self.items[self.rear]
```



## 1.3. 연결리스트 큐

원형 큐의 단점 : 메모리 공간은 잘 활용하지만, 배열로 구현되어 있기 때문에 큐의 크기가 제한된다.

이를 개선한 것이 '연결리스트 큐'

**연결리스트 큐는 크기가 제한이 없고 삽입, 삭제가 편리**

### enqueue 구현

```java
public void enqueue(E item) {
    Node oldlast = tail; // 기존의 tail 임시 저장
    tail = new Node; // 새로운 tail 생성
    tail.item = item;
    tail.next = null;
    if(isEmpty()) head = tail; // 큐가 비어있으면 head와 tail 모두 같은 노드 가리킴
    else oldlast.next = tail; // 비어있지 않으면 기존 tail의 next = 새로운 tail로 설정
}
```

> 데이터 추가는 끝 부분인 tail에 한다.기존의 tail는 보관하고, 새로운 tail 생성큐가 비었으면 head = tail를 통해 둘이 같은 노드를 가리키도록 한다.큐가 비어있지 않으면, 기존 tail의 next에 새로만든 tail를 설정해준다.

### dequeue 구현

```java
public T dequeue() {
    // 비어있으면
    if(isEmpty()) {
        tail = head;
        return null;
    }
    // 비어있지 않으면
    else {
        T item = head.item; // 빼낼 현재 front 값 저장
        head = head.next; // front를 다음 노드로 설정
        return item;
    }
}
```

> 데이터는 head로부터 꺼낸다. (가장 먼저 들어온 것부터 빼야하므로)head의 데이터를 미리 저장해둔다.기존의 head를 그 다음 노드의 head로 설정한다.저장해둔 데이터를 return 해서 값을 빼온다.

이처럼 삽입은 tail, 제거는 head로 하면서 삽입/삭제를 스택처럼 O(1)에 가능하도록 구현이 가능하다.

### 



### References

- https://lktprogrammer.tistory.com/47?category=676210

- https://mailmail.tistory.com/33

- https://velog.io/@changyeonyoo/자료구조python-원형큐-덱-CircularQueue-CircularDeque-구현

- 

  

