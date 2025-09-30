# CCNP-LAB-GNS3
This GNS3 lab demonstrates advanced CCNP-level networking skills with multi-protocol routing (OSPF, EIGRP, BGP), redistribution, spanning-tree design, and BGP path manipulation. It also explores beyond CCNP scope with IPsec VPN and MPLS backbone integration.

CCNP GNS3 LAB – Multi-Domain Network Scenario

This repository documents a complete GNS3 lab project built to validate and showcase CCNP-level networking skills and extend them with VPN IPsec and MPLS.
Each section corresponds to a key configuration step, with explanations and configs provided.

🔹 1. OSPF / EIGRP Interzone

Redistribution between OSPF and EIGRP domains.
Higher EIGRP metric configured to prefer OSPF as the default routing path.

🔹 2. OSPF Multi-Area Design

Areas 0, 10, and 20 deployed with backup links between R9 ↔ R8.
Default route originated on R2 and R8, with R2 using a lower metric to ensure primary path selection.

🔹 3. BGP Inter-AS Configuration

Multiple AS domains (65100, 65200, 65300).
Routes exchanged between ASes through eBGP sessions.

🔹 4. BGP Path Selection Tuning

Implementation of Local Preference and MED to influence routing decisions.
Example: AS65200 traffic prefers R2 as entry point (higher LP), backup via R8.

🔹 5. BGP Communities & Advanced Attributes

Use of communities to define Internet-bound preferences:
Traffic to AS65200 → via R1
Traffic to AS65300 → via R7
Application of Weight on border routers to demonstrate in-depth Cisco path manipulation.

🔹 6. LAN Switching – MSTP & PVST+

MSTP deployed in the Spain LAN.
PVST+ integrated for redundancy and per-VLAN spanning-tree.

🔹 7. VPN IPsec (France ↔ Canada/US)

Site-to-Site IPsec tunnels between remote branches.
IKEv2, encryption policies, and SLA tracking for tunnel stability.

🔹 8. MPLS VPN Backbone

MPLS between Main Branch ↔ Datacenter ↔ Spain LAN.
VRF isolation and PE-CE connectivity simulated.

🔹 9. Automation (Other Repos In progress)

CLI automation examples available in dedicated repos:
Python (Netmiko / NAPALM)
Ansible Playbooks
Check profile for links to automation labs.

🎯 Skills Highlighted

Multi-protocol routing (OSPF, EIGRP, BGP)
Route redistribution & path-control techniques
LAN switching with MSTP / PVST+
VPN IPsec configuration


🚀 Future Work

QoS for Real-Time Traffic
Implement basic VoIP QoS policies (class-map, policy-map, priority queuing).
Validate with simulated traffic flows to ensure low latency and jitter.
Showcase automated deployment of QoS configs using Python/Netmiko and Ansible playbooks.
VRF-Lite Expansion
Segment customer/department traffic via VRF-lite.
Combine with existing MPLS backbone to simulate multi-tenant design.
Automation Pipelines (CI/CD)
GitHub Actions for linting configs (Black/Ruff for Python).
Automated push of configs to lab via Ansible.
Integrate testing with pyATS or Nornir for config validation.
MPLS VPN introduction
Network automation with Python & Ansible
