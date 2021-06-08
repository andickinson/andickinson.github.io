---
title:  "TryHackMe: Sysinternals"
date:   2021-06-08 16:00:00 +1000
excerpt: Learning to use the Sysinternals tools to analyze Window systems or applications. 
---

This is a write up for the [**Sysinternals**](https://tryhackme.com/room/btsysinternalssg) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

### There is a txt file on the desktop named file.txt. What is the text within the ADS?

<img src="{{ site.baseurl }}/assets/images/2021-06-08-sysinternals/01-ads.jpg">

> Answer: **I am hiding in the stream.**

### Using WHOIS tools, what is the ISP/Organization for the remote address in the screenshots above?

The command that should be executed is displayed below.

```
whois -v <ip>
```

However, the IP addresses listed in the room does not list any results. Given we are using Windows and the process is **svchost.exe** we can assume the answer is related to Microsoft.

> Answer: **Microsoft Corporation**

### Run Autoruns and inspect what are the new entries in the Image Hijacks tab compared to the screenshots above.

```
autoruns -accepteula
```

<img src="{{ site.baseurl }}/assets/images/2021-06-08-sysinternals/02-image-hijack.jpg">

### What entry was updated?

> Answer: **taskmgr.exe**

### What is the updated value?

> Answer: **c:\tools\sysint\procexp.exe**

### Run the Strings tool on ZoomIt.exe. What is the full path to the .pdb file?

```
strings .\ZoomIt.exe | findstr /i ZoomIt
```

<img src="{{ site.baseurl }}/assets/images/2021-06-08-sysinternals/03-zoomit.jpg">

> Answer: **C:\agent\_work\112\s\Win32\Release\ZoomIt64.pdb**

### Recap

In this task we learnt how to:
 * Use Sysinternals tools to find Windows system information
 