---
title:  "TryHackMe: Enumerating Telnet"
date:   2021-03-11 22:40:00 +1100
excerpt: Conucting a port scan with nmap and interpreting the results.
---

This is a write up for the **Enumerating Telnet** task of the [**Network Services**](https://tryhackme.com/room/networkservices) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

### How many ports are open on the target machine?

Run an nmap scan on the target machine as instructed.

```
nmap -A -p- <ip>
```

<img src="{{ site.baseurl }}/assets/images/2021-03-11-enumerating-telnet/01-nmap.jpg">

The result of the nmap scan shows that one port is open.

> Answer: **1**

### What port is this?

As per the above image, we can see that port 8012 is open.

> Answer: **8012**

### This port is unassigned, but still lists the protocol it's using, what protocol is this?

As per the above image, we can see that the open port is running over tcp.

> Answer: **tcp**

### Now re-run the nmap scan, without the -p- tag, how many ports show up as open?

Run the following nmap command as instructed, this will only scan 1000 common ports.

```
nmap -A <ip>
```

<img src="{{ site.baseurl }}/assets/images/2021-03-11-enumerating-telnet/02-nmap-2.jpg">

As port 8012 is not a commonly used port, it is not scanned and therefore no results are returned.

> Answer: **0**

### Based on the title returned to us, what do we think this port could be used for?

Referring back to the scan results, we can infer that this port could be used for a backdoor.

<img src="{{ site.baseurl }}/assets/images/2021-03-11-enumerating-telnet/03-backdoor.jpg">

> Answer: **A backdoor**

### Who could it belong to? Gathering possible usernames is an important step in enumeration.

Inferring from the previous image, we can assume that 'Skidy' is likely a username.

> Answer: **Skidy**

### Recap

In this task we learnt how to:
 * Conduct a port scan with **nmap** and interpreted the results