# Offensive Lab Setup Guide

## 📋 Prerequisites
- VMware Workstation 17 Pro (or equivalent)
- 8GB+ RAM recommended
- 50GB+ free disk space
- Administrative access to host system

## 🏗️ Phase 1: Virtual Network Architecture

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
Device	Interface	Network	IP Address	Gateway	Purpose
Kali Linux	eth0	VMnet8 (NAT)	192.168.32.128	192.168.32.2	Internet Access
Kali Linux	eth1	VMnet1 (Host-Only)	192.168.56.128	N/A	Attack Traffic
Metasploitable2	eth0	VMnet1 (Host-Only)	192.168.56.129	N/A	Vulnerable Target

## 🖥️ Phase 2: Kali Linux Configuration
### 2.1 Virtual Machine Creation
VM Settings:
- Name: kali
- OS: Linux → Debian 11.x 64-bit
- RAM: 4096 MB
- Processors: 2
- Disk: 30 GB (split virtual disk)
- Network Adapter 1: NAT (VMnet8)
- Network Adapter 2: Host-Only (VMnet1)

## 2.2 Installation Process

- Boot from the Kali Linux ISO  
- Select **Graphical Install**

**Installation choices:**
- **Language:** English (United States)
- **Network configuration:**
  - Hostname: `kali-attacker`
  - Domain: `lab.local` (or leave blank)
- **Partitioning:** Use entire disk → All files in one partition
- **User setup:** Create a low-privilege user for daily use
- **Bootloader:** Install GRUB to the master boot record

---

### Evidence to Capture

- `screenshots/03-kali-vm-settings.png`
- `screenshots/04-kali-installation-progress.png`
- `screenshots/05-kali-installation-complete.png`

---
### 2.3 Post-Installation Configuration

After installation, the system was updated and basic networking was verified.

```bash
# Update system packages
sudo apt update && sudo apt full-upgrade -y

# NAT interface (DHCP)
echo -e "auto eth0\niface eth0 inet dhcp" | sudo tee /etc/network/interfaces.d/eth0

# Host-Only interface (lab network)
echo -e "auto eth1\niface eth1 inet static\naddress 192.168.56.128\nnetmask 255.255.255.0" | sudo tee /etc/network/interfaces.d/eth1

# Restart networking
sudo systemctl restart networking
```
### Verification
```bash
ip a
ip route
nmap --version
msfconsole --version
whoami
```

### Evidence to Capture
- `screenshots/06-kali-network-config.png`
- `screenshots/07-kali-tools-verification.png`

---

## 🎯 Phase 3: Metasploitable 2 Deployment

### 3.1 Download & Verification

```bash
# Download Metasploitable2 from the official source
wget https://downloads.metasploit.com/data/metasploitable/metasploitable-linux-2.0.0.zip

# Verify SHA256 hash
sha256sum metasploitable-linux-2.0.0.zip
# Expected : d97c2f6a3bfb5d5b86c6c95c3d0e24c2b1f6e7a7e8f9c0a1b2c3d4e5f6a7b8c9d
```

### 3.2 Import & Configuration

- Extract the ZIP archive to obtain the `.vmx` file

**VMware Import**
- File → Open → Select `Metasploitable.vmx`
- Accept any hardware compatibility warnings if prompted

**Network Configuration**
- Settings → Network Adapter → Host-Only (VMnet1)
- Remove all other network adapters

⚠️ **Critical Security Note**
- NEVER enable NAT or Bridged networking on Metasploitable2
- NEVER expose this VM to any network except the isolated lab network

---

### 3.3 Initial Boot & Verification

**Default credentials**
- Username: `msfadmin`
- Password: `msfadmin`

```bash
# Check network configuration
ifconfig
# Expected: only one interface with IP 192.168.56.129

# Attempt internet connectivity (should fail)
ping -c 2 8.8.8.8
```

### Evidence to Capture
- screenshots/08-metasploitable-import.png
- screenshots/09-metasploitable-network-config.png
- screenshots/10-metasploitable-no-internet.png

---

## ✅ Phase 4: Lab Validation

### 4.1 Connectivity Tests

```bash
# From Kali Linux

# Test 1: Kali internet access via NAT
ping -c 2 8.8.8.8
# Expected: SUCCESS (via eth0 / NAT)

# Test 2: Kali → Metasploitable connectivity
ping -c 4 192.168.56.129
# Expected: SUCCESS (via eth1 / Host-Only)
```
```bash
# From Metasploitable console

# Test 3: Metasploitable internet access
ping -c 2 8.8.8.8
# Expected: FAILURE (no NAT adapter)
```

### 4.2 Network Segmentation Verification

```bash
# Verify routing table on Kali
ip route show
# Expected: default route via 192.168.32.2 (NAT gateway)

# Scan Host-Only network
```bash
nmap -sn 192.168.56.0/24
# Expected: Only two hosts respond
# 192.168.56.128 (Kali)
# 192.168.56.129 (Metasploitable)
```
### Evidence to Capture
- `screenshots/11-kali-ping-success.png`
- `screenshots/12-metasploitable-ping-failure.png`
- `screenshots/13-nmap-scan-results.png`
---








