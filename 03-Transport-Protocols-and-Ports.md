# 03 - Transport Protocols and Ports

Up to this point, we have operated in the lower layers (Physical, Data Link, and Network). Now, we move up to the **Transport Layer**, which decides _how_ data is delivered, and the **Application Layer**, where services reside.

End-user applications do not have direct access to the IP layer. Instead, two main Transport Layer protocols bridge the gap between the application and the network: **TCP** and **UDP**.

## 🚚 TCP vs. UDP

When an application sends data, developers must choose between reliability (TCP) and speed (UDP).

### 1. TCP (Transmission Control Protocol)

TCP is a **connection-oriented** and highly reliable protocol.

- It guarantees that data will arrive exactly as it was sent, without loss, and in the correct order.
- TCP fragments incoming data (e.g., into 64KB segments) and ensures sequential delivery.
- It expects a reply (acknowledgment) from the receiver for every segment sent. If a segment is lost in transit, TCP automatically retransmits it.

#### 🤝 The 3-Way Handshake

Before TCP sends any actual data, it must establish a logical connection between the client and the server. This is called the **3-Way Handshake**:

1. **SYN:** The client sends a synchronization packet (`SYN`) with a random sequence number (Seq) to the server.
2. **SYN-ACK:** The server receives the SYN, generates its own sequence number, adds 1 to the client's Seq number (to create the Ack number), and replies with a `SYN-ACK` packet.
3. **ACK:** The client receives the SYN-ACK, increments the numbers, and sends an `ACK` (Acknowledgment) packet back to the server.

_Boom! The connection is established, and data can now flow securely._

### 2. UDP (User Datagram Protocol)

UDP is a **connectionless** and unreliable protocol.

- It does NOT perform a 3-way handshake.
- It does NOT track lost packets, nor does it guarantee the order of delivery.
- Because it lacks these overheads, it is incredibly **fast**. It is preferred for real-time applications where a dropped frame is better than a delayed frame (e.g., VoIP calls, online gaming, live video streaming).

## 🚪 Ports: The Doors to Your Services

If an IP address is the street address of an apartment building, the **Port Number** is the specific apartment number.
A single server (with one IP address) can run multiple services simultaneously (e.g., a web server, an email server, and a database). Ports ensure that incoming traffic goes to the correct application.

There are a total of **65,535** ports.

- **Well-known ports (0 - 1024):** Reserved for standard, universally accepted services.
- **Ephemeral (Dynamic) ports (above 1024):** Used temporarily by the client OS as source ports when initiating a connection.

**Common Well-Known Ports:**

- `21` - FTP (File Transfer)
- `22` - SSH (Secure Shell)
- `25` - SMTP (Email Routing)
- `53` - DNS (Domain Name System)
- `80` - HTTP (Web)
- `443` - HTTPS (Secure Web)

### 🛠️ Port Troubleshooting Commands

To check if a specific port is open on your local machine (using the loopback address `127.0.0.1`):

```cmd
telnet 127.0.0.1 80
```

To view active connections and see which source ports your machine is currently using to reach external servers:

```cmd
netstat -an
```

## 🌍 DNS (Domain Name System)

IP addresses (like `86.108.193.199`) are hard for humans to remember. DNS (Port `53`) solves this by acting as the phonebook of the internet. It translates human-readable domain names (like `turkcell.com.tr`) into IP addresses.
_Note: DNS queries typically use UDP for speed._

**Clearing the DNS Cache:**
Operating systems cache DNS results to speed up future requests. If a website changes its IP or you encounter DNS spoofing, you need to flush this cache:

```cmd
ipconfig /flushdns
```

## 🔄 DHCP (Dynamic Host Configuration Protocol)

Assigning IP addresses manually (Static IP) to hundreds of computers in a corporate network is a nightmare. DHCP automates this by dynamically assigning an IP address, Subnet Mask, Default Gateway, and DNS server to devices as soon as they connect to the network.

When a device connects, it sends a Broadcast message to the entire network: "Is there a DHCP server here? I need an IP address!" The server responds and leases an IP to the client.

**DHCP Commands (Windows):**

```cmd
# View current IP configuration, including DHCP server
ipconfig /all

# Release your current DHCP IP address
ipconfig /release

# Request a new IP address from the DHCP server
ipconfig /renew
```
