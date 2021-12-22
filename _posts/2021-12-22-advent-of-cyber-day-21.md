---
title:  "TryHackMe: Advent of Cyber - Day 21 - Needles in Computer Stacks"
date:   2021-12-22 08:00:00 +1000
excerpt: Learning about Yara.
---

This is a write up for the Day 21 - Needles in Computer Stacks challenge in the [**Advent of Cyber**](https://tryhackme.com/room/adventofcyber3) room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### We changed the text in the string $a as shown in the eicaryara rule we wrote, from X5O to X50, that is, we replaced the letter O with the number 0. The condition for the Yara rule is $a and $b and $c and $d. If we are to only make a change to the first boolean operator in this condition, what boolean operator shall we replace the 'and' with, in order for the rule to still hit the file?

If the first element no longer matches then we are required to use an 'or' operator.

```
    condition:
      $a or $b and $c and $d
```

> Answer: **or**

### What option is used in the Yara command in order to list down the metadata of the rules that are a hit to a file? 

```
yara -m eicaryara testfile
```

> Answer: **-m**

### What section contains information about the author of the Yara rule?

```
    meta:
      author="tryhackme"
      description="eicar string"
```

> Answer: **metadata**

### What option is used to print only rules that did not hit?

```
yara -n eicaryara testfile
```

> Answer: **-n**

### Change the Yara rule value for the $a string to X50. Rerun the command, but this time with the -c option. What is the result?

<img src="{{ site.baseurl }}/assets/images/2021-12-22-advent-of-cyber-day-21/d21_01.jpg">

> Answer: **0**

### Recap

In this task we learnt:
 * What are Yara rules
 * What is the basic structure of Yara rules
 * How to write basic Yara rules
 * How Yara rules are used