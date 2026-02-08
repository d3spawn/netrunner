

# Home Lab

This home lab forms the foundational environment for all practical work in the **netrunner** repository.

The lab focuses on understanding system behavior, network design, and security trade-offs through deliberately constructed and isolated virtual environments.

## Objectives

- Design and maintain isolated lab environments
- Understand system behavior from both offensive and defensive perspectives
- Practice safe enumeration, exploitation, and detection techniques
- Document architectural decisions and technical reasoning clearly

## Lab Design

The home lab supports two complementary perspectives:

- **Offensive lab** — focuses on attacker behavior against intentionally vulnerable systems
- **Defensive lab** — focuses on visibility, logging, monitoring, and analysis

Both perspectives are built on shared assumptions around isolation, scope, and authorization.


### Core Design Principles

- **Isolation First**  
  All lab environments are separated from production networks and personal data.

- **Intentional Connectivity**  
  Every network path, service exposure, and trust relationship is deliberate and documented.

- **Reproducibility**  
  Configurations and assumptions are recorded to allow consistent rebuilding and testing.

- **Progressive Complexity**  
  The lab evolves from basic setups to more complex scenarios as understanding improves.

## Structure
00-home-lab/
├── shared/ # Network topology, assumptions, and scope
├── offensive-lab/ # Attacker-focused environment and workflows
└── defensive-lab/ # Monitoring, logging, and analysis environment


## Getting Started
1. **Begin with** `offensive-lab` for foundational attack simulation
2. **Progress to** `defensive-lab/` for detection and response

## Skills Demonstrated
- Virtualization & Network Segmentation
- Security Architecture Design
- Controlled Testing Methodologies
- Technical Documentation
- Ethical Security Practice

---

*"Building this lab taught me that security begins not with tools, but with boundaries."*


## Scope & Ethics

All activities in this home lab are performed exclusively within:
- Local virtualized environments
- Intentionally vulnerable machines
- Authorized training or challenge platforms

No testing is performed against real-world systems, networks, or data without explicit permission. 
This lab exists solely for education, experimentation, and defensive security learning.

This lab exists solely for security learning, experimentation, and defensive skill development.

---

