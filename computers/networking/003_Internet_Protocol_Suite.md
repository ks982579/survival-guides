# 3. The Internet Protocol Suite

pp. 57-76

After completing this unit you should know / be able to:
- Describe the history of the internet and the World Wide Web.
- Understand the concepts of the transmission control protocol/internet protocol (TCP/IP) reference model and protocol stack.
- Apply the knowledge of internet protocols and services to analyze data packets. 
- Analyze the security aspects of computer networking and the internet.

## Introduction

The **internet** is the most widely used computer network and the largest computer network in terms of
- the total number of connected devices,
- number of users
- spatial area
- organizational scope.

The term *Inter-Net* refers to "Inter Network", which is meant to represent that it is a network of many interconnected networks. 

It comprises mostly all types of networks regardless of spatial (i.e. WAN, MAN, LAN, PAN) and organizational scopes (i.e. intranet, extranet), network topologies, and network devices. 

It also provides all types of network services:
- World Wide Web (WWW)
- Email
- File sharing
- Audio and video streaming

The internet uses the transmission control protocol/internet protocol (TCP/IP) suites to establish and maintain communication between connected devices/nodes.
- Compared to the Open System Interconnected model from the International Organization for Standardization (OSI/ISO)

## 3.1 - History of the Internet and the World Wide Web

p. 58

The idea of the internet originated in the early 1960s with the invention of the **packet switching network**. 

The protocol standard TCP/IP was introduced in the 1980s. The proliferation of modern internet started after the invention of the WWW in the 1990s.

### 3.1.1 1960-1970: Development of Packet Switching (ARPANET)

Before the internet, telegraph and telephone networks were considered cutting-edge technology for communications. 
- Telegraph = textual messages.
- Telephone = audio communication.

Both of these technologies were based on circuit switching technology and used to exchange data at a constant rate. 

