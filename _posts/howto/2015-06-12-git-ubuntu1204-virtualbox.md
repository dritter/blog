---
layout: post
title: Git + Ubuntu 12.04 + VirtualBox
category: How-To
tags: github ubuntu virtualbox program how-to
description: git know how series
---

# Setting GitHub for VM Linux Ubuntu 12.04

By [Ferdian Pratama](http:/ferdianap.github.io/)

Latest update: Jun 12, 2015 13:50:29 PM

<!-- MarkdownTOC depth=3 -->

- Update Git into the latest version
- Creating a token
- Setting up the token
- First time initialization
- 3 Simple Steps / 2 Quick Steps
    - Rename a git folder
    - Remove directory from git and local
    - Remove directory from git but NOT local

<!-- /MarkdownTOC -->



## Update Git into the latest version

(Tested on ver. 2.4.3)

```sh
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```


## Creating a token

see [https://help.github.com/articles/creating-an-access-token-for-command-line-use/]()

1. Settings icon in the user barIn the top right corner of any page, click your profile photo, then click `Settings`.
2. Personal access tokens in the user settings sidebar, click `Personal access tokens`.
3. Click `Generate new token`.
4. Give your token a descriptive name.
5. Select the scopes you wish to grant to this token. The default scopes allow you to interact with public and private repositories, user data, and gists.
6. Click `Generate token`.
7. Copy the token to your clipboard. For security reasons, after you navigate off this page, no one will be able to see the token again.

Remember to keep your tokens secret; treat them just like passwords!

They act on your behalf when interacting with the API.

Don't hardcode them into your programs. Instead, opt to use them as environment variables.

When you're done using your token, feel free to click Delete to get rid of it permanently.


## Setting up the token

Run `git init` in each of the project folder.
In the terminal, do the following in the project folder, for each project

```sh
git config remote.{project}.url "https://{token}@github.com/{username}/{project}.git"
```

for instance

```sh
git config remote.eris.url "https://f723740a0019a95480d950dffe0a6f7043394ca9@github.com/ferdianap/eris.git"
```

**OR**

go to the git folder of the project and open the `/.git/config` file, make sure that the `[remote "project_name"]` url has the format as above.

The final file looks more or less like this.

```json
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
[remote "Eris_test"]
    url = https://f723740a0019a95480d950dffe0a6f7043394ca9@github.com/ferdianap/Eris_test.git
    fetch = +refs/heads/*:refs/remotes/Eris_test/*
[branch "master"]
    remote = Eris_test
    merge = refs/heads/master
```

## First time initialization

```sh
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config --global push.default matching
```


Navigate to the project folder, either `git init` for a new git project, or `git pull` pull from repository first.


## 3 Simple Steps / 2 Quick Steps

Initially, <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>, TYPE `init` must be done ONCE only.

<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>, TYPE `add`

<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>, TYPE `quick`, THEN type `message`

<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>, TYPE `push`


**OR**

To add and commit all in one step, just skip straight to the Quick Commit command. That will stage and commit for you.

It’s the equivalent of git commit -am 'im staging and committing!'.

### Rename a git folder

```sh
git mv <old name> <new name>
```

followed by commit and push would be the simplest way.

### Remove directory from git and local

You could checkout `master` with both directories;

```sh
git rm -r one-of-the-directories
git commit -m "Remove duplicated directory"
git push origin master
```

### Remove directory from git but NOT local

As mentioned in the comments, what you usually want to do is remove this directory from git but not delete it entirely from the filesystem (local)

In that case use:

```sh
git rm -r --cached myFolder
```