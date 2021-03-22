---
title:  "TryHackMe: Splunk - Can you dig it?"
date:   2021-03-22 21:30:00 +1100
excerpt: Learning the basic commands for Splunk. 
---

This is a write up for the **Can you dig it?** task of the [**Splunk**](https://tryhackme.com/room/bpsplunk) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

### Splunk queries always begin with this command implicitly unless otherwise specified. What command is this? When performing additional queries to refine received data this command must be added at the start. This is a prime example of a slight trick question.

> Answer: **search**

### When searching for values, it's fairly typical within security to look for uncommon events. What command can we include within our search to find these?

> Answer: **rare**

### What about the inverse? What if we want the most common security event?

> Answer: **top**

### When we import data into splunk, what is it stored under?

> Answer: **index**

### We can create 'views' that allow us to consistently pull up the same search over and over again; what are these called?

> Answer: **dashboards**

### Importing data doesn't always go as planned and we can sometimes end up with multiple copies of the same data, what command do we include in our search to remove these copies?

> Answer: **dedup**

### Splunk can be used for more than just a SIEM and it's commonly used in marketing to track things such as how long a shopping trip on a website lasts from start to finish. What command can we include in our search to track how long these event pairs take?

> Answer: **transaction**

### In a manner similar to Linux, we can 'pipe' search results into further commands, what character do we use for this?

> Answer: **\|**

### In performing data analytics with Splunk (ironically what the tool is at it's core) it's useful to track occurrences of events over time, what command do we include to plot this?

> Answer: **timechart**

### What about if we want to gather general statistical information about a search?

> Answer: **stats**

### Data imported into Splunk is categorized into columns called what?

> Answer: **fields**

### When we import data into Splunk we can view it's point of origination, what is this called? I'm looking for the machine aspect of this here.

> Answer: **host**

### When we import data into Splunk we can view its point of origination from within a system, what is this called?

> Answer: **source**

### We can classify these points of origination and group them all together, viewing them as their specific type. What is this called? Use the syntax found within the search query rather than the proper name for this.

> Answer: **sourcetype**

### When performing functions on data we are searching through we use a specific command prior to the evaluation itself, what is this command?

> Answer: **eval**

### Love it or hate it regular expression is a massive component to Splunk, what command do we use to specific regex within a search?

> Answer: **rex**

### It's fairly common to create subsets and specific views for less technical Splunk users, what are these called?

> Answer: **pivot table**

### What is the proper name of the time date field in Splunk

> Answer: **_time**

### How do I specifically include only the first few values found within my search?

> Answer: **head**

### More useful than you would otherwise imagine, how do I flip the order that results are returned in?

> Answer: **reverse**

### When viewing search results, it's often useful to rename fields using user-provided tables of values. What command do we include within a search to do this?

> Answer: **lookup**

### We can collect events into specific time frames to be used in further processing. What command do we include within a search to do just that?

> Answer: **bucket**

### We can also define data into specific sections of time to be used within chart commands, what command do we use to set these lengths of time? This is different from the previous question as we are no longer collecting for further processing.

> Answer: **span**

### When producing statistics regarding a search it's common to number the occurrences of an event, what command do we include to do this?

> Answer: **count**

### Last but not least, what is the website where you can find the Splunk apps at?

> Answer: **splunkbase.splunk.com**

### We can also add new features into Splunk, what are these called?

> Answer: **apps**

### What does SOC stand for?

> Answer: **security operations center**

### What does SIEM stand for?

> Answer: **Security Information and Event Management**

### How about BOTS?

> Answer: **Boss of the SOC**

### And CIM?

> Answer: **Common Information Model**

### what is the website where you can find the Splunk forums at?

> Answer: **answers.splunk.com**

### Recap

In this task we learnt how to:
 * Execute basic commands for Splunk searches