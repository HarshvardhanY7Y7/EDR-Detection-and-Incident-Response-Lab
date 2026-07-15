# T1105 – Ingress Tool Transfer

## MITRE ATT&CK

| Field | Value |
|------|------|
| Technique ID | T1105 |
| Technique Name | Ingress Tool Transfer |
| ATT&CK Tactic | Command and Control |

---

# Objective

The objective of this Atomic Red Team test was to simulate an attacker transferring a tool or payload onto a compromised Windows endpoint.

Ingress Tool Transfer is commonly observed after initial access, where attackers download additional tools, scripts, or malware required to continue an intrusion.

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

The available Atomic Red Team tests for **T1105** were displayed using:

```powershell
Invoke-AtomicTest T1105 -ShowDetailsBrief
```

The available Atomic tests included multiple methods for downloading files onto a Windows endpoint.

---

# Atomic Test Details

The selected Atomic test was reviewed using:

```powershell
Invoke-AtomicTest T1105 -TestNumbers 1 -ShowDetails
```

The output displayed:

- Technique information
- Executor
- Attack command
- Cleanup command
- Dependencies

---

# Technique Execution

The Atomic test was executed using:

```powershell
Invoke-AtomicTest T1105 -TestNumbers 1
```

The execution simulated downloading a file to the Windows endpoint and generated endpoint telemetry for investigation.

---

# LimaCharlie Investigation

Following execution, the endpoint was investigated using LimaCharlie.

The investigation focused on identifying the process responsible for downloading the file and reviewing the associated endpoint telemetry.

The following investigation views were examined:

- Timeline
- Event Details
- Process Information

---

# Observed Telemetry

During the investigation the following endpoint information was reviewed:

- Process Creation
- Command Line
- Executable Path
- Parent Process
- Process Hash
- Timestamp
- User Context

The generated telemetry captured the download activity and associated process execution.

---

# Investigation Notes

Ingress Tool Transfer is commonly performed after an attacker gains initial access to a system.

Typical objectives include:

- Downloading additional malware
- Retrieving offensive tooling
- Deploying scripts
- Staging payloads for later execution

Although the downloaded file in this lab was part of an Atomic Red Team simulation, the telemetry generated closely resembles real-world attacker behaviour.

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
| Technique ID | T1105 |
| Technique | Ingress Tool Transfer |
| ATT&CK Tactic | Command and Control |

---

# Key Takeaways

- Download activity generates observable endpoint telemetry.
- Process creation and command-line logging provide valuable context for investigations.
- LimaCharlie successfully captured the process responsible for the simulated transfer.
- File transfer activity should always be analysed in conjunction with the originating process.
