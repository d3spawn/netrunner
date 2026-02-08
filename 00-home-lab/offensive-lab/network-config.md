

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

### Evidence to Capture:
screenshots/01-vmware-network-editor.png
screenshots/02-vmnet-subnet-settings.png


### 1.2 IP Address Planning

| Device          | Interface | Network             | IP Address      | Gateway     | Purpose         |
|-----------------|-----------|---------------------|-----------------|-------------|-----------------|
| Kali Linux      | eth0      | VMnet8 (NAT)        | 192.168.32.128  | 192.168.32.2| Internet Access |
| Kali Linux      | eth1      | VMnet1 (Host-Only)  | 192.168.56.128  | N/A         | Attack Traffic  |
| Metasploitable2 | eth0      | VMnet1 (Host-Only)  | 192.168.56.129  | N/A         | Vulnerable Target |

### 1.3 Image Overview
```text
file from draw.io
```
