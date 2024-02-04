---
layout: post
title: Exploring RouterOS on MikroTik hEX
image: /assets/img/blog/motherboard.webp
accent_image: 
  background: url('/assets/img/blog/motherboard.webp') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Join me as I venture through the capabilites of MikroTik's RouterOS!
invert_sidebar: false
---

# Exploring RouterOS on MikroTik hEX

Mullet-Moose here, and today I’ll be playing around with my new Mikrotik hEX router.  This was a Christmas gift from one of my best friends and I’ve been eager to learn more about all the bells and whistles that MikroTik has to offer.  In this post I’ll give a brief overview of some of the different features available in RouterOS and how those features might be integrated into my own network.  I'll be using MikroTik's <a href="https://help.mikrotik.com/docs/display/ROS/RouterOS">RouterOS Documentation</a> as a guide.  Feel free to follow along :)


Without further ado…let’s dive in!

* toc
{:toc}


## MikroTik hEX
Mikrotik remains popular in the marketplace because of their competitive prices and the impressive capabilities of their devices.  The hEX model boasts a dual core 880MHz CPU, 256MB RAM, 16MB storage, and 5x Gigabit Ethernet ports.  It also supports PoE and includes a USB port and microSD slot.  On top of that, RouterOS has an array of advanced features and configurations. The physical design of the hEX is sleek and simple; big things come in small packages they say. 


## Set Up
Set-up was easy and straightforward (almost plug and play!).  Previously we were using a consumer-grade NETGEAR Orbi as our router with two additional satellites.  Of course, we still wanted to take advantage of the mesh coverage, so Orbi was put into AP mode.  The hEX now serves as our primary router.  As is tradition, while playing around with some settings during the initial set up, I managed to completely lock myself of the network.  Luckily, resetting the configuration on the hEX was simple (holding down the reset button for a few seconds) and I was back in a matter of minutes.  Alternatively, for situations such as these, RouterOS supports a small utility known as Winbox, which can connect to the admin console via MAC address.  
A word to the wise for anyone considering one of the baby’s…the default configurations are NOT secure.  Taking some time to go through and do some hardening is highly advised.  More on that to come in a later post!



## CAPsMAN
CAPsMAN (Controlled Access Point System Manager) is a MikroTik application on RouterOS that allows for centralized management of one or more MikroTik AP devices.  Specifically, a ‘system manager’ can manage AP configurations, authentication, and even data forwarding.  Honestly, for how inexpensive these devices are, this appears to be a very robust feature that would prove useful in SMB or larger home networks.  This won’t be a feature I’ll be utilizing in my home lab at the moment, as I don’t have any compatible APs, but may be something to look into for the future 😊


## Wireless
The MikroTik hEX does not include a built-in wireless interface, so I won’t spend too much time here.  Notable features that can be seen in RouterOS include a wireless sniffer and snooper, repeater, and WPS client/server.  There is also support for MikroTik’s proprietary nstreme protocol, which utilizes a pair of wireless cards to improve point-to-point links.  


## Interfaces
Lots of interesting things in the Interfaces tab.  EoIP (Ethernet over IP) Tunneling is worth a mention.  This protocol builds an Ethernet tunnel over an IP connection between routers.   Basically, this is a fairly simple way to bridge together LAN’s over the internet or via encrypted tunnels.  RouterOS also supports GRE tunneling, VLANs, and VRRP.  VRRP (Virtual Router Redundancy Protocol) was new to me.  It essentially combines routers into a Virtual Router group, which can assist in reducing the overhead caused by the detection of unreachable routers.  Cool stuff!


## Tunneling
Moving right along are the tunneling capabilities of RouterOS.  There is support for PPP, PPPoE, PPTP, SSTP, L2TP, and OVPN.  At the risk of getting “tunnel vision” (Aha!), I won’t spend too much time on this.  Just know that PPTP is no longer considered secure!


## HWMP+ (Mesh)
Now this is something I really wanted to investigate more, considering our wireless mesh network here at home.  Based on HWMP (Hybrid Wireless Mesh Protocol), HWMP+ (Mesh) is an alternative for (Rapid) STP in mesh networks that eliminates loops and optimizes routing.  Also worth noting is that HWMP+ supports WDS and Ethernet interfaces within the mesh.  Additionally, there is a Mesh traceroute command that assists in identifying routing paths within the network.  Alas, my research did reveal that this feature is only capable with other MikroTik devices.  Still neat to know that it’s there!


## IP
The IP tab includes most of the “standard” settings we expect to see in most routers.  This includes DHCP, DNS, Firewall, SMB, SNMP, SSH, etc.  We’ll explore more on this in my next post where we’ll delve into hardening techniques and configurations for the hEX.

## MPLS
A protocol I’m not terribly familiar with.  According to MikroTik’s <a href="https://help.mikrotik.com/docs/display/ROS/Mpls+Overview">documentation</a>:

	“MPLS stands for MultiProtocol Label Switching. It kind of replaces IP routing - packet forwarding decision (outgoing interface and next-hop router) is no longer based on fields in IP header (usually destination address) and routing table, but on labels that are attached to packet. This approach speeds up the forwarding process because next-hop lookup becomes very simple compared to routing lookup (finding the longest matching prefix).”

Also worth mentioning:

	“The efficiency of the forwarding process is the main benefit of MPLS, but it must be taken into account that MPLS forwarding disables the processing of network layer (e.g. IP) headers, therefore no network layer-based actions like NAT and filtering can be applied to MPLS forwarded packets."

## Routing
In the routing tab we find various options including BFD and BGP.  BFD (Bidirectional Forwarding Detection) is used to identify faults between forwarding engines.  Simply, it checks whether a neighbor is reachable or not.  BGP (Border Gateway Protocol) enhances dynamic routing by automatically updating routing tables in the event of a network topology change.

## RADIUS
This is something I will be messing with more in the future.  RouterOS includes a RADIUS client to enhance it’s AAA functionality.   Support for RADIUS authentication extends to the aforementioned tunneling protocols and utilizes the User and Profile databases.  

## Tools
Last but not least, there are an array of tools RouterOS has to offer.  These cover a wide range of capabilities including email servers, MAC servers, packet sniffers, SMS, and traffic monitoring.  Honestly, I prefer using other tools like Wireshark, but it is really impressive to see that these are included with such an inexpensive device.  

## Conclusion
That wraps up our brief exploration of RouterOS.  It’s apparent that MikroTik delivers a huge span of functionality with RouterOS, and the hEX is a welcome addition to my network.  There is still a lot more to learn about all it’s capabilities but so far the journey has been fun and easy!


*[SERP]: Search Engine Results Page
