# 04 - Layer 2 Switching and VLANs

In previous chapters, we learned that devices use MAC addresses to communicate on a local network and rely on ARP broadcasts to find each other. But what happens when hundreds of devices broadcast at the same time? The network slows down, and security risks arise.

To solve this, we use **Layer 2 Switching** and **VLANs (Virtual Local Area Networks)**.

## 💥 Collision Domains vs. Broadcast Domains

Understanding how network devices separate traffic is crucial for network performance and security (especially when planning sniffing or man-in-the-middle attacks).

### 1. Collision Domains

A collision domain is a network segment where data packets can collide with one another when sent simultaneously. If a collision occurs, devices must wait and retransmit the data.

- **Hubs (Layer 1):** A hub simply repeats the electrical signal to all connected ports. It creates **1 Collision Domain** and **1 Broadcast Domain**. All devices share the same channel, leading to frequent collisions.
- **Bridges (Layer 2):** Think of a bridge as a 2-port switch. It separates the network into **2 Collision Domains**, improving efficiency.
- **Switches (Layer 2):** A switch intelligently forwards data (frames) based on MAC addresses. **Every port on a switch is a separate Collision Domain**. This means devices can communicate simultaneously without collisions.

### 2. Broadcast Domains

A broadcast domain is the logical area that a broadcast frame (like an ARP request) can reach.

- By default, **all ports on a switch belong to 1 Broadcast Domain**.
- **Routers (Layer 3)** stop broadcasts. **Every port on a router creates a separate Broadcast Domain**.

## 🎭 VLANs (Virtual Local Area Networks)

While switches isolate collision domains, they still forward broadcasts to all ports. If you want to isolate traffic—for example, keeping a "Guest Wi-Fi" completely separate from the "Internal Corporate Network"—you use **VLANs**.

A VLAN logically segments a physical switch into multiple virtual switches.

- **Security & Isolation:** A broadcast starting in VLAN 10 will **never** reach VLAN 20. Devices in different VLANs cannot communicate with each other directly (they require a router to bridge the gap).
- Operates at **Layer 2**.
- A maximum of **4096** VLANs can be created on a switch.

### 📌 Types of VLANs

1. **Default VLAN:** By default, all ports on a switch belong to VLAN 1. If no configuration is made, all connected devices can talk to each other.
2. **Data VLAN:** Configured specifically to carry standard user-generated data traffic.
3. **Voice VLAN:** Configured to carry voice traffic (VoIP). Requires prioritization for quality.
4. **Native VLAN:** Used on trunk links to carry untagged traffic. Usually defaults to VLAN 1.

## 🔌 Port Types and Frame Tagging

When you assign a VLAN to a switch port, you configure how the switch handles the frames entering and exiting that port.

### 1. Access Ports (Untagged Frames)

- An Access Port belongs to **only one VLAN**.
- End devices (like PCs or printers) do not understand VLAN tags.
- When a switch sends a frame to a PC out of an access port, it strips the VLAN information (**Untagged Frame**).

### 2. Trunk Ports (Tagged Frames)

- A Trunk Port can carry traffic for **multiple VLANs** simultaneously.
- Used for connections between two switches or a switch and a router.
- To distinguish which frame belongs to which VLAN, the sending switch adds a "Tag" to the frame header (**Tagged Frame**). The receiving switch reads this tag, removes it, and forwards it to the correct access port on the other side.
- You can also restrict which VLANs are allowed on a trunk port to save bandwidth and increase security.

### 3. Voice Ports

- Many modern switches allow you to connect an IP Phone and a PC to the **same physical switch port** to save cabling costs.
- The switch is configured with an Access VLAN (for the PC) and a Voice VLAN (for the phone).
- The switch tags the voice packets but leaves the data packets untagged, allowing the IP phone to separate the traffic locally and pass the data to the PC.
