---
title:  "TryHackMe: Intro to ISAC"
date:   2021-06-02 23:00:00 +1000
excerpt: Learning how to utilize Information Sharing and Analysis Centers to gather threat intelligence and collect IOCs.
---

This is a write up for the **Investigation Scenarios** task of the [**Intro to ISAC**](https://tryhackme.com/room/introtoisac) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

### What is the name of the file from Scenario 1?

<img src="{{ site.baseurl }}/assets/images/2021-06-02-intro-to-isac/01-file.png">

> Answer: **29D6161522C7F7F21B35401907C702BDDB05ED47.bin**

### What is the size of the file from Scenario 1 in bytes?

<img src="{{ site.baseurl }}/assets/images/2021-06-02-intro-to-isac/02-size.png">

> Answer: **96,535**

### What is the size on disk of the file from Scenario 1 in bytes?

<img src="{{ site.baseurl }}/assets/images/2021-06-02-intro-to-isac/02-size.png">

> Answer: **98,304**

### What is the MD5 hash of the file from Scenario 1?

Open WinMD5 and select the Scenario 1 file.

<img src="{{ site.baseurl }}/assets/images/2021-06-02-intro-to-isac/03-md5.png">

> Answer: **8baa9b809b591a11af423824f4d9726a**

### What is the name of the file from Scenario 2?

<img src="{{ site.baseurl }}/assets/images/2021-06-02-intro-to-isac/04-cryptowall.png">

> Answer: **cryptowall.bin**

### What is the size of the file from Scenario 2 in bytes?

<img src="{{ site.baseurl }}/assets/images/2021-06-02-intro-to-isac/04-cryptowall.png">

> Answer: **246,272**

### What is the size on disk of the file from Scenario 2 in bytes?

<img src="{{ site.baseurl }}/assets/images/2021-06-02-intro-to-isac/04-cryptowall.png">

> Answer: **249,856**

### What is the MD5 hash of the file from Scenario 2?

Open WinMD5 and select the Scenario 2 file.

<img src="{{ site.baseurl }}/assets/images/2021-06-02-intro-to-isac/05-md5.png">

> Answer: **47363b94cee907e2b8926c1be61150c7**

### Recap

In this task we learnt how to:
 * Find file information in Windows
 * Use WinMD5 to generate hash values
 * Use IOCe to create IOCs
 * Use AlienVault to search for and identify existing threats
 