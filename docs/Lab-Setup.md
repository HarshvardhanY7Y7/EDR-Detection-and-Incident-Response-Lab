# Lab Setup

## Overview

This document describes the complete environment used to build the **EDR Detection and Incident Response Lab**. The objective of this setup was to create a Windows endpoint capable of generating detailed telemetry that could be monitored and investigated using LimaCharlie EDR while executing Atomic Red Team techniques.

---

# Lab Objective

The primary goal of the lab was to:

- Build a monitored Windows endpoint.
- Configure endpoint telemetry using Sysmon.
- Connect the endpoint to LimaCharlie EDR.
- Execute MITRE ATT&CK Atomic Red Team simulations.
- Investigate endpoint telemetry.
- Document the findings in a professional incident response portfolio.

---

# Lab Architecture

```text
Host Machine
      │
      ▼
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
LimaCharlie Cloud Platform
      │
      ▼
Threat Hunting
Detection Engineering
Incident Response
```

---

# Environment Overview

| Component | Description |
|------------|-------------|
| Hypervisor | Oracle VirtualBox |
| Guest Operating System | Windows 11 |
| Endpoint Telemetry | Microsoft Sysinternals Sysmon |
| Sysmon Configuration | SwiftOnSecurity Sysmon Configuration |
| Endpoint Detection & Response | LimaCharlie |
| Attack Simulation | Atomic Red Team |
| Command Shell | Windows PowerShell |

---

# Phase 1 – Virtual Environment

## Oracle VirtualBox

Oracle VirtualBox was used to create an isolated environment for testing and attack simulation.

Reasons for choosing VirtualBox:

- Safe environment for attack simulation
- Isolation from the host operating system
- Snapshot support
- Easy recovery after testing

---

## Windows 11 Virtual Machine

A fresh Windows 11 virtual machine was created and configured as the endpoint used throughout the project.

The VM was configured with:

- Virtual CPU allocation
- Memory allocation
- Virtual hard disk
- Network configuration

---

## Guest Additions

VirtualBox Guest Additions were installed to improve usability.

Enabled features included:

- Automatic screen resizing
- Improved graphics performance
- Shared clipboard
- Enhanced mouse integration

---

# Virtual Machine Snapshots

Snapshots were created throughout the project to provide stable recovery points.

## Snapshot 1

**Purpose:** Fresh Windows installation.

## Snapshot 2

**Purpose:** Windows with Guest Additions installed.

## Snapshot 3

**Purpose:** Fully operational lab with:

- Sysmon installed
- LimaCharlie sensor connected
- Telemetry verified

---

# Phase 2 – Endpoint Telemetry

## Sysmon Installation

Microsoft Sysinternals Sysmon was installed to provide detailed endpoint telemetry beyond the default Windows event logs.

Installation command:

```powershell
.\Sysmon64.exe -accepteula -i .\sysmonconfig.xml
```

---

## Sysmon Configuration

The **SwiftOnSecurity Sysmon configuration** was used.

This configuration improves endpoint visibility by enabling security-relevant events while reducing unnecessary logging noise.

---

## Sysmon Verification

Sysmon installation was verified using:

```powershell
Get-Service Sysmon64
```

The service was confirmed to be running successfully.

---

## Event Viewer Verification

Telemetry was verified using Windows Event Viewer.

Navigation path:

```text
Applications and Services Logs
    └── Microsoft
          └── Windows
                └── Sysmon
                      └── Operational
```

Sysmon events were successfully generated, confirming that endpoint telemetry was functioning correctly.

---

# Phase 3 – LimaCharlie EDR

## Organization Creation

A LimaCharlie organization was created to manage the monitored endpoint.

---

## Installation Key

A Windows installation key was created for sensor deployment.

Purpose:

- Authorize endpoint registration
- Connect the Windows VM to LimaCharlie

---

## Sensor Installation

The LimaCharlie Windows sensor was installed on the virtual machine.

Once installed, the sensor securely transmitted endpoint telemetry to the LimaCharlie cloud platform.

---

## Sensor Verification

The sensor was verified within the LimaCharlie console.

Verification confirmed:

- Sensor online
- Endpoint connected
- Agent healthy

---

## Live Telemetry Verification

After the sensor connected successfully, live endpoint telemetry was observed within LimaCharlie.

Events included:

- NEW_PROCESS
- TERMINATE_PROCESS
- DNS_REQUEST
- NETWORK_CONNECTIONS

This confirmed successful communication between the Windows endpoint and LimaCharlie.

---

## Process Monitoring Verification

Process monitoring was validated by launching **Notepad.exe**.

LimaCharlie successfully captured:

- Process Name
- Process ID (PID)
- Parent Process ID (PPID)
- Executable Path
- Command Line
- User Context

This confirmed that endpoint process telemetry was functioning correctly before attack simulation began.

---

# Attack Simulation Framework

After validating endpoint telemetry, the lab was prepared for attack simulation using **Atomic Red Team**.

Atomic Red Team was used to execute MITRE ATT&CK techniques covering:

- Execution
- Discovery
- Collection
- Defense Evasion
- Command and Control

Each Atomic test generated endpoint telemetry that was investigated using LimaCharlie throughout this project.

---

# Final Lab State

Before beginning ATT&CK simulations, the environment consisted of:

- Oracle VirtualBox
- Windows 11 Virtual Machine
- Sysmon
- SwiftOnSecurity Sysmon Configuration
- LimaCharlie Windows Sensor
- Atomic Red Team
- Windows PowerShell

This configuration provided a fully functional endpoint detection and incident response lab capable of generating and investigating endpoint telemetry across multiple MITRE ATT&CK techniques.

---

# Outcome

At the conclusion of the lab setup:

- Windows 11 endpoint deployed
- Sysmon installed and verified
- SwiftOnSecurity configuration applied
- LimaCharlie sensor enrolled
- Endpoint telemetry validated
- Live process monitoring confirmed
- Stable virtual machine baseline created

The environment was then ready for Atomic Red Team attack simulations and subsequent endpoint investigations documented throughout this repository.