**Circuit Switching** technology is stuff when the communicating nodes are connected through dedicated links. 
- [Circuit Switching | Wiki](https://en.wikipedia.org/wiki/Circuit_switching) - two network nodes establish a dedicated communications channel (circuit) through the network before the nodes may communicate. 
	- Circuit *guarantees* full bandwidth of the channel and remains connected for the duration of the communication session. 
	- Circuit functions as if the nodes were physically connected as with an electrical circuit. 

In 1961 the Massachusetts Institute of Technology (MIT) developed the idea of **packet switching**, a network where there is no dedicated path between sender and receiver. Packets from the same source can take different paths to reach the destination. This allows for data transmission with variable bit rates. 

In 1964, the Rand Institute implemented packet switching for military networks to ensure secured audio transmission. 

In 1965, the British National Physical Laboratory (NPL) introduced the idea of the "packet". The invention of the packet and packet switching initialized the founding of the internet. 

First packet switched network was implemented in 1967 by the Advanced Research Projects Agency (ARPA), of the United States Department of Defense. It was used to create a small computer network called ARPANET - Advanced Research Projects Agency Network. 
- Idea was to connect computers from different manufacturers to a specialized computer called the **Interface Message Processor** (IMP).
- In 1969 - ARPANET connected four nodes via IMP located at 4 universities
	- University of California, Los Angeles
	- University of California, Santa Barbara
	- Stanford Research Institute
	- University of Utah

### 3.1.2 1970-1980: Development of TCP (ALOHANet, PRNET, and SATNET)

Timeline:
- 1972
	- ARPNET was able to connect 15 nodes
		- First protocol used to communicate between end nodes is called **Network Control Protocol** (NCP). 
		- Initial ARPANET was a single network.
- Later 1972
	- ARPANET initiated the internetting project to connect nodes from different networks with different properties
		- Such as variant transmission rates or packet sizes.
	- Introduced idea of a *gateway*.
		- a device used to connect two different networks.
- 1973
	- Same research group introduced idea of transmission control protocol (TCP)
		- [Transmission Control Protocol | Wiki](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)

Other packet switching networks were introduced in mid-1970s:
- Microwave-based ALOHANet
	- developed by University of Hawaii
- Packet Radio Network (PRNET)
	- from the Defense Advanced Research Projects Agency (DARPA)
- The Atlantic Packet Satellite Network (SATNET)
	- From BBN Technologies and the Advanced Research Projects Agency

### 3.1.3 1980-1990: Growth of TCP/IP (BITNET, CSNET, MILNET, NSFNET, and ANSNET)

After development of other technologies beyond ARPANET, TCP was divided into two parts:
- Transmission Control Protocol (TCP)
- Internet Protocol (IP)

The combination of TCP and IP was named the TCP/IP protocol stack. 

Purposes:
- IP = to deal with packet routing;
- TCP = to deal with other higher-level services
	- e.g. packet structuring, data segmentation and reassembling, and error detection.

- 1981
	- University of California Berkeley included TCP/IP with a UNIX operating system. 
	- The National Science Foundation (NSF) developed the computer science network (CSNET) to connect universities that had no access to ARPANET.
		- No access to ARPANET was due to lack of collaboration with the U.S. Department of Defense (DoD).
	- The **"Because It's There Network"**, aka "Because It's Time Network" (BITNET), also developed in this year, by Ira Fuchs.
		- Goal to provide email and file sharing services to universities. 
- 1983
	- The military network (MILNET) was developed for military services.
		- ARPANET was left for non-military usage. 
	- TCP/IP replaced NCP as the official protocol for ARPANET.
- 1986
	- NSF developed NSFNET to connect the supercomputer centers with a 1.5Mbps transmission rate. 
- 1990
	- ARPANET was abolished!
	- NSFNET was adopted. 
	- NSFNET was replaced by the Advanced Network Services Network (ANSNet) due to excessive traffic demand. 
		- It was product of a nonprofit organization called the Advanced Network Service (ANS)
			- Formed by 3-companies:
				- IBM
				- Merit
				- Verizon

### 3.1.4 The 1990s: Development of the World Wide Web

p. 60;

1990s was the massive development in internet applications and services. The invention of the World Wide Web played a key role. 

WWW was invented by the European Organization for Neuclear Research (CERN) between 1989 and 1991. 

CERN developed four fundamental elements of the WWW:
- hypertext markup language (HTML)
- hypertext transmission protocol (HTTP)
- the web browser
- the web server

And by 1993 there were around 200 web servers across the world!

### 3.1.5 Who Controls the Internet? Standards and Administrations

No single authority owns or rules the internet. However, various groups and organizations maintain and regulate the Internet's infrastructure, standards, protocols, and other aspects. 

Some organizations:
- The Internet Society (ISOC)
- The Internet Architecture Board (IAB)
- The Internet Engineering Task Force (IETF)
	- managed by the Internet Engineering Steering Group (IESG)
- The Internet Research Task Force (IRTF)
	- Managed by the Internet Research Steering Group (IRSG)
- The Internet Assigned Numbers Authority (IANA)
	- Managed by Public Technical Identifiers (PTI)
		- Affiliated with Internet Corporation for Assigned Names and Numbers (ICANN)


## 3.2 - TCP/IP Reference Model and Protocol Stack

p. 60;

The transmission control protocol/internet protocol, aka 
- TCP/IP protocol stack
- TCP/IP protocol suite
- TCP/IP

This protocol suite is a set of standardized protocols arranged in hierarchical layers. Each layer below supports the one above. And each protocol is compatible with its corresponding upper and lower layer protocols. 

TCP/IP is the standard protocol suite for the internet. Traditionally it is divided into 4 layers:
- application
- transport
- internet
- link layer

Modern internet protocols divide into 5 layers:
- application
- transport
- internet or network
- link or data link
- physical layers

The data unit transferred is called something different at each layer. 

p. 61 shows figure 17 with comparison of TCP/IP and OSI layers.

- TCP/IP Layer: Application
	- TCP/IP Data Unit: Message
	- OSI Layers
		- Application Layer
			- Data Unit: Message
		- Presentation Layer
			- Data Unit: PPDU
		- Session Layer
			- Data Unit: SPDU
- TCP/IP Layer: Transport
	- TCP/IP Data Unit: Segment
	- Addresses: Port No.
	- OSI Layers
		- Transport Layer
			- Data Unit: Segment
- TCP/IP Layer: Network
	- TCP/IP Data Unit: Packet
	- Addresses: IP
	- OSI Layers
		- Network Layer
			- Data Unit: Packet
- TCP/IP Layer: Interface
	- TCP/IP Data Unit: Frame and then Bits
	- Addresses: MAC
	- OSI Layers
		- Data Link Layer
			- Data Unit: Frame
		- Physical Layer
			- Data Unit: Bits

### 3.2.1 TCP/IP Layers

Unlike the OSI model, TCP/IP does not include *presentation* and *session* layers. The services of these two layers are merged into the application and transport layers. Descriptions of each layer of TCP/IP protocol suite are given below. We view on a top-down approach.

#### 3.2.1.1 Application Layer

The **Application Layer** is the top tier of the TCP/IP protocol suite. Layer is responsible for process-to-process communication. 

The layer establishes logical connections between the application programs, or processes, installed on sender receiver nodes. Examples being: browsers, email managers, and messengers. 

The application layer is only available on end nodes. It is not on connecting nodes like routers, switches, bridges, and hubs. 

Data transmitted and received at the application layer is called a **message**. 

Frequently used application layer protocols are:
- hypertext transfer protocol (HTTP) for web applications
- simple mail transfer protocol (SMTP) for email forwarding
- Email access protocols
	- post office protocol (POP)
		- connects to service and downloads messages
		- they are removed from email service once delivered
	- internet message access protocol (IMAP)
		- read emails from email service
		- can check from different devices
- domain name system (DNS) for finding network layer addresses
- file transfer protocol (FTP) for sharing files
- simple network management protocol (SNMP) for managing networks
- TELNET for remote access
- Secure Shell (SSH) for secured remote access

#### 3.2.1.2 Transport Layer

The **Transport** layer maintains logical connections between end-to-end system processes. This also is not available on connecting node (e.g. routers).

On a Sender's side, the transport layer receives the message from the application layer and breaks it into smaller pieces. It encapsulates the pieces with the transport layer header bits. These encapsulated pieces are called **segments**.

A **segment** is the transferred data unit in the transport layer.

The header bits contain the transport layer addresses of the source and destination:
- Source and destination port numbers.

The purpose of the **port number** is to identify the desired application program on a device. 

The main service of a transport layer protocol is reliable packet delivery. This is accomplished through multiple services such as:
- error detection
- in-order packet delivery
- packet loss detection and retransmission
- or congestion detection and congestion control. 

Two of the most important transport layer protocols are the transmission control protocol (TCP) and user datagram protocol (UDP).
- TCP
	- Used for services that require reliable data transfer
		- e.g. email or file transfer
- UDP
	- used for services that do not guarantee reliable data transfer
		- e.g. video streaming or real-time services

**Stream control transmission protocol** (SCTP) is a transport layer protocol that is aimed at multimedia services.

#### 3.2.1.3 Network Layer

The **Internet Layer**, or **Network Layer**, is responsible for maintaining communication between system programs between sender and receiver. 

The network layer encapsulates *segments* with network layer header bits and forms them into **datagrams**, also simply known as **packets**. The **packet** is the transferred data unit at the network layer level. 

A network layer address is called an **internet protocol** (IP) address. 

The purpose of the IP address is to identify a device, as its highest layer is the network layer. 

The two main services of the network layer protocols are:
- packet forwarding
- routing

The IP (internet protocol) is the main protocol for this layer and is responsible for packet formatting and routing. 

#### 3.2.1.4 Link Layer

The **Link Layer** is also known as the **interface layer** or **data link layer**. 

On the sender's side, the data link layer protocols receive network layer packets and encapsulate with link layer header bits to form a **frame**. 

A **Frame** is the name of the transferred data unit at the link layer. 

The data link layer maintains a logical connection between the network interface cards (NICs) of sender and receiver nodes. 

A **Network Interface Card** (NIC) is a hardware device, or circuit, that connects a node to the network or the internet.
- [What is a Network Interface Card (NIC)? | TechTarget.com](https://www.techtarget.com/searchnetworking/definition/network-interface-card)
	- The term is interchangeable with others such as
		- network interface controller
		- network adapter
		- local area network adapter
	- Provides dedicated point of connectivity to a network.
	- Shows the OSI model - the NIC has a physical layer circuit.
	- There are many kinds of NICs
	- Components of a NIC include
		- Controller (like CPU)
		- Driver
		- Bus interface
		- Router
		- etc...
	- Each NIC has a unique and immutable MAC address.

Nodes can connect to a network in many ways, e.g.:
- Wi-Fi
- twisted pair cable-based ethernet
- optical fiber
- satellite radio link
- cellular radio link

If a node is connected in multiple ways, each type of link requires a separate NIC. 

Services provided by link layer protocols include:
- frame formation
- error detection
- media access control
- flow control

Some important link layer protocols are:
- ethernet
- IEEE 802
- point-to-point protocol (PPP)

#### 3.2.2 Exercise

Download open sample captured packets with Wireshark's website. Investigate the transferred data unit at each protocol layer. Find:
- packet sequence number
- number of layers
- header bit lengths
- addresses at different layers

What information can you extract from different layers. 

## 3.3 - Examples of Internet Protocols and Services

p. 63

The TCP/IP protocol stack is a collection of protocols for the internet. They are divided into layers - common ones are shown below.

### 3.3.1 Application Layer Protocols

#### 3.3.1.1 Hypertext Transfer Protocol (HTTP)

p. 63;

**HTTP** defines how a client-server program will be coded to retrieve web-based objects from a server. 

Transfer of an object from server to client is done through request and response messages, defined by HTTP. 
- HTTP operates over port no. 80
- HTTPS operates over port no. 443

The client sends a request message to the server, containing:
- port no. 80
- uniform resource locator (URL) or web address of desired object
	- e.g. HTML file, text or document file, image, audio, or video.

The server replies with the response message that contains the requests object. 

HTTP connection can be either Persistent or NonPersistent.

#### 3.3.1.2 File Transfer Protocol (FTP)

FTP is used to transmit files from server to client. It is a better solution to transfer larger files compared to HTTP. 

Additionally, two systems may have different file naming convention, different directory system, different ways of formatting data. These are all issues FTP considers.
- Operates on TCP port number 21

#### 3.3.1.3 Simple Mail Transfer Protocol (SMTP)

SMTP is used to forward emails from a client to an email server, or from one email server to another. 
- Operates on TCP port no. 25

#### 3.3.1.4 Post Office Protocol Protocol (POP3)

POP3 is used to retrieve email to receiver's computer or system from the email server. 
- First - client establishes a TCP connection on port 110.
- Second - they send the username and password for authentication.
- Third - If passed authentication, the client should be able to see the received email list

POP3 allows the client to keep or delete an email after retrieving it. 

#### 3.3.1.5 Internet Message Access Protocol version 4 (IMAP4)

IMAP4 is also used for retrieving email from the server.

Unlike POP3, IMAP4 allows users to organize emails in directories or folders. 
- Uses port 143 or 993 for secured TCP connection.

I think I mentioned above, but IMAP allows users to access emails on the server, and POP downloads them from the server. 

#### 3.3.1.6 Domain Name System (DNS)

DNS protocol is used to retrieve IP addresses from the `hostname`. 

DNS maintains a distributed database through a hierarchy of DBS servers. DNS operates the user datagram protocol (UDP), port no. 53. 

Generally, DNS is used by application layer protocols, such as HTTP and SMTP, to translate hostname to an IP address. 

#### 3.3.1.7 Simple Network Management Protocol (SNMP)

SNMP is an application layer protocol to manage and monitor networks and devices. The protocol is employed on several servers, called **manager stations**, to control and monitor other devices, known as **agents**.

SNMP accomplishes tasks through two subprotocols:
- Structure of management information (SMI)
- Management information base (MIB)

### 3.3.2 Transport Layer Protocols

p. 64;

No introduction - right into the protocols.

#### 3.3.2.1 Transmission Control Protocol (TCP)

TCP is used for reliable data transfer. This means TCP provides the following services:
- Error detection
	- Done through internet checksum
- Ordered delivery
	- TCP uses a buffer on the receiver side to ensure packet order and delivery.
- Flow control
	- Done by keeping transmission window lower than the free buffer space in the receiver's system. 
- Congestion detection and control
- Packet loss detection
	- The receiver sends acknowledgement each time a packet is received. 
	- The sender uses a timer to track delayed acknowledgment
		- Sender will consider a packet lost of acknowledgment exceeds timeout. 
- Retransmission if a packet is lost

There are several variants of TCP used to handle network congestion. 2 common TCP variants:
- TCP Tahoe
- TCP Reno

Note: TCP ensures ordered delivery and retransmission due to lost packets. This causes undesired delays for real-time services (e.g. video streaming). 
#### 3.3.2.2 User Datagram Protocol (UDP)

UDP is a transmport layer protocol designed for real-time services or services where the bit rate is guaranteed. UDP is a connectionless protocol, which means the receiver does not acknowledge packet delivery. 

Also, UDP does not provide the following services:
- flow control
- packet loss detection
- retransmission
- congestion control services

UDP does provide error detection using a checksum mechanism. 

#### 3.3.2.3 Real-time transport protocol (RTP) and Stream Control Transmission protocol (SCTP)

RTP and SCTP are two types of transport layer protocols used for real-time multi-media services. 

They are both transport layer protocols but the RTP and SCTP datagrams are encapsulated by UDP header bits.

Unlike applications, payload RTP does not have any specific port number. 
- RTP port number is chosen arbitrarily - but always an even number;
- SCTP like RTP but uses odd numbers;

RTP supports only one data type. SCTP support multiple data types. 

### 3.3.3 Network Layer Protocols

p. 65;

#### 3.3.3.1 Internet Protocol (IP)

The **Internet Protocol** (IP) is the network layer protocol of TCP/IP protocol suite. 

There are 2 major versions of IP:
- IPv4
	- uses 32-bit network layer address
- IPv6
	- uses 128-bit network layer address

IPv6 is gradually replacing IPv4. But it will take time and the majority of devices still run on IPv4. 

The TCP/IP network layer provides few supplementary protocols such as the:
- internet control message protocol (ICMP)
- internet group management protocol (IGMP)
	- supports core network-layer functions like:
		- error reporting
		- diagnostics
		- multicast group management.
- dynamic host configuration protocol (DHCP)
- Address Resolution Protocol (ARP)

When a new device joins a network it does not initially posses an IP address. IP addresses can be setup manually or automatically. 
- DHCP is the protocol to setup an IP address automatically to a new device to a network. 
	- 1.) New device, or client, broadcasts a message called the **discovery message**.
		- Source IP address set to: `0.0.0.0:68`
		- Source IP address set to: `255.255.255.255:67`
	- 2.) DHCP server replies with an **offer message** that includes an IP address for the client.
		- DHCP is an application-layer protocol because it provides IP configuration services via client-server messaging over UDP.
			- Sometimes DHCP is associated with the network layer due to its role in assigning IP addresses - directly supports network connectivity.

