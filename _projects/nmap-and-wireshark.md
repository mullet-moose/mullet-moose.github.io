---
layout: project
title: 'Nmap and Wireshark'
caption: Identifying anomalies and vulnerabilities with Nmap and Wireshark.
description: >
  This is a project for my *Emerging Technologies in Cybersecurity* course at WGU.
date: '2023-09-11'
image: 
  path: /assets/img/projects/c844t1/cover.jpeg
accent_image: 
  background: url('/assets/img/projects/c844t1/cover.jpeg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
sitemap: false
---

In this *Emerging Technologies in Cybersecurity* project we were tasked with identifying anomalies and vulnerabilities using Nmap and Wireshark.  We then had to discuss their associated implications and recommend solutions.

* toc
{:toc}

### Network Topology

<img src="/assets/img/projects/c844t1/s1.png">

<img src="/assets/img/projects/c844t1/s2.png">

NMAP scan was run using the Zenmap GUI. The target domain was specified as 10.168.27.0/24. A star topology was identified as shown in Screenshot 2. The following lists the 6 hosts and their corresponding IP addresses, operating systems, and open ports:

Host: 10.168.27.1:
  - Operating System: Unknown
  - Open Ports: 0
  
Host: 10.168.27.10:
  - Operating System: Microsoft Windows Server 2012 or Windows Server 2012 R2
  - Open Ports: 8
  
Host: 10.168.27.14:
  - Operating System: Linux 2.6.32
  - Open Ports: 1
  
Host: 10.168.27.15:
  - Operating System: Microsoft Windows Server 2008 R2 or Windows 8.1
  - Open Ports: 10
  
Host: 10.168.27.20:
  - Operating System: Linux 2.6.32
  - Open Ports: 1
  
Host: 10.168.27.132:
  - Operating System: Linux 2.6.32
  - Open Ports: 1
  
### Vulnerabilties and Implications

<img src="/assets/img/projects/c844t1/s3.png">

The first vulnerability I discovered is regarding the multiple hosts running Linux 2.6.32. There is a known vulnerability in this version of the Linux kernel, specifically the Marvell WiFi chip driver, that allows a heap-based buffer overflow attack. A remote attacker could cause a denial of service or execute arbitrary code when the Ibs_ibss_join_existing function is called after a station connects to an access point (CVE-2019-14896). The implications of this vulnerability would be the lack of availability to the network and its resources because of a denial or service attack, as well as the ability for a remote hacker to execute malware through arbitrary code.

<img src="/assets/img/projects/c844t1/s4.png">

Another vulnerability that I discovered was on host 10.168.27.15 relating to Microsoft IIS httpd 8.5. This is an IIS security feature bypass vulnerability that allows remote attackers to bypass rule sets with an HTTP request, because IIS 8.5 doesn’t correctly process allow and deny rules for wildcard domains within the restrictions list (CVE-2014-4078, 2014). An implication would be that an attacker from a denied domain could access websites that were believed to be restricted by the administrator (Microsoft Security Bulletin MS14-076, 2014).

<img src="/assets/img/projects/c844t1/s5.png">

The last vulnerability that I discovered relates to the MSRPC service running on hosts 10.168.27.10 and 10.168.27.15.On both Windows Server 2008 and Windows Server 2012, RPC channels are not correctly established via the LSADand SAM protocol implementation. An implication would be that a man-in-the-middle attacker could exploit this vulnerability to impersonate users and perform protocol-downgrade attacks by altering the client-server data stream (CVE-2016-0128).

### Wireshark Anomalies

<img src="/assets/img/projects/c844t1/s6.png">

The first anomaly I noticed was relating to the SMB protocol. A source IP address from outside of the network (10.16.80.243) makes multiple protocol negotiation requests and attempts to login to a guest account on host 10.168.27.10, which is running Windows Server 2012. SMB allows for files to be shared over a network.

<img src="/assets/img/projects/c844t1/s7.png">

The next anomaly I noticed was regarding ICMP. There are numerous recursive requests from the same IP address outside of the network (10.16.80.243) with the resulting information being port unreachable. The source and destination ports specified in the UDP are 137, which is reserved for NetBIOS Name Service.

<img src="/assets/img/projects/c844t1/s9.png">

The last anomaly I noticed was the abundance of MySQL response errors and malformed packets. Again, these communications are with an IP address that is outside of the network (10.16.80.243) and host 10.168.27.10. The response error is consistently 1130.

### Wireshark Anomaly Implications

#### Anamoly 1

It’s clear an outside attacker was attempting to gain access into host 10.168.27.10, as seen by their attempt to login into a guest user account. Had this account not been disabled, the attacker could have gained access to the host; depending on the privileges allotted for that guest account, the results could range from minimal to catastrophic. The attacker could have also been attempting to exploit a known vulnerability relating to Windows Server 2012 and SMB, where specially crafted requests are made to the server to cause a denial of service (CVE-2018-8335). This can be surmised from the multiple requests made to the host in the instance.

#### Anamoly 2

ICMP is used to indicate the success or failure of communications between two IP addresses. In the recursive requests seen in the Wireshark scan, it appears an outside attacker may have been attempting to cause a denial of service. This is done through a known vulnerability in Windows Server 2012, where the NAT driver incorrectly validates memory addresses during the processing of ICMP packets (CVE-2013-3182).

#### Anamoly 3

There was an abundance of MySQL response errors 1130, all made in frequent succession. This may have been another attempt by an outside attacker to cause a denial of service. Error 1130 also indicates that an attempt is being made to connect to the server by someone other than the host on which the MySQL server is running (Navicat, 2018).

## Recommended Solutions

#### Vulnerability 1

Ubuntu acknowledged this vulnerability and released Ubuntu 14.04 ESM. Ubuntu recommends updating the current system to the previously specified package version to mitigate this vulnerability (Ubuntu, 2020).

#### Vulnerability 2

Microsoft recommends utilizing router or firewall rule sets to deny any incoming requests from wildcard domains (Microsoft Security Bulletin MS14-076, 2014).

#### Vulnerability 3

Microsoft recommends installing the latest security update which modified how SAM and LSAD handle authentication levels (Microsoft Security Bulletin MS16-047, 2016).

#### Anomaly 1

Microsoft recommends installing the latest security update which corrected the way that SMB handles specially crafted client requests (Windows SMB Denial of Service Vulnerability, 2018).

#### Anomaly 2

Microsoft recommends installing the latest security update which corrected how the Windows NAT Driver service validates addresses and handles specially crafted ICMP packets (Microsoft Security Bulletin MS13-064, 2013).

#### Anomaly 3

Oracle recommends applying the latest Critical Patch Update and doing a review of user privileges and applying the principles of least privilege (Oracle Critical Patch Update Advisory, 2018).

## References

CVE -CVE-2019-14896. (n.d.). CVE -CVE-2019-14896. https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-14896

CVE -CVE-2014-4078. (n.d.). CVE -CVE-2014-4078. https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-
4078

Microsoft Security Bulletin MS14-076 - Important. (2023, March 1). Microsoft Security Bulletin MS14-076 - Important. Microsoft Learn. https://learn.microsoft.com/en-us/security-updates/securitybulletins/2014/ms14-076

CVE -CVE-2016-0128. (n.d.). CVE -CVE-2016-0128. https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-0128

CVE -CVE-2018-8335. (n.d.). CVE -CVE-2018-8335. https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-8335

1130 – Host xxx is not allowed to connect to this MySQL server. (2018, February). https://help.navicat.com/hc/en-us/articles/218283147-1130-Host-xxx-is-not-allowed-to-connect-to-this-MySQL-server

CVE -CVE-2013-3182. (n.d.). CVE -CVE-2013-3182. https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2013-3182

USN-4228-2: Linux kernel (Xenial HWE) vulnerabilities. Ubuntu security notices. Ubuntu. (n.d.). USN-4228-2: Linux Kernel (Xenial HWE) Vulnerabilities. Ubuntu Security Notices. Ubuntu. https://ubuntu.com/security/notices/USN-4228-2

Microsoft Security Bulletin MS16-047 - Important. (2023, March 1). Microsoft Security Bulletin MS16-047 - Important. Microsoft Learn. https://learn.microsoft.com/en-us/security-updates/securitybulletins/2016/ms16-047

Security Update Guide - Microsoft Security Response Center. (n.d.). Security Update Guide - Microsoft Security Response Center. https://msrc.microsoft.com/update-guide/en-US/advisory/CVE-2018-8335

Microsoft Security Bulletin MS13-064 - Important. (2023, March 1). Microsoft Security Bulletin MS13-064 - Important. Microsoft Learn. https://learn.microsoft.com/en-us/security-updates/securitybulletins/2013/ms13-064

Oracle Critical Patch Update. (2018, October). Oracle Critical Patch Update - October 2018. https://www.oracle.com/security-alerts/cpuoct2018.html
