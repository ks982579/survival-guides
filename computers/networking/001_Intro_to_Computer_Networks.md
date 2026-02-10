# 1. Computer Networks

## Study Goals

After completing this unit you should understand / be able to:
- Explain the concepts of computer networking, types of computer networks, network topologies, and interconnections.
- Understand the concepts of digital data transmission, communication engineering, and coding theory.
- Apply the concepts of physical layer mediums and data transmission methods.
- Estimate, analyze, and evaluate network performance. 

## Introduction

Examples of aspects of life moving towards dependency on computer networks:
- Education
- Healthcare
- Security
- Daily transactions
- Banking
- Entertainment
- Communication

And more!

There are various types of networks with different architectures, spatial scales, and organizational scopes and services. 

The fundamental task of a computer network is to transmit data from one device to another, a process known as **data communication**. 

**Data Communication** involves several steps:
- Converting analogue information into digital data;
- Data encoding;
- Compression;
- Encryption;
- Data-to-Signal conversion;
- Modulation;
- Signal transmission;
- Propagation.

The **Quality of Service** (QoS) of a computer network depends on the performance of data communication. This can be measured in terms of:
- Delay
- Throughput
- Bit-error rate

## 1.1 - Basic Concepts of Digital Data Transmission

**Computer Network**: a collection of communicating computing devices.
- communication done by transmitting digital data between sending and receiving devices through a series of intermediary connecting devices.
- Can be wired or wireless physical media.

A **Node** is a network device. A **Link** is the physical medium that nodes communicate on.

Nodes communicate through a series of steps. These mechanisms are standardized by governing bodies, known as protocols. This gives us the below 5 key components of digital data transmissions (Forouzan, 2013).

Here are the 5 key components of digital transmissions:
- 1.) Message
	- The **Message** is the data or information to be conveyed between the communicating devices.
- 2.) Sender
	- The sender is the device that transmits the message.
- 3.) Receiver 
	- The receiver is the device that receives the message.
- 4.) Link
	- The link is the physical medium of communication through which the message is conveyed from the sender to receiver.
- 5.) Protocols
	- Protocols are standardized mechanisms that assist the communication.

### Digital Data Transmission Steps

- A **Computer** is a digital device that stores data as a collection of binary numbers. 
- Communicating nodes _basically_ exchange a collection of zeros and ones. 
- Data _mostly_ propagate through the *link* in the form of electric or electromagnetic waves.
	- We call the electromagnetic waves **signals**. 
- Requires a mechanism to encode digital data into electromagnetic waveform, known as a **digital signal**. 
	- The mechanism is known as **line coding**, or **digital baseband modulation**. 

Know that different nodes are required to transmit the signal at different frequency based on the type of the physical media. 
- To do this, the digital signal is _modulated_ using an analogue signal with the desired frequency. 
- This signal is known as a **carrier**. 
- The device that performs modulation and demodulation is called the **modem**.
	- The word "modem" is short for "modulator-demodulator".
		- Applies to (e.g. Digital Subscriber Line (DSL) modem, or Cable Modem).
	- A **Digital Subscriber Line** (DSL) modem connects computers or routers with access to telephone lines to the broadband internet. 
	- A **Cable Modem** provides broadband internet access to a network node through cable TV connections.

I believe the magic is that they can send digital data at different frequencies across the same wire as your TV without causing interference.

The core idea here is that computers work with **digital data**, binary 1s and 0s. To send that data over a wire or through the air it needs to be converted into a **physical signal**. This is actual electrical voltages, light pulses, or radio waves. 

Digital Signals are like the electrical representation of 1s and 0s, a high voltage can represent a 1 and a low voltage can represent a 0. This is was **line coding** creates, a representation of discrete values. 

An **analog** signal is a smooth, continuously varying wave, like a sine wave. Think of it like a radio wave oscillating at a specific frequency. 

