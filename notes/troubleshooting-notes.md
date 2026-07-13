# Troubleshooting Notes

## Issue 1

### ZIP archive not created

Cause

The destination archive already existed or one of the source files was locked.

Resolution

Delete the existing archive or rerun:

```powershell
Compress-Archive -Path C:\InsiderLab\Staging\* -DestinationPath C:\InsiderLab\EmployeeData.zip -Force
```

---

## Issue 2

### No Sysmon Event ID 11 in Wazuh

Cause

File Creation events had not yet been indexed or the selected dashboard time range was too narrow.

Resolution

- Set the Wazuh time range to **Last 24 Hours**.
- Refresh the Threat Hunting page.
- Search:

```
data.win.system.eventID:11
```

---

## Issue 3

### PowerShell process not found

Cause

The event was outside the current search window or additional process events pushed it out of recent results.

Resolution

Search:

```
data.win.system.eventID:1
```

Filter for:

- powershell.exe
- Compress-Archive
- Copy-Item

---

## Issue 4

### Deleted files still visible

Cause

PowerShell window was not refreshed or files were still open.

Resolution

Run:

```powershell
Get-ChildItem C:\InsiderLab\Confidential
```

Verify the directory is empty.

---

## Issue 5

### Wazuh events delayed

Cause

Normal synchronization delay between the Wazuh Agent and Manager.

Resolution

- Wait 30–60 seconds.
- Refresh the dashboard.
- Verify the Wazuh Agent service is running.

---

## Issue 6

### Unexpected search results

Cause

Other endpoint activity generated additional Sysmon events.

Resolution

Use more specific searches:

```
EmployeeData.zip
```

```
Compress-Archive
```

```
Salaries.txt
```

```
Customers.txt
```

```
Revenue.txt
```

---

# Lessons Learned

- Correlating process execution with file activity provides valuable context during insider threat investigations.
- ZIP archive creation can indicate legitimate business activity or malicious data staging, depending on the surrounding events.
- File deletion immediately after archiving increases the need for analyst review.
- Behavioral analysis is more effective than relying on a single event when investigating potential insider threats.

---

# Final Status

Lab completed successfully.

Validated:

- Process Creation
- File Creation
- File Staging
- ZIP Archive Creation
- Original File Deletion
- Wazuh Threat Hunting Investigation
- Timeline Reconstruction

The investigation demonstrated how Wazuh and Sysmon can be used together to identify and analyze suspicious data collection and staging activities in a Windows environment.
