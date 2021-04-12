# 연결 리스트(Linked List)

### 연결리스트

- 데이터와 다음주소를 담고 있는 노드가 한 줄로 연결되어 있는 방식의 자료구조

- 연결되는 방식에 따라 다음과 같이 구분한다.

  - Singly linked list(단일 연결리스트)
  - Doubly linked list(이중 연결리스트)
  - Circular linked list(환형 연결리스트)

  ![img](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/68a2472d-f515-46ee-8de8-577ea3757821/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210412%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210412T092339Z&X-Amz-Expires=86400&X-Amz-Signature=691fe8a829ecc940419864f01533f7885da198826e4dc8da40b20b1d3a67c74b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

### 연결리스트의 장단점

#### 장점

- linked list 길이를 동적으로 조정할 수 있다.
- 데이터의 삽입과 삭제가 용이하다.

#### 단점

- 임의의 노드에 바로 접근할 수 없고, 첫 노드부터 탐색해야 한다.

- 다음 위치를 저장하기 위한 추가 공간이 필요하다.

- Linked list를 거꾸로 탐색하기 어려움

- cash locality를 활용해 근접 데이터를 사전에 캐시에 저장하기 어려움

  



## References

- https://daimhada.tistory.com/72