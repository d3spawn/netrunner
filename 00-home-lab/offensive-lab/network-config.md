## 🏗️ Virtual Network Architecture

### 1.1 VMware Network Configuration

**Objective:** Create isolated segments for internet access and lab traffic.

#### Configuration Checklist

- [ ] **Launch Network Editor**
  - Open VMware Workstation → `Edit` → `Virtual Network Editor`
  - Grant administrator permissions if prompted

- [ ] **Configure VMnet8 (NAT Network)**
  - Type: NAT
  - Subnet: `192.168.32.0/24`
  - Gateway: `192.168.32.2`

- [ ] **Configure VMnet1 (Host-Only Network)**
  - Type: Host-only
  - Subnet: `192.168.56.0/24`
  - DHCP: Disabled

- [ ] **Apply Security Hardening (Optional)**
  - Disable VMnet0 (Bridged)
  - Disable all unused VMnets
  - Click `Apply` to save changes

---

### Network Configuration Evidence

#### 1. VMware Virtual Network Editor

<div align="center">
  <img src="screenshots/01-vmware-network-editor.png" alt="VMware Network Editor" width="600">
  <br>
  <em>Configuring VMnet1 (Host-Only) and VMnet8 (NAT) networks</em>
</div>

#### 2. Subnet Settings

<div align="center">
  <img src="screenshots/02-vmnet-subnet-settings.png" alt="Subnet Settings" width="600">
  <br>
  <em>192.168.56.0/24 (lab) and 192.168.32.0/24 (internet) subnets</em>
</div>

---

### 1.2 IP Address Planning

| Device | Interface | Network | IP Address | Gateway | Purpose |
|--------|-----------|---------|------------|---------|---------|
| Kali Linux | eth0 | VMnet8 (NAT) | 192.168.32.128 | 192.168.32.2 | Internet Access |
| Kali Linux | eth1 | VMnet1 (Host-Only) | 192.168.56.128 | N/A | Attack Traffic |
| Metasploitable 2 | eth0 | VMnet1 (Host-Only) | 192.168.56.129 | N/A | Vulnerable Target |

---

### 1.3 Network Architecture Overview

