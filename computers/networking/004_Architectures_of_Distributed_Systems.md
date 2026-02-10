# 4. Architectures of Distributed Systems

pp. 75 - 92;

Study goals - we will learn the following:
- Understand the concept of distribute system architectures, such as client-server architecture and service-oriented architecture.
- Understand the concept of edge computing, cloud computing, and peer-to-peer computing.
- Understand the concept of web- and micro-services.
- Analyze various types of distributed systems.
- Design and implement distributed systems. 

## Introduction

The distributed system has been defined in various ways and from different sources. To put it simply, a **Distributed System** runs multiple programs or processes on multiple nodes to accomplish a common goal or service. 

A **computer network** is a great example of a distributed system, especially the internet. 

Consider the browser, a client application that can run web services. It can send requests, receive web services from another computer, which runs a server process such as Apache HTTP web server. 

The client-server based distributed architecture is most prevalent in the *internet*. 

Another distributed architecture is **peer-to-peer** (P2P). This is where a group of computers use a common application or process to share files. 

It is noted that the advancement and increased complexity of internet services introduced several advanced variants of client-server architectures, such as:
- service-oriented architectures,
- edge computing,
- cloud computing,
- fog computing
- ubiquitous computing,
- and pervasive computing. 

We will look into different types of distributed systems, more specifically:
- client-server architecture
- service-oriented architectures
- edge and cloud computing
- peer-to-peer computing

## 4.1 - Client-Server Architectures

p. 76;

**Client-Server architecture** is most widely used distributed architecture. The terms 'client' and 'server' refer to software programs.
- Client
	- Generally refers to the computer that runs the client program and is the process that requests and receives services.
- Server
	- Generally refers to a computer with powerful processing speed, memory, and storage capacity that runs the server program. 
	- Is the process that provides services to clients. 

The server and client are identified by a pair of identifiers or addresses.
- Computer's address (IP address)
- applications address (port number aka a socket)

The IP identifies a particular computer and the port number identifies a particular process on that computer.

In client-server architecture, the server is *always* active, always listening to receive requests from the client. The client is not always active, but will start the connection by sending the connection request to the server through the socket.

Then we dive into the TCP like sequence of events
- client sends a request to the server
- the server receives the connection request
- the server accepts it by sending an acknowledgment
- connection is established
- the client sends the request for the service or object
	- could be file or data
- the server transfers the requested object to the client
- the server then terminates the connection. 
- the client also ends the connection after receiving the object. 

Widely used client-server architectures are web services, email services, and the domain name system.

Page 77 shows Figure 19, a Client-Server architecture Scenario. 
- Client makes request to interior router
- to gateway routers / maybe I mean border routers
- to the server network and to the server itself. 

### 4.1.1 - Client-Server TCP/IP Layers

p. 77;

**Apache Server** is an open-source HTTP server for modern operating systems, including UNIX and Windows. 

- Client-server architecture utilizes the TCP/IP protocol stack for internet services. 
- Web services operate on this architecture, with browsers as client applications and web servers like Apache as server applications.  
- It supports both connection-oriented (TCP) and connectionless (UDP) transport layer protocols.  
- The network layer can use IPv4 or IPv6 protocols.  
- Transport and network layer protocols are implemented as system programs of the operating system.  
- Software for the link layer is implemented through system programs and drivers, while the hardware component is the **network interface** card (NIC).  
- Some system programs are implemented in the OS that deal with the transport and network layer activities of the client or server.
	- Like what? 
- Some driver programs are implemented in the OS that deals with the software part of the datalink layer of the client or server. 
	- Like what?
- Apache server is an open-source HTTP server compatible with UNIX and Windows.  
- The client or server application programs are situated above the operating system within the architecture.

Page 78 has Figure 20 that shows both the client and server programs are in the User Space of the computer - probably best way to explain it. The Software (like a browser or maybe NGINX) communicates with their underlying operating. The OS contains
- System programs
- OS Kernel
- Driver programs

The drivers communicate with hardware, which is the NIC. The NIC communicates to the physical link, and this is where computers connect. 
### 4.1.2 - Client-Server Interaction