ARP works below the IP protocol. 
- ARP Purpose is to translate network layer address to the link layer address.
	- This requires retrieval of MAC address of a device based on its IP address. 

The sender broadcasts the destination's IP address (which all nodes receive). However, only the destination node matches the IP address and returns the MAC address to the sender. All other nodes just discard the message. 

ARP is mainly associated with the link layer because it uses link-layer frames and MAC addresses. 
- Newer sources associate it with the network layer due to its role in IP address resolution.
- Kind of creates some intermediate layer, 2.5...

#### 3.3.3.2 ICMP & IGMP

The **Internet Control Message Protocol** (ICMP) is implemented in network layers of routers to exchange control information. 
- ICMP uses IP headers
	- The datagram does not carry a payload from the transport layer.
	- The IP header encapsulates the control message.
	- First octet of the header is called **field**.
	- Second octet is called **code**. 
	- Combination of field and code number indicates a specific **control message** or **error notification**.
		- field = 3 and code = 1 ~ indicates the host is unreachable.
		- field = 3 and code = 3 ~ indicates the port is unreachable.
	- ICMP protocol is standardized in RFC 792 and 6918.

ICMP is an integral part of IP and provides error reports about datagram processing. 

ICMP is defined in RFC 792, 777, 760.

The **Internet Group Management Protocol** (IGMP) provides group membership reporting for multi-casting services. The IP host uses this protocol to report the immediate multi-cast router about multi-cast group membership. It is also part of the IP protocol. 

