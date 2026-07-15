# Indicators of Compromise (IOC) Reference

## Overview

This document consolidates the Indicators of Compromise (IOCs) and endpoint artefacts observed throughout the EDR Detection and Incident Response Lab.

The IOCs listed below are based on telemetry generated during Atomic Red Team simulations and investigated using LimaCharlie EDR and Sysmon.

> **Note:** These IOCs originate from a controlled lab environment and do not represent malicious activity on a production system. No external Indicators of Compromise have been included.

---

# IOC Categories

The investigations produced several categories of endpoint artefacts.

- Process Creation
- Command-Line Activity
- Executable Paths
- Parent Processes
- File Activity
- PowerShell Activity
- Windows Management Instrumentation (WMI)
- Windows Native Binaries (LOLBins)
- Encoded Commands
- Network / System Discovery Activity
- Data Collection Activity
- Obfuscation Indicators

---

# Process Indicators

The following processes were observed during the project.

| Process | Associated Technique |
|----------|----------------------|
| powershell.exe | T1059.001, T1027, T1005 |
| cmd.exe | T1016, T1082, T1083 |
| rundll32.exe | T1218.015 |
| wmic.exe (attempted) | T1047 |

---

# Command-Line Indicators

Examples of command-line activity observed during the project include:

## PowerShell

```powershell
Invoke-AtomicTest T1059.001 -TestNumbers 17
```

## Encoded PowerShell

```text
powershell.exe -EncodedCommand <Base64 Encoded Command>
```

Observed during: T1027 – Obfuscated/Compressed Files and Information

## System Information Discovery

```cmd
ver
```

Observed during: T1082 – System Information Discovery

## Network Discovery

```cmd
ipconfig /all
netsh interface show interface
arp -a
nbtstat -n
net config
```

Observed during: T1016 – System Network Configuration Discovery

## File and Directory Discovery

```cmd
dir /s C:\
tree /F
```

Observed during: T1083 – File and Directory Discovery

---

# Parent Processes

During investigations, the following parent-child process relationships were analysed:

- PowerShell → Child Process
- cmd.exe → Discovery Commands
- rundll32.exe → Proxy Execution
- Windows Explorer → User Initiated Processes

Parent process analysis provided valuable context for understanding process execution.

---

# File Activity

## File Enumeration

Recursive directory enumeration observed during T1083 using `dir` and `tree /F`.

## Archive Creation

Observed during T1005 – Data from Local System, where files of interest were compressed into a single ZIP archive.

## Temporary Files

Atomic Red Team generated temporary files during several simulations which were later removed by cleanup commands (relevant to T1070 – Indicator Removal).

---

# PowerShell Indicators

PowerShell activity was investigated during multiple ATT&CK techniques.

Examples of evidence collected included:

- Standard PowerShell execution
- Encoded PowerShell commands (`-EncodedCommand`)
- Parent process relationships
- Execution path and command-line parameters

---

# Windows Management Instrumentation (WMI)

During the WMI investigation (T1047), telemetry focused on:

- WMI process execution attempts
- Parent process
- Command-line activity
- Process creation events

Note: the `wmic.exe` execution attempt failed on the Windows 11 lab endpoint, as the utility is deprecated on modern Windows versions — however, the attempted execution still generated reviewable telemetry.

---

# LOLBins Observed

The following legitimate Windows binaries were observed being used during the project.

| Binary | Technique |
|---------|-----------|
| powershell.exe | T1059.001 |
| rundll32.exe | T1218.015 |
| cmd.exe | T1016, T1082, T1083 |
| wmic.exe | T1047 (attempted execution) |

---

# Endpoint Artefacts Reviewed

Throughout the investigations, the following endpoint metadata was reviewed within LimaCharlie whenever available.

- Process Name
- Process ID (PID)
- Parent Process ID (PPID)
- Executable Path
- Command Line
- Process Hash
- Timestamp
- User Context

---

# IOC Investigation Workflow

```text
Atomic Red Team
        │
        ▼
Technique Execution
        │
        ▼
Endpoint Telemetry
        │
        ▼
LimaCharlie Timeline
        │
        ▼
Event Details
        │
        ▼
IOC Identification
        │
        ▼
Investigation
```

---

# Defensive Value

Although the executed Atomic tests were performed in a controlled environment, the resulting telemetry closely resembles activity that defenders may encounter during real-world investigations.

Monitoring these indicators enables analysts to:

- Identify suspicious process execution
- Detect encoded PowerShell commands
- Investigate discovery activity
- Correlate parent-child process relationships
- Trace attacker behaviour through endpoint telemetry

---

# IOC Documentation Strategy

Individual technique documentation contains the specific IOCs associated with that ATT&CK technique. This document serves as a central reference describing the categories of endpoint evidence collected throughout the project.

---

# Scope

This IOC reference is limited to telemetry generated within the controlled Windows 11 laboratory environment. No production systems were involved.

---

# Conclusion

The IOC reference provides a consolidated view of the endpoint artefacts generated during this project.

Rather than relying on a single IOC, investigations combined process information, command-line activity, parent-child relationships, and endpoint telemetry to build context around each simulated ATT&CK technique.
