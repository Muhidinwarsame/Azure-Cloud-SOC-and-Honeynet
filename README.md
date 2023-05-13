# Azure SOC-Real world Cyber Attacks
<a href="https://imgur.com/HcOiyKZ"><img src="https://i.imgur.com/HcOiyKZ.png" title="source: imgur.com" /></a>


## Introduction

I built  a HoneyNet and SOC infrastructure within the Microsoft Azure platform as part of a project. This involved the provisioning of various cloud resources, including virtual machines, flow logs for each VM, a log analytics workspace to collect log data, a storage account, a key vault, network security groups,virtual networks,and a Azure Sentinel (SIEM-Security Information and Event Management).

# Objective

The main objective of this project was to set up purposely vulnerable virtual machines on the Azure infrastructure to attract and investigate cyberattacks.


# Regulations, and Azure Components Deployed



* Azure Virtual Network (VNet)
* Azure Network Security Group (NSG)
* Virtual Machines (2x Windows, 1x Linux)
* Azure Storage Account for Data Storage
* Log Analytics Workspace
* Azure Key Vault for Secure Secrets Management
* Windows Remote Desktop for Remote Access
* Installed SQL Server on the Virtual Machine
* Command Line Interface (CLI) for System Management
* NIST SP 800-61 Revision 2 for Incident Handling Guidance
* Microsoft Defender for Cloud to Protect Cloud Resources
* Microsoft Sentinel for Security Information and Event Management (SIEM)





I intentionally exposed the resources to the internet for a 24-hour period to detect and capture any malicious activity. Subsequently, I implemented a series of security measures to fortify the environment and kept it operational for another 24-hour period. Finally, I analyzed the captured log data and developed a spreadsheet to illustrate the changes in traffic trends following the security hardening of the environment.

Metrics Gathered

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
<a href="https://imgur.com/SC4XH1C"><img src="https://i.imgur.com/SC4XH1C.png" title="source: imgur.com" /></a>


"BEFORE Hardening", all resources were set up to be accessible through the internet. The Virtual Machines had no security restrictions in place, meaning anyone could access them. Similarly, all other resources were deployed with public endpoints that were visible to the internet, so there was no need to use more secure Private Endpoints.

## Attack Maps Before Hardening / Security Controls
# NSG Allowed Inbound Malicious Flows 
* Unsecured Network Security Groups (NSGs) in Azure can have serious consequences, including unauthorized access to resources, data breaches, and loss of sensitive data. Hackers can exploit unsecured NSGs to gain access to vulnerable virtual machines or other resources, which can result in costly downtime, loss of revenue, and reputational damage.


<a href="https://imgur.com/xHVKCrS"><img src="https://i.imgur.com/xHVKCrS.png" title="source: imgur.com" /></a>

* The attack map displayed attempts to gain unauthorized access from external sources, indicating that the deployed resources were targeted in this case, Linux server.

Linux Syslog Auth Failures <a href="https://imgur.com/OfITA2P"><img src="https://i.imgur.com/OfITA2P.png" title="source: imgur.com" /></a>


* The attack map reveals multiple instances of failed RDP and SMB connections, which highlights the ongoing efforts of potential attackers to target these protocols.

Windows RDP/SMB Auth Failures <a href="https://imgur.com/7OIySfa"><img src="https://i.imgur.com/7OIySfa.png" title="source: imgur.com" /></a>

## Metrics Before Hardening / Security Controls

Resources were exposed to insecure environments for 24 hours: start time 2023-04-30 stop Time 2023- 05-02. The following Table shows the metrics captured in 24hrs.


<a href="https://imgur.com/Uqouj4k"><img src="https://i.imgur.com/Uqouj4k.png" title="source: imgur.com" /></a>

# Metrics After Hardening (Security Controls)


Metrics After Hardening (Security Controls)
We measured the same things in our environment for another 24 hours, but this time after we added security controls. Start Tim  2023-05-03T02:22:00 and Stop Time 2023-05-04T02:22:00
The results are shown in the table below.

<a href="https://imgur.com/9KT9RsJ"><img src="https://i.imgur.com/9KT9RsJ.png" title="source: imgur.com" /></a>

