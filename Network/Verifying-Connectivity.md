# Verifying Connectivity

## Ping: Internet Control Message Protocol

- 네트워크 에러가 발생했을 때 ICMP(Internet Control Message Protocol)가 사용된다.
  - ICMP는 주로 라우터에 의해 또는 원격 호스트에 의해 사용된다. 
  - ![](https://images.velog.io/images/dmsgk/post/dcbc3e29-6838-455c-b3b8-057ba74985c9/image.png)
  - The point is so that these sorts of error messages can be delivered between networked computers automatically.
  - But there's also a specific tool and two message types that are very useful to human operators. - Ping
- Ping 
  - Ping lets you send a special type of ICMO message called an **Echo Request**
  - If the destination is up and running and able to communicate on the network, it'll send back an ICMP **Echo Reply** message type

## Traceroute

- Traceroute
  - A utility that lets you discover the path between two nodes, and gives you information about each hop along the way

## Testing Port Connectivity

- Network layer가 아닌 transport layer에서 connectivity를 확인하고 싶을 때
  - netcat - Linux/MacOS
  - Test-NetConnection - Windows