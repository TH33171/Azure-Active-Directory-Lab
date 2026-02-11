# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/a/OwONO3s.jpg)

## Introduction

Throughout this project, I creted various virtual VMs and built a mini honeynet in Azure to help attract attacks from various sources. I later used a log analytics workspace in order to ingest log sources from different sources.  I then used Microsft sentinel in order to map out the attacks and their sources, triggered different alerts (e.g brute force attacks), and created various incidents. Later on, I measured some security metrices such as Azure Network Analytics_CL (malicious flaws triggered allowed into my honeynet), SecurityAlert (Triggered log analytics alerts), SecurityIncident( Incidents creted by sentintel), Syslog (Linux Events Logs), and SecurityEvent (windows Event Logs), in an insecure evironment over the course of 24 hours. Then, I apllied some security controls in order to harden the system and the environment, before I Finally measured the metrics for and another 24 hours.

The metrics I measured are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

To measure the "BEFORE" metrics, I left all my vms' built-in firewalls and Network Security Groups wide open and deployed them, making sure to expose them to the internet. I also deployed all the other resources with public endpoints ( there was no use for private endpoints).

To measure the "AFTER" metrics, I hardened all the NSGs by blocking ALL traffic except for the my admin workstation. I also used all the other resources' built-in forewalls to protect them as well as private endpoint. 

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2025-03-10 21:03
Stop Time  2025-03-11 21:03

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4358
| Syslog                   | 2345
| SecurityAlert            | 6
| SecurityIncident         | 73
| AzureNetworkAnalytics_CL | 103

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```  -------------------------------------------------------

## Metrics After Hardening / Security Controls

The following table shows the metrics I measured in my environment for another 24 hours, but after I have applied security controls:
Start Time 2025-03-13 21:03
Stop Time	 2025-03-14 21:03

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 110
| Syslog                   | 344
| SecurityAlert            | 1
| SecurityIncident         | 2
| AzureNetworkAnalytics_CL | 0

## Conclusion##

Throughout this projest, I constructed a mini honeynet using Microsift Azure. amd integrated log sources into a log analytics workspace. I also triggered alerts and created incidents based on the ingested logs vi Micrososft Sentinel's deployment. In addition, I measured 5 metrics in the insecure environment for 24 hours before applying security controls. I then later implemented security measures before measuring the metrics again for another 24 hours. The security controls applied have proven to be effective as they seemed to have decreased the number of security events and incidents. 


Had the network been heavily used by normal users, it would have likely caused more security alerts in the 24 hours after the security controls' implementation. .
