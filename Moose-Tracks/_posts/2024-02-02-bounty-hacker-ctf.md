---
layout: post
title: Bounty Hacker CTF Write-Up
image: /assets/img/blog/bounty/cowboy.webp
accent_image: 
  background: url('/assets/img/blog/bounty/cowboy.webp') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  A Cowboy Bepop inspired CTF from THM
invert_sidebar: false
---

# Bounty Hacker CTF Write-Up

"You talked a big game about being the most elite hacker in the solar system. Prove it and claim your right to the status of Elite Bounty Hacker!"

Time for another CTF from TryHackMe.  This is an easy level room inspired by the hit anime *Cowboy Bepop*.

* toc
{:toc}

## Who wrote the task list?

Starting off with an nmap scan to find that ports 21(FTP), 22(SSH), and 80(HTTP) are open.  

<img src="/assets/img/blog/bounty/nmap.png">

I can see that we do an anonymous login with FTP.  Starting there a simple ls -la reveals locks.txt and task.txt.  

<img src="/assets/img/blog/bounty/ftp.png">

I downloaded these to my attacking machine using wget and inspected the files.  The locks.txt appears to be a word list that will come in handy shortly.  The task.txt file contains a brief to-do list for lin.  Let's see what we can do with this new information ;)

<img src="/assets/img/blog/bounty/locks.png">

<img src="/assets/img/blog/bounty/task.png">

## What service can you bruteforce with the text file found?

Using hyrda we should be able to brute force our way onto ssh using our gathered credentials.

## What is the users password? 

<img src="/assets/img/blog/bounty/hydra.png">

Haza!  Now we can login as lin :D

<img src="/assets/img/blog/bounty/lin.png">

## user.txt

Now that we're logged in as lin you can cat the user.txt file in /Desktop.

<img src="/assets/img/blog/bounty/user.png">

## root.txt

Now we need to escelate our privelages.  Using sudo -l we can see lin's available privileges.  Lin can run tar with sudo, so I need to figure out how to use that to my advantage.  After some googling I came accross <a href="https://gtfobins.github.io/">GTFOBins</a>.  Absolutely going to bookmark this, as it contains a list of "living off the land" techniques that can be used.  Searching "tar" brings up a helpful binary that should help me escalate my privelages.  

<img src="/assets/img/blog/bounty/sudo.png">

<img src="/assets/img/blog/bounty/tar.png">

Running the command was a success!

<img src="/assets/img/blog/bounty/whoami.png">

After some digging around I found the root.txt file.

<img src="/assets/img/blog/bounty/flag.png">

And there we have it!  Another CTF in the books :)




