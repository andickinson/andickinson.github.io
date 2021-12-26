---
title:  "TryHackMe: Advent of Cyber - Day 24 - Learning From The Grinch"
date:   2021-12-26 08:30:00 +1000
excerpt: Learning about post exploitation and cracking passwords.
---

This is a write up for the Day 24 - Learning From The Grinch challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### What is the username of the other user on the system?

<img src="{{ site.baseurl }}/assets/images/2021-12-26-advent-of-cyber-day-24/d24_01.jpg">

> Answer: **emily**

### What is the NTLM hash of this user?

<img src="{{ site.baseurl }}/assets/images/2021-12-26-advent-of-cyber-day-24/d24_02.jpg">

> Answer: **8af326aa4850225b75c592d4ce19ccf5**

### What is the password for this user?

<img src="{{ site.baseurl }}/assets/images/2021-12-26-advent-of-cyber-day-24/d24_02.jpg">

> Answer: **1234567890**

### Recap

In this task we learnt:
 * Understand post exploitation
 * Understand how passwords are stored on Windows
 * Dump passwords from LSASS process on Windows
 * Crack Password Hashes