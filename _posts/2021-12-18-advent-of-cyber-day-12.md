---
title:  "TryHackMe: Advent of Cyber - Day 12 - Sharing Without Caring"
date:   2021-12-18 13:00:00 +1000
excerpt: Learning about nmap.
---

This is a write up for the Day 12 - Sharing Without Caring challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### Scan the target server with the IP 10.10.152.229. Remember that MS Windows hosts block pings by default, so we need to add -Pn, for example, nmap -Pn 10.10.152.229 for the scan to work correctly. How many TCP ports are open?

Run `nmap -Pn 10.10.152.229 -v`.

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-12/d12_01.jpg">

> Answer: **7**

### In the scan results you received earlier, you should be able to spot NFS or mountd, depending on whether you used the -sV option with Nmap or not. Which port is detected by Nmap as NFS or using the mountd service?

> Answer: **2049**

### How many shares did you find?

Run `showmount -e 10.10.152.229`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-12/d12_02.jpg">

> Answer: **4**

### How many shares show “everyone”?

> Answer: **3**

### What is the title of file 2680-0.txt?

Run `mount 10.10.152.229:/share tmp1`

There are two txt files in the folder.

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-12/d12_03.jpg">

Run `head 2680-0.txt`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-12/d12_04.jpg">

> Answer: **Meditations**

### It seems that Grinch Enterprises has forgotten their SSH keys on our system. One of the shares contains a private key used for SSH authentication (id_rsa). What is the name of the share?

Run `mount 10.10.152.229:/confidential tmp2`

You can see the ssh folder inside this directory.

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-12/d12_05.jpg">

> Answer: **confidential**

### We can calculate the MD5 sum of a file using md5sum FILENAME. What is the MD5 sum of id_rsa?

Run `md5sum id_rsa`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-12/d12_06.jpg">

> Answer: **3e2d315a38f377f304f5598dc2f044de**

### Recap

In this task we learnt:
 * More about nmap
 * Investigating NFS
 