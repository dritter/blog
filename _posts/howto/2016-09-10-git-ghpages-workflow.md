---
layout: post
title: Git - gh-pages workflow
category: How-To
tags: git program how-to
description: git know how series
---

## Intro

Working with gh-pages can be sometimes confusing for a git n00b.
This particular blog is powered by Jekyll, which takes a full advantage of Github static site generator in the `gh-pages` branch.
It is way more convenient to publish post as Markdown files and focusing on the content that dealing with the usual html stuffs.

> Since the fact that only the `gh-pages` branch will be displayed, I wasn't sure whether I should mainly work on the `master` and keep the `gh-pages` synced, or the other way around.

Here's the catch.

First, since my default url of `ferdianap.github.io` has been occupied with my academic website, I can only host my blog using a baseurl `/blog` under `ferdianap.github.io`.
When you use the default url, you'll have no problem of working on your `master` entirely without the need of `gh-pages` branch, and this is obviously not the case for me.

Second, in the conventional workflow, in most cases you would want to work on a separate branch to test new features and merge/rebase them with `master` when you're done. This allows you to experiment stuffs without messing around with the `master`.

However, in case of `gh-pages`, since the fact mentioned before, I couldn't think of a reason why you would want to mainly work on `master` and sync the `gh-pages` later, when in fact: **it is faster and more convenient to do the opposite**. Besides, once you push to `gh-pages`, the changes are displayed live immediately.

And finally, you may think it's easier to just [delete][6] the `master`. Well, I'd like to avoid that, just in case someone is interested to fork my repo and would like to use the `username.github.io` url instead of with baseurl.

## My gh-pages workflow

It turns out the solution is simple, since most of the time the commit tree is linear.
I mainly work on `gh-pages`, and after I'm done,

```sh
git checkout master # I switch to master
git merge gh-pages # this will fast-forward master to gh-pages
```
This concept conversely applicable for master to gh-pages.

## Run Jekyll dev server

Run the following in a separate terminal

	jekyll serve --watch --baseurl ''

From your browser, go to `localhost:4000` to see the preview
	
```sh
--watch  # Enable auto-regeneration of the site when files are modified.
--baseurl '' # empty because we run it inside the `blog` directory
```

## Alternative workflows

### Rebase from gh-pages

This is a recommended approach too. This applies **if you are working mainly in `gh-pages` and would like to apply the changes to `master`**, at the point where `gh-pages` and `master` have a common parent branch (Figure 1).

			   (gh-pages)
			       ↓
			  ┌─── C4
	C0 ─ C1 - C2 - C3
			       ↑
			    (master) 
	Figure 1. Simple divergent history

In this case, you’d do your work in a `gh-pages` and then rebase your work onto `origin/master` when you were ready to submit your patches to the main project.
That way, the maintainer doesn’t have to do any integration work – just a fast-forward or a clean apply.

			   (gh-pages)
			       ↓
			  ┌─── C4 ──┐
	C0 ─ C1 - C2 - C3 ─ C5
			    	    ↑
			        (master) 
	Figure 1.1. A new C5 appears when you merge

You can take the patch of the change that was introduced in C4 and reapply it on top of C3. In Git, this is called rebasing. (From Fig 1 to Fig 2).

	git checkout gh-pages
	git rebase master # rebase gh-pages on top of master

and then the `master` will be 1 commit behind the `gh-pages`,

			    	(gh-pages)
			       		↓
	C0 ─ C1 - C2 - C3 ─ C4'
			       ↑
			   (master) 
	Figure 2. Rebasing the change introduced in C4 onto C3

so you go back to `master` and do fast-forward merge.

	git checkout master
	git merge gh-pages

then the `master` is now pointing to the same commit with `gh-pages`.

			    	(gh-pages)
			       		↓
	C0 ─ C1 - C2 - C3 ─ C4'
			       		↑
			   		(master) 
	Figure 3. Fast-forwarding the master branch

[Original post][2]

### Mirror gh-pages onto master

No 2 recommendation alternative.
There's this similar [workflow][1] by doing the following

```sh
git checkout gh-pages
git merge -s ours master
git checkout master
git merge gh-pages
```
The result should be your `master` is now essentially `gh-pages`.

`git merge branch` means to merge the `branch` into your active branch (e.g. `master`)

### Rebase from master

If you prefer working on your master, there are plenty of workflows proposed by others.
[This article][4] compiles all the useful workflows when working on your `master`.

[Lea Verou][5] proposed using `rebase` to sync `master` with `gh-pages`.

```sh
git add .
git status # to see what changes are going to be committed
git commit -m 'Some descriptive commit message'
git push # push the master branch changes to GitHub

git checkout gh-pages # go to the gh-pages branch
git rebase master # bring gh-pages up to date with master
git push # push the gh-pages branch changes to GitHub Pages
git checkout master # return to the master branch
```
By rebasing, all commits on the master branch (and their commit messages) are applied to the gh-pages branch.

### Push once to both repo

If you prefer working on your `master` and [push once for both master and gh-pages][3], the link provide some suggestions on how to do that, although I prefer my current workflow for safety.

I'm curious to hear other perspective on their situation and how to deal with it.


[1]: http://stackoverflow.com/questions/2862590/how-to-replace-master-branch-in-git-entirely-from-another-branch
[2]: https://git-scm.com/book/en/v2/Git-Branching-Rebasing
[3]: http://stackoverflow.com/questions/5807459/github-mirroring-gh-pages-to-master#answer-7472481
[4]: http://oli.jp/2011/github-pages-workflow/
[5]: http://lea.verou.me/2011/10/easily-keep-gh-pages-in-sync-with-master/
[6]: http://oli.jp/2011/github-pages-workflow/#deleting-master
