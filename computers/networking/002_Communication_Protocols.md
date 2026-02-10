# 2. Communication Protocols

p. 31

After completing this unit you should know / be able to:
- Analyze the transmitted and received packets and protocol.
- Apply the concepts of networking layers, services, and protocols.
- Understand the basics of services, addressing, and protocols for datalink, network, and transport layers. 

## Introduction

p. 32

When someone wants to send information a series of events must occur. Using a written letter as an example:
1. Logical information is encoded into physical form by writing with ink on paper.
2. The sender includes recipient's:
	1. name
	2. address
3. The sender includes
	1. Their own name 
	2. Their own address
	3. The current date
	4. Their *signature*
4. The letter is concealed in an envelope to:
	1. protect it from damage
	2. secure the information from being read by others
5. Sender and receiver addresses must be included outside the envelope.
	1. This includes a *hierarchy* of information for delivery
6. The sender includes a stamp

And these really just represent the FIRST step in the process of mailing the letter. Once dropped at the post office the mail carriers and postal workers from both sides get involved. These people and machines, vehicles, pilots, etc... have their own job protocols. 

This whole process can be divided into several steps or layers, each with different services to get the letter to the proper destination. Each service is maintained by a different job protocol. 

A Computer network, or digital communication, can be compared to sending a letter. Writing the letter can be like an email or text editor, folding the paper is like data compression, the envelope might be cryptography, the post offices might be  the routers of a network, roads like network links, and houses like the end receiver devices. 

Digital communication also uses a hierarchy of addresses. We will dive into the steps, or layers, of sending data in digital communication, and how each layer provides a different service and follows various protocols. 


## 2.1 - The ISO/OSI Reference Model

p. 32

The **International Organization of Standardization** (ISO) has a **standardized open system interconnection** (OSI) model that indicates that a computer networks communicate data through the following SEVEN successive layers:
- Layer 7: Application
- Layer 6: Presentation
- Layer 5: Session
- Layer 4: Transport
- Layer 3: Network
- Layer 2: Datalink
- Layer 1: Physical

The application layer is topmost of the ISO/OSI model. The physical layer makes up the bottom. The typical process is when a sender sends a message it starts in the application layer and travels through the other layers down to the physical layer until it gets to the application layer of the receivers device. 

The 7 layers exist only on end devices. Connecting devices do not have the top four layers, so they only have Physical, Datalink, and Network layers. Software applications are installed only on the end devices, not connecting devices. 

Routers have only the three lower layers, and switches have only the two lower layers. 

### Layer 7: Application Layer

The **Application Layer** deals with the software applications and application layer protocols. End users communicate through software applications, examples being
- Email applications
- Web browsers
- Audio & video messengers
- etc...

Applications are installed on the end devices and communicate using various protocols depending on the types of service. 

Classic example is the **hypertext transfer protocol** (HTTP), which is used for web services. Also the **Simple Mail Transfer Protocol**, used for email services. 

The primary service of the application layer is to establish communication between end-user devices and following application layer protocols. It also provides various services based on the application service, such as user-login, message upload and download, and file transfer. 

#### Layer 6: Presentation Layer

On the *sending side*, the **Presentation layer** receives the message from the application layer and formats it into a desired data structure using various encoding techniques. 

The encoding is also used to compress the data and pass it to the following layer (Layer 5: Session Layer). 

On the receiving side, this layer receives data from the session layer, decompresses, decodes, and formats the data to present to the application layer. 

Some examples, loosely speaking:
- Secure Socket Layer (SSL)
- HTTP/HTML (agent)
- File Transfer Protocol (FTP)
- AppleTalk Filing Protocol,
- Telnet

#### Layer 5: Session Layer

The **Session Layer** is responsible for establishing, maintaining and ending communication sessions between end-users. It also *synchronizes* the end-users for various modes of communication, for example:
- Simplex
	- Example here is node A can transmit data to node B, but not vice-versa.
- Half Duplex
	- Supports bidirectional communication
		- Node A can transmit to Node B and vice-versa
	- They cannot transmit to each other simultaneously.
- Duplex
	- Supports simultaneous bidirectional communication.

The example to remember is when someone logs into a server using a web browser. The session layer establishes a connection, tracks session times, and closes the connection once the user logs out or the session time expires. 

#### Layer 4: Transport Layer

The **Transport Layer** provides reliable data transfer services. 

On the sending side, it:
- Receives data from the Session Layer;
- Breaks it into segments;
- Adds additional bits to ensure reliable data transfer;

What is this *reliable data transfer*? **Reliable data transfer** services include:
- error detection-correction mechanisms;
- flow control;
- congestion control;
- data loss detection and re-transmission.

#### Layer 3: Network Layer

The **Network Layer** receives data from the transport layer and adds routing information. The two most important services of the network layer are:
- Packet Forwarding
	- Mainly deals with forwarding data to the appropriate router output port.
- Routing
	- Determines the best path between the end-users.

#### Layer 2: Data Link Layer

The **Data Link** layer connects the logical and physical forms of data. It receives data from the network layer as logical bits. This layer then converts these logical bits to physical bits as electric or electromagnetic signals. It also provides media access control and synchronization between sender and receiver. 

It also provides error-detection and flow-control mechanisms.

#### Layer 1: Physical Layer

The **Physical Layer** is the connecting path, or link, between network nodes. 

Here, data travel as electrical, electromagnetic, or optical signals. 

Most popular physical links are:
- Coaxial cables;
- Twisted pair cables;
- Optical Fiber;
- Wi-Fi;
- Microwave signals;
- Radio Signals.


### Protocol Data Unit and Addressing

p. 34

