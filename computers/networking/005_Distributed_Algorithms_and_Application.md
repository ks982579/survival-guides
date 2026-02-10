# 5. Distributed Algorithms and Applications

pp. 93-106;

We will learn the following:
- Understand the concept of communication and synchronization of distributed systems.
- Analyze the concept of transactions and data management.
- Apply the aspects for distributed services and applications.
- Design and implement distributed algorithms.

## Introduction

A **System Call** is a computer programming term requesting a function or system program of an operating system. 

- A distributed system consists of programs installed on various geographical locations, machines, and operating systems, necessitating synchronization across these differences.  
- In contrast to centralized systems, where programs are located on a single machine, distributed systems face challenges due to differing clock readings across machines.  
- Inter-process communication is complex in distributed systems as functions may be spread across different machines.
	- The challenge is because the callee and caller functions of a system call are located on different machines. 
- A key advantage of distributed systems is data replication across multiple storage points, which raises the challenge of **consistency**; updates to data must be reflected in all replicas to ensure uniformity.  
- Processes within a distributed system may share common data, leading to the necessity for distributed algorithms to manage mutual exclusion and prevent simultaneous resource access.  
- The unit discusses critical topics related to distributed systems, including inter-process communication, synchronization, mutual exclusion algorithms, data consistency for distributed transactions, and various security issues.

## 5.1 - Communication and Synchronization in Distributed Systems

p. 94;

In a **centralized system** multiple programs (i.e., processes) are installed on a common system. 
- processes can communicate with each other through shared data and memory.

Unlike the centralized system, programs or processes of a **distributed system** are installed in different systems.
- processes cannot communicate through shared memory.
- communication takes place through exchanging messages between processes.

We will look at some widely used communication models for large-scale distributed systems because their immense size and complexity makes it difficult to implement inter-process communication through a simple message-passing technique. 

We also need to look at various process-synchronization techniques for distributed systems because when resources are shared among multiple processes, they should synchronized in order to protect the resource from unwanted or accidental access.

### 5.2.1 - Inter-Process Communication in Distributed Systems

Two widely known communication models for distributed systems are:
- remote procedure call (RPC)
- message-oriented middleware (MOM)

#### Remote Procedure Call (RPC)

The **Little Endian** is an order where the least significant value is stored in the lowest address space.

The **Big Endian** is an order where the most significant value is stored in the lowest address space. 

- Remote Procedure Call (RPC) allows a process on machine A to call a process on machine B, suspending the caller on A while the called process executes on B.  
- Messages can be exchanged between the caller and called process as function arguments and returns.  
- RPC is interactive, dealing with differences in address spaces, data representation, machine availability, and parameter passing challenges.  
- It operates as a request-response protocol similar to HTTP, where the client sends a request message containing parameters to the server.  
- Key terminologies in RPC include:  
	- **Stub**: Program segment that converts parameters during an RPC call between different machines.  
	- **Client Stub**: Encapsulates the message from the client to the server.  
	- **Server Stub**: Handles incoming messages at the server.  
	- **Marshalling**: The process of packaging parameters in a neutral format for transmission.  
	- **Unmarshalling**: Converts data from a neutralized format back to the machine-specific format.  
- Different byte-ordering conventions (little endian and big endian) necessitate the need for neutral data representation.

The six steps of RPC are as follows (van Steen & Tanenbaum, 2017):
1. The client procedure calls the client stub.
2. The client stub performs marshalling (i.e., encapsulates the parameter to form the
message or packet and calls the client’s operating system (OS) program for message
transmission). 
3. The client’s OS (via link and physical layer) transmits the packet from the client’s
machine to the server’s machine.
4. The server’s OS passes the received packet to the serverstub.
5. The server’s stub performs unmarshalling (i.e., decapsulates the received packet).
6. The server procedure calls the serverstub and repeats the above-mentioned steps in
reverse order to respond to the client.
The RPC protocol is standardized in the Request for Comments (RFC) 5531 (Thurlow,
2009).

#### Message-Oriented Middleware (MOM)

**Middleware** is a software which lies between the OS and application software on both the client side and server side (Etzkorn, 2017).

