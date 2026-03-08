# 06 - Physical Layer and Cabling

While logical addressing (IP) and hardware addressing (MAC) handle the routing and switching of data, nothing moves without the **Physical Layer (Layer 1)**. In cybersecurity, specifically in Physical Penetration Testing (Red Teaming), understanding how physical signals are transmitted is crucial for network tapping, sniffing, and unauthorized device configuration.

Most local area networks (LANs) rely on Ethernet technology, which uses copper cabling to transmit data via electrical signals. The standard connector used for these cables is the **RJ-45** connector.

## 🎨 Ethernet Wiring Standards

Inside a standard Unshielded Twisted Pair (UTP) Ethernet cable, there are 8 smaller wires, color-coded and twisted together into 4 pairs to prevent electromagnetic interference (crosstalk).

When terminating (crimping) an RJ-45 connector, the global standard dictates a specific color sequence. The most common standard is **T568B**:

1. White/Orange
2. Orange
3. White/Green
4. Blue
5. White/Blue
6. Green
7. White/Brown
8. Brown

Depending on the arrangement of these wires on both ends of the cable, we get different types of connections.

## 🔌 Types of Network Cables

How you connect devices dictates what type of cable you need. The general rule of thumb is:

- **Different types of devices** (e.g., PC to Switch) use a **Straight-Through** cable.
- **Same types of devices** (e.g., Switch to Switch, PC to PC) use a **Crossover** cable.

### 1. Straight-Through Cable

This is the most standard network cable. Both ends of the cable use the exact same color standard (e.g., T568B on both ends). Pin 1 on one end connects to Pin 1 on the other.

**Use cases (Connecting unlike devices):**

- PC to Switch
- PC to Hub
- Switch to Router
- Hub to Router

### 2. Crossover Cable

In the past, if you wanted to connect two computers directly without a switch in the middle, a straight-through cable wouldn't work because both PCs would try to "transmit" data on the same wire, causing a collision.
A crossover cable solves this by crossing the transmit (TX) and receive (RX) pins. One end uses the T568A standard, and the other uses T568B.

_(Note: Modern network cards have a feature called Auto-MDIX, which automatically detects and corrects the cable type via software, making physical crossover cables less necessary today. However, the concept remains fundamental.)_

**Use cases (Connecting like devices):**

- PC to PC
- Switch to Switch
- Hub to Hub
- Router to Router

### 3. Rollover Cable (Console Cable)

This is a very specific, flat, light-blue cable used almost exclusively to manage network devices out-of-band. The pinout on one end is completely reversed on the other end (Pin 1 to Pin 8, Pin 2 to Pin 7, etc.).

**Use cases:**

- Connecting a PC's serial port (or USB adapter) to the **Console Port** of a Cisco Router or Switch.
- This is how network administrators (and physical penetration testers) perform the initial configuration or password recovery on a network device before it even has an IP address.
