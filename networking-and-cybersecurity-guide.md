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
| IPv4 | IPv6 |
|---|---|
| 32-bit | 128-bit |
| Dotted decimal | Hexadecimal colon notation |
| NAT commonly required | NAT generally unnecessary |
| No native IPsec | IPsec built-in |

---

# Subnetting

Subnetting divides a large network into smaller, more manageable sub-networks (subnets) by borrowing bits from the host portion of an IP address.

#### Why Subnet
- Reduces broadcast traffic
- Improves security through segmentation
- Efficient IP address utilization
- Easier network management

#### Key Concepts
- **Subnet Mask**: Defines which bits represent the network vs the host (e.g., 255.255.255.0 = /24).
- **CIDR Notation**: Shorthand like /24, /26, indicating the number of network bits.
- **Binary Subnetting**: Converting the subnet mask and IP to binary to calculate network address, broadcast address, and valid host range.

#### Example
Given 192.168.1.0/26 (mask 255.255.255.192):
- Increment = 256 - 192 = 64
- Subnets: 192.168.1.0, .64, .128, .192
- For 192.168.1.0/26: Network = .0, Broadcast = .63, Usable hosts = .1 to .62 (62 hosts)

#### Formulae
- Number of subnets = 2^(borrowed bits)
- Number of usable hosts per subnet = 2^(host bits) - 2

#### VLSM (Variable Length Subnet Masking)
Allows subnets of different sizes within the same network, optimizing address allocation instead of using one fixed mask everywhere.

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

# TCP, UDP, and Other Protocols

#### TCP (Transmission Control Protocol)
Connection-oriented, reliable protocol that guarantees ordered delivery through acknowledgments, retransmissions, and flow control.

**Three-Way Handshake:**
1. SYN - client requests connection
2. SYN-ACK - server acknowledges and responds
3. ACK - client confirms, connection established

**Four-Way Termination:** FIN, ACK, FIN, ACK

Used for: HTTP/HTTPS, FTP, SMTP, SSH - anywhere reliability matters.

#### UDP (User Datagram Protocol)
Connectionless, "fire and forget" protocol with no guarantee of delivery or order, but low overhead and low latency.

Used for: DNS, DHCP, video streaming, VoIP, online gaming.

### TCP vs UDP
| TCP | UDP |
|---|---|
| Connection-oriented | Connectionless |
| Reliable, ordered | Unreliable, unordered |
| Higher overhead | Lower overhead |
| Slower | Faster |

#### Other Common Protocols
- **HTTP/HTTPS**: Web traffic (port 80/443); HTTPS adds TLS encryption.
- **DNS**: Resolves domain names to IP addresses (port 53).
- **DHCP**: Dynamically assigns IP addresses to devices (ports 67/68).
- **FTP/SFTP**: File transfer (port 21/22).
- **SSH**: Secure remote login and command execution (port 22).
- **Telnet**: Unencrypted remote login (port 23) - insecure, largely deprecated.
- **SMTP/POP3/IMAP**: Email sending and retrieval (ports 25, 110, 143).
- **ICMP**: Used for diagnostics like ping and traceroute; not a transport protocol.
- **ARP**: Resolves IP addresses to MAC addresses on a local network.
- **SNMP**: Network device monitoring and management (port 161).
- **NTP**: Time synchronization across devices (port 123).

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

#### Symmetric Encryption
Uses a single shared key for both encryption and decryption. Fast, efficient for large data, but key distribution is a challenge. Examples: AES, DES, 3DES.

#### Asymmetric Encryption
Uses a mathematically linked key pair - a public key (shared openly) and a private key (kept secret). Solves the key distribution problem but is slower. Examples: RSA, ECC, Diffie-Hellman.

#### Hashing
A one-way function that converts data into a fixed-length digest; used for integrity verification, not encryption (cannot be reversed). Examples: SHA-256, MD5 (weak/deprecated), bcrypt (for passwords).

#### Digital Signatures
Uses a sender's private key to sign data and the corresponding public key to verify it, ensuring authenticity, integrity, and non-repudiation.

#### PKI (Public Key Infrastructure)
A framework of policies, roles, and systems (Certificate Authorities, digital certificates, registration authorities) used to manage public-key encryption and verify identities.

#### Digital Certificates
Issued by a trusted Certificate Authority (CA), binding a public key to an entity's identity, used to establish trust (e.g., SSL/TLS certificates for websites).

#### SSL/TLS
Protocols that encrypt data in transit between a client and server. TLS is the modern, secure successor to SSL. Establishes a secure session through a TLS handshake (certificate exchange, key negotiation).

#### Salting
Adding random data to a password before hashing to defend against precomputed rainbow-table attacks.

### Symmetric vs Asymmetric
| Symmetric | Asymmetric |
|---|---|
| One shared key | Public/private key pair |
| Faster | Slower |
| Key distribution challenge | Solves key distribution |
| AES, DES | RSA, ECC |

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