We need both because for the phoneline, that was designed for voice, analog audio frequencies. Cable TV lines use specific frequency ranges, and Fiber Optic uses light frequencies. 

For the phone line (DSL), you can't send raw digital pulses; but instead, take your digital signal and use it to **modulate** (modify) an analog carrier wave that operates at frequencies the phone line handles well. 

Physical media includes:
- Twister pair copper cables (CAT5, CAT6, etc.)
	- Ethernet over CAT typically uses direct digital signalling (line coding).
- Coaxial cable (cable TV)
	- Cable and DSL do use analog carrier modulation because the original infrastructure was designed for other purposes.
- Fiber optic cable
- Wireless (radio waves)

In **computer systems**, information must be presented *digitally*. **Source Coding** is a technique of converting analog information into digital data. 

Getting Physical - When a signal propagates through a physical medium it may experience:
- attenuation due to path loss;
- fading;
- transmission loss.

The signal can also become distorted due to:
- noise,
- interference
- multipath effect
- shadowing

The Impact! Attenuation and distortion can flip a zero to one or vice-versa - it flips the bit. This is known as a **bit-error**. Nodes that are communicating use **channel encoding** as an error detection and correction mechanism to find and fix bit errors. 

Sending nodes requires time to transmit data, the time is called **transmission delay**. It is proportional to the size of the data. 

The sender uses a mechanism called **source encoding** to *compress* the data before converting it into a signal. After *data compression*, the sending node must add "extra bits" along side the actual data bits called **header bits**. Let's do bullet points:
- Header Bits:
	- Contain the communicating parties' addresses.
- Data Bits:
	- Contain the content, or the "message".

A Network link can have multiple **channels**, i.e.) a physical medium can simultaneously carry transmissions from multiple senders. 

**Multiplexing** is a mechanism of combining transmissions from multiple sources. 

**Demultiplexing** is the process of separating multiple transmissions from a combined signal (Comer, 2015; Kurose & Keith, 2017). 

There is a diagram, "Figure 1: Digital Communication Steps" in the course book. 

Communication Steps:
- Sender 1
	- Message ->
	- Source encoder ->
	- Header bits, encryption ->
	- Channel Encoder ->
- Sender 2 ... Sender n
	- Multiplexer ->
	- Modulator Modem ->
	- Physical Medium ->
	- Demodulator Modem ->
	- Demultiplexer ->
- Receiver 2 ... Receiver n
- Receiver 1
	- Channel Decoder ->
	- Strip header bits, decryption ->
	- Source Decoder ->
	- Message (Yay)

### Digital Communication Performance

The **Quality of Service** (QoS) is the overall performance of a digital communication system or computer network. Depends largely on:
- transmission rate;
	- this is the number of bits per second a sender transmits or releases at the physical medium.
- delay;
	- Time to send a message from sender to receiver.
	- **Transmission Delay** is the time a sender takes to transmit or release a bit.
- channel capacity;
	- The maximum number of bits a link can carry per second. 
	- In general, the sender transmits data at a rate equal to the channel capacity.
- Link Utilization;
	- the ratio of the number of bits a link is currently carrying over the channel capacity. 
	- e.g.) if the *link capacity* is 2Mbps (megabits per second), and the sender is transmitting at 1Mbps, the link utilization is 50%. 
- throughput;
	- The number of bits per second successfully received by the receiver(s). 
	- e.g.) if channel capacity is 2Mbps, transmission rate is 1Mbps, the throughput is 1Mbps. 
	- Seems like whatever is the limiting factor.
- bit error rate (BER);
	- the ratio of the number of bit errors and the number of total transmitted bits. 
- And more!

> Knowledge Check

- Q1: What is the mechanism of combining transmissions from multiple sources?
- Q2: What is the process of separating multiple transmissions from a combined signal?

- A1: Multiplexing
- A2: Demultiplexing

## 1.2 - Network Topologies and Interconnections

Very important, before beginning construction, an engineer must plan the layout of the structure! 

