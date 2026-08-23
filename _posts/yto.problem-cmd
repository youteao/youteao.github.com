---
layout: My first post!
title: "make 'cmd"
date:   2026-06-10 20:30:13 +0800
categories: Default
tags: test Test
comments: 1
---
명령 프롬포트 만들기

> ```python
> import os
> class CMD:
>     def cd(self,a):
>         if a == "..":
>             c = os.getcwd().split("\\")
>             b = ''
>             for i in range(len(c)):
>                 if i == len(c)-1:
>                     pass
>                 else:
>                     b += c[i] + '\\'
>             os.chdir(b)
>         else:
>             b = os.getcwd() +"\\" + str(a)
>             os.chdir(b)
>     def dir(self):
>         a = os.popen("dir")
>         print(a.read())
>     def cat(self,b):
>         a = open(os.getcwd()+ '\\' + str(b),'r')
>         while True:
>             d = a.readline()
>             if not d:
>                 break
>             print(d)
>         a.close()
> 
> 
> while True:
>     a = CMD()
>     b = input(os.getcwd() + '>').split()
>     if b[0] == "cd":
>         a.cd(b[1])
>     elif b[0] == "dir":
>         a.dir()
> 
>     elif b[0] == "cat":
>         a.cat(b[1])
> 
>     else:
>         print("명령어가 존재하지 않습니다.")
> ```
