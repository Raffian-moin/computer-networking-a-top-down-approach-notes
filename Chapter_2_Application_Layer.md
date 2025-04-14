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

### 2.2.2 Non-Persistent and Persistent Connections

In the example from section 2.2.1, we rec
if the subsequent requests for the five images are made over the same TCP connection, it is called a persistent connection. In contrast, if each of the five requests is made over a new, separate TCP connection, it is referred to as a non-persistent connection. HTTP uses persistent TCP connection as default.

#### HTTP with Non-Persistent Connections

description of previous example if 5 images were downloaded how it would do for each connection?
Is the connections are created serially or parallel?
RTT for each request/response

#### HTTP with Persistent Connections


Questions
If a single connection is used how client/server diffrentiate the packet for which request/response is this?
What is HTTP pipelining?

### 2.2.3 HTTP Message Format
We have learned that HTTP communicates via sending and receiving HTTP messages. But what actually is HTTP message looks like?

There are two kinds of HTTP messages - Request and Response message

#### HTTP Request Message
HTTP request with five lines and their description
Image of HTTP format
Entity body is for POST method
HEAD method

Question
What is crlf?
Why Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36 in Chrome although I'm using Chrome?
what is content negotiation headers?


### 2.2.4 User-Server Interaction: Cookies

### 2.2.5 Web Caching


### 2.2.6 HTTP/2

HTTP/2 was standardized in 2015. HTTP/2 offers -

- Resolves the Head of Line (HOL) blocking problem
- Request prioritization and server push
- Efficient compression of HTTP header fields

#### HTTP/2 Framing

If a web page requires 6 resources, the client and server can use a single TCP connection to handle all requests, reducing the number of socket connections on the server. However, if the first response is large (e.g., 100MB) and the remaining five are small (e.g., 100KB each), the small responses must wait for the large one to finish. This delay is known as Head-of-Line (HOL) blocking. To mitigate HOL blocking, browsers open multiple parallel TCP connections, but this increases the number of sockets on the server, which has scalability limits.

HTTP/2 uses a single TCP connection and breaks HTTP messages into frames, allowing multiple requests and responses to be interleaved and sent in a round-robin fashion. Thus solves the HOL blocking. Framing is done by the framing sub-layer of HTTP protocol.

Note: Each TCP connection from a client to the server results in a separate socket on the server.

#### Response Message Prioritization and Server Pushing

When a client makes concurrent requests in HTTP/2, it can assign a weight (1 to 256) to each stream, allowing higher-priority requests to be served first.

If a web page has 5 linked resources, the server can proactively send these responses without waiting for the client to request them—this is called server push.

Questions:

- For priority response wouldn't the remaining suffer from HOL blocking?

## 2.3 Electronic Mail on the Internet

The Internet mail system consists of three major components: the user agent, mail servers, and the Simple Mail Transfer Protocol (SMTP).

- User Agent: This is the application or interface through which users send, receive, and manage their emails. Common examples include email clients such as Microsoft Outlook, Gmail, and Thunderbird.

- Mail Servers: These servers are responsible for storing emails. At least two mail servers are required:
  - The SMTP client, which is typically the server that sends emails to the recipient's mail server.
  - The SMTP server, which is the server that receives and stores emails sent by the SMTP client.

- SMTP (Simple Mail Transfer Protocol): SMTP is an application layer mail delivery protocol used to send emails between mail servers or client user agent to SMTP client.

When User A sends an email to User B, User A's user agent sends the email to the SMTP client, which then forwards it to the SMTP server. User B's user agent pulls the email from the SMTP server. If the SMTP server For SMTP client to send to SMTP server, SMTP server should be active/online, otherwise client would retry later.


### 2.3.1 SMTP
