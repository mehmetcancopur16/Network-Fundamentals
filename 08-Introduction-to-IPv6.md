# 08 - Introduction to IPv6 (Addressing and Subnetting)

We learned that IPv4 uses 32-bit addresses, providing roughly 4.3 billion unique IPs. With the explosion of smartphones, laptops, and IoT (Internet of Things) devices, the world simply ran out of IPv4 addresses. While NAT (Network Address Translation) bought us some time, the permanent solution is **IPv6**.

From a cybersecurity perspective, understanding IPv6 is critical. Many organizations deploy security tools (like firewalls and IDS) that monitor IPv4 traffic perfectly but completely ignore IPv6 traffic. Attackers often use IPv6 for stealthy lateral movement inside a compromised network.

## 🔢 The IPv6 Address Format

An IPv6 address is **128 bits** long. Instead of the decimal format used in IPv4, IPv6 uses **Hexadecimal** numbers.
It is written as 8 groups of 4 hexadecimal digits, separated by colons (`:`).

**Example of a full IPv6 Address:**
`2001:0DB8:0000:0042:0000:8A2E:0370:7334`

### ✂️ Rules for Shortening IPv6 Addresses
Looking at 128 bits is exhausting, so there are two rules to compress them:

1. **Omit Leading Zeros:** You can remove the zeros at the beginning of any group. 
   * `0DB8` becomes `DB8`
   * `0042` becomes `42`
   * `0000` becomes `0`
2. **Double Colon (`::`):** You can replace consecutive groups of all zeros with a double colon. **Rule: You can only use `::` ONCE in an address.**

**Compressing our example:**
* Original: `2001:0DB8:0000:0042:0000:8A2E:0370:7334`
* Apply Rule 1: `2001:DB8:0:42:0:8A2E:370:7334`
*(We cannot use the double colon here because there are no consecutive zero groups, just single zero groups).*

**Another Example:**
* Original: `2001:0DB8:0000:0000:0000:0000:0000:0001`
* Compressed: `2001:DB8::1`

## 🌍 Types of IPv6 Addresses

Unlike IPv4, IPv6 devices usually have multiple IP addresses assigned to the same network interface simultaneously.

1. **Global Unicast Address (Public IPs):** These are globally unique and routable on the internet. They typically start with `2000::/3`.
2. **Unique Local Address (Private IPs):** Used for local communications within a site. Similar to IPv4 private IPs (`192.168.x.x`). They start with `FC00::/7` or `FD00::/8`.
3. **Link-Local Address:** Every IPv6 interface automatically generates one. It is used to communicate with devices on the exact same local link (subnet) and is NOT routable. They always start with `FE80::/10`.
4. **Loopback Address:** Equivalent to `127.0.0.1` in IPv4. In IPv6, it is `::1`.

## 🚫 The Death of Broadcasts

One of the biggest changes in IPv6 is that **Broadcasts do not exist**. 
In IPv4, an ARP broadcast disrupts every device on the subnet. IPv6 replaces ARP with **NDP (Neighbor Discovery Protocol)**, which uses **Multicast**. 
Instead of shouting to the entire room, IPv6 politely sends a multicast message only to the specific group of devices that need to hear it, making networks much more efficient.

## 🧮 IPv6 Subnetting

Subnetting in IPv6 is actually easier than in IPv4 because there are so many addresses. The standard subnet mask for a local area network (LAN) is almost always **/64**.

This means the first 64 bits are the **Network ID** (assigned by your ISP or network admin), and the last 64 bits are the **Interface ID** (the host portion, often generated automatically from the device's MAC address using a method called EUI-64).

* **Network Prefix:** `2001:DB8:1:1::/64`
* You have 64 bits left for hosts, which equals $18,446,744,073,709,551,616$ IP addresses in a single subnet. You will never run out!

## 🛠️ IPv6 Troubleshooting Commands

Your toolkit works with IPv6 too:

```cmd
# Ping an IPv6 address
ping -6 google.com

# Trace the route over IPv6
tracert -6 google.com

# View your IPv6 configurations
ipconfig /all
```