A **network engineer** must make a layout of the network before deploying the network links and nodes (i.e. devices). This layout is known as **Network Topology**. 

Network Topology can be:
- Physical Topology
	- A physical mapping of the network.
	- Depicted locations of the network nodes are scaled according to physical measurements and properties of the network entities.
- Logical Topology
	- A logical mapping of the network that depicts how network nodes are connected to each other without considering actual physical locations of nodes. 

Physical topology is important for designing, deploying and analysing a specific network.

Logical topology is important for studying an analysing a *generic* network. 

### Network Topologies

**Network Topology** is a logical or physical depiction of how the network nodes (i.e., devices) are connected.

The simplest network topology contains only a sender and a receiver. 

Networks with the same resources may produce different quality of service (QoS) due to differences in topologies. 

Some well-know network topologies are:
- **Bus Topology**
	- All end nodes are connected to a common line or bus known as the **backbone**. 
- **Line Topology**
	- Nodes are connected in a serial manner. 
	- There are two end nodes, and each has only one connection. 
	- All other nodes have 2 connections.
- **Ring Topology**
	- Similar to a line topology.
	- Except that there are no end nodes in a ring topology.
- **Star Topology**
	- The point at which all end nodes are connected to a common connecting node.
	- Is it called a "topology"?
- **Mesh Topology**
	- Nodes are connected to each other in a random manner. 
	- **Fully Connected Mesh Network**
		- A mesh network where all nodes are connected to each other directly.
- **Tree Topology**
	- Combines the bus and star topologies.
	- Another name is the *star-bus topology*
- **Hybrid Topology**
	- Combination of other topologies.
	- Most common in practice for large networks.

The course book has an image of topologies.

Particular topologies can be useful for particular network based on the purpose of the network, QoS requirements, and resource availability. 

Dive a little deeper into each one...

#### Bus Topology

It has the simplest architecture. It requires only one bus (or cable) to connect all end nodes. 
- It does **not** require any connecting device or node. 
	- this mean installation cost is inexpensive.
- Installing additional devices (not "connecting" devices) is *comparatively* easy. 
- failure of a node does not hamper the connections between other nodes. 
- However, failure of the **backbone** will collapse the entire network. 
- Performance of nodes can be affected by the addition of more modes.

#### Line Topology

A network with **line topology** consisting of $n$ nodes requires $(n-1)$ links!
- Data may travel through multiple *repeaters*.
	- This is because nodes are connected through other nodes. 
	- Looking up wifi "repeaters" - they appear to be what you plug in to carry a network further. So devices connect to it and it connect to the original network hub or another repeater.
- Failure of a node breaks the network into two disconnected line networks. 
- Failure of an end node does not impact the connection between other nodes. 
	- probably just devices connected to that end.
- Installing new devices is not as easy as in the bus topology.

#### Ring Topology

Each node in the **ring topology** has two connections. A line topology can become a ring if you connect the end nodes together. Or, the failure of a node in a ring will turn it into a line topology.
- The number of nodes is equal to the number of links. 
- Like in the line - data may travel through multiple connecting nodes. 
- Ring top. allows data to travel bidirectionally.
	- Data can move in 2 directions, so if a single node is malfunctioning, other nodes can still be connected. 

#### Star Topology

Each pair of communicating end devices has two links between them. 
- First link connects the *sender* to the connecting device.
- Second link connects the connecting device to the receiver. 
- Failure of connecting central node hampers connection to all other nodes. 
	- breaks entire network.
- Network extension is *relatively* easier for Star top. compared to other tops.
- All nodes of 2 separate star networks can be brought together by connecting the central connecting devices. 
- A star network with $n$ end nodes requires $n$ connections or links.

#### Tree Topology

In a **Tree Topology** nodes are called **vertices**, links are called **edges**. 
- A tree network with $n$ nodes requires $(n-1)$ links. 
- Network expansion is considered easy in tree topology (like for star and bus).
- *Primary Disadvantage* = failure of parent node can create multiple disconnected networks.

