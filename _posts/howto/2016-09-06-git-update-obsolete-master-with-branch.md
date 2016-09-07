---
layout: post
title: Git - update obsolete master with branch
category: How-To
tags: git program how-to
description: git know how series
---

	git checkout gh-pages
	git merge -s ours master
	git checkout master
	git merge gh-pages

The result should be your master is now essentially gh-pages.

git merge `branch` means to merge the `branch` into your active branch (e.g. `master`)

[Original post](http://stackoverflow.com/questions/2862590/how-to-replace-master-branch-in-git-entirely-from-another-branch)