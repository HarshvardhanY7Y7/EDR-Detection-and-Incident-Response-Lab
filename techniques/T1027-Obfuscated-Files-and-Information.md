# T1027 – Obfuscated/Compressed Files and Information

## MITRE ATT&CK

| Field | Value |
|------|------|
| Technique ID | T1027 |
| Technique Name | Obfuscated/Compressed Files and Information |
| ATT&CK Tactic | Defense Evasion |

---

# Objective

The objective of this Atomic Red Team test was to simulate the execution of an obfuscated PowerShell command and observe how the activity appears within endpoint telemetry collected by Sysmon and LimaCharlie.

Obfuscation is commonly used by attackers to make malicious commands more difficult to read and analyse while attempting to evade simple detection methods.

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

The available Atomic Red Team tests for **T1027** were displayed using:

```powershell
Invoke-AtomicTest T1027 -ShowDetailsBrief
```

This command listed the available Atomic tests for the Obfuscated/Compressed Files and Information technique.

---

# Atomic Test Details

The selected Atomic test was reviewed using:

```powershell
Invoke-AtomicTest T1027 -TestNumbers 1 -ShowDetails
```

Verified information:

| Field | Value |
|------|------|
| Technique | T1027 – Obfuscated/Compressed Files and Information |
| Atomic Test Number | 1 |

---

# Technique Execution

The Atomic test was executed using:

```powershell
Invoke-AtomicTest T1027 -TestNumbers 1
```

The execution completed successfully and generated endpoint telemetry that was later investigated within LimaCharlie.

---

# LimaCharlie Investigation

Following execution, the endpoint was investigated using LimaCharlie.

The Timeline showed the creation of a **powershell.exe** process responsible for executing an encoded PowerShell command.

The Event Details confirmed the use of the **`-EncodedCommand`** parameter.

Observed command line:

```text
powershell.exe -EncodedCommand <Base64 Encoded PowerShell Command>
```

The investigation also displayed:

- Executable Path
- Parent Process
- Process Hash
- Timestamp
- Hostname

---

# Observed Telemetry

During the investigation the following endpoint information was reviewed:

- Process Creation
- Encoded PowerShell Command
- Command-Line Arguments
- Parent Process
- Executable Path
- Process Hash
- Timestamp

The encoded command was clearly visible within the LimaCharlie Event Details, allowing the activity to be identified during the investigation.

---

# Investigation Notes

This Atomic Red Team test demonstrates how encoded PowerShell commands appear within endpoint telemetry.

Although Base64 encoding itself is not malicious, encoded PowerShell execution is commonly observed during real-world attacks and should always be investigated within the context of surrounding activity.

Reviewing endpoint telemetry allows analysts to determine:

- Which process executed the encoded command
- The complete command line
- Parent-child process relationships
- The execution timeline
- Associated process metadata

---

# Evidence Collected

The following evidence was collected during this investigation:

- Atomic Red Team Technique Enumeration
- Atomic Red Team Technique Execution
- LimaCharlie Timeline
- LimaCharlie Event Details

---

# MITRE ATT&CK Mapping

| ATT&CK Field | Value |
|--------------|-------|
| Technique ID | T1027 |
| Technique | Obfuscated/Compressed Files and Information |
| ATT&CK Tactic | Defense Evasion |

---

# Key Takeaways

- Encoded PowerShell execution generates observable endpoint telemetry.
- LimaCharlie successfully captured the encoded PowerShell command line.
- The **`-EncodedCommand`** parameter is an important indicator for defenders during endpoint investigations.
- Reviewing command-line arguments together with process metadata provides valuable context when analysing obfuscated activity.
