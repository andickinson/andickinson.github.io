---
title:  "TryHackMe: Advent of Cyber - Day 16 - Ransomware Madness"
date:   2021-12-19 08:30:00 +1000
excerpt: Learning about Exploiting CI/CD.
---

This is a write up for the Day 16 - Ransomware Madness challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-16/d16_01.jpg">

### What is the operator's username?

From the Russian translation we can see the username.

> Answer: **GrinchWho31**

### What social media platform is the username associated with?

Using a username checker online we can see that the account likely belongs to Twitter.

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-16/d16_02.jpg">

> Answer: **Twitter**

### What is the cryptographic identifier associated with the operator?

The Grinch posted the identifier in a Twitter post here: https://twitter.com/GrinchWho31/status/1460683925836152843

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-16/d16_03.jpg">

> Answer: **1GW8QR7CWW3cpvVPGMCF5tZz4j96ncEgrVaR/**

### What platform is the cryptographic identifier associated with?

The platform is also referenced in the Twitter post.

> Answer: **keybase.io**

### What is the bitcoin address of the operator?

They bitcoin address is available on the keybase.io page here: https://keybase.io/grinchwho31/sigs/1GW8QR7CWW3cpvVPGMCF5tZz4j96ncEgrVaR

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-16/d16_04.jpg">

> Answer: **bc1q5q2w2x6yka5gchr89988p2c8w8nquem6tndw2f**

### What platform does the operator leak the bitcoin address on? 

The Bitcoin address is referenced in a *.cpp file on GitHub here: https://github.com/ChristmasHater31/Christmas-Stealer/blob/main/ransom.cpp#L6

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-16/d16_05.jpg">

> Answer: **GitHub**

### What is the operator's personal email?

This is also available on a GitHub repository here: https://github.com/ChristmasHater31/ChristBASHTree/commit/51b5bb9afc4563b791119a3f7942a3edec74b6b1#diff-93bdbed0b2e86eac9acbb6055efa34dfbb57341146daa9c58ad65ae72cb2d25eR72

> Answer: **DonteHeath21@gmail.com**

### What is the operator's real name?

We can extrapolate the operator's real name from the email address.

> Answer: **Donte Heath**

### Recap

In this task we learnt:
 * What OSINT is and where it originates
 * Tthe implications of OSINT and how it can be used for reconnaissance and information gathering
 * How to conduct an OSINT investigation to gather information on an individual
 