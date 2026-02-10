# 6. From Distributed Systems to Ubiquitous Computing

pp. 107-116;

We will learning the following:
- Understand the concepts of decentralized mobile computing.
- Analyze the concepts of mobile computing protocols.
- Apply the aspects for distributed ledger technology in Internet of Things (IoT).
- Design and implement a decentralized application.

## Introduction

- Centralized computer networks control services and decisions from a single node.  
- Distributed systems perform computation simultaneously across multiple nodes.  
- Centralized distributed systems involve multiple nodes for computation but maintain central control.  
- Decentralized distributed systems operate without centralized control.  
- Distributed ledger technology exemplifies decentralized systems, where a ledger is shared among nodes.  
- Nodes in a distributed ledger can access and update the ledger concurrently.  
- The unit explores distributed ledger systems, ubiquitous computing, and the Internet of Things (IoT).  
- Ubiquitous computing, or pervasive computing, seeks to enable computing across various devices everywhere.  
- Devices for ubiquitous computing include computers, smartphones, wearables, appliances, and vehicles.  
- IoT connects diverse devices to the internet.

## 6.1 - Distributed Ledger Technology

p. 108;

- Distributed Ledger Technology (DLT) operates on a decentralized network without a central authority, enabling a platform for decentralized applications for transaction management.  
- Key features of DLT include:  
	- **Decentralization**: No central authority prevents single point failures and security attacks.
		- protects against tempering by a single party.
	- **Distribution**: Resources are spread across multiple machines, including software and hardware.
	- **Immutability**: Transactions can be traced and audited via a secure ledger.
	- **Irreversibility**: Transactions become irreversible after a certain period.
	- **Data Consistency**: Ensures consistency of ledger data in distributed environments.
	- **Data Provenance**: Digital signatures via public key cryptography validate data authenticity.
	- **Distributed Consensus**: Utilizes consensus algorithms to achieve agreement on data.
	- **Accountability and Transparency**: Preserves transaction authenticity, immutability, irreversibility, and provenance, fostering trust in recorded transactions.

Think of it like a database deployed over multiple distributed machines. There's no central authority to maintain the database. The DLT platform is used for developing decentralized and distributed applications for registering, sharing, and synchronizing transactions on digital assets. 

DLT is a decentralized and distributed technology. It is primarily build on Peer-to-Peer (P2P) network architecture instead of a client-server architecture. 

### 6.1.1 - Types of Distributed Ledgers

- Two main types of distributed ledgers exist: public and private.  
- A public ledger is characterized by transparency and openness, allowing anyone to update it via transactions, which can raise privacy concerns.  
- In contrast, a private ledger restricts access and updates to authorized entities, thereby preserving data privacy.

### 6.1.2 - DLT Data Structure

- Two main data structures for a distributed ledger are blockchain and **direct acyclic graph** (DAG).  
- Blockchain is characterized by a chain of blocks or linked lists with hashes, containing recent transactions from the last few seconds or minutes.  
- Each block's transactions are hashed to form a **Merkel Tree**, with the tree's root indicated in the block.  
- Blockchain is append-only, confirming an immutable log of all transaction histories in the network.  
- DAG is a less common data structure for distributed transactions, beginning with an initial transaction that is validated by previous transactions.  
- Newly submitted transactions in a DAG must validate two prior, unapproved transactions in the graph.

### 6.1.3 - DLT Protocol Stack
#### Application Layer

The application layer provides the software user interface. This can be developed by 3rd party on top of an underlying DLT architecture. 

#### Contract Layer

**Smart contracts** are computer protocols that define a set of rules about state transitions and corresponding actions. They are executed automatically on each node. 
- each contract has its own set of assets and states with a unique address
- Smart contract can execute polynomial computational tasks.

Essentially, smart contracts provide a platform to build business applications such as cryptocurrencies. 

#### Consensus Layer

**Consensus Layer** handles distributed consensus to ensure trustworthiness of a block. It also ensures all nodes have consistent ledger copies. 
- Why might different nodes have different copies of the ledger?
	- network faults
	- delays
	- malicious nodes
	- The above reasons may cause disagreement between network nodes and the consensus layer aims to resolve these disputes.

#### Network Layer

The *goal* of the **Network Layer** is to provide distributed network architecture. 
- This is done by forming a P2P network based on communication protocols like:
	- transmission control protocol/internet protocol (TCP/IP)

#### Data Layer

The **Data Layer** collects data from the lower layer through transactions and encapsulates it with data layer headers. It also digitally signs the data for authentication and integrity purposes. 

#### Device Layer