When a sender sends data to the receiver, data are passed through all 7 layers. Each layer adds additional bits to the data received from the upper layer. The data unit of a layer is called the **protocol data unit** (PDU). 

The PDU is known by different names at each layer. It has two parts: 
- Header
	- Additional bits added to the received data, also called *header bits*. 
	- These include service information and the layer addresses of the sender and receiver. 
		- Example being a transport layer header includes the port numbers, a network layer includes IP addresses, and a datalink layer includes the MAC addresses of sender and receiver. 
- Payload
	- Typically the data received from the previous layer.

p. 35

A **port number** is a 16-bit number that addresses an application program installed on sending or receiving end nodes. Examples are:
- Port 80 for  HTTP web services;
- Port 440 for HTTPS;
- Port 993 for secured mail transfer. 

You can find a list of transport layer port numbers from Internet Assigned Numbers Authority (IANA). 

An **Internet Protocol** (IP) is a 32-bit number that indicates a device on a network. Devices connected to the internet or a LAN obtain an IP address. 

A **MAC** address is a 48-bit number that indicates the link layer device of a network node. 

The **Socket Address** is a combo of an IP address and port number. 

The course book on page 35 shows the ISO model architecture, layer names, PDU names of each layer, and corresponding layer addresses. 

![[Pasted image 20251102163504.png]]


## 2.2 - Data Link Layer: Standards and Technologies

p. 35

The **Data Link Layer** is the second layer, between the network and physical layers. It is implemented in a **Network Interface Controller** (NIC) card. NIC is hadware that connects the data link layer to the physical layer. Two widely used NIC cards:
- Ethernet
- Wireless Wi-Fi

As stated before, data from the physical layer is in the form of electric or electromagnetic energy or waves. The datalink layer connects the logical and physical layers. 

The protocol data unit is called the **frame**. The *frame header* encapsulates the network layer datagram, or *packet* (network data unit). 

Datalink layer is divided into two sublayers:
- logical link control (LLC)
	- provides error detection and flow control services.
- media access control (MAC)
	- provides MAC-based packet forwarding and multiple access control services.

### MAC

The datalink layer address is called the MAC address, might stand for **Media Access Control**. It is a 48-bit, or 6-byte, hardware address. Each NIC card has a unique MAC address. The network layer IP address is a logical address that can be chosen or edited by the user. But the MAC address is a physical address burnt into the NIC card. It cannot be edited. 

A device can have multiple NIC cards though, so it can have multiple MAC addresses. Virtual machines also allows multiple MAC addresses on a single device. 

MAC address is presented in hexadecimal format and each byte is separated by a colon. The **broadcast address** is all 1s:
- `FF:FF:FF:FF:FF:FF`

### Error Detection

p. 36

The datalink layer calculates **Error Detection Bits** (EDBs) based on payload bit values. 
- these are added in the frame header. 
- the receiver recalculates the EDBs. 
- if the calculated bits differ then the bit error is detected. 
	- else, no bit error is detected. 

The datalink layer uses **Cyclic Redundancy Check** (CRC) to detect bit errors. 
1. Sender chooses the number of bits in EDBs ($r$).
2. Then $r+1 = G$ bit number called the **generator**. 
3. The data $D$ are padded with $r$ zeros. 
	1. $D \prime = D + r$ -> is the zero-padded data.
4. Then, $D^{\prime} \mod G = R$ is the remainder.
5. $R$ represented in $r$ bits is the desired EDBs. 
	1. Calculating the remaineder is made simple by performing substuctions using XOR functions. 

In practice, the datalink layer frame uses 32-bit or 4B CRC bits. Typically there is not a correction mechanism, if an error is detected then the frame is simply dropped. 

### Multiple Access Protocols

p. 37

An important service of the datalink layer is that it allows multiple users to transmit over a single physical resource. There are numerous multiple access mechanisms, which can *broadly* be categorized into three types:
- Resource Partitioning
	- resources, such as time or frequency, are partitioned into small portions and divided among multiple users. 
	- Protocols are centralized.
- Taking Turns
	- Users take turns using common resources.
	- Protocols are centralized.
- Random Access Protocols.
	- Random...
	- Protocols are decentralized. 

The protocols that are centralized have a central node that maintains the resource distributions. For decentralized protocols, users access shared resources in a random manner, more or less. 

#### Random Access Protocols

**Carrier Sense Multiple Access** (CSMA) protocol is a solution for random access.

The operation of the protocol is similar to human conversation:
- Node listens before talking.
- If it senses another node is transmitting, it will refrain from transmitting;
	- waiting a random amount of time, then retransmits.
	- CSMA may still suffer from collisions if 2 nodes sense at the same time others are not transmitting and start transmitting simultaneously. 
		- Called the *hidden node problem*.

There are 2 improved versions of CSMA:
- **Carrier Sense Multiple Access with Collision Detection** (CSMA/CD) implements the mechanism to detect collision. 
	- It detects collision by measuring a *signal-to-noise ratio*. 
	- If collision is detected it enters the **binary exponential backoff phase**.
		- If a node experienced collision for $m$ times  to transmit a frame
			- Then it will wait for the time to transmit $512 \times K$ bits. 
				- $K$ is a number randomly chosen from range ${0, 1, 2, \dots, 2^m -1}$
	- Efficiency of CSMA/CD is given by $[1 / ( 1 + ( (5dp) / dt ))]$
		- Where $dp$ and $dt$ are propagation and transmission delays for a transmitted frame.
	- Considered a *reactive* solution to tackle hidden node problems.
- **Carrier Sense Multiple Access with Collision Avoidance** (CSMA/CA) 
	- This is considered a proactive solution to the hidden node problem.
	- Done through exchanging requests to send (RTS) and *clear-to-send* (CTS) messages. 

