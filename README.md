# AI Security Engineering Troubleshooting Agent

## Overview

A PowerShell-based Security Engineering troubleshooting platform designed to automate DNS, network connectivity, TLS certificate, PKI, proxy, and certificate authority diagnostics.

The tool helps Security Engineers, IAM Engineers, SOC Analysts, and IT professionals quickly identify potential root causes, validate certificate trust relationships, and generate incident-style reports with remediation guidance.

---

## Project Summary

Security Engineering teams frequently investigate issues involving:

* DNS resolution failures
* Application connectivity issues
* TLS certificate trust failures
* Certificate authority validation problems
* SSL inspection issues
* Proxy and Zscaler-related access issues
* VPN connectivity failures
* Internal application access problems

This project automates the initial investigation process and provides a repeatable troubleshooting workflow.

---

## Architecture

> Upload `architecture-diagram.png` to your repository and replace this section with the image.

```text
User Input
    ↓
PowerShell Troubleshooting Agent
    ↓
DNS Validation
Port Connectivity Testing
TLS Certificate Inspection
Root CA Validation
    ↓
Analysis Engine
    ↓
Incident Report Generation
```

---

## Security Operations Workflow

```text
Reported Issue
    ↓
Guided Intake
    ↓
Automated Diagnostics
    ↓
Security Analysis
    ↓
Recommended Remediation
    ↓
Incident Report
```

---

# Features

## DNS Resolution Testing

Validates hostname resolution using PowerShell.

Example:

```powershell
Resolve-DnsName www.google.com
```

Detects:

* DNS outages
* Incorrect hostnames
* Internal DNS issues
* VPN DNS problems

---

## Port Connectivity Testing

Validates network reachability.

Example:

```powershell
Test-NetConnection www.google.com -Port 443
```

Detects:

* Firewall blocks
* Service outages
* Routing issues
* Proxy-related failures

---

## TLS Certificate Inspection

Collects:

* Subject
* Issuer
* Thumbprint
* Expiration Date
* Certificate Validity
* Hostname Mismatch Indicators

Detects:

* Expired certificates
* Trust failures
* Hostname mismatches
* Missing intermediates

---

## Certificate Authority Validation

Reviews trusted certificate stores.

Example:

```powershell
Get-ChildItem Cert:\LocalMachine\Root
```

Detects:

* Missing root CAs
* Missing enterprise certificates
* Trust chain issues

---

## Zscaler Root CA Validation

Checks for trusted Zscaler root certificates.

Example:

```powershell
Get-ChildItem Cert:\LocalMachine\Root |
Where-Object {$_.Subject -like "*Zscaler*"}
```

Supports troubleshooting of:

* SSL inspection issues
* Proxy trust failures
* Missing Zscaler certificates

---

## Automated Incident Reporting

Generates Markdown reports containing:

* Executive Summary
* Diagnostic Results
* Root Cause Analysis
* Recommended Actions
* Security Engineering Notes

---

# Project Structure

```text
ai-security-troubleshooting-agent-powershell/
│
├── Start-TroubleshootingAgent.ps1
├── Run-QuickCheck.ps1
├── README.md
│
├── modules/
│   ├── Diagnostics.psm1
│   ├── Analyzer.psm1
│   └── ReportWriter.psm1
│
├── docs/
│
├── reports/
│
├── screenshots/
│
└── images/
```

---

# Requirements

* Windows 10 or Windows 11
* PowerShell 5.1+
* Internet connectivity
* Administrative permissions (recommended)

---

# Installation

## Clone Repository

```powershell
git clone https://github.com/YOUR-USERNAME/ai-security-troubleshooting-agent-powershell.git
```

Navigate into the folder:

```powershell
cd ai-security-troubleshooting-agent-powershell
```

---

## Configure Execution Policy

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

Verify:

```powershell
Get-ExecutionPolicy -List
```

Expected:

```text
CurrentUser    RemoteSigned
```

---

## Unblock Downloaded Files

```powershell
Get-ChildItem -Recurse | Unblock-File
```

---

# Usage

## Quick Diagnostic Test

Run:

```powershell
.\Run-QuickCheck.ps1 -Target www.google.com -Port 443
```

Example Output:

```text
[1] DNS Check
Status : Success

[2] Port Check
Status : Success

[3] TLS Certificate Check
Status : Success

[4] Zscaler Root Certificate Check
Status : Not Found
```

---

## Guided Troubleshooting Workflow

Run:

```powershell
.\Start-TroubleshootingAgent.ps1
```

Example prompts:

```text
What system are you troubleshooting?
What destination are you trying to reach?
What port should be tested?
What error do you see?
Are you using VPN, proxy, Zscaler, or direct internet?
```

---

# Viewing Reports

Reports are stored in:

```text
.\reports\
```

List reports:

```powershell
dir .\reports
```

View a report:

```powershell
Get-Content .\reports\incident_report_YYYYMMDD_HHMMSS.md
```

Open in Notepad:

```powershell
notepad .\reports\incident_report_YYYYMMDD_HHMMSS.md
```

Open in VS Code:

```powershell
code .\reports\incident_report_YYYYMMDD_HHMMSS.md
```

---

# Example Troubleshooting Scenarios

### DNS Failure

Symptoms:

```text
Host not found
```

Possible Causes:

* DNS outage
* VPN DNS issue
* Internal DNS failure

---

### Port Connectivity Failure

Symptoms:

```text
Connection timeout
```

Possible Causes:

* Firewall block
* Routing issue
* Service outage

---

### Certificate Not Trusted

Symptoms:

```text
Certificate not trusted
```

Possible Causes:

* Missing Root CA
* Missing Intermediate CA
* Expired Certificate
* SSL Inspection Issue

---

### Zscaler SSL Inspection Issue

Symptoms:

```text
Works off-network but fails on corporate network
```

Possible Causes:

* Missing Zscaler Root CA
* SSL Inspection Policy Issue
* Proxy Configuration Issue

---

# Technical Skills Demonstrated

### Security Engineering

* TLS
* PKI
* Certificate Authorities
* Root Cause Analysis

### Networking

* DNS
* TCP/IP
* HTTPS
* Connectivity Testing

### Automation

* PowerShell
* Reporting Automation
* Diagnostic Workflows

### Operations

* Incident Response
* Troubleshooting Methodology
* Technical Documentation

---

# Future Enhancements

Planned improvements:

* Microsoft Entra ID Diagnostics
* Conditional Access Validation
* Microsoft Graph API Integration
* Splunk Integration
* Microsoft Sentinel Integration
* CrowdStrike Integration
* Zscaler API Integration
* AI-Assisted Root Cause Analysis
* PDF Report Generation
---

# Disclaimer

This project is intended for defensive troubleshooting and diagnostic purposes only. Only run against systems you own or are authorized to assess.
