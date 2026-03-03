---
layout: topic
title: "Data Transmission"
level: "AS Level"
level_url: "/as/"
unit_name: "Unit 1: Fundamentals of Computer Science"
unit_url: "/as/unit1/"
prev_topic: "/as/unit1/logical-operations/"
next_topic: "/as/unit1/data-representation/"
---

## Serial and Parallel Transmission (Advantages/Disadvantages)

Data transmission between devices can be classified by how many bits are sent at the same time.

### Serial Transmission

In **serial transmission**, data bits are sent **one at a time**, one after another, along a single data channel (wire or path).

- Bits arrive in sequence and must be reassembled at the destination
- Only one data wire is needed (plus ground and possibly control wires)
- Used for most modern external connections: USB, SATA, Ethernet, Thunderbolt

**Advantages of serial transmission:**
- Cheaper cables (fewer wires)
- Reliable over long distances -- no synchronisation issues between wires
- No crosstalk (electromagnetic interference between parallel wires)
- Simpler connectors and interfaces

**Disadvantages of serial transmission:**
- Slower than parallel for short distances (only one bit at a time)
- Data must be converted from parallel (internal bus) to serial for transmission, then back again (using a UART or similar)

### Parallel Transmission

In **parallel transmission**, multiple bits (typically 8, 16, 32, or 64) are sent **simultaneously** along multiple parallel data channels.

- Each bit travels on its own wire at the same time
- All bits must arrive simultaneously for the data to be valid
- Used for short-distance internal connections: CPU to memory via the system bus

**Advantages of parallel transmission:**
- Faster over short distances (multiple bits per clock cycle)
- Natural match for internal computer architecture (buses are parallel)

**Disadvantages of parallel transmission:**
- More expensive cables (more wires)
- Suffers from **data skew** over longer distances -- bits travelling on different wires arrive at slightly different times, causing errors
- Suffers from **crosstalk** -- electromagnetic interference between closely spaced wires
- Bulkier connectors

<div class="key-term" markdown="1">
**Data skew** occurs in parallel transmission when bits travelling on different wires arrive at slightly different times due to minor differences in wire length or electrical properties. This limits parallel transmission to short distances.
</div>

| Feature | Serial | Parallel |
|---|---|---|
| **Bits at a time** | 1 | Multiple (8, 16, 32, 64) |
| **Wires needed** | 1 data wire | Multiple data wires |
| **Cable cost** | Low | High |
| **Distance** | Long distances | Short distances only |
| **Speed (short distance)** | Lower | Higher |
| **Speed (long distance)** | Higher (no skew) | Unreliable (skew) |
| **Crosstalk** | Not an issue | Can be problematic |
| **Examples** | USB, SATA, Ethernet | Internal buses, old printer ports (LPT) |

<div class="exam-tip" markdown="1">
Modern high-speed serial connections (like USB 3.0 and SATA III) are actually faster than older parallel connections because they avoid skew and crosstalk problems. Do not assume parallel is always faster -- it depends on the distance and clock speed.
</div>

---

## Simplex, Half Duplex and Full Duplex Transmission

The **direction** in which data can flow between two devices is classified into three modes.

### Simplex

- Data flows in **one direction only**
- The sender can only send; the receiver can only receive
- No acknowledgement or response is possible in the reverse direction
- **Examples:** Television broadcast, keyboard to computer, fire alarm sensor to control panel

### Half Duplex

- Data can flow in **both directions**, but **not at the same time**
- When one device is transmitting, the other must wait before it can respond
- The channel switches direction as needed
- **Examples:** Walkie-talkie, CB radio, some Wi-Fi implementations

### Full Duplex

- Data can flow in **both directions simultaneously**
- Both devices can send and receive at the same time
- Requires either two separate channels or a single channel capable of carrying data in both directions at once
- **Examples:** Telephone call, modern Ethernet, video conferencing

| Mode | Direction | Simultaneous? | Example |
|---|---|---|---|
| **Simplex** | One way only | N/A | TV broadcast, keyboard |
| **Half duplex** | Both ways | No -- takes turns | Walkie-talkie |
| **Full duplex** | Both ways | Yes -- at the same time | Telephone, Ethernet |

<div class="key-term" markdown="1">
**Simplex** allows one-way communication only. **Half duplex** allows two-way communication but only one direction at a time. **Full duplex** allows simultaneous two-way communication.
</div>

<div class="exam-tip" markdown="1">
A common exam question asks you to identify the transmission mode for a given scenario. Always consider: can data go both ways? If yes, can it go both ways at the same time? This determines the answer.
</div>

---

## Need for Multiplexing and Switching

### Multiplexing

**Multiplexing** is the technique of combining multiple data signals into a single shared communication channel, then separating them at the receiving end. This is essential because building a separate physical link for every pair of communicating devices would be impractical and prohibitively expensive.

**Types of multiplexing:**

