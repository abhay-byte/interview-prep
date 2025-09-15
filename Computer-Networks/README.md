### **Computer Networks: 10 Theoretical Questions**

**1. Q: Compare the OSI model and the TCP/IP model. Which is more practical and why?**
*   **A:**
    *   **OSI Model (Open Systems Interconnection):** A 7-layer theoretical model developed as a standard for network communication. Its layers are: Physical, Data Link, Network, Transport, Session, Presentation, and Application. It is a highly detailed, prescriptive model.
    *   **TCP/IP Model:** A 4-layer (or sometimes 5-layer) descriptive model that is the practical foundation of the modern internet. Its layers are: Network Access (Link), Internet, Transport, and Application.
    *   **Practicality:** The **TCP/IP model is more practical** because it was developed alongside the protocols that run the internet (like TCP and IP). It is less rigid and more accurately describes real-world networking. The OSI model is often used as a teaching tool for its clear separation of concerns, but its protocols are not widely implemented.

**2. Q: What are the primary differences between TCP and UDP? Provide a clear use case for each.**
*   **A:**
    *   **TCP (Transmission Control Protocol):** A **connection-oriented** protocol that guarantees reliable, ordered data delivery. It establishes a connection via a three-way handshake and uses sequence numbers, acknowledgements, and retransmissions to ensure data integrity. This reliability comes with higher overhead.
        *   **Use Case:** Web browsing (HTTP/HTTPS), file transfer (FTP), and email (SMTP), where every piece of data must arrive correctly and in order.
    *   **UDP (User Datagram Protocol):** A **connectionless** protocol that provides a simple, fast, but unreliable "best-effort" delivery. It sends packets (datagrams) without establishing a connection or checking for delivery. It has very low overhead.
        *   **Use Case:** Live video/audio streaming, online gaming, and DNS lookups, where speed is more critical than 100% reliability, and losing a few packets is acceptable.

**3. Q: How does TCP establish a connection and ensure data reliability?**
*   **A:** TCP ensures reliability through several key mechanisms:
    *   **Three-Way Handshake:** To establish a connection, it uses a SYN (synchronize), SYN-ACK (synchronize-acknowledge), and ACK (acknowledge) packet exchange to ensure both client and server are ready to communicate.
    *   **Sequence Numbers:** TCP assigns a sequence number to each byte of data it sends. This allows the receiver to reassemble the packets in the correct order, even if they arrive out of order.
    *   **Acknowledgements (ACKs):** The receiver sends cumulative acknowledgements back to the sender, confirming which bytes of data have been successfully received.
    *   **Retransmission Timeout:** If the sender does not receive an ACK for a segment within a certain time (the retransmission timeout), it assumes the packet was lost and sends it again.

**4. Q: Explain the difference between Flow Control and Congestion Control in TCP.**
*   **A:**
    *   **Flow Control:** A mechanism to prevent a fast sender from overwhelming a slow receiver. The receiver advertises a "receive window" size in its ACKs, telling the sender how much buffer space it has available. The sender agrees not to send more data than the receiver can handle. This is a point-to-point mechanism between two endpoints.
    *   **Congestion Control:** A mechanism to prevent a sender from overwhelming the **network** itself. The sender monitors network conditions (like packet loss or delay) to infer congestion. If congestion is detected, the sender reduces its transmission rate (its "congestion window"). This is a network-aware mechanism.

**5. Q: Describe the process of a DNS lookup. What happens when you type a URL in a browser?**
*   **A:** DNS (Domain Name System) translates human-readable domain names (like `www.google.com`) into machine-readable IP addresses. The process is typically recursive:
    1.  **Check Local Cache:** The browser/OS first checks its own cache to see if it already knows the IP.
    2.  **Resolver Query:** If not cached, the OS queries a **DNS Resolver** (usually provided by the ISP).
    3.  **Root Server Query:** The Resolver queries a **Root DNS Server**, which doesn't know the IP but redirects the resolver to the correct Top-Level Domain (TLD) server (e.g., the `.com` server).
    4.  **TLD Server Query:** The Resolver then queries the **TLD Server**, which redirects it to the **Authoritative Name Server** for the specific domain (e.g., `google.com`).
    5.  **Authoritative Server Query:** Finally, the Resolver queries the **Authoritative Name Server**, which holds the actual IP address record and returns it.
    6.  **Return and Cache:** The Resolver returns the IP address to the OS/browser, which can now initiate a TCP connection. The result is cached locally for future use.

**6. Q: What is the purpose of NAT (Network Address Translation)?**
*   **A:** NAT is a method used by routers to allow multiple devices in a private network (using private IP addresses like `192.168.x.x`) to share a single public IP address for accessing the internet. When an internal device sends a packet to the internet, the router replaces the private source IP address with its own public IP address and keeps a record in a NAT table. When the response comes back, the router uses the table to translate the public IP back to the correct private IP and forwards it to the device. This was crucial for conserving the limited IPv4 address space.

**7. Q: How does HTTPS provide a secure connection compared to HTTP?**
*   **A:** HTTPS (Hypertext Transfer Protocol Secure) secures the connection by layering HTTP on top of the **SSL/TLS (Secure Sockets Layer/Transport Layer Security)** protocol. SSL/TLS provides three key security guarantees:
    1.  **Encryption:** It encrypts the data exchanged between the browser and the server, making it unreadable to anyone who might intercept it (man-in-the-middle attack).
    2.  **Authentication:** It uses digital certificates (issued by a Certificate Authority) to verify that you are communicating with the legitimate server and not an impostor.
    3.  **Integrity:** It uses message authentication codes (MACs) to ensure that the data has not been tampered with or altered during transit.

**8. Q: What is the function of ARP (Address Resolution Protocol)?**
*   **A:** ARP operates at the boundary of Layer 2 (Data Link) and Layer 3 (Network). Its function is to **resolve a Layer 3 (logical) IP address into a Layer 2 (physical) MAC address** within a local network segment. When a host needs to send a packet to another host on the same LAN, it knows the destination IP address but not its hardware MAC address. It broadcasts an ARP request ("Who has this IP address?"), and the host with that IP replies with its MAC address. This mapping is then cached in an ARP table for future use.

**9. Q: What is a subnet mask and why is subnetting used?**
*   **A:** A **subnet mask** is a 32-bit number that divides an IP address into two parts: the **network prefix** and the **host identifier**. The mask specifies which part of the IP address identifies the network and which part identifies the specific host on that network.
    **Subnetting** is the process of breaking a large network into smaller, more manageable sub-networks. This is done for several reasons:
    *   **Efficiency:** It reduces the size of broadcast domains, preventing network traffic from flooding the entire network.
    *   **Security:** It allows for the isolation of different network segments. For example, the finance department's network can be kept separate from the guest Wi-Fi network.
    *   **Organization:** It simplifies network administration and management.

**10. Q: What is the difference between a router and a switch?**
*   **A:**
    *   **Switch:** A **Layer 2 (Data Link)** device. It operates within a single local area network (LAN). A switch learns the MAC addresses of the devices connected to its ports and uses this information to intelligently forward frames only to the specific port of the intended destination device.
    *   **Router:** A **Layer 3 (Network)** device. Its primary function is to connect different networks together and route traffic *between* them (e.g., connecting your home LAN to the internet). Routers use IP addresses to make decisions about the best path to forward packets to their final destination across multiple networks.