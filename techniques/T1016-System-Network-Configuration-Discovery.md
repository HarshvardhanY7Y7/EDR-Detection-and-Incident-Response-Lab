# T1016 – System Network Configuration Discovery

## MITRE ATT&CK

| Field | Value |
|------|------|
| Technique ID | T1016 |
| Technique Name | System Network Configuration Discovery |
| ATT&CK Tactic | Discovery |

---

# Objective

The objective of this Atomic Red Team test was to simulate an attacker collecting network configuration information from a Windows endpoint.

Network configuration discovery is commonly performed after initial access to understand the victim's network environment, identify interfaces, routing information, and discover potential paths for lateral movement.

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

The available Atomic Red Team tests for **T1016** were displayed using:

```powershell
Invoke-AtomicTest T1016 -ShowDetailsBrief
```

The available tests included:

- T1016-1 – System Network Configuration Discovery on Windows
- T1016-2 – List Windows Firewall Rules
- T1016-4 – System Network Configuration Discovery (TrickBot Style)
- T1016-5 – List Open Egress Ports
- T1016-6 – Adfind – Enumerate Active Directory Subnet Objects
- T1016-7 – Qakbot Recon
- T1016-9 – DNS Server Discovery Using nslookup

---

# Atomic Test Details

The details of the selected Atomic Test were displayed using:

```powershell
Invoke-AtomicTest T1016 -TestNumbers 1 -ShowDetails
```

The following information was confirmed from the output.

| Field | Value |
|------|------|
| Technique | T1016 – System Network Configuration Discovery |
| Atomic Test Number | 1 |
| Atomic Test Name | System Network Configuration Discovery on Windows |
| Atomic Test GUID | 970ab6a1-0157-4f3f-9a73-ec4166754b23 |
| Executor | Command Prompt |
| Elevation Required | False |

---

# Attack Commands

The Atomic test executed the following Windows commands.

```cmd
ipconfig /all
netsh interface show interface
arp -a
nbtstat -n
net config
```

These commands collect information about the network configuration of the Windows endpoint.

---

# Technique Execution

The Atomic test was executed using:

```powershell
Invoke-AtomicTest T1016 -TestNumbers 1
```

The execution completed successfully and generated endpoint telemetry that was investigated using LimaCharlie.

---

# LimaCharlie Investigation

After executing the Atomic test, the endpoint was investigated within LimaCharlie.

The Timeline view showed a new **cmd.exe** process associated with the execution of the discovery commands.

The Event Details panel confirmed the executed command line.

Observed command line:

```cmd
cmd.exe /c ipconfig /all & netsh interface show interface & arp -a & nbtstat -n & net config
```

The investigation also displayed:

- Executable Path
- Process Hash
- Parent Process
- Timestamp
- Hostname

---

# Investigation Notes

The executed commands are legitimate Windows administration utilities used to gather network configuration information.

Although these commands are not inherently malicious, they are commonly observed during the discovery phase of an intrusion.

Reviewing endpoint telemetry allows analysts to determine:

- Which process executed the commands.
- When the commands were executed.
- The complete command line.
- The parent-child process relationship.
- The endpoint where the activity
