---
title:  "TryHackMe: Advent of Cyber - Day 18 - Playing With Containers"
date:   2021-12-19 10:00:00 +1000
excerpt: Learning about AWS, Docker, and Elastic Containers.
---

This is a write up for the Day 18 - Playing With Containers challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### What command will list container images stored in your local container registry?

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-18/d18_01.jpg">

> Answer: **docker images**

### What command will allow you to save a docker image as a tar archive?

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-18/d18_02.jpg">

> Answer: **docker save**

### What is the name of the file (including file extension) for the configuration, repository tags, and layer hash values stored in a container image?

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-18/d18_03.jpg">

> Answer: **manifest.json**

### What is the token value you found for the bonus challenge?

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-18/d18_04.jpg">

> Answer: **7095b3e9300542edadbc2dd558ac11fa**

### Recap

In this task we learnt:
 * How to exploit AWS implementations
 * How to interrogate Docker containers