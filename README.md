# windows-failed-login-investigation
Beginner SOC Analyst lab investigating Windows failed logon events using PowerShell.
# Windows Failed Login Investigation

## Project Overview

This is a beginner SOC Analyst lab using Windows PowerShell to investigate failed login attempts recorded in the Windows Security Event Log.

## Objective

The goal of this investigation is to identify failed login events, examine their details, and understand what the logs can tell a security analyst.

## Tools Used

* Windows 10 Pro
* Windows PowerShell (Administrator)
* Windows Security Event Log

## Investigation Steps

### 1. Checked the Windows Security Log

Used PowerShell to confirm that the Security Event Log was available and review its configuration.

### 2. Searched for Failed Login Events

Used the following command to search for Event ID 4625:

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} -MaxEvents 10 |
Select-Object TimeCreated, Id, ProviderName, Message |
Format-List
```

### 3. Examined the Event Details

The investigation identified failed logon events with these characteristics:

* **Event ID:** 4625
* **Logon Type:** 2 (interactive logon)
* **Failure Reason:** Unknown user name or bad password
* **Status Code:** 0xC000006D
* **Substatus Code:** 0xC000006A
* **Source Address:** 127.0.0.1 (loopback address)

Personal account and computer names have been omitted for privacy.

## Findings

The reviewed logs contained failed interactive logon attempts. The status codes were consistent with an unsuccessful logon caused by invalid authentication information.

The source address, 127.0.0.1, is the loopback address, which refers to the local computer. The reviewed events alone do not establish whether the attempts were malicious or what caused them.

Further investigation would be needed to determine the cause and assess whether there was any security risk.

## What I Learned

* How to access Windows Security Event Logs using PowerShell.
* How to search for failed logon events using Event ID 4625.
* How to interpret logon types and authentication status codes.
* Why analysts must avoid drawing conclusions without sufficient evidence.
* The importance of protecting personal information when sharing investigation results.

## Project Status

This is my first hands-on Windows log investigation as I continue developing practical cybersecurity and SOC Analyst skills.

## Disclaimer

This project uses Windows Security Event Logs from my own computer for educational purposes.
