---
layout: post
title:  "undefined reference to math function"
date:   2018-09-15 10:33:42 +0530
categories: programming error
---

undefined reference to `pow'
collect2: error: ld returned 1 exit status

undefined reference to `sqrt'
collect2: error: ld returned 1 exit status

In Linux(Ubuntu 18.04.1 LTS), when we compile c program (gcc -o executableName programName.c ) we may face the above errors

 Since <b>libm.a</b> is not linked by default, we have to add <b>-lm</b> in the command-line to use standard library functions declared in math.h.
```
 gcc -o executableName programName.c -lm
```
[Reference](https://stackoverflow.com/questions/1033898/why-do-you-have-to-link-the-math-library-in-c)
 