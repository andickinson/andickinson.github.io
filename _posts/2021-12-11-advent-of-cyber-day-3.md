---
title:  "TryHackMe: Advent of Cyber - Day 3 - Christmas Blackout"
date:   2021-12-11 16:30:00 +1000
excerpt: Learning Cookie Manipulation techniques. 
---

This is a write up for the Day 3 - Christmas Blackout challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### Using a common wordlist for discovering content, enumerate http://10.10.159.240 to find the location of the administrator dashboard. What is the name of the folder?

Run the following command in terminal.

```
dirb http://<ip> /usr/share/wordlist/dirb/common.txt
```

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-3/d3_1.jpg">

> Answer: **admin**

### In your web browser, try some default credentials on the newly discovered login form for the "administrator" user. What is the password?

Access the server's ip from the web browser.

```
http://<ip>/admin
```

Trying a common username/password such as:

```
administrator:administrator
```

> Answer: **administrator**

### Access the admin panel. What is the value of the flag?

Once logged in, we can see the flag.

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-3/d3_2.jpg">

> Answer: **THM{ADM1N_AC3SS}**

### Recap

In this task we learnt how to:
 * Use Dirbuster with word lists to find URLs
 