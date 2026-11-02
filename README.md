# Secure Healthcare Network Architecture (Cardiff NHS Clinic)

## Overview
An enterprise network infrastructure and security architecture engineered for a four-floor healthcare facility (Cardiff NHS Clinic) serving 400 staff members, 300 inpatient critical care beds, and up to 600 concurrent peak winter guest users[cite: 62, 64, 67]. Developed for the Networks and Security module (SEC5000) under the Cardiff Metropolitan University curriculum[cite: 58, 59]. Grade Achieved: 65% (Upper Second-Class Honours - 2:1).

## Architecture & System Highlights

### 1. Hierarchical Multi-Tier Infrastructure & Cabling
- **Physical Topology:** High-availability three-tier enterprise design (Core, Distribution, Access) eliminating single points of failure across clinical and emergency wings[cite: 76].
- **Core / Distribution Layer:** Redundant Cisco Catalyst 9500 Layer 3 switches handling multi-gigabit inter-VLAN routing[cite: 67, 76].
- **Edge Layer:** Cisco Catalyst 8300 Series edge routers terminating site-to-site IPsec VPN tunnels to the remote cloud data center[cite: 67, 74].
- **Physical Media:** Category 6a SFTP copper cabling for horizontal runs to prevent electromagnetic interference (EMI) from medical machinery, paired with laser-optimized OM4 multimode fiber (10GBASE-SR) vertical backbone risers[cite: 68, 69, 76].

### 2. Multi-Tenancy VLSM Segmentation & VLANs
Enforces dynamic broadcast domain separation via 802.1Q tags to mitigate lateral cyber threats[cite: 62, 66, 78]:
- **VLAN 10 (`10.0.4.0/24`):** Patients Department desktop workstations (150 hosts)[cite: 64, 65].
- **VLAN 20 (`10.0.5.0/24`):** Emergency Department workstations and mobile clinical tablets (100 hosts)[cite: 64, 65].
- **VLAN 30 (`10.0.6.0/24`):** Clinical laboratory diagnostic and analysis equipment (100 hosts)[cite: 64, 65].
- **VLAN 40 (`10.0.8.0/26`):** Pharmacy inventory terminals and helpdesk systems[cite: 64, 66].
- **VLAN 50 (`10.0.0.0/22`):** Isolated Patient Public Wi-Fi scaled for winter surge capacity (up to 1,022 addresses)[cite: 63, 64, 66].
- **VLAN 60 (`10.0.7.0/24`):** Secure Staff WPA3 enterprise Wi-Fi for clinical roaming tablets[cite: 62, 64, 66].
- **VLAN 70 (`10.0.8.64/26`):** Dedicated, isolated Network Management enclave for router/switch consoles[cite: 63, 64, 66].

### 3. Layered Security Stack & Access Control
- **Perimeter Defense:** Next-Generation Firewall (Cisco Firepower 2100) running integrated Snort IDS/IPS engines for deep packet inspection and ransomware neutralization[cite: 69, 73].
- **Cloud Protection:** Web Application Firewall (WAF) deployed with geofencing and Layer 7 inspection protecting remote database (SQL 1433/3306), web, and application servers against SQLi and XSS[cite: 70, 73, 74].
- **Zero-Trust ACLs:** Interface-level Access Control Lists enforcing strict default-deny policies, blocking guest traffic from scanning internal hospital subnets or directly routing to patient EHR databases[cite: 70, 71, 72].

### 4. GNS3 Simulation & Linux Implementation
- Virtual network slice prototype built and tested in GNS3 using software-defined OpenvSwitch (OVS) and Alpine Linux routers[cite: 77].
- Configured 802.1Q sub-interfaces (`eth0.10`, `eth0.20`) with enabled kernel IPv4 packet forwarding (`sysctl net.ipv4.ip_forward=1`)[cite: 79, 80, 81].
- Validated end-to-end data traversal, port-to-VLAN tag bindings, and ICMP routing across isolated tenant boundaries[cite: 78, 83].

## Repository Contents
- `st20320120 SEC5000 WRIT1.pdf` - Full 27-page engineering report, hardware inventory, and topology diagrams[cite: 58, 59, 84].
- `README.md` - Technical project summary and architectural breakdown.
