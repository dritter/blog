---
layout: post
title: Git setup in Ubuntu
category: How-To
tags: git ubuntu program how-to
description: git know how series
---

Latest update: Jun 12, 2015 13:50:29 PM

<!-- MarkdownTOC depth=3 -->

- Update Git into the latest version
- Creating a token
- Setting up the token
- First time initialization
- 3 Simple Steps in ST3

<!-- /MarkdownTOC -->

## Update Git into the latest version

(Tested ver. 2.4.3 in Ubuntu 12.04)

```sh
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

## Creating a token

see [https://help.github.com/articles/creating-an-access-token-for-command-line-use/](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)

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

## 3 Simple Steps in ST3

Quick commit in Sublime Text 3, this can be done conveniently.
Initially, <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>, TYPE `init` must be done ONCE only.

<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>, TYPE `add`

<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>, TYPE `quick`, THEN type the message

<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>, TYPE `push`