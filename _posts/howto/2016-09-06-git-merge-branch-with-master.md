---
layout: post
title: Git - merge branch with master
category: How-To
tags: git program how-to
description: git know how series
---

To keep `branch` in sync with `master`, do the following:

	git checkout master
	git pull
	git checkout branch
	git merge master

