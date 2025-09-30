# 📡 CCNP GNS3 LAB – Multi-Domain Network Scenario  

This GNS3 lab demonstrates **advanced CCNP-level networking skills** with:  
- Multi-protocol routing (OSPF, EIGRP, BGP)  
- Route redistribution & path manipulation  
- Spanning-tree design (MSTP, PVST+)  
- BGP attributes & communities  
- Plus beyond CCNP scope: **VPN IPsec** & **MPLS backbone**  

---

## 🗂️ Repository Overview  
This repository documents a complete GNS3 lab project.  
Each section corresponds to a key configuration step, with explanations and configs provided.  

---

## 🖼️ Network Topology  
The following diagram represents the global lab infrastructure:  

![Network Topology](CCNP%20DRAWING%20PROJECT.png)  

---

## 🔹 Lab Sections  

### 1. OSPF / EIGRP Interzone  
- Redistribution between OSPF and EIGRP domains.  
- Higher EIGRP metric configured → OSPF preferred as default path.  

### 2. OSPF Multi-Area Design  
- Areas **0, 10, 20** deployed with backup links **R9 ↔ R8**.  
- Default route originated on **R2** and **R8**, with R2 preferred.  

### 3. BGP Inter-AS Configuration  
- Multiple AS domains: **65100, 65200, 65300**.  
- Routes exchanged between ASes via eBGP sessions.  

### 4. BGP Path Selection Tuning  
- **Local Preference** & **MED** influence routing.  
- Example: AS65200 → prefers R2 (higher LP), backup via R8.  

### 5. BGP Communities & Advanced Attributes  
- Communities define Internet-bound preferences:  
  - Traffic to **AS65200 → R1**  
  - Traffic to **AS65300 → R7**  
- **Weight** used on border routers to refine Cisco path control.  

### 6. LAN Switching – MSTP & PVST+  
- **MSTP** deployed in Spain LAN.  
- **PVST+** for redundancy & per-VLAN spanning-tree.  

### 7. VPN IPsec (France ↔ Canada/US)  
- Site-to-Site tunnels between remote branches.  
- **IKEv2, encryption policies, SLA tracking**.  

### 8. MPLS VPN Backbone  
- MPLS between **Main Branch ↔ Datacenter ↔ Spain LAN**.  
- VRF isolation & PE-CE connectivity simulated.  

---

## 🎯 Skills Highlighted  
✔ Multi-protocol routing (OSPF, EIGRP, BGP)  
✔ Route redistribution & path-control advanced techniques  
✔ LAN switching with MSTP / PVST+  
✔ VPN IPsec configuration  
✔ MPLS VPN introduction  
✔ Network automation with Python & Ansible  

---

## 📌 Next Steps / In Progress  

- **Beyond CCNP Scope**  
  - **MPLS VPNs**: continuing refinement of PE-CE connectivity and VRF isolation.  
  - **VPN IPsec**: extending site-to-site security, testing IKEv2 & SLA failover scenarios.  

- **Automation (Work in Progress)**  
  - Only **basic automation configs** available in Python for now.  
  - See repo 👉 [Python Networking Lab](https://github.com/Mamat078/python-networking-lab)  
  - Planned: expand to **Ansible playbooks** and more advanced automation use-cases.  

- **Configurations Documentation**  
  - A dedicated `/configs/` folder will include:  
    - Step-by-step configs  
    - Verification commands (`show`, `debug`)  
    - Explanations  

---

## 🚀 Future Work  
- **QoS for Real-Time Traffic**  
  - Basic VoIP QoS policies (class-map, policy-map, priority queuing)  
  - Automated deployment via Python/Netmiko & Ansible  

- **VRF-Lite Expansion**  
  - Segmentation of customer/department traffic  
  - Combine with MPLS backbone for multi-tenant design  

- **Automation Pipelines (CI/CD)**  
  - GitHub Actions for linting configs (Black/Ruff for Python)  
  - Automated pushes via Ansible  
  - Testing with **pyATS** / **Nornir**  
