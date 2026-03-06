# 🛡️ Secure Corporate Network Design — Tech Zolutions Inc.

A fully implemented, multi-layered secure network infrastructure for a 150-employee software company, built and verified in Cisco Packet Tracer.

---

## 📋 Project Description

This project involves the end-to-end design, configuration, and security hardening of a corporate network for Tech Zolutions Inc. The network supports five departments, a server room, a conference room, and a remote branch office — all segmented, secured, and interconnected.

The work spans three core areas: network design and configuration, zone-based security, and advanced security features including VPN and AAA authentication.

---

## ⚙️ What It Does

| Component | Detail |
|---|---|
| Network Architecture | Cisco three-tier model (Core / Distribution / Access) |
| IP Scheme | 172.16.10.0/24 — subnetted per department |
| VLANs | 7 VLANs across departments, server room, and conference room |
| Routing | OSPF configured on all three routers (Internal, Main, External) |
| Servers | Web, File (FTP), Email (SMTP/POP3), DHCP — all statically assigned |
| Wireless | Per-department access points with DHCP-assigned IPs |
| Firewall | Zone-Policy Firewall (ZPF) — INSIDE and OUTSIDE zones |
| ACLs | Extended ACLs per VLAN enforcing inter-department access rules |
| Remote Branch | External router + site-to-site IPsec VPN (AES-256 / SHA-HMAC) |
| AAA | TACACS+ server — centralised auth on L3 switch and internal router |

---

## 📊 Key Results

| Test | Expected | Actual | **Status** |
|---|---|---|---|
| Intra-VLAN communication (Finance) | Successful ping | Successful ping | **✅ Pass** |
| Inter-VLAN communication (S&M → IT) | Successful ping | Successful ping | **✅ Pass** |
| ZPF: Inside → Outside ping | Successful | Successful | **✅ Pass** |
| ZPF: Outside → Inside telnet (blocked) | Timed out | Timed out | **✅ Pass** |
| ACL: Dev → HR (allowed) | Successful ping | Successful ping | **✅ Pass** |
| ACL: Finance → Dev (blocked) | Host unreachable | Host unreachable | **✅ Pass** |
| ACL: Conference Room → IT (blocked) | Host unreachable | Host unreachable | **✅ Pass** |
| VPN tunnel (Main ↔ Remote) | Tunnel established | Tunnel established | **✅ Pass** |
| AAA: Telnet to L3 switch | Login successful | Login successful | **✅ Pass** |
| AAA: Telnet to Internal Router | Login successful | Login successful | **✅ Pass** |
| ZPF: Inside → Outside telnet (Testcase 2) | Timed out | Successful | **❌ Fail** |
| ZPF: Outside → Inside telnet (Testcase 4) | Timed out | Successful | **❌ Fail** |

---

## 💡 Key Insight

Telnet blocking via ZPF was not fully effective in Packet Tracer — the protocol was not explicitly excluded in the class maps, allowing telnet through despite the intent. In a production environment, explicit `deny` rules for Telnet and other unencrypted protocols should be added to class maps, and SSH should be enforced instead.

---

## ⚠️ Limitations

- Simulated in Cisco Packet Tracer — not tested on physical hardware
- ZPF telnet restriction failed in two test cases; class maps would need updating in a real deployment
- DHCP for the conference room inherited IPs from a prior subnet due to subnetting order
- AAA configuration was applied to the Internal Router and L3 Switch only — not all devices

---

## 🎓 Academic Context

This project was completed as part of a Network Security assignment (Student ID: 5663138). It covers network design, VLAN segmentation, zone-based firewalling, ACL policy, VPN configuration, and centralised authentication.

---

👤 Author

- Rakesh Elamaran
- MSc Cyber Security Engineering – University of Warwick
- Security Engineer | Licensed Penetration Tester | NCSC Certified Graduate

🌐 rakeshelamaran.com

## 📄 Licence

This project is for viewing and educational reference only. No part of this code may be copied, modified, distributed, or used without explicit written permission from the author.
