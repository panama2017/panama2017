---
layout:     post
title:      "Download Resources from Website Using Python"
subtitle:   ""
date:       2016-09-27
author:     "Baoxiang Pan"
header-img: "img/home.jpg"
comments: true
---

There are many conditions that we need to download files of certain type from a website, for example, the handouts  of a course in pdf form from the class website. A very simple Python scripit is provided [here](https://github.com/lambdamore/My_Lib/blob/master/Python_Lib/WebSpider/DownloadLink.py) for this kind of work: 

```python
DownloadLink(link,type)
```
The first argument is the link site and the second being the file type you want to download.

The script relies on mechanize library, which can be downloaded from pip.

Good luck.
