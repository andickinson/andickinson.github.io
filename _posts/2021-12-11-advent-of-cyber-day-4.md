---
title:  "TryHackMe: Advent of Cyber - Day 4 - Santa's Running Behind"
date:   2021-12-11 17:00:00 +1000
excerpt: Learning about fuzzing and Burp Suite. 
---

This is a write up for the Day 4 - Santa's Running Behind challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### What valid password can you use to access the "santa" account?

<img src="{{ site.baseurl }}/assets/images/2021-12-11-advent-of-cyber-day-4/d4_1.jpg">

The entry that returned Status 302 and a different length will be the password we are looking for.

> Answer: **cookie**

### What is the flag in Santa's itinerary?

Logging in as Santa reveals the answer.

<img src="{{ site.baseurl }}/assets/images/2021-12-11-advent-of-cyber-day-4/d4_2.jpg">

> Answer: **THM{SANTA_DELIVERS}**

### Recap

In this task we learnt how to:
 * Understanding authentication and where it is used
 * Understanding what fuzzing is
 * Understanding what Burp Suite is and how we can use it for fuzzing a login form to gain access
 