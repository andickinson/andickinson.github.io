---
title:  "TryHackMe: Active Directory Basics"
date:   2021-05-29 23:00:00 +1000
excerpt: Learning the basics of Active Directory and how it is used in the real world today.
---

This is a write up for the **Hands-On Lab** task of the [**Active Directory Basics**](https://tryhackme.com/room/activedirectorybasics) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

### What is the name of the Windows 10 operating system?

```
Get-NetComputer -fulldata | select operatingsystem
```

<img src="{{ site.baseurl }}/assets/images/2021-05-29-active-directory-basics/01-os.png">

> Answer: **Windows 10 Enterprise Evaluation**

### What is the second "Admin" name?

```
Get-NetUser | select cn
```

<img src="{{ site.baseurl }}/assets/images/2021-05-29-active-directory-basics/02-admin.png">

> Answer: **Admin 2**

### Which group has a capital "V" in the group name?

```
Get-NetGroup -GroupName *V*
```

<img src="{{ site.baseurl }}/assets/images/2021-05-29-active-directory-basics/03-v.png">

> Answer: **Hyper-V Administrators**

### When was the password last set for the SQLService user?

```
Get-NetUser -SPN | ?{$_.memberof -match 'Domain Admins'}
```

<img src="{{ site.baseurl }}/assets/images/2021-05-29-active-directory-basics/04-pwd.png">

> Answer: **5/13/2020 8:26:58 PM**

### Recap

In this task we learnt how to:
 * Conduct basic queries on Active Directory
 