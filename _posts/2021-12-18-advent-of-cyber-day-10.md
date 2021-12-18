---
title:  "TryHackMe: Advent of Cyber - Day 10 - Offensive Is The Best Defence"
date:   2021-12-18 12:00:00 +1000
excerpt: Learning about nmap.
---

This is a write up for the Day 9 - Day 10 - Offensive Is The Best Defence challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### Help McSkidy and run nmap -sT 10.10.175.143. How many ports are open between 1 and 100?

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-10/d10_01.jpg">

> Answer: **2**

### What is the smallest port number that is open?

> Answer: **22**

### What is the service related to the highest port number you found in the first question?

> Answer: **http**

### Now run nmap -sS 10.10.175.143. Did you get the same results? (Y/N)

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-10/d10_02.jpg">

> Answer: **Y**

### If you want Nmap to detect the version info of the services installed, you can use nmap -sV 10.10.175.143. What is the version number of the web server?

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-10/d10_03.jpg">

> Answer: **Apache httpd 2.4.49**

### By checking the vulnerabilities related to the installed web server, you learn that there is a critical vulnerability that allows path traversal and remote code execution. Now you can tell McSkidy that Grinch Enterprises used this vulnerability. What is the CVE number of the vulnerability that was solved in version 2.4.51?

The CVE is stated on https://httpd.apache.org/security/vulnerabilities_24.html

> Answer: **CVE-2021-42013**

### You are putting the pieces together and have a good idea of how your web server was exploited. McSkidy is suspicious that the attacker might have installed a backdoor. She asks you to check if there is some service listening on an uncommon port, i.e. outside the 1000 common ports that Nmap scans by default. She explains that adding -p1-65535 or -p- will scan all 65,535 TCP ports instead of only scanning the 1000 most common ports. What is the port number that appeared in the results now?

The Attack Box was too slow to run such a large query, so a Kali VM was used.

```
nmap -sT 10.10.175.143 -p- -v
```

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-10/d10_04.jpg">

> Answer: **20212**

### What is the name of the program listening on the newly discovered port?

For some reason my Kali VM was not returning the service name. I had to switch back to the Attack Box to get the answer.

<img src="{{ site.baseurl }}/assets/images/2021-12-18-advent-of-cyber-day-10/d10_05.jpg">

> Answer: **telnetd**

### Recap

In this task we learnt:
 * How nmap works
 * How to conduct port scans
 