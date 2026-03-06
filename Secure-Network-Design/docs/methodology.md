# 🔧 Methodology

## 🗺️ Overview

The network was designed around Cisco's three-tier hierarchical model — core, distribution, and access layers — with security built in at every level. The 172.16.10.0/24 address space was subnetted to allocate the right block size per department, minimising waste while leaving room for growth. Configuration and testing were done entirely in Cisco Packet Tracer, working through three sequential phases: network design and connectivity, zone-based security, and advanced features (VPN + AAA).

---

## 🛠️ Tools & Environment

| Tool / Technology | Role |
|---|---|
| Cisco Packet Tracer | Network simulation environment |
| Cisco IOS (routers + switches) | Device configuration (CLI) |
| Layer 3 Switch (Catalyst) | Inter-VLAN routing via SVI |
| OSPF | Dynamic routing across all three routers |
| VTP (Server/Client mode) | VLAN synchronisation across switches |
| TACACS+ | Centralised AAA authentication |
| IPsec / IKE (AES-256, SHA-HMAC) | Site-to-site VPN tunnel |
| Zone-Policy Firewall (ZPF) | Stateful traffic inspection between zones |
| Extended ACLs | Per-VLAN inter-department access control |

---

## 🏗️ What Was Built and How

**Phase 1 — Network Design & Configuration**  
Seven VLANs were created and assigned to departments, the server room, and the conference room. Each VLAN got a dedicated subnet, default gateway, and DHCP pool. Static IPs were assigned to the four servers (Web, File, Email, DHCP). OSPF was configured on all three routers with verified neighbour relationships and full routing tables. Wireless access points were deployed per department with DHCP addresses.

**Phase 2 — Security and Zones of Trust**  
The network was divided into INSIDE (all internal departments and servers) and OUTSIDE (internet and remote branch) zones. ZPF was implemented on the Main Router using class maps and policy maps to inspect and filter traffic between zones. Extended ACLs were applied per VLAN to enforce cross-department restrictions — for example, Finance cannot reach Development or Sales, and the Conference Room is isolated from operational departments. All devices were secured with passwords; login banners were configured.

**Phase 3 — Advanced Security**  
A site-to-site IPsec VPN was established between the Internal Router (main office) and External Router (remote branch) using IKE Phase 1/2 with AES-256 encryption. The remote branch uses a /28 subnet (172.16.20.0) with DHCP on the External Router. A TACACS+ AAA server (172.16.10.198) was configured and integrated with the L3 Switch and Internal Router for centralised telnet authentication, verified through multiple login test cases.

---

## ✅ Verification Approach

Every configuration step was validated through Packet Tracer test cases — ping tests for connectivity, host-unreachable responses for blocked paths, tunnel verification commands (`show crypto ipsec sa`), and telnet login checks for AAA. Results were logged against expected outcomes, with failures noted and explained.

---
