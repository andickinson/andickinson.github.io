---
title:  "TryHackMe: Advent of Cyber - Day 1 - Save the Gifts"
date:   2021-06-08 16:00:00 +1000
excerpt: Learning to exploit Indirect Direct Object Reference vulnerabilities. 
---

This is a write up for the Day 1 - Save the Gifts challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### After finding Santa's account, what is their position in the company?

Santa is important, so lets assume his user_id=1.

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-1/d1.jpg">

> Answer: **The Boss!**

### After finding McStocker's account, what is their position in the company?

Increment user_id until McStocker is found.

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-1/d1_2.jpg">

> Answer: **Build Manager**

### After finding the account responsible for tampering, what is their position in the company?

Increment user_id until Grinch is found.

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-1/d1_3.jpg">

> Answer: **Mischief Manager**

### What is the received flag when McSkidy fixes the Inventory Management System?

Click 'Revert' on all entries under Grinch and the flag will appear.

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-1/d1_4.jpg">

> Answer: **THM{AOC_IDOR_2B34BHI3}**

### Recap

In this task we learnt how to:
 * Exploit Indirect Direct Object Reference vulnerabilities
 