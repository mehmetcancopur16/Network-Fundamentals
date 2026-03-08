# 05 - Network Routing and NAT

We know that different VLANs and different subnets cannot communicate directly. So, how do we bridge the gap? This is where **Routing** (Layer 3) comes in.

Routers act as the post offices of the network. They maintain a **Routing Table** containing maps of how to reach different networks. If a packet's destination is outside the local network, the router determines the best path to send it forward.

## 🚪 The Default Gateway

As discussed in the addressing chapter, when a client wants to talk to an unknown network (like the Internet), it sends its packets to the **Default Gateway**. Your home modem is a perfect example of a default gateway—it receives all your web traffic and routes it to the ISP (Internet Service Provider).

## 📯 Step-by-Step: The Journey of a Packet

Let's break down exactly what happens when Host A (`192.168.5.2`) tries to `ping` Host B (`10.0.0.5`) on a different network, connected by a router.

1. **ICMP Creation:** Host A generates an ICMP Echo Request.
2. **IP Encapsulation:** The ICMP request is passed to the IP layer. An IP packet is created with the Source IP (`192.168.5.2`) and Destination IP (`10.0.0.5`).
3. **Network Check:** The IP layer checks if the destination is on the local network. It is not.
4. **Gateway Forwarding:** Since it's a remote network, Host A must send the packet to its Default Gateway (`192.168.5.1` - the router's interface).
5. **ARP Request:** To send the packet locally to the router, Host A needs the router's MAC address. It broadcasts an ARP request.
6. **Frame Creation:** Once the router's MAC is learned, the IP packet is encapsulated into a Layer 2 Frame and sent to the router.
7. **Router Receives Frame:** The router receives the frame and strips away the Layer 2 header.
8. **Routing Table Lookup:** The router inspects the Destination IP (`10.0.0.5`) and checks its Routing Table for a match.
9. **Discard (If No Match):** If the router doesn't know how to reach the `10.0.0.0` network, it drops the packet and sends a "Destination Unreachable" message back to Host A.
10. **Forwarding (If Match Found):** The router finds that `10.0.0.0` is connected to another interface (e.g., Fa0/1).
11. **Second ARP Request:** The router now needs Host B's MAC address. It sends an ARP broadcast out of Fa0/1.
12. **Frame Delivery:** After receiving Host B's MAC, the router encapsulates the packet into a new frame and sends it to Host B.
13. **Echo Reply:** Host B receives the ping, generates an Echo Reply, and the entire process happens in reverse.
14. **Success!** Host A receives the reply and displays a successful ping result on the screen.

## 🗺️ Building the Routing Table

Routers build their routing tables in three primary ways:

### 1. Directly Connected Routes

When you assign an IP address to a router's interface and turn it on, the router automatically adds that specific network to its routing table.
_Example: If Fa0/0 is `192.168.5.1/24`, the router automatically knows how to reach the `192.168.5.0/24` network._

### 2. Static Routing

When networks are not directly connected, network administrators manually teach the router how to reach them. You must tell the router the Destination Network, Subnet Mask, and the Next-Hop IP (where to send the packet next).

**Example:**
To tell R1 how to reach the `192.168.2.0/24` network via R2 (`192.168.12.2`):

```text
192.168.2.0   255.255.255.0   192.168.12.2
(Target Net)  (Subnet Mask)   (Next-Hop IP)
```

**Crucial Rule:** Routing is a two-way street! If R1 knows how to send a packet to R3, R3 must have a static route pointing back to R1, otherwise, the return packet will be dropped.

### 3. Default Route (0.0.0.0)

A Default Route is the router's version of a Default Gateway. It tells the router: "If you receive a packet for a network that is NOT in your routing table, send it here."

```text
0.0.0.0   0.0.0.0   192.168.1.1
```

## 🎯 Longest Prefix Match Rule

If a router has multiple routes to the same destination, it always chooses the most specific one (the one with the longest subnet mask).
For example, if a router has a route for `192.168.10.0/24` and another for `192.168.10.13/32`, a packet destined for `.13` will take the `/32` route. A `/32` mask (a single host) is the most specific route possible.

## 🎭 NAT (Network Address Translation)

We know that Private IPs (like 192.168.x.x or 10.x.x.x) cannot be routed on the public internet. If they can't be routed, how are you reading this GitHub page right now? The answer is NAT.

NAT translates your internal Private IP address into a Public IP address before the packet leaves your network.
When the response comes back from the internet to your Public IP, the NAT device (usually your router or firewall) remembers the translation and forwards the packet back to your specific internal Private IP.

- This conserves the limited pool of IPv4 addresses.
- It adds a layer of security, as internal IPs are hidden from the outside world.
