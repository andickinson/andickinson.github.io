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

```
index=botsv1 sourcetype="suricata" src_ip="192.168.250.70" dest_ip="23.22.63.114" 
|  stats count by http.http_method, http.hostname, http.url 
|  sort -count
```

> Answer: **poisonivy-is-coming-for-you-batman.jpeg**

### This attack used dynamic DNS to resolve to the malicious IP. What fully qualified domain name (FQDN) is associated with this attack?

```
index=botsv1 sourcetype=fgt_utm "poisonivy-is-coming-for-you-batman.jpeg" 
| rex field="_raw" "hostname=(?<hostname>\w+)" 
| table hostname
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/19-hostname.png">

> Answer: **prankglassinebracket.jumpingcrab.com**

### What IP address has P01s0n1vy tied to domains that are pre-staged to attack Wayne Enterprises?

```
index=botsv1 sourcetype=fgt_utm "poisonivy-is-coming-for-you-batman.jpeg" 
| table dstip
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/20-dstip.png">

> Answer: **23.22.63.114**

### Based on the data gathered from this attack and common open source intelligence sources for domain names, what is the email address that is most likely associated with P01s0n1vy APT group?

Doing a google search for **23.22.63.114** provdes the following page: https://www.threatcrowd.org/ip.php?ip=23.22.63.114.

On this page a diagram is provided which reveals a potential email address.

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/21-email.png">

> Answer: **lilian.rose@po1s0n1vy.com**

### GCPD reported that common TTPs (Tactics, Techniques, Procedures) for the P01s0n1vy APT group if initial compromise fails is to send a spear phishing email with custom malware attached to their intended target. This malware is usually connected to P01s0n1vy’s initial attack infrastructure. Using research techniques, provide the SHA256 hash of this malware.

Searching for **23.22.63.114 malware hash** provides a link to https://www.threatminer.org/host.php?q=23.22.63.114#gsc.tab=0&gsc.q=23.22.63.114&gsc.page=1.

This reveals a hash for a number of trojans.

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/22-malware.png">

Following the link on the MD5 provides a SHA256 hash related to this malware - https://www.threatminer.org/sample.php?q=c99131e0169171935c5ac32615ed6261#gsc.tab=0&gsc.q=c99131e0169171935c5ac32615ed6261&gsc.page=1

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/23-sha256.png">

> Answer: **9709473ab351387aab9e816eff3910b9f28a7a70202e250ed46dba8f820f34a8**

### What special hex code is associated with the customized malware discussed in the previous question?

Following the VirusTotal link on the previous page reveals the HEX code - https://www.virustotal.com/gui/file/9709473ab351387aab9e816eff3910b9f28a7a70202e250ed46dba8f820f34a8/community

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/24-hex.png">

> Answer: **53 74 65 76 65 20 42 72 61 6e 74 27 73 20 42 65 61 72 64 20 69 73 20 61 20 70 6f 77 65 72 66 75 6c 20 74 68 69 6e 67 2e 20 46 69 6e 64 20 74 68 69 73 20 6d 65 73 73 61 67 65 20 61 6e 64 20 61 73 6b 20 68 69 6d 20 74 6f 20 62 75 79 20 79 6f 75 20 61 20 62 65 65 72 21 21 21**

### What does this hex code decode to?