• Communication in RPC is inherently synchronous, blocking the client process until a server response is received.  
• Modifications to RPC promote asynchronous communication via message-oriented middleware (MOM).  
• Middleware functions as a bridge between the operating system and application software on both client and server sides.  
• It simplifies the deployment of distributed applications, manages hardware and OS heterogeneity, and provides uniform interfaces and common services for building portable and interoperable applications.  
• MOM enables both persistent and nonpersistent communication methods, accommodating both synchronous and asynchronous communication modes.  
• In synchronous communication, the sender waits for a response before sending a second message, while in asynchronous communication, the sender can dispatch subsequent messages without waiting for prior responses.

Processes in a distributed system can be synchronized in two ways:
- using physical clocks
- using logical clocks

#### Physical Clock Synchronization

• Each computer contains a physical clock or timer that oscillates at a frequency determined by the voltage applied.  
• The oscillations are counted as clock ticks, leading to variability in timing known as clock skew.  
• To synchronize clocks in a distributed system, an external global clock is necessary, which provides universal coordinated time (UTC).  
• UTC is maintained by 40 shortwave radio stations and various satellites that broadcast time signals.  
• Distributed systems rely on UTC for synchronization.  
• Several algorithms exist to address synchronization issues, including Network Time Protocol (NTP), Berkeley algorithm, and Reference Broadcast Synchronization (RBS).

#### Network Time Protocol (NTP)

• Network Time Protocol (NTP) is based on a client-server model for clock synchronization.  
• It utilizes a connectionless transport protocol, specifically the User Datagram Protocol (UDP).  
• The synchronization process begins when the client requests a timestamp from the server at time T0.  
• The server's clock is synchronized with Coordinated Universal Time (UTC).  
• The server records the message receive time (T1) and responds with timestamps for T1 and T2 (message transmission time).  
• The client records the time it receives the server's timestamp (T3).  
• Using these timestamps, the client calculates the round trip time and estimates the delay to minimize clock synchronization error.  
• NTP is standardized in multiple RFCs: 5905, 7822, and 8573.

#### Barkeley Algorithm

• The NTP protocol involves a passive server that only responds to client requests.  
• In contrast, the Berkeley algorithm is an active protocol where the time server actively collects time data from clients over a set period.  
• The server utilizes the average time from clients to recommend adjustments in client time settings (speed up or slow down).  
• This protocol is particularly useful when synchronization with UTC is not achieved.

So it can tell when times are getting off-track and instruct servers to adjust. 

#### Reference Broadcast Synchronization (RBS)

• RBS protocol is effective for time synchronization in wireless sensor networks.  
• Similar to the Berkeley algorithm, it involves a sender broadcasting a message.  
• Receivers are assumed to be at a first hop distance from the sender.  
• Receivers compare the time the message is constructed with the time it is delivered to estimate delay.  
• The measured delay includes propagation time and message processing time at the network interface card.

#### Logical Clock Synchronization

- In distributed systems, node agreement on a physical clock is not essential.  
- The key requirement is the synchronization of the order of events across different nodes.  
- This synchronization approach is termed logical clock synchronization.  
- Two prominent protocols for logical clock synchronization:
	- Lamport’s logical clocks
	- vector clocks.

#### Lamport's Logical Clock

**Lamport's** logical clock utilizes the term **happens before**, which is indicated by the arrow symbol $A\to B$, reads "Event A happens before event B". 

The book then talks about logical times being different sizes, like $C(A) < C(B)$. Then another event $C$ happens on another node and it is known to happen after $B$. 

Logical time is always increases, it never decreases. 

If $A \to B$ is true, then $C(B) = C(A) + n$ where $n$ indicates the number of events occurring between $A$ and $B$. 

#### Vector Clocks

Lamport's logical clock does not account for *causality* (what causes an event to occur). 

If a node receives two messages, one before the other, we can say $C(m_1) < C(m_2)$. However, this relationship does not mean the events are related. The messages could have been sent by two different nodes that are independent of each other. 

The **vector clocks** algorithm considers causality, which means the clock time infromation also provides information about the relation between messages. This is done by including some additional information with the clock time value. Information may include:
- process ID number
- node ID number

## Exercise

