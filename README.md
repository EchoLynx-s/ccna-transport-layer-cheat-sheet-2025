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

