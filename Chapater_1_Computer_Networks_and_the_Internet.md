## 1.2 The Network Edge
An internet network consists of various interconnected devices such as routers, switches, modems, gateways, smartphones devices, computers, and servers. Devices like routers, switches etc make up the network core and devices like smartphones, computers, and servers make up the network edge (because they sit at the edge of the internet network). Network edge devices are called host or end system.

### 1.2.1 Access Networks


## The Network Core
Routers, Switches, Communication links (Wired and Wireless medium) make up the network core.

### 1.3.1 Packet Switching
When Host A wants to send data to Host B, the data is divided into smaller units called packets. These packets travel through the communication medium, passing through various routers and switches along the way. Each router or switch forwards the packet to the next router or switch based on its routing table. Finally, the packets reach the destination host. The process of guiding packets from the sending host to the receiving host through routers and switches is known as packet switching.

Questions:
- Do all the packets sent by the sending host travel along the same path to reach the destination?
- A packet contains a portion of the original data. Does the sending device's communication link transmit the entire packet at once, or does it send it bit by bit?
- Is it possible for the bits to arrive out of order at the receiving end? What will happen in that case?
- Is it possible for some bits from the packets to be lost? What will happen in that case?
- What is a routing table?

#### Store-and-Forward Transmission