---
layout: post
title: Rick and Morty CTF Write-Up
image: /assets/img/blog/rickandmorty/pickle.webp
accent_image: 
  background: url('/assets/img/blog/rickandmorty/pickle.webp') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  “ThIs iS…*burp*…goNNA bE a Fun oNe MorTy….*louder burp*."
invert_sidebar: false
---

# Rick and Morty CTF Write-Up

Today we’re jumping into the Rick and Morty CTF by TryHackMe.com.  Rick’s done it again, and we’re tasked with exploiting a web server to find 3 special ingredients for a potion that will turn Rick back to “normal” (whatever that is).

Want to follow along?

<a href="https://tryhackme.com/room/picklerick">Pickle Rick</a>

* toc
{:toc}

## What is the first ingredient that Rick needs?

First things first.  I utilized nmap for some enumeration.  The scan revealed that there are two open ports we may be able to exploit:  Port 22 (SSH) and Port 80 (HTTP).  

<img src="/assets/img/blog/rickandmorty/nmap.png">

Navigating to the website brings up some cute instructions for Morty, but it's basically telling us what we already know.  Diving into the source code, however, reveals a helpful "note to self" and a username!

<img src="/assets/img/blog/rickandmorty/website.png">

<img src="/assets/img/blog/rickandmorty/sourcecode.png">

Sweet.  Surely there's more hiding on this server, so I decided to do some dirbusting.

<img src="/assets/img/blog/rickandmorty/dirb.png">

Interesting...robots.txt simply has Rick's mantra (burps).  My gut tells me this is most likely a password.  Now to figure out where to login...

<img src="/assets/img/blog/rickandmorty/robot.png">

Running a Nikto scan revealed a login page!  Using the previously gathered credentials I was able to successfully login and access a command panel.

<img src="/assets/img/blog/rickandmorty/nitko.png">

<img src="/assets/img/blog/rickandmorty/login.png">

<img src="/assets/img/blog/rickandmorty/command.png">

In the command panel I started with ls -la.  This revealed two suspicious files: *Sup3rS3cretPickl3Ingred.txt* and *clue.txt*.  Trying to cat the files in the command panel was unsuccessful.  I guess Rick didn't want this to be TOO easy for Morty.

<img src="/assets/img/blog/rickandmorty/lsla.png">

<img src="/assets/img/blog/rickandmorty/tryagain.png">

Luckily visiting the text file in my browser was successful!

<img src="/assets/img/blog/rickandmorty/1rst.png">

*What is the first ingredient that Rick needs?*
	
	mr. meeseek hair
	
## What is the second ingredient in Rick’s potion?

My next step was to investigate *clue.txt*.  Believe it or not...it gave us a clue!

"Look around the file system for the other ingredient."

<img src="/assets/img/blog/rickandmorty/clue.png">

I guess we'll take Rick's advice.  When has he steered Morty wrong before?

After messing around with the command panel for awhile I was able to achieve some directory traversal with cd.  After getting into the root directory, I went into home to find Rick's folder.  Rick's folder contained the file with the second ingredient, and I was finally able to read it with less!

<img src="/assets/img/blog/rickandmorty/dt.png">

<img src="/assets/img/blog/rickandmorty/home.png">

<img src="/assets/img/blog/rickandmorty/rickdir.png">

<img src="/assets/img/blog/rickandmorty/2nd.png">

*What is the second ingredient in Rick’s potion?*
	
	1 jerry tear
	
Poor Jerry :(

## What is the last and final ingredient?

On to the last ingredient!  I assumed we'd probably need to escalate privelages (that's normally how these rooms go) so I ran sudo -l in the command panel to see if there were any privelages to take advantage of.  Suprisingly, I could run all commands with no password.  Rick must have things other than security on his mind...

<img src="/assets/img/blog/rickandmorty/priv.png">

I managed to gain access to /root/ via sudo ls, which revealed the file containing our last ingredient.  It can be read using sudo less.

<img src="/assets/img/blog/rickandmorty/rootdir.png">

<img src="/assets/img/blog/rickandmorty/3rd.png">

*What is the last and final ingredient?*
	
	fleeb juice
	
That about wraps this one up!  Such a fun room, and I really have to give THM props for always finding ways to make things interesting, engaging, and FUN!  This room is also beginner friendly and a great way to get started or just reinforce the basics.  Why not try it for yourself?

<a href="https://tryhackme.com/room/picklerick">Pickle Rick</a>