The **Device Layer** represents the hardware or physical devices such as:
- sensors
- actuators
- networking hardware

These can be connected with wires or wirelessly. 

The concept of the device layer is similar to that of the physical layer of the open systems interconnection (OSI) model or TCP/IP model.

### 6.1.4 - DLT Platforms

- **Bitcoin**: First digital currency utilizing a P2P distributed network, operates as a public DLT using proof of work (PoW) consensus for block validation.
- **Ethereum**: Similar to Bitcoin, supports cryptocurrency and smart contracts via Ether; transitioned from PoW to proof of stake (PoS) in 2022.  
- **Multichain**: A public platform allowing the use of a private distributed ledger; based on the Bitcoin blockchain, it permits updating block size and protocols.  
- **EOS.io**: Initially developed on Ethereum, it now employs a delegated proof-of-stake (DPoS) consensus algorithm with 21 validators known as block producers.  
- **Other Platforms**: Includes Cardano, Fabric, Sawtooth, IOTA, Cobra, and Waltonchain.

## 6.2 - Aspects of Mobile Computing

p. 111;

- **Mobile Computing** refers to a computing system that is based on a mobile network. 
- Term "**Mobile Network**" refers to nodes of a network that can... *move*. 
	- e.g.) mobile phone devices, wearables (e.g., fitness trackers or smart watches), laptops, and **personal digital assistants** (PDAs).
- A **mobile computing system** is developed on a wireless network and is mainly built on wireless communication protocols.

### 6.2.1 - Mobile Computing and Mobile Networks

The key characteristic of a mobile computing system is that it is deployed on a mobile network.

A network can be considered *mobile* if it shows **any** of the following criteria:
- **User Mobility**
	- the user should be able to access the same service from various geographical locations.
	- Ensures consistent functionality and experience regardless of physical position.
- **Device Mobility**
	- The user should have access to a service from various end devices.
		- e.g.)
			- smartphones
			- tablets
			- laptops
	- Should access services without compromising the service's continuity or quality
- **Network Mobility**
	- The entire network can be mobile
		- e.g.) mobile ad-hoc or body sensor network.
	- Can also mean a user should be able to access a service through a different networks.
		- e.g.) User can connect to a real-time service through Wi-Fi whilst roaming through the home, coffee shop, or campus network.
- **Host Mobility**
	- The mobile device could be either a client or a server.
	- If it is a server;
		- Then it should be able to serve a client whilst roaming through various geographical areas and networks. 

### 6.2.2 - Mobile IP Management

- Mobile devices roam between networks based on the owner's mobility, creating challenges for IP address management.  
- IP mobility is managed through the implementation of a **home agent**.  
- A mobile node retains its home IP address, regardless of its geographical location.
- While away from the home location, the mobile node is associated with a "care of" address that reflects its current location.
	- Current location of the mobile node. 
- Datagrams intended for a mobile node are first received by the home agent, which then forwards them to the mobile node.  
- The management protocol for IP mobility is outlined in RFCs 3344, 4721, 5944, and 6275 (Perkins, 2010).

When a Datagram is *directed* to a mobile node, the datagram is first received by the home agent. This forwards the datagram to the mobile node. 

Figure 26 on page 112 shows how it works. 

### 6.2.3 - Mobile Network Routing Protocols

- The topology of a mobile network continuously changes over time.
	- It is NOT fixed.
- Therefore the following may change over time:
	- ID or IP of a neighbor node, 
	- route between two nods,
	- link cost between two nodes
- Traditional routing algorithms or protocols perform poorly for mobile networks because they do not address this issue.

Below are some common routing protocols for mobile networks.

#### Ad-hoc On-Demand Distance Vector (AODV)

- **Ad-hoc On-Demand Distance Vector** (AODV) is developed to resolve routing issues on mobile ad-hoc networks.
	- Used by the mobile nodes of the network.
- AODV offers:
	- Small memory and processing overhead
	- Low power consumption
	- Low network utilization
- Avoids problems of classical distance vector protocols.
- AODV is defined in RFC 3561.
- Other sources:
	- https://en.wikipedia.org/wiki/Ad_hoc_On-Demand_Distance_Vector_Routing
	- https://datatracker.ietf.org/doc/rfc3561/
	- https://datatracker.ietf.org/doc/html/rfc3561/
	- https://www.sciencedirect.com/topics/computer-science/ad-hoc-on-demand-distance-vector
	- https://www.geeksforgeeks.org/computer-networks/working-of-manets-aodv-reactive-routing-protocol/
	- https://ieeexplore.ieee.org/document/749281

#### Dynamic Source Routing Protocol (DSR)

