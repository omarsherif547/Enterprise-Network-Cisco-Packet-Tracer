# 🌐 Multi-Building Enterprise Network — Cisco Packet Tracer

A multi-building enterprise network designed and configured using **Cisco Packet Tracer**. The project demonstrates practical implementation of enterprise networking concepts across a three-building infrastructure.

## 📌 Project Overview

The network connects **three buildings** through a central router and redundant multilayer switching infrastructure. Access switches provide connectivity to end devices on different LAN segments.

The design demonstrates routing, switching, VLAN segmentation, VLSM subnetting, redundancy, network services, and basic network security.

## 🏗️ Network Architecture

The topology contain:

- **3 Buildings**
- **1 Central Router**
- **6 Multilayer Switches**
- Multiple Layer 2 access switches
- Multiple client devices
- Server infrastructure
- Multiple VLANs and IP subnets
- Redundant network paths

The central router connects to the six multilayer switches using point-to-point links. Each building contains two multilayer switches providing Layer 3 connectivity and redundancy to the access layer.

## 📡 IP Addressing & VLSM

The network uses **Variable Length Subnet Masking (VLSM)** to efficiently divide the `192.168.1.0/24` address space according to LAN requirements.

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

## 🔗 Point-to-Point Networks

The central router connects to the multilayer switches using `/30` point-to-point networks with subnet mask `255.255.255.252`.

| Network | Prefix |
|---|---:|
| 10.0.0.0 | /30 |
| 10.0.0.4 | /30 |
| 10.0.0.8 | /30 |
| 10.0.0.12 | /30 |
| 10.0.0.16 | /30 |
| 10.0.0.20 | /30 |

## 🔄 OSPF Dynamic Routing

**Open Shortest Path First (OSPF)** is used to dynamically exchange routing information between the central router and multilayer switching infrastructure.

The routing table confirms remote LAN networks are learned through OSPF. Several destinations have multiple equal-cost next hops, providing redundant Layer 3 paths.

Example:

```text
O 192.168.1.0/27
  [110/2] via 10.0.0.2, FastEthernet0/0
  [110/2] via 10.0.0.6, Ethernet1/0
```

## 🏷️ VLANs & Inter-VLAN Routing

VLANs divide the physical infrastructure into separate logical broadcast domains. The multilayer switches provide Layer 3 functionality and allow communication between the VLANs using inter-VLAN routing.

This provides better network organization, segmentation, scalability, and traffic control.

## 🛡️ Redundancy

The design uses redundant multilayer switches and network paths to improve network availability. **HSRP** provides first-hop gateway redundancy so end devices do not depend on a single physical Layer 3 gateway.

## 🖥️ Network Services

The project includes server-based network services such as:

| Service | Purpose |
|---|---|
| DHCP | Automatic IP configuration |
| DNS | Domain name resolution |
| HTTP | Web services |
| FTP | File transfer |
| Email | Email communication |

## 🔐 Network Security

The network applies basic security concepts including:

- Access Control Lists (ACLs)
- Port Security
- VLAN segmentation
- Controlled device and service access

## 🧪 Verification & Troubleshooting

Cisco IOS commands used to configure, verify, and troubleshoot the network include:

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

## 🛠️ Technologies & Skills

**Cisco Packet Tracer • Cisco IOS • Network Design • Routing & Switching • OSPF • VLANs • Inter-VLAN Routing • Multilayer Switching • HSRP • VLSM • IPv4 Subnetting • DHCP • DNS • ACLs • Port Security • Network Troubleshooting**

## 📂 Project Files

```text
Enterprise-Network-Cisco-Packet-Tracer/
├── README.md
└── project1.pkt
```

## ▶️ Open the Project

Download **`project1.pkt`** and open it using **Cisco Packet Tracer** to explore the complete topology, device configurations, routing tables, VLAN configuration, services, and connectivity.

## 🚀 Future Improvements

Possible future improvements include SSH for encrypted remote management, EtherChannel, Spanning Tree optimization, IPv6, NAT/PAT, WAN/Internet connectivity, Syslog, NTP, SNMP, and network monitoring.

---

## 👨‍💻 Author

### Omar Sherif

**Computer & Communication Engineering Student**  
**Aspiring Network Engineer**

[LinkedIn](https://www.linkedin.com/in/omar-abdelbakyy-egy)

> This project was created for educational and networking practice purposes using Cisco Packet Tracer.
