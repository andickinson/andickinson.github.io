---
title:  "TryHackMe: Wireshark 101"
date:   2021-03-21 22:30:00 +1100
excerpt: Using Wireshark to analyze various protocols and PCAPs. 
---

This is a write up for the [**Wireshark 101**](https://tryhackme.com/room/wireshark) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

## ARP Traffic

### What is the Opcode for Packet 6?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/01-opcode.jpg">

> Answer: **request (1)**

### What is the source MAC Address of Packet 19?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/02-mac.jpg">

> Answer: **80:fb:06:f0:45:d7**

### What 4 packets are Reply packets?

Use the following filter to return only ARP Reply packets.

```
arp.opcode == 2
```

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/03-arp.jpg">

> Answer: **76,400,459,520**

### What IP Address is at 80:fb:06:f0:45:d7?

This information is available in the **info** column.

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/04-ip.jpg">

> Answer: **10.251.23.1**

<hr>

## ICMP Traffic

### What is the type for packet 4?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/05-type4.jpg">

> Answer: **8**

### What is the type for packet 5?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/06-type5.jpg">

> Answer: **0**

### What is the timestamp for packet 12, only including month day and year?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/07-date.jpg">

May 31, 2013 does not appear to work. As instructed, we try the day before and the answer is accepted.

> Answer: **May 30, 2013**

### What is the full data string for packet 18?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/08-data.jpg">

> Answer: **08090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f202122232425262728292a2b2c2d2e2f3031323334353637**

<hr>

## DNS Traffic

### What is being queried in packet 1?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/09-query.jpg">

> Answer: **8.8.8.8.in-addr.arpa**

### What site is being queried in packet 26?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/10-site.jpg">

> Answer: **www.wireshark.org**

### What is the Transaction ID for packet 26?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/11-transaction.jpg">

> Answer: **0x2c58**

<hr>

## HTTP Traffic

### What percent of packets originate from Domain Name System?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/12-dnspackets.jpg">

> Answer: **4.7**

### What endpoint ends in .237?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/13-ip.jpg">

> Answer: **145.254.160.237**

### What is the user-agent listed in packet 4?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/14-ua.jpg">

> Answer: **Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.6) Gecko/20040113**

### Looking at the data stream what is the full request URI from packet 18?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/15-uri.jpg">

> Answer: **http://pagead2.googlesyndication.com/pagead/ads?client=ca-pub-2309191948673629&random=1084443430285&lmt=1082467020&format=468x60_as&output=html&url=http%3A%2F%2Fwww.ethereal.com%2Fdownload.html&color_bg=FFFFFF&color_text=333333&color_link=000000&color_url=666633&color_border=666633**

### What domain name was requested from packet 38?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/16-domain.jpg">

> Answer: **www.ethereal.com**

### Looking at the data stream what is the full request URI from packet 38?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/17-uri.jpg">

> Answer: **http://www.ethereal.com/download.html**

<hr>

## HTTPS Traffic

### Looking at the data stream what is the full request URI for packet 31?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/18-uri.jpg">

> Answer: **https://localhost/icons/apache_pb.png**

### Looking at the data stream what is the full request URI for packet 50?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/19-uri.jpg">

> Answer: **https://localhost/icons/back.gif**

### What is the User-Agent listed in packet 50?

<img src="{{ site.baseurl }}/assets/images/2021-03-21-wireshark/20-ua.jpg">

> Answer: **Mozilla/5.0 (X11; U; Linux i686; fr; rv:1.8.0.2) Gecko/20060308 Firefox/1.5.0.2**

### Recap

In this task we learnt how to:
 * Use Wireshark to analyse ARP, ICMP, TCP, DNS, HTTP and HTTPS traffic