<div align="center">
  <a href="https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Strategic%20Network%20Segmentation.drawio&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22Page-1%22%20id%3D%228NOXjuymnfao87ymoqRj%22%3E7Vtbd6I6FP41rnXOQ1mQgOhjtbZ1TWs7o2d6et5QomYViQfipfPrZ0fCLejoWHFNS%2B1DZSduQr5vX4Eabs%2FWN4Ezn94zl3g1pLvrGr6qIWQYugH%2FhOQ1ktg6jgSTgLpyUiro0x9ECnUpXVCXhLmJnDGP03leOGK%2BT0Y8J3OCgK3y08bMy5917kxIQdAfOV5R%2BkRdPo2kuKGn8ltCJ1N5ZozkwNAZvUwCtvDl6Xzmk2hk5sRa5NRw6rhslRHhTg23A8Z49G22bhNP7Gq8YdHvrneMJisOiM8P%2BcHzv3Vy8Y%2F%2B9b8bzhpXw3bjR%2Fj1wipqkYpD%2FhpvTvhC%2BEhcjF7DrTmjPidBZwk%2FEJtugCy5NDHBdcIpceXBlM%2B8eBIP2AtpM48FINlsFG6NqefFohrCJjZN0wK5E84jmMd0LZS1PGdIvEcWUk6ZD%2FIREauAgSUJOAUg75QJQ8Y5m2UmXHp0IgY4m4sTyKNED1twj%2FqwvphgenRhc7EJs%2FVE8F5bLl3NJ3zFghfqT2BCtFdLx1vIvZICOCdZZ%2FZTQnJD2Izw4BWmTDN0MiVFVin1YpFUguvy%2BDW2G3nsSOJPEs0pBeCLZMFvMKJ%2BCCPg4nge3dWUctKfOyMxYwWbdQjiUlTAQoVsRl1XnLq1sbSEXFs2v%2B6JdY0ZLB28QLQakP6%2FEFbWuluMqOvACKAcMtCYjMC3ifjfFSsAhGNNsIWRsmj4KHRxEd26gq6VR9cuC1w70kvcgjf8FdrEdy%2BFjxUQeU4Y0lEe%2B72o7Nuh%2BPID4jmcLvNry2yb9Yt9kWd4FO4ps7N2U7PylqMqCdkiGBH5u6z%2F3KsqiV6xKu4EE8ILqjZQJZd%2BPHrNQ8A60h9mHbXi9IYOIK4FG6%2BYmi9K7Tey8zhublREAR4JPlDgxma51sn8JdKLJpWEZKkmibuvyvHJjco4KIh%2BWJfZuxzAcC%2BKivDtr1jlMJ7x%2FR48aiPjUpORv0%2FpZ7dE0cTYYxs2zkYKu9KkMJpIM%2BoNDSMNdvgamWUDreZLKtBmaUA3Kg10wdgfF8GchWSbtdfwZaQKLtPzYFVIT%2FMtvTMJSBiWzBOkOARkKSG9XhpPDoreauyVxUaINDoSYbxYGCkVVOdK%2FBW4BCP65gMjoNmlsIbMmNWqG3UMY%2FJ8qAtn68dVnZEZGE6ui3w8vjjby%2BQoO8kua%2BvuzJhPuVhSburzw3gcErFbF7qm601l%2BEm5NiG7Faai2SY6WbKCbW13JhvTsJl3V1jNLE9GwzjgVdRdfYG1wPgd9RfrM4ckZOZdDTYTYpwe5YPqug%2BLciEoET7Vd0ekTLJioMaZU9JkTkyL0op%2FJFs7Va7%2BTXyy6t9snrf6RwdVFJUo%2Fxu%2FX%2F5bpTVM0UEFwGdiV83EzrYVtwF4aHEmcHoufhYZn1zcxUUT8pszchG%2F50qjC4mlwzctikvOndHLIS1OY0eL8xg8t7QudGuPaykvxuH3XE%2FE6b1VT3qRZ0OktP4yRu8YkTc2DROL7C%2BCTXV4PjxLayNj%2FAHw%2FPP6MltQNtIwGOOM6xpSIqMF%2FqK0yGhWGutt3ZmtoTPfnQH3feLuzDZymFizVXboWh3n2WGXyY5q306%2BJxzKD49R7gw9gs7cjcONQo5s4RKxrvbTVjnTbpZt2shW%2FD5upsZ%2BFsuu9jMBvQcY7fYGnW%2B9jnhkpP3Q63Xag%2B737uB5J%2FaR2KVLVfTGddw%2B9DePrXQGTw%2Ffvoikst3u9Pt71gHi3FLOlXfaatv6ZJw033Nl9xYuZC4vQxCFKsVCP6o9WiybpZbzONMWojSV5qLyULDVKLGdY36EgvOMRBls7gb9ASwxDTWlKZcnsrip0F1Gs9DjP%2FYuYxGrgqqS7zKa1c5IC2a85YWAoTr5PC8JmIq3x3ZpJly51wRM9dmcRlMz9Wb6sY%2B0Z32LXkNPPsrzP0fbNhymL5JF09P39HDnJw%3D%3D%3C%2Fdiagram%3E%3C%2Fmxfile%3E">
    <img src="diagrams/Strategic%20Network%20Segmentation.png" alt="Network Architecture Diagram" width="600">
  </a>
  <br>
  <em>Click the diagram to open interactive viewer (zoom, layers, edit)</em>
</div>

**Design Features:**
- ✅ Complete isolation from production networks
- ✅ Dual-segment architecture for controlled testing
- ✅ No internet access for vulnerable target
- ✅ Host system protected from lab traffic

---

### 1.4 Network Isolation Fix

**Issue:** Host machine could ping Metasploitable (security risk)

**Fix:** Disabled host virtual adapter for VMnet1 in VMware Network Editor

<div align="center">
  <img src="screenshots/net-004-fix.png" alt="VMware Network Editor Fix" width="600">
  <br>
  <em>Disabling host virtual adapter for VMnet1</em>
</div>

---

### 🎓 Lesson Learned

> *"Isolation isn't automatic—you must verify it. A simple ping test from host to target should always fail in a properly configured security lab."*

**Result:** Host now cannot access lab network; proper isolation achieved
