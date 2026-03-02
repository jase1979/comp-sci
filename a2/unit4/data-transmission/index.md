---
layout: topic
title: "Data Transmission"
level: "A2"
level_url: "/a2/"
unit_name: "Unit 4: Architecture, Data, Communication & Applications"
unit_url: "/a2/unit4/"
---

## Calculate Data Transfer Rates on a Network

### Routing Cost Formula

The cost of transmitting data along a network link is calculated as:

```
Link cost = 1 Mbps ÷ Transmission speed of the link
```

A **lower cost** means a **faster** (and therefore cheaper) link. A higher-speed link has a lower cost because data travels more quickly.

### Unit Conversions

| Unit | Equivalent |
|------|-----------|
| 1 byte | 8 bits |
| 1 Kbps (kilobits per second) | 1,000 bps |
| 1 Mbps (megabits per second) | 1,000 Kbps = 1,000,000 bps |
| 1 Gbps (gigabits per second) | 1,000 Mbps |
| 1 KB (kilobyte) | 1,000 bytes = 8,000 bits |
| 1 MB (megabyte) | 1,000 KB = 8,000,000 bits |

<div class="exam-tip" markdown="1">
Pay close attention to the units in exam questions. **Mbps** is mega**bits** per second. **MBps** is mega**bytes** per second. To convert MBps to Mbps, multiply by 8. Always check which unit the question uses.
</div>

### Worked Example 1 — Link Cost

A network link has a transmission speed of 100 Mbps. Calculate its cost.

```
Cost = 1 Mbps ÷ 100 Mbps = 0.01
```

### Worked Example 2 — Comparing Links

| Link | Speed | Cost |
|------|-------|------|
| A → B | 10 Mbps | 1 ÷ 10 = **0.1** |
| A → C | 100 Mbps | 1 ÷ 100 = **0.01** |
| B → D | 50 Mbps | 1 ÷ 50 = **0.02** |
| C → D | 20 Mbps | 1 ÷ 20 = **0.05** |

---

## Calculate Lowest Cost Routes on a Network

To find the **lowest cost route** between two nodes, add up the costs of all links on each possible path and choose the path with the **smallest total cost**.

### Worked Example — Simple Routing

Using the link costs above, find the lowest cost route from A to D:

**Route 1:** A → B → D = 0.1 + 0.02 = **0.12**

**Route 2:** A → C → D = 0.01 + 0.05 = **0.06**

**Lowest cost route:** A → C → D (cost = 0.06)

This makes sense — the route through C uses faster links overall.

### Worked Example — Larger Network

Consider a network with nodes A, B, C, D, E:

| Link | Speed (Mbps) | Cost |
|------|-------------|------|
| A → B | 100 | 0.01 |
| A → C | 50 | 0.02 |
| B → D | 20 | 0.05 |
| B → E | 200 | 0.005 |
| C → D | 100 | 0.01 |
| D → E | 50 | 0.02 |

**Find the lowest cost route from A to E:**

| Route | Links | Total Cost |
|-------|-------|------------|
| A → B → E | 0.01 + 0.005 | **0.015** |
| A → B → D → E | 0.01 + 0.05 + 0.02 | 0.08 |
| A → C → D → E | 0.02 + 0.01 + 0.02 | 0.05 |

**Lowest cost route:** A → B → E (cost = 0.015)

---

### Routing with Delay Factors

In real networks, links may experience **delays** due to congestion, distance, or equipment. A **delay factor** is a multiplier applied to the base cost.

```
Adjusted link cost = Base cost × Delay factor
```

A delay factor of 1.0 means no delay. A factor greater than 1.0 increases the effective cost.

### Worked Example — Delay Factors

Using the same network, but now with delay factors:

| Link | Base Cost | Delay Factor | Adjusted Cost |
|------|-----------|-------------|---------------|
| A → B | 0.01 | 3.0 | 0.01 × 3.0 = **0.03** |
| A → C | 0.02 | 1.0 | 0.02 × 1.0 = **0.02** |
| B → E | 0.005 | 5.0 | 0.005 × 5.0 = **0.025** |
| C → D | 0.01 | 1.5 | 0.01 × 1.5 = **0.015** |
| D → E | 0.02 | 1.0 | 0.02 × 1.0 = **0.02** |

**Find the lowest cost route from A to E (with delays):**

| Route | Adjusted Costs | Total |
|-------|---------------|-------|
| A → B → E | 0.03 + 0.025 | **0.055** |
| A → C → D → E | 0.02 + 0.015 + 0.02 | **0.055** |

Both routes have equal adjusted cost (0.055). Either could be chosen — in practice, a router might use additional criteria (e.g. hop count, reliability) to break the tie.

<div class="exam-tip" markdown="1">
Always show your working clearly in routing questions. State the formula, calculate each link cost, sum them for each route, and clearly identify the lowest. If delay factors are given, multiply **before** summing. Common errors include forgetting to apply the delay factor or confusing bits and bytes.
</div>

---

## The Internet as a World-Wide Communications Infrastructure

### What is the Internet?

The Internet is a **global network of interconnected networks** that uses a standardised set of protocols (TCP/IP) to enable communication between billions of devices worldwide.

<div class="key-term" markdown="1">
The **Internet** is a worldwide collection of interconnected computer networks that communicate using the TCP/IP protocol suite. It is not a single network but a **network of networks**.
</div>

### Key Characteristics

| Characteristic | Description |
|---------------|-------------|
| **Decentralised** | No single authority controls the entire Internet |
| **Packet-switched** | Data is broken into packets that travel independently |
| **Fault-tolerant** | If one route fails, packets can take alternative paths |
| **Scalable** | New networks and devices can be added easily |
| **Open standards** | Uses publicly available protocols (TCP/IP, HTTP, etc.) |

