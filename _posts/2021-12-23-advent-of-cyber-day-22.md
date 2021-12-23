---
title:  "TryHackMe: Advent of Cyber - Day 22 - How It Happened"
date:   2021-12-23 08:00:00 +1000
excerpt: Learning about Encryption.
---

This is a write up for the Day 22 - How It Happened challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

Run the following command.

```
oledump.py -s 8 -d C:\Users\Administrator\Desktop\Santa_Claus_Naughty_List_2021\Santa_Claus_Naughty_List_2021.doc
```

This will reveal a base 64 encoded string.

<img src="{{ site.baseurl }}/assets/images/2021-12-23-advent-of-cyber-day-22/d22_01.jpg">

This then needs to be decoded in Cyber Chef as pictured below.

<img src="{{ site.baseurl }}/assets/images/2021-12-23-advent-of-cyber-day-22/d22_02.jpg">

### What is the username (email address of Grinch Enterprises) from the decoded script?

<img src="{{ site.baseurl }}/assets/images/2021-12-23-advent-of-cyber-day-22/d22_03.jpg">

> Answer: **Grinch.Enterprises.2021@gmail.com**

### What is the mailbox password you found?

<img src="{{ site.baseurl }}/assets/images/2021-12-23-advent-of-cyber-day-22/d22_04.jpg">

> Answer: **S@ntai$comingt0t0wn**

### What is the subject of the email?

<img src="{{ site.baseurl }}/assets/images/2021-12-23-advent-of-cyber-day-22/d22_05.jpg">

> Answer: **Christmas Wishlist**

### What port is the script using to exfiltrate data from the North Pole?

<img src="{{ site.baseurl }}/assets/images/2021-12-23-advent-of-cyber-day-22/d22_06.jpg">

> Answer: **587**

### What is the flag hidden found in the document that Grinch Enterprises left behind? (Hint: use the following command oledump.py -s {stream number} -d, the answer will be in the caption).

Run the following command.

```
oledump.py -s 7 -d C:\Users\Administrator\Desktop\Santa_Claus_Naughty_List_2021\Santa_Claus_Naughty_List_2021.doc
```

<img src="{{ site.baseurl }}/assets/images/2021-12-23-advent-of-cyber-day-22/d22_07.jpg">

> Answer: **YouFoundGrinchCookie**

### There is still a second flag somewhere... can you find it on the machine?

We know attachments are stored under `$env:USERPROFILE\Pictures\Grinch2021\`

<img src="{{ site.baseurl }}/assets/images/2021-12-23-advent-of-cyber-day-22/d22_08.jpg">

<img src="{{ site.baseurl }}/assets/images/2021-12-23-advent-of-cyber-day-22/d22_09.jpg">

> Answer: **S@nt@c1Au$IsrEAl**

### Recap

In this task we learnt:
 * How to decode strings with CyberChef
 * How to decode Base64
 * How to decode XOR strings
 * How to use oledump to extract data streams from files