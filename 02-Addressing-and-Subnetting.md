# 02 - Addressing and Subnetting

In the previous chapter, we learned how data moves through the TCP/IP layers. But how do devices actually find each other in a massive network? This is where addressing comes into play. We use two main types of addresses: **Physical (MAC)** and **Logical (IP)**.

## 🏷️ MAC Addresses (Media Access Control)

Communication at the Data Link layer relies on MAC addresses. Every Network Interface Card (NIC) is manufactured with a unique identifier.
A MAC address is a **48-bit** physical address, usually represented in hexadecimal format (e.g., `00:1A:2B:3C:4D:5E`).

The first 24 bits (3 octets) are assigned by the **IANA** (Internet Assigned Numbers Authority) to the manufacturer, acting as an Organizationally Unique Identifier (OUI). The remaining 24 bits are assigned by the manufacturer.
You can find your MAC address in Windows using the command line:

```cmd
ipconfig /all
```

## 🔍 ARP: How IP and MAC Work Together

Two devices that know each other's MAC addresses can communicate directly. But how do they learn these addresses? Through IP addresses and ARP (Address Resolution Protocol).

When a packet leaves your computer, the IP address tells it the final destination, but the MAC address tells it exactly which device to jump to next on the local network.

If your computer knows the target's IP but not its MAC address, it sends an ARP Request to the entire network: "Who has this IP address? Send me your MAC address!"

- **Broadcast**: Sending a message to all devices on a network (like an ARP Request). Consumes bandwidth.
- **Unicast**: A direct message from one device to another (like the ARP Reply).
- **Multicast**: Sending a message to a specific group of devices, saving bandwidth compared to broadcast.

## 🌍 IP Addressing (IPv4)

Computers must speak the same language to communicate. An IP (Internet Protocol) address ensures devices don't conflict. If two devices have the same IP on a network, a collision occurs, and communication drops.

An IPv4 address is 32 bits long, divided into 4 sections of 8 bits each, called octets.

Example: `11010011.10101011.00010101.10011001 (Binary)` -> `211.171.21.153 (Decimal)`.

### IP Address Classes

- **Class A**: 0.0.0.0 - 127.255.255.255
- **Class B**: 128.0.0.0 - 191.255.255.255
- **Class C**: 192.0.0.0 - 223.255.255.255
- **Class D**: 224.0.0.0 - 239.255.255.255 (Multicast)
- **Class E**: 240.0.0.0 - 255.255.255.255 (Experimental)

### Special IP Ranges

- **Private IPs**: Used in local networks (LAN). They cannot access the internet directly without NAT.
  - 10.0.0.0 - 10.255.255.255
  - 172.16.0.0 - 172.31.255.255
  - 192.168.0.0 - 192.168.255.255
- **Loopback IP** (127.0.0.1): Represents your own local machine (localhost). Used for testing services on your computer.
- **Link-Local** (169.254.x.x): Assigned automatically by your OS when a DHCP server is unavailable.
- **Public IPs**: Unique addresses used on the internet, managed by Regional Internet Registries (RIRs) like RIPE.

## 🧮 Subnetting and Subnet Masks

A Subnet Mask divides an IP address into two parts: the Network portion and the Host portion.
For two devices to communicate directly, they must be on the same network. Computers perform a logical AND operation between their IP and the Subnet Mask to find their Network ID.

The formula to calculate the number of usable hosts in a subnet is:
**Number of Hosts = $2^n - 2$** (Where 'n' is the number of host bits. We subtract 2 because the Network IP and Broadcast IP cannot be assigned to devices).

**CIDR Notation**: Instead of writing 255.255.255.0, we count the number of network bits (1s in binary). Since there are 24 ones, we write it as `/24`. Example: `192.168.1.0/24`.

## 🛠️ Subnetting Example (Classless)

Imagine your manager gives you the `10.100.100.0/24` block. You need to divide it into 3 departments: 50 hosts, 20 hosts, and 10 hosts.

- **Dept 1 (50 hosts)**: We need $2^n - 2 \ge 50$. The smallest $n$ is 6. ($2^6 = 64$).
  - Network bits = 32 - 6 = 26. Subnet mask is `/26`.
  - Network: `10.100.100.0/26` (Usable range: `.1` to `.62`, Broadcast: `.63`)

- **Dept 2 (20 hosts)**: We need $2^n - 2 \ge 20$. Smallest $n$ is 5. ($2^5 = 32$).
  - Network bits = 32 - 5 = 27. Subnet mask is `/27`.
  - Network starts where the last one ended: `10.100.100.64/27`

- **Dept 3 (10 hosts)**: We need $2^n - 2 \ge 10$. Smallest $n$ is 4. ($2^4 = 16$).
  - Network bits = 32 - 4 = 28. Subnet mask is `/28`.
  - Network starts next: `10.100.100.96/28`

_Note: For a point-to-point router connection, you only need 2 IPs. The subnet mask used is `/30` (4 IPs total: 1 Network, 1 Broadcast, 2 Usable)._

## 🚪 Default Gateway

If a client wants to communicate with a device on a different network (like the Internet), the ARP request won't work because broadcast traffic doesn't pass through routers.
Instead, the client sends the packet to its Default Gateway. A gateway is a routing device (like your home modem or a corporate router) that knows how to forward packets outside your local network.
