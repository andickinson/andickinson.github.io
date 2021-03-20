---
title:  "TryHackMe: Investigating Windows"
date:   2021-03-21 00:15:00 +1100
excerpt: Investigating a hacked Windows machine to find clues to what the hacker might have done. 
---

This is a write up for the [**Investigating Windows**](https://tryhackme.com/room/investigatingwindows) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

### Whats the version and year of the windows machine?

Press Windows+R to open the Run prompt then type **regedit** then enter.

Navigate to:
```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProductName
```

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/01-os.jpg">

> Answer: **Windows Server 2016**

### Which user logged in last?

Navigate to:
```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI\LastLoggedOnUser
```

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/02-user.jpg">

> Answer: **Administrator**

### When did John log onto the system last?

Open cmd.exe and enter the following command.

```
net user John
```

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/03-john.jpg">

> Answer: **03/02/2019 5:48:32 PM**

### What IP does the system connect to when it first starts?

Open **regedit** again and navigate to:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run\UpdateSvc
```

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/04-updatesvc.jpg">

> Answer: **10.34.2.3**

### What two accounts had administrative privileges (other than the Administrator user)?

Open **Run** and enter:

```
lusrmgr.msc
```

Open Groups -> Administrators

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/05-users.jpg">

It is very interesting that the **Guest** user is part of the **Administrators** group.

> Answer: **Jenny, Guest**

### Whats the name of the scheduled task that is malicous.

Open the Task Scheduler.

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/06-apt.jpg">

The following tasks appears to be doing something suspicious:
 
 * Clean file system
    * Attempts to open **C:\TMP\nc.ps1 -l 1348**
    * This appears to be an [APT simulator](https://github.com/NextronSystems/APTSimulator/blob/master/toolset/nc.ps1)
 * GameOver
    * Attempts to save LogonPasswords to a text file every 5 minutes

However, TryHackMe wants us to answer 'Clean file system'.

> Answer: **Clean file system**

### What file was the task trying to run daily?

> Answer: **nc.ps1**

### What port did this file listen locally for?

> Answer: **1348**

### When did Jenny last logon?

Open **cmd.exe** and type:

```
net user Jenny
```

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/07-jenny.jpg">

> Answer: **Never**

### At what date did the compromise take place?

The 'Clean file system' task was created no 03/02/2019, we can assume that is the date of the compromise.

> Answer: **03/02/2019**

### At what time did Windows first assign special privileges to a new logon?

Open **Event Viewer** and look for the correct entry.

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/08-priv.jpg">

> Answer: **03/02/2019 04:04:49 PM**

### What tool was used to get Windows passwords?

We know from earlier questions that the scheduled tasks are executing applications in **C:\TMP**.

Open Windows Explorer and navigate to:

```
C:\TMP\mim-out.txt
```

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/09-mim.jpg">

> Answer: **Mimikatz**

### What was the attackers external control and command servers IP?

There is probably an entry in the **hosts** file.

Open the following in notepad:

```
C:\Windows\System32\drivers\etc\hosts.txt
```

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/10-hosts.jpg">

> Answer: **76.32.97.132**

### What was the extension name of the shell uploaded via the servers website?

Something related to a webserver is probably stored in **C:\inetpub\wwwroot**.

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/11-jsp.jpg">

> Answer: **.jsp**

### What was the last port the attacker opened?

Open **Windows Firewall** and then click on **Inbound Rules**.

The most recent entry shows which port was opened.

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/12-firewall.jpg">

> Answer: **1337**

### Check for DNS poisoning, what site was targeted?

Back to the hosts file again.

<img src="{{ site.baseurl }}/assets/images/2021-03-21-investigating-windows/13-google.jpg">

> Answer: **google.com**

### Recap

In this task we learnt how to:
 * Utilise **forensic techniques** on a compromised Windows Server 2016 system
 * Navigate the **registry** to find relevant information
 * Use the **net** command to find user information
 * Use **lusrmgr.msc** to find user group assignments
 * Use the **Task Scheduler** to identify malicious tasks
 * Use **Event Viewer** to identify suspicious events
 * Investigate the **hosts** file to find DNS poisoning attempts
 * Review the **Windows Firewall** to find errant rules