### Data Link Layer Standards

p. 38

There are several datalink layer standards depending on characteristics of physical layer.

The **Ethernet** is the most widely used datalink layer standard for wired LAN. Ethernet has multiple variations:
- 10BASE-T
	- Designed for 10 Mbps
- 10BASE-2
	- Designed for 10 Mbps
	- standardized for thin coaxial cables.
- 100BASE-T
	- Designed for 100 Mbps
- 1000BASE-LX
	- Designed for 1 Gbps
	- For optical fiber.
- 10GBASE-T
	- Designed for 10 Gbps
- 40GBASE-T
	- Designed for 40 Gbps

The "T" stands for *twisted pair* cable. 

The "BASE" stands for baseband transmission. 

The ethernet-based LANs are standardized by IEEE 802.3. It implements CSMA/CD random access protocol and a 4-byte CRC error detection technique. 

Wireless **Wi-Fi LAN** is the second most widely used LAN. It operates over 2.4 GHz or 5 GHz microwave frequency. 
- Wi-Fi is standardized by IEEE 802.11.
- It implements CSMA/CA random access protocol. 

**Data-Over-Cable** service interface specifications (DOC-SIS) is a standard protocol for hybrid fiber-coaxial (HFC) that combines optical fiber and coaxial cable.

IEEE 802.15 standardizes the physical (PHY) and datalink layers for wireless personal area networks (WPAN). 

There are several versions of IEEE 802.15 for different types of WPAN. 
- 802.15.1 - for Bluetooth technology-based WPAN. 
- 802.15.3 - for high-rate WPAN
- 802.15.4 - for low-rate WPAN (6LoWPAN).
	- Considered the standard for the **Internet of Things** (IoT).
- 802.15.5 - standardize the WMAN mesh network. 
- 802.15.6 - wireless body area network. 

### Switching 

p. 38

**Switches** are layer 2 devices. They have two layers:
- Physical
- Datalink

A switch can filter data based on the MAC address and forward it to the desired output port. 

A **Hub** is a layer 1 device. It cannot filter and forward data based on the MAC address. It forwards incoming data to all output ports.
- This floods the network with unnecessary overheads. 
- Switches overcome this shortcoming through MAC-based forwarding. 

### VLAN

Generally, all end nodes of a LAN are connected to a common switch. 
- For $N$ number of LANs there should be $N$ number of switches. 

Also, all nodes of a LAN reside in the same geographical area.
- Such as the same office floor or building. 

A **Virtual LAN** (VLAN) is a technology that allows the creation of multiple LANs in the same geographical area using only one switch, called the **VLAN Switch**. 
- VLAN is standardized by IEE 802.1Q protocol.
	- It *shims* a 4-byte VLAN tag within a traditional ethernet data frame. 
- Example - Suppose we have a VLAN switch with 100 ports
	- Port numbers 2, 3, 6, 11, 77 are grouped to form LAN 1
	- Port numbers 10, 22, 42, 50 and 87 are grouped to form LAN 2
	- and so on...

A [shim | Wikipedia](https://en.wikipedia.org/wiki/Shim_(computing)) in computing is a library that transparently intercepts API calls and changes arguments passed, handles the operation itself, or redirects the operation elsewhere. 

A **Virtual Private Network** (VPN) overlays a private network on a public network, allowing remote access to a private network. 

VLAN is different from a VPN. The nodes in a VPN are not necessarily connected to a common switch like for a VLAN.
There's a diagram on page 39 showing a router connected to a VLAN switch, which is connected to multiple VLANs itself. 

### MPLS

**Multiprotocol Label Switching** (MLPS) is a 2.5 layer protocol that allows forwarding of data through routers based on an MPLS header instead of an IP address. 
- This technique makes the forwarding process faster by avoiding reading the IP header and looking up routing tables. 

How it works:
- 1.) A selected routed path is chosen between the source and destination (first).
	- In a traditional connectionless network, when a packet travels through a path, each router reads teh header bits and IP addresses, then applies the routing algorithm, looks up routing tables, and then finds the *next hop*. 
		- this process imposes significant processing delays.
	- MPLS choses a path first from source to destination.
- 2.) The network layer data are encapsulated using an MPLS header. 
	- This uses a short label instead of long IP addresses. 
	- This label tells the router what the next hop is.

MPLS is standardized in **Request for Comments** (RFC) 3031, 6178, and 6790.

### Exercise

**Wireshark** is the most popular open-source **packet sniffer** and **protocol analyzer**. It allows your machine to capture real-time packets that are being sent or received by a computer. 

The exercise is to check out this open-source tool. Also, check out the Wireshark Foundation website. 

```bash
sudo add-apt-repository ppa:wireshark-dev/stable

sudo apt update

sudo apt install wireshark

# check version
apt show wireshark

sudo wireshark
```

