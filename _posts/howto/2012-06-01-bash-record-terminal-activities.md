---
layout: post
title: Bash - record terminal activities
category: How-To
tags: bash program how-to
description: bash know how series
---

The command to record activities in the terminal is `script`, before executing any other thing, you just need to run the following command to make a log file

	script log.txt  


After that, everything you run afterward in the terminal and the outputs will be recorded into this log file.

If you dont want to record the activities anymore, you just need to hit <kbd>Ctrl</kbd> + <kbd>D</kbd>.

To start recording again to the same log file, you can run this command

	script -a log.txt  

[Original post](http://www.linuxandlife.com/2012/06/how-to-record-terminal-activities-and.html#sthash.jn4irK0C.dpuf)