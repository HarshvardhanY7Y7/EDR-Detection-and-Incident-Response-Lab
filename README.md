# 🛡️ EDR Detection & Incident Response Lab

> A hands-on Blue Team project demonstrating endpoint detection, telemetry analysis, threat hunting, and incident investigation using **Windows 11**, **Sysmon**, **LimaCharlie EDR**, and **Atomic Red Team**.

---

## Project Overview

This repository documents the design, implementation, execution, and investigation of a Windows Endpoint Detection and Response (EDR) laboratory.

The objective of the project was to build a monitored Windows endpoint, generate high-quality endpoint telemetry, simulate adversary behaviour using Atomic Red Team, and investigate the resulting activity through LimaCharlie from a SOC analyst's perspective.

Rather than focusing only on attack execution, this project demonstrates how endpoint telemetry can be collected, analysed, and documented throughout an investigation.

---

# Project Objectives

- Build a monitored Windows endpoint.
- Deploy Sysmon to generate detailed endpoint telemetry.
- Integrate the endpoint with LimaCharlie EDR.
- Validate endpoint telemetry collection.
- Simulate ATT&CK techniques using Atomic Red Team.
- Investigate telemetry generated during each simulation.
- Document observations from a defender's perspective.

---

# Lab Architecture

```text
Oracle VirtualBox
        │
        ▼
Windows 11 Virtual Machine
        │
        ▼
Sysmon
        │
        ▼
Windows Event Logs
        │
        ▼
LimaCharlie Sensor
        │
        ▼
LimaCharlie Cloud
        │
 ┌──────┼────────┐
 ▼      ▼        ▼
Threat Hunting
Detection Engineering
Incident Response
```

---

# Technology Stack

| Component | Technology |
|-----------|------------|
| Hypervisor | Oracle VirtualBox |
| Operating System | Windows 11 |
| Endpoint Telemetry | Microsoft Sysinternals Sysmon |
| Sysmon Configuration | SwiftOnSecurity Sysmon Configuration |
| EDR Platform | LimaCharlie |
| Attack Simulation | Atomic Red Team |
| Endpoint Protection | Microsoft Defender |
| Shell | Windows PowerShell |

---

# MITRE ATT&CK Techniques

The following techniques were executed and investigated during this project.

| Technique ID | Technique |
|--------------|-----------|
| T1059.001 | PowerShell |
| T1218.015 | Signed Binary Proxy Execution |
| T1105 | Ingress Tool Transfer |
| T1047 | Windows Management Instrumentation |
| T1036 | Masquerading |
| T1070 | Indicator Removal |
| T1082 | System Information Discovery |
| T1016 | System Network Configuration Discovery |
| T1083 | File and Directory Discovery |
| T1005 | Data from Local System |
| T1027 | Obfuscated / Compressed Files and Information |

---

# Skills Demonstrated

- Endpoint Detection & Response (EDR)
- Windows Endpoint Monitoring
- Sysmon Deployment
- Endpoint Telemetry Analysis
- Threat Hunting
- Incident Investigation
- Process Creation Analysis
- Parent–Child Process Analysis
- Command-Line Investigation
- MITRE ATT&CK Mapping
- Atomic Red Team Attack Simulation
- Technical Documentation

---

# Repository Structure

```text
EDR-Detection-and-Incident-Response-Lab/
│
├── README.md
├── LICENSE
│
├── docs/
│   ├── Lab-Setup.md
│   ├── Lab-Architecture.md
│   ├── MITRE-Mapping.md
│   ├── IOC-Reference.md
│   ├── Detection-Engineering.md
│   └── Lessons-Learned.md
│
├── techniques/
│   ├── T1059.001-PowerShell.md
│   ├── T1218.015-Signed-Binary-Proxy-Execution.md
│   ├── T1105-Ingress-Tool-Transfer.md
│   ├── T1047-Windows-Management-Instrumentation.md
│   ├── T1036-Masquerading.md
│   ├── T1070-Indicator-Removal.md
│   ├── T1082-System-Information-Discovery.md
│   ├── T1016-System-Network-Configuration-Discovery.md
│   ├── T1083-File-and-Directory-Discovery.md
│   ├── T1005-Data-from-Local-System.md
│   └── T1027-Obfuscated-Files-and-Information.md
│
├── diagrams/
└── screenshots/
```

---

# Documentation

This repository contains:

- Lab setup documentation
- Individual ATT&CK technique documentation
- MITRE ATT&CK mapping
- IOC reference
- Detection engineering observations
- Lessons learned

---

# Project Status

| Component | Status |
|-----------|:------:|
| Windows Lab | ✅ |
| Sysmon Deployment | ✅ |
| LimaCharlie Deployment | ✅ |
| Telemetry Validation | ✅ |
| ATT&CK Execution | ✅ |
| Documentation | ✅ |

---

# References

- Microsoft Sysinternals Sysmon
- SwiftOnSecurity Sysmon Configuration
- LimaCharlie
- Atomic Red Team
- MITRE ATT&CK
- Oracle VirtualBox

---

# Disclaimer

This project was performed within an isolated virtual lab environment for educational and defensive cybersecurity purposes. All attack simulations were executed against systems owned and controlled by the author.
