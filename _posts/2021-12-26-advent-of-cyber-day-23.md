---
title:  "TryHackMe: Advent of Cyber - Day 23 - PowershELlF"
date:   2021-12-26 08:00:00 +1000
excerpt: Learning about Powershell.
---

This is a write up for the Day 23 - PowershELlF challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### What command was executed as Elf McNealy to add a new user to the machine?

<img src="{{ site.baseurl }}/assets/images/2021-12-26-advent-of-cyber-day-23/d23_01.jpg">

> Answer: **Invoke-Nightmare**

### What user executed the PowerShell file to send the password.txt file from the administrator's desktop to a remote server?

<img src="{{ site.baseurl }}/assets/images/2021-12-26-advent-of-cyber-day-23/d23_02.jpg">

> Answer: **adm1n**

### What was the IP address of the remote server? What was the port used for the remote connection? (format: IP,Port)

<img src="{{ site.baseurl }}/assets/images/2021-12-26-advent-of-cyber-day-23/d23_03.jpg">

> Answer: **10.10.148.96,4321**

### What was the encryption key used to encrypt the contents of the text file sent to the remote server?

<img src="{{ site.baseurl }}/assets/images/2021-12-26-advent-of-cyber-day-23/d23_04.jpg">

> Answer: **j3pn50vkw21hhurbqmxjlpmo9doiukyb**

### What application was used to delete the password.txt file?

<img src="{{ site.baseurl }}/assets/images/2021-12-26-advent-of-cyber-day-23/d23_05.jpg">

> Answer: **sdelete.exe**

### What is the date and timestamp the logs show that password.txt was deleted? (format: MM/DD/YYYY H:MM:SS PM)

<img src="{{ site.baseurl }}/assets/images/2021-12-26-advent-of-cyber-day-23/d23_06.jpg">

> Answer: **11/11/2021 7:29:27 PM**

### What were the contents of the deleted password.txt file?

<img src="{{ site.baseurl }}/assets/images/2021-12-26-advent-of-cyber-day-23/d23_07.jpg">

> Answer: **Mission Control: letitsnowletitsnowletitsnow**

### Recap

In this task we learnt:
 * How to analyze Windows event logs to understand actions performed in an attack.
 * How to recover key artifacts in unencrypted web communications. 
 * How to utilize PowerShell Scripting to recover a delete artifact. 
