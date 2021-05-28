# REST API

> 주요 내용: API, REST의 개념, REST 구성, REST 특징, HTTP METHOD

## API(Application-Programming-Interface)

- 소프트웨어가 다른 소프트웨어로부터 지정된 형식으로 요청, 명령을 받을 수 있는 수단

## REST

### REST 개념

- REST는  **Representational State Transfer**의 약자

- HTTP를 효율적으로 사용하기 위한 Architecture Style 

### REST 구성

REST API는 다음의 구성으로 이루어짐

- **자원(RESOURCE)** - URI
- **행위(Verb)** - HTTP METHOD
- **표현(Representations)**

### REST 의 특징 (RESTful한 상태)

#### 1) Uniform (유니폼 인터페이스)

>  Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 의미

#### 2) Stateless (무상태성)

> REST는 작업을 위한 상태정보를 따로 저장하고 관리하지 않음.  세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 된다. 때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해짐

#### 3) Cacheable (캐시 가능)

> REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능하다는 것.  따라서 HTTP가 가진 캐싱 기능이 적용 가능함. HTTP 프로토콜 표준에서 사용하는 Last-Modified태그나 E-Tag를 이용하면 캐싱 구현이 가능.

#### 4) Self-descriptiveness (자체 표현 구조)

> REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것

#### 5) Client - Server Architecture

> REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어들게 된다.

#### 6) 계층형 구조

> REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 한다.



## REST API에서 사용하는 HTTP METHOD

각각의 method들이 목적에 따라 구분되어 있는 것은 아니나, 누구나 각 요청의 의도를 쉽게 파악할 수 있도록 RESTfu하게l API를 만들기 위해서는 각각을 목적에 따라 사용하는 것이 좋다. 

### HTTP GET : Read. 데이터 조회

### HTTP POST: Create. 새로운 정보 추가

### HTTP DELETE: 리소스 삭제

### HTTP PUT: 현재 존재하는 리소스의 전체적인 업데이트

### (HTTP Patch): 부분 리소스의 업데이트





### References

- https://www.redhat.com/ko/topics/api/what-is-a-rest-api
- https://www.youtube.com/watch?v=iOueE9AXDQQ
- https://sabarada.tistory.com/29



