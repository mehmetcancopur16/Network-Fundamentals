# 09 - Wireless Networking and Security

In physical penetration testing, if you cannot plug a cable into a network switch, your next target is the airwaves. Wireless networks (Wi-Fi) transmit data using radio frequencies. Because the data is flying through the air in all directions, anyone with an antenna within range can intercept it. This makes wireless networking a critical domain in cybersecurity.

## 📡 IEEE 802.11 Standards and Frequencies

Wi-Fi networks operate under the **IEEE 802.11** family of standards. They primarily transmit data over two main radio frequency bands:

* **2.4 GHz Band:** Has a longer range and passes through solid objects (like walls) much better. However, it is slower and highly congested because it only has 3 non-overlapping channels (1, 6, and 11).
* **5 GHz Band:** Has a shorter range and struggles with solid objects, but it is much faster, supports more channels, and experiences less interference.



**Common 802.11 Standards:**
* `802.11n` (Wi-Fi 4): Uses both 2.4 GHz and 5 GHz.
* `802.11ac` (Wi-Fi 5): Operates strictly in the 5 GHz band. Much faster data rates.
* `802.11ax` (Wi-Fi 6): Operates in both bands with massive efficiency improvements for handling multiple devices simultaneously.

## 🏷️ Wireless Concepts

When you scan for Wi-Fi networks (e.g., using a cybersecurity tool like `airodump-ng`), you will encounter a few key terms:

* **SSID (Service Set Identifier):** The human-readable name of the network (e.g., "Corporate_Guest_WiFi").
* **BSSID (Basic Service Set Identifier):** The actual MAC address of the wireless access point (router) broadcasting that specific SSID.
* **Beacon Frames:** Access points constantly broadcast "beacons" into the air to announce their presence, SSID, and security capabilities to nearby devices.

## 🔒 Wi-Fi Security Protocols

Since anyone can "sniff" the radio waves, encryption is absolutely mandatory. If a network is "Open" (no password), all traffic is transmitted in plain text, making users extremely vulnerable to packet sniffing and Man-in-the-Middle (MitM) attacks.

### 1. WEP (Wired Equivalent Privacy)
* Introduced in 1997, utilizing the RC4 encryption algorithm.
* **Cybersecurity Note:** WEP is completely broken due to a flawed Initialization Vector (IV). An attacker can easily crack a WEP password in minutes by capturing enough packets. **Never use WEP.**

### 2. WPA (Wi-Fi Protected Access)
* A temporary fix introduced after WEP was cracked. It used TKIP (Temporal Key Integrity Protocol).
* It is now considered obsolete and is also vulnerable to various attacks.

### 3. WPA2 (Wi-Fi Protected Access II)
* The most common standard in use today. It uses the highly secure **AES (Advanced Encryption Standard)** algorithm via CCMP.
* **The 4-Way Handshake:** When a client connects to a WPA2 network with the correct password, the router and the client perform a 4-way handshake to establish a secure encryption key for their session.
* **Cybersecurity Note (The Vulnerability):** While AES encryption itself is solid, WPA2 is vulnerable to **Offline Dictionary Attacks**. A hacker can force a user to disconnect (Deauthentication Attack), capture the 4-Way Handshake when the user automatically reconnects, and then take that handshake offline to crack the password using powerful graphics cards (e.g., using Hashcat or John the Ripper).



### 4. WPA3 (Wi-Fi Protected Access III)
* The latest and most secure standard. It replaces the vulnerable 4-Way Handshake with **SAE (Simultaneous Authentication of Equals)**.
* **Cybersecurity Note:** SAE completely mitigates offline dictionary attacks. Even if an attacker captures the connection process, they cannot take it offline to guess the password. They must interact with the router for every single guess, making brute-force attacks practically impossible.
