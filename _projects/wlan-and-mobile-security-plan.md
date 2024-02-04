---
layout: project
title: 'WLAN and Mobile Security Plan'
caption: Identifying vulnerabilities and recommending solutions for WLAN and Mobile.
description: >
  This is another project for my *Emerging Technologies in Cybersecurity* course at WGU.
date: '2023-09-13'
image: 
  path: /assets/img/projects/c844t2/cover.webp
accent_image: 
  background: url('/assets/img/projects/c844t2/cover.webp') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
sitemap: false
---

In this *Emerging Technologies in Cybersecurity* project we were given a mock scenario and were tasked with identifying vulnerabilities and recommending soltuions for WLAN and Mobile.

* toc
{:toc}

### WLAN Vulnerabilities

The first vulnerability that should be taken note of is the access point servicing the back
patio. As this access point is easily discoverable, it paves the way for numerous avenues in
which attackers can exploit the network. Evil twin access points could be easily made to trick
employees into connecting to a false SSID mimicking the trusted network. Additionally, there is
no mention of any type of SATE program at Alliah, which means many employees may be
uneducated in this threat. Furthermore, having an easily discoverable network increases the risk
for denial of service attacks and sniffing.

The next vulnerability that should be taken note of is the potential for rouge access points
to be introduced into the network. While having the vacant third floor is excellent for expansion
purposes, the lack of physical security measures make this a prime location for potential
attackers to install a rouge AP. Considering traffic to this area would be low to non-existent, a
rouge AP could go unnoticed for a great deal of time. Such a vulnerability could lead to sniffing,
malware, and exposure of personal employee information and sensitive company assests.

### Mobile Vulnerabilities

The five account representatives who travel pose the first vulnerability I see with mobile
devices. These employees are provided a company laptop, tablet, and smartphone. There is no
mention of installed anti-malware software on these devices, which puts them at greater risk,
especially as they are traveling and making use of public Wi-Fi in several locations.
Additionally, these employees are returning to use the office network on occasion, which means
these employees could be bringing threats directly to Alliah’s network.

Another vulnerability also relates to the five employees who travel for significant
portions of time. All of the company issued devices are at greater risk for theft while they are
traveling. There is no mention of any form of a stored data encryption standard, which means
stolen devices could easily be hacked to gain sensitive company or employee information.

### Mitigation

A mitigation technique for the access point in the back patio would be to reconsider the
design of the network and placement of access points. Utilizing semi directional atennas on the
building perimeter, with omni directional attenas in central locations would assist in containing
the broadcast and mitigate the likelihood of attackers discovering the network. Lowering the
power on some devices would also help contain the scope of the broadcast (Doherty, 2021). Alliah could also opt to hide the SSID making discovery and access for non-employees more
difficult, and decrease the likelihood of evil twins. It would also be recommended to ensure that
proper wireless encryption standards are enabled, such as WPA3. Additionally, having a well
thought out disaster recovery plan in the event of a denial of service attack would lessen the
impact and ensure a swift return to normal operations.

To mitigate the risks associated with rogue access points, I would advise enacting a
policy that requires periodic sweeps of all areas to physically check for any unknown devices. It
would also be wise to invest in an Intrusion Detection System and/or Inrustion Prevention
System that would alert the IT staff when anomalies are detected on the network.

To mitigate the risks associated with company issued devices that are susecipable to
malware, I would recommend that the IT staff install a robust anti-malware program and ensure
that this software, as well as the operating system, are up to date on company issued devices.
Additionally, making use of VPN’s while employees are traveling would assist in making
communications more secure and decrease the likelihood of sensitive data being intercepted.

To mitigate the risks associated with company devices being lost or stolen, I would
recommend requiring stored data encryption for all company devices to protect sensitive or
confidential employee and company information. I would also make use of remote locking and
data wiping tools for company devices to protect the previously mentioned information and
ensure hackers are unable to access it (Doherty, 2021).

### Preventative Measures

A defense in depth approach would be the best preventative measure to maintain the
security posture of the WLAN at Alliah. As the company grows, so will their associated threats
and vulnerabilities which puts the company, it’s employees, and it’s clients at greater risk. Also
worth noting, since Alliah is a social media company, they have increased access to an
abundance of Personally Identifiable Information for it’s users. I would recommend providing
greater physical security, both at the office and off-site data center, such as hiring security
guards, installing security systems, and using adequate locks and authentication mechanisms for
access to either premises. Making use of a DMZ for public facing servers and installing
additional firewalls with more robust permission definitions would also secure the confidentiality
and integrity of sensitive data. Both of these options would prevent the access and misuse of the
WLAN by potential attackers.

As noted Alliah is a social media company and it’s user base will extend outside of the
United States. Adhering to the European Union’s General Data Protection Regulation (GDPR)
would maintain and expand the security posture of the WLAN at Alliah, and ensure theconfidentiality, integrity, and availability of the company’s information and that of it’s users
(European or not).

	“The GDPR has seven key principles:

		Lawfullness, fairness, and transparency
		Purpose limitation
		Data minimization
		Accuracy
		Storage limitation,
		Integrity and confidentiality (security)
		Accountability” (Doherty, 2021).
		
In summation, applying a defense in depth approach and complying to the GDPR key principles
would maintain and expand the security posture of the WLAN at Alliah.

I would recommend instating methods of authentication, authorization, and accountability to
maintain and expand the security posture of the mobile environment at Alliah. This also falls
under a defense in depth approach, and increases security measures for both employee owned
and company issued devices. Authentication validates user and/or device identity, authorization
grants specific access rights to those users and devices, and accountability records their system
activity (Doherty, 2021). Applying these measures would prevent the access and misuse of
company, employee, and customer data.

As stated in the case study, Alliah is considering going public in the near future. The
previously mentioned measures (AAA) would support the compliance to the Sarbanes-Oxley Act
(SOX) which mitigates financial fraud through standardized reporting and auditing at public
companies (Doherty, 2021). The adherence to SOX not only protects the integrity of financial
data. It also serves as a guideline for protecting the integrity of all data within the company and
the importance of information security (Doherty, 2021).

### Recommendations

The BYOD policy is a major vulnerability at Alliah, as with many other companies.
Employee owned devices tend to be lacking in updates which make them susceptible to malware
and exploitation. My first recommendation would be to utilize a SaaS Mobile Device
Management solution in conjunction with a Choose Your Own Device program. This ensures
that company issued devices are receiving necessary updates, proper configuration settings are
maintained, and would provide additional services like remote locking and wiping (Doherty,
2021). The remote locking and wiping services are specifically important in mitigating risks
associated with lost or stolen devices.

My next recommendation would be providing and enforcing an Accetpable Use Policy as
well as applying the principles of least privealge to all company devices. When switching to a
CYOD program, employees may be tempted to jailbreak company issued devices to gain more personal functionality (Doherty, 2021). An Acceptable Use Policy would deter such actions and
lay out specific consequences for any ethical or legal violations while company devices are being
used. Additionally, applying the principles of least privilege would decrease the attack vector of
the network by providing only the necessary permissions and access needed on company
devices.

### References

Doherty, J. (2021). Wireless and Mobile Device Security (2nd ed.). Jones & Bartlett Learning,
LLC. https://ebookcentral.proquest.com/lib/westerngovernors-
ebooks/reader.action?docID=6461875&ppg=1