- **Dynamic Source Routing Protocol** (DSR) is a simple on-demand routing protocol for mobile ad-hoc networks with multiple hops. 
- Allows for:
	- Multiple routes to a destination.
	- the sender to choose a route.
- Two goals of this algorithm are:
	- route discovery 
	- route maintenance to an arbitrary destination
- DSR guarantees *loop-free* routing and offers rapid recovery from a change in topology.
- Primarily designed for a network with up to 200 mobile nodes. 
- DSR protocol is defined in RFC 4728.
- [The Dynamic Source Routing Protocol | IETF.org](https://datatracker.ietf.org/doc/html/rfc4728)
	- looks like legit paper
- [Dynamic Source Routing Protocol | Science Direct](https://www.sciencedirect.com/topics/computer-science/dynamic-source-routing-protocol)
	- Dynamic Source Routing (DSR) protocol is defined as an on-demand routing protocol that utilizes source routing, allowing the initiator to know the complete hop-by-hop route to the destination while maintaining a route cache for network topology information. It consists of two major phases: route discovery and route maintenance.
- [Dynamic Source Routing | Wikipedia](https://en.wikipedia.org/wiki/Dynamic_Source_Routing)

#### Optimized Link State Routing Protocol (OLSR)

- OLSR protocol was developed for mobile ad-hoc wireless networks. 
- As it's name suggests, it is an optimized form of link state routing algorithm that selects some nodes as multipoint relays (MPRs). 
	- Purpose of these selected nodes is to broadcast messages to declare link state information. 
	- The use of MPRs reduces the message overhead compared to the classical link state algorithm.
	- In classical link state algorithm, each node retransmits each message once it has been received for the first time. 
	- In OLSR, only the selected nodes (i.e., MPRs) generate link state information.
		- This reduces *network flooding*.
- OLSR is suitable for large scale mobile ad-hoc network with high node density. 
- OLSR is defined in RFC 3626. 
- Other sources:
	- [Optimized Link State Routing Protocol | Wikipedia](https://en.wikipedia.org/wiki/Optimized_Link_State_Routing_Protocol)
		- optimized for mobile ad-hoc networks. 
		- OLSR is a proactive link-state routing protocol.
	- [OLSR Protocol | IETF.org](https://datatracker.ietf.org/doc/html/rfc3626)
		- looks like paper again
		- Request for Comments 3626
	- [OLSR | Geeks For Geeks](https://www.geeksforgeeks.org/computer-networks/optimized-link-state-routing-protocol/)
		- Nodes re-broadcasts link state information received from its neighbors. 
		- Lists of advantages, disadvantages, and applications. 

## 6.3 - Aspects of Pervasive Computing and the Internet of Things

• Pervasive computing seeks to provide computing access from any location and device at any time.  
• It encompasses end nodes such as desktop computers, laptops, cellphones, sensors, actuators, home appliances, and wearables.  
• The Internet of Things (IoT) is an emerging application of pervasive computing.  
• Pervasive computing is also known as ubiquitous computing.

### 6.3.1 - Properties of Pervasive Computing

Key properties of pervasive computing:
- **Context Awareness**
	- Network nodes have to be aware of context in order to optimize performance.
- **Distribution**
	- The system should be deployed over a distributed network.
- **Autonomy**
	- Network nodes should be self-governing, meaning that they should be able to operate without human intervention.
- **Human-Computer Interactions (HCI)**
	- Human-computer interactions should be minimized and hidden.
- **Intelligence**
	- The network nodes should be intelligent
		- (i.e., artificial intelligence should be integrated)

### 6.3.2 - Internet of Things

- One of the biggest outcomes of ubiquitous or pervasive computing is the IoT. 
- IoT connects computers, like traditional internet, along with a wide variety of electronics.
- Over the years, the following have been introduced for IoT
	- several protocol standards
	- hardware platforms
	- other technologies

#### IoT Protocol Standards

- The **Internet Engineering Task Force** (IETF) formed the Constrained RESTful Environments (CORE) research group.
	- CORE develops protocol standards for constrained IP networks.
- A **constrained IP networks** includes nodes with:
	- limited memory size
	- low power
	- low throughput capacity
- Constrained IP networks may experience comparatively more packet loss and may include a large number of nodes (sensors and actuators) that may turn on or off periodically.
- IoT is an example of a constrained IP network.

Below are some IoT protocol standards.

### 6.3.3 - Constrained Application Protocol (CoAP)

- CoAP is a web transfer protocol designed for a wireless network with constrained nodes
	- low power, low memory, low data transfer rate.
- Nodes may have 8-bit microcontrollers and small ROM and RAM.
- CoAP operates on request/response architecture.
- It includes basic ideas of the web
	- e.g., unifrom resource identifiers (URIs) and media types
- CoAP is standardized in 7252, 7959, 8613, and 8974.

### 6.3.4 - IPv6 Over Low-Power Wireless Personal Area Networks (6LoWPAN)

- The **Low-Power Wireless Personal Area Network** (LoWPAN) comprises devices with:
	- low power
	- low computation speed
	- low memory
	- low bit rate
- Devices follow properties given in IEEE 802.15.4-2003.
- 6LoWPAN network assumptions, problem statements, and goals are standardized in RFC 4919.

### WebSocket

- **WebSockets** is aimed at supporting browser-based applications that required bidirectional communication with servers that do not depend on opening multiple HTTP connections.
- WebSockets utilizes existing concepts:
	- Proxies
	- filtering
	- authentication
- WebSockets operates over port 80 and 443 to use the HTTP proxies
- WebSocket is defined in RFC 6455.

### 6.3.5 - IoT Technologies

- The development of **system-on-chip** (SoC) technology introduced a few low-power, low cost, lightweight network nodes. 
	- They are being treated as the hardware platform of various IoT technologies. 
- Some of the popular IoT technologies and relevant hardware platforms include:
	- radio frequency identification (RFID)
	- Long Range (LoRa)

#### Radio Frequency Identification (RFID)

- **Transponders** are network devices that operate as both a transmitter and a responder.
- **Radio Frequency Identification** (RFID) system uses an electromagnetic field to identify or track objects and record data. 
- In RFDI setup there are
	- RFID tags (AKA transponders)
		- the tag is attached to the target object.
		- generally the tag is passive and powered by the radio wave released from the RFID reader, but some are powered by battery (active RFID tags). 
	- RFID readers
		- These are **transceivers**, containing a **radio frequency interface** (RFI) module and a wireless switch.

#### LoRa

- **LoRa** stands for long range.
	- It is a spread spectrum modulation technique for low-power wide area network (LPWAN) technology. 
- LoRa provides long-range communication using low-power network nodes. 
	- e.g.,
		- using LoRa makes it possible to communicate over a distance of 160 meters using 86.5 megajoules of energy.
- LoRa operates on lower industrial, scientific, and medical (ISM) band frequencies 
	- 868 megahertz (MHz) and 433 MHz for the EU
	- 915 MHz and 433 MHz for the US.
- LoRaWAN is a MAC layer protocol that operates on a network with star topology.

#### NodeMCU

- **NodeMCU** is an open-source firmware and development kit designed for building IoT products.
- it is based on **Espressif Non-OS SDK** for the ESP8266.
	- ESP8266 is a low-cost Wi-Fi chip with a full TCP/IP stack and microcontroller capabilities. 
	- It is developed by Espressif Systems, a Chinese manufacturer based in Shanghai. 

## Summary

p. 115;

- A distributed ledger technology (DLT) is a decentralized distributed network infrastructure in which a ledger (i.e., database) is deployed over multiple distributed machines with no central authority to maintain the database. 
	- DLT provides a platform for developing decentralized and distributed applications for registering, sharing, and synchronizing transactions on digital assets. 
	- These are key properties of DLT: 
		- decentralized, distributed, immutability, irreversibility, data consistency, data provenance, distributed consensus, accountability, and transparency.
	- There are two types of distributed ledger: 
		- public and private. 
	- Two data structures that prevent (?) DLT are blockchain and direct acyclic graph. 
	- DLT protocol stack contains the following layers: application, contract, consensus, network, data, and device. 
	- Some popular DLT platforms are Bitcoin, Ethereum, Multichain, and EOS.
- Mobile computing considers mobile computing nodes, such as user mobility, device mobility, network mobility, and host mobility. The IP of a mobile node is managed by implementing a home agent. Ad hoc on-demand distance vector (AODV), dynamic source routing protocol (DSR), and optimized link state routing protocol (OLSR) are some well-known routing protocols for mobile networks. One of the biggest outcomes of ubiquitous or pervasive computing is Internet of Things (IoT). Traditional internet connects computers, while the IoT also connects a wide variety of electronics, such as home appliances, handheld devices, sensors, switches, and actuators.
- Constrained application protocol (CoAP), constrained RESTful environments (CoRE), and IPv6 over low-power wireless personal area networks (6LoWPAN) are some well-known protocols for IoT. There are various hardware and software platforms for IoT. Some of the popular platforms are RFID, NodeMCU, and LoRa.