Putting the HEX code into an online converter (https://cryptii.com/pipes/hex-decoder) reveals the following message.

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/25-message.png">

> Answer: **Steve Brant's Beard is a powerful thing. Find this message and ask him to buy you a beer!!!**

<hr>

## Ransomware

### What was the most likely IP address of we8105desk on 24AUG2016?

```
index=botsv1 host=we8105desk| top limit=20 src_ip
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/26-ip.png">

> Answer: **192.168.250.100**

### What is the name of the USB key inserted by Bob Smith?

```
index=botsv1 host=we8105desk sourcetype=WinRegistry friendlyname 
| top limit=1 data
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/27-name.png">

> Answer: **MIRANDA_PRI**

### After the USB insertion, a file execution occurs that is the initial Cerber infection. This file execution creates two additional processes. What is the name of the file?

```
index=botsv1 host=we8105desk sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" "d:\\" 
| reverse
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/28-file.png">

> Answer: **miranda_tate_unveiled.dotm**

### During the initial Cerber infection a VB script is run. The entire script from this execution, pre-pended by the name of the launching .exe, can be found in a field in Splunk. What is the length in characters of this field?

```
index=botsv1 sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" *.exe CommandLine=* EventCode=1
| eval length=len(CommandLine) 
| table CommandLine length 
| sort - 1 length
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/29-length.png">

> Answer: **4490**

### Bob Smith's workstation (we8105desk) was connected to a file server during the ransomware outbreak. What is the IP address of the file server?

```
index=botsv1 host="we8105desk" sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" src="we8105desk.waynecorpinc.local" 
| stats count by dest_ip
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/30-ip.png">

> Answer: **192.168.250.20**

### What was the first suspicious domain visited by we8105desk on 24AUG2016?

```
index=botsv1 src="192.168.250.100" sourcetype="stream:dns" record_type=A NOT (query{}=*.microsoft.com OR query{}=*.bing.com OR query{}=wpad* OR query{}=isatap OR query{}=*.waynecorpinc.local OR query{}=*.windows.com OR query{}=*.msftncsi.com)
| table _time query{} src dest
| reverse
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/31-url.png">

> Answer: **solidaritedeproximite.org**

### The malware downloads a file that contains the Cerber ransomware cryptor code. What is the name of that file?

```
index=botsv1 src="192.168.250.100" sourcetype="suricata" url=*
| stats count values(url) by dest
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/32-mhtr.png">

The first result is **mhtr.jpg**, doing a google search of this file reveals it is related to a ransomware  attack.

> Answer: **mhtr.jpg**

### What is the parent process ID of 121214.tmp?

```
index=botsv1 sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" 121214.tmp 
| table _time CommandLine ProcessId ParentProcessId ParentCommandLine 
| reverse
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/33-pid.png">

> Answer: **3968**

### Amongst the Suricata signatures that detected the Cerber malware, which signature ID alerted the fewest number of times?

```
index=botsv1 sourcetype=suricata alert.signature=*cerber* 
| stats count by alert.signature_id
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/34-sid.png">

> Answer: **2816763**

### The Cerber ransomware encrypts files located in Bob Smith's Windows profile. How many .txt files does it encrypt?

```
index=botsv1 sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" host=we8105desk *.txt EventCode=2 TargetFilename="C:\\Users\\bob.smith.WAYNECORPINC\\*.txt" 
| stats dc(TargetFilename)
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/35-count.png">

> Answer: **406**

### How many distinct PDFs did the ransomware encrypt on the remote file server?

```
index=botsv1 sourcetype="*win*" pdf dest="we9041srv.waynecorpinc.local" Source_Address="192.168.250.100" 
| stats dc(Relative_Target_Name)
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/36-pdf.png">

> Answer: **257**

### What fully qualified domain name (FQDN) does the Cerber ransomware attempt to direct the user to at the end of its encryption phase?

```
index=botsv1 sourcetype="stream:DNS" src=192.168.250.100 record_type=A NOT (query{}=*.microsoft.com OR query{}=wpad OR query{}=isatap OR query{}=*.waynecorpinc.local OR query{}=*.bing.com OR query{}=*.windows.com OR query{}=*.msftncsi.com OR query{}=*.live.com) 
| table _time query{} src dest
```

<img src="{{ site.baseurl }}/assets/images/2021-03-25-splunk-boss-of-the-soc-v1/37-fqdn.png">

> Answer: **cerberhhyed5frqa.xmfir0.win**

### Recap

In this task we learnt how to:
 * Conduct search queries to find information in Splunk
 * Find identifiers of APT activity
 * Find identifiers of Ransomware activity
 * Conduct OSINT to find malware information

 