### The Three-Tier Structure

The Internet is organised into three tiers of Internet Service Providers (ISPs):

| Tier | Role | Examples |
|------|------|---------|
| **Tier 1** | Global backbone providers. Own and operate major long-distance fibre-optic links that span continents. Peer with other Tier 1 providers (exchange traffic at no cost). | BT, AT&T, NTT, Lumen |
| **Tier 2** | Regional ISPs. Purchase **transit** from Tier 1 providers and sell connectivity to Tier 3. May also peer with other Tier 2 providers. | Sky, Virgin Media, regional carriers |
| **Tier 3** | Local ISPs. Purchase connectivity from Tier 2 providers and sell directly to **end users** (homes and businesses). | Local broadband providers, mobile operators |

**How tiers connect:**
- **Peering** — two networks of similar size agree to exchange traffic directly, usually at no cost. Common between Tier 1 providers.
- **Transit** — a smaller network pays a larger network to carry its traffic to the rest of the Internet. Tier 3 pays Tier 2, Tier 2 pays Tier 1.
- **Internet Exchange Points (IXPs)** — physical locations where multiple ISPs connect their networks to exchange traffic efficiently.

---

## Protocols and Standards

### TCP/IP Protocol Suite

The **TCP/IP model** is the standard framework for Internet communication, organised into four layers:

| Layer | Name | Protocols | Function |
|-------|------|-----------|----------|
| 4 | **Application** | HTTP, HTTPS, FTP, SMTP, DNS | Provides services directly to the user (web, email, file transfer) |
| 3 | **Transport** | TCP, UDP | Ensures reliable delivery (TCP) or fast delivery (UDP). Manages port numbers. |
| 2 | **Internet** | IP, ICMP | Handles addressing and routing. IP addresses identify source and destination. |
| 1 | **Network Access** | Ethernet, Wi-Fi | Handles physical transmission of data over the network medium |

### Key Protocols

| Protocol | Full Name | Purpose |
|----------|-----------|---------|
| **HTTP/HTTPS** | HyperText Transfer Protocol (Secure) | Transfers web pages between browser and server. HTTPS encrypts the connection using TLS/SSL. |
| **FTP** | File Transfer Protocol | Transfers files between computers. Supports upload and download. |
| **SMTP** | Simple Mail Transfer Protocol | Sends emails from client to server and between servers |
| **POP3** | Post Office Protocol v3 | Downloads emails from server to client (removes from server) |
| **IMAP** | Internet Message Access Protocol | Accesses emails on the server without downloading (syncs across devices) |
| **DNS** | Domain Name System | Translates domain names (e.g. `www.example.com`) into IP addresses (e.g. `93.184.216.34`) |
| **TCP** | Transmission Control Protocol | Reliable, connection-oriented data transfer with error checking and retransmission |
| **UDP** | User Datagram Protocol | Fast, connectionless transfer without guaranteed delivery (used for streaming, gaming) |
| **IP** | Internet Protocol | Addresses and routes packets across networks |

### DNS Resolution Process

When you type a URL into a browser:

1. Browser checks its **local cache** for the IP address
2. If not cached, the OS checks the **hosts file**
3. If not found, a request is sent to the **local DNS resolver** (usually provided by your ISP)
4. The resolver checks its cache; if not found, it queries a **root DNS server**
5. The root server directs the resolver to the appropriate **Top-Level Domain (TLD) server** (e.g. `.com`, `.co.uk`)
6. The TLD server directs the resolver to the **authoritative DNS server** for the specific domain
7. The authoritative server returns the **IP address**
8. The resolver caches the result and returns it to the browser
9. The browser connects to the web server using the IP address

---

## Why Standards Matter

### The Importance of Standards

- **Interoperability** — devices and software from different manufacturers can communicate because they all follow the same standards
- **Competition** — standards prevent vendor lock-in and allow multiple companies to compete, driving innovation and lowering prices
- **Reliability** — standardised protocols have been extensively tested and are well-understood
- **Global reach** — the Internet works worldwide because all connected networks use TCP/IP

### Challenges in Developing Standards

- **Competing interests** — different companies may want standards that favour their products
- **Speed of change** — technology evolves faster than standards bodies can work (e.g. the long development of HTML5)
- **Legacy compatibility** — new standards must often maintain backward compatibility with older systems
- **Global agreement** — standards must work across different countries, languages, and legal frameworks

---

## Internet Services

| Service | Description | Protocols Used |
|---------|-------------|---------------|
| **World Wide Web (WWW)** | System of interlinked hypertext documents accessed via web browsers | HTTP/HTTPS, HTML, CSS, JavaScript |
| **Email** | Electronic messaging between users | SMTP (sending), POP3/IMAP (receiving) |
| **VoIP** | Voice over IP — telephone calls over the Internet | SIP, RTP, UDP |
| **Cloud computing** | On-demand access to computing resources (storage, processing, software) over the Internet | HTTPS, various APIs |
| **Streaming** | Real-time delivery of audio/video content without downloading first | HTTP (adaptive streaming), UDP (live) |
| **File sharing** | Transfer of files between users or systems | FTP, BitTorrent, HTTP |
| **Instant messaging** | Real-time text communication | XMPP, proprietary protocols |

<div class="exam-tip" markdown="1">
Questions about the Internet often ask you to explain the difference between the **Internet** (the global network infrastructure) and the **World Wide Web** (a service that runs on the Internet, using HTTP to deliver web pages). The Internet existed before the Web and supports many other services (email, VoIP, streaming, etc.).
</div>
