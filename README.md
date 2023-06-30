
# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/7OWSykQ.png)

## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Opening NSG and Windows Firewall

- Made a Windows and Linux VM. After being made i intenionally configured the firewall and NSG to allow all traffic from all ports. Also went into the VM and disabled the Microsoft Firewalls as well. This created a vulnerable enviorment that attracted Attackers across the world.

## Allow NSG Traffic
![Allow all Traffic to NSG](https://imgur.com/wMp1PF0.jpg)

## Turned off Windows Firewalls
![Turning off Firewall settings](https://imgur.com/9wSKUL7.jpg)


## Utilizing Microsoft Sentinel

- Made KQL Queries to trigger aletrs/events
- BRUTE FORCE ATTEMPTS: FAILURES/SUCCESSES
- AUTHORIZATION ATTEMPS: FAILURES/SUCCESSES

- Set them to run 10 min and to lookup data everyday
![10min](https://imgur.com/WhWDdhT.jpg)

- ## VM on for 24 HOURS 
 
 74 Incidents

![incidents](https://imgur.com/vgGr0V9.jpg)

  ## Logging and Monotring/SOC
 I assigned myself too incident 92 and began to investigate

![Incident92](https://imgur.com/4ltnqdS.jpg)

 This Attacker is coming from Amsterdam also triggered 2 more alerts

![Nland](https://imgur.com/mqfYsvL.jpg)

![Alerts](https://imgur.com/LTzxRaj.jpg)

## Log Analytics

 Further look in log analytics i queried the attackers ip address/failed logons

![attack](https://imgur.com/GWrTjo6.jpg)    

![wiw](https://imgur.com/JeH7so4.jpg)

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

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint


## Attack  Hardening / Security Controls

## Security contols

- Security controls consisted of hardening the NSG by disabling public access to the virtual machines and blob storage account, I created private endpoints for the storage account and virtual machine, an additional network security group was created to protect the subnet, and a NSG rule was generated for these virtual machines to only allow traffic from my own IP address source, and private links were enabled to keep key vault safe to where only Machines in the subnet could access.


- Compiled with NIST SP 800-53  within the compliance section of Microsoft Defender and focused on fulfilling the compliance standards associated with SC.7.*. Additional assessments for SC-7 - Boundary Protection

![Bou](https://imgur.com/f2C271K.jpg)

## Toplogy

![Top](https://imgur.com/w9Cnuz3.jpg)

![ology](https://imgur.com/TRExKdF.jpg)


## Attack Maps Before Hardening / Security Controls

Map shows NSG Attacks

![NSG](https://imgur.com/3F7bWQa.jpg)

Map shows Linux VM Attacks

![Linux Syslog Auth Failures](https://imgur.com/hke4JcR.jpg)

Map shows Windows VM Attacks

![Windows](https://imgur.com/4bqO6mo.jpg)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

Start Time 2023-06-28 17:04:29

Stop Time 2023-06-29  17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19937
| Syslog                   | 6152
| SecurityAlert            | 10
| SecurityIncident         | 230
| AzureNetworkAnalytics_CL | 843
| NSG Inbound Flows        | 1127      



- ## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:

Start Time 2023-06-29 16:37:29

Stop Time	2023-06-30  16:37:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4433
| Syslog                   | 177
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0
| NSG INBOUND FLOW         | 94


RESULTS of HARDENING

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 77%
| Syslog                   | 97%
| SecurityAlert            | 100%
| SecurityIncident         | 100%
| AzureNetworkAnalytics_CL | 100%
| NSG INBOUND FLOW         | 91%





## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

## THANKS FOR VISITING