**Time Division Multiplexing (TDM):**
- The channel is divided into **time slots**
- Each data stream is allocated a fixed time slot in a repeating cycle
- Each sender takes turns transmitting during its assigned slot
- Like a round-robin where each person gets a fixed speaking time
- Used in digital telephone systems

**Frequency Division Multiplexing (FDM):**
- The available bandwidth of the channel is divided into **frequency bands**
- Each data stream is transmitted on a different frequency simultaneously
- Like multiple radio stations broadcasting on different frequencies
- Used in cable TV, FM radio, and ADSL broadband

| Feature | TDM | FDM |
|---|---|---|
| Division method | By time | By frequency |
| Transmission | Takes turns | Simultaneous on different frequencies |
| Use case | Digital telephony | Cable TV, radio |

<div class="key-term" markdown="1">
**Multiplexing** is the process of combining multiple signals over a single shared communication channel. A **multiplexer (MUX)** combines the signals at the sending end, and a **demultiplexer (DEMUX)** separates them at the receiving end.
</div>

### Switching

**Switching** is the mechanism by which data is directed from its source to its destination across a network. There are two main types:

**Circuit Switching:**
- A dedicated communication path is established between the sender and receiver **before** data transfer begins
- The path remains reserved for the entire duration of the communication, even during silences
- Provides a guaranteed, consistent connection with no contention
- Wasteful of bandwidth if the channel is not fully utilised
- **Example:** Traditional telephone network (PSTN)

**Packet Switching:**
- Data is broken into **packets** that are sent independently across the network
- Each packet may take a **different route** to the destination
- Packets are **reassembled** in the correct order at the destination
- More efficient use of bandwidth -- the network is shared between many users
- No dedicated path means packets may experience **variable delay** (jitter)
- **Example:** The Internet

| Feature | Circuit Switching | Packet Switching |
|---|---|---|
| Path | Dedicated, fixed | Dynamic, varies per packet |
| Setup | Connection established first | No setup required |
| Bandwidth use | Reserved (can be wasted) | Shared (efficient) |
| Delay | Consistent | Variable (jitter) |
| Reliability | High (dedicated path) | Packets may be lost/reordered |
| Example | Telephone call (PSTN) | Internet, email |

<div class="exam-tip" markdown="1">
Packet switching is the basis of the Internet. Exam questions often ask you to compare circuit and packet switching. Remember: circuit switching wastes bandwidth but gives consistent quality; packet switching is efficient but packets may arrive out of order or be lost.
</div>

---

## Communication Networks: Packet Contents Using TCP/IP

When data is transmitted across a TCP/IP network (such as the Internet), it is broken into **packets**. Each packet is a self-contained unit that carries part of the original data along with control information needed to deliver it correctly.

### Structure of a TCP/IP Packet

A packet consists of a **header**, a **payload** (data), and often a **trailer**.

**Packet Header** (added by TCP and IP layers):

| Field | Purpose |
|---|---|
| **Source IP address** | Identifies the sending device |
| **Destination IP address** | Identifies the intended recipient |
| **Source port number** | Identifies the application on the sending device |
| **Destination port number** | Identifies the application on the receiving device |
| **Sequence number** | Indicates the order of this packet within the original data stream |
| **Acknowledgement number** | Confirms which packets have been received (TCP) |
| **Packet length** | Total size of the packet |
| **Time To Live (TTL)** | Maximum number of hops (routers) the packet can pass through before being discarded; prevents packets circulating forever |
| **Protocol** | Identifies the transport protocol used (e.g., TCP or UDP) |
| **Checksum** | Used for error detection -- the receiver calculates its own checksum and compares it |
| **Flags** | Control bits such as SYN, ACK, FIN used in TCP handshaking |

**Payload:** The actual data being transmitted (a portion of the original file, message, or web page).

**Trailer:** Typically contains an error-checking value (e.g., CRC -- Cyclic Redundancy Check) to verify the integrity of the entire packet.

<div class="key-term" markdown="1">
A **packet** is a formatted unit of data containing a header (with addressing and control information), a payload (the actual data), and sometimes a trailer (for error checking). Packets are the fundamental unit of data transmission on TCP/IP networks.
</div>

### How Packets Are Processed

1. The application layer data (e.g., a web page) is passed to the transport layer
2. **TCP** breaks the data into segments, adds port numbers and sequence numbers
3. **IP** wraps each segment into a packet, adding source and destination IP addresses
4. The network access layer adds physical addressing (MAC addresses) and transmits the packet
5. At the destination, each layer strips its header and passes the data upward
6. TCP reassembles the segments in the correct order using sequence numbers

---

## Network Collision and Collision Detection

### What Is a Collision?

A **collision** occurs on a network when two or more devices attempt to transmit data on the same shared medium at the same time. The signals interfere with each other and both transmissions are corrupted. Collisions are particularly common on shared media networks such as bus topology networks and wireless networks.

### CSMA/CD (Carrier Sense Multiple Access with Collision Detection)

**CSMA/CD** is the protocol used on wired Ethernet networks to handle collisions:

