

## 🏗️ Virtual Network Architecture

### 1.1 Configure VMware Virtual Networks
**Objective**: Create isolated segments for different traffic types

### ✅ Network Editor Configuration Checklist

- [ ] **Launch Network Editor**
  - Open VMware Workstation
  - Click `Edit` → `Virtual Network Editor`
  - Grant administrator permissions if prompted

- [ ] **Configure VMnet8 (NAT Network)**
  - [ ] Type: NAT
  - [ ] Subnet IP: `192.168.32.0`
  - [ ] Subnet Mask: `255.255.255.0`
  - [ ] Gateway: `192.168.32.2`

- [ ] **Configure VMnet1 (Host-Only Network)**
  - [ ] Type: Host-only
  - [ ] Subnet IP: `192.168.56.0`
  - [ ] Subnet Mask: `255.255.255.0`
  - [ ] DHCP: Disabled

### (optional) if full isolation needed on kali 
- [ ] **Apply Security Hardening**
  - [ ] Disable VMnet0 (Bridged)
  - [ ] Disable all unused VMnets
  - [ ] Click `Apply` to save changes


## Network Configuration Evidence

### 1. VMware Virtual Network Editor

<div align="center">
  
![VMware Network Editor](screenshots/01-vmware-network-editor.png)

*Configuring VMnet1 (Host-Only) and VMnet8 (NAT) networks*
</div>

### 2. Subnet Settings

<div align="center">

![Subnet Configuration](screenshots/02-vmnet-subnet-settings.png)

*192.168.56.0/24 (lab) and 192.168.32.0/24 (internet) subnets*
</div>

### 3. Kali Linux VM Configuration
<div align="center">
  
![Kali VM Settings](screenshots/03-kali-vm-settings.png)

*Kali VM with dual network adapters for segmented testing*
</div>

### 1.2 IP Address Planning

| Device          | Interface | Network             | IP Address      | Gateway     | Purpose         |
|-----------------|-----------|---------------------|-----------------|-------------|-----------------|
| Kali Linux      | eth0      | VMnet8 (NAT)        | 192.168.32.128  | 192.168.32.2| Internet Access |
| Kali Linux      | eth1      | VMnet1 (Host-Only)  | 192.168.56.128  | N/A         | Attack Traffic  |
| Metasploitable2 | eth0      | VMnet1 (Host-Only)  | 192.168.56.129  | N/A         | Vulnerable Target |


### 1.3 Network Architecture Overview

<div align="center">
  
![Strategic Network Segmentation](diagrams/Strategic%20Network%20Segmentation.png)

*Lab network segmentation strategy showing isolated attack surface*
</div>

**Design Features:**
- ✅ Complete isolation from production networks
- ✅ Dual-segment architecture for controlled testing
- ✅ No internet access for vulnerable target
- ✅ Host system protected from lab traffic



## Network Architecture

View interactive diagram: **[network-topology.drawio](diagrams/Strategic-Network-Segmentation.drawio)**

GitHub will automatically show a preview with an "Edit" button that opens in Draw.io!


## 🏗️ Network Architecture

### Interactive Diagram
[![Network Topology Preview](diagrams/Strategic-Network-Segmentation.drawio)](diagrams/Strategic-Network-Segmentation.drawio)

*Click the preview above to view the interactive diagram in GitHub*
