

## 🏗️ Virtual Network Architecture

### 1.1 Configure VMware Virtual Networks
**Objective**: Create isolated segments for different traffic types

```text
Network Editor Actions:
1. Open VMware → Edit → Virtual Network Editor
2. Verify VMnet8 (NAT) exists with subnet 192.168.32.0/24
3. Verify VMnet1 (Host-Only) exists with subnet 192.168.56.0/24
4. Disable all other VMnets for lab isolation
```

## Network Configuration Evidence

### 1. VMware Virtual Network Editor
![VMware Network Editor](screenshots/01-vmware-network-editor.png)
*Figure 1: Configuring VMnet1 (Host-Only) and VMnet8 (NAT) networks*

### 2. Subnet Settings
![Subnet Configuration](screenshots/02-vmnet-subnet-settings.png)
*Figure 2: 192.168.56.0/24 (lab) and 192.168.32.0/24 (internet) subnets*

### 3. Kali Linux VM Configuration
![Kali VM Settings](screenshots/03-kali-vm-settings.png)
*Figure 3: Kali VM with dual network adapters for segmented testing*
### 1.2 IP Address Planning

| Device          | Interface | Network             | IP Address      | Gateway     | Purpose         |
|-----------------|-----------|---------------------|-----------------|-------------|-----------------|
| Kali Linux      | eth0      | VMnet8 (NAT)        | 192.168.32.128  | 192.168.32.2| Internet Access |
| Kali Linux      | eth1      | VMnet1 (Host-Only)  | 192.168.56.128  | N/A         | Attack Traffic  |
| Metasploitable2 | eth0      | VMnet1 (Host-Only)  | 192.168.56.129  | N/A         | Vulnerable Target |


### 1.3 Network Architecture Overview

  ![Strategic Network Segmentation Diagram](diagrams/Strategic%20Network%20Segmentation.png)

**Key Components:**
- **VMnet8 (NAT)**: Internet access for Kali
- **VMnet1 (Host-Only)**: Isolated attack network
- **Dual-Homed Kali**: Connects to both segments
- **Isolated Target**: No external connectivity
