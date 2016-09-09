---
layout: post
title: Git - undo pushed commit
category: How-To
tags: git program how-to
description: git know how series
---

If you made mistakes in the previous commit and you already pushed it to the remote repo, you can use

	git revert <commit_hash>

This will create a new commit which reverts the changes of the commit you specified with the `<commit_hash>`.

Use `git log` to find the `<commit_hash>`

[Original post](http://stackoverflow.com/questions/22682870/git-undo-pushed-commits)