#### Mesh Topology

In this topology, multiple paths exist between two nodes. Therefore, failure of a node does not break the connections between other nodes. 
- If there are $n$ nodes, then *fully connected* mesh network requires $n(n-1)/2$ links.
- Fully connected mesh network provides the highest fault tolerance. 
- Installation costs can be high for a large number of nodes $n$.

### Interconnections

Depending on the network type, a computer network can have a few devices (nodes) to a billion devices. Network nodes are categorized into 2 types:
- end node
- connecting node

Application programs run on end nodes such as:
- laptops
- mobile phones
- servers

When 2 end nodes communicate, this means the two application programs running on those two end nodes are communicating. 

Connecting nodes are not capable of running application programs. They are designed to connect to the end nodes within a network and can connect devices from two different networks. 

#### Network Types

Based on spatial size or coverage, networks are divided into **many** categories:
- **Body Area Network** (BAN) - nodes located on human body.
- **Personal Area Network** (PAN) - covers individuals' workplaces, typically a room.
- **Local Area Network** (LAN) - generally covers home or office.
- **Metropolitan Area Network** (MAN) - includes a city or metropolitan area.
- **Wide Area Network** (WAN) - Largest coverage, including global area. 
	- Most common example is the internet.

Based on service type, networks can be categorized into the following types:
- An **intranet** is a private network that serves network facilities within an organization.
- An **extranet** is an extension of the intranet. A limited number of authorized outsiders are allowed to access an organization's private network. 
	- Outsiders are usually partners, suppliers, vendors, or service providers.
- The **internet** is a global platform of interconnected networks. 
	- Nodes from different networks can also communicate through the internet!

#### Connecting Devices

A **connecting device** is a devices the connects two networks. A connecting device, such as a router, between two networks is also known as a gateway. This device would typically have multiple input and output ports. 

What does it do?
- It receives a *packet*, digital data.
- It transfers the packet to the relevant outgoing port to deliver to the desired receiver

Hence, sometimes known as "packet switches". I believe the actual process is more complicated. 

There are many types of connecting devices, some common ones:
- Repeater
	- Used to boost energy level of incoming signal.
- Bridge
	- A repeater with a filter for incoming packets.
- Hub
	- Allows multiple end nodes to be connected to a common network.
- Switch
	- Like a hub, it connects multiple devices with the capability of filtering incoming packets based on the media access control address
- Router
	- No definition provided.

### Delays

A *data packet* will experience a delay when traveling through a connecting device. Precise estimation of delay is important to design network parameters to ensure the desired QoS. There are four types of delays. 
- **Transmission Delay**
	- The time required by a node to transmit a data packet.
	- Given packet length $L$ and data transmission rate $R$, $T_{td} = L/R$. 
	- **n-hop** connection has $(n-1)$ connecting devices and $n$ links.
	- Transmission delay for **n-hop** connection is $T_{td} = nL/R$.
- **Propagation Delay**
	- When a packet is transmitted it *propagates* through the physical medium towards the receiver. The propagation delay is the time it takes to propagate and is proportional to the distance between the sender and receiver. 
	- Given distance $D$ and propagation speed $S$, $T_{pd} = D/S$. 
	- For a wireless medium the speed is equal to the speed of light.
- **Processing Delay**
	- After propagation the packet arrives at the incoming port of a connecting device and requires *processing* to forward it to the actual destination through the proper output port - the time this takes is known as **processing delay**. 
		- It is dependent on the processing speed and packet size. 
	- Given processing speed $P$ and packet size $L$, $T_{prd} = L/P$. 
- **Queuing Delay**
	- The packet will arrive at the connecting device and wait in a **buffer queue** until all prior packets have been processed. The wait time in the buffer queue is called the **queuing delay**.
		- I feel like the Queuing happens before the processing?
		- This is the most challenging delay to estimate!
	- Given packet arrival rate at the buffer $\lambda$ and the service rate $\mu$, $T_{qd} = 1 / (\mu - \lambda)$. 