IGMPv2 is an updated version that is typically used and defined in RFC 2236, 3376.
#### 3.3.3.3 Interior Gateway Protocols (IGPs)

Each internet service provider (ISP) can be considered a domain or autonomous system (AS). 

The routing protocol that operates inside a domain is called **intradomain routing protocol**, or **interior routing protocol**. Examples are:
- Routing Information Protocol (RIP)
- Open Shortest Path First (OSPF)

Different doamins may have different IGPs. 
- RIP is based on distance vector routing algorithm
- OSPF is based on link-state routing algorithm.

IGP is defined in RFC 3906.

#### 3.3.3.4 Exterior Gateway Protocol (EGP)

An EGP is used to perform interdomain routing to find a path between nodes residing in different domains or ISPs.

EGP is defined in RFC 827, 904.

#### 3.3.3.5 Protocol Independent Multicase (PIM)

PIM is a "one-to-many" and "many-to-many" multi-cast protocol. Key characteristics include:
- Ability to create the routing table based on the information or routing table provided by the unicast protocols, such as distance vector or link state protocols.

PIM is defined in RFC 7761, 8736.

### 3.3.4 Link Layer Protocols

p. 65;

#### 3.3.4.1 Reverse Address Resolution Protocol (RARP)

Consider the Address Resolution Protocol. An unknown MAC address is searched for based on a known IP address. In the **Reverse Address Resolution Protocol** (RARP) an unknown IP address is searched for based on a known MAC address. 

