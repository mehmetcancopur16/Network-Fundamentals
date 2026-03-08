# 📖 Glossary of Networking Terms

A comprehensive dictionary of essential networking terminology used throughout this repository. Understanding these terms is foundational for any cybersecurity professional or network engineer.

---

- **ARP (Address Resolution Protocol):** Defined in RFC 826, it is the protocol used to map an IP address to a physical MAC address on a local network.
- **Bandwidth:** The range between the highest and lowest frequencies used in network signals. Commonly refers to the maximum throughput capacity of a network medium.
- **Binary:** A base-2 numbering system using only 1s and 0s. It is the foundation of all digital data representation.
- **Bit:** A single binary digit (1 or 0). Eight bits make up one byte.
- **Bridge:** A device used to connect two network segments, filtering and forwarding packets between them based on MAC addresses. It operates at Layer 2 (Data Link) and creates two separate collision domains.
- **Broadcast Domain:** A logical group of devices that will all receive a broadcast frame initiated by any single device in that group. Routers block broadcasts, keeping domains isolated.
- **CIDR (Classless Inter-Domain Routing):** A method of IP addressing that replaces older classful network assignments. It uses a slash notation (e.g., `/24`) to represent the subnet mask.
- **Collision:** Occurs on an Ethernet network when two nodes transmit data at the exact same time on a shared medium, resulting in corrupted frames.
- **Collision Domain:** A network segment where data collisions can occur. Hubs create a single collision domain, whereas switches create a separate collision domain for each port.
- **Connectionless:** A data transfer method that does not establish a virtual circuit or guarantee delivery before sending data (e.g., UDP).
- **Connection-Oriented:** A data transfer method that establishes a virtual circuit (like a 3-way handshake) and uses acknowledgments for reliable delivery (e.g., TCP).
- **Crossover Cable:** An Ethernet cable used to connect devices of the same type directly (e.g., PC to PC, Switch to Switch).
- **Data Link Layer:** Layer 2 of the OSI model. Responsible for physical addressing (MAC), network topology, error notification, and flow control over a physical link.
- **De-encapsulation:** The process where a receiving layer removes the header information added by its peer layer on the sending device.
- **Default Route:** A static route (usually `0.0.0.0`) in a routing table used to forward frames when a specific destination network is unknown.
- **DNS (Domain Name System):** The protocol used to resolve human-readable hostnames (like `google.com`) into IP addresses.
- **Encapsulation:** The process where a layer adds its specific header information to the data payload received from the layer above it.
- **Ethernet:** A widely used LAN technology utilizing CSMA/CD over various cable types.
- **Fast Ethernet:** An Ethernet standard operating at 100 Mbps.
- **Frame:** The logical unit of data handled by the Data Link layer.
- **FTP (File Transfer Protocol):** A TCP/IP protocol used for transferring files between network nodes (RFC 959).
- **Handshake:** A sequence of transmissions exchanged between devices to establish and synchronize a connection.
- **Hop Count:** A routing metric that counts the number of routers a packet must pass through to reach its destination.
- **Hub:** A physical layer device that acts as a multi-port repeater. It broadcasts incoming signals to all ports, creating a single collision domain.
- **IEEE (Institute of Electrical and Electronics Engineers):** A professional organization that defines standards in computing and communications (e.g., IEEE 802.3 for Ethernet).
- **Internet:** The global "network of networks," connecting vastly different platforms via standard TCP/IP protocols.
- **IP (Internet Protocol):** A connectionless Network layer protocol responsible for addressing and routing packets.
- **IP Address:** A logical, dotted-decimal address uniquely identifying a device on a TCP/IP network.
- **IP Multicast:** A routing technique allowing traffic to be replicated from one source to a specific group of destinations.
- **LAN (Local Area Network):** A network connecting devices within a limited geographical area, like a home or office building.
- **LAN Switch:** A high-speed bridging device that forwards data frames based on MAC addresses, operating at the Data Link layer.
- **Layer:** A term describing the hierarchical levels of the OSI or TCP/IP models used to structure network communications.
- **MAC (Media Access Control):** A sublayer of the Data Link layer responsible for hardware addressing and media access.
- **MAC Address:** A 48-bit physical hardware address burned into a Network Interface Card (NIC).
- **Maximum Hop Count:** The limit on how many routers a packet can traverse before being discarded (to prevent infinite network loops).
- **Multicast:** Communication targeted from a single sender to multiple specific receivers (unlike a broadcast, which goes to everyone).
- **NAT (Network Address Translation):** A mechanism that translates private IP addresses into a public IP address, allowing local devices to access the internet.
- **Native VLAN:** The default VLAN (usually VLAN 1) configured to carry untagged traffic across a trunk link.
- **Octet:** An 8-bit segment of an IP address (also known as a byte).
- **OSI (Open Systems Interconnection):** An international standard framework for network communication.
- **OSI Reference Model:** A conceptual 7-layer model defining the functions of a telecommunication or computing system.
- **OUI (Organizationally Unique Identifier):** The first 24 bits of a MAC address, assigned by the IEEE to identify the hardware manufacturer.
- **Packet:** The basic logical unit of data routed over a network at Layer 3.
- **Packet Switching:** A network technology where data is broken into packets and routed dynamically over shared infrastructure.
- **Physical Layer:** Layer 1 of the OSI model. It converts logical bits into electrical, optical, or radio signals for physical transmission.
- **Router:** A Layer 3 networking device that uses metrics to forward packets between different networks.
- **Sequencing:** The process of numbering data segments so the receiver can reassemble them in the correct order.
- **Subnetwork (Subnet):** A smaller, segmented portion of a larger IP network, created for better routing and management.
- **Switch:** A Layer 2 device that filters and forwards frames based on MAC addresses.
- **Telnet:** A legacy, unencrypted terminal emulation protocol used for remote device management.
- **TFTP (Trivial File Transfer Protocol):** A lightweight, connectionless version of FTP used for simple file transfers without directory browsing.
- **TTL (Time to Live):** A value in an IP packet header that decreases by 1 at each router hop. When it hits 0, the packet is discarded.
- **UDP (User Datagram Protocol):** A connectionless, fast Transport layer protocol that does not guarantee data delivery.
- **UTP (Unshielded Twisted-Pair):** The standard copper cabling used to connect local network devices.
- **VLAN (Virtual LAN):** A logical grouping of network devices into a single broadcast domain, regardless of their physical location on a switch.

---

_End of Glossary._
