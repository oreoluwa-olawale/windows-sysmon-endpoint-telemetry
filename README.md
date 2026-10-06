# Windows Sysmon Endpoint Telemetry Investigation

## Project Overview

This project documents a hands-on Windows endpoint telemetry investigation conducted in a controlled Windows 10 virtual machine as part of my cybersecurity training.

The objective was to configure endpoint process monitoring, generate controlled activity, collect Sysmon telemetry, reconstruct process relationships, and assess activity using an evidence-based approach.

All activity in this project was deliberately generated in a controlled lab environment. No malware was used.

## Lab Environment

- Operating System: Windows 10 Pro
- Virtualization Platform: Oracle VirtualBox
- Virtual Machine: Operation Forge - Windows Lab
- Monitoring Tool: Microsoft Sysmon
- Primary Log Source: Sysmon Operational Event Log
- Relevant Event: Sysmon Event ID 1 - Process Creation
- Windows Security Log: Process Creation Event ID 4688
- User Account: `DESKTOP-5D4PUL7\tkb`

## Objectives

The investigation focused on learning how to:

- Capture Windows process creation telemetry
- Understand Sysmon Event ID 1
- Identify parent and child processes
- Analyze command-line arguments
- Identify the user associated with a process
- Use Process IDs to correlate endpoint evidence
- Distinguish normal administrative activity from potentially suspicious behavior
- Apply evidence-based investigation rather than assuming malicious intent

## Tools Used

### Oracle VirtualBox

Used to create and operate the isolated Windows 10 virtual machine used for the investigation.

### Windows Event Viewer

Used to review Windows Security logs and Sysmon Operational logs.

### Microsoft Sysmon

Sysmon provides detailed Windows endpoint telemetry, including process creation information and command-line data.

### Command Prompt

Used to generate controlled process activity in the lab.

### PowerShell

Used to generate controlled administrative and discovery commands.

### Tasklist

Used to correlate a Sysmon Process ID with a currently running process.

## Telemetry Configuration

Windows process creation auditing was enabled through Local Security Policy.

This allowed Windows Security Event ID 4688 to record process creation.

Sysmon was subsequently installed and configured to provide more detailed process telemetry.

Sysmon Event ID 1 was used to examine:

- Process image
- Command line
- Parent process
- Parent command line
- User
- Process ID

## Controlled Activities

The following activities were deliberately generated in the lab.

### Activity 1: Notepad

Process relationship:

```text
cmd.exe
    |
    └── notepad.exe
cmd.exe
    |
    └── powershell.exe
            |
            └── Get-Date
powershell.exe -NoProfile -Command "Get-Date"

cmd.exe
    |
    └── powershell.exe
            |
            └── Get-Service
powershell.exe -NoProfile -Command "Get-Service"