RARP is defined in RFC 903. And updated version of RARP called **Dynamic RARP** (DRARP) is defined in RFC 1931.

#### 3.3.4.2 - Neighbor Discovery Protocol (NDP)

The **Neighbor Discovery Protocol** (NDP) is a link layer protocol of TCP/IP protocol suite that utilizes IPv6. NDP is used to gather network information such as:
- discovering the presence of nodes
- finding routers
- finding reachability information of the routes to the neighbor nodes.

NDP is defined in RFC 4861, 5942, 6980, 7048, 7527, 7559, 8028, 8319, 8425.

### 3.3.5 Exercise

p. 67;

Download and open sample captured packets (.pcap or .cap files) for HTTP, SMTP, DNS, TCP, UDP, SCTP, DHCP, and ARP protocols from Wireshark. 

Investigate the packets for each protocol. Find types of messages exchanged for each protocol between sending and receiving nodes, and find the addresses and contents of each message. 

[SampleCaptures | WireShark](https://wiki.wireshark.org/samplecaptures#sample-captures).

Looks like for HTTP we have:
- Ethernet II - header
	- IPv6 - header - has source and destination IP addresses
		- TCP - header - Source and Destination Ports and flags, checksum, acknowledgments, etc
			- HTTP
				- Header = GET, Host, Accept, Accept-Encoding, Accept-Language, User-Agent
				- Body = After TCP is connected the body has the HTML
			- Then TCP Sends FIN, ACK, and couple more ACKs, and another FIN, ACK

Looking at SMTP:
- DNS at the top
- TCP follows
- Then SMTP
- Ethernet II
	- Header = Type IPv4; source and destination looks like hardware addresses
	- Body: IPv4
		- Header = source and destination IP addresses, total length, protocol being TCP, checksum, etc...
		- Body: TCP
			- header = source and destination ports (1470, 25); segment length, sequence number, Flags, etc...
			- Body: SMTP
				- Header: from, to, subject, date, message id, content-type, etc...
				- Body: Honestly, it all might just be body... but a few parts say "NextPart" so maybe that is when it's pieced together. 
					- There is a "Reassembled in Frame 45" message. It's protocol is SMTP/IMF and has everything all here. 
				- Internet Message Format - Once all assembled, SMTP says "18 DATA fragments" and the message is assembled in frame 45. 

## 3.4 - Security Aspects of Communication on the Internet

p. 67;

Our modern world depends on the internet but also various aspects of life are made vulnerable due to security issues of the internet. Ensuring secure communication is crucial!

From Cyber Security, securing communication means ensuring confidentiality, integrity, and availability of information. This is referred to as the CIA Triad. 
- Confidentiality - refers to preventing disclosure of data or information to unauthorized users.
- Integrity - refers to preventing unauthorized users from editing or corrupting data.
- Availability - implies authorized users should be able to access resources on demand. Unauthorized users should not be able to access the resources. 

The key component of internet security is **cryptography**. There are 2 broad categories of cryptography:
- Symmetric
- Asymmetric
	- AKA **public key** cryptography

These broad categories have many techniques to implement these types and we will focus on the most contemporary and widely used cryptography techniques. 

A cryptography scheme is made up of an encryption and decryption algorithm. Each algorithm takes in 2 inputs and produces an output. The two inputs for encryption algorithms are:
- plaintext or message ($m$)
- a key ($k_e$)

The output is called **ciphertext**, or **encrypted text**, and is described as:

$$
c = k_e(m)
$$

Inputs for a decryption algorithm are:
- Ciphertext ($c$)
- a key ($k_d$)

The output is the decrypted text

$$
d = k_d(c) = k_d(k_e(m))
$$

This just means that if the encrypted text is decrypted correctly, then the resulting decrypted test will be equal to the initial plaintext. 

Figure 18 on page 68 illustrates the idea of the cryptography technique. One thing to note is we have symmetric encryption if $k_e = k_d$. 

### 3.4.1 Symmetric Key Cryptography


Again, we have symmetric encryption if $k_e = k_d = k$, both encryption and decryption algorithms use the same key. Simplest example is **Caesar Cipher Cryptography** (CCC).

Discussing this simple algorithm, the key ranges from 0 to 25, (i.e. $k \in 0,1,2, \dots, 25$). We replace a letter $\alpha$ with $(\alpha + k)^{th}$ from the alphabet. Decrypting is $d=(\alpha - k)$. 

CCC is a primitive example because it is too easy to *crack*. 

Many other symmetric key cryptography algorithms are also easy to decode, or crack, with modern day computers. The **Advanced Encryption Standard** (AES) is the most frequent used symmetric key algorithm. **Data Encryption Standard** (DES) is another popular algorithm, but can be cracked with a powerful computer. There's 3DES, a newer version, that is stronger.

The aforementioned algorithms are called **Block Ciphers** because each of these techniques break the plaintext into fixed size blocks before performing encyrption on each block. Each uses multiple steps called *rounds* to accomplish encryption, decryption, and generate a key. 

One limitation of symmetric key encryption is if a bad actor obtains the key then they can decipher all ciphertext. This means the key must be shared between sender and receiver securely. This is usually done via asymmetric key encryption or public key encryption. 

Table on page 69 covers some differences between AES, DES, and 3DES. 

### 3.4.2 Asymmetric Key or Public Key Cryptography

p. 69;

In **Asymmetric Key Cryptography**, the following is true

$$
k_e \ne k_d
$$

That is, the encryption algorithm requires a different key from the decryption algorithm. The encryption algorithm in total requires a pair of keys. We have names for them:
- The sender's **public key** ($k_zp_u$)
- The sender's **private key** ($k_sp_r$)

The decryption algorithm also requires two keys:
- The receivers's **public key** ($k_rp_u$)
- The receivers's **private key** ($k_rp_r$)

Public keys can be shared and known by any user. However, a private key must only be known by the owner of the key. 

Ciphertext is found by encrypting the plaintext ($m$) with the receiver's public key ($k_rp_u$), hence:

$$
c = k_rP_u(m)
$$

And decryption is done using the receiver's private key, hence

$$
\begin{align}
d &= k_rP_r(c) \\
&= k_rP_r(k_rP_u(m)) \\
&= m
\end{align}
$$

The Rivest-Shamir-Adleman (RSA) algorithm is the most popular asymmetric key cryptography algorithm, first described in 1978. Other popular algorithms are: Elliptic Curve algroithm; Diffie-Hellman algorithm.

#### 3.4.2.1 The RSA Algorithm

The RSA algorithm has the following three stages:
1. Key generation:
	- Algorithm chooses 2-prime numbers $p$ and $q$ such that $p \ne q$. 
	- Calculate $n = pq$
	- Calculate $\varphi(n) = (p-1)(q-1)$
	- Select integer $e$, given $\varphi(n)$ and $e$ are *coprime* such that $1 < e < \varphi(n)$.
		- Coprime means that of two or more numbers in relation to each other having no common integral factor except unity... they are relatively prime, or mutually prime, if the only positive integer that is a divisor of both of them is 1. 
	- Calculated $d = e^{-1}(\bmod(\varphi(n)))$ 
	- Public key $k_{pu} = {e,n}$
	- Private key $k_{pr} = {d,n}$
2. Encryption: ciphertext is calculated as $c = m^e\bmod(n)$ 
3. Decryption: decrypted text is calculated by $d = c^d \bmod(n)$

The book transforms the letter A as an example. 

#### 3.4.2.2 - Authentication using Public Key Cryptography

Another use case for public key cryptography is user authentication. Because the private keys should only belong to one owner, it can be used to ensure messages were sent by a specific user. The process is as follows:
- Encrypt the message $m$ with the private key of the sender ($k_sp_r$) and attaching the encrypted text. 
- The receiver decrypts with the sender's public key ($k_sp_u$)

Only the sender has the public key so messages can only be decrypted correctly if sent by the authenticated user. 

Encrypting an entire message can be time-consuming. A faster solution is to apply a hash function.

#### 3.4.2.3 - Hash Function

A **hash function** produces a fixed length output irrespective of the input length. That is, a 128-bit hash function produces a 128-bit output for a given input, regardless of input length. The output will vary depending on inputs, but the length of the output remains constant. 

A good hash function has the following properties:
- For message $m$, an $n$-bit hash function will produce the output $h(m)$ of $n$-bit length.
- It should be computationally infeasible to find the inverse of the hash function $h^{-1}(h(m)) = m$.
	- This property is called **preimage resistance**.
- It should be computationally infeasible to produce a message $m'$ for which $h(m') = h(m)$.
	- This property is called **second preimage resistance**.

