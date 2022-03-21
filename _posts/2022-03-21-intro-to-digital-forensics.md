---
title:  "TryHackMe: Intro to Digital Forensics"
date:   2022-03-21 08:30:00 +1000
excerpt: Learning about digital forensics and the related processes and experiment with a practical example.
---

This is a write up for the [**Intro to Digital Forensics**](https://tryhackme.com/room/introdigitalforensics) challenge room on [TryHackMe](https://tryhackme.com). Some tasks may have been omitted as they do not require an answer.

***

### Consider the desk in the photo above. In addition to the smartphone, camera, and SD cards, what would be interesting for digital forensics?

> Answer: **Laptop**

### It is essential to keep track of who is handling it at any point in time to ensure that evidence is admissible in the court of law. What is the name of the documentation that would help establish that?

> Answer: **Chain of Custody**

### Using pdfinfo, find out the author of the attached PDF file.

<img src="{{ site.baseurl }}/assets/images/2022-03-21-intro-to-digital-forensics/01.jpg">

> Answer: **Ann Gree Shepherd**

### Using exiftool or any similar tool, try to find where the kidnappers took the image they attached to their document. What is the name of the street?

Enter the following command:

```
exiftool letter-image.jpg
```

<img src="{{ site.baseurl }}/assets/images/2022-03-21-intro-to-digital-forensics/02.jpg">

Search the Lat/Long in [Google Maps](https://www.google.com/maps/place/51%C2%B030'51.9%22N+0%C2%B005'38.7%22W/@51.5143906,-0.0945229,19.25z/data=!4m5!3m4!1s0x0:0x2e4d5730133ca516!8m2!3d51.514417!4d-0.094092).

<img src="{{ site.baseurl }}/assets/images/2022-03-21-intro-to-digital-forensics/03.jpg">

> Answer: **Milk Street**

### What is the model name of the camera used to take this photo?

<img src="{{ site.baseurl }}/assets/images/2022-03-21-intro-to-digital-forensics/04.jpg">

> Answer: **Canon EOS R6**

### Recap

In this task we learnt:
 * The basics of the Digital Forensics process
 * How to use exiftool
 * How to use pdfinfo