Write a program to simulate the classic "producer-consumer" concurrency problem. 
- should have 2 threads, 'producer' and 'consumer'. 
- Assume that the producer and consumer share a common buffer. Consider that the buffer size is N . The producer generates data and writes them into the buffer, while the consumer removes data from the buffer. Declare a variable called “counter.” The producer increases the counter value by one once it writes data in the buffer, and the consumer decreases the counter value by one each time it removes a piece of data from the buffer. While the counter value is N , the producer is not allowed to write in the buffer. The consumer is not able to remove a data from the buffer while the counter value is zero. Santiago (2020) provides a Python-based tutorial related to concurrency problems.

## 5.2 - Distributed Algorithms

p. 99;

**Starvation** is a situation where a process unfairly waits for a shared resource while other processes keep progressing.

**DealLock** is a situation where causally related process are forced to wait for each other, meaning that no process can progress. 

• A distributed system relies on concurrency and collaboration among processes on different machines.  
• Non-causally related processes can access shared resources simultaneously, while causally related processes must maintain an execution order.  
• Mutual exclusion is crucial to prevent concurrent access to shared resources among causally related processes (van Steen & Tanenbaum, 2017).  
• Distributed algorithms should ensure mutual exclusion, as well as avoid starvation and deadlock.  
• The dining philosophers problem exemplifies issues of deadlock and concurrency, where philosophers (processes) need forks (resources) to eat but cannot all access them simultaneously.  
• In scenarios where all philosophers attempt to pick up two forks, it's impossible for all to do so at once, leading to potential starvation and deadlock.  
• A proposed solution limits the number of philosophers to four at a time, allowing forks to be picked only if both are available, where odd-numbered philosophers pick their right fork first, then the left (Silberschatz et al., 2013).

Let us look at some commonly used distributed algorithms.

### 5.2.1 - Centralized Algorithm

• A centralized algorithm uses a process as a scheduling **coordinator** for accessing shared resources.  
• Processes must request access from the coordinator; permission is granted if the resource is available.  
• The algorithm is easier to implement and aims to ensure fairness, preventing process starvation.  
• A potential drawback is the single **point of failure**; if the coordinator fails, the entire system is affected.  
• Request **overloading** can occur if too many processes attempt to access resources simultaneously.

### 5.2.2 - Distributed Algorithms

• Distributed algorithms were introduced by Ricart and Agrawala in 1981.  
• A process sends a request message containing its identification, the resource name, and a logical timestamp to all other processes to access a resource.  
• All responding processes send an okay (OK) message if they are not using the resource or their timestamps are greater than the request's timestamp.  
• If a process is utilizing the resource, it queues the request and sends the OK message once it is done.  
• A process with an earlier timestamp than the request does not send an OK message but uses the resource first and responds after.  
• Distributed algorithms eliminate the single point of failure seen in centralized algorithms but still face N point failure risks.  
- However it suffers from N point failure. In N point failure, if any one of N processes fails, it affects the ability of others to receive OK messages, leading to starvation.  
- Also, Excessive processes can lead to a high volume of broadcast messages, decreasing system throughput.

### 5.2.3 - Token Ring Algorithm

• The algorithm involves distributed processes forming a logical ring.  
• Each process is aware of its neighboring process (van Steen et al, 2017).  
• A token is passed from one process (p0) to another (p1, p2) to access a shared resource.  
• The algorithm ensures fairness and prevents starvation among processes.  
- Issues arise if a process becomes out of order; thus, a mechanism to bypass it is needed to maintain the ring.
	- might be node failure.
- Adding a new process necessitates the reforming of the ring.

### 5.2.4 - Decentralized Algorithm

Lin et al. (2004) proposed a fully distributed algorithm where $N$ replicas are created of a resource. 
- A coordinator is assigned for each resource replica. 
- When a process requests to use a resource
	- Then the coordinators vote for the access permission
	- If votes for permission is $m > N/2$ 
		- Then the process is allowed to access the resource. 

## 5.3 - Transactions and Data Management (Consistency ...)

p. 101;

