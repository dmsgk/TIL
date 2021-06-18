# Wireless Networking

## 802.11 

- The most common specifications for how wireless networking devices should communicate, are defined by the **IEEE 802.11 standards.**

  -  Different 802.11 standards generally use the same basic protocol, but might operate at different frequency bands. 
    - A frequency band: is a certain section of the radio spectrum that's been agreed upon to be used for certain communications. 

- The most common  802.11  specifications :  `802.11b, 802.11a, 802.11g, 802.11n, and 802.11ac` 

- define how we operate at both the physical and the data link layers. 

- has a number of fields

  ![802.11 Frame Format | mrn-cciew](https://mrncciew.files.wordpress.com/2013/03/802-11-frames-01.png)

  - Frame Control Field
    - Is 16 bits long and contains a number of subfields that are used to describe how th frame itself should be processed
  - Duration Field
    - It specifies how long the total frame is, so the receiver knows how long it should expect to have to listen to this transmission
  - Wireless access point
    - A device that bridges the wireless and wired portions of a network
    - 4 address fields cause there needs to be room to indicate which wireless access point should be processing the frame
  - ![](https://images.velog.io/images/dmsgk/post/b2209c8d-0a69-473a-8e93-b0ee66fb67ff/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-18%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2010.55.17.png)
  - Sequence Control Field
    - Is 16 bits long and mainly contains a sequence number used to keep track of the ordering of frames
  - ​	Data payload
    - Has all of the data of the protocols further up the stack
  - Frame check sequence field
    - Contains a checksum used for a cyclical redundancy check, just like how ethernet does it

## Wireless Network Configurations

### Ad-hoc

- Ad-hoc networks are the simplest of the three, in an ad-hoc network, there isn't really any supporting network infrastructure. 
- Every device involved with the network communicates with every other device within range and all nodes help pass along messages

### Wireless LANS(WLANS)

- A wireless LAN consists of one or more **access points**, which act as bridges between the wireless and wired networks. 
- In order to access resources outside of the WLAN, wireless devices would communicate with access points. 
- They then forward traffic along to the gateway router, where everything proceeds like normal.

### Mesh network

- If you were to draw lines for all the links between all the nodes, most mesh networks you'll run into are made up of only wireless access points and will still be connected to a wired network.



## Wireless Channels

- Channels
  - Individual, smaller sections of the overall frequency band used by a wireless network

-  these channels can overlap for all of the 802.11 specifications causing bad wireless connectivity problems or slowdowns in the network. 

## Wireless Security

- Wireless networking에서는 radiowave를 통해 공중으로 전파되기 때문에 누군가가 전송을 가로챌 수 있음. 그래서 나온 개념이 WEP이다
- Wired Equivvalent Privacy(WEP)
  - An encryption technology that provides a very low level of privacy
  - WEP was quickly replaced in most places with WPA(WiFi Protected Access)

- WPA(WiFi Protected Access)
  - uses 128 bits key
- WPA2
  - the most commonly used nowadays
  - Uses 256 bits key
    - Make it even harder to crack
- MAC filtering
  - You can figure your access points to only allow for connections from a specific set of MAC addresses belonging to devices you trust

## Celluar Networking (Mobile Networking)

- One of the biggest differences is that these frequencies can travel over longer distances more easily, usually over many kilometers or miles.
- Celluar networks are built around the concept of cells
  - Each cell is assigned a specific frequency band for use. Neighboring cells are set up to use bands that don't overlap.