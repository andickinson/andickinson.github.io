---
title:  "TryHackMe: Advent of Cyber - Day 13 - They Lost The Plan!"
date:   2021-12-18 13:30:00 +1000
excerpt: Learning about Windows Privilege Escalation.
---

This is a write up for the Day 13 - They Lost The Plan! challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### Complete the username: p.....

Open the Command Prompt and type `net users`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-13/d13_01.jpg">

> Answer: **pepper**

### What is the OS version?

Run `systeminfo`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-13/d13_02.jpg">

> Answer: **10.0.17763 N/A Build 17763**

### What backup service did you find running on the system?

Run `wmic service list | findstr "Backup"`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-13/d13_03.jpg">

> Answer: **IperiusSvc**

### What is the path of the executable for the backup service you have identified?

> Answer: **C:\Program Files (x86)\Iperius Backup\IperiusService.exe**

### Run the whoami command on the connection you have received on your attacking machine. What user do you have?

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-13/d13_04.jpg">

> Answer: **the-grinch-hack\thegrinch**

### What is the content of the flag.txt file?

Run `cd C:\Users\thegrinch\Documents`
Run `type flag.txt`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-13/d13_05.jpg">

> Answer: **THM-736635221**

### The Grinch forgot to delete a file where he kept notes about his schedule! Where can we find him at 5:30?

Run `type Schedule.txt`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-13/d13_06.jpg">

> Answer: **jazzercize**

### Recap

In this task we learnt:
 * How to conduct Windows Privilege Escalation
 