[GeeksForGeeks | Install Wireshark](https://www.geeksforgeeks.org/linux-unix/how-to-install-and-use-wireshark-on-ubuntu-linux/). 

Installing allows members of the "wireshark" system group to capture packets, recommended over running directly as root so less code runs with elevated privileges. 
- I will not install this feature. 

```bash
iwconfig
ifconfig

sudo wireshark -i <network-name /> -k
```

A Screen pops up and just very busy.

## 2.3 - The Network Layer: Addressing and Routing

p. 40

Network layer is between the datalink and transport layers. It is implemented in Operating Systems (OS). 

network layer address is called the **Internet Protocol** (IP) address. Indicates a network node. More specifically, the OS of a network node. 

Computers can have multiple OSs on them. This includes virtual machines, each with different IPs. 

Network layers are implemented in both end nodes and routers. Two major services of network layer are:
- packet forwarding
- Routing

### 2.3.1 Network Layer Addressing

Two types of IP addresses:
- IPv4
	- Internet Protocol version four
	- This is traditional network layer addressing scheme. 
	- It has four octets; or 32-bits.
	- written like `a.b.c.d`
	- Each end device of a network has a unique IP addressed
		- each port of a router has a unique IP address.
- IPv6
	- Internet Protocol version six

#### Subnet Mask

p. 41

All end nodes or hosts connected to the internet through a common router port maintain a common IP pattern, called a **subnet mask**. 

The network that connects to the internet through a common router port is called the **subnet**. 

The IP address of a subnet host is usually denoted by the following classless interdomain routing (CIDR) notation
- `a.b.c.d/e`
- `e` indicates that the subnet mask contains *e* bits, allowing for $2^{(32-e)}$ hosts in a network. 
	- To be more practical, the total number of hosts $2^{(32-e)} - 2$ hosts in a network.
	- e.g.) `192.168.0.4/23` indicates the leftmost 23 bits (of 32 total bits) of IP address make up the subnet mask. 
		- Gives a maximum of $2^9-2 = 510$  hosts. 
		- `1100 0000`
		- `1010 0010`
		- `0000 000-`
		- `---- ----`
- The **internet service provider** (ISP) assigns a subnet mask to limit the number of users in a network. 
- Subnet mask is also used to filter incoming and outgoing packets of a network. 

