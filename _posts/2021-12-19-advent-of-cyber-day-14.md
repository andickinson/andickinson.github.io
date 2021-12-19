---
title:  "TryHackMe: Advent of Cyber - Day 14 - Dev Insecure Ops"
date:   2021-12-19 08:00:00 +1000
excerpt: Learning about Exploiting CI/CD.
---

This is a write up for the Day 14 - Dev(Insecure)Ops challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### How many pages did the dirb scan find with its default wordlist?

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-14/d14_01.jpg">

> Answer: **4**

### How many scripts do you see in the /home/thegrinch/scripts folder?

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-14/d14_02.jpg">

> Answer: **4**

### What are the five characters following $6$G in pepper's password hash?

Edit the `loot.sh` file to print /etc/shadow.
Wait for CI/CD runner to update and refresh the page.

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-14/d14_03.jpg">

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-14/d14_04.jpg">

> Answer: **ZUP42**

### What is the content of the flag.txt file on the Grinch's user’s desktop?

Update the `loot.sh` file and print the contents of the `flag.txt` file.

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-14/d14_05.jpg">

> Answer: **DI3H4rdIsTheBestX-masMovie!**

### Recap

In this task we learnt:
 * CI/CD concepts
 * Risks associated with CI/CD
 * CI/CD exploitation vectors
 