• In a distributed system, a **transaction** involves operating on dispersed data across multiple databases or network nodes.  
• An example includes multiple users or processes collaborating on a common file in the cloud from different machines.  
• Data replication is a significant advantage of distributed transactions, commonly used for backup and enhancing quality of service (QoS).  
• Ensuring consistency is essential for distributed transactions.

### 5.3.1 - Distributed Transaction

Distributed transaction maintains the following properties:
- Location transparency
- replication transparency
- concurrency transparency
- failure transparency

• A distributed transaction has four main properties:  
- **Location Transparency:** Users can access data from multiple locations and nodes.  
- **Replication Transparency:** Data can be updated in one location, automatically replicating the update across all nodes.  
- **Concurrency Transparency:** Multiple transactions can occur simultaneously on the same distributed data.  
- **Failure Transparency:** Ensures that either all transactions on the distributed data are completed or none are, maintaining data consistency.

### 5.3.2 - Distributed Replication

• Distributed replication serves two main purposes: data backup and enhanced service quality through increased throughput.  
• High request volume to a server in a large data center can lead to overload and inability to meet user demands.  
• A common solution is to replicate data to servers closer to users to alleviate server load and minimize latency.  
• Challenges in distributed replication include determining the optimal placement of replica servers and replica content.

#### Placement of replica-server

**Inter-node latency** is the time that elapses while data are transferred between two nodes.

• Placement of replica-server requires suitable geographical location selection.  
• Qiu et al. (2001) suggest calculating the average distance from user nodes to server nodes, choosing the one with the smallest average.  
• They recommend considering bandwidth distance over geographical distance.  
• Radoslavov et al. (2002) focus on the server's service area, assuming uniform user distribution within that region.  
• Szymaniak et al. (2006) propose an algorithm to identify regions with the highest content demand and select the node with the least inter-node latency.

#### Placement of replica-content

• Three types of content replicas are identified: permanent replicas, server-initiated replicas, and client-initiated replicas (van Steen & Tanenbaum, 2017).  
• Permanent replicas are the initial, locally initiated copies and are generally fewer, serving primarily as data storage for content.  
• Server-initiated replicas are created by a server in response to requests from another server, aiming to enhance system performance.  
• Client-initiated replicas are also created by a server but originate from requests made by client processes.

### 5.3.3 - Consistency Management

Push and Pull protocols.

• Once a replica is edited, all other replicas must be updated for consistency.  
• Two types of protocols for updating nodes are push and pull.  
- Push protocols, also known as server-based protocols, automatically forward updates to all other nodes when data changes.  
- Pull protocols, or client-based protocols, only forward update information when requested by a client.  
• Maintaining continuous consistency in distributed systems is crucial but challenging.  
• Three criteria characterize inconsistency:  
- Deviation in numerical values between replicas  
- Deviation in staleness between replicas  
- Deviation in the ordering of updated information.  

Important consistency models are further discussed below.

#### Data-centric consistency

• The data centric consistency model serves as a contract between a server process and a data store, ensuring correct memory performance when processes adhere to rules (van Steen & Tanenbaum, 2017).  
• Sequential consistency, introduced for multi-process systems with shared memory, requires that read and write operations occur in a preferred order as per the program's algorithm (Lamport, 1979).  
• Causal consistency modifies sequential consistency by establishing that events are causally related if one event's occurrence depends on another; it dictates the order of causally related events while allowing concurrent events to differ across machines (van Steen et al., 2017).  
- **Eventual consistency** applies to large-scale distributed systems, where databases converge to a consistent state over time despite long periods without updates; this is part of the BASE model (Fox et al., 1997).  
• The domain name system (DNS) exemplifies eventual consistency, as lower-level databases replicate a top-level database but do not immediately reflect updates until requested, eventually achieving consistency (van Steen & Tanenbaum, 2017).

#### Client-centric consistency

• Client-centric consistency focuses on maintaining local or individual consistency for replicas on distributed nodes, contrasting with data-centric consistency, which ensures global consistency for various users.  
• Popular client-centric consistency protocols include:  
- **Monotonic read consistency:** Guarantees that once a process sees an updated value of data, it will not see an older value (e.g., email databases).  
- **Monotonic write consistency:** Ensures processes apply writes in order across all data copies, reflecting all previous writes by the same process.  
- **Read your writes consistency:** Requires write operations to complete before read operations, regardless of the node that performed the writing.  
- **Writes-follow-reads consistency:** Ensures that if a process writes to a data item after reading it, the write applies to the same or a more recent version of the data, preventing inconsistencies.



