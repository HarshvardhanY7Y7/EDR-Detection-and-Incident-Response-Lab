# T1082 – System Information Discovery

## MITRE ATT&CK

| Field | Value |
|------|------|
| Technique ID | T1082 |
| Technique Name | System Information Discovery |
| ATT&CK Tactic | Discovery |

---

# Objective

The objective of this Atomic Red Team test was to simulate an attacker gathering operating system information from a Windows endpoint.

System information discovery is commonly performed during the discovery phase of an intrusion to understand the target operating system before conducting additional actions.

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

The available Atomic Red Team tests for **T1082** were displayed using:

```powershell
Invoke-AtomicTest T1082 -ShowDetailsBrief
```

This command listed all available Atomic tests associated with the System Information Discovery technique.

---

# Atomic Test Details

The selected Atomic test was examined using:

```powershell
Invoke-AtomicTest T1082 -TestNumbers 35 -ShowDetails
```

The following information was confirmed from the output.

| Field | Value |
|------|------|
| Technique | T1082 – System Information Discovery |
| Atomic Test Number | 35 |
| Atomic Test Name | Check OS version via "ver" command |
| Atomic Test GUID | f6ecb109-df24-4303-8d85-1987dbae6160 |
| Executor | Command Prompt |
| Elevation Required | False |

---

# Attack Command

The Atomic test executes the following Windows command.

```cmd
ver
```

Purpose:

The `ver` command displays the Windows operating system version.

---

# Technique Execution

The Atomic test was executed using:

```powershell
Invoke-AtomicTest T1082 -TestNumbers 35
```

The execution completed successfully and generated endpoint activity that was later investigated within LimaCharlie.

---

# LimaCharlie Investigation

Following execution, the endpoint telemetry was reviewed inside LimaCharlie.

The investigation focused on identifying the generated process and analysing the associated endpoint telemetry.

The following investigation views were examined:

- Timeline
- Event Details

---

# Observed Telemetry

During the investigation the following endpoint information was reviewed:

- Process Creation
- Command Line
- Executable Path
- Parent Process
- Process ID (PID)
- Process Hash
- Timestamp

The event details confirmed execution of the discovery command and provided the associated process metadata.

---

# Investigation Notes

Although the `ver` command is a legitimate Windows utility, operating system discovery is commonly observed during the early stages of attacker activity.

Reviewing endpoint telemetry allows defenders to determine:

- Which process executed the command
- When the activity occurred
- Which parent process launched it
- How the command appeared within the endpoint timeline

---

# Evidence Collected

The following evidence was collected during this investigation:

- Atomic Red Team Technique Enumeration
- Atomic Red Team Test Details
- Atomic Red Team Test Execution
- LimaCharlie Timeline
- LimaCharlie Event Details

---

# MITRE ATT&CK Mapping

| ATT&CK Field | Value |
|--------------|-------|
| Technique ID | T1082 |
| Technique | System Information Discovery |
| ATT&CK Tactic | Discovery |

---

# Key Takeaways

- Simple discovery commands generate observable endpoint telemetry.
- Sysmon records process creation associated with the executed command.
- LimaCharlie provides visibility into process metadata and command-line activity.
- Even legitimate Windows commands should be investigated when executed in suspicious contexts.
