# Lessons Learned

## Overview

This project provided practical experience in building, monitoring, and investigating a Windows endpoint using Sysmon, LimaCharlie, and Atomic Red Team.

Rather than focusing solely on executing ATT&CK techniques, the project emphasized understanding how attacker behaviour appears from a defender's perspective through endpoint telemetry.

---

# Key Technical Lessons

## 1. Endpoint Telemetry is Critical

One of the biggest takeaways from this project was the importance of high-quality endpoint telemetry.

Without Sysmon, Windows provides only limited logging. After deploying Sysmon with the SwiftOnSecurity configuration, significantly more endpoint activity became available for investigation, greatly improving the ability to analyse process execution and attacker behaviour.

---

## 2. Telemetry Is More Valuable Than Alerts

Investigations are driven by endpoint telemetry rather than alerts alone.

Reviewing process execution, command-line arguments, executable paths, timestamps, and parent-child relationships provided significantly more context than simply knowing a technique had executed.

---

## 3. Parent–Child Process Relationships Matter

Nearly every investigation involved identifying the parent process, child process, and execution chain.

Understanding these relationships made it much easier to explain how a technique executed and where the activity originated.

---

## 4. Command-Line Analysis Is Essential

The command line often provided the clearest explanation of what a process was attempting to do.

Across multiple ATT&CK techniques, command-line arguments helped identify PowerShell execution, discovery commands, encoded commands, and file collection activity.

---

## 5. Timeline Correlation Improves Investigations

Viewing activity chronologically inside LimaCharlie helped correlate related events generated during Atomic Red Team executions, rather than analysing isolated events in a vacuum.

---

## 6. Legitimate Windows Utilities Can Be Abused

Many of the ATT&CK techniques relied on trusted Windows binaries rather than custom malware, including:

- powershell.exe
- cmd.exe
- rundll32.exe
- wmic.exe

This reinforced the importance of analysing behaviour rather than trusting a process simply because it is a legitimate Windows executable.

---

## 7. Failed Executions Can Still Be Useful

Not every Atomic Red Team simulation completed successfully. For example, **T1047 – Windows Management Instrumentation** failed because **WMIC** is no longer included by default on modern Windows 11 systems.

Although the attack simulation did not complete successfully, the attempted execution still generated useful endpoint telemetry for investigation — demonstrating that unsuccessful executions can still provide valuable defensive insight.

---

## 8. Controlled Attack Simulation Builds Confidence

Executing ATT&CK techniques inside a dedicated lab environment provided practical experience without introducing unnecessary risk. Atomic Red Team allowed techniques to be executed repeatedly while observing how each appeared inside the EDR platform.

---

# Investigation Lessons

During every investigation, the same methodology proved effective:

1. Execute the Atomic test.
2. Verify execution.
3. Review Timeline.
4. Inspect Event Details.
5. Analyse process metadata.
6. Document findings.

Following a consistent workflow made investigations repeatable and easier to understand.

---

# Practical Skills Developed

Throughout this project, practical experience was gained with:

- Building a Windows security lab
- Configuring Sysmon
- Deploying LimaCharlie EDR
- Validating endpoint telemetry
- Investigating endpoint activity
- Analysing process creation events
- Reviewing command-line activity
- Understanding parent-child process relationships
- Mapping activity to the MITRE ATT&CK framework
- Producing technical investigation documentation

---

# Challenges Encountered

Several challenges were encountered during the project:

### Windows Version Compatibility

Some Atomic Red Team tests relied on Windows components that are deprecated or unavailable on newer Windows versions. The WMI execution test demonstrated how operating system differences can affect attack simulations.

### Understanding Endpoint Telemetry

Initially, interpreting endpoint telemetry within LimaCharlie required time and experimentation. Repeated investigation of Timeline and Event Details improved familiarity with process creation, command-line activity, parent-child relationships, and process metadata.

### Documentation

One of the most time-consuming aspects of the project was documenting every ATT&CK technique using real evidence rather than generic descriptions. Although this required additional effort, it resulted in a much stronger and more realistic portfolio project.

---

# Project Strengths

This project demonstrates practical experience with:

- Endpoint Detection and Response (EDR)
- Windows endpoint monitoring
- Threat hunting fundamentals
- Endpoint telemetry analysis
- SOC investigation workflow
- MITRE ATT&CK mapping
- Technical documentation

---

# Future Improvements

Potential future enhancements include:

- Creating custom LimaCharlie detection rules
- Writing Sigma rules for selected techniques
- Expanding the lab with additional ATT&CK techniques
- Building detection dashboards and investigation playbooks
- Integrating another SIEM platform for comparison
- Simulating multi-stage attack scenarios
- Adding additional Windows endpoints for lateral movement testing

These improvements represent future work and are not included as completed activities within this repository.

---

# Overall Outcome

This project successfully demonstrated how a monitored Windows endpoint can be used to investigate common ATT&CK techniques within a controlled environment.

By combining Sysmon, LimaCharlie, and Atomic Red Team, the project provided practical experience in building an endpoint monitoring environment, executing attacker techniques safely, investigating endpoint telemetry, mapping activity to MITRE ATT&CK, and producing structured incident response documentation.

---

# Conclusion

Building this lab provided practical experience across the complete workflow of a basic endpoint investigation.

Starting from a clean Windows virtual machine, the environment was configured with Sysmon and LimaCharlie, endpoint telemetry was validated, ATT&CK techniques were executed using Atomic Red Team, and the resulting activity was investigated and documented.

The project reinforced the importance of endpoint visibility, structured investigations, and evidence-based documentation when analysing attacker behaviour from a SOC analyst's perspective.
