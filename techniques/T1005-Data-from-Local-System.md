# T1005 – Data from Local System

## MITRE ATT&CK

| Field | Value |
|------|------|
| Technique ID | T1005 |
| Technique Name | Data from Local System |
| ATT&CK Tactic | Collection |

---

# Objective

The objective of this Atomic Red Team test was to simulate an attacker collecting data from the local Windows system.

Data collection is commonly performed after the discovery phase to identify and gather files that may contain valuable or sensitive information.

---

# Lab Environment

| Component | Value |
|-----------|-------|
| Operating System | Windows 11 |
| Hypervisor | Oracle VirtualBox |
| Endpoint Telemetry | Sysmon |
| EDR Platform | LimaCharlie |
| Attack Simulation | Atomic Red Team |
| Command Shell | Windows PowerShell |

---

# Atomic Test Enumeration

The available Atomic Red Team tests for **T1005** were displayed using:

```powershell
Invoke-AtomicTest T1005 -ShowDetailsBrief
```

Available Atomic Test:

- T1005-1 – Search files of interest and save them to a single zip file (Windows)

---

# Atomic Test Details

The Atomic test was reviewed using:

```powershell
Invoke-AtomicTest T1005 -TestNumbers 1 -ShowDetails
```

Verified information:

| Field | Value |
|------|------|
| Technique | T1005 – Data from Local System |
| Atomic Test Number | 1 |

---

# Technique Execution

The Atomic test was executed using:

```powershell
Invoke-AtomicTest T1005 -TestNumbers 1
```

The execution completed and generated endpoint telemetry that was later investigated within LimaCharlie.

---

# LimaCharlie Investigation

Following execution, the endpoint was investigated using LimaCharlie.

The Timeline view showed PowerShell activity associated with the Atomic Red Team execution.

The Event Details displayed a PowerShell command responsible for creating a ZIP archive containing the collected files.

During the investigation the following endpoint information was reviewed:

- Command Line
- Executable Path
- Parent Process
- Process Hash
- Timestamp
- Hostname

---

# Investigation Notes

This Atomic test simulated local data collection by searching for files of interest and packaging the collected data into a ZIP archive.

From a defender's perspective, archive creation immediately following file enumeration can be a useful indicator of potential collection activity.

Reviewing endpoint telemetry helps identify:

- Archive creation
- File collection behaviour
- PowerShell activity
- Parent-child process relationships
- Execution timeline

---

# Evidence Collected

The following evidence was collected during this investigation:

- Atomic Red Team Technique Enumeration
- Atomic Test Execution
- LimaCharlie Timeline
- LimaCharlie Event Details

---

# MITRE ATT&CK Mapping

| ATT&CK Field | Value |
|--------------|-------|
| Technique ID | T1005 |
| Technique | Data from Local System |
| ATT&CK Tactic | Collection |

---

# Key Takeaways

- File collection activity generates observable endpoint telemetry.
- LimaCharlie successfully captured the PowerShell execution responsible for archive creation.
- Archive creation following file enumeration may indicate collection activity.
- Endpoint telemetry provides valuable context during collection investigations.
