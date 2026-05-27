 ## File: networking-syllabus.md

# Networking: From Physical Signals to Global-Scale AI Infrastructure

## A University-Level, Industry-Grade Technical Syllabus

**Version:** 2026.05  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level Infrastructure Candidates  
**Prerequisites:** Solid C/C++, operating systems fundamentals, computer architecture basics, comfort with binary arithmetic and probability  
**Estimated Duration:** 350–450 hours of focused study + 150 hours of capstone projects  
**Last Updated:** May 2026

---

## Table of Contents

1. [Meta: How to Use This Syllabus](#meta-how-to-use-this-syllabus)
2. [Phase 0: Mathematical & Signals Foundations](#phase-0-mathematical--signals-foundations)
3. [Phase 1: Physical Layer & Data Transmission](#phase-1-physical-layer--data-transmission)
4. [Phase 2: Data Link Layer & Local Networks](#phase-2-data-link-layer--local-networks)
5. [Phase 3: Network Layer — IP, Routing, and Internetworking](#phase-3-network-layer--ip-routing-and-internetworking)
6. [Phase 4: Transport Layer — TCP, UDP, and Beyond](#phase-4-transport-layer--tcp-udp-and-beyond)
7. [Phase 5: Application Layer Protocols & APIs](#phase-5-application-layer-protocols--apis)
8. [Phase 6: Network Security & Cryptography](#phase-6-network-security--cryptography)
9. [Phase 7: Production Network Engineering](#phase-7-production-network-engineering)
10. [Phase 8: Distributed Systems Networking](#phase-8-distributed-systems-networking)
11. [Phase 9: AI/ML Infrastructure Networking](#phase-9-aiml-infrastructure-networking)
12. [Phase 10: Advanced & Emerging Topics](#phase-10-advanced--emerging-topics)
13. [Capstone Projects](#capstone-projects)
14. [Assessment & Certification Rubric](#assessment--certification-rubric)
15. [Recommended Reading & Reference Library](#recommended-reading--reference-library)

---

## Meta: How to Use This Syllabus

This syllabus is designed as a **layered, progressive curriculum** that builds intuition from electromagnetic signals to planet-scale AI infrastructure. Each phase corresponds to a layer of the network stack, with explicit dependency chains and production relevance.

**Study Protocol:**
- **Theory → Implementation → Systems → Production:** Every concept must be understood mathematically, implemented in C/Go/Rust, integrated into a system, and operationalized in production contexts.
- **Spaced Reinforcement:** Concepts from earlier phases reappear in later phases at increasing depth.
- **Build-Measure-Learn:** Every module includes explicit packet capture, simulation, profiling, and benchmarking exercises.
- **Architecture Reasoning:** Each phase includes design exercises requiring trade-off analysis (latency vs. throughput, reliability vs. cost, consistency vs. availability).

**Required Tools & Environment:**
- Linux environment with root access (VM or bare metal)
- Wireshark, tcpdump, tshark for packet analysis
- Mininet for network emulation
- iperf3, netperf, sockperf for benchmarking
- Docker/Kubernetes cluster for service mesh experiments
- Access to cloud networking (AWS VPC, GCP VPC, Azure VNet) for production exercises
- eBPF tools (bcc, bpftrace) for kernel networking introspection

---

## Phase 0: Mathematical & Signals Foundations

> **Objective:** Establish the mathematical language and physical intuition required for rigorous networking. Skip only if you can derive Shannon capacity, analyze a Markov chain for queueing, and explain why TCP congestion control is a control system.

### 0.1 Signals and Systems
- **Continuous-Time Signals:** Sinusoids, exponentials, impulse response, step response, convolution integral
- **Fourier Analysis:** Fourier series, Fourier transform, frequency domain representation, bandwidth, spectral analysis
- **Sampling Theory:** Nyquist rate, aliasing, reconstruction, pulse-code modulation (PCM), quantization noise
- **Modulation:** Amplitude modulation (AM), frequency modulation (FM), phase modulation (PM), quadrature amplitude modulation (QAM)
- **Key Exercise:** Implement a QAM modulator/demodulator in Python. Add AWGN. Measure bit error rate vs. SNR. Plot constellation diagrams.

### 0.2 Probability and Queueing Theory
- **Random Variables and Distributions:** Exponential (inter-arrival times), Poisson (arrival processes), Pareto (heavy-tailed traffic)
- **Markov Chains:** Discrete-time and continuous-time, steady-state probabilities, birth-death processes
- **Queueing Models:** M/M/1, M/M/c, M/G/1, Little's Law (L = λW), Pollaczek-Khinchine formula
- **Network Queueing:** Jackson networks, Burke's theorem, Kleinrock's independence approximation
- **Key Exercise:** Model a network router as an M/M/1 queue. Calculate steady-state probabilities. Simulate with varying load factors (ρ = 0.5, 0.9, 0.99). Measure queue length distributions.

### 0.3 Information Theory
- **Entropy and Information:** Shannon entropy, joint entropy, conditional entropy, mutual information
- **Source Coding:** Huffman coding, Lempel-Ziv, arithmetic coding, compression ratios
- **Channel Capacity:** Shannon-Hartley theorem, bandwidth-SNR tradeoff, AWGN channel capacity
- **Error Detection and Correction:** Hamming distance, parity, CRC, Hamming codes, Reed-Solomon, convolutional codes, LDPC, Turbo codes
- **Key Exercise:** Implement a Hamming(7,4) encoder/decoder. Introduce single-bit errors. Verify correction capability. Calculate coding overhead.

### 0.4 Control Theory for Networking
- **Feedback Control Systems:** Open-loop vs. closed-loop, transfer functions, poles and zeros, stability
- **PID Control:** Proportional-integral-derivative, tuning (Ziegler-Nichols), steady-state error, overshoot
- **TCP as a Control System:** AIMD as a controller, stability analysis, fairness convergence
- **Key Exercise:** Model TCP congestion window as a discrete-time control system. Analyze stability under varying RTT and loss rates.

---

## Phase 1: Physical Layer & Data Transmission

> **Objective:** Understand how bits move across physical media. Build intuition for bandwidth, latency, and error rates in real channels.

### 1.1 Transmission Media
- **Guided Media:** Twisted pair (UTP/STP, Cat5e/Cat6/Cat7/Cat8), coaxial cable, fiber optic (single-mode, multi-mode, graded-index)
- **Unguided Media:** Radio propagation, microwave, satellite, infrared, free-space optical
- **Signal Degradation:** Attenuation, dispersion (chromatic, modal), noise (thermal, crosstalk, intersymbol interference), SNR
- **Key Exercise:** Calculate maximum data rate for a 1km multi-mode fiber link given dispersion parameters. Compare with single-mode.

### 1.2 Digital Transmission
- **Line Coding:** NRZ, NRZI, Manchester, 4B/5B, 8B/10B, 64B/66B, scrambling, clock recovery
- **Multiplexing:** TDM, FDM, WDM (DWDM, CWDM), CDM, OFDM, statistical multiplexing
- **Physical Layer Standards:** Ethernet PHY (10BASE-T, 100BASE-TX, 1000BASE-T, 10GBASE-T), SONET/SDH, DSL, PON
- **Key Exercise:** Implement Manchester encoding/decoding in C. Test with a simulated bitstream. Analyze clock recovery robustness.

### 1.3 Wireless Physical Layer
- **Radio Propagation:** Path loss (free-space, two-ray ground reflection), fading (Rayleigh, Rician), Doppler shift
- **Cellular Architecture:** Frequency reuse, cell sectoring, handoff strategies, power control
- **Wi-Fi Physical Layer:** 802.11a/b/g/n/ac/ax/be, OFDM, MIMO, channel bonding, MU-MIMO, OFDMA
- **5G NR:** mmWave, sub-6GHz, massive MIMO, beamforming, numerology, slot structure
- **Key Exercise:** Simulate path loss for a 5G mmWave link at 28GHz. Calculate required transmit power for 100m range. Analyze blockage effects.

### 1.4 Error Detection and Correction in Practice
- **CRC Implementation:** Polynomial arithmetic, hardware CRC generators (LFSR), software CRC32, CRC64
- **Forward Error Correction (FEC):** Reed-Solomon in storage/communication, LDPC in 10GBase-T and Wi-Fi, Turbo codes in 3G/4G, Polar codes in 5G
- **ARQ Protocols:** Stop-and-wait, Go-Back-N, Selective Repeat, hybrid ARQ (HARQ)
- **Key Exercise:** Implement CRC-32 in C. Verify against zlib implementation. Measure throughput for large buffers.

---

## Phase 2: Data Link Layer & Local Networks

> **Objective:** Master local area networking, framing, media access, and switching. Build production-grade LANs.

### 2.1 Framing and Data Link Control
- **Framing:** Byte count, byte stuffing, bit stuffing (HDLC), length fields, CRC trailers
- **Flow Control:** Stop-and-wait, sliding window (go-back-N, selective repeat), piggybacking
- **Error Control:** ACKs, NAKs, timeouts, duplicate detection, sequence numbers
- **PPP and HDLC:** Frame format, LCP, NCP, authentication (PAP, CHAP)
- **Key Exercise:** Implement a sliding window protocol (selective repeat) over a simulated unreliable channel. Measure throughput vs. window size and error rate.

### 2.2 Medium Access Control (MAC)
- **Channel Allocation:** Static (FDM, TDM) vs. dynamic, centralized vs. distributed
- **Random Access:** ALOHA, slotted ALOHA, CSMA, CSMA/CD (Ethernet), CSMA/CA (Wi-Fi)
- **Contention-Free:** Token passing, token ring, polling, reservation protocols
- **Ethernet Evolution:** 10 Mbps → 100 Mbps → 1 Gbps → 10 Gbps → 25/40/100/400 Gbps, full-duplex, auto-negotiation
- **Key Exercise:** Simulate CSMA/CD and CSMA/CA under varying loads. Measure collision probability, throughput, and fairness. Plot throughput vs. offered load.

### 2.3 Local Area Networks (LAN)
- **Ethernet Frame Format:** Preamble, SFD, MAC addresses, EtherType, VLAN tagging (802.1Q), MTU, jumbo frames
- **Switched Ethernet:** Learning bridges, MAC address tables, flooding, filtering, forwarding, spanning tree
- **VLANs:** Port-based VLANs, tagged VLANs, trunking, VLAN hopping attacks, private VLANs
- **Link Aggregation:** LACP (802.3ad), static aggregation, load balancing algorithms (L2, L3, L4 hashing)
- **Key Exercise:** Configure a managed switch with VLANs and LACP. Test inter-VLAN routing. Verify with Wireshark.

### 2.4 Spanning Tree Protocol (STP)
- **STP Operation:** Root bridge election, path cost, port roles (root, designated, blocked), BPDU format
- **Rapid STP (RSTP):** Port states (discarding, learning, forwarding), proposal/agreement mechanism, backward compatibility
- **Multiple STP (MSTP):** Multiple spanning trees, region concept, IST, MSTIs
- **STP Security:** BPDU guard, root guard, loop guard, storm control
- **Key Exercise:** Build a network with redundant links. Configure RSTP. Verify convergence time on link failure. Test BPDU guard.

### 2.5 Wireless LAN (Wi-Fi)
- **802.11 Architecture:** BSS, ESS, AP, STA, SSID, BSSID, association, authentication, roaming
- **MAC Layer:** DCF (CSMA/CA), RTS/CTS, NAV, fragmentation, power management, QoS (EDCA)
- **Security:** WEP (broken), WPA (TKIP), WPA2 (AES-CCMP), WPA3 (SAE, forward secrecy), 802.1X/EAP
- **Wi-Fi 6/6E/7:** OFDMA, BSS coloring, target wake time, 6GHz spectrum, 320MHz channels, 4K-QAM, MLO (Multi-Link Operation)
- **Key Exercise:** Capture Wi-Fi frames with monitor mode. Analyze association, authentication, and 4-way handshake. Verify WPA2 security.

---

## Phase 3: Network Layer — IP, Routing, and Internetworking

> **Objective:** Master the global internet. Understand IP, routing algorithms, and the protocols that bind networks together.

### 3.1 Internet Protocol (IPv4)
- **IPv4 Addressing:** Classful vs. classless (CIDR), subnetting, VLSM, supernetting, private addresses (RFC 1918), NAT
- **IPv4 Header:** Version, IHL, TOS, length, ID, flags, fragment offset, TTL, protocol, checksum, options
- **Fragmentation and Reassembly:** MTU discovery, path MTU, don't fragment bit, reassembly timeout
- **NAT and NAPT:** Static NAT, dynamic NAT, PAT/port forwarding, NAT traversal (STUN, TURN, ICE), ALG
- **Key Exercise:** Implement a CIDR route lookup (longest prefix match) using a trie. Benchmark with a full BGP table (~900K routes).

### 3.2 Internet Protocol (IPv6)
- **IPv6 Addressing:** 128-bit addresses, hexadecimal notation, compression, prefixes, interface identifiers (EUI-64), privacy extensions
- **IPv6 Header:** Fixed 40-byte header, flow label, next header chain, extension headers (hop-by-hop, routing, fragment, AH, ESP, mobility)
- **Transition Mechanisms:** Dual-stack, tunneling (6to4, Teredo, ISATAP), translation (NAT64, DNS64), 464XLAT
- **NDP (Neighbor Discovery Protocol):** Replaces ARP, router solicitation/advertisement, neighbor solicitation/advertisement, redirect
- **Key Exercise:** Configure a dual-stack network. Set up NAT64/DNS64. Test IPv6-only client accessing IPv4-only server.

### 3.3 Routing Fundamentals
- **Routing Basics:** Forwarding vs. routing, routing tables, next hop, administrative distance, metrics
- **Distance Vector:** Bellman-Ford, RIP, split horizon, poison reverse, count to infinity, triggered updates
- **Link State:** Dijkstra's algorithm, OSPF, LSA types, area design, DR/BDR election, SPF calculation
- **Path Vector:** BGP, AS paths, path attributes, route selection process, iBGP vs. eBGP, route reflectors, confederations
- **Key Exercise:** Implement Dijkstra's algorithm for link-state routing. Simulate a 50-node network. Measure convergence time on link failure.

### 3.4 Interior Gateway Protocols (IGP)
- **OSPF:** Hello packets, neighbor adjacency, LSDB synchronization, SPF tree, area types (stub, totally stubby, NSSA), virtual links, LSA flooding
- **IS-IS:** CLNS addressing, TLV encoding, level-1/level-2 routing, pseudonode, metric styles (narrow/wide)
- **EIGRP:** DUAL algorithm, feasibility condition, successor, feasible successor, composite metric, stub routing
- **Key Exercise:** Configure OSPF multi-area network. Verify LSDB. Simulate link failure and measure SPF recalculation time.

### 3.5 Border Gateway Protocol (BGP)
- **BGP Operation:** TCP port 179, OPEN, UPDATE, NOTIFICATION, KEEPALIVE, route advertisement/withdrawal
- **Path Attributes:** ORIGIN, AS_PATH, NEXT_HOP, LOCAL_PREF, MED, COMMUNITY, EXTENDED_COMMUNITY
- **BGP Policy:** Route filtering (prefix-lists, AS-path filters, route-maps), traffic engineering, communities for blackholing
- **BGP Security:** RPKI (Resource Public Key Infrastructure), ROAs (Route Origin Authorizations), BGPsec, IRR databases
- **Key Exercise:** Set up a mini-internet with 4 ASes using BGP. Implement traffic engineering with LOCAL_PREF and MED. Verify with `traceroute`.

### 3.6 Multicast and Anycast
- **IP Multicast:** Class D addresses, IGMP (v1/v2/v3), PIM (sparse mode, dense mode, SSM), MSDP, MBGP
- **Multicast Routing:** RPF check, shared trees (*,G), source trees (S,G), graft/prune, bootstrap router
- **Anycast:** Same IP on multiple servers, BGP anycast, DNS anycast, CDN anycast, health checking
- **Key Exercise:** Implement IGMP snooping on a switch. Set up PIM-SM. Test multicast streaming. Measure group join/leave latency.

### 3.7 Software-Defined Networking (SDN)
- **SDN Architecture:** Data plane, control plane, application plane, southbound API (OpenFlow), northbound API (REST)
- **OpenFlow:** Flow tables, match fields, actions, pipeline processing, group tables, meter tables
- **Controllers:** OpenDaylight, ONOS, Ryu, Floodlight — topology discovery, path computation, flow installation
- **Network Virtualization:** Overlay networks (VXLAN, NVGRE, GENEVE), network functions virtualization (NFV), service chaining
- **Key Exercise:** Build an SDN network with Mininet and Ryu. Implement a simple load-balancing application. Measure flow setup latency.

---

## Phase 4: Transport Layer — TCP, UDP, and Beyond

> **Objective:** Master end-to-end transport. Understand TCP at the packet level, congestion control dynamics, and modern transport protocols.

### 4.1 User Datagram Protocol (UDP)
- **UDP Header:** Source/destination port, length, checksum, pseudo-header
- **UDP Characteristics:** Connectionless, unreliable, no flow control, no congestion control, low overhead
- **Use Cases:** DNS, DHCP, VoIP, video streaming, QUIC (built on UDP), gaming
- **Key Exercise:** Implement a reliable file transfer over UDP. Add sequence numbers, ACKs, timeouts, and retransmissions. Compare performance with TCP.

### 4.2 Transmission Control Protocol (TCP) — Fundamentals
- **TCP Header:** Source/destination port, sequence number, acknowledgment number, data offset, flags (SYN, ACK, FIN, RST, PSH, URG), window size, checksum, urgent pointer, options
- **Connection Management:** Three-way handshake, four-way termination, simultaneous open/close, TIME_WAIT state (2MSL), SYN cookies
- **Reliable Data Transfer:** Sequence numbers, cumulative ACKs, duplicate ACKs, selective ACKs (SACK), retransmission timers (RTO calculation, Karn's algorithm, Jacobson's algorithm)
- **Flow Control:** Sliding window, window scaling (RFC 1323), silly window syndrome, Nagle's algorithm, delayed ACKs
- **Key Exercise:** Implement a minimal TCP stack (handshake, data transfer, teardown) in userspace using raw sockets or a packet capture library. Test with `nc`.

### 4.3 TCP Congestion Control
- **Congestion Window (cwnd):** Slow start, congestion avoidance, AIMD, fast retransmit, fast recovery
- **Classic Algorithms:** Tahoe, Reno, NewReno — behavior on timeout vs. triple duplicate ACK
- **Modern Algorithms:** CUBIC (Linux default), BBR (Bottleneck Bandwidth and RTT), Vegas, Illinois, Hybla
- **ECN (Explicit Congestion Notification):** IP ECN bits, TCP ECN-Echo/CWR flags, AQM (RED, CoDel, FQ-CoDel, PIE)
- **Key Exercise:** Implement CUBIC congestion control in a network simulator. Compare with Reno under varying BDP (bandwidth-delay product) links.

### 4.4 TCP Advanced Topics
- **SACK and DSACK:** Selective acknowledgment, duplicate SACK, recovery from multiple losses
- **TCP Options:** Timestamp (RTTM, PAWS), window scaling, SACK permitted, MSS, fast open (TFO)
- **TCP Offload:** TSO (TCP Segmentation Offload), GSO (Generic Segmentation Offload), LRO (Large Receive Offload), GRO, checksum offload
- **TCP in Production:** Tuning for high BDP (10Gbps+), buffer bloat, `tcp_mem`, `tcp_rmem`, `tcp_wmem`, `tcp_congestion_control`, `tcp_notsent_lowat`
- **Key Exercise:** Tune a 10Gbps TCP connection for maximum throughput. Measure with iperf3. Analyze with `ss -i` and Wireshark.

### 4.5 Modern Transport Protocols
- **QUIC:** Built on UDP, 0-RTT handshake, connection migration, stream multiplexing, head-of-line blocking elimination, TLS 1.3 integration
- **SCTP:** Multi-homing, multi-streaming, message-oriented, partial reliability, use in telecom (SIGTRAN)
- **DCCP:** Datagram Congestion Control Protocol, unreliable but congestion-controlled
- **MPTCP:** Multi-path TCP, subflows, scheduler, coupled congestion control, use in mobile devices
- **Key Exercise:** Implement a minimal QUIC client/server using a library (quiche, msquic, or ngtcp2). Measure handshake latency vs. TCP+TLS.

### 4.6 Socket Programming Deep Dive
- **Berkeley Sockets API:** `socket()`, `bind()`, `listen()`, `accept()`, `connect()`, `send()`, `recv()`, `close()`, `shutdown()`
- **I/O Models:** Blocking, non-blocking, I/O multiplexing (`select`/`poll`/`epoll`/`kqueue`/`IOCP`), asynchronous I/O (`io_uring`, aio)
- **Socket Options:** `SO_REUSEADDR`, `TCP_NODELAY`, `TCP_QUICKACK`, `SO_BUSY_POLL`, `SO_ZEROCOPY`
- **Zero-Copy:** `sendfile()`, `splice()`, `mmap()`, `MSG_ZEROCOPY`, kernel bypass (DPDK, RDMA)
- **Key Exercise:** Build an epoll-based echo server handling 100K concurrent connections. Measure latency percentiles. Compare with io_uring implementation.

---

## Phase 5: Application Layer Protocols & APIs

> **Objective:** Master the protocols that power modern applications. Build production-grade HTTP services, DNS infrastructure, and real-time systems.

### 5.1 Domain Name System (DNS)
- **DNS Hierarchy:** Root servers, TLD servers, authoritative servers, recursive resolvers, zones, delegations
- **DNS Records:** A, AAAA, CNAME, MX, NS, SOA, PTR, SRV, TXT, CAA, DNSSEC (RRSIG, DNSKEY, DS, NSEC)
- **Resolution Process:** Iterative vs. recursive queries, caching, TTL, negative caching, DNS over HTTPS (DoH), DNS over TLS (DoT)
- **DNS Security:** DNSSEC validation, zone signing, KSK/ZSK, DANE, DNS amplification attacks, response rate limiting
- **Key Exercise:** Set up an authoritative DNS server (BIND or CoreDNS). Configure DNSSEC. Validate chain of trust with `dig +dnssec`.

### 5.2 Hypertext Transfer Protocol (HTTP)
- **HTTP/1.1:** Request/response format, methods (GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS), status codes, headers, keep-alive, pipelining
- **HTTP/2:** Binary framing, multiplexing, stream prioritization, header compression (HPACK), server push, flow control
- **HTTP/3:** QUIC-based, 0-RTT, connection migration, improved congestion control, no head-of-line blocking
- **REST Architecture:** Resources, URIs, statelessness, HATEOAS, idempotency, safety, Richardson Maturity Model
- **Key Exercise:** Implement an HTTP/2 server from scratch (or using a low-level library). Support multiplexing and HPACK. Benchmark against HTTP/1.1.

### 5.3 WebSockets and Real-Time Protocols
- **WebSocket Protocol:** Upgrade handshake, framing (text, binary, ping/pong, close), masking, extensions (permessage-deflate)
- **Server-Sent Events (SSE):** One-way streaming, event format, reconnection, last-event-ID
- **gRPC:** HTTP/2 transport, Protocol Buffers, unary/streaming RPC, bidirectional streaming, deadlines, metadata
- **GraphQL:** Schema, queries, mutations, subscriptions, resolvers, N+1 problem, batching, federation
- **Key Exercise:** Build a real-time chat system using WebSockets. Implement backpressure handling. Measure message latency at 10K concurrent connections.

### 5.4 Email and Messaging Protocols
- **SMTP:** Mail submission, relaying, MX records, STARTTLS, AUTH (PLAIN, LOGIN, CRAM-MD5), SPF, DKIM, DMARC
- **IMAP/POP3:** Mailbox access, folder management, IDLE, synchronization strategies
- **Message Queues:** AMQP (RabbitMQ), MQTT (IoT), Kafka protocol, NATS, ZeroMQ patterns (req/rep, pub/sub, push/pull, dealer/router)
- **Key Exercise:** Implement an SMTP server subset. Handle EHLO, MAIL FROM, RCPT TO, DATA. Add SPF validation.

### 5.5 Network Management and Monitoring
- **SNMP:** v1/v2c/v3, MIBs, OIDs, traps/informs, GET/SET/WALK, security models (USM, VACM)
- **NetFlow/sFlow/IPFIX:** Flow records, collectors, analysis, DDoS detection
- **Syslog:** Facility, severity, format, TLS transport, structured data (RFC 5424)
- **Network Telemetry:** gRPC-based streaming telemetry, YANG models, OpenConfig, gNMI
- **Key Exercise:** Build a network monitoring dashboard. Collect SNMP data and NetFlow records. Visualize bandwidth utilization and top talkers.

---

## Phase 6: Network Security & Cryptography

> **Objective:** Secure networks at every layer. Master cryptographic primitives, protocol security, and operational defense.

### 6.1 Cryptographic Primitives
- **Symmetric Encryption:** AES (ECB, CBC, CTR, GCM), ChaCha20-Poly1305, key sizes, modes of operation, IV/nonce management
- **Asymmetric Encryption:** RSA (key generation, padding: OAEP, PKCS#1 v1.5), ECC (curve25519, secp256r1), ECDH, ECDSA
- **Hash Functions:** SHA-256, SHA-3, BLAKE2, HMAC, length extension attacks
- **Key Exchange:** Diffie-Hellman, ECDH, post-quantum (Kyber, Dilithium), perfect forward secrecy (PFS)
- **Key Exercise:** Implement AES-256-GCM from a lower-level library (OpenSSL EVP or libsodium). Benchmark encryption throughput. Verify authentication tag.

### 6.2 Transport Layer Security (TLS)
- **TLS 1.3:** Handshake (1-RTT, 0-RTT), key schedule, record layer, AEAD ciphers, downgrade protection
- **Certificate Infrastructure:** X.509, PKIX, certificate chains, CA/Browser Forum, certificate transparency (CT), OCSP, CRL
- **TLS in Practice:** SNI, ALPN, session resumption (tickets, IDs), certificate pinning, HSTS, HPKP (deprecated)
- **TLS Attacks:** BEAST, CRIME, BREACH, POODLE, Heartbleed, ROBOT, Raccoon, Bleichenbacher attacks
- **Key Exercise:** Implement a TLS 1.3 client handshake using a crypto library. Verify certificate chain. Implement certificate pinning.

### 6.3 Network Layer Security
- **IPsec:** AH vs. ESP, transport vs. tunnel mode, IKEv2, SA (Security Association), SPI, NAT traversal
- **VPN Technologies:** Site-to-site IPsec, SSL VPN (OpenVPN), WireGuard (Noise protocol framework), Tailscale/Headscale
- **DDoS Mitigation:** Volumetric (UDP flood, ICMP flood), protocol (SYN flood, Ping of Death), application (HTTP flood, Slowloris), mitigation (rate limiting, scrubbing centers, Anycast, BGP flowspec)
- **Key Exercise:** Set up a WireGuard mesh VPN between 3 nodes. Measure throughput and latency overhead. Implement a simple DDoS detection algorithm using NetFlow.

### 6.4 Firewalls and Intrusion Detection
- **Packet Filtering:** Stateless vs. stateful, ACLs, iptables/nftables, connection tracking, conntrack
- **Application Layer Firewalls:** WAF (ModSecurity, AWS WAF), DPI (Deep Packet Inspection), protocol validation
- **IDS/IPS:** Signature-based (Snort, Suricata), anomaly-based, behavioral analysis, SIEM integration
- **Zero Trust Architecture:** Micro-segmentation, identity-aware proxy, device posture, least privilege, continuous verification
- **Key Exercise:** Configure nftables with stateful rules. Set up Suricata IDS with emerging threats rules. Generate alerts and analyze a simulated attack.

### 6.5 Operational Security
- **Network Segmentation:** VLANs, private subnets, DMZ, bastion hosts, jump boxes, service mesh isolation
- **Secrets Management:** HashiCorp Vault, AWS Secrets Manager, TLS certificate rotation, short-lived credentials
- **Audit and Compliance:** Flow logs, packet capture (tcpdump rotation), network access logs, PCI-DSS, SOC 2 networking requirements
- **Key Exercise:** Design a zero-trust network architecture for a 3-tier application. Document segmentation, authentication, and monitoring.

---

## Phase 7: Production Network Engineering

> **Objective:** Build and operate production networks at scale. Master routing, switching, load balancing, and observability.

### 7.1 Data Center Network Architecture
- **Topologies:** Three-tier (core/aggregation/access), spine-leaf (Clos), fat-tree, Jellyfish, random graphs
- **Oversubscription:** Ratios, bisection bandwidth, full bisection bandwidth, trade-offs
- **Network Virtualization:** VXLAN (MAC-in-UDP), EVPN (BGP-based), VTEP, BUM traffic handling, ARP suppression
- **Traffic Engineering:** ECMP (Equal-Cost Multi-Path), UCMP, flowlet switching, congestion-aware routing
- **Key Exercise:** Design a 2-tier spine-leaf network for 10K servers. Calculate oversubscription ratios. Configure EVPN-VXLAN.

### 7.2 Load Balancing and Traffic Management
- **Layer 4 Load Balancing:** LVS (Linux Virtual Server), HAProxy (TCP mode), Maglev (Google), consistent hashing
- **Layer 7 Load Balancing:** HAProxy (HTTP mode), Nginx, Envoy, path-based routing, health checks, sticky sessions
- **Global Server Load Balancing (GSLB):** DNS-based, anycast-based, health-checked, proximity routing
- **Service Mesh:** Istio, Linkerd, Consul Connect — sidecar proxy, mTLS, traffic splitting, circuit breaking, retries, observability
- **Key Exercise:** Deploy Envoy as a sidecar in Kubernetes. Configure traffic splitting (canary), circuit breaking, and retry policies. Measure with load tests.

### 7.3 Network Observability
- **Flow Monitoring:** NetFlow v5/v9/IPFIX, sFlow, packet sampling, flow records, collectors (nfdump, Elastiflow)
- **Packet Capture:** tcpdump filters, Wireshark analysis, tshark scripting, capture filters vs. display filters
- **Active Measurement:** Ping, traceroute, pathchar, OWAMP, TWAMP, synthetic monitoring
- **Network Telemetry:** Streaming telemetry (gRPC/gNMI), YANG models, OpenConfig, real-time dashboards
- **Key Exercise:** Build a network observability pipeline. Collect sFlow, parse with Python, store in ClickHouse, visualize in Grafana. Detect anomalies.

### 7.4 Network Automation
- **Infrastructure as Code:** Ansible (network modules), Terraform (network providers), NAPALM, Netmiko
- **Intent-Based Networking:** Declarative configuration, validation, remediation, closed-loop automation
- **Configuration Management:** Git-based workflows, pre-commit validation, configuration drift detection
- **Testing:** Batfish (configuration analysis), pyATS (Cisco), network emulation (Containerlab, EVE-NG)
- **Key Exercise:** Automate configuration of 10 routers using Ansible. Implement configuration validation with Batfish. Detect and remediate drift.

### 7.5 Cloud Networking
- **AWS Networking:** VPC, subnets, route tables, IGW, NAT Gateway, Transit Gateway, VPC peering, PrivateLink, Direct Connect
- **GCP Networking:** VPC, subnets (regional), Cloud Router, Cloud Interconnect, VPC Service Controls, Private Service Connect
- **Azure Networking:** VNet, subnets, NSG, Azure Firewall, ExpressRoute, Virtual WAN, Private Link
- **Multi-Cloud Networking:** Cloud exchange, SD-WAN, SASE (Secure Access Service Edge), Zero Trust Network Access (ZTNA)
- **Key Exercise:** Design a multi-region, multi-cloud network. Implement private connectivity between AWS and GCP. Document security boundaries.

---

## Phase 8: Distributed Systems Networking

> **Objective:** Understand the networking implications of distributed systems. Master consensus, replication, and partition tolerance.

### 8.1 Time and Ordering in Distributed Systems
- **Physical Clocks:** NTP, PTP, clock skew, clock drift, bounded synchrony assumptions
- **Logical Clocks:** Lamport timestamps, vector clocks, version vectors, causal consistency
- **Total Order:** Atomic broadcast, total order broadcast, sequencer-based ordering, Paxos/Raft log ordering
- **Key Exercise:** Implement vector clocks for a 3-node distributed system. Detect concurrent updates. Visualize the partial order.

### 8.2 Consensus and Replication
- **Two-Phase Commit (2PC):** Coordinator, participants, prepare, commit, blocking problem
- **Three-Phase Commit (3PC):** Non-blocking under certain failures, complexity trade-offs
- **Paxos:** Proposers, acceptors, learners, safety, liveness, Multi-Paxos, leader election
- **Raft:** Leader election, log replication, safety, membership changes, snapshotting, log compaction
- **Key Exercise:** Implement Raft consensus (log replication only). Test leader election, network partitions, and recovery. Use Jepsen-style tests.

### 8.3 CAP Theorem and Consistency Models
- **CAP Theorem:** Consistency, Availability, Partition tolerance — pick two, practical implications
- **Consistency Models:** Linearizability, sequential consistency, causal consistency, eventual consistency, read-your-writes, monotonic reads
- **Quorum Systems:** Read/write quorums, sloppy quorums, hinted handoff, read repair, anti-entropy
- **Gossip Protocols:** Epidemic broadcast, rumor mongering, membership protocols (SWIM), dissemination
- **Key Exercise:** Build a key-value store with tunable consistency (eventual to linearizable). Measure latency and availability under partition.

### 8.4 Distributed Messaging and Streaming
- **Message Queues:** RabbitMQ (AMQP), Kafka (log-based), NATS, Pulsar — delivery guarantees, ordering, partitioning
- **Stream Processing:** Exactly-once semantics, idempotent producers, transactional writes, windowing (tumbling, sliding, session)
- **Backpressure:** TCP-like flow control, credit-based, pull-based, reactive streams
- **Key Exercise:** Build a Kafka-like log broker. Implement replication (leader-follower), consumer groups, and exactly-once semantics.

### 8.5 Service Discovery and RPC
- **Service Discovery:** DNS-based (SRV records), Consul, etcd, ZooKeeper, Kubernetes DNS, service mesh registry
- **RPC Frameworks:** gRPC, Thrift, Avro, Cap'n Proto — serialization, transport, streaming, deadlines, retries
- **Circuit Breakers:** Failure detection, half-open state, exponential backoff, jitter, bulkhead pattern
- **Key Exercise:** Build a service discovery system with health checking. Implement a simple RPC framework with circuit breaker and retry logic.

---

## Phase 9: AI/ML Infrastructure Networking

> **Objective:** Master the specialized networking requirements of AI/ML systems. This is where networking meets distributed training and inference at scale.

### 9.1 High-Performance Computing (HPC) Networking
- **InfiniBand:** RDMA, verbs API, RC/UC/RD/UD transport types, subnet manager, QoS
- **RoCE (RDMA over Converged Ethernet):** v1 (L2) vs. v2 (L3), PFC (Priority Flow Control), ECN, DCBX, congestion control
- **Omni-Path:** Intel's discontinued HPC fabric, lessons learned
- **Slingshot:** Cray's adaptive routing, congestion control, quality of service
- **Key Exercise:** Set up RoCEv2 on a small cluster. Configure PFC and ECN. Run `ib_write_bw` and `ib_read_bw`. Measure latency and bandwidth.

### 9.2 GPU Interconnect and Scale-Up Networks
- **NVLink:** GPU-to-GPU high-speed interconnect, NVSwitch, topology (cube mesh, fat tree), bandwidth evolution
- **NVLink Switch System:** NVLink 4/5, 900 GB/s per GPU, multi-node NVLink domains (DGX GH200, NVL72)
- **PCIe Topology:** Root complex, switches, lanes, generations (PCIe 4.0/5.0/6.0), P2P access, BAR sizes
- **GPUDirect:** RDMA (peer-to-peer), P2P (GPU-to-GPU), ASYNC (GPU-initiated RDMA)
- **Key Exercise:** Map the PCIe and NVLink topology of a multi-GPU server. Measure P2P bandwidth with `p2pBandwidthLatencyTest`. Analyze topology constraints.

### 9.3 Distributed Training Networking
- **All-Reduce Algorithms:** Ring all-reduce, tree all-reduce, recursive halving/doubling, bandwidth-optimal algorithms
- **NCCL (NVIDIA Collective Communications Library):** Ring, tree, and NVLS (NVLink SHARP) algorithms, topology detection, auto-tuning
- **Communication Patterns:** Data parallelism (parameter servers vs. all-reduce), model parallelism (pipeline bubbles), 3D parallelism
- **Network Requirements:** Bandwidth (400Gbps+), latency (<1μs), congestion-free fabrics, adaptive routing
- **Key Exercise:** Implement ring all-reduce in Python using MPI. Measure scaling efficiency on 8 GPUs. Compare with NCCL performance.

### 9.4 Inference Serving Networking
- **Load Balancing for LLMs:** Request routing based on sequence length, KV cache availability, model sharding
- **Batching and Scheduling:** Continuous batching, iteration-level scheduling, preemption, priority queues
- **Network Overhead:** Serialization/deserialization, gRPC overhead, tensor transmission, zero-copy inference
- **Edge Deployment:** Model partitioning, speculative execution across edge and cloud, network-aware scheduling
- **Key Exercise:** Design a load balancer for a multi-node LLM inference cluster. Route requests based on KV cache state. Measure tail latency.

### 9.5 In-Network Computing
- **SmartNICs and DPUs:** BlueField, IPU, Pensando — offloading encryption, compression, virtualization, storage
- **In-Network Aggregation:** SwitchML, SHARP (Scalable Hierarchical Aggregation and Reduction Protocol), in-network all-reduce
- **Programmable Switches:** P4, Tofino, programmable data plane, in-network caching, load balancing
- **Key Exercise:** Write a P4 program for in-network load balancing. Implement consistent hashing in the data plane. Test with bmv2 or Tofino.

---

## Phase 10: Advanced & Emerging Topics

> **Objective:** Explore cutting-edge networking research and emerging paradigms. Develop the ability to read, implement, and critique networking papers.

### 10.1 Software-Defined Wide Area Networking (SD-WAN)
- **Architecture:** Overlay networks, path selection, application-aware routing, zero-touch provisioning
- **Traffic Engineering:** Dynamic path selection, SLA enforcement, link bonding, packet duplication
- **Security:** IPsec overlay, micro-segmentation, SASE integration
- **Key Exercise:** Design an SD-WAN architecture for a global enterprise. Document failover, QoS, and security policies.

### 10.2 5G and Edge Networking
- **5G Core:** Service-based architecture (SBA), network functions (AMF, SMF, UPF), network slicing, MEC (Multi-Access Edge Computing)
- **Edge Computing:** Low-latency requirements, edge orchestration, federated learning at the edge
- **Private 5G:** CBRS, local spectrum, industrial IoT, campus networks
- **Key Exercise:** Design a private 5G network for a smart factory. Specify latency, reliability, and device density requirements.

### 10.3 Quantum Networking
- **Quantum Key Distribution (QKD):** BB84 protocol, entanglement-based QKD, quantum repeaters
- **Quantum Internet:** Quantum memory, quantum repeaters, quantum teleportation for communication
- **Post-Quantum Cryptography:** NIST standards (Kyber, Dilithium), hybrid deployments, key exchange
- **Key Exercise:** Simulate the BB84 protocol. Calculate quantum bit error rate (QBER). Implement privacy amplification.

### 10.4 Networking for AI/ML Research
- **In-Network Machine Learning:** Running ML inference on switches, P4-based neural networks, NetCache
- **Networked Federated Learning:** Communication-efficient aggregation, gradient compression, sparse updates
- **Network Topology Optimization:** Topology-aware training, dragonfly, slimfly, optimization for all-reduce patterns
- **Key Exercise:** Survey recent papers on in-network ML. Implement a simple in-network cache eviction policy using P4.

### 10.5 Formal Methods for Networking
- **Network Verification:** Header space analysis, Batfish, Minesweeper, reachability verification
- **Property Checking:** Loop freedom, blackhole freedom, waypointing, isolation
- **Control Plane Verification:** BGP policy verification, stable paths, convergence
- **Key Exercise:** Use Batfish to verify a network configuration. Check for loops, blackholes, and ACL violations.

---

## Capstone Projects

> **Objective:** Demonstrate mastery by building production-grade networking systems. Each project should be portfolio-ready and include architecture diagrams, performance benchmarks, and operational documentation.

### Capstone 1: High-Performance TCP Stack
**Scope:** Implement a userspace TCP stack from scratch.
**Requirements:**
- Implement connection establishment, reliable data transfer, flow control, and congestion control (CUBIC)
- Pass interoperability tests with Linux TCP
- Achieve >1 Gbps throughput on loopback
- Implement SACK and window scaling
- Document design decisions and performance characteristics

### Capstone 2: Production SDN Controller
**Scope:** Build an SDN controller for data center traffic engineering.
**Requirements:**
- Use OpenFlow 1.5+ or P4Runtime
- Implement traffic engineering with ECMP and congestion-aware routing
- Support at least 100 switches in Mininet
- Include network monitoring and visualization
- Document failover behavior and convergence time

### Capstone 3: Distributed Consensus System
**Scope:** Build a production-ready Raft implementation.
**Requirements:**
- Full Raft protocol (leader election, log replication, membership changes, snapshotting)
- Linearizable key-value store built on top
- Jepsen-style testing (network partitions, crashes, message delays)
- Performance: >10K writes/sec with <10ms latency
- Comprehensive test suite and formal safety argument

### Capstone 4: AI Training Network Optimizer
**Scope:** Optimize network configuration for distributed deep learning.
**Requirements:**
- Profile NCCL all-reduce on a multi-node GPU cluster
- Implement topology-aware rank assignment
- Tune RoCE/InfiniBand parameters (PFC, ECN, MTU)
- Achieve >90% scaling efficiency on 16 GPUs
- Document bandwidth and latency requirements

### Capstone 5: Zero-Trust Service Mesh
**Scope:** Deploy a production-grade service mesh with security and observability.
**Requirements:**
- Istio or Linkerd deployment on Kubernetes
- mTLS for all service-to-service communication
- Fine-grained authorization policies (RBAC)
- Distributed tracing (Jaeger/Tempo) and metrics (Prometheus)
- Circuit breaking, retries, and rate limiting
- Document security model and operational runbooks

---

## Assessment & Certification Rubric

### Knowledge Assessment
- **Theory Exams:** Closed-book exams on protocol design, queueing theory, routing algorithms, and security
- **Configuration Reviews:** Review of network device configurations, ACLs, routing policies
- **Architecture Reviews:** Design reviews of capstone projects focusing on scalability, reliability, and security trade-offs

### Practical Assessment
- **Troubleshooting Challenges:** Broken networks (routing loops, ACL misconfigurations, MTU issues) that candidates must diagnose and fix
- **Performance Optimization:** Given a slow network path, achieve target throughput/latency with profiling evidence
- **Security Audit:** Simulated penetration test requiring vulnerability identification and mitigation

### Certification Levels
- **Level 1 — Practitioner:** Completes Phases 1–5, passes theory exams, completes Capstone 1
- **Level 2 — Specialist:** Completes Phases 1–8, passes practical assessments, completes Capstones 1–3
- **Level 3 — Expert:** Completes all phases, leads architecture reviews, completes all capstones with production deployment evidence

---

## Recommended Reading & Reference Library

### Foundational Textbooks
1. **"Computer Networking: A Top-Down Approach"** — Kurose & Ross
2. **"TCP/IP Illustrated, Volume 1: The Protocols"** — Stevens & Fall
3. **"Unix Network Programming, Volume 1"** — Stevens, Fenner, Rudoff
4. **"High Performance Browser Networking"** — Ilya Grigorik (free online)
5. **"Network Algorithmics"** — George Varghese
6. **"Designing Data-Intensive Applications"** — Martin Kleppmann
7. **"The Art of Computer Systems Performance Analysis"** — Raj Jain

### Protocol Standards (RFCs)
- **IP:** RFC 791 (IPv4), RFC 2460 (IPv6), RFC 1918 (Private Addresses)
- **TCP:** RFC 793, RFC 5681 (Congestion Control), RFC 6298 (RTO), RFC 8312 (CUBIC)
- **TLS:** RFC 8446 (TLS 1.3)
- **QUIC:** RFC 9000-9002
- **BGP:** RFC 4271, RFC 4272 (Security)
- **DNS:** RFC 1034/1035, RFC 4033-4035 (DNSSEC)

### Research Papers
- **"A Protocol for Packet Network Intercommunication"** — Cerf & Kahn (1974) [TCP/IP foundation]
- **"Congestion Avoidance and Control"** — Van Jacobson (1988)
- **"Maglev: A Fast and Reliable Software Network Load Balancer"** — Google (2016)
- **"The QUIC Transport Protocol"** — IETF (RFC 9000)
- **"In-Network Aggregation for Shared Machine Learning Clusters"** — SwitchML (2021)
- **"P4: Programming Protocol-Independent Packet Processors"** — Bosshart et al. (2014)

### Tools & References
- **Wireshark:** https://www.wireshark.org/
- **tcpdump/libpcap:** https://www.tcpdump.org/
- **Mininet:** http://mininet.org/
- **FRRouting:** https://frrouting.org/
- **Batfish:** https://batfish.org/
- **P4 Language:** https://p4.org/
- **Linux Networking Documentation:** https://www.kernel.org/doc/html/latest/networking/

### Courses
- **CS144: Computer Networking** (Stanford) — Full stack implementation
- **6.829: Computer Networks** (MIT) — Graduate networking
- **CS244: Advanced Topics in Networking** (Stanford) — Research-focused
- **Cloud Networking Specialization** (Coursera/Google Cloud)

---

## Appendix: Glossary of Terms

| Term | Definition |
|------|------------|
| **ACK** | Acknowledgment |
| **AEAD** | Authenticated Encryption with Associated Data |
| **AQM** | Active Queue Management |
| **AS** | Autonomous System |
| **BGP** | Border Gateway Protocol |
| **BDP** | Bandwidth-Delay Product |
| **CIDR** | Classless Inter-Domain Routing |
| **CoDel** | Controlled Delay (AQM algorithm) |
| **CUBIC** | TCP congestion control algorithm |
| **DPDK** | Data Plane Development Kit |
| **ECMP** | Equal-Cost Multi-Path |
| **ECN** | Explicit Congestion Notification |
| **EVPN** | Ethernet VPN |
| **FIB** | Forwarding Information Base |
| **gRPC** | Google Remote Procedure Call |
| **HOL** | Head-of-Line blocking |
| **IGP** | Interior Gateway Protocol |
| **LACP** | Link Aggregation Control Protocol |
| **LSA** | Link-State Advertisement |
| **MSS** | Maximum Segment Size |
| **MTU** | Maximum Transmission Unit |
| **NAT** | Network Address Translation |
| **NDP** | Neighbor Discovery Protocol |
| **NIC** | Network Interface Card |
| **NVLink** | NVIDIA high-speed GPU interconnect |
| **OSPF** | Open Shortest Path First |
| **P4** | Programming language for data planes |
| **PFC** | Priority Flow Control |
| **QUIC** | Quick UDP Internet Connections |
| **RDMA** | Remote Direct Memory Access |
| **RIB** | Routing Information Base |
| **RoCE** | RDMA over Converged Ethernet |
| **RTT** | Round-Trip Time |
| **RTO** | Retransmission Timeout |
| **SACK** | Selective Acknowledgment |
| **SDN** | Software-Defined Networking |
| **SLO** | Service Level Objective |
| **SMT** | Simultaneous Multithreading |
| **SNI** | Server Name Indication |
| **STP** | Spanning Tree Protocol |
| **TCAM** | Ternary Content-Addressable Memory |
| **TE** | Traffic Engineering |
| **TLB** | Translation Lookaside Buffer |
| **TLS** | Transport Layer Security |
| **ToS** | Type of Service |
| **VLAN** | Virtual LAN |
| **VXLAN** | Virtual Extensible LAN |
| **WAF** | Web Application Firewall |

---

## Final Notes

This syllabus represents a comprehensive, layered curriculum for networking engineering. It is designed to be iterative — revisit earlier phases as you advance, as deeper understanding reveals new connections between layers.

**The ultimate goal is not just to configure networks, but to understand them deeply enough to design, optimize, debug, and secure systems that span from a single NIC to planet-scale AI infrastructure.**

---

*Document Version: 2026.05.17*  
*Maintained by: Senior Curriculum Designer — Networking & Distributed Systems Track*  
*Next Review Date: 2026.08.17*