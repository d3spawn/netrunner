# Offensive Security Lab

## 📌 Overview
A controlled virtual environment designed for practicing offensive security techniques. The lab emphasizes infrastructure design, network isolation, and reproducible setup, ensuring all activity remains contained.

---

## 📊 Specifications

| Component | Specification | Purpose |
|-----------|---------------|---------|
| **Hypervisor** | VMware Workstation 17 Pro | Virtualization & isolation |
| **Attacker** | Kali Linux (4GB RAM, 2 CPU, 40GB) | Primary testing system |
| **Target** | Metasploitable 2 (1GB RAM, 1 CPU, 20GB) | Isolated test system |
| **Network** | NAT + Host-Only | Controlled communication |

---

## 🌐 Network Design

| Network | Type | Subnet | Purpose |
|---------|------|--------|---------|
| VMnet8 | NAT | 192.168.32.0/24 | Optional internet for attacker |
| VMnet1 | Host-Only | 192.168.56.0/24 | Isolated lab communication |

**Key Principles:**
- Target has no internet access
- Lab traffic stays within Host-Only network
- Clear separation between host and lab systems

---

## 📁 Documentation Structure
```
offensive-lab/
├── README.md
├── network-config.md
├── setup-guide.md
├── verification-tests.md
└── screenshots/
```

## 📁 Documentation

| File | Purpose |
|------|---------|
| [`network-config.md`](network-config.md) | Network topology and isolation rules |
| [`setup-guide.md`](setup-guide.md) | Step-by-step VM configuration |
| [`verification-tests.md`](verification-tests.md) | Connectivity and isolation validation |
| [`screenshots/`](screenshots/) | Visual setup evidence |



---

## ✅ Validation Criteria

A correctly configured lab meets:
- Attacker ↔ Target communication via Host-Only
- Target has no external access
- Attacker has optional internet via NAT
- Host cannot access lab network

---

## 🛡️ Security Controls

| Control | Implementation |
|---------|----------------|
| Network Isolation | Host-Only network contains all lab traffic |
| External Access | Only attacker VM uses NAT |
| Target Containment | No external connectivity for target |
| Host Separation | Host virtual adapter disabled for VMnet1 |
| Auditability | Complete documentation with evidence |

---

## ⚠️ Usage Notice

For isolated, educational use only. Do not expose lab VMs to external networks.
