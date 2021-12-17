---
title:  "TryHackMe: Advent of Cyber - Day 8 - Santa's Bag of Toys"
date:   2021-12-17 11:30:00 +1000
excerpt: Learning about Windows Forensics.
---

This is a write up for the Day 8 - Santa's Bag of Toys challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### What operating system is Santa's laptop running ("OS Name")?

Open the first log file and look for a line starting with `OS Name`.

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-8/d8_01.jpg">

> Answer: **Microsoft Windows 11 Pro**

### What was the password set for the new "backdoor" account?

In the second log file, we can see the `net user` command which shows the password.

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-8/d8_02.jpg">

> Answer: **grinchstolechristmas**

### In one of the transcription logs, the bad actor interacts with the target under the new backdoor user account, and copies a unique file to the Desktop. Before it is copied to the Desktop, what is the full path of the original file? 

The third log file shows the `copy` command.

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-8/d8_03.jpg">

> Answer: **C:\Userse\santa\AppData\Local\Microsoft\Windows\UsrClass.dat**

### The actor uses a Living Off The Land binary (LOLbin) to encode this file, and then verifies it succeeded by viewing the output file. What is the name of this LOLbin?

This can be found in the third log file.

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-8/d8_04.jpg">

> Answer: **certutil.exe**

### Drill down into the folders and see if you can find anything that might indicate how we could better track down what this SantaRat really is. What specific folder name clues us in that this might be publicly accessible software hosted on a code-sharing platform?

Opening the SantaRat folder shows a version control folder.

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-8/d8_05.jpg">

> Answer: **.github**

### Additionally, there is a unique folder named "Bag of Toys" on the Desktop! This must be where Santa prepares his collection of toys, and this is certainly sensitive data that the actor could have compromised. What is the name of the file found in this folder? 

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-8/d8_06.jpg">

> Answer: **bag_of_toys.zip**

### What is the name of the user that owns the SantaRat repository?

The GitHub repository is located here: https://github.com/Grinchiest/SantaRat

> Answer: **Grinchiest**

### Explore the other repositories that this user owns. What is the name of the repository that seems especially pertinent to our investigation?

The following repository is of interest: https://github.com/Grinchiest/operation-bag-of-toys

> Answer: **operation-bag-of-toys**

### What is the name of the executable that installed a unique utility the actor used to collect the bag of toys?

The third log file shows the user installing a utility.

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-8/d8_07.jpg">

> Answer: **uharc-cmd-install.exe**

### What are the contents of these "malicious" files (coal, mold, and all the others)?

The fourth log file shows the values being overridden by a value of `GRINCHMAS`.

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-8/d8_08.jpg">

> Answer: **GRINCHMAS**

### What is the password to the original bag_of_toys.uha archive?

The user accidentally committed the `bag_of_toys.uha` file which also included the password in the commit message.

https://github.com/Grinchiest/operation-bag-of-toys/commit/41615462e4fdc0ceeb4ef1bec693ec3de1125ed2

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-8/d8_09.jpg">

> Answer: **TheGrinchiestGrinchmasOfAll**

### How many original files were present in Santa's Bag of Toys?

Opening the `bag_of_toys.uha` file with the discovered password show us the total number of files.

<img src="{{ site.baseurl }}/assets/images/2021-12-17-advent-of-cyber-day-8/d8_10.jpg">

> Answer: **228**

### Recap

In this task we learnt:
 * Windows Forensics
 * LOLbin encoding
 * Base64 decodes via CyberChef
 * Uses for ShellBagsExplorer
 * GitHub OSINT
 