Frequently used hash algorithms:
- **Message Digest 5** (MD5)
- **Secure hash algorithm-1** (SHA-1)
- SHA-2

#### 3.4.2.3 - Digital Signature

Sometimes a receiver will need to ensure the received message is from the authentic user AND the received message has not been edited or corrupted. See the Blockchain Course - the course is the example...

We can use digital signatures for this. A **Digital Signature** has two purposes:
- Ensure authentication and integrity

How to create a digital signature?
- First, calculate the hash value of the message $hm$.
- Second, Encrypt the hashed message with the sender's private key. This produces a digital dignature.
	- $s = k_sp_r(h(m))$
- The message $m$ is encrypted with the receiver's public key to obtain the ciphertext for confidentiality.
	- $c = k_rp_u(m))$
- The signature is then attached, or merged, with the ciphertext and sent to the receiver. 
- The receiver then uses the sender's public key to decrypt the received hash value.
	- $k_sp_u(k_sp_r(h(m)))$
- The receiver uses their private key to decrypt the received message
	- $d = k_rp_r(k_rp_u(m))$
- The receiver calculates the hash value of the decrypted message
	- $h(d) = h(k_rp_r(k_rp_u(m)))$
- If hash values are equal then the sender is authenticated and the integrity is preserved. 

### 3.4.3 - Securing TCP/IP Layers

