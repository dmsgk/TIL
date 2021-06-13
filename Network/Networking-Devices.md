# Networking Devices

## Cables

- Connect different devices to each other, allowing data to be transmitted over them
- Two categories
  - Copper : binary값에 따라 전압을 바꿔가며 신호를 전달
  - Fiber : pulses of light을 사용해 신호를 전달. 구리 케이블보다 빠르게 데이터를 전송할 수 있고 구리케이블보다 장거리로 데이터 전달이 가능함. 그러나 가격이 비싸고 내구성이 약함

## Hubs and Switches

The primary device used to connect computers on a single network, usually referred to as a LAN, or local area network

- ### Hubs

  - A physical layer device that allows for connections from many computers at once
  - Collision domain을 유발하기도 한다.
    - Collision domain: 
      - A network segment where only one device can communicate at a time
      - If multiple systems try sending data at the same time, the electrical pulses sent across the cable can interfere with each other 
      - 네트워크 통신속도를 저하시킴
  - 현재는 많이 쓰지 않음

- ### Switches

  - 여러 기기를 연결하기 위한 방법으로 허브보다 스위치를 현재 많이 사용한다. 
  - 허브와의 차이점은 허브는 하나의 physical layer device지만, 스위치는 둘의 layer 또는 data link device라는 점이다. 이는 collision을 줄이거나 아예 없앨 수 있다.

## Routers

- A device that knows how to forward data between independent networks
- Network layer device이다.
- Routers share data with each other via a protocol known as **BGP(Border Gateway Protocol)**
  - 이는 가장 최적의 경로를 찾도록 해준다.

## Servers and Clients

대부분의 node는 완전히 서버이거나 클라이언트라고 할 수 없다. 서버와 클라이언트 역할을 함꼐 수행한다. 

### Server 

- 데이터를 요청한 곳에 데이터를 제공하는 역할을 하는 부분

### Client

- 데이터를 요청하고 데이터를 받는 부분