The client-server interaction is implemented through a series of operations:
- Wait-and-listen
	- Server side operation only.
	- Passively listens for requests from a client. 
	- Done by implementing a function or system call called `Listen()` as an example. 
- Connection request
	- Client sends a connection request to the server through system call.
	- The called function takes sockets from cleitn and server as arguments.
		- basically contains IPs of the client and server machines and port numbers of client and server processes. 
		- Server IP identifies the server machine, server port number identifies server process. 
			- HTTP port number is 80
			- HTTPS port is 443
		- DNS protocol retrieves the IP Address of the server based on hostname. 
- Connection Accept
	- Once server is listening to the connection request; it identifies requested application by port number. 
	- If service is available and client socket is valid
		- Then server calls the System Call to accept connection request and notify client. 
- Object request
	- When connection is established between server and client, the desired service (i.e., object file or data) is requested by calling another function such as `RequestObject()`. Object identifier is passed as an argument to the system call. 
	- For a web service, the object identifier is the URL of the target file.
- object send
	- Once object request is received, the server checks the availability of the object.
	- if the object is not available, it send an error message.
	- Else, the server sends the requested object. 
	- This operation is also implemented through a system call, such as `SendObject()`. 
	- Function also return the data size. 
- receive object
	- Object reception at the client side is also done through a system call, such as `ReceiveObject()`. 
	- Method returns the occupied or free buffer space size.
- disconnect
	- Once client receives entire file it may request the next object though `RequestObject()`. 
	- If nothing further is required, it calls `Disconnect()` system call to notify the server it is waiting to end the connection. 
	- It will not disconnect immediately.
		- It waits a period of time before disconnecting.
		- Once the server receives the `Disconnect()` notification it terminates the connection from the server side by calling `Disconnect()`. 

**Connectionless Service** - the connection request and accept operations are absent. Client will also not send the disconnect notification. It just terminates the connection without notifying the server. And the server ends the connection when all the data has been transmitted. 

Figure 21 on page 80 shows Client-Server Interaction for Connection-Oriented Services. It can be handy, it is shown using system calls. 

Figure 22 on page 81 shows the UDP based connectionless service. 

### 4.1.3 - Exercise

Open wireshark and surf the web. Filter by the packets from your computer and the websites you visited. Which packets are responsible for setting up the server-client connection? Investigate messages. 


## 4.2 - Service-Oriented Architectures, Web- and Micro-Services

p. 81;

**Service-Oriented Architecture** (SOA) allows the server to be compatible with various applications developed by different programming languages. 
- Primary goal of SAO
	- provide a structure that allows loosely coupled software components to adapt to existing software with newly developed features while minimizing the expense. 

### 4.2.1 - Benefits of Service-Oriented Architectures (SOA)

- IT technology and the software industry evolve quickly, necessitating flexible software infrastructure for new features.  
- Service-Oriented Architecture (SOA) was developed to address flexibility and low adaptation costs.  
- SOA organizes services in layers, allowing organizations to wrap existing resources as services to integrate new features.  
- This approach avoids complete service redevelopment, enabling quicker adaptation, easier management, and lower implementation costs.  
- Key benefits of SOA include:  
	- Leveraging existing assets  
	- Easier integration of new features  
	- Simplified management  
	- Faster adaptability to new services or technologies  
	- Reuse of existing assets  
	- Reduced implementation cost

### 4.2.2 - Evolution of SOA Standards

- **Distributed computing** standards were established in the 1970s to enhance inter-software communication, notably DCE/RPC (function-oriented) and CORBA (object-oriented) are greate examples.  
	- Inter-software communication is also known as Distributed Computing.
- DCE/RPC is a function-oriented solution.
- COBRA is object-oriented.
- These standards enable **interoperability** among applications across different programming languages and operating systems.  
	- **Interoperability** is a feature that allows communication between applications regardless of the type of programming language or OS. 
- Achieving interoperability is a key objective of distributed architecture, facilitated by collaboration among various vendors.  
- Complexity in these standards and lack of vendor consensus hindered their development and implementation.  
- Microsoft introduced SOAP as a simpler alternative with single-vendor maintenance.  
	- SOAP is the Simple Object Access Protocol. 