TCP/IP protocol stack does not include a security layer. However, an additional security layer is included with TCP/IP, and various security protocols are used at each layer to ensure security. 

Some of the most commonly used protocols for various layers are discussed below.

#### 3.4.3.1 - Application layer security

There are many security protocols at the application layer designed to secure various applications:
- Hypertext Transfer Protocol Secure (HTTPS)
	- HTTPS supports an encryption mechanism to protect data from eavesdropping and man-in-the-middle attacks. 
	- HTTPS works on the secure sockets layer/transport layer security (SSL/TLS). 
	- Uses port 443 instead of 80.
- File Transfer Protocol Secure (FTPS)
	- An extension of the file transfer protocol
	- Like HTTPS, FTPS also works on SSL/TLS
	- Defined in RFC 4217
- Secure Shell (SSH)
	- This protocol provides secure remote access and works on port 22
		- We like this one
- PGP (Pretty Good Privacy)
	- This protocol is primarily used for encrypting and digitally signing individual messages.
	- Particularly signs emails.
	- Uses a combination of symmetric and asymmetric encryption.
	- In contrast to SSH, HTTPS, and SSL/TLS, those are protocols designed to secure entire communication channels between computers or networks. 
		- I think this statement means the PGP is more about securing individual messages.

#### 3.4.3.2 - Transport Layer Security