1. **Carrier Sense:** Before transmitting, a device **listens** to the network to check if the medium is free (no other device is currently transmitting).
2. **Multiple Access:** Multiple devices share the same medium and any device may transmit when the medium is clear.
3. **Transmit:** If the medium is free, the device begins transmitting.
4. **Collision Detection:** While transmitting, the device continues to listen. If it detects a collision (the signal on the wire does not match what it sent), it stops immediately.
5. **Jam Signal:** The device sends a short **jam signal** to notify all other devices that a collision has occurred.
6. **Random Backoff:** Each device involved in the collision waits a **random amount of time** before attempting to retransmit. The random wait reduces the chance of another collision.
7. **Retry:** After the wait period, the device goes back to step 1 and tries again.

### CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)

**CSMA/CA** is used on wireless networks (Wi-Fi) where collision detection is not practical because a wireless device cannot transmit and listen at the same time.

1. **Carrier Sense:** The device listens to check if the medium is free.
2. **Wait:** If the medium is busy, the device waits until it becomes free, then waits an additional random backoff time.
3. **RTS/CTS (optional):** The device may send a **Request To Send (RTS)** signal. The access point responds with a **Clear To Send (CTS)** signal, reserving the medium.
4. **Transmit:** The device transmits the data.
5. **Acknowledgement:** The receiver sends an **ACK**. If the sender does not receive an ACK, it assumes a collision occurred and retries after a random backoff.

| Feature | CSMA/CD | CSMA/CA |
|---|---|---|
| Used on | Wired Ethernet | Wireless (Wi-Fi) |
| Collision handling | Detects collisions during transmission | Avoids collisions before transmission |
| Detection method | Compares sent signal to wire signal | Not possible wirelessly |
| Recovery | Jam signal + random backoff | Timeout + random backoff |
| Optional mechanism | N/A | RTS/CTS handshake |

<div class="key-term" markdown="1">
A **collision** occurs when two devices transmit data simultaneously on a shared medium, causing the signals to interfere. **CSMA/CD** detects collisions on wired networks. **CSMA/CA** avoids collisions on wireless networks.
</div>

<div class="exam-tip" markdown="1">
Remember the difference: CSMA/**CD** is for wired networks and **detects** collisions. CSMA/**CA** is for wireless networks and tries to **avoid** them. Wireless devices cannot detect collisions because they cannot transmit and receive simultaneously.
</div>

---

## Methods of Routing Traffic on a Network

**Routing** is the process of selecting the best path for data packets to travel from source to destination across a network. Routers examine the destination IP address in each packet and decide where to forward it.

### How Routers Work

1. A router receives an incoming packet and examines the **destination IP address** in the packet header.
2. It consults its **routing table** -- a database mapping destination network addresses to the best outgoing interface/next hop.
3. The router forwards the packet to the next router (hop) along the best path.
4. This process repeats at each router until the packet reaches its destination network.
5. The **TTL (Time To Live)** field is decremented by 1 at each hop. If it reaches 0, the packet is discarded to prevent infinite loops.

### Routing Tables

A **routing table** contains:

| Field | Description |
|---|---|
| **Destination network** | The network address being routed to |
| **Subnet mask** | Defines which part of the IP address is the network portion |
| **Next hop** | The IP address of the next router to forward the packet to |
| **Interface** | The physical or logical port to send the packet out of |
| **Metric/Cost** | A value indicating the "cost" of the route (e.g., hop count, bandwidth, delay) |

### Static vs Dynamic Routing

**Static routing:**
- Routes are manually configured by a network administrator
- Do not change automatically in response to network conditions
- Simple and predictable, but inflexible
- Suitable for small, stable networks

**Dynamic routing:**
- Routes are calculated automatically by routing protocols
- Routers exchange information about network topology and adjust routes in response to changes (e.g., link failures, congestion)
- More complex but highly adaptable
- Suitable for large, changing networks like the Internet

### Common Routing Algorithms

**Distance Vector Routing:**
- Each router maintains a table of the distance (hop count) to every known destination
- Routers periodically share their tables with their neighbours
- Each router updates its table if a neighbour advertises a shorter route
- Simple but slow to converge (adapt to changes)
- **Example protocol:** RIP (Routing Information Protocol)

**Link State Routing:**
- Each router builds a complete map of the network topology
- Every router knows the entire network structure and calculates the shortest path to each destination
- Uses algorithms like Dijkstra's shortest path algorithm
- Converges faster and scales better than distance vector
- **Example protocol:** OSPF (Open Shortest Path First)

<div class="key-term" markdown="1">
**Routing** is the process of selecting the optimal path for packets across a network. Routers use **routing tables** to determine the next hop for each packet based on its destination IP address.
</div>

<div class="exam-tip" markdown="1">
Know the difference between **static** (manually configured, suitable for small networks) and **dynamic** (automatically adapting, suitable for large networks) routing. Also understand that each packet can take a different route through the network -- this is a key feature of packet switching.
</div>
