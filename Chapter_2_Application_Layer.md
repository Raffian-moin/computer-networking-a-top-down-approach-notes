# Application Layer

## Introduction

## 2.1 Principles of Network Applications

If we want to develop network applications that can communicate with each other, we need some principles and protocols so that they can understand each other.

### 2.1.1 Network Application Architectures

There are mainly two types of network application architectural paradigms
1. Client-Server architecture
2. Peer-to-Peer architecture

**Client-Server architecture:**
- The host that requests a resource is called the client, while the host that provides the resource is called the server.
- A server can handle multiple client requests simultaneously.
- Each client-server communication involves a single, dedicated connection.
- Direct communication between clients is not possible in a typical client-server model.
- Example: A web browser (client) communicates with a web server (server) to request and receive resources.

**Peer-to-Peer architecture:**
- There is no centralized host that provides the resource; all hosts can act as both clients and servers.
- Each host connected to the network can request and provide resources simultaneously.
- Every host in the network is referred to as a peer.
- Example: file-sharing application BitTorrent


### 2.1.2 Processes Communicating
When we say that two hosts are communicating with each other, what we really mean is that two programs running on those hosts are communicating. More accurately, it's not the programs themselves that communicate, but the processes created by the operating systems to run those programs.

#### Client and Server Processes
- In client-server architecture, the client process (e.g., a browser) communicates with the server process (e.g., a web server).
- In peer-to-peer (P2P) architecture, each peer pair has both a client and a server. The peer that initiates the communication is called the client, while the peer that serves the resource is called the server.

#### The Interface Between the Process and the Computer Network
We learned that remote processes can communicate, but how does this happen? The sending process sends a message to a socket on the sender's side. The sender's transport layer then takes the message and sends it through the network. Once the message reaches the destination, the transport layer on the receiving side passes it to the socket, and finally, the receiving process retrieves the message from the socket.

#### Addressing Processes
We want to send a message from process A1 on host A to process B1 on host B.
- How do we identify the address of the receiving host B?
- Since the receiving host may have multiple processes running simultaneously, how can we ensure the data is correctly sent to process B1?

to answer the first question, we need the IP address of host B to correctly identify the receiving host.
For the second question, we need to know the port number on which process B1 is running on host B, ensuring the data is directed to the correct process.

Questions:
- What is port? Is it a hardware or software thing?
- How do we know the IP address of destination host?
- How do we know the port number of a process running on destination host?

### 2.1.3 Transport Services Available to Applications
As an application developer we can expect some services from the transport layer.

#### Reliable Data Transfer
Messages can get lost in the network or become corrupted during transmission. In either case, we do not want the destination host to process the corrupted or lost message. To handle this, we require the message to be retransmitted by the sender. Transport layer protocols could ensure reliable data transfer by detecting lost or corrupted messages and requesting retransmission from the sender.


#### Throughput

#### Timing

#### Security

### 2.1.4 Transport Services Provided by the Internet

In the previous section, we learned about the services we expect from the transport layer. In this section, we will explore the actual services that the transport layer provides.
There are two types of transport layer protocols: TCP and UDP. The cumulative services offered by both TCP and UDP constitute the actual transport services used in today's internet.

#### TCP Services
TCP provides connection-oriented service and reliable data transfer service

## 2.2 The Web and HTTP

### 2.2.1 Overview of HTTP

The Hypertext Transfer Protocol (HTTP) is an application layer protocol that operates on top of the Transmission Control Protocol (TCP). HTTP allows clients to send request messages to a server, which then responds with HTTP response messages.When a client requests a webpage, the server typically returns the HTML document, which may include references to other resources such as images, JavaScript files, CSS files, and more. Each of these resources has its own URL from which the client can request them.For example, if an HTML page contains five images, the server will first send the HTML file with the URLs (links) to those images. The client will then make separate requests to the server for each image, resulting in five additional requests.

HTTP sends/receives the messages to socket and TCP gets/sends the messages from socket. Before the HTTP request/response cycle begins, a TCP connection must be established between the client and the server. Thanks to TCP's reliability, HTTP can be assured that the data sent from the client will reach the server and vice versa without errors.

HTTP is stateless. This means that each HTTP request is independent of previous ones. For example, if a client requests the same resource multiple times, the server will treat each request as if it is the first time the resource is being requested and will send the resource again.