---
title: "Anaconda Python Update"
date: 2018-04-22T16:26:38+08:00
draft: false
description: ""
tags: [anaconda, python]
categories: [anaconda]
author: "YT"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: false
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
mathjax: true
thumbnailImage: static/images/cover.jpg
---

[Anaconda](https://www.anaconda.com/download/) wrapes python in a pack. It is convenient to use Anaconda to install python when you are new to everything about python.

Recently, I noticed that my python version is 3.5.x while the newest version of python is 3.6. I found this problem when I was tring to use some modules that contain functions be newly added in version 3.6 and thus get errors.

My python was installed via Anaconda, so I have to use anaconda to update my python version. The method I used was
```
conda update python
```
However, it only updated my python between newer 3.5 version. My python was not upated across 3.5 to 3.6.
So, I found another method to update between version distributions.
```
conda install python==3.6
```
This updated my python to version 3.6 along with modules which diff from version 3.5 and 3.6.

## Summary
To update python in the same version distribution, use
```
conda update python
```

To update python across version distribution, use
```
conda install python==$python-version$
```