To convert [Decimal To Binary](https://www.wikihow.com/Convert-from-Decimal-to-Binary) you can continuously divide by 2 and track the remainders. 

#### Network Address Translation

**Network Address Translation** (NAT) is a remapping technique used to hide a local host IP from the global network or internet by combining the port number with an IP address. 
- This is done by a NAT router, which also maintains the remapping table. 

Here is an example of a NAT scenario where the router connects a LAN inside port `192.168.1.3` and connects the LAN to the internet, or WAN, through the outside port `140.5.1.2`. Here is the 4-step process:
- The sending host with socket `193.168.1.1:5060` sends a message to the receiving host with socket `145.3.2.1:80` (typically HTTP).
	- Note which are IP addresses and which are ports.
- The NAT router translates the local IP and port to global (or public) IP and port. 
	- It may have `140.5.1.2:5353`.
	- The port is chosen arbitrarily by the router, but the router then knows that this port is for that internal IP address.
- The router sends the request.
- The request is received by `145.3.2.1:80` and processed.
- A response is sent to `140.5.1.2:5353`, the public socket.
- The NAT table translates the global address `140.5.1.2:5353` to the local address `192.168.1.1:5060`.

There's an image on page 42, and there's also additional complexities abstracted out of this demonstration, like the Gateway IP address, which could be like `192.168.1.3`. I think that is the internal Router IP address, and it has the public facing IP address to the internet. 

#### IPV4 

**IPv4** is a 32-bit address. This means there are a total of $2^{32}$ possible global addresses (around 4.3 billion). 

According to [Number of Internet and Social Media Users Worldwide as of October 2025 | Statista](https://www.statista.com/statistics/617136/digital-population-worldwide/?srsltid=AfmBOorzafTZZKV56Wt_bxRnwK8tZu7oER3NtnXQfIN2claN1Rwv6_wZ) there were around 6.04 billion users in late 2025. [Statista](https://www.statista.com/statistics/1559435/connected-devices-worldwide/?srsltid=AfmBOor_ttinCNDDaB4FVLznENcBSZ4bNNbeAnjZWHJGGxKETuZPZexC) shows another report that in late 2025 there were over 30 billion connected devices, including short-range and wide-area IoT devices. [IoT Analytics](https://iot-analytics.com/number-connected-iot-devices/) finds there to be 21.1 billion IoT devices connected and growing. 

The point is that IPv4 cannot support this number of devices. 

Traditional IPv4 addresses were divided into 5 classes:
- A
	- First octet range between 1-126
- B
	- Octet range between 128-191
- C
	- Octet range between 192-223
- D
	- Reserved for multicasting
- E
	- Reserved for future use.

Using NAT, an ISP can use only one global IP to serve an entire subnet or LAN. So we have layers of IPv4 addresses, where each layer can reuse many IP addresses. Another advantage of NAT is that it hides local IPs from the internet, adding a layer of security to the local network. Another advantage is that if the LAN chooses a new ISP, it can still use the same IP addresses for the LAN devices. 

Disadvantages of NAT:
- NAT hides local IP addresses which can also be considered a security issue. 
	- Are you communicating with the right service?
- The translation process imposes an additional delay and layer of complexity. 
- NAT also violates the OSI layering architecture.
	- The router is a network layer device, there isn't a transport layer (it is absent). 
	- The router should *not* deal with port numbers because that is a transport layer address. 

Is NAT necessary? IPv6 addresses the capacity issue created by IPv4 which could render NAT useless. 

#### IPv6

**IPv6** is a 128-bit network layer address introduced to resolve the capacity limitation of IPv4. IPv6 can represent up to $2^{128} = 3.4 \times 10^{38}$ unique IP addresses. You could say this is an astronomical number. 

Some advantages:
- IPv6 simplifies the network layer datagram header to reduce the processing delay. 
- Allows the filtering and forwarding of data based on traffic flow. 

Moving from IPv4 to IPv6 is a slow process. The **Internet Corporation for Assigned Names and Numbers** (ICANN) maintains and distributes the IP address through the **Internet Assigned Numbers Authority** (IANA). The backward compatibility of IPv6 with IPv4 is achieved through *tunneling*. 

**Tunneling** is a technique of encapsulating entire IPv6 datagrams using IPv4 headers. 

Page 43 has an interesting image of IPv4 and IPv6 headers. I have notes somewhere from a Google Course.

#### DHCP

When a new device is added to a network it initially does not have an IP address. The device requests an IP address from the server and the server will provide it one. **Dynamic Host Configuration Protocol** (DHCP) is the process of achieving a new IP address. It involves the following steps:
- **Discovery**
	- The client broadcasts a DHCPDISCOVERY message with source IP `0.0.0.0:68` and destination IP `255.255.255.255:67`.
- **Offer**
	- The server replies with DHCPOFFER message destination IP `255.255.255.255:68`
		- is it not destination port 67?
		- The message also contains the offered IP address for the client.
- **Request**
	- The client replies with DHCPREQUEST message with
		- source IP `0.0.0.0:68`
		- destination IP `255.255.255.255:67`
		- includes the requested IP address that was offered above. 
- **Acknowledge**
	- The DHCP server acknowledges the request message by sending a DHCPACK message with destination IP `255.255.255.255:68`.

### 2.3.2 Network Layer Services

Primary services a network layer provides are packet forwarding and routing. 
- packet forwarding
	- a per-router local problem.
	- This means forwarding a packet from the router's input port to the proper output port. 
- routing
	- considers the overall scale of the network.
		- including all routers and links.
	- **Routing** is the process of selecting the suitable route or path between sender and receiver. 
	- Each router maintains a forwarding table derived from the *routing algorithm*. 

There are different types of routing protocols used to serve different purposes. 

**Routing** is the process of selecting a suitable path between sending and receiving nodes. 

A **path** is a series of links and a **suitable path** refers to the *least-cost* path. 

**Cost** can be a function of a number of variables:
- distance
- delay
- throughput
- energy

Cost is *inversely* related to the throughput and profit. Some routing techniques are introduced below:
- Dynamic routing
	- Routing table is updated if there are changes in network topology or link cost. 
- Static routing
	- does not update the routing table frequently.
	- Rather; the network administrator decides when to change the routing table.
- Centralized routing
	- A central entity collects routing information from each router. 
	- It then performs the routing algorithm.
	- Then updated table is forwarded to each router by the central entity. 
- Decentralized routing
	- The routing algorithm is performed in each router.
	- Each router updates their own routing tables. 

### 2.3.3 - Routing Algorithms

A **Routing Algorithm** states each step of calculation to find the suitable path. There are 2 main types of routing algorithms: Link State, and Distance Vector. 

#### Link State Routing Algorithm

In a **Link State Routing Algorithm** all routers share routing information with each other by *broadcasting*. 
- Each router receives the routing information about the entire topology.
- Each router runs the same routing algorithm, calculates a suitable path, and updates the forwarding table. 

Dijkstra's Algroithm is widely used to find the least cost path, a widely used link state routing algorithm. It is an iterative algorithm.

[W3 Schools | Dijkstra's Algorithm](https://www.w3schools.com/dsa/dsa_algo_graphs_dijkstra.php) gives a nice explanation. Note this algorithm does not work on graphs with negative edges, but networking should have positive distances anyway. 

Let's talk it through. Suppose we have $z$ as our source node, $D(y)$ is the cost of the least-cost path from $z$ to $y$. Let $p(y)$ be the previous node of $y$ within the least-cost path. Let $N$ be the set of all routers. We can describe Dijkstra's least cost path algorithm as follows:

```python
# N' is the set of all nodes whose least-cost path
# is decisively known.
z = "Source Node"
y = "Destination Node"

def D(y):
	"""
	Cost of the least-cost path from z to y
	"""
	...

n_prime = get_all_nodes()

# N is the set of all routers
for y in N:
	if is_single_hop_distance_with_z(y):
		D_y = c(z, y) // c(z, y) # path cost from z to y
	else:
		D_y = math.inf # infinity

while n_prime != N:
	for x in N/n_prime:
		if c(z, x) == D_x:
			n_prime += x
		# Find D(y) for each neighbor y of x that is not an element of n_prime:
		# D(y) = min(D(y), D(x) + c(x, y))
```

Honestly, don't follow the book. Their instructions are actually terrible. Like, we mentioned $p(y)$ in the preamble, and yet it's not used at all in the algorithm. $D(y)$ shouldn't be a function because it's clearly a variable...

And then the figure show's $p(y)$ - I think the explanation is confusing and poorly done. 

But until $N'$ is the set of all routers, we keep calculating. What do we calculate? *The shortest path from one vertex to all other vertices*. 

Page 46 shows figure 12. D - least cost path, p - last node. If you stare long enough it'll make sense. You will also see that from the starting router $Z$ to $T$, there are multiple paths with the same distance, but some have more steps. 

#### Distance vector routing algorithm

These routers do not broadcast routing information. Each router shares the routing information with the neighbor routers (i.e., within a single hop distance). Information includes the number of links and associated link costs. 

Distance vector routing is an iterative, asynchronous, and distributed algorithm. 

The *least cost path* between $z$ and $y$ is calculated using **Bellman-Ford** equation:

$$
d_z(y) = min_x \lparen c(z, x) + d_x(y) \rparen
$$

Each router updates its table if a change in topology or link cost is noticed. It will then forward the updated information to its neighbors. The neighbors do the same until all router have achieved stable routing tables. 

### 2.3.4 - Routing Protocols

**Routing Protocols** define how the message transfer and information exchange will take place between routers to run the routing algorithm. 

The set of routers within an Autonomous System (AS), or area, is called the **routing domain**. 

The routing protocol for exchanging information among the routers within a domain is called **intra-domain routing** or **Intra-AS Routing Protocol**. It's also known as the **Interior Gateway Protocol** (IGP).

Each domain has a single IGP protocol. Different domains can have different IGP protocols. 

The router (or gateway) that connects the intra-domain routers with another domain is called the **border router**. 

The routing protocol that deals with exchanging information among border routers is called the **inter-domain routing protocol** or **exterior gateway protocol** (EGP). 

Let's talk about some of the various routing protocols below.

#### OSPF

**Open Shortest Path First** (OSPF) is an IGP that finds the shortest path between teh sender and receiver. It's based on the link state routing algorithm. 
- Each router maintains a routing database and routing table.

OSPF is a *dynamic algorithm* in that once it senses any topological changes it immediately recalculates the routing table and broadcasts routing information to other routers. 

OSPF also provides:
- message authentication
- multi-equal-cost paths
- multicasting.

OSPF is standardized in RFC: 2328, 5340, 5709, 7474, 6549, and 6860. 

There is figure on page 47 showing that border routers, AKA gateways, connect different AS areas together, each having their own slew of multiple routers. There is another "Backbone Area" where each gateway connects to a separate *backbone router*. And each backbone router connects to a **Boundry Router** whose connection then leaves the diagram. 

#### RIP

The **Routing Information Protocol** (RIP) is a *traditional* IGP protocol. 
- Based on the distance vector routing algorithm.
	- Bellman-Ford equation.

RIP can handle a maximum 15-hop path. In RIP, a hop count of 16 indicates the destination router is not reachable. 

Maybe it's used for small networks, but it's not popular and used much today. It has limitations, but also fewer overhead bits. 

RIP also supports cryptographic authentication and is standardized in RFC: 2453, 4822.

#### BGP

**Border Gateway Protocol** (BGP) is an EGP (typo?), or inter-domain routing protocol. 
- It finds a suitable route between two nodes that reside in two different autonomous systems or domains. 
- Exchanges information based on TCP transport layer protocol with port 179.

Two types of TCP connections for BGP:
- External BGP (EBGP)
	- communicating routers reside in two different domains. 
	- a border router uses EBGP to exchange information with another border router in a different domain. 
- Internal BGP (IBGP)
	- sets up connections between routers residing in the same domain.
	- a border routers also uses IBGP to exchange information with the interior routers within the same dinaub,

BGP protocol is documented in RFC: 4271, 6286, 6608, 6793, 7607, 7607, 7705, 8212, 8654.

### 2.3.5 -  Software Defined Network

A **Software Defined Network** (SDN) is a network management technology where the routing is done by a central entity. 
- Central entity is a distributed system of multiple servers.
- SDN is mainly based on IPv6
	- Allows for **flow**-based forwarding.
	- **OpenFlow** is a popular protocol for SDN
- The **Open Network Operating System** (ONOS) is a platform for SDN technology.

**Flow**, or *traffic flow*, is a stream of packets that move between the source and destination. They can be distinguished from other packets based on various attributes, or a combination of attributes, such as:
- IP address
- MAC
- port number

Another exercise is to download sample packets (.pcap or .cap files) from ICMP, OSPF, and RIP from Wireshark and investigate the packet header fields and layer addresses. 

## 2.4 - The Transport Layer: Reliability and Flow Control

p. 48

The **Transport Layer Entity** is the software that implements the transport layer services. These are mainly *system programs* implemented in the operating system kernel. A transport layer entity can also be part of an application program. 

The transport layer establishes a logical connection between sender-receiver application programs. It also provides reliable data transfer services between them. Reliable services include:
- flow control
- congestion control
- multiplexing
- order packet delivery
- packet loss detection and retransmission
- connection establishment
- closing

Suppose we are viewing the *sender*, on the sending side.
- The transport layer receives a message from the software application.
- It breaks the message into equal-sized pieces called **segments**.
- Port numbers of the sender and receiver applications are added to each segment header.
	- This is to identify the sender-receiver applications.
- Header also includes the service bits. 
- The segment is then forwarded to the network layer. 

Now, on the receiver side:
- The transport layer receives segments from the network layer and reads the port number from the segment header.
	- To identify the target application program.
- The subsequent segments are then merged and pushed to the application layer. 

The transport layer services can be connection-oriented or connectionless. The most familiar connection-oriented protocol is the **Transmission Control Protocol** (TCP). The most popular connectionless protocol is the **User Datagram Protocol** (UDP). 

TCP provides a reliable data transfer service. UDP provides *best-effort* services, but does not guarantee reliable data transfer. 

Other popular transport layer protocols:
- Stream Control Transmission Protocol (SCTP)
- Resource Reservation Protocol (RSVP)
- Datagram Congestion Control Protocol (DCCP)
- QUIC

### 2.4.1 - User Datagram Protocol (UDP)

UDP is a *connectionless* transport layer protocol. It does **not** guarantee reliable data transfer services. This means it does not provide:
- in-order packet delivery
- flow control
- congestion control
- error detection
- packet loss detection
- retransmission services.

Why is UDP useful?
- Good for when achieving reliable data transfer is not assured, or implementing reliable data transfer is not essential.
- Examples:
	- Real-time services
	- voice over internet protocol (VoIP)
	- data streaming
	- multicasting
	- broadcasting
- Transaction-based or query-response based protocols also use UDP.
	- Domain name system (DNS)
	- Dynamic host configuration protocol (DHCP)

It's usually like, for streaming, so much information is sent that you need something to send data fast. And in the case of streaming a video, if a couple packets go missing, the overall video won't look different to the human eye (I think). 

#### UDP Segment Structure

UDP is standardized in RFC 768. The DUP datagram structure is...
- Header Size is 8 bytes of the following fields
- The **Source** port = 16-bit port number of the sending side application.
	- This field is optional.
- The **Destination** port = 16-bit destination port address.
- The **Length** is the size of the datagram in bytes.
	- includes both header and payload bits. 
	- minimum value of the length field could be 8 bytes.
		- This means the datagram *only* includes the header bits.
- The **Checksum** = 16-bit number used for error detection.
	- AKA **internet checksum**.

Then is the payload.

#### Internet Checksum

To calculate the checksum the data are represented as 16-bit chunks. 
- if the number of bits is not multiple of 16
	- then extra zeros are added at the beginning of data bits until so.
	- This is called **zero padding**.
- The 16-bit chunks are added. 
	- If addition produces a *carry bit*
		- Then the carry bit is added to the sum
		- Else, nothing
- Finally, taking **one's complement** of the result produces the internet checksum. 
	- that is simply flipping ones to zeros and vice-versa

When calculating, both the header and payload bits are considered, but the checksum portion is set to zero. 

When the receiver side receives the segment, it calculates the checksum of the received segment. If the calculated checksum value is equal to the value provided, this indicates there is no bit error. 

### 2.4.2 - Transmission Control Protocol (TCP)

TCP is a *connection-oriented* reliable data transfer protocol standardized in RFC 793, 879, 6528, and 6691. It is **connection-oriented** because it establishes a connection between sender-receiver pair before transferring the data or segment. And after the transmission of the segment, the connection is closed formally by both parties. 

Maximum TCP segment size (MSS) is 536 octets by default. 

TCP is considered reliable because it provides services to ensure error-free in-order data delivery. Services include:
- error detection
- loss detection
- retransmission
- in-order delivery
- flow control
- congestion control

#### TCP Segment Structure

TCP segment structture is defined in RFC 793. It's bigger than UDP, the header segment is usually 40 bytes. It includes the following fields:
- **Source Port Field**
	- 16-bits
	- The port address of sender application
- **Destination Port Field**
	- 16-bits
	- port address of receiving application
- **Sequence Number Field**
	- 32-bits
	- holds the sequence number of the first data octet of the segment. 
	- if the SYN bit is 1
		- then this field value is equal to the ISN (Initial sequence number)
			- And ISN+1 indicates the first data octet.
- **Acknowledgment Number Field**
	- 32-bits
	- The field value is equal to the sequence number of the segment that the sender expects to receive next.
- **Data Offset Field**
	- 4-bits - based on $x + 6 + 6 = 16$ - book didn't explicitly say
	- indicates where the payload data starts in the segment
- **Reserved Field**
	- 6-bits
	- Reserved for future use.
- **Control Flags Field**
	- 6-bits - 6-1 bit flags
	- URG = indicates urgent data
	- ACK = indicates acknowledgement
	- PSH = indicates to push segment immediately to the next layer
	- RST = indicates to reset connection
	- SYN = indicates connection request
	- FIN = indicates to end data transmission
- **Value Window Field**
	- 16-bits
	- indicates the size of the receiver buffer
		- the number of bytes this segment sender expects to receive
- **Checksum Field**
	- 16-bits
	- the internet checksum value
- **Urgent Pointer Field**
	- 16-bits
	- if URG bit is set to 1
		- then this value indicates the sequence number of the octet next to the urgent data.
- **Options Field**
	- Can hold the Maximum Segment Size (MSS) value.
	- If the field does not exist then the segment can be of any size.
- **Padding Field**
	- indicates the number of zero padding bits added to make the segment size multiple of 32

#### TCP Connection: Establishment and Termination

TCP exchanges initial messages to establish a connection between the sender-receiver pair *before* the actual data transmission. 

After a successful data transmission, the two parties exchange some messages to end the communication.

The **Client Process** is the software program that initiates the connection. 

The **Host Process** is the other process that accepts the connection invitation. The step of establishing a connection is the **handshake**. 

TCP used the following three steps to establish a connection called the **three-way handshake**:
- The client sends a TCP header with:
	- SNY = 1
	- ACK = 0
	- Sequence No. = 0
		- or a random number
- The host replies with a TCP header with:
	- SYN = 1
	- ACK = 1
	- Acknowledgement No. = 1
		- i.e.) received sequence No. + 1
	- Sequence No. = 0
- The client replies with TCP header with:
	- SYN = 0
	- ACK = 1
	- Acknowledgement No. = 1
	- Sequence No. = 1

The connection termination is completed with the following four steps:
- The client sends:
	- FIN = 1
	- Sequence No. = X
	- This  means the client has finished sending data, but can still receive data.
- The host sends:
	- ACK = 1
	- Acknowledgement No. = X + 1
- The host sends:
	- FIN = 1
	- Sequence No. = Y
	- This means the host is finished sending data.
- The client sends:
	- ACK = 1
	- Acknowledgement No. = Y + 1
	- The host closes the connection after receiving this acknowledgment. 
	- The client does not close the connection immediately
		- It waits for twice the length of timeout period before terminating the connection.

#### Loss Detection and Recovery

After sending a packet with `Sequence No. = X` the client waits to receive a reply from the host with `Acknowledgement No. = X + 1`. It waits until the timeout interval. 
- If the reply is not received within the timeout interval,
	- then packet is detected as lost
		- And the client retransmits the packet to recover the loss.

Retransmission timeout interval is calculated as follows:

$$
\begin{align}
timeout &= estimatedRRT + 4 \cdot devRTT \\
estimatedRTT &= (1 - \alpha) \times estimatedRTT + \alpha \cdot sampleRTT \\
devRTT &= (1 - \beta) \times devRTT + \beta|estimatedRTT - sampleRTT|
\end{align}
$$

**Round Trip Time** (RTT) is the time interval between sending a packet and receiving corresponding acknowledgment; AKA Round Trip Delay. **Sample RTT** is the RTT of the most recent packet. 

#### Flow Control

We know that a received packet waits in a receiver buffer until the previous packet is processed. When packets are received out of order, the received packets also wait in the buffer until the missing packet is received. 

If the sending side transmits too fast, compared to the receiver's processing speed, the receiver buffer will overflow. This can cause newly arrived packets will be dropped or lost. The **TCP flow control mechanism** restricts the sender from transmitting at a higher rate to protect the receiver buffer from overflow. 
- this is done by setting the **Window** field of the TCP header equal to the free buffer size. 
	- Window is AKA **Receive Window**.
- If the client sets the receive window to 1000 bytes
	- The server will not send more than 1000 bytes of data without acknowledgment.  

#### Congestion Control

Client and server can be connected through multiple links and routers. 

Generally, a router is connected with multiple links. This means it may, and can, receive data from multiple sources simultaneously. 
- If the data arrival rate in a router is *higher* than its service rate (i.e., processing capacity)
	- Then, the router buffer may overflow
		- This can cause packet drop or packet loss

**Network Congestion** is the phenomenon of pushing too many data through a network link. 

TCP detects network congestion in two ways:
- Retransmission timeout
- Triple-Duplicate Acknowledgment

Once detected, the congestion window size is reduced to avoid congestion. 

The two most common congestion control protocols are TCP Tahoe, and TCP Reno. There are over 30 variants of TCP congestion control protocols available. Only a few are really used in practice. 

Concepts to know before discussing TCP congestion control protocols:
- Congestion window is the number of octets, or bytes, a sender sends consecutively without receiving acknowledgment. 
- **Cumulative acknowledgment TCP** uses cumulative acknowledgment scheme.
	- The acknowledgment of $n$ indicates that the receiver received all packets up to $n − 1$ and it is waiting to receive the packet $n$.
- **Duplicate acknowledgment** means 
	- if packet $n + 1$ is received before the packet $n$ (out of order), 
		- then the receiver will send the acknowledgment $n$ again.
			- The sender will receive duplicate acknowledgment of $n$. 
	- If packet $n + 2$ is also received out of order before $n$, 
		- then the receiver will send the acknowledgment $n$ for one more time. 
	- If the packet $n + 3$ is also received out of order, 
		- The sender will receive triple-duplicate acknowledgment of $n$.
- **Fast retransmission** means once the sender receives a triple duplicate acknowledgment, it retransmits the packet $n$ immediately without waiting for the timeout. 
	- This scheme is known as fast retransmission. Fast retransmission indicates mild congestion in the network.
- **Explicit congestion notification** (ECN) is an additional feature of IP and TCP protocols.
	- Allows E2E notification of congestion.

**Explicit Congestion Notification** (ECN) is an extension added to IP that indicates two ECN bits in the IP header and allows congestion to be recognized without any packets being dropped. if a router experiences congestion (i.e., it drops packets due to buffer overflow), it sets the ECN bit of the header to notify the end-nodes that congestion is detected.

So, congestion is detected only when data is lost?

#### TCP Tahoe and Reno

These deal with congestion in two phases:
- Congestion Avoidance
	- AKA: TCP Slow Start
	- Initial congestion window size, CWND, is set to 1 maximum segment size (MSS). 
	- For each successful transmission the CWND is increased to a power of two. 
	- It will stop increasing when it hits a predefined threshold of segment size, increasing linearly instead of exponentially.
		- Usually by 1 MSS per successful transmission.
- Fast Recover
	- TCP enters in fast recovery phase once a retransmission is triggered. 
	- It also re-enters the congestion avoidance phase, setting:
		- `ssthreshold = CWND / 2`
		- `CWND = 1`
	- If re-transmission is triggered due to *triple duplicate acknowledgment*
		- AND we are using TCP Reno,
			- Then it sets:
				- `ssthreshold = CWND / 2`
				- `CWND = CWND - 3`

Another exercise to look into Wireshark things.

## Summary

p. 55

There are seven layers of computer networking: 
1. Application
	- Provides an application interface for users. 
2. Presentation
	- Encodes application layer data for compression and encryption purposes.
3. Session
	- Maintains the sender-receiver session connection
4. Transport
	- Provides reliable data transfer, error detection, flow control, and congestion control services. 
5. Network
	- Provides an application interface for users. 
6. Data Link
	- Provides an application interface for users. 
7. Physical. 
	- Provides an application interface for users. 

Each layer provides various services and addresses: 
- Transport = Port number, 
- Network = IP address
- DataLink = MAC address

The two most popular transport layer protocols are TCP and UDP. TCP is a connection-oriented, reliable protocol, whereas UDP is an unreliable and connectionless protocol. This means UDP does not provide flow control, con-
gestion control, packet loss detection, retransmission, or in-order
delivery services. 

The two main services provided by the network layer are packet forwarding and routing. Two widely used routing algorithms are link state and distance vector routing. Link state routing is based on Dijkstra’s least–cost path algorithm, whereas distance vector routing is based on the Bellman-Ford equation. Some other common network layer protocols are OSPF, RIP, and BGP. OSPF is based on link-state routing, RIP is based on distance vector routing algorithms, and both are predominantly intra-domain routing protocols. BGP is an inter-domain
routing protocol. ICMP protocol is used to exchange control messages
between routers.
