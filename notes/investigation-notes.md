# Investigation Notes

## Incident Summary

A simulated insider threat scenario was performed to demonstrate suspicious file collection and staging behavior on a monitored Windows endpoint.

The objective was to determine whether the observed actions could represent preparation for data exfiltration.

---

# Timeline

## Step 1

Verified Sysmon service.

Status

Running

---

## Step 2

Verified Wazuh Agent service.

Status

Running

---

## Step 3

Created confidential documents.

Observed Files

- Salaries.txt
- Customers.txt
- Revenue.txt

---

## Step 4

Copied files into the staging directory.

Observed Activity

Multiple confidential files were gathered into a single location prior to archiving.

---

## Step 5

Created ZIP archive.

Archive

EmployeeData.zip

Observed Process

PowerShell (Compress-Archive)

MITRE

T1560.001 – Archive Collected Data

---

## Step 6

Deleted original confidential files.

Observed Activity

Original documents removed after archive creation.

MITRE

T1070.004 – File Deletion

---

# Sysmon Investigation

## Event ID 1

Observed

- PowerShell execution
- Compress-Archive command
- File copy operations

Purpose

Confirmed the process responsible for data staging.

---

## Event ID 11

Observed

- Creation of confidential files
- Creation of EmployeeData.zip

Purpose

Confirmed file creation and archive generation.

---

# Wazuh Investigation

Observed

- Process Creation events
- File Creation events

Correlated Activity

Document creation

↓

File staging

↓

ZIP archive creation

↓

Original file deletion

---

# SOC Assessment

The observed behavior is consistent with data staging techniques frequently associated with insider threats or data exfiltration preparation.

Although the actions were performed in a controlled lab environment, the same behavioral pattern should be investigated in production to determine user intent and business justification.

---

# MITRE ATT&CK

Collection

- T1005 – Data from Local System

Collection

- T1560.001 – Archive Collected Data

Defense Evasion

- T1070.004 – File Deletion

---

# Conclusion

The investigation successfully reconstructed the complete sequence of file collection, staging, archiving, and cleanup activities using Sysmon telemetry and Wazuh threat hunting.
