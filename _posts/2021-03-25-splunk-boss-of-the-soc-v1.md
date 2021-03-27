---
title:  "TryHackMe: Splunk - Boss of the SOC v1"
date:   2021-03-25 20:30:00 +1100
excerpt: BOTS is a hands-on, self-paced, blue-team exercise that uses Splunk to defeat threats. 
---

This is a write up for the **Advanced Persistent Threat** and **Ransomware** tasks of the [**Splunk**](https://tryhackme.com/room/bpsplunk) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

## Advanced Persistent Threat

### What IP is scanning our web server?

Navigate to http://10.10.29.30:8000 and then click on **Investigating with Splunk Workshop**.

We know:
 * We have a compromised website: imreallynotbatman.com
 * An index called: botsv1

Lets start with a basic search:

```
index=botsv1 imreallynotbatman.com
```

This provides ~80,0000 results.

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/01-basic-query.jpg">

Something that is scanning our webserver is likely to be via HTTP, so lets set sourcetype to **stream:http**.

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http"
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/02-source.jpg">

Lets see how many different ip addresses we are dealing with.

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" | stats count by src_ip
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/03-ip.jpg">

We can assume that due to the volume of traffic, this source ip is scanning our server.

> Answer: **40.80.148.42**

### What web scanner scanned the server?

Looking at some of the traffic from 40.80.148.42, we can see it is running Acunetix - a vulnerability scanner.

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/04-acunetix.jpg">

> Answer: **Acunetix**

### What is the IP address of our web server?

The requests from 40.80.148.42 are targetting 192.168.250.70

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" src_ip="40.80.148.42" | stats count by dest_ip
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/05-dest.jpg">

> Answer: **192.168.250.70**

### What content management system is imreallynotbatman.com using?

Looking at the dest_headers we can see that Joomla is likely to be the CMS in use.

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" src_ip="40.80.148.42" dest_ip="192.168.250.70" | top limit=20 dest_headers
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/06-joomla.jpg">

> Answer: **Joomla**

### What address is performing the brute-forcing attack against our website?

A brute force attack is against some form of authentication. This will likely require GET/POST requests.

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" dest_ip="192.168.250.70" | stats count by http_method
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/07-http.jpg">

Looking at the http_content for a request shows that the password field is called **passwd**.

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/08-passwd.jpg">

Refining our search further shows how many requests are coming from each ip.

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" dest_ip="192.168.250.70" http_method="POST" username passwd | stats count by src_ip
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/09-ip.jpg">

Listing **form_data** shows a brute force attempt on the **admin** user.

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" src_ip="23.22.63.114" dest_ip="192.168.250.70" http_method="POST" username passwd | top limit=20 form_data
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/10-brute.jpg">

> Answer: **23.22.63.114**

### What was the first password attempted in the attack?

The earliest entry will be at the **tail**.

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" src_ip="23.22.63.114" dest_ip="192.168.250.70" http_method="POST" username passwd | tail 1
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/11-pass.jpg">

> Answer: **12345678**

### One of the passwords in the brute force attack is James Brodsky's favorite Coldplay song. Which six character song is it?

This is an interesting query as we need to separate the passwords from the form_data.

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" src_ip="23.22.63.114" dest_ip="192.168.250.70" http_method="POST" username passwd 
| table form_data
| rex field=form_data "passwd=(?<passwd>\w+)" 
| table passwd 
| regex passwd= \w{6}
```

There is still 343 possibilities, sorting alphabetically reveals the answer.

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/12-yellow.png">

> Answer: **yellow**

### What was the correct password for admin access to the content management system running imreallynotbatman.com?

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" dest_ip="192.168.250.70" http_method="POST" username passwd 
| rex field=form_data "passwd=(?<passwd>\w+)" 
| stats count by passwd
| where count>1
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/13-batman.png">

> Answer: **batman**

### What was the average password length used in the password brute forcing attempt rounded to closest whole integer?

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" dest_ip="192.168.250.70" http_method="POST" username passwd 
| rex field=form_data "passwd=(?<passwd>\w+)" 
| eval length=len(passwd) 
| stats avg(length)
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/14-average.png">

> Answer: **6**

### How many seconds elapsed between the time the brute force password scan identified the correct password and the compromised login rounded to 2 decimal places?

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" dest_ip="192.168.250.70" http_method="POST" username passwd  | rex field=form_data "passwd=(?<passwd>\w+)"  | search passwd=batman 
| transaction passwd 
| eval dur=round(duration, 2)
| table dur
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/15-diff.png">

> Answer: **92.17**

### How many unique passwords were attempted in the brute force attempt?

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" dest_ip="192.168.250.70" http_method="POST" username passwd 
| rex field=form_data "passwd=(?<passwd>\w+)" 
| stats count by passwd
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/16-count.png">

> Answer: **412**

### What is the name of the executable uploaded by P01s0n1vy?

```
index=botsv1 imreallynotbatman.com sourcetype="stream:http" dest_ip="192.168.250.70" form-data
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/17-exe.png">

> Answer: **3791.exe**

### What is the MD5 hash of the executable uploaded?

```
index=botsv1 3791.exe md5 sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" CommandLine="3791.exe" 
| rex field="_raw" "MD5=(?<hash>\w+)" 
| table hash 
| stats count by hash
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/18-hash.png">

> Answer: **AAE3F5A29935E6ABCC2C2754D12A9AF0**

### What is the name of the file that defaced the imreallynotbatman.com website?



> Answer: **poisonivy-is-coming-for-you-batman.jpeg**

### This attack used dynamic DNS to resolve to the malicious IP. What fully qualified domain name (FQDN) is associated with this attack?

> Answer: ****

### What IP address has P01s0n1vy tied to domains that are pre-staged to attack Wayne Enterprises?

> Answer: ****

### Based on the data gathered from this attack and common open source intelligence sources for domain names, what is the email address that is most likely associated with P01s0n1vy APT group?

> Answer: ****

### GCPD reported that common TTPs (Tactics, Techniques, Procedures) for the P01s0n1vy APT group if initial compromise fails is to send a spear phishing email with custom malware attached to their intended target. This malware is usually connected to P01s0n1vy’s initial attack infrastructure. Using research techniques, provide the SHA256 hash of this malware.

> Answer: ****

### What special hex code is associated with the customized malware discussed in the previous question?

> Answer: ****

### What does this hex code decode to?

> Answer: ****

<hr>

## Ransomware

### What was the most likely IP address of we8105desk on 24AUG2016?

> Answer: ****

### What is the name of the USB key inserted by Bob Smith?

> Answer: ****

### After the USB insertion, a file execution occurs that is the initial Cerber infection. This file execution creates two additional processes. What is the name of the file?

> Answer: ****

### During the initial Cerber infection a VB script is run. The entire script from this execution, pre-pended by the name of the launching .exe, can be found in a field in Splunk. What is the length in characters of this field?

> Answer: ****

### Bob Smith's workstation (we8105desk) was connected to a file server during the ransomware outbreak. What is the IP address of the file server?

> Answer: ****

### What was the first suspicious domain visited by we8105desk on 24AUG2016?

> Answer: ****

### The malware downloads a file that contains the Cerber ransomware cryptor code. What is the name of that file?

> Answer: ****

### What is the parent process ID of 121214.tmp?

> Answer: ****

### Amongst the Suricata signatures that detected the Cerber malware, which signature ID alerted the fewest number of times?

> Answer: ****

### The Cerber ransomware encrypts files located in Bob Smith's Windows profile. How many .txt files does it encrypt?

> Answer: ****

### How many distinct PDFs did the ransomware encrypt on the remote file server?

> Answer: ****

### What fully qualified domain name (FQDN) does the Cerber ransomware attempt to direct the user to at the end of its encryption phase?

> Answer: ****

### Recap

In this task we learnt how to:
 * 