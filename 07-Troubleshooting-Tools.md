# 07 - Network Troubleshooting and Discovery Tools

Before using advanced cybersecurity tools like Nmap or Wireshark, you must master the built-in command-line utilities provided by your operating system. Whether you are diagnosing a broken connection or performing initial network reconnaissance (recon) on a target, these tools are your first line of action.

Below are the most critical network troubleshooting commands (examples are based on Windows `cmd`, but similar commands exist in Linux/macOS).

## 🏓 1. Ping (Packet Internet Groper)

Written by Mike Muuss in 1983, `ping` is the easiest way to test the reachability of a host on an IP network. It uses **ICMP (Internet Control Message Protocol)** to send an _Echo Request_ packet (32 bytes by default) to the target. If the target is online and not blocking ICMP, it replies with an _Echo Reply_.

```cmd
ping 8.8.8.8
```

**TTL (Time to Live):** Look at the `TTL=` value in a successful ping response. TTL prevents packets from looping endlessly in a network. Every time a packet passes through a router (a hop), its TTL decreases by 1. If the TTL reaches 0, the router drops the packet and sends an "ICMP Time Exceeded" message back to the sender. Operating systems have different default starting TTL values (e.g., Windows is usually 128, Linux is 64), which can help in OS fingerprinting!

## 🗺️ 2. Tracert (Traceroute)

If ping tells you if a host is reachable, tracert tells you how your packets get there. It maps the exact path (router by router) from your machine to the destination.

```cmd
tracert google.com
```

_(On Linux/macOS, use `traceroute google.com`)_

It works by manipulating the TTL value. It sends the first packet with a TTL of 1 (so the first router drops it and replies), the second with a TTL of 2, and so on, building a list of every router (hop) along the way. This is excellent for finding exactly where a network connection is failing or understanding a target company's external network infrastructure.

## 📓 3. ARP Cache (arp -a)

As we learned, ARP resolves IP addresses to MAC addresses using broadcasts. However, computers don't want to broadcast every single time they send a packet. They save recent IP-to-MAC mappings in a local memory called the ARP Cache.

```cmd
arp -a
```

In a local network penetration test, running `arp -a` immediately shows you the IP and MAC addresses of other devices on the same subnet that your computer has recently talked to. It's a quick, stealthy way to discover local targets without sending noisy network scans.

## 📖 4. Nslookup (Name Server Lookup)

`nslookup` is a tool for querying the DNS (Domain Name System) to obtain domain name or IP address mapping. It is a fundamental tool for Information Gathering (OSINT).

```cmd
nslookup turkcell.com.tr
```

You can find the IP address of a website, or perform a "reverse lookup" to find the domain name associated with an IP address. You can also specify exactly which DNS server you want to query.

## 🧹 5. DNS Flush (ipconfig /flushdns)

Operating systems cache DNS results to load websites faster. However, if a website changes its IP, or if you are the victim of a DNS Spoofing (Poisoning) attack, your computer will keep going to the wrong IP address.

```cmd
ipconfig /flushdns
```

This command clears the local DNS cache, forcing the computer to ask the DNS server (like Google's 8.8.8.8) for the fresh, correct IP address.

## 🕵️ 6. Netstat (Network Statistics)

`netstat` is arguably one of the most important commands for a security analyst. It displays all active TCP and UDP connections, as well as the ports your computer is "listening" on.

```cmd
netstat -an
```

- `-a`: Displays all active connections and listening ports.
- `-n`: Displays addresses and port numbers in numerical form (prevents it from trying to resolve names, making the command run much faster).

**Cybersecurity Use Case:** If you suspect your machine is infected with malware or a backdoor, running `netstat -an` will show you exactly which ports are open and if your machine has an active, hidden connection to a malicious external IP address (Command and Control server).
