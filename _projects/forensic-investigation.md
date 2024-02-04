---
layout: project
title: 'Forensic Investigation'
caption: A mock forensic investigation project for my *Digital Forensics in Cybersecurity* course at WGU.
description: >
  In this project we were tasked with using Autopsy to analyze a storage device for evidence of company violations.
date: '2023-09-26'
image: 
  path: /assets/img/projects/d431t2/cover.jpg
accent_image: 
  background: url('/assets/img/projects/d431t2/cover.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
sitemap: false
---

In this project we were given a mock scenario about an oil company that's investigating a potential breach of company policy.  As the digital forensic analyst, I was tasked with using Autopsy to investigate and identify any evidence relating to the potential breach.

I started this project by opening Autopsy and creating a new case.  The appropriate data source was fed into the program (an acquired usb drive from our potentially bad actor), and I was able to begin my analysis.

* toc
{:toc}

### Analysis

The screenshots below show the steps of my analysis. I started by expanding the tabs on the left-hand pane and
extracting files to C:\Users\LabUser\Desktop\Evidence Files\Oil Company Investigation\Export. This included
files from $CarvedFiles, $Unalloc, and all Deleted Files.

Reviewing these files revealed a few things. First, there were numerous images of different schematics relating
to the oil company’s equipment and operations. There were also PDF files marked as confidential, which
included information regarding the oil company’s business strategies. Lastly, there were PDFs of saved
websites that included information on how to anonymously launder Bitcoin.

I made note that there was a Keyword Hit for email addresses. This was related to source file
Unalloc_4_12656640_1087102976.

I proceeded to view the Timeline by selecting the Timeline icon on the toolbar. This is important information as
it shows the sequence of events from 8/11/2021 to 8/13/2021 for when files were created and modified.

I also viewed the Data Source Summary by right clicking on JSmith_Q1.001 and selecting View Summary
Information. This showed that the data source was a 4GB Flash Drive and included a pie graph of the different
file types it contained.

#### File Extraction

<img src="/assets/img/projects/d431t2/fileext.png">

<img src="/assets/img/projects/d431t2/fileext2.png">

#### File Review

<img src="/assets/img/projects/d431t2/rev1.png">

<img src="/assets/img/projects/d431t2/rev2.png">

<img src="/assets/img/projects/d431t2/rev3.png">

#### Keywork Hit

<img src="/assets/img/projects/d431t2/key.png">

#### Timeline

<img src="/assets/img/projects/d431t2/time.png">

#### Data Source

<img src="/assets/img/projects/d431t2/data.png">

### Summary of Findings and Conclusions

Through my analysis I identified that John Smith did have possession of the oil company’s confidential
proprietary information which included schematic images and PDFs. I also identified that Smith was
researching, to some degree, how to anonymously launder money with Bitcoin which was deduced by the
related website PDFs found on the flash drive. The proprietary information was created and modified to the
4GB flash drive between the dates of 8/11/2021 and 8/13/2021, as shown in the Autopsy Timeline.

In conclusion, the provided evidence does show that John Smith violated company policy by taking proprietary
information without prior approval. It can also be presumed that Smith had intentions of selling this
information through anonymous Bitcoin transactions, however, more evidence would need to be gathered to
substantiate this claim and prove it beyond a reasonable doubt.

<img src="/assets/img/projects/d431t2/con.png">
