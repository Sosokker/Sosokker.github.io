---
title: Network Modeling
---

----

## Protocol Suites and Layering Models

We need *complete* and *efficient* result from **communications system** so a set of protocols must be constructed carefully.

Each protocol should *handle a part* of communication *not handled by other protocols*.

We will design protocols in *suites* or *families*: the complete, cooperative sets instead of creating each one in isolation. This make sure that protocols can work together.
## Layering Model

**Layering Model** is *fundamental abstraction* used to collect protocols into *unified whole*. 

It show us how can all *aspects* of a *communication problem* can be *partitioned* into pieces that *work together*. 

Each piece is **Layer**

----

## TCP/IP Example

TCP/IP is one of the suite where TCP is The Transmission Control protocol and IP is The Network Protocol

TCP/IP in fact consists of dozens of different protocols, but only a few are the “main” protocols

The _Internet Protocol (IP)_ is the primary OSI network layer (layer three) protocol that provides addressing, datagram routing and other functions in an internetwork. The _Transmission Control Protocol (TCP)_ is the primary transport layer (layer four) protocol, and is responsible for connection establishment and management and reliable data transport between software processes on devices.


### [[Overview of Data communication|Layer 1: Physical]]
Protocols in **Physical** Layer specify about *transmission medium and associated hardware* 

- Electrical properties
- Radio Frequencies
- Signals
### Layer 2: Network Interface or MAC
Protocols in **Network Interface** layer specify about *communication over a single network* and *the interface between network hardware and Layer 3* 

- Network addresses
- Maximum packet size that network can support
- Protocols used to access medium and hardware addressing

### Layer 3: Internet
Protocols in **Internet** Layer specify *communication between two computer across Internet* (Across interconnected networks)

- Internet addressing structure
- Format of Internet packets
- The method for dividing large packet into smaller packets for transmission
- Mechanism for reporting errors.

### Layer 4: Transport
Protocols in **Transport** Layer provide for *communication from an application program on one computer to an application program on another*

- Maximum rate receiver can accept data
- Mechanisms to avoid network congestion(crowded traffic)
- Technique to ensure that all data received in the correct order.

### Layer 5: Application
Protocols in the **Application** Later, top Layer of the TCP/IP specify *how a pair of application interact when they communicate*.

Specify details about the *format and meaning of messages* that *applications can exchange* 

and *procedures to be followed during communication*.

- When a programmer *builds an application that communicates across a network*, the programmer *design* a layer 5 protocol

----
## How data passes through each layer
![[Layering.png| 500]]
Let sends data from one application to others.

1. Send data
	1. Data is placed in packet
2. Packet passes down to each layer of protocols
	1. Pass through all Layer in sending computer.
	2. Leave sending computer
3. Transmitted across the underlying physical network
4. Reach receiving computer
5. Packet passes up through layers of protocols.

If the application on the *receiving computer sends a response*, then the process is *reversed*.
