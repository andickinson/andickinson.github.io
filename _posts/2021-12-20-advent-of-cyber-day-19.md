---
title:  "TryHackMe: Advent of Cyber - Day 19 - Something Phishy Is Going On"
date:   2021-12-20 08:00:00 +1000
excerpt: Learning about Phishing.
---

This is a write up for the Day 19 - Something Phishy Is Going On challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### Who was the email sent to? (Answer is the email address)

<img src="{{ site.baseurl }}/assets/images/2021-12-20-advent-of-cyber-day-19/d19_01.jpg">

> Answer: **elfmcphearson@tbfc.com**

### Phishing emails use similar domains of their targets to increase the likelihood the recipient will be tricked into interacting with the email. Who does it say the email was from? (Answer is the email address)

<img src="{{ site.baseurl }}/assets/images/2021-12-20-advent-of-cyber-day-19/d19_02.jpg">

> Answer: **customerservice@t8fc.info**

### Sometimes phishing emails have a different reply-to email address. If this email was replied to, what email address will receive the email response?

<img src="{{ site.baseurl }}/assets/images/2021-12-20-advent-of-cyber-day-19/d19_03.jpg">

> Answer: **fisher@tempmailz.grinch**

### Less sophisticated phishing emails will have typos. What is the misspelled word?

<img src="{{ site.baseurl }}/assets/images/2021-12-20-advent-of-cyber-day-19/d19_04.jpg">

> Answer: **stright**

### The email contains a link that will redirect the recipient to a fraudulent website in an effort to collect credentials. What is the link to the credential harvesting website?

We can decode the base64 email message with CyberChef.

<img src="{{ site.baseurl }}/assets/images/2021-12-20-advent-of-cyber-day-19/d19_05.jpg">

<img src="{{ site.baseurl }}/assets/images/2021-12-20-advent-of-cyber-day-19/d19_06.jpg">

> Answer: **https://89xgwsnmo5.grinch/out/fishing/**

### View the email source code. There is an unusual email header. What is the header and its value?

<img src="{{ site.baseurl }}/assets/images/2021-12-20-advent-of-cyber-day-19/d19_07.jpg">

> Answer: **X-GrinchPhish: >;^)**

### You received other reports of phishing attempts from other colleagues. Some of the other emails contained attachments. Open attachment.txt. What is the name of the attachment?

`head attachment.txt`

<img src="{{ site.baseurl }}/assets/images/2021-12-20-advent-of-cyber-day-19/d19_08.jpg">

> Answer: **password-reset-instructions.pdf**

### password-reset-instructions.pdf

`mcskidy@elfmode$ cat attachment-base64-only.txt | base64 -d > file.pdf` will decode the output and create a PDF.

Opening the PDF reveals the flag.

<img src="{{ site.baseurl }}/assets/images/2021-12-20-advent-of-cyber-day-19/d19_09.jpg">

> Answer: **THM{A0C_Thr33_Ph1sh1ng_An4lys!s}**

### Recap

In this task we learnt:
 * About Phishing and investigating Email Headers
 * Reconstructing base64 encoded artifacts