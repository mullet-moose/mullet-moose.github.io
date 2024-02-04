---
layout: project
title: 'Digital Forensics - Investigative Plan of Action'
caption: Creating a plan of action for a digital forensics investigation.
description: >
  Creating a plan of action for a digital forensics investigation.
date: '2023-09-28'
image: 
  path: /assets/img/projects/d431t1/cover.png
accent_image: 
  background: url('/assets/img/projects/d431t1/cover.png') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
invert_sidebar: false
sitemap: false
---

This is a project for my *Digital Forensics in Cybersecurity* course at WGU.  We were given a case study and asked to create an investigative plan of action.

* toc
{:toc}

### Strategy

It is imperative that we formulate a strategy that allows our team to collect the maximum
amount of necessary evidence swiftly and thoroughly while also ensuring the least amount of
disruption to the organization and its day-to-day operations. It is also paramount that we engage
in detailed documentation of all our actions during the investigation and maintain a proper chain
of custody to allow the evidence to be admissible in court if need be.

To prepare the investigation team, we will hold a preliminary meeting with senior
management and the legal office to gather pertinent information about the accused, John Smith,
including his authorizations, system accessibility, and general job requirements. This will assist
in evaluating and mapping possible avenues in which Smith may have been able to exfiltrate
proprietary information and when he may have done so. This information will help us determine
the scope of our investigation and our plan of action to ensure the maximum collection of
evidence.

After determining the scope of our investigation, we will be able to strategically plan our
evidence collection in a way that minimizes the impact on the organization. While our team
wants to ensure that evidence is collected quickly, we also want to avoid any disruptions that will
negatively impact business. Senior management will advise on peak performance hours;
evidence gathering will occur outside of this time frame.

To acquire the appropriate data, our team will first document and photograph the current
physical state of the applicable systems as identified by senior management. Our team will then
utilize FTK Imager to collect volatile and non-volatile memory. We will utilize the included
write blocker in FTK Imager to prevent any source data modification. Hash values will also be
created for both the source and image files to ensure integrity.

The senior management and legal office will advise on the appropriate terminology to be
used in a keyword search of the acquired data, as well as the file format and location. This will
allow our team to locate the proprietary information more easily and how it may have been
accessed and exfiltrated.

### Tools and Techniques

Our team will utilize the FTK Suite of products as well as Autopsy. FTK Imager will
allow us to image volatile and non-volatile data. It is important to note that our team will create
two images of the source with SHA1 hashes to ensure integrity. One image will be analyzed
with FTK, while another will be analyzed with Autopsy. This method will allow us to validate
our results. The FTK Suite also includes useful tools for password cracking, examining email,
and Windows Registry analysis should the need arise during our investigation (Easttom, 2021).
Other techniques to make note of will include proper documentation of all actions and
procedures, maintaining a proper chain of custody, and ensuring all evidence is transported and
stored securely.

### Collection and Preservation of Evidence

It is extremely important that our team engages in thorough documentation of all steps
and procedures when collecting data. It is equally as important to maintain a proper chain of
custody for all evidence from the moment of its collection. Strictly adhering to both practices
will allow our evidence to be admissible in court and minimize any scrutiny of our findings.

It will be most likely that Smith’s host machine will need to be collected and transported
to our forensics lab for proper imaging and analysis. Before collection, we will make note of the
physical layout of his workstation and take photographs. Our team will then investigate what
current processes may be running and photograph the results while being careful to touch the
system as little as possible (Easttom, 2021). Additionally, a memory capture will take place
before transport using FTK Imager. This could yield valuable information regarding how the
proprietary information may have been accessed and exfiltrated. Once these steps have been
completed, our team will securely transport the computer in a locked vehicle to the forensics lab.

When the computer has been successfully transported to the forensics lab, our team will
carefully begin to dismantle the system, making proper documentation of its interconnections.
This will be followed by a check of the systems BIOS. Subsequently, images of all non-volatile
memory will be created using FTK Imager, and SHA1 hashes will be utilized on all images and
the source to verify integrity. While analysis of the images takes place, all evidence will be
locked and secured and will only be accessible by authorized investigators.

### Examination of Evidence

During our preliminary meeting with senior management, our team will acquire the file
format, location, and any keywords relating to the proprietary information in question. It would
also be advantageous to know who had authorized access to this information without needing
prior approval. This information will help our investigators sift and analyze the data quickly and
thoroughly.

It would also be wise to review the NDA and AUP with senior management and the legal
team. Any vague or unelaborated statements in these documents may help our team discover
possible avenues of Smith’s alleged activities. Perhaps Smith saw a loophole in either of these
documents that he could take advantage of?

With this information, our team will be able to utilize the FTK Suite and Autopsy to
search for and analyze the relevant data. Our team will utilize live analysis, physical analysis,
and logical analysis, as well as the order of volatility in our examination of the data. Our team
will also make sure to do a thorough search and analysis of any relevant information that may be
hidden in areas such as the volume slack, file slack, and unallocated space. Additionally, it
would be wise to perform steganalysis on any suspect files to check for hidden content that may
be related to our investigation.

### Approach to Drawing Conclusions

In our preliminary meeting with senior management and the legal team, we will review
the NDA and AUP. This is important, as identifying exactly what the company policies are and
how Smith allegedly violated them will assist us in drawing our conclusion. This preliminary
meeting will also allow our team to ensure that our investigation is done in accordance with
company policy.

To draw a sound and accurate conclusion, our team will make sure that no data is altered
through the course of our collection and analysis. The integrity of the information can be
validated using SHA1 hashes on the data source and images. As we will be creating two images
of the source, our team will also be sure to analyze the data with both the FTK Suite and Autopsy
to validate our findings.

It is imperative that the evidence used in our conclusion is directly related to both the
proprietary information and policies at hand. Our evidence needs to clearly show that the
proprietary information was accessed by Smith without prior authorization, how it may have
been shared and with whom, and how these actions clearly violate the NDA and AUP.

### Presentation of Details and Conclusions

An expert report will be generated that will detail our processes and procedures including
all documentation and the maintained chain of custody. The expert report will also identify the
tools and techniques we used to gather and analyze the data as well as our subsequent conclusion
from our findings. Additionally, a curriculum vitae will be provided to exemplify my expertise
as a digital investigator (Easttom, 2021).

In addition to the expert report, we will brief senior management on our findings. Our
presentation will be clear, concise, and cohesive. The presentation will be made orally with a
supplemented digital slide show including relevant information. It is important that this
presentation be made in layman’s terms, avoiding overly technical language, and provide the
general scope of our investigation and conclusions. This will aid in the senior management’s
comprehension of our findings and assist them in determining their next course of action.

### References

Easttom, C. (2021). Digital Forensics, Investigation, and Response (4th ed.). Jones & Bartlett
Learning, LLC.
