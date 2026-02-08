

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
### Evidence Gallery:

<div align="center">
  ![VMware Network Editor](screenshots/01-vmware-network-editor.png)
  *VMnet1 and VMnet8 Network Modes*
</div>

#### 2. Subnet Settings
<div align="center">
  ![VMnet Subnet Settings](screenshots/02-vmnet-subnet-settings.png)
  *VMnet1 and VMnet8 Subnets*
</div>

#### 3. Kali VM Settings
<div align="center">
  ![Kali VM Configuration](screenshots/03-kali-vm-settings.png)
  *Kali VM with dual network adapters (NAT + Host-Only)*
</div>
### 1.2 IP Address Planning

| Device          | Interface | Network             | IP Address      | Gateway     | Purpose         |
|-----------------|-----------|---------------------|-----------------|-------------|-----------------|
| Kali Linux      | eth0      | VMnet8 (NAT)        | 192.168.32.128  | 192.168.32.2| Internet Access |
| Kali Linux      | eth1      | VMnet1 (Host-Only)  | 192.168.56.128  | N/A         | Attack Traffic  |
| Metasploitable2 | eth0      | VMnet1 (Host-Only)  | 192.168.56.129  | N/A         | Vulnerable Target |


### 1.3 Network Architecture Overview

<div align="center">
  ![Strategic Network Segmentation Diagram](diagrams/Strategic%20Network%20Segmentation.png)
  *Lab network segmentation strategy showing isolated attack surface*
</div>

**Key Components:**
- **VMnet8 (NAT)**: Internet access for Kali
- **VMnet1 (Host-Only)**: Isolated attack network
- **Dual-Homed Kali**: Connects to both segments
- **Isolated Target**: No external connectivity