- SOAP supports enhancements such as encryption, authentication, security, service management, and transaction management.  
	- Course book kind of says "However..." so requires more research. 
- In a Service-Oriented Architecture (SOA), standards are organized in layers, allowing integration of new features seamlessly.

### 4.2.3 - Web Services

**Heterogenous**, in the software industry, means something is independent of programming language, operating system, or hardware specification and provides loose coupling between consumer and provider. 

- Web services architecture is favored for its distributed nature and ability to support diverse applications over the internet. 
	- Course book says Web Service Architecture can support *heterogenous* applications via the internet. 
- It is independent of programming languages, operating systems, and hardware, emphasizing loose coupling between consumer and provider.  
- The architecture relies on open standards including XML, SOAP, UDDI, and WSDL, promoting interoperability between solutions from different vendors.  
	- eXtensible Markup Language
	- Universal Description, Discovery and Integration (UDDI)
	- Web Services Description Language (WSDL)
- Key characteristics of web services include:  
	- **Self-contained:** Requires only a basic client application (XML or HTTP) and a web server application.  
	- **Self-describing:** Client and server need to understand only the format and content of requests and responses.  
	- **Modular:** Utilizes technologies like J2EE, CORBA, and DCOM for web deployment to ensure compatibility.  
		- To ensure heterogeneity.
	- **Independent and interoperable language:** Client-server applications work/compatible regardless of programming languages.  
	- **Based on open standards:** Supports critical standards such as XML, SOAP, UDDI, and WSDL.  
	- **Composable:** Basic web services can serve as foundations for more complex services.  
	- **Dynamic:** Web services are adaptable to change.

### 4.2.4 - Microservices

- Microservices represent a distributed software architecture that comprises small, independent services, each executing its own process.  
- WireMock serves as a mock server for testing microservices.  
- The term “small” is flexible, allowing for heterogenous processes developed in various programming languages, with distinct data structures.  
- Microservices contrast with monolithic architecture, characterized by large, singular codebases.  
- Monolithic structures have drawbacks, including reduced productivity, slow adaptability to new services, integration challenges, and limited scalability and interoperability.  
- The microservice architecture addresses these shortcomings by promoting greater independence and flexibility in development.


### 4.2.5 - Service Mesh Architectures

- Service mesh functions as an infrastructure layer facilitating service-to-service communication in microservices.  
- Communication occurs via proxies, as described by Khatri & Khatri (2020).  
- Modern applications consist of microservices, each dedicated to specific business functions, allowing for collaborative data sharing.  
- Overloaded service requests from other microservices are managed by the service mesh, routing requests effectively between services.  
- A typical request flow: a user’s request goes to a proxy server, which forwards it to the server if the requested object is unavailable.  
- Once retrieved, subsequent requests for the same object are served directly from the proxy.  
- The service mesh employs sidecars, enabling microservices to operate together while avoiding the need for individual programming for service-to-service communication, as noted by Sharma & Singh (2020).
	- **Sidecars** is a concept where microservices run alongside...

### 4.2.6 - Exercise

Docker is a popular open-source tool for providing services within **virtualized containers**. Docker enables easy development, shipping, and running of software applications. 


## 4.3 - Edge and Cloud Computing

p. 84;

**Cloud** refers to a remote storage or computing platform provided by a third party, which is remotely accessible over the internet. 

- Cloud computing and edge computing are distributed architectures based on client-server models.  
- Cloud computing provides on-demand IT resources via the internet, functioning as a remote storage or computing platform managed by third parties.  
- The cloud comprises database centers that deliver a variety of services remotely, utilizing a centralized yet distributed infrastructure across data centers.  
- Clients benefit from larger storage, rapid computing, and processing capabilities without needing additional hardware or software.  
- Cloud servers typically reside at the network core, with clients positioned at the network edge, which limits real-time data processing due to communication delays.  
- Edge computing addresses this limitation by situating data centers closer to edge devices to facilitate time-sensitive data processing, while less urgent processing occurs in remote clouds.

### 4.3.1 - Properties of Clouds