# Approach

To enhance the environment's overall security posture, I introduced a range of hardening measures and security controls. These enhancements included:
- Built-in Firewalls: I set up the built-in firewalls on the virtual machines to restrict access and safeguard the resources against unauthorized connections.
- Network Security Groups (NSGs)-to increase security, I strengthened the NSGs by blocking all incoming and outgoing traffic, except for traffic coming from my own public IP address.
- Private Endpoints - to fortify the security of the Azure resources, I swapped the public endpoints with Private Endpoints. This made sure that sensitive resources, like databases and storage accounts, could only be accessed from within the virtual network and not from the public internet.


During the first 24-hour study, I discovered that the lab was at risk of various threats because it could be accessed through the public internet. To address this, I turned on NIST 800-53 r4 in Microsoft Defender's compliance section and worked on meeting the compliance standards for SC.7. I also conducted extra evaluations for SC-7, which deals with boundary protection.

<a href="https://imgur.com/ftoS63r"><img src="https://i.imgur.com/ftoS63r.png" title="source: imgur.com" /></a>


# Microsoft Defender for Cloud

<a href="https://imgur.com/J1FnS3W"><img src="https://i.imgur.com/J1FnS3W.png" title="source: imgur.com" /></a>

# NSG rules

<a href="https://imgur.com/PKeYGeA"><img src="https://i.imgur.com/PKeYGeA.png" title="source: imgur.com" /></a>


# Closed wide insecurity Opens.

<a href="https://imgur.com/T430d4W"><img src="https://i.imgur.com/T430d4W.png" title="source: imgur.com" /></a>

# General Improvement



<a href="https://imgur.com/D41Bdwg"><img src="https://i.imgur.com/D41Bdwg.png" title="source: imgur.com" /></a>



- Linux Brute Force Attempt
- Windows Brute Force Success
- Privilege Escalation
- AAD Brute Force Success.




I also used PowerShell scripts or triggered events manually to simulate targeted attacks. Then, I monitored the results using Log Analytics Workspace and Sentinel Incident Creation.



# Attacks and SImulations



<a href="https://imgur.com/8kRtYmE"><img src="https://i.imgur.com/8kRtYmE.png" title="source: imgur.com" /></a>



Azure Private Link & Firewall for Resources.
Observe Network Watcher Topology for the region and resource group all of your stuff is in.
Observe the Key Vault and Storage Account Private Endpoints are there.Storage account image is not listed here.



<a href="https://imgur.com/6nN1BTC"><img src="https://i.imgur.com/6nN1BTC.png" title="source: imgur.com" /></a>



# Azure Network Watcher Topology.



<a href="https://imgur.com/IaTi9DD"><img src="https://i.imgur.com/IaTi9DD.png" title="source: imgur.com" /></a>


# Incident lifecycle


<a href="https://imgur.com/YTz5YGJ"><img src="https://i.imgur.com/YTz5YGJ.png" title="source: imgur.com" /></a>



NIST 800-61 is a publication that outlines guidelines for computer security incident handling. It provides a structured approach to detecting, analyzing, and responding to security incidents.


In this project, I used Microsoft Azure to set up a honeynet and collect logs from different resources in a Log Analytics workspace. I also utilized Microsoft Sentinel to create attack maps, alerts, and incidents. Over a 48-hour period, I gathered metrics to show the importance of configuring cloud assets with security in mind. By implementing one section of NIST SP 800-53 r4, I significantly reduced the number of security events and incidents.





## Conclusion

NIST 800-61 is a publication that outlines guidelines for computer security incident handling. It provides a structured approach to detecting, analyzing, and responding to security incidents.


In this project, I used Microsoft Azure to set up a honeynet and collect logs from different resources in a Log Analytics workspace. I also utilized Microsoft Sentinel to create attack maps, alerts, and incidents. Over a 48-hour period, I gathered metrics to show the importance of configuring cloud assets with security in mind. By implementing one section of NIST SP 800-53 r4, I significantly reduced the number of security events and incidents.


It's worth mentioning that if the resources in the network were frequently utilized by regular users, it's possible that the implementation of security controls may have resulted in more security events and alerts being generated within the 24-hour timeframe.
