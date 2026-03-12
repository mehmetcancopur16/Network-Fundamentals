# 10 - Network Security Appliances (Firewalls, IDS/IPS, VPNs & Proxies)

Building a network is only half the battle; defending it is where true cybersecurity begins. As packets flow across the globe, malicious actors constantly attempt to intercept data, exploit vulnerabilities, or flood servers with traffic (DDoS). 

To secure the perimeter and internal zones of a network, organizations deploy specialized security appliances. Understanding how these devices work is crucial for Blue Teams (Defenders) to configure them, and for Red Teams (Attackers) to bypass them.

## 🧱 1. Firewalls

A firewall is the primary line of defense. It monitors and controls incoming and outgoing network traffic based on predetermined security rules. It acts as a barrier between a trusted internal network and an untrusted external network (like the Internet).



### Types of Firewalls:
* **Stateless (Packet Filtering) Firewalls:** The oldest type. They inspect each packet individually against a set of rules (ACLs - Access Control Lists) looking at the Source/Destination IP and Ports. They do not remember previous packets.
* **Stateful Firewalls:** These are smarter. They remember the "state" of a connection (e.g., the TCP 3-Way Handshake). If an internal PC requests a website, the stateful firewall remembers this and automatically allows the website's reply back in, without needing a specific rule for the return traffic.
* **NGFW (Next-Generation Firewalls):** Modern firewalls (like Palo Alto or Fortinet) go beyond IPs and ports. They perform **Deep Packet Inspection (DPI)** to understand the actual application (e.g., blocking Facebook chat while allowing Facebook login) and integrate antivirus and intrusion prevention.

## 🚨 2. IDS vs. IPS (Intrusion Detection/Prevention)

While firewalls block traffic based on rules (like a bouncer at a club checking IDs), they don't always catch someone behaving badly once they are inside. This is where IDS and IPS come in.

* **IDS (Intrusion Detection System):** A passive system. It analyzes a copy of the network traffic looking for known attack signatures or abnormal behavior. If it spots an attack, it logs it and sends an alert to the administrator, but it **does not** stop the traffic.
* **IPS (Intrusion Prevention System):** An active system. It sits inline with the traffic. If it detects malicious activity, it can instantly drop the packet, block the attacker's IP, or reset the connection.



### Detection Methods:
1. **Signature-Based:** Compares traffic against a database of known malware hashes or attack patterns (like an antivirus). Fails against brand new (Zero-Day) attacks.
2. **Anomaly/Behavior-Based:** Uses machine learning to establish a "baseline" of normal network traffic. If suddenly a printer tries to connect to an external server in Russia at 3 AM, it flags it as an anomaly.

## 🚇 3. VPNs (Virtual Private Networks)

A VPN creates a secure, encrypted tunnel over an untrusted network (the Internet). If an attacker intercepts VPN traffic (using a packet sniffer like Wireshark), they will only see encrypted gibberish.



* **Remote Access VPN:** Used by an individual employee working from home to securely connect to the corporate network (often using protocols like OpenVPN, WireGuard, or SSL/TLS).
* **Site-to-Site VPN:** Used to connect two entire branch offices together over the internet as if they were on the same local network. This relies heavily on **IPsec (Internet Protocol Security)**, which encrypts packets at the Network Layer (Layer 3).

## 🎭 4. Proxies

A proxy server acts as an intermediary for requests from clients seeking resources from other servers. 

* **Forward Proxy:** Protects the **Client**. When internal users browse the internet, their traffic goes to the forward proxy first. The proxy fetches the webpage and sends it back to the user. This hides the user's internal IP, filters bad websites, and caches content to save bandwidth.
* **Reverse Proxy:** Protects the **Server**. Placed in front of web servers. When the internet tries to access a company's website, they hit the reverse proxy instead. It hides the real web server's IP, balances the load among multiple servers, and often provides SSL decryption (acting as a Web Application Firewall - WAF).