Transport layer and application layer security is achieved by introducing a security layer between the application and transport layer, called the **secure sockets layer** (SSL). The updated version of SSL is called **Transport Layer Security** (TLS). 

TLS primarily uses AES for confidentiallity, Diffie-Hellman or RSA for key exchange, and secure hash algorithms (SHA) for hashing. TLS/SSL supports a range of encryption algorithms called **cipher suites**. The client-server pair agrees upon the cipher suite during the TLS handshake. 

#### 3.4.3.3 - Network Layer Security

Network layer security is achieved through internet protocol security (IPsec). This works with both TCP and UDP transport protocols. It protects and encapsulates the entire packet presented to the IP layer, including all upper layer header bits. 

### 3.4.4 - OWASP

p. 72;

OWASP stands for **Open Web Application Security Project** (OWASP). This is an online platform for open-source articles, documentation, software tools, and technologies related to the web application security. 

### 3.4.5 - Exercise

Get more packets for HTTPS and HTTP. Compare the packets and note the differences. The look for TLS protocol packets and find supported encryption algorithms and keys. 

## Summary

p. 72;

The internet is the most complicated, widespread, and utilized computer network. The protocol stack for the internet is known as TCP/IP protocol suites. 

The communication protocols for the internet are divided into five layers:
- application
- transport
- network, or IP
- data link
- physical layers

OSI model also includes presentation and session layers, TCP/IP model does not include these layers. Services of these two layers are merged into the application and transport layers. 

Popular application layer protocols are:
- HTTP for web services
- SMTP for forwarding email
- POP3 and IMAP for retrieving email from servers
- DNS for tranlating host names to IP addresses

Most popular transport layer protocols:
- TCP for reliable transmission
- UDP for unreliable transmission

The network layer protocol is IP, or IPv4. There are multiple supplementary protocols for IPv4 such as:
- ICMP
- IGMP

Commonly used link layer protocols are:
- ARP
- RARP
- NDP

TLS protocol is used to secure the transport lyer.

IPsec is used to secure network layer communication.

Some application layer security protocols are:
- HTTPS
- SSH
- PGP
- FTPS
