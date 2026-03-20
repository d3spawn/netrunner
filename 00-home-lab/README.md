# 🏠 Home Lab

The home lab serves as the foundational environment for all practical work in the **netrunner** repository. It focuses on understanding system behavior, network design, and security trade-offs through deliberately constructed virtual environments.

---

## 📁 Structure


## Structure
```
00-home-lab/
├── offensive-lab/       # Attacker-focused environment and workflows (Kali + Metasploitable)
└── defensive-lab/       # Monitoring, logging, and analysis environment (planned - FLARE-VM, REMnux)
```
---

## 🧠 Skills Demonstrated
- Virtualization & network segmentation  
- Security architecture thinking  
- Controlled testing methodologies  
- Technical documentation  
- Ethical security practice  

> *Building this lab taught me that security begins not with tools, but with boundaries.*

---

## Objectives

- Design and maintain isolated lab environments
- Understand system behavior from both offensive and defensive perspectives
- Practice safe enumeration, exploitation, and detection techniques
- Document architectural decisions and technical reasoning clearly

---

## 🧱 Lab Design Philosophy

The lab is built around two complementary perspectives:

| Perspective | Focus | Status |
|-------------|-------|--------|
| **Offensive Lab** | Attacker behavior on intentionally vulnerable systems | ✅ Complete |
| **Defensive Lab** | Visibility, logging, and analysis (FLARE-VM, REMnux) | ⏳ Planned (hardware constraints) 

Both are built on shared assumptions around **isolation, scope, and authorization**.

### Core Principles

| Principle | Description |
|-----------|-------------|
| 🔒 **Isolation First** | All lab environments separated from production networks |
| 🔗 **Intentional Connectivity** | Every network path exists for a specific reason |
| 🔁 **Reproducibility** | Full documentation for consistent rebuilds |
| 📈 **Progressive Complexity** | Lab evolves as understanding improves |
  
---

## Scope & Ethics

All activities in this home lab are performed exclusively within:
- Local virtualized environments
- Intentionally vulnerable machines
- Authorized training or challenge platforms

> **⚠️ Educational Use Only**  
> This lab is strictly for learning. All testing is contained within isolated virtual environments. No real-world systems, networks, or data are ever targeted without explicit authorization.

---





