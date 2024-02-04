---
layout: post
title: Cyborg CTF Write-Up
image: /assets/img/blog/cyborg/cyborg.gif
accent_image: 
  background: center / cover url(https://mullet-moose.github.io/assets/img/blog/cyborg/cyborg.gif)
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  A fun TryHackMe CTF that includes encrypted archives and source code analysis.
invert_sidebar: false
---

# Cyborg CTF Write-Up

Today I'm jumping into another CTF on THM!  Cyborg is a beginner level box that will have us investigating some encrypted archives and doing some source code analysis.  I'm a huge Teen Titans fan, so subject matter alone had me hooked from the start!  

Feel free to follow along: <a href="https://tryhackme.com/room/cyborgt8">Cyborg</a>

* toc
{:toc}

## Scan the machine, how many ports are open?

As is tradition, we'll do some enumerating and run an nmap scan to discover any open ports.  The scan reveals that ports 22 and 80 are open for business!

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/nmap.png">

Scan the machine, how many ports are open?
	
	2

## What service is running on port 22?

Well this is pretty easy...

What service is running on port 22?
	
	ssh

## What service is running on port 80?

Again...

What service is running on port 80?

	http

## What is the user.txt flag?

First step is to continue our enumeration on the http port.  I'm using dirbuster for the task.  Dirbuster gives us a few more pages to explore.  

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/dirb.png">

Navigating to /admin reveals this might be a personal site for Alex, a music producer from the UK.

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/admin.png">

The "Admins" tab reveals a shoutbox with some interesting information...

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/box.png">

Alex is pretty sure he's making his site more insecure by not configuring his squid proxy correctly.  I guess we should test his theory!

Navigating to /etc revevals a squid directory.  Inside, a passwd file with some credentials.  Taking note of those for later...

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/squid.png">

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/cred.png">

Back at the /admin page I decided to try the "Download" option under the "Archive" tab.  This gives us Alex's archive.tar.  Let's untar!

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/tar.png">

Revisiting those credentials in the passwd file; lets see if we can crack the hash with hashcat.  But first, we'll need to cross reference some examples to deduce what mode we're working with.  The $apr1$ prefix is indicitive of mode 1600 MD5 (APR).  After saving the hash to a file we can run hashcat in the 1600 mode.

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/arch.png">

Now that we have a cracked hash we can head back over to our extracted archive.  Navigating through here I found a README file in final_archive that states "This is a Borg Backup repository."  That seems like useful information.  

After doing some research I found that there's an extract command we can use with borgbackup.  I installed borgbackup and used our gathered credentials to extract the files from music_archive.

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/borg.png">

We can now sift through Alex's home directory.  Navigating to /home/alex/Documents reveals a note.txt which includes some more credentials.  I used those credentials to gain ssh access.

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/alex.png">

A simple ls and cat and we have our first flag!

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/userflag.png">

What is the user.txt flag?
	
	flag{1_hop3_y0u_ke3p_th3_arch1v3s_saf3}
	
## What is the root.txt flag?

On to the root flag, I ran sudo -l to see what all Alex can sudo, and find that he can run backup.sh.

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/sudo.png">

Investigating backup.sh reveals that there is a backup being performed on all mp3 files in /home.  The most interesting thing though, was a small section of script with the word flag in it.  Also worth noting is the end function, which will take a parameter and run it at the end of the script.  We can use this to our advnatage!

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/backup.png">

First we need to give /bin/bash the SUID bit.

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/c.png">

Sweet!  Now just bash -p to get some rooty goodness and read our final flag :)

<img src="https://mullet-moose.github.io/assets/img/blog/cyborg/root.png">


What is the root.txt flag?

	flag{Than5s_f0r_play1ng_H0p£_y0u_enJ053d}
	
Neato!  I had a pretty fun time with this box.  It was a great opportunity to brush up on some fundamentals :)

