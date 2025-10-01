# 📡 CCNP GNS3 LAB – Multi-Domain Network Scenario  

This GNS3 lab demonstrates **advanced CCNP-level networking skills** with:  
- Multi-protocol routing (OSPF, EIGRP, BGP)  
- Route redistribution & path manipulation  
- Spanning-tree design (MSTP, PVST+)  
- BGP attributes & communities  
- Plus beyond CCNP scope: **VPN IPsec** & **MPLS backbone**  

## 🗂️ Repository Overview  
This repository documents a complete GNS3 lab project.  
Each section corresponds to a key configuration step, with explanations and configs provided.  

## 🖼️ Network Topology  
The following diagram represents the global lab infrastructure:  

![Network Topology](CCNP%20DRAWING%20PROJECT.png)  

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

BGP communities are used as a **scalable tagging mechanism** to classify routes, then apply policies at border routers.  
This avoids hardcoding policies on individual prefixes and allows consistent enforcement across the network.  

**Example implementation in the lab:**  

- **On R3 (AS65300)** → routes from R1 are tagged:  

```cisco
route-map TAG-DTC-65100 permit 10
 match ip address prefix-list TO-DATACENTER-65100
 set community 65300:65100 additive
```

Communities are then **propagated with `send-community`** to iBGP peers.

- **On R14** → policies match the tagged routes and apply attributes:  

```cisco
ip community-list standard DTC permit 65300:65100
!
route-map TO-DTC-65100 permit 10
 match community DTC
 set local-preference 111
```

#### Why use communities?  
- **Simplifies configuration**:  
  - All “Datacenter-bound” prefixes are tagged `65300:65100`.  
  - Border routers simply match the tag and apply LP/Weight accordingly.  
- **Ensures consistent policy enforcement** across multiple routers and domains.  
- **Provides scalability**: adding new prefixes does not require updating every border router policy, only tagging them once.  

#### Attributes combined with communities  
- **Weight** → Cisco-specific, local to a router; used for fine-tuning on edge routers.  
- **Local Preference** → AS-wide decision; propagated via iBGP and can be extended to other BGP peers.  
- **Communities** → decide which routes receive which attributes, enabling flexible and scalable routing control.  

### 6. LAN Switching – MSTP & PVST+  
- **MSTP** deployed in Spain LAN.  
- **PVST+** for redundancy & per-VLAN spanning-tree.  

### 7. VPN IPsec (France ↔ Canada/US)  
- Site-to-Site tunnels between remote branches.  
- **IKEv2, encryption policies, SLA tracking**.  

### 8. MPLS VPN Backbone  
- MPLS between **Main Branch ↔ Datacenter ↔ Spain LAN**.  
- VRF isolation & PE-CE connectivity simulated.  

## 🎯 Skills Highlighted  
✔ Multi-protocol routing (OSPF, EIGRP, BGP)  
✔ Advanced BGP path control with Local Pref, MED, Weight & Communities  
✔ Scalable routing policies via tagging (ASN:VALUE, additive communities)  
✔ LAN switching with MSTP / PVST+  
✔ VPN IPsec configuration  
✔ MPLS VPN introduction  
✔ Network automation with Python & Ansible  

## 📌 Next Steps / In Progress  
- **Beyond CCNP Scope**  
  - **MPLS VPNs**: continuing refinement of PE-CE connectivity and VRF isolation.  
  - **VPN IPsec**: extending site-to-site security, testing IKEv2 & SLA failover scenarios.  
- **Automation (Work in Progress)**  
  - Only **basic automation configs** available in Python for now.  
  - Planned: expand to **Ansible playbooks** and more advanced automation use-cases.  
- **Configurations Documentation**  
  - A dedicated `/configs/` folder will include:  
    - Step-by-step configs  
    - Verification commands (`show`, `debug`)  
    - Explanations  

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
