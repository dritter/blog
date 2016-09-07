---
layout: post
title: Bash - print using enscript
category: How-To
tags: bash program how-to
description: bash know how series
---

1. modify the `/etc/enscript.cfg`, uncomment the `Default A4`

2. use command

		enscript --color=1 -Ecpp -c2 -C1 -r -j --tabsize=4 --word-wrap filename.cpp

3. add in `.bashrc`

		alias pcode='enscript --color=1 -Ecpp -c2 -C1 -r -j --tabsize=4 --word-wrap'


> help: `enscript --help-pretty-print`
>
> where:
> ```sh
> -E is the flag format
> --color=1 means enabled
>
> -c2: 2 columns
> -C1: start line numbering from 1 onwards
> -r: print in landscape
> -j: print border around the columns
> ```

It can even generate syntax highlighted code in html, which makes it useful when you want to blog about source code:

	enscript --color=1 -w html -Eruby your_source_code.rb

add in `.bashrc`
	
	alias pcode='enscript --color=1 -Ecpp -c2 -C1 -r -j --tabsize=4 --word-wrap'
	alias pmcode='enscript --color=0 -Ecpp -c2 -C1 -r -j --tabsize=4 --word-wrap'