# 🌐 Multi-Building Enterprise Network

A multi-building enterprise network designed and configured using **Cisco Packet Tracer**.

This project demonstrates the practical implementation of enterprise networking concepts including **VLAN segmentation, VLSM, multilayer switching, OSPF dynamic routing, HSRP redundancy, DHCP, network services, ACLs, and port security** across a three-building network infrastructure.

---

## 📌 Project Overview

The objective of this project was to design a scalable network infrastructure connecting **three buildings** while providing segmentation, redundancy, dynamic routing, network services, and basic security.

The topology consists of a central router connected to redundant multilayer switches in each building. Access switches provide connectivity to end devices on the different floor networks.

The network was designed to demonstrate concepts commonly used in enterprise network environments.

---

## 🗺️ Network Topology

![Network Topology](screenshots/topology.png)

### Infrastructure

The topology contains:

- 🏢 **3 Buildings**
- 🌐 **1 Central Router**
- 🔀 **6 Multilayer Switches**
- 🔌 Multiple Access Switches
- 💻 Multiple Client Devices
- 🖥️ Server Infrastructure
- 🏷️ Multiple VLANs
- 🔄 Redundant network paths

Each building contains two multilayer switches to provide connectivity and redundancy to the access layer.

---

# 🧠 Network Design

The network uses a hierarchical approach consisting of:

### Core / Routing Layer

A central router connects the three building networks.

Six point-to-point links connect the router to the multilayer switches.

### Distribution Layer

Each building contains **two multilayer switches**.

These switches perform Layer 3 functionality and provide redundant connectivity between the access networks and the central router.

### Access Layer

Access switches connect end devices such as PCs and servers to the network.

VLANs are used to logically separate the different LAN segments.

---

# 📡 IP Addressing & VLSM

The network uses **Variable Length Subnet Masking (VLSM)** to efficiently divide the `192.168.1.0/24` address space according to the requirements of each LAN.

The LAN topology includes both `/27` and `/28` networks.

### LAN Networks

| Network | Prefix | Subnet Mask |
|---|---:|---|
| 192.168.1.0 | /27 | 255.255.255.224 |
| 192.168.1.32 | /27 | 255.255.255.224 |
| 192.168.1.64 | /27 | 255.255.255.224 |
| 192.168.1.96 | /27 | 255.255.255.224 |
| 192.168.1.128 | /28 | 255.255.255.240 |
| 192.168.1.144 | /28 | 255.255.255.240 |
| 192.168.1.160 | /28 | 255.255.255.240 |
| 192.168.1.176 | /28 | 255.255.255.240 |

VLSM allows address space to be allocated according to the number of hosts required by each network instead of assigning the same subnet size everywhere.

---

# 🔗 Point-to-Point Networks

The connections between the central router and the six multilayer switches use **/30 point-to-point networks**.

A `/30` subnet provides two usable IPv4 addresses, making it suitable for traditional point-to-point router links.

| Link Network | Prefix |
|---|---:|
| 10.0.0.0 | /30 |
| 10.0.0.4 | /30 |
| 10.0.0.8 | /30 |
| 10.0.0.12 | /30 |
| 10.0.0.16 | /30 |
| 10.0.0.20 | /30 |

Subnet Mask:

`255.255.255.252`

---

# 🔄 OSPF Dynamic Routing

**Open Shortest Path First (OSPF)** is used to dynamically exchange routing information between the central router and the multilayer switching infrastructure.

Instead of manually defining routes to every remote network, OSPF allows routing devices to dynamically learn available networks.

### OSPF Verification

The following routing table was captured from the central router using:

```text
show ip route
```

![OSPF Routing Table](screenshots/ospf-routing-table.png)

The routing table confirms that the LAN networks are being successfully learned through OSPF.

For example:

```text
O 192.168.1.0/27
  [110/2] via 10.0.0.2, FastEthernet0/0
  [110/2] via 10.0.0.6, Ethernet1/0
```

The `O` indicates an **OSPF-learned route**.

The `[110/2]` value represents:

- **110** → OSPF administrative distance
- **2** → OSPF metric for the route

Several destination networks have two equal-cost next hops, demonstrating redundant routing paths through the multilayer switching infrastructure.

---

# 🏷️ VLAN Segmentation

VLANs are used to divide the physical infrastructure into separate logical networks.

This provides:

- Broadcast-domain separation
- Better network organization
- Improved scalability
- Better traffic control
- Easier network administration

Different LAN segments are assigned their own IP subnets.

### VLAN Verification

The VLAN configuration can be verified using:

```text
show vlan brief
```

Screenshot:

![VLAN Configuration](screenshots/vlan-configuration.png)

---

# 🔀 Inter-VLAN Routing

Because devices located in different VLANs belong to different Layer 3 networks, routing is required for communication between them.

The **multilayer switches** provide Layer 3 functionality and enable communication between the VLANs using switched virtual interfaces (SVIs).

This allows devices in different network segments to communicate while maintaining logical VLAN separation.

---

# 🛡️ HSRP Gateway Redundancy