Cloud and cloud computing are described in various ways across sources. The following are key characteristics of cloud computing systems (Ward & Barker, 2013):
- on-demand: A cloud computing system should be able to provide the recourse of services to an authorized user on an on-demand basis.
- broad access: The cloud should be accessible from multiple locations and multiple platforms, such as desktop PCs, laptops, smartphones, Windows OS, MAC OS, and Android OS.
- resource pooling: The cloud provider should be able to pool resources in a shared manner among customers or consumers of various hardware or software specifications.
- rapid elasticity: The provider should be able to provide scalable services to the consumers based on their demand.
- measured service: The cloud provider should be able to monitor and meter the services or resources provided to each consumer.


### 4.3.2 - Clouds Services

- Cloud computing services are categorized into three primary models:  
	- **Software-as-a-service (SaaS):** Users access cloud-based applications without managing infrastructure; updates and maintenance are handled by the provider. Example: web-based email services.  
	- **Platform-as-a-service (PaaS):** Provides a cloud environment for application development and management without infrastructure management; includes operating systems and databases. Developers can utilize pre-configured environments.  
	- **Infrastructure-as-a-service (IaaS):** Offers fundamental computing resources like virtual machines and storage; allows users to configure their own operating systems and applications, providing flexibility and scalability.
		- allows highest level of flexibility and control.



### 4.3.3 - Types of Clouds


• Clouds are categorized into three types: private, public, and hybrid.  
• A private cloud offers IT resources to a single organization and can be maintained internally or by a third party.  
• A public cloud provides services to multiple organizations, leading to shared resources and heightened security concerns.  
• A hybrid cloud combines features of both private and public clouds, with dedicated resources for one organization alongside shared resources.


### 4.3.4 - Edge Computing

• Edge computing is a distributed computing architecture relevant to technologies like IoT, 5G, and V2V communication.  
• Its primary goal is to reduce latency while enabling mobility and location awareness for real-time applications.  
• End nodes, particularly mobile ones, have limited processing speed, memory, and storage compared to core devices like clouds and data centers.  
• Light computations are handled by end devices while heavy computations are processed in the cloud.  
• Traditional architectures struggle with real-time data processing due to the distance between mobile end devices and core clouds, leading to potential latency issues.  
• Edge computing addresses this by placing data processing closer to the network edge, **reducing latency** for delay-sensitive applications.


#### 4.3.4.1 - Edge Computing Characteristics

• Proximity: Edge computing ensures cloud services are located near end users through smaller, densely deployed data centers.  
• Mobility support and location awareness: Real-time computing for mobile nodes is facilitated by the **Locator ID Separation Protocol** (LISP), which identifies network locators and nodes using IP addresses, MAC addresses, or GPS coordinates.  
• Low latency: Bringing cloud services closer to users reduces physical distance and the number of communication hops, thereby minimizing overall latency and processing delays.  
• Context-awareness: Edge computing utilizes network load, user location, and real-time information to deliver context-aware services, enhancing user satisfaction and quality of service (QoS).  
• Heterogeneity: Edge computing must accommodate diverse software applications, platforms, operating systems, hardware specifications, and infrastructures from various vendors.


#### 4.3.4.2 - Variants of Edge Computing

- Recent research has focused on edge computing, leading to several variants based on infrastructure and services.  
- Key variants include:  
	- **Mobile Edge Computing (MEC)**: Targets mobile endpoints by deploying clouds at cellular network base stations.  
		- MEC is Multi-access Edge Computing - the book says. It's an AKA.
	- **Fog Computing**: Connects to numerous sensors, processing data at co-located devices before forwarding it to the cloud to prevent overload.  
	- **Cloudlet**: A small-scale cloud data center situated between mobile devices and the core cloud, designed to reduce latency for mobile applications.  
- Numerous companies have launched edge computing platforms and products, including Cloudpath, pCloud, ParaDrop, SpanEdge, AWS IoT Greengrass, Azure IoT Edge, and Cloud IoT Edge.  
- Liu et al. (2020) provide a detailed survey of edge computing tools.


## 4.4 - Peer-to-Peer Computing

p. 88;

- In client-server architecture, the server is always active, while the client can choose to be active or inactive.  
	- The client requests objects (such as files or data), which the server provides.  
