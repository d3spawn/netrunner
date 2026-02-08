# Offensive Lab Network Validation

## 🎯 Purpose
To verify and document that the lab network operates as designed, with proper isolation and connectivity.

## 📊 Test Matrix
| Test ID | Test Description | Expected Result | Pass/Fail | Evidence |
|---------|-----------------|-----------------|-----------|----------|
| NET-001 | Kali internet access | Success | ✅ | `screenshots/net-001.png` |
| NET-002 | Kali → Metasploitable | Success | ✅ | `screenshots/net-002.png` |
| NET-003 | Metasploitable → Internet | Failure | ✅ | `screenshots/net-003.png` |
| NET-004 | Host → Metasploitable | Failure | ✅ | `screenshots/net-004.png` |
| NET-005 | Network isolation scan | 2 hosts only | ✅ | `screenshots/net-005.png` |

## 🔍 Detailed Test Procedures

### Test NET-001: Kali Internet Connectivity
```bash
# Execute from Kali terminal
ping -c 4 8.8.8.8
curl -I https://google.com
sudo apt update | head -5

# Success Criteria: All commands execute without network errors
```

### Test NET-002: Attack Path Connectivity
```bash
# Execute from Kali terminal
ping -c 4 192.168.56.129
nmap -Pn 192.168.56.129
telnet 192.168.56.129 21  # Test FTP service

# Success Criteria:
# Ping: 0% packet loss
# Nmap: Shows at least 5 open ports
# Telnet: FTP banner received
```


### Test NET-003: Target Isolation Verification
```bash
# Execute from Metasploitable terminal
ping -c 4 8.8.8.8
ping -c 4 192.168.32.1
curl --max-time 5 http://example.com
# Success Criteria: All commands timeout or fail (100% packet loss)
```

### Test NET-004: Host Machine Isolation
```bash
# Execute from Host OS (Windows/Linux/Mac)
ping 192.168.56.129
nmap -Pn 192.168.56.129
# Success Criteria: No response from Metasploitable IP
```

### Test NET-005: Network Segment Purity
```bash
# Execute from Kali terminal
# Scan entire Host-Only subnet
nmap -sn 192.168.56.0/24

# Scan entire NAT subnet (from Kali)
nmap -sn 192.168.32.0/24
# Success Criteria:
# VMnet1 (192.168.56.0/24): Exactly 2 hosts respond
# VMnet8 (192.168.32.0/24): Multiple hosts may respond (NAT network)
```


## Result Summary 
{
  "test_date": "08-02-2026",
  "tester": "Divyanshu Gautam",
  "environment": "Offensive Security Lab v1.0",
  "tests_performed": 5,
  "tests_passed": 5,
  "isolation_verified": true,
  "connectivity_verified": true,
  "security_controls_effective": true
}