**Hot Standby Router Protocol (HSRP)** is used to provide first-hop gateway redundancy.

Instead of hosts relying on a single physical multilayer switch as their default gateway, HSRP provides a **virtual gateway address** shared between redundant Layer 3 devices.

If the active gateway becomes unavailable, the standby device can take over the gateway role.

This improves network availability and removes a potential single point of failure at the default gateway.

### HSRP Verification

HSRP can be verified using:

```text
show standby brief
```

Screenshot:

![HSRP Verification](screenshots/hsrp-verification.png)

---

# 📥 DHCP

**Dynamic Host Configuration Protocol (DHCP)** is used to automatically provide network configuration to client devices.

DHCP can provide clients with information such as:

- IP address
- Subnet mask
- Default gateway
- DNS server

This reduces the need to manually configure every client device.

### DHCP Verification

![DHCP Configuration](screenshots/dhcp-configuration.png)

---

# 🖥️ Network Services

The project includes server infrastructure for common network services.

| Service | Purpose |
|---|---|
| DHCP | Automatic IP configuration |
| DNS | Domain name resolution |
| HTTP | Web services |
| FTP | File transfer |
| Email | Email communication |

Servers use static addressing so that network services remain reachable at predictable addresses.

---

# 🔐 Access Control Lists

**Access Control Lists (ACLs)** are used to control which traffic is permitted or denied within the network.

ACLs can be used to restrict communication between selected devices or networks while allowing authorized traffic.

This demonstrates basic Layer 3 traffic filtering and network access control.

### ACL Verification

ACL configuration can be checked using commands such as:

```text
show access-lists
```

Screenshot:

![ACL Configuration](screenshots/acl-configuration.png)

---

# 🔒 Port Security

Port Security is implemented on selected access switch interfaces to improve Layer 2 security.

Port Security can restrict which devices are permitted to connect through a particular switch port based on MAC addresses.

This helps protect the access layer from unauthorized devices.

---

# 🧪 Connectivity & Testing

After configuration, connectivity tests were performed to verify communication across the network.

Testing included:

- Local VLAN connectivity
- Inter-VLAN communication
- Communication between buildings
- OSPF route learning
- DHCP address assignment
- Server connectivity
- ACL behavior
- HSRP redundancy
- End-to-end connectivity

Example verification commands used throughout the project include:

```text
show ip route
show ip ospf neighbor
show vlan brief
show interfaces trunk
show ip interface brief
show standby brief
show access-lists
ping
tracert
```

### Connectivity Test

![Connectivity Test](screenshots/connectivity-test.png)

---

# 🛠️ Technologies & Concepts Used

### Routing & Switching

- Cisco Routing & Switching
- OSPF
- VLANs
- Inter-VLAN Routing
- Multilayer Switching
- Trunking
- VLSM
- IPv4 Subnetting

### High Availability

- HSRP
- Redundant uplinks
- Multiple OSPF paths

### Network Services

- DHCP
- DNS
- HTTP
- FTP
- Email

### Security

- Access Control Lists
- Port Security
- VLAN Segmentation

### Tools

- Cisco Packet Tracer
- Cisco IOS CLI

---

# 📂 Repository Structure

```text
Multi-Building-Enterprise-Network/
│
├── README.md
├── Multi-Building-Enterprise-Network.pkt
│
└── screenshots/
    ├── topology.png
    ├── ospf-routing-table.png
    ├── vlan-configuration.png
    ├── hsrp-verification.png
    ├── acl-configuration.png
    ├── dhcp-configuration.png
    └── connectivity-test.png
```

---

# 📥 Download & Run

To explore the complete network:

1. Download `Multi-Building-Enterprise-Network.pkt`
2. Install **Cisco Packet Tracer**
3. Open the `.pkt` file
4. Inspect the router, multilayer switches, access switches, servers, and client configurations
5. Use Cisco IOS verification commands to inspect the network

Cisco Packet Tracer can be obtained through the Cisco Networking Academy.

---

# 🎯 Skills Demonstrated

This project demonstrates practical experience with:

`Network Design`  
`Cisco IOS`  
`Routing & Switching`  
`OSPF`  
`VLANs`  
`Inter-VLAN Routing`  
`HSRP`  
`VLSM`  
`IPv4 Subnetting`  
`DHCP`  
`DNS`  
`ACLs`  
`Port Security`  
`Multilayer Switching`  
`Network Troubleshooting`

---

# 🚀 Future Improvements

Possible future improvements to the network include:

- SSH instead of Telnet for secure remote management
- EtherChannel
- Spanning Tree optimization
- IPv6 addressing
- NAT/PAT
- WAN/Internet connectivity
- Additional ACL security policies
- Network monitoring
- Syslog
- NTP
- SNMP

---

## 👨‍💻 Author

### Omar Abdelbaky

**Computer & Communication Engineering Student**  
**Aspiring Network Engineer**

[LinkedIn](https://www.linkedin.com/in/omar-abdelbakyy-egy)

---

> This project was created for educational and networking practice purposes using Cisco Packet Tracer.
