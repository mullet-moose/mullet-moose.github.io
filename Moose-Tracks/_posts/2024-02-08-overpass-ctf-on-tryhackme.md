---
layout: post
title: Overpass CTF Write-Up
image: /assets/img/blog/overpass/lock.webp
accent_image: 
  background: url('/assets/img/blog/overpass/lock.webp') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Can we hack a password manager?  I think we can!
invert_sidebar: false
---
# Overpass CTF Write-Up

Mullet-Moose attempts to hack into a password manager on this room by TryHackMe.

Want to follow along?  <a href="https://tryhackme.com/room/overpass">Overpass</a>

* toc
{:toc}

## Hack the machine and get the flag in user.txt

Starting off with an nmap scan which reveals that ports 22(SSH) and 80(HTTP) are open.  Also worth noting the hint that THM gives us for this first question: "OWASP Top 10 Vuln! Do NOT bruteforce."

<img src="/assets/img/blog/overpass/nmap.png">

Navigating to the webpage gives us a little more information on what "Overpass" is.  Viewing the source code also reveals a clue via the comment: "Yeah right, just because the Romans used it doesn't make it military grade, change this?"

<img src="/assets/img/blog/overpass/source1.png">

Hmm....Roman Cryptgraphy eh?  Sounds like the Ceasar Cipher to me!

Next I used gobuster to do a little more enumerating.  This gives us an admin login page and a few other things to explore.  

<img src="/assets/img/blog/overpass/gobuster.png">

<img src="/assets/img/blog/overpass/admin.png">

The about us page includes a staff list.  Taking note of this as they might be potential usernames for later!

<img src="/assets/img/blog/overpass/aboutus.png">

Back to our admin page...we need to figure out a way to bypass.  I intercepted a login request with Burp and messed around with a few different forward requests with not much success.  Before trying again I peeked at the source code of the admin page to see if there was any other information I could use.  There is a reference to login.js, and reviewing that code gave me my next step.  

<img src="/assets/img/blog/overpass/source2.png">

In that screenshot you can see the if statement that handles the successful/unsuccessful login request.  If the credentials provided are correct, window.location = "/admin".  Amending this in another Burp interception allows us to bypass the login page.  Once you've captured a login request, right click and select "Do intercept -> response to this request."  Remove the "incorrect credentials" line, add "location: /admin", and change line 1 to show "302 FOUND."  Now we have a hepful note from Paradox and a fancy ssh key!

<img src="/assets/img/blog/overpass/burp1.png">

<img src="/assets/img/blog/overpass/burp2.png">

<img src="/assets/img/blog/overpass/admin2.png">

I saved this key to a file on my desktop, and proceeded to use ssh2john to generate a hash of our private key.

<img src="/assets/img/blog/overpass/ssh2john.png">

We'll save this hash to a new document, and use john the ripper to crack!

<img src="/assets/img/blog/overpass/john.png">

Sick.  Now we can use these credentials to login as james via ssh.  Do note, you may need to adjust the privelages for that key file to avoid ssh ignoring the request.  To do so simple chmod 600 key.txt.

Once you're in you can cat the user.txt file and get the first flag!

<img src="/assets/img/blog/overpass/ssh.png">

## Escalate your privileges and get the flag in root.txt

Now we need to escalate our privelages so we can get the root flag.  First, lets see what's in that todo.txt file.

<img src="/assets/img/blog/overpass/todo.png">

And we can see if there are any interesting hidden files with ls -la.  There is a .overpass file, which includes some ciphertext.  Remembering that this is "Roman Military Cryptogrpahy" I decided to try and decode it via Ceaser Cipher (ROT47).  This reveals: 

	{"name":"System","pass":"saydrawnlyingpicture"}
	
Helpful...but where can we use this?  Lets see if linpeas can locate a path to escalation for us!  Once you have the linpeas.sh on your local machine, you can set up an http server with python using "python3 -m http.server" and curl the file from the victim machine.

In the cron jobs section we can see that there's a job that runs every minute as root.  Let's use this to our advantage!

<img src="/assets/img/blog/overpass/peas.png">

My thought here was that every minute there's a curl request for buildscript.sh, so if we can create a malicious buildscript.sh to be curled instead we should be able to get root access.  I used nano to edit /etc/hosts and changed the "overpass.thm" ip to my own.  

Next, we need to duplicate that same file path on our local machine.  I simply created an "src" directory in my own Downlads folder and created the malicious buildscript.sh.

<img src="/assets/img/blog/overpass/nano.png">

<img src="/assets/img/blog/overpass/build.png">

Last we need to use netcat to set up a listener, so that when curl gets called by the cron job it can access the malicious buildscript.sh.  Once this has all been completed, open up the listener and enjoy a cup of coffee while you wait :)

<img src="/assets/img/blog/overpass/root.png">

And now we can cat our root flag!

<img src="/assets/img/blog/overpass/rootflag.png">

Overall a pretty fun room, and not too hard.  I personally enjoy opportunities to use linpeas!