And the total delay, unsurprisingly is:

$$
T = T_{td} + T_{pd} + T_{rpd} + T_{qd}
$$

## 1.3 - Basics of Communication Engineering and Coding Theory

p. 22

Computers are digital systems. In a computer network, data are stored, presented, and transmitted digitally. However, the transmitted data propagate as an **analog signal** through a physical media. 

We need to understand the properties of digital and analog signals to properly understand digital communication. 

[This article](https://www.bbc.co.uk/bitesize/guides/z8rxsbk/revision/3) about wave characteristics explains some nice terms:
- Crest of a wave is the highest point, so increases on the left and decreases to the right. 
- Trough is the lowest point of a wave, so decreasing on the left and increasing to the right. 
- The amplitude of a wave is the distance from the *centre line* (x-axis) to the top of a crest, or bottom of a trough. 
	- The greater the amplitude of a wave then the more energy it is carrying.
- The wavelength (usually $\lambda$) is the distance from any point of a wave to the same point on the next wave along.
	- Think like from crest to crest. 
- The frequency of a wave is the number of waves passing a point in a certain time. 
	- Usually measured in hertz ($Hz$), which is one wave per second. 
	- Frequency is not a distance travelled nor a speed or velocity. 

But what is a wave? It's something that carries energy from one place to another. There are sound waves, water waves, and all parts of the electromagnetic spectrum. 

### Types of Signals

A **signal** is a *function* that provides information about a physical *phenomenon*. 

In communication engineering, the *signal* is the time varying voltage, current or electromagnetic wave that conveys information. 

Generally, voltage $v$ is the dependent variable of independent variable time $t$. We will classify signals based on particular characteristics.
- **Continuous and Discrete Signals**
	- In a Continuous time signal, the independent variable time $t$ is measured continuously. 
	- In a Discrete time signal, the independent variable time $t$ is measured as a discrete value. 
- **Periodic and Aperiodic Signals**
	- In a periodic signal the *amplitude* will repeat after a certain period of time. 
- **Analog and Digital Signals**
	- In an analog signal the value of the dependent variable is continuous!
		- signal amplitude can be any real number.
	- In a digital signal, amplitude can be only fixed discrete values from a predefined set. 
		- Generally discrete in both time and amplitude.
- **Composite Signal, Modulating Signal, Carrier, and Modulated Signal**
	- A *composite signal* is formed by combining multiple sine waves. 
	- A *modulating signal* is a digital signal that represents the message or data to be transmitted.
		- It is combined with a **pure sinusoid** (i.e. sine wave) with the desired frequency to produce the modulate signal.
		- The **sinusoid** is called the **carrier signal**, or just "carrier".
- **Even and Odd Signals**
	- Signal $v(t)$ is an *even signal* if property $v(t) = v(-t)$ is true.
	- Signal $v(t)$ is an *odd signal* if property $v(t) = -v(-t)$ is true. 

### Coding Theory

Coding can be used in digital communication for purposes such as:
- data compression
- encryption
- error detection
- error correction
- analog to digital signal conversion
- data transmission

**Source coding** is the coding technique used to convert analog to digital signal. 

**Channel coding** is a technique by which redundant bits are added to the data bits in order to detect the correct bit errors. 

**Line coding** is a coding technique used for data transmission; that is, converting digital data to digital signal.

#### Source Coding

**Source coding** converts data, or a signal, to a bit stream. Simplest example is **pulse code modulation** (PCM). PCM converts an analog signal to a digital bit stream through the following 3 steps:
1. Sampling reads the analog signal amplitude periodically. The idea is to convert the continuous-time signal into a discrete-time signal.
2. Quantizing converts the sample values into integer numbers based on a predefined set of integer values. The idea is to convert the analog amplitude values into discrete or digital values.
3. Encoding represents quantized values into binary numbers. If the quantization has four levels, then the possible quantized value4s are zero, one, two, and three. The equivalnent binary values are 00, 01, 10, and 11. If there are $N$ quantization levels, then it would take $\lceil log_2(N) \rceil$ bits to represent a quantized value.

### Important Terminologies and Concepts

#### Bandwidth

In *digital communication*, the transmitted signal is a composite signal, which is made of multiple sinusoids. The frequency **bandwidth** is the range of frequencies of the sinusoids, starting from the lowest to the highest. 

The unit of frequency bandwidth is hertz ($Hz$). In computer networking, bandwidth is the capacity of  the transmission link to carry the maximum number of bits per second. Network bandwidth is also known as digital bandwidth.

#### Baseband and Passband Signals

The **baseband** is a type of transmission used in ethernet LANS. Wi-fi uses the **passband** transmission. 

baseband refers to the bandwidth of the tranmitted signal before it is modulated using a carrier (i.e. it is the bandwidth of the digital signal of the information signal). 

Passband is the bandwidth of the transmitted composite signal *after* analog modulation.

Page 25 has a nice image that solidifies bits and frequencies. When the amplitude is set to 1, that can be a 0 bit. And when the amplitude is like 5, that can be interpreted as a 1 bit. If these waves are energy, then the bits are instructions for low and high amounts of energy. 

#### Noise

**Noise** is an *unwanted* signal that interferes with the desired signal. It's an *indeterministic* signal, which means the amplitude of the noise is indeterministic for a given time. 

**Additive white Gausian Noise** (AWGN) is the simplest noise modeling for digital communication and follows the Gaussian distribution. White noise has equal intensity for all frequencies. 

#### Shannon-Hartley Theorem

According to the **Shannon-Hartley** theorem: if $B$ is the passband bandwidth, then the **channel capacity** $(C)$ in bits per second is:

$$
\begin{align}
C &= B \log_2 \lparen 1 + \frac{S}{N} \rparen \\
&= B \log_2 \lparen 1 + SNR \rparen
\end{align}
$$

Where $S$ is the signal power and $N$ is the noise power.

The term $SNR$ is known as the signal-to-noise ratio, usually expressed in decibels $dB$.

#### Nyquist Theorem 

The **Nyquist Theorem** indicates how frequently an analog signal should be sampled to convert it to a digital signal. According to it, the sampling rate must be at least twice the maximum frequency of the composite signal (Tanenbaum & Wetherall, 2014).

#### Transmission Modes

A **full-duplex** system supports simultaneous bidirectional data transmission.

A **half-duplex** system only supports unidirectional data transmission at any given time. 

And **Simple systems** support data transmission in one direction only.


## 1.4 - The Physical Layer: Transmission Methods and Media

p. 26

As we've said before, in digital systems, all data are presented using binary numbers. So, when 2 devices exchange data, they exchange a collection of 0s and 1s. 

Two communicating devices can be connected through a guided medium or an unguided medium, known as the physical layer. When data propagate through the physical layer, they propagate in the form of energy. 

The Quality of Service (QoS) of the network is directly impacted by the physical layer characteristics such as:
- Propagation speed
- Attenuation
- Noise

The QoS includes:
- Delay
- Jitter
- Bit Error Rate
- Channel Capacity
- Throughput

What doesn't it include? Error messages?

### Physical Layer Types

p. 26

When a packet is traveling from the sender to the receiver it may travel through various physical media. 

We have 2 categories of physical layer media:
- Guided
	- Primarily refers to twisted pair copper cable, coaxial cable, and optical fiber (multi-fiber optical cable).
- Unguided
	- Commonly includes *free space* where data propagates as electromagnetic waves of various ranges - such as:
		- radio wave
		- microwave
		- infrared

Installing guided media is generally less expensive than using unguided media. The book provides an image of different medias. 

On the electromagnetic spectrum...
- Radio
	- wavelength start (m): $10^3$
	- frequency start (Hz): $10^4$
- Microwave
	- wavelength start: $10^{-2}$
	- frequency start: $10^{8}$
- Infrared
	- wavelength start: $10^{-5}$
	- frequency start: $10^{12}$
- Visible
	- wavelength start: $0.5 \times 10^{-6}$
	- frequency start: $10^{15}$

#### Twisted Pair Cable

Made of isolated copper wires, so data are transmitted as electrical signal or voltage wave. One wire transmits the voltage wave and the other is used as a ground. 

The difference between the two wires represents data.

Copper wires can be affected by external noise sources such as heat or other electromagnetic waves. If the noise affects the wires unequally then the voltage difference of the wires can output incorrect data. This is at least one reason why the the wires are twisted together, so any noise will affect them more equally. 

The cables can be **shielded** or **unshielded**, so they can be covered with a metal layer to reduce electromagnetic noise. Shielded are commonly used for LAN. 

Generally, data rate varies from 100 megabits per second (Mbps) to 1 gigabit per second (Gbps) with a **bit error rate** (BER) of $10^{-7}$ to $10^{-9}$. 

A major downside is that these cables are relatively easy to *tap*. 

#### Coaxial Cable

The core of this cable is essentially an insulated copper wire that carries the signal. A metal foil is wrapped around the core to serve as the ground. It also serves as a metal sheath to protect from external noise. 

Coaxial cables provide comparatively higher frequency bandwidth but also higher attenuation. This requires repeaters to boost the signal energy for long distance communication. 

These are widely used by telephone, television, and internet connection providers. The data rate is up to 1 Gbps with a BER of $10^{-9}$. 

#### Optical Fiber

In this medium, data propagates as optical signals. The wire's structure is close to the coaxial cable but the inside is flexible glass instead of metal. The core is coated to give it a lower refractive index, directing light towards the core.

Optical fiber is *lightweight* and offers very low attenuation and BER within the range of $10^{-11}$ to $10^{-13}$. The data rate is also quite high, up to a few hundred Gbps. 

A bonus is that these cables are immune to electromagnetic noise and hard to *tap*. They are suitable for long-distance communication. This is why it is widely used as the backbone of the internet and telephone networks. 

A major drawback is that the cables are more fragile and can be damaged more easily. This requires more maintenance, and they are expensive to install. 

#### Radio Wave

p. 28

Primarily uses electromagnetic waves to transmit data ranging from 3kHz (kilohertz) to 300GHz (gigahertz). 

Waves in the range of 3kHz to 1Ghz frequencies are called **radio waves**. 

On key characteristic of radio waves is that they/it propagates through *wireless media* (i.e. free space, omnidirectional). 

A radio wave with low frequency (i.e., 3 kHz to 3 MHz (megahertz)) is known as a ground wave. This is because, due to the diffraction, its propagation follows the contour of the ground, or earth. 

**Diffraction** ([isaacscience.org](https://isaacscience.org/concepts/cp_diffraction)) is the spreading out of waves as they pass through an aperture or around objects. This happens when the size of the aperture or obstacle is the same order of magnitude as the wavelength of the incident wave. 
- For small aperture sizes, the majority of the wave is blocked.
- For large apertures, the wave passes by, or through, the obstacle without any *significant* diffraction. 

I think to sum up that term, I think of diffraction as how a wave interacts with an object. The object has properties that can change the wave. 

Radio waves within the 3 to 30 MHz range are called **skywave**. This is because it gets absorbed by the ground but gets refracted by the ionosphere and comes back to earth. This propagation mode is called **skip propagation**. 

The **Ionosphere** ([Wikipedia](https://en.wikipedia.org/wiki/Ionosphere)) is the ionized part of the upper atmosphere, or the Earth. It exists between 48 km to 965 km above sea level. It is ionized by solar radiation. 

Finally, the propagation mode of a radio wave with a high frequency, greater than 30 MHz, is called **line-of-sight communication** because any obstacle between the transmitter and receiver can highly attenuate or block the transmitted signal. 


#### Microwaves

These are electromagnetic waves within the frequency range of 1 GHz to 300 GHz. They also follow the *ling-of-sight* propagation, mentioned above. 

A collection of frequency ranges within microwave range are preserved for industrial, scientific, and medical (ISM) purposes. The most commonly used ISM band frequencies are 2.4 GHz and 5 GHz, also used for Wi-Fi.

Bluetooth and **near-field communication** (NFC) technologies also use ISM-band frequencies. 

The frequency range from 3 GHz to 300 GHz are called **millimeter waves** (mmWave) because the wavelengths varies from 10 mm to 1 mm. The mmWave *tends* to be absorbed by moisture and oxygen in the atmosphere, making it sutable for short-distance communication. 
- However, short-range communication significantly improves the frequency reuse.
- **Frequency Reuse** is a key concept in wireless communication.
	- Because the signals cannot travel far, we can use the same frequency channels, much closer together, without interference. 

#### Infrared

Frequency range of infrared waves varies from 300 GHz to 400 *terahertz* (THz). These waves cannot penetrate through walls, also making it suitable for secured short-range line-of-sight communication. 

A common example of infrared communication is a TV remote. 

### Contemporary Broadband Technologies

p. 29

The **digital subscriber line** (DSL) and cable connections are currently the two most popular wired broadband technologies.
- DLS
	- Allows for fast data transmission over a copper telephone line.
	- Has a wide range of variations
		- The *asymmetric digital subscriber line* (ADSL) is most widely used.
- Cable
	- Cable broadband allows for fast data over a coaxial copper TV cable.
		- **Fiber-to-the-home** (FTTH) is another broadband solution based on optical fiber. 
			- This has many variations, the collection of which is called "Fiber to the X" (FTTX). 
		- **Long-term Evolution** (LTE) is a wireless solution for broadband connection.
			- it allows for fast data transmission over cellular phone infrastructure using radio waves. 

Let's compare physical layer properties of different broadband connection solutions:
- DSL
	- Physical Layer: Twisted pair copper wire.
	- Downlink bitrate: ~ 256 Kbps - 100 Mbps with a max of 1 Gbps.
- Cable
	- Physical Layer: Coaxial cable.
	- Downlink bitrate: Up to 42.8 Mbps.
- LTE
	- Physical Layer: Radio wave 410-2495 MHz.
	- Downlink bitrate: Up to 100 Mbps.
- FTTH
	- Physical Layer: Optical fiber.
	- Downlink bitrate: Average 20 Mbps but up to 10 Gbps.


## Summary

p. 29

A **computer network** is a collection of communication devices connected through links, including copper cable, optical fiber, and electromagnetic waves, and connecting devices, such as routers, hubs, bridges, switches, and repeaters. It is a digital system where data are presented and exchanged in digital form. 

Converting a piece of analog information into digital data is done through **source coding** in three stages: *sampling*, *quantizing*, and *encoding*. 
- Encoding is the process of presenting data using binary bits which may involve compression and encryption techniques. 
- The process of converting digital data into signal is known as digital modulation or line coding. 

Combining a signal with a high-frequency carrier wave is known as modulation. This combined signal is a composite signal that is made of multiple sinusoids. The band-width of the data-bearing digital signal is called baseband, and the bandwidth of the composite signal is called passband. 

According to the **Nyquist theorem**, the sampling rate should be more than twice the signal bandwidth. While the signal propagates, it is affected by interfering signals or noise signals, which causes bit errors. The capacity of a noisy channel can be calculated using the Shannon-Hartley theorem. The quality of service of a network depends on various parameters such as bit-error rate, throughput, and delay. There are four main types of delays: propagation, transmission, queuing, and processing.
