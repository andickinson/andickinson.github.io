---
title:  "TryHackMe: Advent of Cyber - Day 2 - Elf HR Problems"
date:   2021-12-10 16:30:00 +1000
excerpt: Learning Cookie Manipulation techniques. 
---

This is a write up for the Day 2 - Elf HR Problems challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### What is the name of the new cookie that was created for your account?

Attempt to create a new account. You will see an "error" message as per below.

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-2/d2_1.jpg">

Looking at browser Cookies you will see the user-auth object.

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-2/d2_2.jpg">

> Answer: **user-auth**

### What encoding type was used for the cookie value?

Putting the cookie value in [CyberChef](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')&input=N2I2MzZmNmQ3MDYxNmU3OTNhMjAyMjU0Njg2NTIwNDI2NTczNzQyMDQ2NjU3Mzc0Njk3NjYxNmMyMDQzNmY2ZDcwNjE2ZTc5MjIyYzIwNjk3MzcyNjU2NzY5NzM3NDY1NzI2NTY0M2EyMjU0NzI3NTY1MjIyYzIwNzU3MzY1NzI2ZTYxNmQ2NTNhMjI3NDY1NzM3NDIyN2Q) shows the content is encoded as Hex.

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-2/d2_3.jpg">

> Answer: **Hexadecimal**

### What object format is the data of the cookie stored in?

The data is stored as JSON.

```
{company: "The Best Festival Company", isregistered:"True", username:"test"}
```

> Answer: **JSON**

### What is the value of the administrator cookie? (username = admin)

Reverse the formula in CyberChef and update username to "admin".

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-2/d2_4.jpg">

> Answer: **7b636f6d70616e793a2022546865204265737420466573746976616c20436f6d70616e79222c206973726567697374657265643a2254727565222c20757365726e616d653a2261646d696e227d**

### What team environment is not responding?

Update the cookie in developer tools and refresh the page.

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-2/d2_5.jpg">

> Answer: **HR**

### What team environment has a network warning?

<img src="{{ site.baseurl }}/assets/images/2021-12-10-advent-of-cyber-day-2/d2_5.jpg">

> Answer: **Application**

### Recap

In this task we learnt how to:
 * Decode cookies and manipulate them
 * Bypass authentication
 