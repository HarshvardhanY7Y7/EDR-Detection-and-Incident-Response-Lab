# T1070 – Indicator Removal

## MITRE ATT&CK

| Field | Value |
|------|------|
| Technique ID | T1070 |
| Technique Name | Indicator Removal |
| ATT&CK Tactic | Defense Evasion |

---

# Objective

The objective of this Atomic Red Team test was to simulate an attacker removing forensic artefacts from the Windows endpoint after executing malicious activity.

Indicator Removal is commonly used by attackers to reduce evidence, hinder incident response, and complicate forensic investigations.

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

The available Atomic Red Team tests for **T1070** were displayed using:

```powershell
Invoke-AtomicTest T1070 -ShowDetailsBrief
```

The command listed the available Indicator Removal Atomic tests.

---

# Atomic Test Details

The selected Atomic test was reviewed using:

```powershell
Invoke-AtomicTest T1070 -TestNumbers 1 -ShowDetails
```

The output included:

- Technique information
- Executor
- Attack command
- Cleanup command
- Dependencies

---

# Technique Execution

The Atomic test was executed using:

```powershell
Invoke-AtomicTest T1070 -TestNumbers 1
```

The execution completed successfully and generated endpoint telemetry that was investigated within LimaCharlie.

---

# LimaCharlie Investigation

Following execution, the endpoint was investigated using LimaCharlie.

The investigation focused on identifying file deletion or cleanup activity together with the associated process execution.

The following investigation views were reviewed:

- Timeline
- Event Details
- Process Information

---

# Observed Telemetry

The following endpoint information was analysed:

- Process Creation
- Command Line
- Executable Path
- Parent Process
- Process Hash
- Timestamp
- User Context

The generated telemetry allowed the cleanup activity to be correlated with the originating process.

---

# Investigation Notes

Indicator Removal is frequently performed after malicious activity to reduce evidence left on the endpoint.

Examples include:

- Deleting temporary files
- Removing staged payloads
- Clearing execution artefacts
- Cleaning up attacker-created files

Although attackers attempt to remove evidence, endpoint telemetry often records the cleanup process itself, providing valuable information during an investigation.

---

# Evidence Collected

The following evidence was collected:

- Atomic Red Team Technique Enumeration
- Atomic Red Team Test Details
- Atomic Red Team Execution
- LimaCharlie Timeline
- LimaCharlie Event Details

---

# MITRE ATT&CK Mapping

| ATT&CK Field | Value |
|--------------|-------|
| Technique ID | T1070 |
| Technique | Indicator Removal |
| ATT&CK Tactic | Defense Evasion |

---

# Key Takeaways

- Cleanup activity can itself become valuable forensic evidence.
- Endpoint telemetry records process execution even when files are removed.
- Parent-child process relationships remain valuable during post-execution investigations.
- LimaCharlie successfully captured endpoint activity generated during the Atomic Red Team simulation.