- **Peer-to-peer** (P2P) architecture does not have a dedicated server; no node or peer is consistently active.  
- Nodes (peers) can connect through multiple nodes without server assistance.  
- Each peer operates a common P2P application, sharing objects or files with the network.  
- Peers can search for objects via an application user interface (API) that displays available objects from other peers.  
- Peers can download objects from any available source.  
- Examples of popular P2P file sharing applications include BitTorrent and µ.  
- P2P architecture is also utilized by VOIP services like Skype.  

Page 88 has figure 23 showing the P2P architecture. 

### 4.4.1 - BitTorrent

- BitTorrent is a peer-to-peer (P2P) protocol used for file distribution.  
- Peers in the network share content, allowing for downloads and uploads among them.  
- Each peer has a "torrent" index that lists other peers and available content; this index starts empty and fills as peers share metadata about the files.  
- The torrent contains metadata, not the complete files.  
- A "tracker" keeps track of all active peers, while the group of these peers is referred to as a "swarm."  
- Files can be shared by multiple peers, known as **seeds**.  
- The tracker provides information about seed locations.  
- Some nodes are only downloaders (**leeches**) and do not share files, leading these nodes to be choked by other peers to encourage uploading.  
- A single tracker can centralize the system, leading to potential overloads or failures.  
- Distributed Hash Tables (DHT) provide a way to decentralize the network using multiple trackers.

### 4.4.2 - P2P vs Client-Server Architecture Performance

Suppose there are $N$ nodes. 

Let the upload capacity of the nodes be $\{ \mu_1, \mu_2, \mu_3, \dots, \mu_{n-1}, \mu_n \}$. 

Let the download capacity of the nodes be $\{ d_1, d_2, \dots, d_{n-1}, d_n \}$. 

Let the minimum download capacity be $d_{min}$. 

Suppose all nodes are required to download a file with the file size $F$. The file can be distributed using client-server architecture or P2P architecture. 

In the case of client-server architecture, files are distributed by the server. Server upload rate is $\mu_s$. Therefore the upload time would be $F/\mu_s$. To distribute the file to $N$ clients it would be uploaded $N$ times. So the total upload time is $NF/\mu_s$. 

Download time of the file by the $i^{th}$ nodes is $F/d_i$. Maximum download time is $F/d_{min}$. File distribution time to all nodes is 

$$
\max{\left\{ NF/\mu_s, F/d_{min} \right\}}
$$

Looking at the case of P2P architecture, we assume that initially the node has the file. hence, a node downloads the file from the server. So the server upload time is $F/\mu_s$. The rest of the nodes have two options: download the file from the server or from the first node. And once the second node downloads the file the rest of the nodes have three options...

Therefore the file distribution time to all nodes in a P2P architecture is 


$$
\max{\left\{ NF/\mu_s, F/d_{min}, F/ \left( \mu_s + \sum_i^n=0 \ \mu_i \right) \right\}}
$$

Page 90 shows Figure 24, plots of the client-server vs P2P for a performance comparison. 

### 4.4.3 - Hybrid Architecture

Client-server and P2P architectures are the most prevalent, but there are also many hybrid architectures that combine both client-server and P2P models. 

An example is **messenger applications**. The messenger server maintains the list of locations of users. Once connected, they exchange information based on P2P architecture. 

## 4.5 - Summary

p. 90;

- Distributed computing is the execution of multiple processes across various platforms and devices to achieve a common goal.  
- The processes can operate on both homogenous and heterogeneous systems.  
- The internet exemplifies distributed computing, featuring two main architectures: client-server and P2P (peer-to-peer).  
- In a client-server architecture, a client requests services from a server, which provides files or data.  
- P2P architecture allows nodes (peers) to communicate directly without a server, utilizing a common application for sharing objects.  
- Basic client-server architectures encapsulate shareable resources as objects.  
- Service-oriented architecture (SOA) enhances client-server models by encapsulating resources as services for improved interoperability.  
- Microservices extend SOA by allowing applications to consist of loosely coupled services.  
- Cloud computing represents another form of client-server architecture, offering various services from a networked cluster of data centers.  
- Edge computing, a variant of cloud computing, places a small-scale cloud at the network edge to enhance QoS for sensitive services and user mobility.
