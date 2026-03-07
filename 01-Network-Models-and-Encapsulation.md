# 01 - Network Models and Encapsulation

The internet, one of the most vital mass communication tools today, is used in almost every aspect of life. Its widespread adoption necessitated the creation of a robust and highly structured infrastructure. Building this infrastructure requires a deep understanding of network topologies, cabling techniques, and communication models.

To transmit information securely and accurately from a source to a destination—whether printing a document in an office or browsing a website—a well-structured network must be in place. To understand this, we must first look at the foundation of network communication: **TCP/IP**.

## 📜 A Brief History of TCP/IP

In May 1974, the IEEE published a paper titled _"A Protocol for Packet Network Intercommunication"_ by Vint Cerf and Bob Khan. They defined a network protocol using **packet-switching** to share resources among nodes on a network, laying the groundwork for TCP.

TCP/IP was originally designed to meet the data communication needs of the U.S. Department of Defense (DoD). In the late 1960s, the Advanced Research Projects Agency (ARPA) aimed to create a vendor-independent protocol to exchange data with universities. This effort led to the creation of **ARPANET** in 1969, the first wide-area, packet-switched network in internet history, initially operating with just four nodes.

## 🏗️ TCP/IP and OSI Models

To understand how devices communicate, we use network models. The two most prominent are the **OSI (Open Systems Interconnection) Model** (7 layers) and the **TCP/IP Model** (4 or 5 layers, depending on the literature). Both serve to standardize network communication.

[Image of TCP/IP vs OSI model layers]

### The TCP/IP Layers Explained

1. **Application Layer:** This layer contains the application attempting to send data and the file format it uses. It includes protocols necessary to access the network, such as **HTTP, SMTP, and FTP**. Unlike the OSI model, this layer also encompasses the functions of OSI's Presentation and Session layers.
2. **Transport Layer:** This layer defines _how_ the data is sent. It handles quality of service, reliable data transfer, flow control, and error control. The primary protocols here are **TCP** and **UDP**.
   - **TCP (Transmission Control Protocol):** Connection-oriented and reliable. It establishes a logical connection before sending data and guarantees that data arrives sequentially and without loss.
   - **UDP (User Datagram Protocol):** Connectionless and unreliable (best-effort). It is faster than TCP because it lacks extensive headers and error-checking mechanisms.

3. **Internet (Network) Layer:** Often called the IP layer, this is where **IP addresses** are added to the data, and routing decisions are made. Its main responsibility is to find the best path to the destination. Protocols include **IPv4, IPv6, ICMP, and IGMP**. **Routers** operate at this layer.

4. **Network Interface (Data Link Layer):** This layer handles the physical transmission of data within the same local network (LAN). It deals with error notification, network topology, and flow control. It uses **Hardware Addresses (MAC)** to deliver messages to specific devices. **Switches** operate here.

5. **Physical Layer:** This layer dictates how data bits (1s and 0s) are converted into electrical, light, or radio signals and transmitted over the physical medium (cables, air). **Hubs** operate at this layer.

---

## 📦 Encapsulation and Decapsulation

When two devices communicate, data doesn't just travel raw. As data moves down the layers from the sender's application to the physical network, each layer adds its own specific header (and sometimes a trailer). This process is called **Encapsulation**.

1. The data moves down, layer by layer, getting wrapped in headers.
2. It travels across the physical network.
3. Once it reaches the destination, the process is reversed. The data moves up the layers, and each layer reads and removes its corresponding header. This is called **Decapsulation**.

Each layer only understands and processes the header created by its peer layer on the other side.
