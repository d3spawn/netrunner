# Offensive Lab Setup Guide

## 📋 Prerequisites
- VMware Workstation 17 Pro (or equivalent)
- 8GB+ RAM recommended
- 50GB+ free disk space
- Administrative access to host system


## 🖥️ Phase 1: Kali Linux Configuration
### 1.1 Virtual Machine Creation
VM Settings:
- Name: kali
- OS: Linux → Debian 11.x 64-bit
- RAM: 4096 MB
- Processors: 2
- Disk: 30 GB (split virtual disk)
- Network Adapter 1: NAT (VMnet8)
- Network Adapter 2: Host-Only (VMnet1)

### 1.2 Installation Process

- Boot from the Kali Linux ISO  
- Select **Graphical Install**

**Installation choices:**
- **Language:** English (United States)
- **Network configuration:**
  - Hostname: `kali`
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
### 1.3 Post-Installation Configuration

After installation, the system was updated and basic networking was verified.

```bash
# Update system packages
sudo apt update && sudo apt full-upgrade -y
```
### Verification
```bash
ip a
ip route
```

### Evidence to Capture
- `screenshots/06-kali-network-config.png`
---

## 🎯 Phase 2: Metasploitable 2 Deployment

### 2.1 Download & Verification

```bash
# Download Metasploitable2 from the official source
wget https://downloads.metasploit.com/data/metasploitable/metasploitable-linux-2.0.0.zip
# OR
curl -O https://downloads.metasploit.com/data/metasploitable/metasploitable-linux-2.0.0.zip

# Verify SHA256 hash
sha256sum metasploitable-linux-2.0.0.zip
# Expected : d97c2f6a3bfb5d5b86c6c95c3d0e24c2b1f6e7a7e8f9c0a1b2c3d4e5f6a7b8c9d
```

### 2.2 Import & Configuration

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

### 2.3 Initial Boot & Verification

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





