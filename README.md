# wazuh-threat-hunting-lab18-insider-threat-investigation

## Overview

This lab simulates a potential insider threat scenario where an employee collects confidential documents, stages them into a separate directory, compresses them into a ZIP archive, and deletes the original files.

The objective is to investigate the generated telemetry using Sysmon and Wazuh, correlate the activities into a single timeline, and determine whether the observed behavior could indicate data staging before exfiltration.

---

# Lab Objectives

- Verify Sysmon and Wazuh services
- Create confidential documents
- Stage files into a separate directory
- Compress files into a ZIP archive
- Delete the original files
- Investigate Process Creation events
- Investigate File Creation events
- Correlate related activities in Wazuh
- Build an insider threat investigation timeline

---

# Lab Environment

## Host Machine

- Windows 11

## SIEM

- Wazuh Manager
- Wazuh Dashboard

## Endpoint Monitoring

- Wazuh Agent
- Sysmon

## Tools

- Windows PowerShell
- Compress-Archive

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Collection | Data from Local System | T1005 |
| Collection | Archive Collected Data | T1560.001 |
| Defense Evasion | File Deletion | T1070.004 |

---

# Attack Scenario

A user performs the following actions:

1. Creates confidential business documents.
2. Copies the documents into a staging folder.
3. Compresses the staged files into a ZIP archive.
4. Deletes the original files.
5. Leaves the archive available for potential exfiltration.

---

# Investigation Workflow

1. Verify monitoring services.
2. Create the working directory.
3. Create confidential documents.
4. Stage files for collection.
5. Create a ZIP archive.
6. Delete the original files.
7. Investigate Sysmon Event ID 1.
8. Investigate Sysmon Event ID 11.
9. Search related events in Wazuh.
10. Build the attack timeline.

---

# Wazuh Queries

## Process Creation

```
data.win.system.eventID:1
```

## File Creation

```
data.win.system.eventID:11
```

---

# Investigation Summary

The investigation identified a sequence of activities commonly associated with insider threat behavior. Multiple confidential files were created, copied into a staging directory, archived into a ZIP file, and the originals were deleted. Wazuh and Sysmon telemetry enabled reconstruction of the complete activity timeline.

---

# Skills Demonstrated

- Threat Hunting
- Insider Threat Investigation
- Process Analysis
- File Activity Analysis
- Timeline Correlation
- Sysmon Investigation
- Wazuh SIEM
- MITRE ATT&CK Mapping

---

# Learning Outcome

This lab demonstrates how security analysts investigate suspicious data collection and staging activities that may precede data exfiltration attempts. Correlating multiple endpoint events provides greater context than analyzing individual alerts in isolation.
