---
layout: post
title:  "How to indent c program in vim"
date:   2018-11-10 17:30:00 +0530
categories: programming vim indentation
---
1 First select all the code
```
Shift + V       (visual line)(select using arrow keys manually )
```
or 
```
ggVG
```
2 Move all the code to the left side
```
 Shift + <
```
3 Remove trailing space
```
:%s/#*$/    (# represents space; replace with space)
``` 
4 Auto indent 
```
gg=G
```
[Vim commands]()
 