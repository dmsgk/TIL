# TCP/IP Five-Layer Network Model

> 주요 내용: Physical layer, Data link layer, Network layer, Transport layer, Application layer

![TCP-IP Network Model](https://images.velog.io/images/dmsgk/post/c8de5b39-7306-4b76-8e25-20d933923b2f/TCP:IP%20Five-Layer%20Network%20Model.png)

## 1. Physical layer

- Represents the physical devices that interconnet computers
- is about cabling, connectors and sending signals

---

### Moving Bits Across the Wire

- Bit
  - 컴퓨터가 이해할 수 있는 가장 작은 단위의 데이터표현(0,1)

- Copper cable이 기기 간 연결되면 **modulation(변조)**이라는 프로세스를 통해 0, 1 데이터가 전달된다. 
  - Modulation:  A way of varying the voltage of this charge moving across the cable

### Twisted Pair Cabling and Duplexing

- 구리 선이 두 가닥으로 꼬아져 있어 twist pair
- 이러한 케이블은 **Duplex communication**을 가능케 한다.
  - Duplex communication : The concept that information can flow in both directions across the cable. 즉 양방향 전달이 가능하다.
    - Full - duplex : 양방향 커뮤티케이션이 동시에 일어날 수 있음
    - Half-duplex : 양방향 커뮤니케이션이 일어날 수 있지만 동시에 일어날 수는 없음
- [보충자료_Ethernet over twisted pair](https://en.wikipedia.org/wiki/Ethernet_over_twisted_pair)

### Network Ports and Patch Panels

- 가장 유명한 플러그는 RJ45. RJ45 네트워크 포트와 연결할 수 있음
- Network ports are generally directly attached to the devices that make up a computer network.
- 대부분의 네트워크 포트는 2개의 small led가 있다.(Link LED, Activity LED)
- Patch panel -  A device containing many network ports. But it does no other work. 

## 2. Data link layer

- is responsible for defining a common way of interpreting these signals so network devices can communicate
- 다른 layer가 Physical layer나 하드웨어가 어떻게 사용되는지 알 필요없이 작동하도록 한다.
- 예) 이더넷 

---

### Ethernet and MAC Addresses

- Individual link 간 데이터를 전송하는 프로토콜 중 가장 널리 쓰이는 것은 **이더넷**

  - 과거 두 컴퓨터가 동시에 데이터를 wire를 통해 보내면 collision이 발생했음. Ethernet as a protocol solved this problem by using a technique known as **carrier sense multiple access** with **collision detection**
    - **CSMA/CD** : used to determine when the communications channels are clear, and when a device is free to transmit data. Network segment에서 전달되는 데이터가 없으면 데이터를 전송하고, 동시에 두 개 이상의 컴퓨터가 데이터를 전송하려고 할 경우 데이터전송을 중단
  - Ethernet uses MAC addresses to ensure that the data it sends has both an address for the machine that sent the transmission, as well as the one that the transmission was intended for. 

- **MAC(Media Access Control) Address**

  ![img](https://upload.wikimedia.org/wikipedia/commons/thumb/9/94/MAC-48_Address.svg/1920px-MAC-48_Address.svg.png)

  - A globally unique identifier attached to an individual network interface
  - 48비트 숫자. 8bits * 6그룹 octet
    - Octet : In computer networking, any number that can be represented by **8 bits**
  - 처음 3개의 octets는 OUI(Organizatioinally Uniquee Identifier)
  - 뒤 3개의 octets는 NIC(Network Interface Controller)
    - can be assigned in any way that the manufacturer would like with the condition that they only assign each possible address once to keep all MAC addresses globally unique.

### Unicast, Multicast, and Broadcast

- **Unicast** 
  - is always meant **for just one receiving address**
  - MAC address에서 If the least significant bit in the first octet of a destination address is set to **zero**, it means that Ethernet frame is intended for only the destination address.
- **Multicast**
  - MAC address에서 If the least significant bit in the first octet of a destination address is set to **one**, it means you're dealing with a **multicast** frame.  
  - multicast frame은 모든 기기를 local network signal에 두는 것과 유사하다. What's different is that it will be accepted or discarded by each device depending on criteria aside from their own hardware MAC address.
- **Broadcast**
  - 이더넷 broadcast는 LAN을 기반하여 모든 기기에 보내진다.
  - Broadcast address
    - Ethernet broadcast address는 F들로 구성된다. `FF:FF:FF:FF:FF`

### Dissecting an Ethernet Frame

- Data packet

  - An all-encompassing term that represents any single set of binary data being sent across a network link
  - 이더넷 레벨에서의 데이터 패킷은 **Ethernet frame**으로 알려져 있다.

- Ethernet Frame

  ![img](https://upload.wikimedia.org/wikipedia/commons/thumb/4/42/Ethernet_frame.svg/570px-Ethernet_frame.svg.png)

  - Preamble
    - 8 bytes long, and can itself be split into two sections
    - 마지막 1바이트는 SFD(Start Frame Delimiter)
      - SFD: Signals to a receiving device that the preamble is over and that the actual frame contents will now follow
  - Destination MAC Address
    - The hardware address of the intended recipient
  - Source MAC Address
  - Ether-type field
    - 16bits long and used to describe the protocol of the contents of the frame
    - VLAN header
      - Indicates that the frame itself is what's called a VLAN(Virtual LAN) frame
        - VLAN : a technique that lets you have multiple logical LANs operatin on the same physical equipment
      - If a VLAN header is present, the Ether Type field follows it
  - Payload
    - In networking terms, is the actual data being transported, which is everything that isn't a header
  - FCS(Frame Check Sequence)
    - A 4 byte number that represents a checksum value for the entire frame. 
      - This checksum value is calculated by performng what's known as a cyclical redundancy check(CRC) against the frame

## 3. Network layer ( = Internet layer)

- Allows different networks to communicate with each other through devices known as routers
- 데이터가 네트워크들 간에 전달되도록 하는 계층
- 예) IP, Internet Protocol
- Internetwork 
  - A collection of networks connected together through routers, the most famous of these being the Internet

---

### Network Layer

#### IP addresses

- 32비트 길이. Four octet으로 구성
  - Dotted decimal notation(ex) 12.34.56.78
- 물리적 주소보다 더 위계적이며 쉽게 저장할 수 있다. 
- **IP address belong to networks**, not to the devices attached to those networks
- Dynamic IP address(⇔Static IP address)
  - 대부분의 경우 static ip address는 서버나 네트워크 기기에 사용되고, dynamic ip address는 클라이언트에 사용된다. 

#### IP datagram and encapsulation

- IP protocol에서 패킷은 IP datagram으로 불린다. 

![IPv4 Packet -en.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/7/71/IPv4_Packet_-en.svg/1920px-IPv4_Packet_-en.svg.png)

- Version: 4비트, 사용되는 프로토콜의 버전을 알려준다. 
- Header Length : 4비트. 총 헤더의 길이를 선언한다. 
- Service Type(TOS): 8비트. Can be used to specify details about quality of service, QoS technologies.
- Total length : 16비트. Ip datagram의 길이를 알려줌
- Identification: 16비트. Group messages together
- Flags: used to indicate if a datagram is allowed to be fragmented, or to indicate that the datagram has already been fragmented. 
- Fragment offset: process of taking a single IP datagram and splitting it up into several smaller datagrams. 
- TTL: 8비트. indicates how many router hops a datagram can traverse before it's thrown away. 
- Protocol: 8비트. 어떤 transport layer protocol이 사용되었는지 포함한다.
- Header checksum: a checksum of the contents of the entire IP datagram header. 
- Source IP address
- Destination IP address
- Options:  used to set special characteristics for datagrams primarily used for testing 
- Padding: a series of zeros used to ensure the header is the correct total size

#### IP address classes

- network ID, host ID 두 섹션으로 나뉜다.
- Address class system
  - A way of defining how the global IP address space is split up
  - 3 primary types of address classes: Class A, Class B, Class C
    - Class A
      - First octet은 network ID를 나타내고, 나머지 세 개가 host ID를 나타내는 방식
    - Class B
      - 처음 두 octets이 network ID, 나머지 두 개가 host ID
    - Class C
      - 처음 세 octetdl network ID, 나머지 하나가 host ID 나타냄

#### Address resolution protocol(ARP)

- A protocol used to discover the hardware address of a node with a certain IP address
- ARP table
  - a list of IP addresses and the MAC addresses associated with them
  - ARP table entries generally expire after a short amount of time to ensure changes in the network are accounted for

### Subnettig

- subnetting
  - 큰 네트워크를 개별적이고 작은 subnetworks, subnet 등으로 나누는 프로세스
  - 각각의 subnet들은 각자 gateway router가 있어 ingress, egress point를 제공할 수 있다.

## 4. Transport layer

- Sorts out whicth client and server programs are supposed to get that data
- TCP/UDP

## 5. Application layer

- 유저가 필요한 interface, protocol을 제공하는 계층



