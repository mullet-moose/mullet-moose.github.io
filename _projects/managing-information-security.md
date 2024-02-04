---
layout: project
title: 'Managing Information Security'
caption: Analyzing the relationship between inforamtion security and business goals/objectives.
description: >
  In this project we were given a case study and asked to analyze the relationship between inforamtion security and business goals/objectives.
date: '2023-11-18'
image: 
  path: /assets/img/projects/c843/cover.jpg
accent_image: 
  background: url('/assets/img/projects/c843/cover.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
invert_sidebar: false
sitemap: false
---

This is a project for my *Managing Information Security* course at WGU.  We were given a case study and tasked with developing an information security governance framework, aligning security programs with best practices, and recommending procedures that minimize risk to the company.  

* toc
{:toc}

### Attack Successes and Vulnerabilities

Elecktores was successful in their spear-phishing of John Smith.  The vulnerability that contributed to this successful attack was the lack of end-user awareness and training.  John was neither hesitant or suspicious of the Elecktores email; proper training may have helped mitigate this attack from the start.

Elecktores was able to gain access to the volunteer database within Azumer Water’s main office network.  Azumer Water’s main office network is un-segmented.  Anyone within the network can easily traverse to the database server and access volunteer information.  Had the database server been segmented with an additional properly configured firewall, Elecktores may not have been successful in accessing the information it contained.

### Compromise of CIA and PII

Confidentiality and PII:  
  -  PII can include any information held by an agency that can be used to identify an individual (NIST SP 800-122, 2010).  The database server within Azumer Water’s network contained volunteer information including basic contact information, background checks, and the last 4 digits of volunteer’s social security numbers (Case Study, Azumer Water, n.d.).  Confidentiality and PII were compromised when Elecktores gained access to the database server and successfully obtained volunteer information, which they used to engage in a phishing campaign to obtain credit card information from volunteers.  “Personal data should be protected by reasonable security safeguards against such risks as loss or unauthorized access, destruction, use, modification or disclosure of data” (NIST SP 800-122, 2010).    

Integrity:  
  -  Integrity was compromised when Elecktores previously engaged in malicious activities to cancel the delivery of ordered bottled water (Case Study, Azumer Water, n.d.).  According to ISO/IEC 27002: “Information involved in electronic commerce passing over public networks should be protected from fraudulent activity, contract dispute, and unauthorized disclosure and modification.”  Elecktores was able to compromise integrity by altering messages in order to cancel a delivery that had already ordered.
  
Availability:  
  -  The morning after falling victim to Elecktores’ email, John Smith was unable to find or access the volunteer database.  This is a compromise of availability, as Elecktores was able to hinder his needed access to the information within the database.  Additionally, Azumer Water does not back up the database.  John currently has limited options to accessing the data he needs.
  
### Federal Regulation Violation

FISMA – Federal Information Security Management Act:  This act requires that federal agencies implement programs to ensure the security of information and  information systems within that agency (FISMA, 2002).  Azumer Water is an extension of FEMA (Federal Emergency Management Agency), thus FISMA would apply to Azumer Water.

Azumer Water did not attempt to create and implement an adequate information security program which resulted in the compromise of confidentiality of volunteer PII held within their networks database server.  Pruhart Tech was contracted by Azumer Water to provide IT services and maintain it’s IT infrastructure.  Maria Rodriguez, CEO of Azumer Water, had been aware that the security posture of the company was lacking.  Still, despite frequent recommendations from Pruhart, Maria decided to accept the risks as she thought the likelihood of any attacks were slim.  Pruhart was also unable to perform any vulnerability assessments or risk mitigations (Case Study, Azumer Water, n.d.).   Furthermore, there is no mention of any documentation efforts regarding the information security controls of Azure Water.  These facts all constitute violations of FISMA, which require regular risk assessments, annual security reviews, documentation of controls, and the adherence to a security control baseline (FISMA, 2002).  

### Mitigating the Impact of the Incident

1st Recommendation:  

I would first recommend that Azumer Water reset the credentials on all full time employee accounts associated with their network.  This would assist in mitigating the further misuse of any previously gathered credentials that could be used to gain access to and compromise their system.  Unless alternative paths had been created, Elecktores would no longer have access the Azumer Water network, and would no longer be able to exfiltrate sensitive information (like volunteer PII), compromise the integrity of any communications, and prevent any further denial of availability of company information or information systems to the full time employees.

2nd Recommendation:  

I would then recommend that Azumer Water immediately inform all volunteers, full time employees, and any related stakeholders (water bottle vendors, shipping companies, etc.) of their networks compromise.  In doing so Azumer Water can advise that suspicious impersonation emails may be coming from their company and that they should proceed with caution; do not click on any links, open any attachments, or reply.  This would mitigate Elecktores efforts in gaining volunteer credit card information, as well as any future actions they may had planned to compromise water bottle orders, shipping schedules, or volunteer trainings.  

### Incident Response Plan

NIST SP 800-61 outlines the basic steps in an Incident Response Plan as: Preparation, Detection and Analysis, Containment, Eradication, and Recovery, and Post-Incident Activity (NIST SP 800-61, 2012).

Benefit #1:  

Considering no incident response plan was in place, the Preparation step would have helped immensely in dealing with the unauthorized access of Azumer Water’s database server and subsequent exfiltration of volunteer PII by Elecktores.  First, preparing for an incident would have forced the consideration of the overall security posture of the organization.  Preparation not only signifies an organizations capability to respond to an incident, but also the prevention of incidents through implementing and maintaining a substantial security posture (NIST SP 800-61, 2012).  

Had Azumer Water taken steps to prepare for an incident, they may have realized that security was lacking, especially pertaining to the PII of volunteers.  Such a realization could have encouraged them to not only prepare for an incident, but also take steps to properly secure this information.  This could include segmenting their network and placing the database behind a well configured firewall, properly configuring their public facing firewall, encrypting the information at rest within the database, and enacting some form of data loss protection to add an additional layer of security.  Furthermore, the actual preparation for an incident would have allowed for a much quicker response to Elecktores’ unauthorized access and exfiltration.  

It seems as though John Smith was still unaware of the situation at hand during his meeting with Maria and I, which clearly showed that the incident itself had not detected at this point.  This would also fall on Pruhart, who handles the IT infrastructure at Azumer Water.  Proper preparation would have including discussions with Pruhart on their involvement through the IRP and how they would communicate with Maria and I through the process.  Had these measures been in place, it is likely that Elecktores would never have so easily gained access to the database server.   If they eventually still gained accessed, the incident could have been detected and dealt with swiftly, mitigating it’s impact the Azumer Water and it’s volunteers.  

Benefit #2:  

Detection and Analysis would have been extremely beneficial to Azumer Water.  After working with Pruhart on a well defined IRP, the access of Elecktores to their network could have been identified in a timely manner.  Implementation of various tools including Intrusion Detection Systems, Anti-Virus/Anti-Malware programs, NextGen Firewalls, or Log Analyzers would have alerted Azumer Water and Pruhart that Elecktores had gained unauthorized access to their database.  

If the attack vector in Elecktores attack had been a backdoor trojan downloaded through their malicious email link, an Anti-Virus/Anti-Malware could have alerted Pruhart that an incident may be taking place and allowed them to investigate further.  Similarly, an IDS could have alerted Pruhart that unauthorized access had been made from an external source and allowed them to investigate further.  

In either scenario, Pruhart’s analysis would have likely led to the conclusion that something nefarious was taking place, and the proper steps would have been initiated to contain and eradicate the threat before substantial harm could be done.  In this case, Elecktores would most likely have not gained access to the database, and the volunteers PII would have been protected from exfiltration.  This reduces any potential damage to the volunteers, as well as any reputational damage to Azumer Water.  

### Compliance with FISMA

Azumer Water is in violation of FISMA, which requires the development and implementation of a security program, regular risk assessments, annual security reviews, documentation of controls, and the adherence to a security control baseline (FISMA, 2002).  

Process #1:  

First and foremost, Azure Water (with assistance from Pruhart Tech) needs to develop and implement a security program that meets security control baselines.  I would recommend they start this process by initially performing a system risk categorization to identify the risk levels associated with the information they are in possession of.  This categorization will guide them in implementing the correct controls.  I would make sure that the security of the PII would be front of mind for this process.  Additionally, adequate documentation of security controls needs to be maintained in an SSPP (System Security and Privacy Plan) to remain compliant with FISMA (FISMA, 2002).  

Process #2:  

Regular risk and vulnerability assessments, as well as annual security reviews, need to be scheduled and maintained in order to remain complaint with FISMA.  I would recommend Azumer Water immediately begin with their risk and vulnerability assessments while as they develop and implement their security program.  After the program is in place, I would recommend doing an initial security review to ensure their program is in compliance and no important aspects have been overlooked.  Utilizing Pruhart to engage in continuous monitoring after the fact would also be recommend to ensure continual compliance with FISMA. 

### Technical Solutions

Technical Solution #1:  Encryption for Data at Rest

The PII held within Azumer Water’s database server is sensitive and was the target of the attack by Elecktores in which volunteer information was exfiltrated and used in a phishing campaign to obtain volunteers credit card information.  Encrypting this data at rest would have ensured it’s protection and mitigated it’s misuse by Elecktores.  Specifically, Elecktores would have been unable to obtain the volunteer email addresses that they used in their subsequent campaign.  I would recommend using a secure symmetric encryption algorithm such as AES-256 to encrypt the data.

Technical Solution #2:  Firewalls

Once Elecktores gained access to Azumer Water’s network, they were able to easily traverse to the database server and exfiltrate volunteer PII.  The use of multiple properly configured firewalls would have made their movement into and through the network more difficult and could have possibly thwarted their attack by preventing their access to the database server.  First, the public facing firewall should be correctly configured with an implicit deny rule that blocks all traffic that is not explicitly allowed via allow rules.  This could have stopped their initial entrance into the network.  Second, I would recommend using additional firewalls to logically segment the internal network.  Specifically, placing the database server on it’s own VLAN behind a properly configured and highly secure firewall would have stopped Elecktores from easily gaining access to it, even if they had managed to gain access into the network.

### Risk Management Categorization

<img src="/assets/img/projects/c843/rm.png">

### Risk Management Approach

I believe that Azumer Water should approach Risk Management via NIST 800-37.  The NIST 800-37 lays out steps for their Risk Management Framework which include: Prepare, Categorize, Select, Implement, Assess, Authorize, and Monitor (NIST SP 800-37, 2018).  The reason I believe this approach would work best is because it is a nationally recognized approach that is widely accepted and easily implemented.  Because Azumer Water currently has no Risk Management in place, this would be an excellent starting point so they can engage in an effective Risk Management strategy.  It would allow them to properly manage current risks, as well as risks that arise in the future.  This would also heighten the company wide security posture.

A specific risk this could be applied to is the risk of an attacker gaining unauthorized access and exfiltrating volunteer PII.  The framework would start with establishing priorities for the company’s overall security and privacy.  This specific risk would then be categorized as high priority based on it’s likelihood and impact severity.  Next, controls would be selected to reduce the risk, such as using an Intrusion Detection System.  This control would be implemented and assessed to ensure it is working correctly.  The system would then be authorized and monitored to ensure effectiveness and determine if any changes are necessary.  


### References

NIST SP 800-122.  Guide to Protecting the Confidentiality of Personally Identifiable Information (PII).  McCallister, E., Grance, T., Scarfone, K. (April, 2010).  Retrieved from: https://srm--c.vf.force.com/apex/FDP/CommonsExpandedChatter?code=C843 

Azumer Water Case Study. Retrieved from: https://srm--c.vf.force.com/apex/FDP/CommonsExpandedChatter?code=C843 

ISO/IEC 27002.  Information Technology – Security techniques – Code of practice for information security management.  (2005).  Retrieved from: https://srm--c.vf.force.com/apex/FDP/CommonsExpandedChatter?code=C843 

Federal Information Security Management Act (FISMA). (2002).  Retrieved from: https://security.cms.gov/learn/federal-information-security-management-act-fisma 

NIST SP 800-61.  Computer Security Incident Handling Guide.  Cichonski, P., Millar, T., Grance, T., Scarfone, K.  (August, 2012).  Retrieved from: https://srm--c.vf.force.com/apex/FDP/CommonsExpandedChatter?code=C843 

NIST SP 800-37.  Risk Management Framework for Information Systems and Organizations.  (December, 2018).  Retrieved from: https://srm--c.vf.force.com/apex/FDP/CommonsExpandedChatter?code=C843 