## 5.4 - Security Aspects for Distributed Services and App...

p. 104;

• Security of a computer system relies on the confidentiality, integrity, and availability triad (CIA-triad).  
• Ensuring security in distributed systems is more complex than in centralized systems due to their design vulnerabilities.  
• Three major security challenges in distributed systems include:  
- Secure channel  
- Access control  
- Security management  
• These challenges are all dependent on the CIA-triad.

### 5.4.1 - Secure Channel

• Securing the channel ensures authentication of sender and receiver, preventing impersonation by attackers.  
• A secure channel protects messages from unauthorized access, maintaining confidentiality for authorized users only.  
• Integrity is assured as messages cannot be altered by unauthorized entities.  
• Key properties of a secure channel include confidentiality, authentication, and integrity.  
• Confidentiality is established using symmetric-key encryption, with the advanced encryption standard (AES) being the most widely adopted.  
• Asymmetric key encryption is utilized for the secure exchange of symmetric keys, typically involving the RSA algorithm.  
• Sender authenticity is achieved via asymmetric encryption, where the message is encrypted with the sender’s private key.  
• The receiver uses a public key from a trusted authority to decrypt the message.  
• Due to the time-consuming nature of asymmetric encryption, a digital signature process is employed, where the message's hash code is encrypted instead.  
• Data integrity is protected through digital signatures, preventing forgery and verifying content authenticity.

### 5.4.2 - Access Control

• Access control regulates who or what can access resources in a system and enforces usage policies.  
• Authorization, a key aspect of access control, determines permissions for users or processes following user authentication.
- Authorization comes after authentication of the user or process. 
• A common violation of authorization is privilege escalation, where access is gained beyond intended permissions.  
- Methods of implementing access control include:  
	- **Access Control List (ACL):** A database containing names or IDs of authorized users or processes.  
	- **Access Certificates:** Issued by a third-party authority listing rights for various resources, potentially causing delays in revocation.
		- shortcoming is reliance on thrid-party authority to issue certificates.
	- **Firewalls:** They filter user access based on properties like IP address and MAC address, can be set between machines and routers (packet-filtering gateways), or at the application level (proxy-gateways).


### 5.4.3 - Security Management

• Security management involves various activities to safeguard information systems.  
• Key activities include the generation, secure storage, and distribution of cryptographic keys.  
• Asymmetric encryption utilizes public-private key pairs for secure communication, authentication, and digital signatures.  
• Trusted third-party authorities, such as Certificate Authorities (CAs), are essential for managing public keys.  
• CAs verify identities and issue digital certificates to ensure public key authenticity.

### 5.4.4 - Secure Mobile Code

• Securing mobile code is a crucial issue in distributed systems due to the transfer of data and executable code.  
• Malicious code types, including malware, spyware, and ransomware, can be embedded in data, creating security risks.  
• Sandboxing is a widely adopted method to combat malicious code.  
• Every smartphone app operates within a sandbox, which limits access to system resources.  
• The sandbox monitors app activities; it halts the app if malicious behavior is detected, enhancing security by isolating harmful code.


## Summary

p. 106;

• Inter-process communication in distributed systems utilizes remote procedure calls (RPC), which operate on a request-response and synchronous basis.  
• To enable asynchronous communication, message-oriented middleware (MOM) is developed as an intermediary between system and application programs on both client and server sides.  
• Synchronization can be achieved using a global physical clock (universal coordinated time, UTC) or logical clocks, with Lamport's logical clocks and vector clocks being notable protocols.  
• A significant benefit of distributed systems is data replication across various stores; consistency issues arise when changes in one store necessitate updates in others to ensure uniform information for users.  
• Consistency management can be approached from either the server side (data-centric) or the client side (client-centric).  
• Security in distributed systems is ensured through confidentiality, integrity, and availability measures, with access control maintained by access control lists (ACL), access certificates, and firewalls.
