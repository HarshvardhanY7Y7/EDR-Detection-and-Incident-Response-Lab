# T1083 – File and Directory Discovery

## MITRE ATT&CK

| Field | Value |
|------|------|
| Technique ID | T1083 |
| Technique Name | File and Directory Discovery |
| ATT&CK Tactic | Discovery |

---

# Objective

The objective of this Atomic Red Team test was to simulate an attacker searching the Windows file system to identify files and directories of interest.

File and directory discovery is commonly performed during the discovery phase of an intrusion to locate user data, sensitive files, configuration files, and other information that may be useful during later stages of an attack.

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

The available Atomic Red Team tests for **T1083** were displayed using:

```powershell
Invoke-AtomicTest T1083 -ShowDetailsBrief
```

The available tests included:

- T1083-1 – File and Directory Discovery (cmd.exe)
- T1083-2 – File and Directory Discovery (PowerShell)
- T1083-5 – Simulating MAZE Directory Enumeration
- T1083-6 – Launch DirLister Executable
- T1083-7 – Enumerate VMDKs available on an ESXi Host
- T1083-9 – Recursive Enumerate Files and Directories by PowerShell

---

# Atomic Test Details

The selected Atomic Test was reviewed using:

```powershell
Invoke-AtomicTest T1083 -TestNumbers 1 -ShowDetails
```

The following information was confirmed from the output.

| Field | Value |
|------|------|
| Technique | T1083 – File and Directory Discovery |
| Atomic Test Number | 1 |
| Atomic Test Name | File and Directory Discovery (cmd.exe) |
| Atomic Test GUID | 0e36303b-6762-4500-b003-127743b80ba6 |
| Executor | Command Prompt |
| Elevation Required | False |

---

# Attack Commands

The Atomic test executed the following commands.

```cmd
dir /s c:\ >> %temp%\T1083Test1.txt

dir /s "C:\Documents and Settings" >> %temp%\T1083Test1.txt

dir /s "C:\Program Files\" >> %temp%\T1083Test1.txt

dir "%systemdrive%\Users\*.*" >> %temp%\T1083Test1.txt

dir "%userprofile%\AppData\Roaming\Microsoft\Windows\Recent\*.*" >> %temp%\T1083Test1.txt

dir "%userprofile%\Desktop\*.*" >> %temp%\T1083Test1.txt

tree /F >> %temp%\T1083Test1.txt
```

The collected output was written to:

```text
%temp%\T1083Test1.txt
```

---

# Cleanup Command

The Atomic test removed the generated output file using:

```cmd
del %temp%\T1083Test1.txt
```

---

# Technique Execution

The Atomic test was executed using:

```powershell
Invoke-AtomicTest T1083 -TestNumbers 1
```

The execution completed successfully.

The generated discovery results were written to the temporary file before being removed during the cleanup phase.

---

# LimaCharlie Investigation

Following execution, the endpoint was investigated using LimaCharlie.

The Timeline view showed a new **cmd.exe** process responsible for executing the discovery commands.

The Event Details confirmed the complete command line executed during the Atomic test.

Observed command line included:

```cmd
cmd.exe /c dir /s c:\ >> %temp%\T1083Test1.txt
```

followed by additional directory enumeration commands targeting:

- C:\Documents and Settings
- C:\Program Files
- %systemdrive%\Users
- %userprofile%\Desktop
- Windows Recent folder

The investigation also displayed:

- Executable Path
- Process Hash
- Parent Process
- Timestamp
- Hostname

---

# Investigation Notes

This Atomic test simulates an attacker performing large-scale directory enumeration across the Windows file system.

Although all commands are legitimate Windows utilities, extensive directory enumeration is a common behaviour observed during attacker reconnaissance.

The generated telemetry allows defenders to identify:

- Directory enumeration activity
- Command-line arguments
- Parent-child process relationships
- Output file creation
- Timeline of execution

---

# Evidence Collected

The following evidence was collected during this investigation:

- Atomic Red Team Technique Enumeration
- Atomic Red Team Test Details
- Atomic Red Team Execution
- LimaCharlie Timeline
- LimaCharlie Event Details

---

# MITRE ATT&CK Mapping

| ATT&CK Field | Value |
|--------------|-------|
| Technique ID | T1083 |
| Technique | File and Directory Discovery |
| ATT&CK Tactic | Discovery |

---

# Key Takeaways

- File and directory enumeration generates observable endpoint telemetry.
- Multiple Windows discovery commands were executed through a single **cmd.exe** process.
- LimaCharlie captured the complete command line used during execution.
- Command-line logging provides valuable context when investigating discovery behaviour.
- Directory enumeration can indicate preparation for data collection or further compromise.
