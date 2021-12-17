---
title:  "TryHackMe: Advent of Cyber - Day 9 - Where Is All This Data Going"
date:   2021-12-17 12:00:00 +1000
excerpt: Learning about basic packet analysis with Wireshark.
---

This is a write up for the Day 9 - Where Is All This Data Going challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### What operating system is Santa's laptop running ("OS Name")?

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-9/d9_01.jpg">

> Answer: **login**

### What is the username and password used in the login page in the HTTP #2 - POST section? 

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-9/d9_02.jpg">

> Answer: **McSkidy:Christmas2021!**

### What is the User-Agent's name that has been sent in HTTP #2 - POST section?

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-9/d9_03.jpg">

> Answer: **TryHackMe-UserAgent-THM{d8ab1be969825f2c5c937aec23d55bc9}**

### In the DNS section, there is a TXT DNS query. What is the flag in the message of that DNS query?

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-9/d9_04.jpg">

> Answer: **THM{dd63a80bf9fdd21aabbf70af7438c257}**

### In the FTP section, what is the FTP login password?

> Answer: **TryH@ckM3!**

### In the FTP section, what is the FTP command used to upload the secret.txt file?

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-9/d9_05.jpg">

> Answer: **STOR**

### In the FTP section, what is the content of the secret.txt file?

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-9/d9_06.jpg">

> Answer: **123^-^321**

### Recap

In this task we learnt:
 * Basic packet analysis with Wireshark
 