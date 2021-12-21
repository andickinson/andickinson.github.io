---
title:  "TryHackMe: Advent of Cyber - Day 20 - What's the Worst That Could Happen?"
date:   2021-12-21 08:00:00 +1000
excerpt: Learning about file forensics and virus identification.
---

This is a write up for the Day 20 - What's the Worst That Could Happen? challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### Open the terminal and navigate to the file on the desktop named 'testfile'. Using the 'strings' command, check the strings in the file. There is only a single line of output to the 'strings' command. What is the output?

<img src="{{ site.baseurl }}/assets/images/2021-12-21-advent-of-cyber-day-20/d20_01.jpg">

> Answer: **X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H\***

### Check the file type of 'testfile' using the 'file' command. What is the file type?

<img src="{{ site.baseurl }}/assets/images/2021-12-21-advent-of-cyber-day-20/d20_02.jpg">

> Answer: **EICAR virus test files**

### Calculate the file's hash and search for it on VirusTotal. When was the file first seen in the wild?

```
md5sum testfile
```

<img src="{{ site.baseurl }}/assets/images/2021-12-21-advent-of-cyber-day-20/d20_03.jpg">

Search the md5 hash on Virus Total. https://www.virustotal.com/gui/file/275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f/details

<img src="{{ site.baseurl }}/assets/images/2021-12-21-advent-of-cyber-day-20/d20_04.jpg">

> Answer: **2005-10-17 22:03:48**

### On VirusTotal's detection tab, what is the classification assigned to the file by Microsoft?

<img src="{{ site.baseurl }}/assets/images/2021-12-21-advent-of-cyber-day-20/d20_05.jpg">

> Answer: **Virus:DOS/EICAR_Test_File**

### Go to this link to learn more about this file and what it is used for. What were the first two names of this file?

<img src="{{ site.baseurl }}/assets/images/2021-12-21-advent-of-cyber-day-20/d20_06.jpg">

> Answer: **ducklin.htm or ducklin-html.htm**

### The file has 68 characters in the start known as the known string. It can be appended with whitespace characters upto a limited number of characters. What is the maximum number of total characters that can be in the file?

<img src="{{ site.baseurl }}/assets/images/2021-12-21-advent-of-cyber-day-20/d20_07.jpg">

> Answer: **128**

### Recap

In this task we learnt:
 * How to identify the file type of a file regardless of file extension
 * How to find strings in a file
 * How to calculate hash of a file
 * Using VirusTotal to perform preliminary analysis of a suspicious file