# Offensive Lab Network Validation

## 🎯 Purpose
Verify that the lab network operates as designed with proper isolation and connectivity.

---

## 📊 Test Matrix

| Test ID | Description | Expected | Status | Evidence |
|---------|-------------|----------|--------|----------|
| NET-001 | Kali internet access | Success | ✅ | [![Screenshot](screenshots/net-001.png)](screenshots/net-001.png) |
| NET-002 | Kali → Metasploitable | Success | ✅ | [![Screenshot](screenshots/net-002.png)](screenshots/net-002.png) |
| NET-003 | Metasploitable → Internet | Failure | ✅ | [![Screenshot](screenshots/net-003.png)](screenshots/net-003.png) |
| NET-004 | Host → Metasploitable | Failure | ✅ | [![Screenshot](screenshots/net-004.png)](screenshots/net-004.png) |
| NET-005 | Network isolation scan | 2 lab VMs | ✅ | [![Screenshot](screenshots/net-005.png)](screenshots/net-005.png) |

---

## 🔍 Test Procedures

### NET-001: Kali Internet Connectivity
```bash
ping -c 4 8.8.8.8
curl -I https://google.com
sudo apt update | head -5

# Success Criteria: All commands execute without network errors
```

### Test NET-002: Attack Path Connectivity
```bash
# Execute from Kali terminal
ping -c 4 192.168.56.129
traceroute 192.168.56.129
nmap -Pn 192.168.56.129 --top-ports 10 

# Success Criteria:
# Ping: 0% packet loss
# Nmap: Shows open ports
# Traceroute: Direct connection (1 hop)
```


### Test NET-003: Target Isolation Verification
```bash
# Execute from Metasploitable terminal
ping -c 4 8.8.8.8
curl --max-time 5 http://example.com
# Success Criteria: All commands timeout or fail (100% packet loss)
```

### Test NET-004: Host Machine Isolation
```bash
# Execute from Host OS (Windows/Linux/Mac)
ping 192.168.56.129
traceroute 192.168.56.129
# Success Criteria: No response from Metasploitable IP

```

### fixed isolation issue 
| Screenshot | Name | Description |
|------------|------|-------------|
| [View Image](screenshots/net-004-failure.png) | `net-004-failure.png` | Host pinging Metasploitable (FAIL) |
| [View Image](screenshots/net-004-fix.png) | `net-004-fix.png` | VMware Network Editor with VMnet1 unchecked |
| [View Image](screenshots/net-004-fixed.png) | `net-004-fixed.png` | Host ping timeout (PASS) |

### Test NET-005: Network Segment Purity
```bash
### Test NET-005: Network Segment Purity
**Objective:** Confirm lab VMs are present in each network

# From Kali terminal
# Scan Host-Only network
nmap -sn 192.168.56.0/24

# Scan NAT network
nmap -sn 192.168.32.0/24

# Expected Result:
VMnet1: Kali (192.168.56.128) + Metasploitable (192.168.56.129)
VMnet8: Kali (192.168.32.128) accessible
```

### Results NET-005:

| Network | IP | Device | Status |
|---------|-----|--------|--------|
| **VMnet1** | 192.168.56.1 | VMware adapter | Expected |
| | 192.168.56.128 | Kali | ✅ |
| | 192.168.56.129 | Metasploitable | ✅ |
| | 192.168.56.254 | VMware DHCP | Expected |
| **VMnet8** | 192.168.32.1 | VMware gateway | Expected |
| | 192.168.32.2 | VMware NAT | Expected |
| | 192.168.32.128 | Kali | ✅ |
| | 192.168.32.254 | VMware | Expected |
```

```

## 📈 Results Summary

| Metric | Value |
|--------|-------|
| Test Date | 21-03-2026 |
| Tester | Divyanshu Gautam |
| Environment | Offensive Security Lab v1.0 |
| Tests Performed | 5 |
| Tests Passed | 5 |
| Isolation Verified | ✅ |
| Connectivity Verified | ✅ |
| Security Controls | Effective |
