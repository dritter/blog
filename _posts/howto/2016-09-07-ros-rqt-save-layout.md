---
layout: post
title: ROS - rqt save layout
category: How-To
tags: ros rqt gui program how-to
description: ros know how series
---

First, design your layout and close the rqt.

To save the prespective/layout:

1. export the perspective and load them as needed

or

2. copy the `rqt_gui.ini` as a backup using:

		cp ~/.config/ros.org/rqt_gui.ini ~

3. when you need to load it, 

		cd
		cp rqt_gui.ini ~/.config/ros.org/rqt_gui.ini