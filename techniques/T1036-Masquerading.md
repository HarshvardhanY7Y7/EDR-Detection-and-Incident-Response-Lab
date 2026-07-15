# T1036 – Masquerading

## MITRE ATT&CK

| Field | Value |
|------|------|
| Technique ID | T1036 |
| Technique Name | Masquerading |
| ATT&CK Tactic | Defense Evasion |

---

# Objective

The objective of this Atomic Red Team test was to simulate masquerading by executing a file that appeared legitimate in order to understand how endpoint telemetry captures this type of activity.

Masquerading is a common defense evasion technique where attackers disguise malicious files or processes as trusted or legitimate software.

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

The available Atomic Red Team tests for **T1036** were displayed using:

```powershell
Invoke-AtomicTest T1036 -ShowDetailsBrief
```

---

# Atomic Test Details

The selected Atomic test was reviewed using:

```powershell
Invoke-AtomicTest T1036 -TestNumbers 1 -ShowDetails
```

The Atomic Red Team output displayed the technique information, executor, attack command, cleanup command, and dependencies.

---

# Technique Execution

The Atomic test was executed using:

```powershell
Invoke-AtomicTest T1036 -TestNumbers 1
```

The execution generated endpoint telemetry that was investigated using LimaCharlie.

---

# LimaCharlie Investigation

Following execution, the endpoint was investigated within LimaCharlie.

The investigation focused on identifying the newly created process and reviewing the telemetry associated with the masquerading activity.

The following investigation views were reviewed:

- Timeline
- Event Details
- Process Information

---

# Observed Telemetry

The following endpoint information was analysed:

- Process Creation
- Executable Path
- Parent Process
- Command Line
- Process Hash
- Timestamp
- User Context

The generated telemetry demonstrated how a masqueraded executable still retains process metadata that can be investigated through an EDR platform.

---

# Investigation Notes

Masquerading attempts to make malicious activity appear legitimate by using deceptive filenames, locations, or executable names.

Although the file may appear benign to a user, endpoint telemetry continues to record:

- Process creation
- Parent-child relationships
- Execution path
- Command-line arguments

These artefacts allow defenders to identify suspicious behaviour despite attempts to disguise the executable.

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
| Technique ID | T1036 |
| Technique | Masquerading |
| ATT&CK Tactic | Defense Evasion |

---

# Key Takeaways

- Masquerading attempts to hide malicious intent by imitating legitimate software.
- Endpoint telemetry still records valuable investigative artefacts.
- Process metadata provides defenders with important context during investigations.
- LimaCharlie successfully captured the process execution generated during the Atomic Red Team simulation.
