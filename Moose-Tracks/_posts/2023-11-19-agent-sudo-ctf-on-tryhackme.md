---
layout: post
title: Agent Sudo CTF Write-Up
image: /assets/img/blog/agentsudo/agentsudo.png
accent_image: 
  background: url('/assets/img/blog/agentsudo/agentsudo.png') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Hacking a secret server in the deep sea!
invert_sidebar: true
---

# Agent Sudo CTF Write-Up

<center>"You found a secret server located under the deep sea. Your task is to hack inside the server and reveal the truth."</center>
<b>

Another CTF from TryHackMe where we'll do some hash cracking, brute forcing, and privelage escalation!

Feel free to follow along: <a href="https://tryhackme.com/room/agentsudoctf">Agent Sudo CTF</a>

* toc
{:toc}

## Task 2 - Enumerate

As always we start off with an nmap scan.

<img src="/assets/img/blog/agentsudo/nmap.png">

### How many open ports?

Our scan reveals 3 open ports: 21(FTP), 22(SSH), and 80(HTTP).

### How you redirect yourself to a secret page?

Navigating to the IP address yields us a note from Agent R.  We are to use our own "codename" as user-agent to access the site.

<img src="/assets/img/blog/agentsudo/site.png">

### What is the agent name?

The user-agent being referred to in the note is a bit of a play on words.  From a browser's perspective, the user agent is a string used to identify itself to a web server.  Perhaps capturing a request with Burp Suite will let us play with this some more?

<img src="/assets/img/blog/agentsudo/burp1.png">

There's a user-agent in captured request!  This is where I had to put my thinking cap on...the only agent we know of so far is "Agent R" so maybe there's an alphabet thing going on?  I tried A, B, and finally C revealed another clue!

<img src="/assets/img/blog/agentsudo/burp2.png">

<img src="/assets/img/blog/agentsudo/agentc.png">

## Task 3 - Hash cracking and brute-force

Now that we know "agent C" is Chris we can try and brute force FTP using hydra.

### FTP password

Hydra gives us our FTP password for Chris!

<img src="/assets/img/blog/agentsudo/hydra.png">

### Zip file password

We have an FTP login.  I wonder what we have access to there?

<img src="/assets/img/blog/agentsudo/ftp.png">

An ls shows us 3 files, which I downladed using mget *.  2 of these are some adorable alien pictures, and the other a text file.  The text file is a note from agent J to agent C.

<img src="/assets/img/blog/agentsudo/ftp2.png">

<img src="/assets/img/blog/agentsudo/ftp3.png">

But what about those images...using strings I was able to extract some more information from cutie.png

<img src="/assets/img/blog/agentsudo/strings.png">

Looks like we have some hidden files in those images!  I used binwalk to extract them from the image.  Navigating to the extracted _cutie.png.extracted directory reveals a zip file.  

<img src="/assets/img/blog/agentsudo/bin.png">

So, now we have a zip file, but trying to unzip it requires a password.  I used zip2john to extract the password hash, and then used john the ripper to crack the hash.

<img src="/assets/img/blog/agentsudo/zip.png">

### steg password

Binwalk was unable to extract anything from cute-alien.jpg, so I decided to try stegcracker instead.  

<img src="/assets/img/blog/agentsudo/zip.png">

### Who is the other agent (in full name)?

Stegcracker was able to successfully extract a note from the image.  The note reveals our second agents full name AND a password!

<img src="/assets/img/blog/agentsudo/note.png">

### SSH password

Refer to the screenshot above.

## Capture the user flag

Using our harvested credentials we can login as james using ssh.  Using cat on the user_flag.txt will reveal our user flag.

<img src="/assets/img/blog/agentsudo/james.png">

### What is the user flag?

Refer to the screenshot above.

### What is the incident of the photo called?

Using scp I downloaded the photo in james' directory.

<img src="/assets/img/blog/agentsudo/auto.png">

Now using TinEye to do a reverse image search we can answer this question!

## Privilege escalation

Our next step is privilege escalation.  Lets find a CVE that's appropriate.

### CVE number for the escalation

A quick search on Exploit-DB gives us our CVE!

<img src="/assets/img/blog/agentsudo/db.png">

### What is the root flag?

Next we'll run sudo -l to see what privilages james has.

<img src="/assets/img/blog/agentsudo/sudol.png"> 

Cross referencing this information with our CVE reveals that running "sudo -u#-1 /bin/bash" will get us some root.  Navigate to /root to get the last flag!

<img src="/assets/img/blog/agentsudo/lastflag.png"> 

### (Bonus) Who is Agent R?

This is revealed in the root.txt flag.



