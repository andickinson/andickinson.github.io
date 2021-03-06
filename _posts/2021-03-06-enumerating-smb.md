---
title:  "TryHackMe: Enumerating SMB"
date:   2021-03-06 18:20:00 +1100
excerpt: Conucting a port scan and enumerating SMB.
---

This is a write up for the **Enumerating SMB** task of the [**Network Services**](https://tryhackme.com/room/networkservices) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

### Conduct an nmap scan of your choosing, How many ports are open?

TryHackMe suggests conducting a scan with the -A and -p- tags where:
 * **-A**: Enables OS Detection, Version Detection, Script Scanning and Traceroute all in one
 * **-p-**: Enables scanning across all ports, not just the top 1000

```
nmap -A -p- <ip>
```

Scanning every port can be a very time consuming process, so in this case lets add a couple more flags:
 * **-T4**: Set speed of the scan to 4 (range from T0 to T5). Increasing this number may increase the possibility of being detected by the client
 * **-v**: Basic verbosity. This will display the ports as they are found

 More information on **nmap** flags can be found [here](https://nmap.org/book/port-scanning-options.html).

This gives us the following command:

```
nmap -A -p- -T4 -v <ip>
```

As the scan is running we notice that 3 open ports are returned early on.

<img src="{{ site.baseurl }}/assets/images/2021-03-06-enumerating-smb/01-nmap-scan.jpg">

This provides us with the correct result:

> Answer: **3**

***

### What ports is SMB running on?

Referring to the [Samba documentation](https://www.samba.org/~tpot/articles/firewall.html) we know that the default ports for SMB are **139** and **445**.
This also correlates with what we found in our scan (image above).

> Answer: ***139/445***

***

### Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the workgroup name?

Run the requested command:

```
enum4linux -A <ip>
```

The workgroup name is listed under the **Enumerating Workgroup/Domain** section.

<img src="{{ site.baseurl }}/assets/images/2021-03-06-enumerating-smb/02-enum4linux-workgroup.jpg">

> Answer: **WORKGROUP**

***

### What comes up as the name of the machine?

The name of the machine is listed under the **OS Information** section.

<img src="{{ site.baseurl }}/assets/images/2021-03-06-enumerating-smb/03-enum4linux-name.jpg">

> Answer: **POLOSMB**

***

### What operating system version is running?

The OS version is also defined under the same section.

> Answer: **6.1**

***

### What share sticks out as something we might want to investigate?

Under the **Share Enumeration** section we note that the profiles section would be worth investigating further.

<img src="{{ site.baseurl }}/assets/images/2021-03-06-enumerating-smb/04-enum4linux-profiles.jpg">

> Answer: **profiles**

***

### Recap

In this task we learnt how to:
 * Conduct a port scan with **nmap**
 * Enumerate SMB with **enum4linux**