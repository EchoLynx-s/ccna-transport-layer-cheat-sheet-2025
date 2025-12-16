# CCNA – Transport Layer (Module 14)

Quick-reference notes for NetAcad CCNA – **Module 14: Transport Layer**.  
Focus is on how the transport layer (TCP & UDP) moves data between applications:
ports, reliability, flow control, and connection setup/teardown.

I use this repo to revise:

- The **role of the transport layer** in the TCP/IP and OSI models.
- Differences between **TCP and UDP** (reliability, overhead, use cases).
- The structure and fields of **TCP and UDP headers**.
- How **port numbers, sockets and socket pairs** identify conversations.
- How **TCP connections** are established/terminated (3-way handshake, FIN).
- How TCP implements **reliability and flow control** (seq/ack, windows, MSS).
- How **UDP** handles communication with minimal overhead.
- Typical **applications** that use TCP vs UDP and why.

---

## Table of Contents

- [Module 14 Overview](#module-14-overview)  
- [Module Map](#module-map)  

- [14.0 Introduction](#140-introduction)  
  - [14.0.1 Why should I take this module?](#1401-why-should-i-take-this-module)  
  - [14.0.2 What will I learn to do in this module?](#1402-what-will-i-learn-to-do-in-this-module)  

- [14.1 Transportation of Data](#141-transportation-of-data)  
  - [14.1.1 Role of the Transport Layer](#1411-role-of-the-transport-layer)  
  - [14.1.2 Transport Layer Responsibilities](#1412-transport-layer-responsibilities)  
  - [14.1.3 Transport Layer Protocols](#1413-transport-layer-protocols)  
  - [14.1.4 Transmission Control Protocol (TCP)](#1414-transmission-control-protocol-tcp)  
  - [14.1.5 User Datagram Protocol (UDP)](#1415-user-datagram-protocol-udp)  
  - [14.1.6 The Right Transport Layer Protocol for the Right Application](#1416-the-right-transport-layer-protocol-for-the-right-application)  
  - [14.1.7 Check Your Understanding – Transportation of Data](#1417-check-your-understanding--transportation-of-data)  

- [14.2 TCP Overview](#142-tcp-overview)  
  - [14.2.1 TCP Features](#1421-tcp-features)  
  - [14.2.2 TCP Header](#1422-tcp-header)  
  - [14.2.3 TCP Header Fields](#1423-tcp-header-fields)  
  - [14.2.4 Applications that use TCP](#1424-applications-that-use-tcp)  
  - [14.2.5 Check Your Understanding – TCP Overview](#1425-check-your-understanding--tcp-overview)  

- [14.3 UDP Overview](#143-udp-overview)  
  - [14.3.1 UDP Features](#1431-udp-features)  
  - [14.3.2 UDP Header](#1432-udp-header)  
  - [14.3.3 UDP Header Fields](#1433-udp-header-fields)  
  - [14.3.4 Applications that use UDP](#1434-applications-that-use-udp)  
  - [14.3.5 Check Your Understanding – UDP Overview](#1435-check-your-understanding--udp-overview)  

- [14.4 Port Numbers](#144-port-numbers)  
  - [14.4.1 Multiple Separate Communications](#1441-multiple-separate-communications)  
  - [14.4.2 Socket Pairs](#1442-socket-pairs)  
  - [14.4.3 Port Number Groups](#1443-port-number-groups)  
  - [14.4.4 The netstat Command](#1444-the-netstat-command)  
  - [14.4.5 Check Your Understanding – Port Numbers](#1445-check-your-understanding--port-numbers)  

- [14.5 TCP Communication Process](#145-tcp-communication-process)  
  - [14.5.1 TCP Server Processes](#1451-tcp-server-processes)  
  - [14.5.2 TCP Connection Establishment](#1452-tcp-connection-establishment)  
  - [14.5.3 Session Termination](#1453-session-termination)  
  - [14.5.4 TCP Three-way Handshake Analysis](#1454-tcp-three-way-handshake-analysis)  
  - [14.5.5 Video – TCP 3-Way Handshake](#1455-video--tcp-3-way-handshake)  
  - [14.5.6 Check Your Understanding – TCP Communication Process](#1456-check-your-understanding--tcp-communication-process)  

- [14.6 Reliability and Flow Control](#146-reliability-and-flow-control)  
  - [14.6.1 TCP Reliability – Guaranteed and Ordered Delivery](#1461-tcp-reliability--guaranteed-and-ordered-delivery)  
  - [14.6.2 Video – TCP Reliability – Sequence Numbers and Acknowledgments](#1462-video--tcp-reliability--sequence-numbers-and-acknowledgments)  
  - [14.6.3 TCP Reliability – Data Loss and Retransmission](#1463-tcp-reliability--data-loss-and-retransmission)  
  - [14.6.4 Video – TCP Reliability – Data Loss and Retransmission](#1464-video--tcp-reliability--data-loss-and-retransmission)  
  - [14.6.5 TCP Flow Control – Window Size and Acknowledgments](#1465-tcp-flow-control--window-size-and-acknowledgments)  
  - [14.6.6 TCP Flow Control – Maximum Segment Size (MSS)](#1466-tcp-flow-control--maximum-segment-size-mss)  
  - [14.6.7 TCP Flow Control – Congestion Avoidance](#1467-tcp-flow-control--congestion-avoidance)  
  - [14.6.8 Check Your Understanding – Reliability and Flow Control](#1468-check-your-understanding--reliability-and-flow-control)  

- [14.7 UDP Communication](#147-udp-communication)  
  - [14.7.1 UDP Low Overhead versus Reliability](#1471-udp-low-overhead-versus-reliability)  
  - [14.7.2 UDP Datagram Reassembly](#1472-udp-datagram-reassembly)  
  - [14.7.3 UDP Server Processes and Requests](#1473-udp-server-processes-and-requests)  
  - [14.7.4 UDP Client Processes](#1474-udp-client-processes)  
  - [14.7.5 Check Your Understanding – UDP Communication](#1475-check-your-understanding--udp-communication)  

- [14.8 Module Practice and Quiz](#148-module-practice-and-quiz)  
  - [14.8.1 Packet Tracer – TCP and UDP Communications](#1481-packet-tracer--tcp-and-udp-communications)  
  - [14.8.2 What did I learn in this module?](#1482-what-did-i-learn-in-this-module)  
  - [14.8.3 Module Quiz – Transport Layer](#1483-module-quiz--transport-layer)  

- [How to talk about this module to a recruiter](#how-to-talk-about-this-module-to-a-recruiter)  

---

## Module 14 Overview

> **Goal:** Understand how the transport layer (TCP/UDP) provides end-to-end
> communication between applications, and be able to choose, configure and
> troubleshoot the **right transport protocol** for each use case.

---

## Module Map

| Topic                         | Focus                                                                 |
|-------------------------------|-----------------------------------------------------------------------|
| 14.1 Transportation of Data   | Role of Layer 4, responsibilities, TCP vs UDP                        |
| 14.2 TCP Overview             | TCP features, header fields, and common TCP applications             |
| 14.3 UDP Overview             | UDP features, header fields, and common UDP applications             |
| 14.4 Port Numbers             | Concurrent sessions, sockets, port ranges, `netstat`                 |
| 14.5 TCP Communication Process| Server processes, 3-way handshake, session teardown                  |
| 14.6 Reliability and Flow     | Sequence numbers, ACKs, retransmission, windows, congestion control  |
| 14.7 UDP Communication        | Lightweight delivery, reassembly and server/client behaviour         |
| 14.8 Practice and Quiz        | TCP/UDP Packet Tracer activity and module review                     |

---

## 14.0 Introduction

### 14.0.1 Why should I take this module?

**Story version**

- Think of the transport layer as the **postal service of the network stack**.  
  IP gets packets from address A to B, but the transport layer decides:
  - *Which* application at B should get the data.
  - Whether we need **reliable, ordered delivery** (TCP) or **fast, best-effort** (UDP).
- Most real-world issues users feel – *“my website is slow”, “my video keeps buffering”* –
  are actually **transport-layer problems** (congestion, retransmissions, wrong ports, etc.).

**Exam view – remember**

- Transport layer = **Layer 4** of the OSI model, above IP.
- Provides **logical communication between processes**, not just hosts.
- Two main protocols in TCP/IP suite:
  - **TCP – Transmission Control Protocol** (reliable, connection-oriented).
  - **UDP – User Datagram Protocol** (unreliable, connectionless, low overhead).

---

### 14.0.2 What will I learn to do in this module?

After this module you should be able to:

- Explain the **purpose of the transport layer** and where it fits in TCP/IP and OSI.
- Compare **TCP vs UDP** and pick the right one for different applications.
- Read, draw and mentally decode **TCP and UDP headers**.
- Explain how **port numbers and sockets** identify specific conversations.
- Walk through TCP’s **3-way handshake** and **connection termination** in detail.
- Describe how TCP provides **reliability, ordered delivery and flow control**.
- Explain how UDP supports **simple, fast** application traffic.
- Use **Packet Tracer** and commands like `netstat` to see real transport-layer behaviour.

---

# CCNA – Module 14.1 Transportation of Data (Transport Layer)

Quick-reference notes for **NetAcad CCNA – Module 14.1: Transportation of Data**.  
Focus: what the **transport layer (TCP/UDP)** actually does, how it supports multiple
conversations, and when to choose **TCP vs UDP**.

I use this file to revise:

- The **role and responsibilities** of the transport layer.
- Differences between **TCP** and **UDP** in design, features and use cases.
- How real applications map to TCP/UDP and ports.
- Typical **exam traps** and how to explain this topic to a **recruiter / interviewer**.

---

## 14.1.1 Role of the Transport Layer

**In one sentence:**  
The transport layer moves data between **applications** on different hosts and hides
the network details from them.

### Key points for study

- Sits between **application layer** (HTTP, DNS, etc.) and **network layer** (IP).
- Provides **logical end‑to‑end communication** between processes on different hosts.
- Breaks application data into **segments** (TCP) or **datagrams** (UDP).
- Adds **headers** with ports, sequence numbers, checksums, etc.
- Hands segments to IP for delivery; IP doesn’t care about conversations, only packets.

> Think: IP gets packets from A to B,  
> **transport layer** makes sure the *right applications* on A and B talk to each other.

### Talking to a recruiter

> “At Layer 4 I’m not routing packets; I’m making sure the right applications can talk
> reliably or quickly. I choose TCP when I need delivery guarantees and ordering,
> and UDP when I need low latency and minimal overhead, like for voice or simple
> queries such as DNS.”

---

## 14.1.2 Transport Layer Responsibilities

The module lists several **responsibilities**. Know these names; they appear directly in
questions.

### 1. Tracking Individual Conversations

- Many applications on a host may use the network at the same time
  (browser, email client, streaming app, etc.).
- Transport layer tracks each conversation separately using **port numbers** and
  sometimes sequence numbers.
- Allows independent control: one stream can be slow or lossy without breaking others.

**Exam focus:**  
If they mention “tracking multiple sessions between applications”, that’s a
**transport‑layer** job.

### 2. Segmenting Data and Reassembling Segments

- Application messages are often too large to send in one piece.
- Transport layer **segments** the data into manageable blocks.
- Receiver **reassembles** segments back into the correct order for the application.
- With TCP this uses **sequence numbers**; UDP leaves most of this to the application.

**Analogy:**  
Splitting a big file into numbered packages before shipping; the receiver uses the
numbers to rebuild the file.

### 3. Add Header Information

- Each segment/datagram gets a **header** with control information:
  - Source and destination **port numbers**
  - Sequence and acknowledgment numbers (TCP)
  - Flags (SYN, ACK, FIN, etc. for TCP)
  - Length and checksum (TCP & UDP)
- This metadata is what allows reliability, multiplexing and basic error checking.

### 4. Identifying the Applications

- Transport layer uses **port numbers** to identify **which application** should
  receive incoming data.
- Examples:
  - TCP/80 → HTTP web server
  - TCP/443 → HTTPS
  - UDP/53 → DNS
- A combination of **IP + port** is a **socket**. A client–server conversation is a
pair of sockets (socket pair).

### 5. Conversation Multiplexing

- Multiple conversations share the same network connection.
- Multiplexing = mixing data from different sessions on the wire, then demultiplexing
at the receiver using port numbers and sequence info.
- Prevents one application from monopolising the link.

### Responsibilities – exam summary

If an option sounds like:

- **Tracking conversations**
- **Segmenting and reassembling**
- **Adding Layer‑4 headers**
- **Identifying applications with ports**
- **Conversation multiplexing**

→ It belongs to the **transport layer**.

If it talks about **routing, frames or MAC addresses**, that’s **not** transport.

### Recruiter angle

> “I understand that at Layer 4 I’m responsible for managing multiple parallel
> conversations, segmenting traffic and providing the level of reliability each
> application needs. That’s essential when troubleshooting, because I can quickly
> check if an issue is per‑flow, per‑application or network‑wide.”

---

## 14.1.3 Transport Layer Protocols

Two main protocols in TCP/IP:

- **TCP – Transmission Control Protocol**
- **UDP – User Datagram Protocol**

Both:

- Use **port numbers**.
- Hand segments to **IP** for forwarding.
- Provide **end‑to‑end communication** between processes.

But they make different trade‑offs.

### TCP – high reliability, more overhead

- **Connection‑oriented** – uses a 3‑way handshake to establish a session.
- Provides **reliable, ordered delivery**:
  - Sequence numbers
  - Acknowledgments (ACKs)
  - Retransmissions of lost segments
- Performs **flow control** and **congestion control**.
- Larger header, more processing, slightly slower.

### UDP – low overhead, best‑effort

- **Connectionless** and **stateless** – no handshake.
- No built‑in reliability, ordering or congestion control.
- Small header, minimal processing → **faster** and lower latency.
- Often used where some loss is acceptable or the application implements its own
recovery.

### Interview one‑liner

> “TCP is your tracked, signed‑for package; UDP is your normal letter.  
> With TCP the network stack guarantees delivery and ordering. With UDP the network
> just tries its best and the application decides how to handle loss.”

---

## 14.1.4 Transmission Control Protocol (TCP)

The course describes TCP as a **reliable, full‑featured** transport protocol.

### How TCP works (study view)

- **Segments data** from applications.
- Numbers segments and tracks what was sent.
- Requires a **connection** between sender and receiver (SYN, SYN‑ACK, ACK).
- Provides reliability via:
  - **ACKs** for received data.
  - **Retransmission** of segments that are not acknowledged.
  - **Sequencing** to reorder out‑of‑order segments.
- Manages sending rate:
  - Avoids overwhelming the receiver.
  - Adapts to network congestion.

TCP operations often listed in the module:

- Number & track data segments.
- Acknowledge received data.
- Retransmit unacknowledged data after a timeout.
- Sequence data that may arrive out of order.
- Send at an efficient rate that the receiver can handle.

### Why this matters for recruiters

> “When tuning or troubleshooting applications like web servers or databases, I’m
> comfortable reading TCP behaviour: slow start, retransmissions, window size, and
> how that impacts throughput and latency.”

---

## 14.1.5 User Datagram Protocol (UDP)

UDP is **simpler and lighter** than TCP.

### How UDP works (study view)

- Also divides data into **datagrams** (often still called segments in exam text).
- **Connectionless** – no setup/teardown; sender just blasts datagrams.
- **Best‑effort delivery**:
  - No acknowledgments.
  - No retransmissions.
  - No session state on either end.
- Because there’s less work per packet, UDP can be **faster**, especially for small,
time‑sensitive messages.

### Consequences

- No guarantee data actually arrived.
- No in‑order delivery guarantee.
- No built‑in flow or congestion control.
- Missing data is handled by the **application** (if it cares).

### Real‑world view

Use UDP when:

- You care more about **low delay** than about losing the occasional packet
  (e.g. VoIP, live video).
- You’re doing simple request/response where missing messages can just be retried
  quickly (e.g. DNS queries).

Recruiter phrase:

> “UDP gives me low‑latency fire‑and‑forget delivery. It makes sense for real‑time
> media and small, stateless queries where retransmitting at the application level
> is cheaper than running a full TCP session.”

---

## 14.1.6 The Right Transport Layer Protocol for the Right Application

This subsection is all about **matching TCP or UDP to the application’s needs**.

### When UDP is a better choice

Characteristics:

- Can tolerate **some loss**, but not **delay**.
- Needs to be **fast** and **lightweight**.
- Retransmission would make the experience worse.

Examples from the module:

- **VoIP / IP telephony**
- **Streaming audio or video** where small glitches are better than pauses.
- **DNS** lookups – small request/response, can easily be retried.

**Required protocol properties (UDP side of the figure):**

- Fast
- Low overhead
- No acknowledgments
- Does not resend lost data
- Delivers data as it arrives

### When TCP is a better choice

Characteristics:

- Data **must not be lost**.
- **Order** matters.
- Application would be broken or corrupted by missing pieces.

Examples:

- **Web browsing – HTTP/HTTPS**
- **Email – SMTP/IMAP/POP3**
- **Database connections**
- File transfers, configuration sync tools, etc.

**Required protocol properties (TCP side of the figure):**

- Reliable
- Acknowledges data
- Resends lost data
- Delivers data in sequenced order

### Hybrid thinking

Some applications can use **either TCP or UDP** depending on implementation
(e.g. video conferencing). Designers weigh:

- Available bandwidth
- Tolerance to loss vs delay
- Firewall behaviour (some block UDP more aggressively)

### How to use this in interviews

You might be asked something like:

> “Why would a real‑time game or VoIP softphone typically use UDP instead of TCP?”

A solid answer:

> “Because for real‑time streams a late packet is as bad as a lost packet. UDP gives
> us lower latency and allows the application to decide how to deal with loss, rather
> than waiting for TCP retransmissions.”

---

## 14.1.7 Check Your Understanding – Transportation of Data

Use this section to practise exam questions and also to phrase answers in
**interview‑ready language**.

---

### Question 1

> **Which layer is responsible for establishing a temporary communication session
> between the source and destination host applications?**

**Correct answer:** `Transport layer`

**Why?**

- The **transport layer** (TCP/UDP) sets up and manages conversations between
  applications, not the network layer.
- TCP in particular uses a **three‑way handshake** to establish a connection‑oriented
  session.

**Interview version**

> “Layer 4 is where we create and manage application sessions – things like TCP
> connections – while IP at Layer 3 just moves packets between hosts.”

---

### Question 2

> **Which three are transport layer responsibilities? (Choose three.)**

- ⬜ Tracking individual conversations  
- ⬜ Identifying frames  
- ⬜ Segmenting data and reassembling segments  
- ⬜ Identifying routing information  
- ⬜ Conversation multiplexing  

**Correct choices:**

- ✅ **Tracking individual conversations**  
- ✅ **Segmenting data and reassembling segments**  
- ✅ **Conversation multiplexing**

**Why not the others?**

- **Identifying frames** – that’s a **data link layer** job.
- **Identifying routing information** – belongs to the **network layer** (IP and
  routing protocols).

**Memory hook**

> “Transport = **track, chop, mix**.”  
> Track conversations, chop data into segments, mix multiple conversations over the
> same link.

---

### Question 3

> **Which transport layer protocol statement is true?**

- UDP is a best‑effort delivery protocol.  
- UDP provides reliability.  
- TCP has fewer fields than UDP.  
- TCP is faster than UDP.  

**Correct answer:** `UDP is a best-effort delivery protocol.`

**Why?**

- UDP sends datagrams without guarantees – no ACKs, no retransmissions, no
  connection state.
- TCP has **more** header fields and typically more overhead than UDP.
- TCP is usually **not faster** than UDP because of that extra work.

**Exam tip**

When you see **“best‑effort”** + **“no acknowledgments”**, think **UDP**.

---

### Question 4

> **Which transport layer protocol would be used for VoIP applications?**

- Transmission Control Protocol (TCP)  
- Session Information Protocol (SIP)  
- User Datagram Protocol (UDP)  
- VoIP Transfer Protocol  

**Correct answer:** `User Datagram Protocol (UDP)`

**Why?**

- VoIP prefers **low delay**; small packet loss is acceptable.
- UDP avoids retransmission delays and heavy connection management.
- **SIP** is a signalling protocol that usually runs *on top* of UDP or TCP, not a
transport‑layer protocol itself.
- “VoIP Transfer Protocol” is a distractor; it doesn’t exist.

**Interview angle**

> “Real‑time voice and video commonly run over UDP because a missing packet causes a
> tiny glitch, but waiting for TCP to retransmit would cause noticeable lag or
> freezes.”

---

### Ultra‑short recap for 14.1

- **Role:** Layer 4 moves data between applications, independent of paths and media.
- **Responsibilities:** Track conversations, segment/reassemble, add headers, identify
applications, multiplex streams.
- **TCP:** Connection‑oriented, reliable, ordered, heavier; for **accuracy‑critical**
apps.
- **UDP:** Connectionless, best‑effort, low overhead; for **delay‑sensitive** or
simple request/response apps.
- **Choosing protocol:**  
  - Need guarantees → **TCP**  
  - Need speed/low latency, some loss OK → **UDP**

---

## Section 14.2 – TCP Overview

Quick-reference notes for **CCNA NetAcad – Module 14, Section 14.2 (TCP Overview)**.

Focus: what makes TCP *reliable*, what the **TCP header** looks like, and which **applications use TCP**.

---

## 14.2.1 TCP Features

**Big picture:** TCP is your *reliable, connection‑oriented* transport protocol.  
It makes sure data gets to the other side, in order, without duplicates.

### Core TCP characteristics

- **Connection-oriented**
  - Before sending data, TCP establishes a **session** between source and destination (3‑way handshake, covered later in 14.5).
  - Session tracks state: which bytes were sent, which were acknowledged, etc.

- **Reliable delivery**
  - Data is divided into **segments**.
  - Each segment uses **sequence numbers** and **acknowledgments (ACKs)**.
  - Lost segments are **retransmitted**.
  - Duplicate segments are **detected and discarded**.

- **Same‑order delivery**
  - Segments can travel over different paths and arrive out of order.
  - TCP uses sequence numbers to **reassemble data in the correct order** before handing it to the application.

- **Flow control**
  - Every receiver advertises a **window size** (how many bytes it can accept at once).
  - The sender adapts its sending rate to avoid overwhelming the receiver.

- **Full‑duplex**
  - Both ends can send and receive at the same time.
  - Each direction has its own sequence and acknowledgment numbers.

#### Analogy

- TCP = **tracked, registered parcel**
  - You get a tracking number, each box is checked off, and the sender knows exactly which boxes arrived and which must be resent.

---

## 14.2.2 TCP Header

A minimum TCP header is **20 bytes (160 bits)**.  
It adds management information on top of the application data.

### TCP header layout (min. header, without options)

| Field                        | Size (bits) |
|------------------------------|-------------|
| Source Port                  | 16          |
| Destination Port             | 16          |
| Sequence Number              | 32          |
| Acknowledgment Number        | 32          |
| Header Length (Data Offset)  | 4           |
| Reserved                     | 6           |
| Control Bits (Flags)         | 6           |
| Window Size                  | 16          |
| Checksum                     | 16          |
| Urgent Pointer               | 16          |
| Options (optional) + Padding | variable    |
| Application Data             | variable    |

<img width="856" height="452" alt="image" src="https://github.com/user-attachments/assets/d9885c9c-4bf6-4ca5-8c95-cafd25d196c0" />


---

## 14.2.3 TCP Header Fields – What They Do

### Port fields

- **Source Port (16 bits)**
  - Identifies the **sending** application on the local host.
  - Example: random high port (ephemeral) like `49152`.

- **Destination Port (16 bits)**
  - Identifies the **target** application on the remote host.
  - Example: `80` for HTTP, `443` for HTTPS, `22` for SSH.

### Sequencing & reliability

- **Sequence Number (32 bits)**
  - Identifies the **first byte** of data in this segment.
  - Used to reorder segments and detect lost data.

- **Acknowledgment Number (32 bits)**
  - “I have received up to (and including) byte **N–1**. Please send me byte **N** next.”
  - Implements positive acknowledgments and cumulative ACKs.

### Header control

- **Header Length / Data Offset (4 bits)**
  - Specifies the total TCP header length in 32‑bit words.
  - Lets the receiver know where the **data** starts.

- **Reserved (6 bits)**
  - Set aside for future use; normally all **0**.

- **Control Bits / Flags (6 bits)**
  - Individual bits that control the session:
    - **URG** – Urgent pointer field is significant
    - **ACK** – Acknowledgment field is significant
    - **PSH** – Push data to the application immediately
    - **RST** – Reset the connection
    - **SYN** – Synchronize sequence numbers (used in handshake)
    - **FIN** – Sender has finished sending data

### Flow control & error checking

- **Window Size (16 bits)**
  - Tells the sender how many bytes the receiver is currently ready to accept.
  - Key to **flow control** and avoiding buffer overflow.

- **Checksum (16 bits)**
  - Error‑checking field over the TCP header + data.
  - Detects bit errors during transmission.

- **Urgent Pointer (16 bits)**
  - Used only when URG flag is set.
  - Points to urgent data that should be processed immediately.

- **Options + Padding**
  - Optional, variable fields (e.g., **Maximum Segment Size (MSS)**, **window scaling**).
  - Padding used so header ends on a 32‑bit boundary.

---

## 14.2.4 Applications that use TCP

**TCP takes care of segmentation, reliability, ordering and flow control, so applications don’t have to.**

Common **TCP‑based application protocols**:

- **HTTP / HTTPS** – Web browsing and APIs  
- **FTP, FTPS, SFTP** – File transfer (reliable, complete file delivery required)  
- **SMTP, POP3, IMAP** – Email transfer and retrieval  
- **SSH** – Secure remote login  
- **Telnet** (legacy) – Unencrypted remote terminal  
- **SMB / CIFS** – Windows file sharing

### When to expect TCP

Use TCP whenever the application needs:

- All data, with **no loss**.
- Data in the **correct order**.
- Automatic **retransmission** of lost segments.
- Built‑in flow control and congestion handling.

Examples:

- Downloading an installer – corrupted/missing bytes would break it.
- Logging into a remote server – you need every keystroke and response in order.
- Viewing banking or shopping websites – integrity and reliability matter.


<img width="1097" height="711" alt="image" src="https://github.com/user-attachments/assets/44396174-45ee-4714-8fbc-256237aa3875" />


---

## 14.2.5 Check Your Understanding – TCP Overview (Exam‑Style)

### Q1 – Reliable, ordered delivery

> **Which transport layer protocol ensures reliable same‑order delivery?**  
> - ICMP  
> - IP  
> - UDP  
> - TCP ✅

**Answer:** `TCP`  
**Why:** TCP provides connection‑oriented, reliable, in‑order delivery using sequence numbers and acknowledgments. IP and ICMP are not transport protocols; UDP is best‑effort and does not guarantee order.

---

### Q2 – TCP header size & fields

> **Which TCP header statement is true?**  
> - It consists of 8 fields in a 10‑byte header.  
> - **It consists of 10 fields in a 20‑byte header. ✅**  
> - It consists of 4 fields in an 8‑byte header.  
> - It consists of 20 fields in a 40‑byte header.

**Answer:** `It consists of 10 fields in a 20‑byte header.`  
**Why:** The **minimum** TCP header is 20 bytes and includes 10 core fields (source/destination ports, sequence and acknowledgment numbers, data offset, reserved, flags, window, checksum, urgent pointer). Options can increase the header beyond 20 bytes, but the base header is always 20.

---

### Q3 – Applications that use TCP

> **Which two applications would use the TCP transport layer protocol? (Choose two.)**  
> - TFTP  
> - ICMP  
> - **FTP ✅**  
> - **HTTP ✅**  
> - VoIP

**Answers:** `FTP` and `HTTP`  
**Why:** Both FTP and HTTP require reliable delivery and use TCP as their transport protocol.  
- **TFTP** uses UDP (simple, lightweight file transfer).  
- **ICMP** is its own protocol at the network layer (used by ping, traceroute).  
- Many **VoIP** implementations use UDP to minimize latency.

---

## Interview / CV Talking Points (Section 14.2)

You can describe this section to a recruiter like this:

- *“I understand how TCP provides **reliable, ordered delivery** using sequence numbers, acknowledgments and flow control.”*
- *“I can read a **TCP header** (20‑byte base header) and explain what each field does – ports, sequence/ack numbers, flags, window size, checksum, urgent pointer.”*
- *“I know which common protocols run over TCP (HTTP/S, FTP, SSH, SMTP/IMAP) versus UDP, and I can choose the right transport protocol based on application requirements.”*

These are great points for:

- **Junior Network / SOC Analyst**
- **Support Engineer / NOC**
- **Cybersecurity Trainee** (packet analysis with Wireshark, etc.)

---

## Ultra‑quick Exam Revision

- TCP is **connection‑oriented, reliable, in‑order, full‑duplex**, with **flow control**.
- Minimum TCP header = **20 bytes, 10 fields**.
- Key header fields: **source/destination ports, sequence & ACK numbers, flags, window, checksum**.
- Typical TCP apps: **HTTP, HTTPS, FTP, SSH, SMTP, IMAP, POP3**.
- If the question mentions **reliability or same‑order delivery** at Layer 4 → **TCP** is the answer.

---


# CCNA – Module 14, Section 14.3: UDP Overview (2025)

Quick-reference notes for **UDP** in the CCNA *Introduction to Networks* course.

Use this file to:
- Revise NetAcad **Module 14.3 – UDP Overview** before quizzes/exams.
- Have ready-made bullets you can quote to **recruiters / in interviews**.

NetAcad mapping:

- **14.3.1** UDP Features  
- **14.3.2** UDP Header  
- **14.3.3** UDP Header Fields  
- **14.3.4** Applications that use UDP  
- **14.3.5** Check Your Understanding – UDP Overview (quiz)

---

## 1. Big picture – What is UDP?

**User Datagram Protocol (UDP)** is the lightweight transport-layer protocol.  
It offers **segmentation and reassembly** like TCP, but **no reliability or flow control**.

- **Best-effort & stateless**
  - No connection setup, no session state tracked.
  - Sender just fires datagrams; if they arrive, great, if not, UDP itself does nothing.
- **Low overhead & fast**
  - Small 8‑byte header (vs 20‑byte TCP minimum).
  - No sequence numbers, ACKs, windows, congestion control.
- **Application responsibility**
  - Any required reliability, ordering, or recovery is handled by the **application**, not by UDP.

> Interview sentence:  
> “UDP trades reliability features for speed and low latency. It’s stateless, best-effort delivery with an 8‑byte header – ideal for real-time traffic like VoIP or simple request/response protocols like DNS.”

---

## 2. 14.3.1 UDP Features

### 2.1 What NetAcad highlights

- UDP is a **best-effort transport protocol**.
- Provides the **same data segmentation and reassembly** functions as TCP.
- **No reliability, no flow control**, fewer header fields ⟶ **less overhead**.
- Typically described by what it *does not* do compared to TCP.

### 2.2 Key UDP features (memorise for exam)

- **Stateless**
  - Neither client nor server tracks the *state* of the conversation.
  - No concept of “session established” or “session terminated” at the UDP layer.
- **Best-effort delivery**
  - Packets may be **lost, duplicated or arrive out of order**.
  - UDP does not try to detect or correct these issues.
- **Order of delivery**
  - Data is *reconstructed in the order it is received*.
  - If datagrams arrive out of order, the application must fix it (if it cares).
- **No retransmissions**
  - Any segments that are lost are **not resent** by UDP.
- **No resource awareness**
  - Sender is **not informed** if the receiver is low on resources.
  - No built-in congestion control, windowing, or backoff like TCP.
- **Low overhead**
  - Only 4 header fields, 8 bytes total (Source Port, Destination Port, Length, Checksum).

### 2.3 “For study” checklist

- [ ] I can explain why UDP is called **stateless** and **best-effort**.  
- [ ] I remember that UDP has **no session establishment** and **no retransmissions**.  
- [ ] I know that **applications** must handle reliability/ordering when using UDP.  
- [ ] I can list at least **three UDP-based application examples** (DNS, DHCP, VoIP, etc.).

### 2.4 “For recruiters” – how to sell it quickly

> “On the transport layer, I’m comfortable choosing between TCP and UDP. If an application needs low latency and can tolerate some loss – like VoIP, live video, DNS or DHCP – I’d favour UDP, then implement any required reliability at the application level.”

---

## 3. 14.3.2 UDP Header

### 3.1 Concept

- UDP is a **stateless protocol** – it does **not** keep track of session state.
- If reliability is needed when using UDP, that logic sits in the **application**.
- The communication blocks are called **datagrams** (or sometimes segments).  
  They are sent as **best effort** by the transport layer.

### 3.2 UDP header layout

Minimum UDP header size: **8 bytes (64 bits)**, four 16‑bit fields:

| Offset | Field              | Size | Notes |
|--------|--------------------|------|------|
| 0–15   | Source Port        | 16 b | Port number of sending application |
| 16–31  | Destination Port   | 16 b | Port number of receiving application |
| 32–47  | Length             | 16 b | Total length of UDP header + data |
| 48–63  | Checksum           | 16 b | Error checking of header and data |

After the header comes the **Application Layer data (size varies)**.

### 3.3 Study mnemonics

- **“4 fields, 8 bytes”** – exam favourite.  
- Only **Source Port**, **Destination Port**, **Length**, **Checksum** – nothing else.

---

## 4. 14.3.3 UDP Header Fields – details

| UDP Header Field | Size | Purpose (exam-style wording) |
|------------------|------|------------------------------|
| **Source Port**  | 16 b | Identifies the **source application** by port number. |
| **Destination Port** | 16 b | Identifies the **destination application** by port number. |
| **Length**       | 16 b | Indicates the **length of the UDP datagram** (header + data). |
| **Checksum**     | 16 b | Used for **error checking** of the UDP header and data. |

> Interview angle:  
> “TCP and UDP share the Source and Destination port fields – that’s how both protocols identify applications. UDP just drops the extra reliability fields to stay minimal.”

---

## 5. 14.3.4 Applications that use UDP

NetAcad groups UDP-friendly apps into **three categories**:

1. ### Live video and multimedia applications
   - Can tolerate **some data loss** but require **very low delay**.
   - Examples:
     - **VoIP (Voice over IP)**  
     - **Live streaming video**  
     - **Video conferencing**
   - Priority: keep the stream moving ⟶ **low latency > perfect reliability**.

2. ### Simple request and reply applications
   - Short, simple transactions where a host sends a **request** and may or may not get a **reply**.
   - If there is no answer, the client can simply **retry**.
   - Examples:
     - **DNS** (Domain Name System) – name resolution.  
     - **DHCP** (Dynamic Host Configuration Protocol) – address assignment.

3. ### Applications that handle reliability themselves
   - Protocol already provides its own **error detection, flow control, or recovery**.
   - Network transport can stay simple and fast.
   - Examples:
     - **SNMP** (Simple Network Management Protocol)  
     - **TFTP** (Trivial File Transfer Protocol)

> Note: DNS and SNMP use UDP **by default**, but can switch to **TCP** when needed  
> (for example, large DNS messages or specific SNMP scenarios).

### 5.1 Quick “TCP vs UDP app” crib

- **Usually UDP:** DNS, DHCP, SNMP, TFTP, VoIP, live video, video conferencing.  
- **Usually TCP:** HTTP/HTTPS, SMTP/IMAP/POP3, SSH, FTP.

---

## 6. 14.3.5 Check Your Understanding – quiz answers

These map to the NetAcad **“UDP Overview”** mini-quiz.

> ⚠️ Use these to understand the *concepts*, not just memorise letters.

---

### Question 1

> **Which of the following is a stateless best-effort delivery transport layer protocol?**  
> - ICMP  
> - UDP  
> - IP  
> - TCP  

**Correct answer: `UDP`** ✅

**Why:**  
- UDP is explicitly defined as a **stateless**, **best-effort** transport-layer protocol.  
- **ICMP** is not a transport protocol; it carries error/control messages.  
- **IP** is a network-layer protocol (Layer 3), not transport.  
- **TCP** is stateful and reliable, not best-effort in this sense.

---

### Question 2

> **Which UDP header statement is true?**  
> - It consists of 4 fields in an 8‑byte header.  
> - It consists of 8 fields in a 10‑byte header.  
> - It consists of 10 fields in a 20‑byte header.  
> - It consists of 20 fields in a 40‑byte header.  

**Correct answer: `It consists of 4 fields in an 8-byte header.`** ✅

**Why:**  
- UDP has **4 header fields**: Source Port, Destination Port, Length, Checksum.  
- Each is 16 bits ⟶ `4 × 16 = 64 bits = 8 bytes`.  
- The other options are distractors based on TCP or completely wrong sizes.

**Exam memory hook:**  
> “UDP = 4F / 8B” – *four fields, eight bytes*.

---

### Question 3

> **Which two applications would use the UDP transport layer protocol? (Choose two.)**  
> - ICMP  
> - HTTP  
> - TFTP  
> - FTP  
> - VoIP  

**Correct answers: `TFTP` and `VoIP`** ✅✅

**Why:**  
- **TFTP** (Trivial File Transfer Protocol) uses UDP by design – the application handles reliability.  
- **VoIP** is real-time voice; it prefers UDP to avoid delays from retransmissions.  
- **ICMP** is not a transport-layer protocol.  
- **HTTP** and **FTP** both use **TCP** because they need reliable delivery.

---

### Question 4

> **Which two fields are the same in a TCP and UDP header? (Choose two.)**  
> - Control bits  
> - Well-known port number  
> - Source port number  
> - Destination port number  
> - Sequence number  

**Correct answers: `Source port number` and `Destination port number`** ✅✅

**Why:**  
- Both TCP and UDP use **Source Port** and **Destination Port** to identify applications.  
- **Control bits** and **Sequence number** exist only in TCP.  
- “Well-known port number” is a concept (0–1023 range), not a specific header field name.

**Exam tip:**  
If a question asks “Which fields do TCP and UDP share?” the safe pair is **Source Port** and **Destination Port**.

---

## 7. Interview & recruiter talking points (UDP)

Drop one or two of these in a screening call or technical interview:

1. **Choosing between TCP and UDP**  
   > “When I design or troubleshoot an application flow, I first decide if we care more about *latency* or *reliability*. For real-time or simple request/response traffic – like VoIP, live video, DNS or DHCP – I’ll typically use UDP and handle any retries at the application level.”

2. **Header size and overhead**  
   > “UDP uses a minimal 8‑byte header with just four fields, compared to TCP’s 20‑byte minimum. That reduced overhead matters on high-throughput or latency-sensitive links.”

3. **Troubleshooting mindset**  
   > “If a UDP-based app misbehaves, I don’t expect retransmissions at the transport layer. I look for packet loss, jitter, and application-level retries instead of TCP-style retransmit patterns.”

4. **Security awareness**  
   > “Because UDP is stateless, it’s often used in amplification or spoofing attacks. In a security role I’d pay attention to unusual UDP patterns on ports like 53 (DNS) or 123 (NTP).”

---

### Final quick review

- UDP = **stateless, best-effort, low overhead**.  
- Header = **4 fields, 8 bytes**: Source Port, Destination Port, Length, Checksum.  
- Used by **VoIP, DNS, DHCP, SNMP, TFTP, live video and conferencing**.  
- **Applications** must handle reliability, ordering and recovery if they need it.

Use this sheet right before the **Module 14 quiz** or CCNA exam to refresh UDP concepts in under 5 minutes. 😺📡


---
## Section 14.4 – Port Numbers (Study Notes & Recruiter‑Friendly Summary)

These notes summarise **Module 14.4 – Port Numbers** of the Cisco NetAcad *Introduction to Networks* course.

They are written so that:

- **I can revise quickly** before exams or labs.
- **Recruiters or mentors** can see what I actually understand about Layer 4 ports and how they relate to sockets and applications.

---

## 14.4 Overview – Why Port Numbers Matter

IP addresses identify **hosts**, but not **which application** on the host should receive the data.

The **transport layer (TCP/UDP)** solves this by adding **port numbers**:

- **Source port** – who sent this segment/datagram (client side, usually dynamic).
- **Destination port** – which service on the remote host should receive it (server side, usually well‑known or registered).

Together with IP addresses, ports allow many **simultaneous conversations** between hosts, even when they use the same application (e.g. several browser tabs).

---

## 14.4.1 Multiple Separate Communications

Both **TCP and UDP** use port numbers to manage **multiple, simultaneous conversations**.

### Key ideas

- Each segment/datagram carries:
  - **Source Port (16 bits)**
  - **Destination Port (16 bits)**

- **Source port**
  - Chosen dynamically by the client OS.
  - Identifies the **originating application** on the local host.
  - Acts like a **return address** for the reply.

- **Destination port**
  - Well‑known / registered value that represents the **service** requested on the remote host.
  - Example: HTTP = port 80, HTTPS = 443, FTP control = 21.

### Example (web page request)

> Host 192.168.1.5 opens a browser and requests a web page from 192.168.1.7.

- The client OS chooses a random, unused **source port** (e.g. 1099).
- It sets **destination port 80** for HTTP.
- Segment headers:
  - Source port = 1099 (client)
  - Destination port = 80 (web server)

Result: the web server knows the request is for HTTP, and when it replies it sends data **back to source port 1099**, so the client’s browser tab receives the response.

---

## 14.4.2 Socket Pairs

A **socket** identifies one end of a Layer‑4 conversation:

> `IP address : Port`

Examples:

- Client socket: `192.168.1.5:1099`
- Web server socket: `192.168.1.7:80`

A **socket pair** is the combination of **both endpoints**:

> `192.168.1.5:1099, 192.168.1.7:80`

### Why sockets matter

- Allow a server to distinguish:
  - Different **clients** (different IPs and/or ports).
  - Different **applications/sessions** on the same client.
- Enable **multiple simultaneous connections** to the same service:
  - One web server on port 80 can serve many clients at once.
- The **transport layer** uses the source port as the **return address**:
  - When the response comes back, it knows which local application should receive it.

### FTP + Web example from the module

Client 192.168.1.5 is using:

- FTP client on source port **1305** communicating with FTP server port **21**.
- Web browser on source port **1099** communicating with web server port **80**.

Two socket pairs exist at the same time:

1. `192.168.1.5:1305, 192.168.1.7:21`  → FTP session  
2. `192.168.1.5:1099, 192.168.1.7:80`  → HTTP session  

The server can keep these completely separate using the **socket pairs**.

---

## 14.4.3 Port Number Groups

Port numbers are **16‑bit values**, so the total range is:

> **0 – 65,535**

The **IANA (Internet Assigned Numbers Authority)** divides this range into three groups.

### 1. Well‑known ports (0 – 1,023)

- Reserved for **common or popular services**.
- Help clients easily identify which service to contact.
- Examples:

| Port | Protocol | Typical Application                                  |
|------|----------|------------------------------------------------------|
| 20   | TCP      | FTP – Data                                           |
| 21   | TCP      | FTP – Control                                        |
| 22   | TCP      | SSH                                                  |
| 23   | TCP      | Telnet                                               |
| 25   | TCP      | SMTP (email sending)                                 |
| 53   | TCP/UDP  | DNS                                                  |
| 67   | UDP      | DHCP – Server                                        |
| 68   | UDP      | DHCP – Client                                        |
| 69   | UDP      | TFTP                                                 |
| 80   | TCP      | HTTP (web)                                           |
| 110  | TCP      | POP3 (email retrieval)                               |
| 143  | TCP      | IMAP (email retrieval/manipulation)                  |
| 161  | UDP      | SNMP                                                 |
| 443  | TCP      | HTTPS (secure web)                                   |

> Recruiter‑friendly summary: I know the main well‑known ports by heart and can map them to real protocols and use cases.

### 2. Registered ports (1,024 – 49,151)

- Assigned by IANA to **specific applications or vendor processes**.
- Used by software that is **popular but not part of the core Internet stack**.
- Examples: many proprietary or enterprise services.
- Some OSes may also use these as **source ports** instead of dynamic ports.

### 3. Private / Dynamic / Ephemeral ports (49,152 – 65,535)

- Typically chosen **dynamically by the client OS** when it starts a connection.
- Used mainly as **source ports** for client applications.
- Allow many **temporary conversations** without conflicts.
- Also called **ephemeral ports**.

---

## 14.4.4 The `netstat` Command

Unexplained TCP connections can be a **security risk**.  
The Windows `netstat` command is a key troubleshooting and security tool.

### What `netstat` shows

Running `netstat` (or `netstat -n` for numeric output) displays:

- **Protocol in use** (TCP/UDP).
- **Local address and port** (e.g. `192.168.1.124:3158`).
- **Foreign address and port** (remote endpoint).
- **Connection state** – e.g. `ESTABLISHED`, `LISTENING`, `TIME_WAIT`.

### Why it matters

- Helps verify which **services are listening** on a machine.
- Shows which **outbound connections** are currently active.
- Useful for:
  - Troubleshooting connectivity problems.
  - Detecting suspicious or unexpected connections.

---

## Check Your Understanding – Port Numbers (Section 14.4)

These are the NetAcad quiz‑style questions for this section with my answers and reasoning.

---

### Question 1

> Assume a host with IP address **10.1.1.10** wants to request web services from a server at **10.1.1.254**. Which of the following would display the correct socket pair?

Correct answer:

> **`10.1.1.10:1099, 10.1.1.254:80`**

**Why**

- Client: `10.1.1.10` uses a **dynamic source port** (e.g. 1099).
- Server: `10.1.1.254` listens on **destination port 80** for HTTP.
- Socket pair is always written as **(client IP:port, server IP:port)**.

---

### Question 2

> Which port group includes port numbers for **FTP, HTTP, and TFTP** applications?

Correct answer:

> **Well‑known ports**

**Why**

- FTP uses ports **20/21**, HTTP uses **80**, TFTP uses **69**.
- All of these are in the **0 – 1,023** range, which is the **well‑known** group.

---

### Question 3

> Which Windows command would display the protocols in use, the local address and port numbers, the foreign address and port numbers, and the connection state?

Correct answer:

> **`netstat`**

**Why**

- `netstat` is designed exactly for listing **active connections and listening ports**.
- It shows protocol, local socket, remote socket, and **state** (e.g. ESTABLISHED).
- `traceroute` (`tracert` on Windows) shows path through routers, not ports.
- `ping` just tests reachability with ICMP.
- `ipconfig /all` displays IP configuration, not live connections.

---

## One‑paragraph summary for recruiters

> I understand how **Layer 4 port numbers** let a single host run many networked applications at once. I can explain and use **socket pairs (`IP:port, IP:port`)** to distinguish individual TCP/UDP conversations, and I know the difference between **well‑known (0–1023), registered (1024–49151), and dynamic/ephemeral (49152–65535)** port ranges. I’m comfortable mapping key services to their ports (e.g. 80/443 web, 20/21 FTP, 22 SSH, 25 SMTP, 53 DNS, 67/68 DHCP, 69 TFTP) and using tools like **`netstat`** to inspect active connections and troubleshoot or detect suspicious traffic.

# 14.5 TCP Communication Process

> Goal of this section: understand how **TCP applications use ports**, how a **TCP connection is established (3‑way handshake)**, and how it is **terminated (4‑step FIN sequence)**.  
> This is basically the *life‑cycle* of a TCP session.

---

## 14.5.1 TCP Server Processes

### What is a TCP server process?

- On a server, **each networked application** (web, mail, SSH, …) is bound to a **specific TCP port number**.
- Examples from the module server:
  - HTTP web server → **TCP port 80**
  - SMTP mail server → **TCP port 25**
- The OS allows **one listening server process per (IP, port)**.
- A server can have **many ports open at the same time**, one per service (e.g. 80 for HTTP, 25 for SMTP, 22 for SSH, …).

When a TCP server application is **configured to use a port and is running**, we say that the **port is open**. The TCP stack on the server listens for incoming segments that have:

- destination IP = one of the server’s IP addresses
- destination port = the port number that application is bound to

Any segment that matches that (IP, port) tuple is handed to that server process.

---

### Clients sending TCP requests (tab: *Clients Sending TCP Requests*)

Example from the figure:

- **Client 1** wants web services from the server.
- **Client 2** wants email services from the same server.
- The server has two applications:
  - HTTP server listening on **TCP 80**
  - SMTP server listening on **TCP 25**

Each client builds a TCP segment with:

- source IP = client IP
- destination IP = server IP
- destination port = **80 (HTTP)** or **25 (SMTP)** depending on service

This is how a single TCP server can **support multiple services** at once.

---

### Request destination ports (tab: *Request Destination Ports*)

- Clients use **well‑known destination ports** to request services:
  - Web browsing → destination port **80**
  - Email (SMTP) → destination port **25**
- Well‑known ports allow clients to **know where to send** their requests without extra configuration.

In the figure:

- Client 1 sends: **source port 49152 → destination port 80** (HTTP).
- Client 2 sends: **source port 51152 → destination port 25** (SMTP).

---

### Request source ports (tab: *Request Source Ports*)

- Client OSs choose a **dynamic (ephemeral) source port** for each new TCP conversation.
- These ports typically come from the **dynamic/private range 49 152–65 535**.
- The source port uniquely identifies **which application/process** on the client started the conversation.

In the example:

- Client 1 dynamic source port = **49152**
- Client 2 dynamic source port = **51152**

Because the server sees both **source IP + source port**, it can keep **multiple simultaneous TCP conversations** from the same or different clients separate.

---

### Response destination ports (tab: *Response Destination Ports*)

When the server responds, it **swaps the ports** compared to the original request:

- For the HTTP reply:
  - source port = **80**
  - destination port = **49152** (client 1’s source port)
- For the SMTP reply:
  - source port = **25**
  - destination port = **51152** (client 2’s source port)

So the **destination port in the response** is the **client’s original source port**. This tells the client’s TCP stack **which local application** should receive the data.

---

### Response source ports (tab: *Response Source Ports*)

- The **source port in the server’s response** is the **server’s application port** (80 or 25).
- This means each direction of the TCP conversation uses the **same port pair**, just swapped:

Example HTTP flow:

- Client → Server: `49152 → 80`
- Server → Client: `80 → 49152`

Example SMTP flow:

- Client → Server: `51152 → 25`
- Server → Client: `25 → 51152`

The combination **(source IP, source port, dest IP, dest port)** is called a **TCP socket pair** and uniquely identifies each conversation.

---

### Check‑your‑understanding mapping (14.5.1)

**Q:** Which of the following would be valid source and destination ports for a host connecting to an email server?  
**A:** **Source: 49152, Destination: 25**  
- Source must be a **dynamic client port**.  
- Destination must be **SMTP’s well‑known port 25**.

---

### Key facts for the exam

- **Server applications listen on well‑known ports** (e.g. 80, 25, 443, 22).  
- **Client applications use dynamic source ports** so they can open many simultaneous TCP connections.  
- A **socket pair** `(src IP, src port, dst IP, dst port)` uniquely identifies a TCP conversation.  
- Replies **swap source and destination ports** compared to the original request.

---

### How I’d explain this to a recruiter

> “On the transport layer I understand the client‑server port model. Server applications listen on well‑known TCP ports like 80 (HTTP) and 25 (SMTP). Clients initiate connections from random high‑numbered ports, and the 4‑tuple of source IP/port and destination IP/port uniquely identifies each TCP session. That lets one server host many services and thousands of simultaneous client connections safely.”

---

## 14.5.2 TCP Connection Establishment (3‑Way Handshake)

TCP is **connection‑oriented**. Before data can flow, both hosts must agree to start a session and **synchronize sequence numbers**. This is done using the **three‑way handshake** with the **SYN** and **ACK** control flags.

### Step 1 – SYN

- The client wants to talk to the server.
- It sends a **TCP segment with the SYN flag set** and an **Initial Sequence Number (ISN)**.  
- Example in the module:
  - Host A → Host B: `SEQ = 100`, `CTL = SYN`

This says, “I want to start a connection, and I’ll start counting my bytes from sequence 100.”

### Step 2 – SYN + ACK

- The server receives the SYN and decides to accept the connection.
- It sends back a single segment with **both SYN and ACK flags set**:
  - Acknowledges the client’s ISN (`ACK = client ISN + 1`).
  - Sends its own ISN as the new sequence number.
- Example:
  - Host B → Host A: `SEQ = 300`, `ACK = 101`, `CTL = SYN, ACK`

This says, “I got your SYN, here is my SYN back, and I acknowledge your starting sequence.”

### Step 3 – ACK

- The client receives the SYN + ACK.
- It sends a final segment with the **ACK flag set** (no SYN this time):
  - `ACK = server ISN + 1`
- Example:
  - Host A → Host B: `SEQ = 101`, `ACK = 301`, `CTL = ACK`

Now **both sides have acknowledged each other’s ISNs**, and the TCP connection is **established**.

---

### Check‑your‑understanding mapping (14.5.2)

**Q:** Which control bit flags are used during the three‑way handshake?  
**A:** **SYN and ACK**.  
- First segment: SYN  
- Second segment: SYN + ACK  
- Third segment: ACK

---

### Key facts for the exam

- TCP uses a **3‑step handshake**: **SYN → SYN+ACK → ACK**.  
- This handshake:
  - Verifies that the **destination host is reachable**.  
  - Confirms that the **service port is listening**.  
  - **Synchronizes sequence numbers** in both directions.  
- The **SYN flag** starts a connection, and the **ACK flag** is used for acknowledgements throughout the session.

---

### How I’d explain this to a recruiter

> “I understand the TCP three‑way handshake: the client sends SYN, the server replies with SYN‑ACK, and the client finishes with ACK. That process proves both hosts are reachable, confirms the service port is listening, and synchronizes sequence numbers so the rest of the conversation can be tracked reliably.”

---

## 14.5.3 Session Termination (4‑Segment FIN Sequence)

To close a TCP connection cleanly, the **FIN (Finish)** control flag is used. Each direction of the full‑duplex TCP session is closed **independently**, so terminating one TCP conversation requires **four segments** – two in each direction.

### Step 1 – FIN (client → server)

- When the client has no more data to send, it sends a segment with the **FIN flag set**.  
- Example: Host A → Host B: **FIN**

This says, “I’m done sending data in this direction.”

### Step 2 – ACK (server → client)

- The server acknowledges the FIN:
  - Host B → Host A: **ACK**

Now the client knows the server received the request to close this direction.

### Step 3 – FIN (server → client)

- When the server has also finished sending data, it sends its own **FIN**:
  - Host B → Host A: **FIN**

This starts closing the reverse direction of the TCP session.

### Step 4 – ACK (client → server)

- Finally, the client acknowledges that second FIN:
  - Host A → Host B: **ACK**

At this point, **both directions** of the TCP session are closed.

> Summary: **FIN → ACK → FIN → ACK** (4 segments, often called “two 2‑way handshakes”).

---

### Check‑your‑understanding mapping (14.5.3)

**Q:** How many exchanges are needed to end both sessions between two hosts?  
**A:** **Four exchanges** (FIN, ACK, FIN, ACK).

---

### Key facts for the exam

- TCP uses **FIN + ACK** segments to **gracefully close** a session.  
- The connection is **full‑duplex**; each direction is closed separately, which is why we need 4 segments.  
- A separate control flag **RST (Reset)** can be used to **abruptly terminate** a connection when an error occurs or a connection is invalid.

---

### How I’d explain this to a recruiter

> “I know TCP terminates connections gracefully with a four‑segment FIN sequence: FIN, ACK, FIN, ACK. That allows each direction of the full‑duplex channel to close cleanly. In troubleshooting tools like Wireshark, I can recognise a healthy TCP teardown versus an abnormal reset (RST).”

---

## 14.5.4 TCP Three‑Way Handshake Analysis & Control Bits

This subsection explains what information TCP tracks during a conversation and how **control bits (flags)** show the state of a connection.

### What the 3‑way handshake achieves

From the module:

1. **Confirms the destination is present on the network.**
2. **Verifies the destination has an active service** listening on the requested port and is accepting new connections.
3. **Informs the destination** that the client intends to establish a communication session on that port.

Combined with sequence and acknowledgement numbers, this lets TCP:

- Maintain **state information** for each session.
- Track **every data segment** within that session.
- Know what data has been **successfully received** and what may need **retransmission**.

### Control bits (flags) in the TCP header

The TCP header has a 6‑bit **Control Bits** field. Each bit is a **flag** that can be on (1) or off (0). The six key flags are:

- **URG** – Urgent pointer field significant (data marked as urgent).  
- **ACK** – Acknowledgement flag; used in connection establishment and throughout the session to confirm receipt.  
- **PSH** – Push function; asks the receiver to pass data to the application immediately (don’t buffer).  
- **RST** – Reset; abruptly resets a connection when there is an error or invalid connection attempt.  
- **SYN** – Synchronise sequence numbers; used to establish a connection (3‑way handshake).  
- **FIN** – Finish; indicates no more data from the sender and is used in session termination.

When you analyse traffic (for example, in **Wireshark**), you can read these flags to see **where in the connection lifecycle** each segment belongs (setup, data transfer, or teardown).

---

### Key facts for the exam

- TCP is **stateful**: it remembers sequence/ack numbers and connection state using fields in the header.  
- The **Control Bits field** provides the flags that define connection behaviour (SYN, ACK, FIN, RST, PSH, URG).  
- The three‑way handshake and four‑segment termination are **just specific sequences of these flags**.

---

### How I’d explain this to a recruiter

> “Beyond just ‘TCP is reliable’, I understand how the protocol tracks state. Sequence and acknowledgement numbers plus control flags like SYN, ACK, FIN, and RST tell you exactly where a connection is in its life‑cycle. I’m comfortable reading those flags in tools like Wireshark to troubleshoot connectivity and application issues.”

---

## 14.5.5 Wireshark View of the TCP 3‑Way Handshake & Termination (Video Summary)

The video in the module walks through **Wireshark captures** of both the 3‑way handshake and the termination of a TCP conversation.

### Handshake in Wireshark

- The capture shows a classic **3‑packet sequence**:
  1. **SYN**
  2. **SYN, ACK**
  3. **ACK**
- In the packet list, you see these as consecutive packets (for example, packets 10, 11, and 12).

**Initial Sequence Number (ISN)**

- In reality, the ISN is a **32‑bit random number** chosen at the start of each new TCP conversation.  
- This randomness helps defend against **TCP connection hijacking attacks**.  
- **Wireshark simplifies analysis** by displaying **“relative sequence numbers”**:
  - It treats the first observed sequence number as **0**.
  - All later sequence and acknowledgement numbers are shown relative to that, making flows easier to follow.

In the details pane for the SYN packet you can see:

- `Sequence number: 0 (relative)`
- Flags with **SYN = 1**, others 0.

In the SYN+ACK packet you can see:

- `Ack number: 1 (relative)` acknowledging the client’s SYN.  
- A new sequence number 0 from the server (relative, for the reverse direction).  
- Flags with **SYN = 1, ACK = 1**.

In the final ACK packet you see:

- `Ack number: 1` acknowledging the server’s SYN.  
- Flags with **ACK = 1**, SYN cleared.

### Termination in Wireshark

Later in the capture, the video shows **how the TCP connection ends**:

1. The server sends a segment with **FIN + ACK** set.  
2. The client replies with an **ACK** (acknowledging the FIN).  
3. The client then sends its own **FIN + ACK**.  
4. The server finishes with a final **ACK**.

This appears as **two back‑to‑back two‑way handshakes** (FIN/ACK, FIN/ACK). In Wireshark, the flags field clearly shows **FIN = 1** when the teardown begins, and acknowledgements continue until the final ACK.

You may notice that acknowledgement numbers are much higher by this point (for example in the 300‑plus range), because they reflect **all bytes that have been successfully transferred** during the session.

---

### Key facts for the exam

- Wireshark uses **relative sequence numbers** to make TCP flows readable.  
- The TCP 3‑way handshake is clearly visible as **SYN → SYN,ACK → ACK**.  
- Termination shows **FIN + ACK** sequences in **both directions**.  
- Flags plus sequence/ack numbers are your best indicators of **connection state** when troubleshooting.

---

### How I’d explain this to a recruiter

> “I’ve practised reading TCP handshakes directly in Wireshark. I can identify SYN, SYN‑ACK, ACK when connections start, and FIN/ACK sequences when they close. I also understand how Wireshark uses relative sequence numbers, and I can use those values plus flags to trace issues like half‑open connections or unexpected resets.”

---

## 14.5.6 Check Your Understanding – TCP Communication Process (Q&A)

A few quick exam‑style checks from this section:

1. **Valid source/destination ports for a host connecting to an email server?**  
   - ✅ **Correct:** `Source: 49152, Destination: 25`  
   - Reason: clients use **dynamic high ports** as the source, and SMTP listens on **TCP 25**.

2. **Which control bit flags are used during the three‑way handshake?**  
   - ✅ **Correct:** **SYN and ACK**  
   - Reason: the handshake is **SYN → SYN,ACK → ACK**.

3. **How many exchanges are needed to end both sessions between two hosts?**  
   - ✅ **Correct:** **Four exchanges**  
   - Reason: TCP teardown uses **FIN, ACK, FIN, ACK** – two segments in each direction.

---

## 14.5 Big‑Picture Recap

- TCP communication life‑cycle:
  1. **Server processes** listen on well‑known ports.  
  2. **Clients initiate** connections from dynamic ports using the **3‑way SYN/SYN‑ACK/ACK handshake**.  
  3. Data is transferred reliably using **sequence numbers, acknowledgements, and control flags**.  
  4. The session ends cleanly using a **four‑segment FIN/ACK sequence**.

---

### How I’d summarise this section on my CV / to a recruiter

> “I’m comfortable working at the transport layer. I understand how TCP uses ports and socket pairs to multiplex many client/server conversations, how the three‑way handshake and flags like SYN/ACK/FIN establish and track connection state, and how to recognise normal versus abnormal TCP setups and teardowns in packet captures. That helps me troubleshoot connectivity issues and reason precisely about how applications use the network.”



---

# CCNA: Introduction to Networks – Module 14  
## Section 14.6 – Reliability and Flow Control (TCP) – Study & Recruiter Notes (2025)

**Author:** EchoLynx  
**Course:** Cisco NetAcad – *Introduction to Networks*  
**Module:** 14 – *Transport Layer*  
**Section:** 14.6 – *Reliability and Flow Control*  
**Status:** ✅ Completed – theory + videos

---

## 1. Why this section matters

TCP is not just “another protocol on top of IP.”  
In this section I studied **how TCP guarantees reliable, ordered delivery** and **how it controls the rate of data flow** so that neither side is overloaded:

- How **sequence numbers** and **acknowledgements (ACKs)** allow a receiver to reassemble data and detect loss.  
- How TCP **retransmits** segments when loss happens (classic and selective acknowledgement).  
- How TCP implements **flow control** using **window size** and **maximum segment size (MSS)**.

These mechanisms are the reason why applications like web browsing, file transfer and email can trust the network to deliver data **completely and in order**, even across an unreliable IP network.

---

## 2. 14.6.1 – TCP Reliability: Guaranteed and Ordered Delivery

### 2.1 Sequence numbers and ISN

Every TCP connection maintains a **byte‑oriented sequence space**:

- Each byte in the stream is numbered; the **Sequence Number** in the TCP header identifies *“first byte of data in this segment”*.
- During session setup, each side chooses an **Initial Sequence Number (ISN)**:
  - 32‑bit value, effectively a random number.
  - Protects against old segments or TCP hijacking attacks.
- As data is transmitted, the sequence number is incremented by the number of data bytes sent.

This means the receiver can:

1. **Detect missing data** (a “gap” in sequence numbers).  
2. **Reorder out‑of‑order segments** into the original sequence before passing data to the application.

> Example: If bytes 1–1460 arrive, then 2921–4380, the receiver knows bytes 1461–2920 are missing and can hold the later segments until the gap is filled.

### 2.2 Reordering at the destination

Because IP is connectionless, **segments may take different routes** and arrive out of order. TCP fixes this:

- The receiving host stores segments in a **reassembly buffer**.
- Segments are placed according to their **sequence numbers**.
- Once all bytes up to the next expected position have arrived, data is passed up to the application.

So even when the network delivers segments in the order `1, 2, 6, 5, 4, 3`, TCP gives the application data in the correct order: `1, 2, 3, 4, 5, 6`.

---

## 3. 14.6.2 – Video: TCP Reliability – Sequence Numbers and ACKs (summary)

The video reinforces three key ideas:

1. **Connection‑oriented:**  
   A TCP connection is established first using the **three‑way handshake** before data is exchanged.

2. **Sequence numbers:**  
   - Every segment is tagged with a sequence number.  
   - This allows the receiver to rebuild the ordered data stream and spot out‑of‑order or missing data.

3. **Acknowledgements (ACKs) and window size:**  
   - The receiver returns **ACKs** containing the **next expected byte number**.  
   - The **window size** is the total number of unacknowledged bytes the sender is allowed to have “in flight”.  
   - The sender must **not exceed the advertised window**; this is how TCP prevents overwhelming the receiver.

> Example from the video (simplified):  
> - Sender: “Starting at byte 1, I’m sending 10 bytes.” (window size 10)  
> - Receiver: “I received bytes 1–10. I expect byte 11 next.” → `ACK = 11`  
> - Sender then sends bytes 11–20. Receiver answers with `ACK = 21`, etc.

Modern TCP implementations support large windows (tens of megabytes or more) using **window scaling**, but the logic is the same.

---

## 4. 14.6.3 – TCP Reliability: Data Loss and Retransmission

Even in a well‑designed network, **packets get lost**. TCP uses its reliability mechanisms to detect this and recover.

### 4.1 Classical retransmission with cumulative ACKs

TCP uses **cumulative acknowledgements**:

- ACK `N` means *“I have received every byte up to N‑1; N is the next byte I expect.”*
- If some segments are lost, the receiver keeps ACKing the **same number**, indicating it is still waiting for that byte.

**Example (numbering segments instead of bytes for clarity):**

1. Host A sends segments `1, 2, 3, 4, 5, 6, 7, 8, 9, 10`.  
2. Segments `3` and `4` are lost in transit.  
3. Host B receives `1, 2, 5, 6, 7, 8, 9, 10` but detects the gap after segment 2.  
4. Host B sends **`ACK 3`**, meaning “I have everything up to segment 2; I expect 3 next.”  
5. Without more advanced features, Host A must **retransmit segments 3–10**, which creates **duplicate segments** and wastes bandwidth.

### 4.2 Selective Acknowledgement (SACK)

Modern TCP stacks commonly support **Selective Acknowledgement (SACK)**, negotiated during the three‑way handshake.

With SACK:

- The receiver can explicitly acknowledge **non‑contiguous blocks** of data:
  - “I have 1–2 (ACK 3) and also 5–10 (SACK 5–10).”
- The sender only needs to retransmit the **missing pieces** (here, segments 3 and 4).

Benefits:

- Less unnecessary retransmission.  
- More efficient use of bandwidth and reduced congestion.  
- Faster recovery from loss.

### 4.3 Timers and retransmission (video summary)

The second video shows the **timeout and retransmission** process:

1. Sender transmits a segment and **starts a timer**.  
2. If an ACK is received **before** the timer expires → OK, send next segment.  
3. If **no ACK** arrives before timeout → sender **retransmits** that segment and restarts the timer.

This continues until all segments are acknowledged.  
TCP typically doesn’t ACK every single segment; it often ACKs **every second segment** or uses **delayed ACKs**, depending on the implementation.

---

## 5. 14.6.5 – TCP Flow Control: Window Size and ACKs

TCP also implements **flow control** so the sender does not overload the receiver.

### 5.1 Window size field

- The TCP header contains a 16‑bit **Window Size** field.  
- It represents the number of bytes the receiver is currently willing to accept beyond the last acknowledged byte.  
- The **sender must obey this advertised window**.

**Example from the course figure:**

- During the three‑way handshake, PC B advertises an initial window size of **10,000 bytes**.  
- This means PC A may send up to 10,000 bytes before it *must* receive an ACK.  
- As PC B processes data and frees up buffer space, it continues to send ACKs with updated window sizes.

This behaviour is called a **sliding window**:

- As the sender receives ACKs like `ACK 2921, window 10,000`, it knows:  
  - “The receiver has successfully received bytes up to 2920 and can still accept 10,000 more bytes.”  
- The sender’s *send window* slides forward as data is acknowledged.

### 5.2 Dynamic adjustment

The receiver can adjust the advertised window depending on available buffer space:

- If the receiver becomes **busy or low on memory**, it can **shrink** the window to slow the sender.  
- If it has plenty of free buffer space, it can advertise a **larger** window to allow more data in flight.

Modern TCP implementations use sliding windows plus algorithms like **congestion control** (e.g., slow start, congestion avoidance). Congestion control is mainly about the **network path**, while the window size field is about **receiver capacity**—but both influence how much data is sent.

> Note: Many stacks ACK approximately every second full‑sized segment rather than literally every packet. The exact behaviour can vary.

---

## 6. 14.6.6 – TCP Flow Control: Maximum Segment Size (MSS)

Besides window size, TCP uses **Maximum Segment Size (MSS)** to control how large each segment’s payload can be.

### 6.1 MSS basics

- **MSS** = maximum number of **data bytes** a device can receive in a single TCP segment.  
- MSS does **not** include TCP or IP header bytes.  
- MSS is usually negotiated in the **options field** during the three‑way handshake.

### 6.2 Relationship with MTU

On Ethernet with IPv4:

- **MTU (Maximum Transmission Unit)** = 1500 bytes (default).  
- IPv4 header = 20 bytes.  
- TCP header = 20 bytes.  
- Therefore, a common MSS is:

  ```text
  MSS = 1500 (MTU) – 20 (IPv4 header) – 20 (TCP header) = 1460 bytes
  ```

Choosing MSS correctly prevents **IP fragmentation** and improves performance.

---

## 7. Key facts for the exam

Quick points I keep in mind:

- TCP provides **reliable, ordered, connection‑oriented** delivery using:
  - Sequence numbers  
  - Acknowledgements (ACKs)  
  - Timers and retransmissions  
  - Flow control (window size, MSS)
- **ISN (Initial Sequence Number)** is a 32‑bit random starting point for sequence numbers; helps against TCP hijacking and old segments.  
- Receivers reorder out‑of‑order segments using **sequence numbers and a reassembly buffer**.  
- With classic cumulative ACKs, loss of a segment causes repeated ACK of the missing byte; sender may retransmit a **range** of segments.  
- **Selective ACK (SACK)** allows the receiver to inform the sender exactly which ranges were received so only the **missing segments** are resent.  
- **Window Size field** = how many additional bytes the receiver is ready to accept beyond the last ACKed byte. This is core to TCP **flow control**.  
- **Sliding window**: window position (and size) moves forward as ACKs arrive; sender keeps the number of unacknowledged bytes ≤ advertised window.  
- **MSS** is negotiated during the three‑way handshake and typically equals **MTU – IP header – TCP header** (often 1460 bytes on Ethernet/IPv4).

---

## 8. How I’d explain this to a recruiter

> “In Module 14.6 I went deeper into how TCP makes unreliable IP networks look reliable to applications. I understand how TCP numbers every byte with sequence numbers, buffers and reorders segments that arrive out of order, and uses ACKs plus timers to detect and retransmit lost data. I also studied selective acknowledgements (SACK), which let modern TCP stacks retransmit only the missing ranges instead of resending everything.  
>  
> On the flow‑control side, I can interpret the TCP window size and MSS fields in packet captures. I know how the advertised receive window and sliding window mechanism prevent senders from overwhelming a receiver, and how MSS is chosen based on the path MTU (for example, 1460‑byte MSS on Ethernet with IPv4). This helps me reason about performance issues like retransmissions, duplicate segments or poor throughput when troubleshooting real networks.”

---

### File info

- **Filename:** `ccna-module-14-section-14.6-reliability-and-flow-control-2025.md`  
- **Purpose:** Personal CCNA study notes + portfolio evidence of networking fundamentals knowledge.





# 14.6 Reliability and Flow Control (TCP)

> Extracted + structured notes from your screenshots (14.6.1 → 14.6.6) + your pasted video transcripts.

---

## 14.6.1 TCP Reliability — Guaranteed and Ordered Delivery

TCP can be a better protocol for some applications because, unlike UDP:
- It **resends dropped packets**.
- It **numbers packets** so data can be delivered in the **proper order**.
- It can also help **maintain the flow of packets** so devices do not become overloaded.

### Why sequence numbers matter
Sometimes TCP segments:
- **do not arrive** at the destination, or
- **arrive out of order**.

For the original message to be understood, **all data must be received** and then **reassembled** in the original order.

**Sequence numbers** are assigned in the header of each packet to achieve this.
- The **sequence number represents the first data byte** of the TCP segment.

### ISN (Initial Sequence Number)
During session setup, an **initial sequence number (ISN)** is set:
- It represents the **starting value** of the bytes transmitted to the receiving application.
- As data is transmitted, the sequence number is **incremented by the number of bytes transmitted**.
- This byte tracking lets each segment be **uniquely identified and acknowledged**, and helps identify **missing segments**.

The ISN does **not** begin at 1 — it’s effectively a **random number** (helps prevent certain types of malicious attacks).
- For simplicity, the examples use **ISN = 1**.

---

## Figure — TCP Segments Are Reordered at the Destination

- **Different segments may take different routes.**
- **Data is divided into segments** (Segment 1, 2, 3, 4, 5, 6).
- Because of different routes, segments can **arrive out of order**.
- TCP then **reorders the segments to the original order**.

### What the receiver does
The receiving TCP process:
- places data from a segment into a **receiving buffer**,
- puts segments in the **proper sequence order**,
- then passes data to the **application layer** once reassembled.

Segments with out-of-order sequence numbers are **held** for later processing.
When missing bytes arrive, the buffered segments are processed **in order**.

---

## 14.6.2 Video — TCP Reliability: Sequence Numbers and Acknowledgements

**On-screen description (from the page):**
- One function of TCP is to ensure each segment reaches its destination.
- The destination host’s TCP services **acknowledge** data received by the source application.
- The lesson focuses on TCP **sequence numbers** and **acknowledgements**.

### Video 1 transcript (your pasted text)

00:04 - [Speaker] This video depicts a simplified example  
00:07 of TCP operations.  
00:10 It is not necessarily a realistic depiction.  
00:13 TCP is a connection-oriented protocol.  
00:16 In that, a connection is established first  
00:19 using a three-way handshake before data is sent.  
00:22 Another characteristic of TCP  
00:25 is that it's a reliable protocol.  
00:27 Two things that make it reliable are sequence numbers  
00:31 and acknowledgements.  
00:32 Every TCP segment that's sent in a TCP conversation  
00:36 gets a sequence number.  
00:38 So every byte of data is numbered  
00:41 basically in a sequential list.  
00:43 This allows a receiving host to rebuild the data  
00:46 from the ordered numbered segments.  
00:49 If data arrives out of order at the receiving end,  
00:53 the data can be put back together in the proper order  
00:56 thanks to the sequence numbers.  
00:59 Acknowledgements come into play by helping the sender know  
01:03 that the data that's being sent is actually being received.  
01:08 The way this works is, the sending host sends TCP segments  
01:12 in bytes, and the receiving host acknowledges bytes received  
01:16 by sending acknowledgements.  
01:19 There is a limit to the amount of data  
01:20 the sending host can send before it receives  
01:23 an acknowledgement from the receiver.  
01:26 This amount is called the window size.  
01:28 The window size is the total number of bytes  
01:31 sent in TCP segments that can be sent  
01:35 before receiving an acknowledgement.  
01:37 Using TCP window scaling, computers are able to achieve  
01:41 large window sizes of up to one gigabyte.  
01:45 So as the sending host sends bytes of data in TCP segments,  
01:49 the receiving host returns acknowledgements as it processes  
01:54 bytes received, and frees up its buffers.  
01:58 We can see this depicted in this graphic.  
02:01 Let's start by reading the message  
02:04 from the sending host here.  
02:06 Start with byte number one; I am sending 10 bytes.  
02:10 In this scenario, the 10 bytes is the window size.  
02:15 In reality the window size would be a lot larger  
02:18 than 10 bytes, since today window sizes are typically  
02:21 16 megabytes or larger.  
02:23 But this works nicely for this example.  
02:28 So the host is sending 10 bytes,  
02:30 starting with byte number one.  
02:32 The receiving host, the server here, says:  
02:35 I received 10 bytes, starting with byte number one.  
02:39 I expect byte 11 next.  
02:42 This is the acknowledgement.  
02:45 The server acknowledges it received the 10 bytes  
02:48 and now is expecting number 11.  
02:52 If we look down here, we can see that in this segment  
02:56 starting with sequence number one, 10 bytes have been sent.  
03:01 The receiver sends an Ack 11.  
03:05 Starting with one, 10 bytes were sent  
03:08 so the next sequence number it's expecting is an 11.  
03:12 This acknowledgement is sent back to the originating host.  
03:17 Now the originating host sends 10 more bytes  
03:21 starting with sequence number 11.  
03:24 If we were to ask ourselves, what would be the next Ack  
03:28 that the server would send back to the originating host?  
03:33 We would have to ask ourselves:  
03:34 What's the last sequence number sent?  
03:37 Starting with 11, 10 bytes were sent,  
03:41 so the last sequence number that was sent was 20.  
03:44 So the Ack would be an Ack 21.  
03:48 That's the next expected sequence number.  
03:52 You can see how sequence numbers and acknowledgements  
03:56 including the window size, make TCP a very orderly  
04:01 and reliable protocol.

---

## 14.6.3 TCP Reliability — Data Loss and Retransmission

No matter how well designed a network is, **data loss occasionally occurs**.
TCP provides methods to manage segment losses, including a mechanism to **retransmit segments for unacknowledged data**.

### SEQ + ACK work together (expectational acknowledgement)
- The **sequence (SEQ) number** identifies the **first byte of data** in the segment being transmitted.
- The **acknowledgement (ACK) number** is sent back to the source to indicate the **next byte expected**.
- This is called **expectational acknowledgement**.

### Before enhancements (why duplicates happened)
Earlier TCP behavior could only acknowledge the **next byte expected**.

Example (using segment numbers for simplicity):
- Host A sends segments **1 through 10** to host B.
- If all segments arrive **except 3 and 4**, host B replies with an acknowledgement saying the next expected is **segment 3**.
- Host A cannot know which later segments arrived, so it may resend **segments 3 through 10**.
- If the resent segments arrive successfully, segments **5 through 10** become **duplicates** → can cause **delays, congestion, and inefficiencies**.

### SACK (Selective Acknowledgement)
Many operating systems use optional **SACK**, negotiated during the **three-way handshake**.
If both hosts support SACK:
- the receiver can explicitly acknowledge which segments (bytes) were received, including **discontinuous segments**,
- the sender only needs to retransmit the **missing** data.

Example:
- Host A sends segments **1 through 10**.
- If everything arrives except **3 and 4**, host B can:
  - acknowledge segments 1 and 2 (**ACK 3**),
  - selectively acknowledge segments 5 through 10 (**SACK 5–10**).
- Host A then only needs to resend **segments 3 and 4**.

**Note:** TCP typically sends ACKs for **every other packet**, but other factors may alter this behavior.

TCP uses **timers** to decide how long to wait before resending a segment.
(The page notes a video + PDF examining TCP data loss and retransmission.)

---

## 14.6.4 Video — TCP Reliability: Data Loss and Retransmission

**On-screen description (from the page):**
- Click Play to view a lesson on TCP retransmission.
- The video shows the process of resending segments not initially received by the destination.

### Video 2 transcript (your pasted text)

00:00 - The graphic depicted in this video  
00:03 uses segment numbers in place of sequence numbers.  
00:07 TCP is a reliable protocol.  
00:09 It uses sequence numbers, and acknowledgements  
00:12 to provide that reliability.  
00:15 But, what happens when data is lost in transit?  
00:19 As a reliable protocol,  
00:21 there has to be a mechanism for resending lost data,  
00:25 so that an entire piece of data,  
00:27 like a file, or an image, or a video can be rebuilt  
00:32 from all of the segments.  
00:34 If we look at this animation,  
00:37 we can see this process in action.  
00:39 I'll press play.  
00:41 The source host here sends segment 1 and starts a timer.  
00:46 You can see the timer's running.  
00:49 The destination host receives segment 1.  
00:54 And, since it's received segment 1,  
00:56 it's going to send an acknowledgement.  
00:58 Let's see what happens.  
01:01 We can see that the destination host  
01:03 has received segment 1, acknowledges the delivery,  
01:08 and is going to send an act 2, an acknowledgement 2,  
01:12 requesting number 2.  
01:13 Why?  
01:15 It received 1, so it sends a request for 2,  
01:17 and an act 2.  
01:19 So, we'll see that get sent.  
01:21 All right, there goes the acknowledgement.  
01:23 The source receives the acknowledgement  
01:26 before the timer expires, and now can send segment 2.  
01:29 There's segment 2, it's sent,  
01:33 and as you can see, the timer has started.  
01:36 It's going to wait to get an acknowledgement.  
01:39 If it doesn't receive an acknowledgement  
01:43 from the destination before the timer expires,  
01:47 it will resend segment 2.  
01:49 Let's see this in action.  
01:52 You can see the destination has not received segment 2.  
01:57 Since it hasn't received segment 2,  
02:00 it won't send an acknowledgement number 3  
02:03 back to the device.  
02:06 It's not going to acknowledge that it received 2,  
02:09 and send an act 3 back to the source host.  
02:11 Let's see what happens.  
02:14 No acknowledgement, the timer expires.  
02:17 You can see here the timer expires.  
02:20 So, what will the source host do?  
02:22 The source host will retransmit, or resend segmeent 2,  
02:27 and restart the timer.  
02:30 This time, the information was received  
02:34 by the destination, and now  
02:36 it's going to send an act 3,  
02:38 or acknowledgement 3,  
02:40 requesting the next piece of data,  
02:42 which in this case would be number 3.  
02:47 The acknowledgement's received before the timer expires,  
02:52 and segment 3 is sent.  
02:54 Segment 3 is received, acknowledged,  
02:58 and a request for 4 is sent in an acknowledgement.  
03:02 The acknowledgement is received  
03:03 before the timer expires,  
03:05 and now the device can send segment 4.  
03:08 Or, in this case, it's the end of the transmission.  
03:11 The ability of TCP to retransmit missing segments  
03:15 makes applications that use the TCP protocol very reliable.

---

## 14.6.5 TCP Flow Control — Window Size and Acknowledgements

Flow control = how much data the destination can receive and process reliably.

TCP maintains reliability by adjusting the **rate of data flow** between source and destination for a session.
- TCP includes a **16-bit field** in the header called the **window size**.

### Window size + ACK number
- **Window size** determines how many bytes can be sent before expecting an acknowledgement.
- **Acknowledgement number** is the **next expected byte**.

In the example:
- PC B initial window size = **10,000 bytes**.
- Starting at byte 1, the last byte PC A can send without receiving an acknowledgement is byte **10,000**.
  - This is the **send window** of PC A.
- Window size is included in every TCP segment so the destination can **modify** it anytime depending on buffer availability.

### How the sliding window “moves”
The initial window is agreed during the **three-way handshake**.
The source must limit bytes sent based on the destination’s window size.

Typically, the destination will **not wait** until all 10,000 bytes are received before replying with an acknowledgement.
As bytes are processed, acknowledgements inform the source it can continue sending.

Example:
- When PC A receives an acknowledgement with ACK number **2,921** (next expected byte),
  - PC A’s send window increments **2,920 bytes**,
  - send window changes from **10,000** → **12,920**,
  - PC A can now send **another 10,000 bytes** as long as it does not exceed the new send window at 12,920.

This continual adjustment is called **sliding windows**.

If the destination’s buffer space decreases, it can **reduce window size** to tell the source to reduce how many bytes it sends without an ACK.

**Note:** Receivers often send an ACK after every **two segments**, but this can vary.
Sliding windows allow continuous sending as long as the receiver acknowledges previous segments.

---

## 14.6.6 TCP Flow Control — Maximum Segment Size (MSS)

In the example, each TCP segment carries **1,460 bytes of data**:
- This is typically the **Maximum Segment Size (MSS)** the destination can receive.
- MSS is an option in the TCP header specifying the largest amount of **data (bytes)** a device can receive in a single TCP segment.
- **MSS does not include the TCP header**.
- MSS is typically included during the **three-way handshake**.

### Common MSS calculation (IPv4 on Ethernet)
A common MSS is **1,460 bytes** when using IPv4:
- Ethernet default **MTU = 1500 bytes**
- Subtract:
  - IPv4 header = **20 bytes**
  - TCP header = **20 bytes**
- Result:
  - MSS = **1460 bytes** payload

Diagram idea:
- Ethernet | IPv4 (20 bytes) | TCP (20 bytes) | Payload (1460 bytes) | FCS  
- Total: **1500 bytes**

---

## Quick key terms (fast review)
- **Sequence Number**: first data byte number in a TCP segment.
- **ISN**: initial sequence number; typically random.
- **ACK Number**: next byte expected by the receiver.
- **Retransmission Timer**: sender timer used to resend unacknowledged data.
- **SACK**: selective acknowledgement (acknowledge received ranges so sender only retransmits missing parts).
- **Window Size**: how many bytes can be sent before an ACK is required (flow control).
- **Sliding Window**: dynamic movement/adjustment of the send window based on ACKs.
- **MSS**: max payload bytes per TCP segment (often MTU − IP header − TCP header).
- **MTU**: maximum size of an IP packet on a link (commonly 1500 bytes on Ethernet).


# 14.6 Reliability and Flow Control (TCP)

> Extracted + structured notes from your screenshots (14.6.1 → 14.6.6) + your pasted video transcripts.

---

## 14.6.1 TCP Reliability — Guaranteed and Ordered Delivery

TCP can be a better protocol for some applications because, unlike UDP:
- It **resends dropped packets**.
- It **numbers packets** so data can be delivered in the **proper order**.
- It can also help **maintain the flow of packets** so devices do not become overloaded.

### Why sequence numbers matter
Sometimes TCP segments:
- **do not arrive** at the destination, or
- **arrive out of order**.

For the original message to be understood, **all data must be received** and then **reassembled** in the original order.

**Sequence numbers** are assigned in the header of each packet to achieve this.
- The **sequence number represents the first data byte** of the TCP segment.

### ISN (Initial Sequence Number)
During session setup, an **initial sequence number (ISN)** is set:
- It represents the **starting value** of the bytes transmitted to the receiving application.
- As data is transmitted, the sequence number is **incremented by the number of bytes transmitted**.
- This byte tracking lets each segment be **uniquely identified and acknowledged**, and helps identify **missing segments**.

The ISN does **not** begin at 1 — it’s effectively a **random number** (helps prevent certain types of malicious attacks).
- For simplicity, the examples use **ISN = 1**.

---

## Figure — TCP Segments Are Reordered at the Destination

- **Different segments may take different routes.**
- **Data is divided into segments** (Segment 1, 2, 3, 4, 5, 6).
- Because of different routes, segments can **arrive out of order**.
- TCP then **reorders the segments to the original order**.

### What the receiver does
The receiving TCP process:
- places data from a segment into a **receiving buffer**,
- puts segments in the **proper sequence order**,
- then passes data to the **application layer** once reassembled.

Segments with out-of-order sequence numbers are **held** for later processing.
When missing bytes arrive, the buffered segments are processed **in order**.

---

## 14.6.2 Video — TCP Reliability: Sequence Numbers and Acknowledgements

**On-screen description (from the page):**
- One function of TCP is to ensure each segment reaches its destination.
- The destination host’s TCP services **acknowledge** data received by the source application.
- The lesson focuses on TCP **sequence numbers** and **acknowledgements**.

### Video 1 transcript (your pasted text)

00:04 - [Speaker] This video depicts a simplified example  
00:07 of TCP operations.  
00:10 It is not necessarily a realistic depiction.  
00:13 TCP is a connection-oriented protocol.  
00:16 In that, a connection is established first  
00:19 using a three-way handshake before data is sent.  
00:22 Another characteristic of TCP  
00:25 is that it's a reliable protocol.  
00:27 Two things that make it reliable are sequence numbers  
00:31 and acknowledgements.  
00:32 Every TCP segment that's sent in a TCP conversation  
00:36 gets a sequence number.  
00:38 So every byte of data is numbered  
00:41 basically in a sequential list.  
00:43 This allows a receiving host to rebuild the data  
00:46 from the ordered numbered segments.  
00:49 If data arrives out of order at the receiving end,  
00:53 the data can be put back together in the proper order  
00:56 thanks to the sequence numbers.  
00:59 Acknowledgements come into play by helping the sender know  
01:03 that the data that's being sent is actually being received.  
01:08 The way this works is, the sending host sends TCP segments  
01:12 in bytes, and the receiving host acknowledges bytes received  
01:16 by sending acknowledgements.  
01:19 There is a limit to the amount of data  
01:20 the sending host can send before it receives  
01:23 an acknowledgement from the receiver.  
01:26 This amount is called the window size.  
01:28 The window size is the total number of bytes  
01:31 sent in TCP segments that can be sent  
01:35 before receiving an acknowledgement.  
01:37 Using TCP window scaling, computers are able to achieve  
01:41 large window sizes of up to one gigabyte.  
01:45 So as the sending host sends bytes of data in TCP segments,  
01:49 the receiving host returns acknowledgements as it processes  
01:54 bytes received, and frees up its buffers.  
01:58 We can see this depicted in this graphic.  
02:01 Let's start by reading the message  
02:04 from the sending host here.  
02:06 Start with byte number one; I am sending 10 bytes.  
02:10 In this scenario, the 10 bytes is the window size.  
02:15 In reality the window size would be a lot larger  
02:18 than 10 bytes, since today window sizes are typically  
02:21 16 megabytes or larger.  
02:23 But this works nicely for this example.  
02:28 So the host is sending 10 bytes,  
02:30 starting with byte number one.  
02:32 The receiving host, the server here, says:  
02:35 I received 10 bytes, starting with byte number one.  
02:39 I expect byte 11 next.  
02:42 This is the acknowledgement.  
02:45 The server acknowledges it received the 10 bytes  
02:48 and now is expecting number 11.  
02:52 If we look down here, we can see that in this segment  
02:56 starting with sequence number one, 10 bytes have been sent.  
03:01 The receiver sends an Ack 11.  
03:05 Starting with one, 10 bytes were sent  
03:08 so the next sequence number it's expecting is an 11.  
03:12 This acknowledgement is sent back to the originating host.  
03:17 Now the originating host sends 10 more bytes  
03:21 starting with sequence number 11.  
03:24 If we were to ask ourselves, what would be the next Ack  
03:28 that the server would send back to the originating host?  
03:33 We would have to ask ourselves:  
03:34 What's the last sequence number sent?  
03:37 Starting with 11, 10 bytes were sent,  
03:41 so the last sequence number that was sent was 20.  
03:44 So the Ack would be an Ack 21.  
03:48 That's the next expected sequence number.  
03:52 You can see how sequence numbers and acknowledgements  
03:56 including the window size, make TCP a very orderly  
04:01 and reliable protocol.

---

## 14.6.3 TCP Reliability — Data Loss and Retransmission

No matter how well designed a network is, **data loss occasionally occurs**.
TCP provides methods to manage segment losses, including a mechanism to **retransmit segments for unacknowledged data**.

### SEQ + ACK work together (expectational acknowledgement)
- The **sequence (SEQ) number** identifies the **first byte of data** in the segment being transmitted.
- The **acknowledgement (ACK) number** is sent back to the source to indicate the **next byte expected**.
- This is called **expectational acknowledgement**.

### Before enhancements (why duplicates happened)
Earlier TCP behavior could only acknowledge the **next byte expected**.

Example (using segment numbers for simplicity):
- Host A sends segments **1 through 10** to host B.
- If all segments arrive **except 3 and 4**, host B replies with an acknowledgement saying the next expected is **segment 3**.
- Host A cannot know which later segments arrived, so it may resend **segments 3 through 10**.
- If the resent segments arrive successfully, segments **5 through 10** become **duplicates** → can cause **delays, congestion, and inefficiencies**.

### SACK (Selective Acknowledgement)
Many operating systems use optional **SACK**, negotiated during the **three-way handshake**.
If both hosts support SACK:
- the receiver can explicitly acknowledge which segments (bytes) were received, including **discontinuous segments**,
- the sender only needs to retransmit the **missing** data.

Example:
- Host A sends segments **1 through 10**.
- If everything arrives except **3 and 4**, host B can:
  - acknowledge segments 1 and 2 (**ACK 3**),
  - selectively acknowledge segments 5 through 10 (**SACK 5–10**).
- Host A then only needs to resend **segments 3 and 4**.

**Note:** TCP typically sends ACKs for **every other packet**, but other factors may alter this behavior.

TCP uses **timers** to decide how long to wait before resending a segment.
(The page notes a video + PDF examining TCP data loss and retransmission.)

---

## 14.6.4 Video — TCP Reliability: Data Loss and Retransmission

**On-screen description (from the page):**
- Click Play to view a lesson on TCP retransmission.
- The video shows the process of resending segments not initially received by the destination.

### Video 2 transcript (your pasted text)

00:00 - The graphic depicted in this video  
00:03 uses segment numbers in place of sequence numbers.  
00:07 TCP is a reliable protocol.  
00:09 It uses sequence numbers, and acknowledgements  
00:12 to provide that reliability.  
00:15 But, what happens when data is lost in transit?  
00:19 As a reliable protocol,  
00:21 there has to be a mechanism for resending lost data,  
00:25 so that an entire piece of data,  
00:27 like a file, or an image, or a video can be rebuilt  
00:32 from all of the segments.  
00:34 If we look at this animation,  
00:37 we can see this process in action.  
00:39 I'll press play.  
00:41 The source host here sends segment 1 and starts a timer.  
00:46 You can see the timer's running.  
00:49 The destination host receives segment 1.  
00:54 And, since it's received segment 1,  
00:56 it's going to send an acknowledgement.  
00:58 Let's see what happens.  
01:01 We can see that the destination host  
01:03 has received segment 1, acknowledges the delivery,  
01:08 and is going to send an act 2, an acknowledgement 2,  
01:12 requesting number 2.  
01:13 Why?  
01:15 It received 1, so it sends a request for 2,  
01:17 and an act 2.  
01:19 So, we'll see that get sent.  
01:21 All right, there goes the acknowledgement.  
01:23 The source receives the acknowledgement  
01:26 before the timer expires, and now can send segment 2.  
01:29 There's segment 2, it's sent,  
01:33 and as you can see, the timer has started.  
01:36 It's going to wait to get an acknowledgement.  
01:39 If it doesn't receive an acknowledgement  
01:43 from the destination before the timer expires,  
01:47 it will resend segment 2.  
01:49 Let's see this in action.  
01:52 You can see the destination has not received segment 2.  
01:57 Since it hasn't received segment 2,  
02:00 it won't send an acknowledgement number 3  
02:03 back to the device.  
02:06 It's not going to acknowledge that it received 2,  
02:09 and send an act 3 back to the source host.  
02:11 Let's see what happens.  
02:14 No acknowledgement, the timer expires.  
02:17 You can see here the timer expires.  
02:20 So, what will the source host do?  
02:22 The source host will retransmit, or resend segmeent 2,  
02:27 and restart the timer.  
02:30 This time, the information was received  
02:34 by the destination, and now  
02:36 it's going to send an act 3,  
02:38 or acknowledgement 3,  
02:40 requesting the next piece of data,  
02:42 which in this case would be number 3.  
02:47 The acknowledgement's received before the timer expires,  
02:52 and segment 3 is sent.  
02:54 Segment 3 is received, acknowledged,  
02:58 and a request for 4 is sent in an acknowledgement.  
03:02 The acknowledgement is received  
03:03 before the timer expires,  
03:05 and now the device can send segment 4.  
03:08 Or, in this case, it's the end of the transmission.  
03:11 The ability of TCP to retransmit missing segments  
03:15 makes applications that use the TCP protocol very reliable.

---

## 14.6.5 TCP Flow Control — Window Size and Acknowledgements

Flow control = how much data the destination can receive and process reliably.

TCP maintains reliability by adjusting the **rate of data flow** between source and destination for a session.
- TCP includes a **16-bit field** in the header called the **window size**.

### Window size + ACK number
- **Window size** determines how many bytes can be sent before expecting an acknowledgement.
- **Acknowledgement number** is the **next expected byte**.

In the example:
- PC B initial window size = **10,000 bytes**.
- Starting at byte 1, the last byte PC A can send without receiving an acknowledgement is byte **10,000**.
  - This is the **send window** of PC A.
- Window size is included in every TCP segment so the destination can **modify** it anytime depending on buffer availability.

### How the sliding window “moves”
The initial window is agreed during the **three-way handshake**.
The source must limit bytes sent based on the destination’s window size.

Typically, the destination will **not wait** until all 10,000 bytes are received before replying with an acknowledgement.
As bytes are processed, acknowledgements inform the source it can continue sending.

Example:
- When PC A receives an acknowledgement with ACK number **2,921** (next expected byte),
  - PC A’s send window increments **2,920 bytes**,
  - send window changes from **10,000** → **12,920**,
  - PC A can now send **another 10,000 bytes** as long as it does not exceed the new send window at 12,920.

This continual adjustment is called **sliding windows**.

If the destination’s buffer space decreases, it can **reduce window size** to tell the source to reduce how many bytes it sends without an ACK.

**Note:** Receivers often send an ACK after every **two segments**, but this can vary.
Sliding windows allow continuous sending as long as the receiver acknowledges previous segments.

---

## 14.6.6 TCP Flow Control — Maximum Segment Size (MSS)

In the example, each TCP segment carries **1,460 bytes of data**:
- This is typically the **Maximum Segment Size (MSS)** the destination can receive.
- MSS is an option in the TCP header specifying the largest amount of **data (bytes)** a device can receive in a single TCP segment.
- **MSS does not include the TCP header**.
- MSS is typically included during the **three-way handshake**.

### Common MSS calculation (IPv4 on Ethernet)
A common MSS is **1,460 bytes** when using IPv4:
- Ethernet default **MTU = 1500 bytes**
- Subtract:
  - IPv4 header = **20 bytes**
  - TCP header = **20 bytes**
- Result:
  - MSS = **1460 bytes** payload

Diagram idea:
- Ethernet | IPv4 (20 bytes) | TCP (20 bytes) | Payload (1460 bytes) | FCS  
- Total: **1500 bytes**

---

## Quick key terms (fast review)
- **Sequence Number**: first data byte number in a TCP segment.
- **ISN**: initial sequence number; typically random.
- **ACK Number**: next byte expected by the receiver.
- **Retransmission Timer**: sender timer used to resend unacknowledged data.
- **SACK**: selective acknowledgement (acknowledge received ranges so sender only retransmits missing parts).
- **Window Size**: how many bytes can be sent before an ACK is required (flow control).
- **Sliding Window**: dynamic movement/adjustment of the send window based on ACKs.
- **MSS**: max payload bytes per TCP segment (often MTU − IP header − TCP header).
- **MTU**: maximum size of an IP packet on a link (commonly 1500 bytes on Ethernet).



---

## 14.6.7 TCP Flow Control — Congestion Avoidance

When **congestion** occurs on a network, it can result in packets being **discarded by an overloaded router**.
If packets containing TCP segments do not reach the destination, they are left **unacknowledged**.

By determining the rate at which TCP segments are sent but **not acknowledged**, the source can assume a certain level of network congestion.

### Why congestion can get worse
Whenever there is congestion, retransmission of lost TCP segments from the source will occur.
If retransmission is not properly controlled:
- additional retransmissions can make congestion **even worse**
- not only are new packets introduced, but retransmitted packets that were lost also add to congestion

To avoid and control congestion, TCP employs several **congestion-handling mechanisms, timers, and algorithms**.

### What the sender does when it senses congestion
If the source determines that TCP segments are either:
- not being acknowledged, or
- not being acknowledged in a timely manner,

then it can **reduce the number of bytes it sends before receiving an acknowledgement**.

**Key note (important):**  
It is the **source** that reduces the number of **unacknowledged bytes** it sends — **not** the destination’s window size.

#### Figure — TCP Congestion Control (simplified)
- PC A: “I’m not getting the acknowledgements I expect from PC B so I will reduce the number of bytes I send before getting an acknowledgement.”
- Example shows lost TCP segments and the sender reducing how much it sends before expecting ACKs.

*Footnote from the figure:*  
Acknowledgement numbers are for the **next expected byte** (not for a segment). Segment numbers are simplified for illustration.

*Course note:* Details of real congestion-handling mechanisms/timers/algorithms are beyond this course scope.

---

## 14.6.8 Check Your Understanding — Reliability and Flow Control

### Question 1
**What field is used by the destination host to reassemble segments into the original order?**
- Source Port  
- Destination Port  
- Window Size  
- Control Bits  
- Sequence Number  

> **Answer:** Sequence Number

### Question 2
**What field is used to provide flow control?**
- Source Port  
- Control Bits  
- Destination Port  
- Sequence Number  
- Window Size  

> **Answer:** Window Size

### Question 3
**What happens when a sending host senses there is congestion?**
- The sending host reduces the number of bytes it sends before receiving an acknowledgement from the destination host.  
- The receiving host increases the number of bytes it sends before receiving an acknowledgement from the sending host.  
- The receiving host reduces the number of bytes it sends before receiving an acknowledgement from the sending host.  
- The sending host increases the number of bytes it sends before receiving an acknowledgement from the destination host.  

> **Answer:** The sending host reduces the number of bytes it sends before receiving an acknowledgement from the destination host.

---

# 14.7 UDP Communication

## 14.7.1 UDP Low Overhead versus Reliability

UDP is ideal for communications that need to be **fast**, like **VoIP**.

Key points:
- UDP **does not establish a connection**.
- UDP provides **low-overhead** data transport because it has:
  - a **small datagram header**
  - **no network management traffic**

**Figure callout:** “UDP does not establish a connection before sending data.”

---

## 14.7.2 UDP Datagram Reassembly

Like TCP segments, when UDP datagrams are sent to a destination, they often take different paths and arrive in the **wrong order**.

However:
- UDP does **not** track sequence numbers the way TCP does.
- UDP has **no way** to reorder datagrams into their original transmission order.

Therefore UDP:
- reassembles data in the **order it was received**
- forwards it to the **application**

If the data sequence is important, the **application** must identify the proper sequence and determine how the data should be processed.

### Figure — UDP: Connectionless and Unreliable
- Different datagrams may take different routes.
- Data is divided into datagrams.
- Having taken different routes, datagrams arrive out of order.
- **Out-of-order datagrams are not re-ordered.**
- **Lost datagrams are not re-sent.**

---

## 14.7.3 UDP Server Processes and Requests

UDP-based server applications are assigned **well-known or registered port numbers** (similar to TCP-based applications).

When these processes are running on a server:
- they accept data matched to their assigned port number
- when UDP receives a datagram destined for one of these ports, it forwards the application data to the correct application based on the **port number**

### Figure — UDP Server Listening for Requests
- Client DNS requests will be received on **Port 53**
- Client RADIUS requests will be received on **Port 1812**

**Note:** The Remote Authentication Dial-In User Service (**RADIUS**) server shown provides authentication, authorization, and accounting services to manage user access. (Operation of RADIUS is beyond the scope of this course.)


# 14.6 Reliability and Flow Control (TCP)

> Extracted + structured notes from your screenshots (14.6.1 → 14.6.6) + your pasted video transcripts.

---

## 14.6.1 TCP Reliability — Guaranteed and Ordered Delivery

TCP can be a better protocol for some applications because, unlike UDP:
- It **resends dropped packets**.
- It **numbers packets** so data can be delivered in the **proper order**.
- It can also help **maintain the flow of packets** so devices do not become overloaded.

### Why sequence numbers matter
Sometimes TCP segments:
- **do not arrive** at the destination, or
- **arrive out of order**.

For the original message to be understood, **all data must be received** and then **reassembled** in the original order.

**Sequence numbers** are assigned in the header of each packet to achieve this.
- The **sequence number represents the first data byte** of the TCP segment.

### ISN (Initial Sequence Number)
During session setup, an **initial sequence number (ISN)** is set:
- It represents the **starting value** of the bytes transmitted to the receiving application.
- As data is transmitted, the sequence number is **incremented by the number of bytes transmitted**.
- This byte tracking lets each segment be **uniquely identified and acknowledged**, and helps identify **missing segments**.

The ISN does **not** begin at 1 — it’s effectively a **random number** (helps prevent certain types of malicious attacks).
- For simplicity, the examples use **ISN = 1**.

---

## Figure — TCP Segments Are Reordered at the Destination

- **Different segments may take different routes.**
- **Data is divided into segments** (Segment 1, 2, 3, 4, 5, 6).
- Because of different routes, segments can **arrive out of order**.
- TCP then **reorders the segments to the original order**.

### What the receiver does
The receiving TCP process:
- places data from a segment into a **receiving buffer**,
- puts segments in the **proper sequence order**,
- then passes data to the **application layer** once reassembled.

Segments with out-of-order sequence numbers are **held** for later processing.
When missing bytes arrive, the buffered segments are processed **in order**.

---

## 14.6.2 Video — TCP Reliability: Sequence Numbers and Acknowledgements

**On-screen description (from the page):**
- One function of TCP is to ensure each segment reaches its destination.
- The destination host’s TCP services **acknowledge** data received by the source application.
- The lesson focuses on TCP **sequence numbers** and **acknowledgements**.

### Video 1 transcript (your pasted text)

00:04 - [Speaker] This video depicts a simplified example  
00:07 of TCP operations.  
00:10 It is not necessarily a realistic depiction.  
00:13 TCP is a connection-oriented protocol.  
00:16 In that, a connection is established first  
00:19 using a three-way handshake before data is sent.  
00:22 Another characteristic of TCP  
00:25 is that it's a reliable protocol.  
00:27 Two things that make it reliable are sequence numbers  
00:31 and acknowledgements.  
00:32 Every TCP segment that's sent in a TCP conversation  
00:36 gets a sequence number.  
00:38 So every byte of data is numbered  
00:41 basically in a sequential list.  
00:43 This allows a receiving host to rebuild the data  
00:46 from the ordered numbered segments.  
00:49 If data arrives out of order at the receiving end,  
00:53 the data can be put back together in the proper order  
00:56 thanks to the sequence numbers.  
00:59 Acknowledgements come into play by helping the sender know  
01:03 that the data that's being sent is actually being received.  
01:08 The way this works is, the sending host sends TCP segments  
01:12 in bytes, and the receiving host acknowledges bytes received  
01:16 by sending acknowledgements.  
01:19 There is a limit to the amount of data  
01:20 the sending host can send before it receives  
01:23 an acknowledgement from the receiver.  
01:26 This amount is called the window size.  
01:28 The window size is the total number of bytes  
01:31 sent in TCP segments that can be sent  
01:35 before receiving an acknowledgement.  
01:37 Using TCP window scaling, computers are able to achieve  
01:41 large window sizes of up to one gigabyte.  
01:45 So as the sending host sends bytes of data in TCP segments,  
01:49 the receiving host returns acknowledgements as it processes  
01:54 bytes received, and frees up its buffers.  
01:58 We can see this depicted in this graphic.  
02:01 Let's start by reading the message  
02:04 from the sending host here.  
02:06 Start with byte number one; I am sending 10 bytes.  
02:10 In this scenario, the 10 bytes is the window size.  
02:15 In reality the window size would be a lot larger  
02:18 than 10 bytes, since today window sizes are typically  
02:21 16 megabytes or larger.  
02:23 But this works nicely for this example.  
02:28 So the host is sending 10 bytes,  
02:30 starting with byte number one.  
02:32 The receiving host, the server here, says:  
02:35 I received 10 bytes, starting with byte number one.  
02:39 I expect byte 11 next.  
02:42 This is the acknowledgement.  
02:45 The server acknowledges it received the 10 bytes  
02:48 and now is expecting number 11.  
02:52 If we look down here, we can see that in this segment  
02:56 starting with sequence number one, 10 bytes have been sent.  
03:01 The receiver sends an Ack 11.  
03:05 Starting with one, 10 bytes were sent  
03:08 so the next sequence number it's expecting is an 11.  
03:12 This acknowledgement is sent back to the originating host.  
03:17 Now the originating host sends 10 more bytes  
03:21 starting with sequence number 11.  
03:24 If we were to ask ourselves, what would be the next Ack  
03:28 that the server would send back to the originating host?  
03:33 We would have to ask ourselves:  
03:34 What's the last sequence number sent?  
03:37 Starting with 11, 10 bytes were sent,  
03:41 so the last sequence number that was sent was 20.  
03:44 So the Ack would be an Ack 21.  
03:48 That's the next expected sequence number.  
03:52 You can see how sequence numbers and acknowledgements  
03:56 including the window size, make TCP a very orderly  
04:01 and reliable protocol.

---

## 14.6.3 TCP Reliability — Data Loss and Retransmission

No matter how well designed a network is, **data loss occasionally occurs**.
TCP provides methods to manage segment losses, including a mechanism to **retransmit segments for unacknowledged data**.

### SEQ + ACK work together (expectational acknowledgement)
- The **sequence (SEQ) number** identifies the **first byte of data** in the segment being transmitted.
- The **acknowledgement (ACK) number** is sent back to the source to indicate the **next byte expected**.
- This is called **expectational acknowledgement**.

### Before enhancements (why duplicates happened)
Earlier TCP behavior could only acknowledge the **next byte expected**.

Example (using segment numbers for simplicity):
- Host A sends segments **1 through 10** to host B.
- If all segments arrive **except 3 and 4**, host B replies with an acknowledgement saying the next expected is **segment 3**.
- Host A cannot know which later segments arrived, so it may resend **segments 3 through 10**.
- If the resent segments arrive successfully, segments **5 through 10** become **duplicates** → can cause **delays, congestion, and inefficiencies**.

### SACK (Selective Acknowledgement)
Many operating systems use optional **SACK**, negotiated during the **three-way handshake**.
If both hosts support SACK:
- the receiver can explicitly acknowledge which segments (bytes) were received, including **discontinuous segments**,
- the sender only needs to retransmit the **missing** data.

Example:
- Host A sends segments **1 through 10**.
- If everything arrives except **3 and 4**, host B can:
  - acknowledge segments 1 and 2 (**ACK 3**),
  - selectively acknowledge segments 5 through 10 (**SACK 5–10**).
- Host A then only needs to resend **segments 3 and 4**.

**Note:** TCP typically sends ACKs for **every other packet**, but other factors may alter this behavior.

TCP uses **timers** to decide how long to wait before resending a segment.
(The page notes a video + PDF examining TCP data loss and retransmission.)

---

## 14.6.4 Video — TCP Reliability: Data Loss and Retransmission

**On-screen description (from the page):**
- Click Play to view a lesson on TCP retransmission.
- The video shows the process of resending segments not initially received by the destination.

### Video 2 transcript (your pasted text)

00:00 - The graphic depicted in this video  
00:03 uses segment numbers in place of sequence numbers.  
00:07 TCP is a reliable protocol.  
00:09 It uses sequence numbers, and acknowledgements  
00:12 to provide that reliability.  
00:15 But, what happens when data is lost in transit?  
00:19 As a reliable protocol,  
00:21 there has to be a mechanism for resending lost data,  
00:25 so that an entire piece of data,  
00:27 like a file, or an image, or a video can be rebuilt  
00:32 from all of the segments.  
00:34 If we look at this animation,  
00:37 we can see this process in action.  
00:39 I'll press play.  
00:41 The source host here sends segment 1 and starts a timer.  
00:46 You can see the timer's running.  
00:49 The destination host receives segment 1.  
00:54 And, since it's received segment 1,  
00:56 it's going to send an acknowledgement.  
00:58 Let's see what happens.  
01:01 We can see that the destination host  
01:03 has received segment 1, acknowledges the delivery,  
01:08 and is going to send an act 2, an acknowledgement 2,  
01:12 requesting number 2.  
01:13 Why?  
01:15 It received 1, so it sends a request for 2,  
01:17 and an act 2.  
01:19 So, we'll see that get sent.  
01:21 All right, there goes the acknowledgement.  
01:23 The source receives the acknowledgement  
01:26 before the timer expires, and now can send segment 2.  
01:29 There's segment 2, it's sent,  
01:33 and as you can see, the timer has started.  
01:36 It's going to wait to get an acknowledgement.  
01:39 If it doesn't receive an acknowledgement  
01:43 from the destination before the timer expires,  
01:47 it will resend segment 2.  
01:49 Let's see this in action.  
01:52 You can see the destination has not received segment 2.  
01:57 Since it hasn't received segment 2,  
02:00 it won't send an acknowledgement number 3  
02:03 back to the device.  
02:06 It's not going to acknowledge that it received 2,  
02:09 and send an act 3 back to the source host.  
02:11 Let's see what happens.  
02:14 No acknowledgement, the timer expires.  
02:17 You can see here the timer expires.  
02:20 So, what will the source host do?  
02:22 The source host will retransmit, or resend segmeent 2,  
02:27 and restart the timer.  
02:30 This time, the information was received  
02:34 by the destination, and now  
02:36 it's going to send an act 3,  
02:38 or acknowledgement 3,  
02:40 requesting the next piece of data,  
02:42 which in this case would be number 3.  
02:47 The acknowledgement's received before the timer expires,  
02:52 and segment 3 is sent.  
02:54 Segment 3 is received, acknowledged,  
02:58 and a request for 4 is sent in an acknowledgement.  
03:02 The acknowledgement is received  
03:03 before the timer expires,  
03:05 and now the device can send segment 4.  
03:08 Or, in this case, it's the end of the transmission.  
03:11 The ability of TCP to retransmit missing segments  
03:15 makes applications that use the TCP protocol very reliable.

---

## 14.6.5 TCP Flow Control — Window Size and Acknowledgements

Flow control = how much data the destination can receive and process reliably.

TCP maintains reliability by adjusting the **rate of data flow** between source and destination for a session.
- TCP includes a **16-bit field** in the header called the **window size**.

### Window size + ACK number
- **Window size** determines how many bytes can be sent before expecting an acknowledgement.
- **Acknowledgement number** is the **next expected byte**.

In the example:
- PC B initial window size = **10,000 bytes**.
- Starting at byte 1, the last byte PC A can send without receiving an acknowledgement is byte **10,000**.
  - This is the **send window** of PC A.
- Window size is included in every TCP segment so the destination can **modify** it anytime depending on buffer availability.

### How the sliding window “moves”
The initial window is agreed during the **three-way handshake**.
The source must limit bytes sent based on the destination’s window size.

Typically, the destination will **not wait** until all 10,000 bytes are received before replying with an acknowledgement.
As bytes are processed, acknowledgements inform the source it can continue sending.

Example:
- When PC A receives an acknowledgement with ACK number **2,921** (next expected byte),
  - PC A’s send window increments **2,920 bytes**,
  - send window changes from **10,000** → **12,920**,
  - PC A can now send **another 10,000 bytes** as long as it does not exceed the new send window at 12,920.

This continual adjustment is called **sliding windows**.

If the destination’s buffer space decreases, it can **reduce window size** to tell the source to reduce how many bytes it sends without an ACK.

**Note:** Receivers often send an ACK after every **two segments**, but this can vary.
Sliding windows allow continuous sending as long as the receiver acknowledges previous segments.

---

## 14.6.6 TCP Flow Control — Maximum Segment Size (MSS)

In the example, each TCP segment carries **1,460 bytes of data**:
- This is typically the **Maximum Segment Size (MSS)** the destination can receive.
- MSS is an option in the TCP header specifying the largest amount of **data (bytes)** a device can receive in a single TCP segment.
- **MSS does not include the TCP header**.
- MSS is typically included during the **three-way handshake**.

### Common MSS calculation (IPv4 on Ethernet)
A common MSS is **1,460 bytes** when using IPv4:
- Ethernet default **MTU = 1500 bytes**
- Subtract:
  - IPv4 header = **20 bytes**
  - TCP header = **20 bytes**
- Result:
  - MSS = **1460 bytes** payload

Diagram idea:
- Ethernet | IPv4 (20 bytes) | TCP (20 bytes) | Payload (1460 bytes) | FCS  
- Total: **1500 bytes**

---

## Quick key terms (fast review)
- **Sequence Number**: first data byte number in a TCP segment.
- **ISN**: initial sequence number; typically random.
- **ACK Number**: next byte expected by the receiver.
- **Retransmission Timer**: sender timer used to resend unacknowledged data.
- **SACK**: selective acknowledgement (acknowledge received ranges so sender only retransmits missing parts).
- **Window Size**: how many bytes can be sent before an ACK is required (flow control).
- **Sliding Window**: dynamic movement/adjustment of the send window based on ACKs.
- **MSS**: max payload bytes per TCP segment (often MTU − IP header − TCP header).
- **MTU**: maximum size of an IP packet on a link (commonly 1500 bytes on Ethernet).



---

## 14.6.7 TCP Flow Control — Congestion Avoidance

When **congestion** occurs on a network, it can result in packets being **discarded by an overloaded router**.
If packets containing TCP segments do not reach the destination, they are left **unacknowledged**.

By determining the rate at which TCP segments are sent but **not acknowledged**, the source can assume a certain level of network congestion.

### Why congestion can get worse
Whenever there is congestion, retransmission of lost TCP segments from the source will occur.
If retransmission is not properly controlled:
- additional retransmissions can make congestion **even worse**
- not only are new packets introduced, but retransmitted packets that were lost also add to congestion

To avoid and control congestion, TCP employs several **congestion-handling mechanisms, timers, and algorithms**.

### What the sender does when it senses congestion
If the source determines that TCP segments are either:
- not being acknowledged, or
- not being acknowledged in a timely manner,

then it can **reduce the number of bytes it sends before receiving an acknowledgement**.

**Key note (important):**  
It is the **source** that reduces the number of **unacknowledged bytes** it sends — **not** the destination’s window size.

#### Figure — TCP Congestion Control (simplified)
- PC A: “I’m not getting the acknowledgements I expect from PC B so I will reduce the number of bytes I send before getting an acknowledgement.”
- Example shows lost TCP segments and the sender reducing how much it sends before expecting ACKs.

*Footnote from the figure:*  
Acknowledgement numbers are for the **next expected byte** (not for a segment). Segment numbers are simplified for illustration.

*Course note:* Details of real congestion-handling mechanisms/timers/algorithms are beyond this course scope.

---

## 14.6.8 Check Your Understanding — Reliability and Flow Control

### Question 1
**What field is used by the destination host to reassemble segments into the original order?**
- Source Port  
- Destination Port  
- Window Size  
- Control Bits  
- Sequence Number  

> **Answer:** Sequence Number

### Question 2
**What field is used to provide flow control?**
- Source Port  
- Control Bits  
- Destination Port  
- Sequence Number  
- Window Size  

> **Answer:** Window Size

### Question 3
**What happens when a sending host senses there is congestion?**
- The sending host reduces the number of bytes it sends before receiving an acknowledgement from the destination host.  
- The receiving host increases the number of bytes it sends before receiving an acknowledgement from the sending host.  
- The receiving host reduces the number of bytes it sends before receiving an acknowledgement from the sending host.  
- The sending host increases the number of bytes it sends before receiving an acknowledgement from the destination host.  

> **Answer:** The sending host reduces the number of bytes it sends before receiving an acknowledgement from the destination host.

---

# 14.7 UDP Communication

## 14.7.1 UDP Low Overhead versus Reliability

UDP is ideal for communications that need to be **fast**, like **VoIP**.

Key points:
- UDP **does not establish a connection**.
- UDP provides **low-overhead** data transport because it has:
  - a **small datagram header**
  - **no network management traffic**

**Figure callout:** “UDP does not establish a connection before sending data.”

---

## 14.7.2 UDP Datagram Reassembly

Like TCP segments, when UDP datagrams are sent to a destination, they often take different paths and arrive in the **wrong order**.

However:
- UDP does **not** track sequence numbers the way TCP does.
- UDP has **no way** to reorder datagrams into their original transmission order.

Therefore UDP:
- reassembles data in the **order it was received**
- forwards it to the **application**

If the data sequence is important, the **application** must identify the proper sequence and determine how the data should be processed.

### Figure — UDP: Connectionless and Unreliable
- Different datagrams may take different routes.
- Data is divided into datagrams.
- Having taken different routes, datagrams arrive out of order.
- **Out-of-order datagrams are not re-ordered.**
- **Lost datagrams are not re-sent.**

---

## 14.7.3 UDP Server Processes and Requests

UDP-based server applications are assigned **well-known or registered port numbers** (similar to TCP-based applications).

When these processes are running on a server:
- they accept data matched to their assigned port number
- when UDP receives a datagram destined for one of these ports, it forwards the application data to the correct application based on the **port number**

### Figure — UDP Server Listening for Requests
- Client DNS requests will be received on **Port 53**
- Client RADIUS requests will be received on **Port 1812**

**Note:** The Remote Authentication Dial-In User Service (**RADIUS**) server shown provides authentication, authorization, and accounting services to manage user access. (Operation of RADIUS is beyond the scope of this course.)



---

## 14.7.4 UDP Client Processes

Client-server communication is initiated by a **client application** requesting data from a **server process**.

### How UDP chooses ports (client side)
- The UDP client process **dynamically selects a port number** from the port range and uses it as the **source port** for the conversation.
- The **destination port** is usually the **well-known** or **registered** port number assigned to the server process.

After the client selects the source and destination ports:
- The same pair of ports is used in the UDP header of **all datagrams** in the transaction.
- When the server replies to the client, the **source and destination ports are reversed** in the returning datagrams.

### Example shown (DNS + RADIUS on the same server)
**Server services**
- DNS: **Port 53**
- RADIUS: **Port 1812**

**Clients sending UDP requests**
- Client 1 (DNS request): **Source Port 49152 → Destination Port 53**
- Client 2 (RADIUS auth request): **Source Port 51152 → Destination Port 1812**

#### UDP request destination ports (key idea)
Clients request the UDP server to use **well-known / registered ports** as the **destination port**.

#### UDP request source ports (key idea)
Clients typically use **random/dynamic ports** as the **source port** (example: 49152 and 51152).

#### UDP response destination (key idea)
When responding, the server uses the **client’s request source port** as the **destination port**:
- Server DNS response: **Source Port 53 → Destination Port 49152**
- Server RADIUS response: **Source Port 1812 → Destination Port 51152**

#### UDP response source ports (key idea)
The **source ports** in the server responses are the **original destination ports** from the requests (well-known/registered ports):
- DNS uses **53** as source
- RADIUS uses **1812** as source

---

## 14.7.5 Check Your Understanding — UDP Communication

### Question 1
**Why is UDP desirable for protocols that make a simple request and reply transactions?**
- Reliability  
- Flow Control  
- Low overhead  
- Same-order delivery  

> **Answer:** Low overhead

### Question 2
**Which UDP datagram reassembly statement is true?**
- UDP does not reassemble the data.  
- UDP reassembles the data in the order that it was received.  
- UDP reassembles the data using sequence numbers.  
- UDP reassembles the data using control bits.  

> **Answer:** UDP reassembles the data in the order that it was received.

### Question 3
**Which of the following would be valid source and destination ports for a host connecting to a DNS server?**
- Source: 53, Destination: 49152  
- Source: 49152, Destination: 1812  
- Source: 1812, Destination: 49152  
- Source: 49152, Destination: 53  

> **Answer:** Source: 49152, Destination: 53

---

# 14.8 Module Practice and Quiz

## 14.8.1 Packet Tracer — TCP and UDP Communications

In this activity, you explore:
- TCP vs UDP behavior
- Multiplexing (multiple conversations sharing the network)
- How **port numbers** determine which local application requested/sent the data

> Packet Tracer does **not** score this activity.

### Objectives (from the lab)
- **Part 1:** Generate Network Traffic in Simulation Mode  
- **Part 2:** Examine the Functionality of the TCP and UDP Protocols  

---

## Packet Tracer Lab — Quick Walkthrough (structured)

### Part 1 — Generate Traffic in Simulation Mode and View Multiplexing

#### Step 1 — Populate ARP tables (reduce noise later)
1. Click **MultiServer** → **Desktop** tab → **Command Prompt**
2. Run:
   - `ping -n 1 192.168.1.255`
3. Wait a few seconds (devices reply), then close MultiServer window.

#### Step 2 — Generate HTTP traffic
1. Switch to **Simulation mode**
2. Click **HTTP Client** → **Desktop** → **Web Browser**
3. URL: `192.168.1.254` → click **Go**
4. PDUs (envelopes) appear → minimize HTTP Client window (don’t close)

#### Step 3 — Generate FTP traffic
1. Click **FTP Client** → **Desktop** → **Command Prompt**
2. Run:
   - `ftp 192.168.1.254`
3. PDUs appear → minimize (don’t close)

#### Step 4 — Generate DNS traffic
1. Click **DNS Client** → **Desktop** → **Command Prompt**
2. Run:
   - `nslookup multiserver.pt.ptu`
3. A PDU appears → minimize (don’t close)

#### Step 5 — Generate Email traffic
1. Click **E-Mail Client** → **Desktop** → **E-Mail**
2. Compose:
   - To: `user@multiserver.pt.ptu`
   - Subject: (your text)
   - Body: (your text)
3. Click **Send** → minimize (don’t close)

#### Step 6 — Verify PDUs exist
You should see PDU entries in the simulation panel for each client.

#### Step 7 — Observe multiplexing with Capture/Forward
1. Click **Capture/Forward** once → PDUs move to the switch
2. Click **Capture/Forward** ~6 times → observe traffic from different hosts

**Question prompts**
- Only one PDU crosses a wire (per direction) at a time — what is this called?
  - Suggested answer: **multiplexing** (multiple conversations share the network medium)
- What do different PDU colors mean?
  - Suggested answer: **different protocols / different PDU types** in the event list

---

### Part 2 — Examine TCP and UDP Protocol Functionality

#### Step 1 — HTTP (TCP) traffic details
1. Click **Reset Simulation**
2. Edit Filters → Show None → select **HTTP** and **TCP**
3. On HTTP Client browser, go to `192.168.1.254`
4. Click **Capture/Forward** until an HTTP PDU appears

**Question prompts**
- Why did it take so long for the HTTP PDU to appear?
  - Suggested answer: TCP must establish a connection (3-way handshake) and may perform ARP first.

Open the PDU → **Outbound PDU Details** → scroll to the **TCP** section.

**More questions**
- What is the section labeled?
  - Suggested answer: **TCP**
- Are these communications reliable?
  - Suggested answer: **Yes — TCP is reliable**
- Record: SRC PORT, DEST PORT, SEQUENCE NUM, ACK NUM
  - (Values vary in Packet Tracer)

**TCP Flags reminder (flag bits mapping used in the lab)**
- URG | ACK | PSH | RST | SYN | FIN

Question: Which TCP flags are set in this PDU?
- Typical pattern:
  - First TCP PDU often sets **SYN** (connection start),
  - Reply often sets **SYN + ACK**,
  - Next often sets **ACK**.

Continue Capture/Forward until a PDU with a checkmark returns to HTTP Client → open **Inbound PDU Details**.
- Compare ports/sequence numbers: ports are typically **reversed** on the return traffic; sequence/ack values advance.

---

#### Step 2 — FTP (TCP) traffic details
1. On FTP Client Command Prompt:
   - `ftp 192.168.1.254`
2. Filters: show only **FTP** and **TCP**
3. Capture/Forward → open the second PDU → outbound details → TCP section

**Question prompts**
- Reliable?
  - Suggested answer: **Yes — TCP**
- Record SRC PORT, DEST PORT, SEQ, ACK (values vary)
- Flag field value?
  - Often shows a handshake/ACK pattern depending on the step.

Keep forwarding until a PDU returns to FTP Client with a checkmark → open it.
- Compare how ports/sequence numbers change between outbound/inbound and between PDUs.

A later PDU of a different color returns:
- Open inbound details and scroll past TCP section.
- “What is the message from the server?”
  - (Usually an FTP server banner/status message; record exactly what Packet Tracer shows.)

---

#### Step 3 — DNS (UDP) traffic details
1. Recreate DNS traffic (as in Part 1)
2. Filters: show only **DNS** and **UDP**
3. Open the DNS PDU

**Question prompts**
- What is the Layer 4 protocol?
  - **UDP**
- Reliable?
  - **No — UDP is not reliable**
- Record SRC PORT and DEST PORT (values vary; dest is commonly 53)

Why are there no sequence/ack numbers?
- **UDP has no sequencing/acknowledgement fields** like TCP.

Forward until the reply PDU returns (checkmark) → open inbound details:
- Ports are typically **reversed** on the return traffic.

“What is the last section of the PDU called, and what IP address was returned for `multiserver.pt.ptu`?”
- Last section is typically **DNS**
- IP address depends on the Packet Tracer file (record what you see).

---

#### Step 4 — Email (TCP) traffic details
1. Recreate email traffic (as in Part 1)
2. Filters: show only **POP3**, **SMTP**, and **TCP**
3. Open the first PDU → outbound details → last section

**Question prompts**
- What transport layer protocol does email traffic use?
  - **TCP**
- Reliable?
  - **Yes (TCP)**
- Record SRC PORT, DEST PORT, SEQ, ACK, flag value (varies)

Forward until a TCP PDU returns to the E-Mail Client (checkmark) → open inbound details:
- Compare ports/sequence numbers (typically reversed + updated values)

Final questions from the lab:
- What email protocol is associated with TCP port **25**?
  - **SMTP**
- What protocol is associated with TCP port **110**?
  - **POP3**


14.8.2 What did I learn in this module?
Transportation of Data

The transport layer is the link between the application layer and the lower layers that are responsible for network transmission. The transport layer is responsible for logical communications between application running on different hosts. The transport layer includes TCP and UDP. Transport layer protocols specify how to transfer messages between hosts and is responsible for managing reliability requirements of a conversation. The transport layer is responsible for tracking conversations (sessions), segmenting data and reassembling segments, adding header information, identifying applications, and conversation multiplexing. TCP is stateful, reliable, acknowledges data, resends lost data, and delivers data in sequenced order. Use TCP for email and the web. UDP is stateless, fast, has low overhead, does not requires acknowledgments, do not resend lost data, and delivers data in the order it arrives. Use UDP for VoIP and DNS.

TCP Overview

TCP establishes sessions, ensures reliability, provides same-order delivery, and supports flow control. A TCP segment adds 20 bytes of overhead as header information when encapsulating the application layer data. TCP header fields are the Source and Destination Ports, Sequence Number, Acknowledgment Number, Header Length, Reserved, Control Bits, Window Size, Checksum, and Urgent. Applications that use TCP are HTTP, FTP, SMTP, and Telnet.

UDP Overview

UDP reconstructs data in the order it is received, lost segments are not resent, no session establishment, and UDP does not inform the sender of resource availability. UDP header fields are Source and Destination Ports, Length, and Checksum. Applications that use UDP are DHCP, DNS, SNMP, TFTP, VoIP, and video conferencing.

Port Numbers

The TCP and UDP transport layer protocols use port numbers to manage multiple simultaneous conversations. This is why the TCP and UDP header fields identify a source and destination application port number. The source and destination ports are placed within the segment. The segments are then encapsulated within an IP packet. The IP packet contains the IP address of the source and destination. The combination of the source IP address and source port number, or the destination IP address and destination port number is known as a socket. The socket is used to identify the server and service being requested by the client. There is a range of port numbers from 0 through 65535. This range is divided into groups: Well-known Ports, Registered Ports, Private and/or Dynamic Ports. There are a few Well-known Port numbers that are reserved for common applications such at FTP, SSH, DNS, HTTP and others. Sometimes it is necessary to know which active TCP connections are open and running on a networked host. Netstat is an important network utility that can be used to verify those connections.

TCP Communications Process

Each application process running on a server is configured to use a port number. The port number is either automatically assigned or configured manually by a system administrator. TCP server processes are as follows: clients sending TCP requests, requesting destination ports, requesting source ports, responding to destination port and source port requests. To terminate a single conversation supported by TCP, four exchanges are needed to end both sessions. Either the client or the server can initiate the termination. The three-way handshake establishes that the destination device is present on the network, verifies that the destination device has an active service and accepting requests on the destination port number that the initiating client intends to use, and informs the destination device that the source client intends to establish a communication session on that port number. The six control bits flags are: URG, ACK, PSH, RST, SYN, and FIN.

Reliability and Flow Control

For the original message to be understood by the recipient, all the data must be received and the data in these segments must be reassembled into the original order. Sequence numbers are assigned in the header of each packet. No matter how well designed a network is, data loss occasionally occurs. TCP provides ways to manage segment losses. There is a mechanism to retransmit segments for unacknowledged data. Host operating systems today typically employ an optional TCP feature called selective acknowledgment (SACK), negotiated during the three-way handshake. If both hosts support SACK, the receiver can explicitly acknowledge which segments (bytes) were received including any discontinuous segments. The sending host would therefore only need to retransmit the missing data. Flow control helps maintain the reliability of TCP transmission by adjusting the rate of data flow between source and destination. To accomplish this, the TCP header includes a 16-bit field called the window size. The process of the destination sending acknowledgments as it processes bytes received and the continual adjustment of the source's send window is known as sliding windows. A source might be transmitting 1,460 bytes of data within each TCP segment. This is the typical MSS that a destination device can receive. To avoid and control congestion, TCP employs several congestion handling mechanisms. It is the source that is reducing the number of unacknowledged bytes it sends and not the window size determined by the destination.

UDP Communication

UDP is a simple protocol that provides the basic transport layer functions. When UDP datagrams are sent to a destination, they often take different paths and arrive in the wrong order. UDP does not track sequence numbers the way TCP does. UDP has no way to reorder the datagrams into their transmission order. UDP simply reassembles the data in the order that it was received and forwards it to the application. If the data sequence is important to the application, the application must identify the proper sequence and determine how the data should be processed. UDP-based server applications are assigned well-known or registered port numbers. When UDP receives a datagram destined for one of these ports, it forwards the application data to the appropriate application based on its port number. The UDP client process dynamically selects a port number from the range of port numbers and uses this as the source port for the conversation. The destination port is usually the well-known or registered port number assigned to the server process. After a client has selected the source and destination ports, the same pair of ports are used in the header of all datagrams used in the transaction. For the data returning to the client from the server, the source and destination port numbers in the datagram header are reversed.

14.8.3 Module Quiz – Transport Layer (With Answers ✅)
Q1

Which transport layer feature is used to establish a connection-oriented session?
✅ Answer: TCP 3-way handshake

Q2

What is the complete range of TCP and UDP well-known ports?
✅ Answer: 0 to 1023

Q3

What is a socket?
✅ Answer: The combination of a source IP address and port number or a destination IP address and port number

Q4

How does a networked server manage requests from multiple clients for different services?
✅ Answer: Each request has a combination of source and destination port numbers, coming from a unique IP address.

Q5

What happens if part of an FTP message is not delivered to the destination?
✅ Answer: The part of the FTP message that was lost is re-sent.

Q6

What type of applications are best suited for using UDP?
✅ Answer: Applications that are sensitive to delay

Q7

Network congestion caused loss of TCP segments. What is one way TCP addresses this?
✅ Answer: The source decreases the amount of data that it transmits before it receives an acknowledgement from the destination.

Q8

Which two operations are provided by TCP but not by UDP? (Choose two.)
✅ Answers:

Retransmitting any unacknowledged data

Acknowledging received data

Q9

What is the purpose of using a source port number in a TCP communication?
✅ Answer: To keep track of multiple conversations between devices

Q10

Which two flags in the TCP header are used in a TCP three-way handshake? (Choose two.)
✅ Answers: SYN and ACK

Q11

What TCP mechanism enhances performance by allowing continuous sending as long as ACKs are received?
✅ Answer: Sliding window

Q12

Which action is performed by a client when establishing communication with a server via UDP?
✅ Answer: The client randomly selects a source port number.

Q13

Which two services use UDP for fast transmission and low overhead? (Choose two.)
✅ Answers: DNS and VoIP

Q14

Which number or set of numbers represents a socket?
✅ Answer: 192.168.1.1:80

Q15

What is a responsibility of transport layer protocols?
✅ Answer: Tracking individual conversations
