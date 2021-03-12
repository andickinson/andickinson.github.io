---
title:  "TryHackMe: Enumerating FTP"
date:   2021-03-12 23:30:00 +1100
excerpt: Using nmap to enumerate FTP.
---

This is a write up for the **Enumerating FTP** task of the [**Network Services**](https://tryhackme.com/room/networkservices) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

### How many ports are open on the target machine?

Run the following nmap command:

```
nmap -A -p- -v <ip>
```

<img src="{{ site.baseurl }}/assets/images/2021-03-13-enumerating-ftp/01-nmap.jpg">

In my tests the nmap scan only returns 1 open port, however the correct answer appears to be 2 in the TryHackMe lab.

> Answer: **1 or 2**

### What port is ftp running on?

> Answer: **21**

### What variant of FTP is running on it?

> Answer: **vsftpd**

### What is the name of the file in the anonymous FTP directory?

Attempt to connect to the FTP server by entering the following command and entering a username of 'anonymous'.

```
ftp <ip>
```

List out the files on the server with ```ls```

<img src="{{ site.baseurl }}/assets/images/2021-03-13-enumerating-ftp/02-ftp-ls.jpg">

> Answer: **PUBLIC_NOTICE.txt**

### What do we think a possible username could be?

Download the PUBLIC_NOTICE.txt file.

```
get PUBLIC_NOTICE.txt
```

<img src="{{ site.baseurl }}/assets/images/2021-03-13-enumerating-ftp/03-ftp-get.jpg">

Exit the FTP session and print out the contents of PUBLIC_NOTICE.txt.

<img src="{{ site.baseurl }}/assets/images/2021-03-13-enumerating-ftp/04-name.jpg">

> Answer: **mike**

### Recap

In this task we learnt how to:
 * Read nmap results
 * Connect to an anonymous session on an FTP server