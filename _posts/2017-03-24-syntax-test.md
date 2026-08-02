---
layout: post
title:  "problems"
date:   2017-03-24 01:30:13 +0800
categories: default
tags: test syntax
---

w = ''
a = open("C:/Python/새파일.txt", 'w')
while True:
    b = input("이름을 입력하세요:")
    c = input("점수을 입력하세요:")
    w = w + (f"{b}:{c} ")
    if input("계속하시겠습니까?(y/n):") == "n":
        break
a.write(w)
a.close()
a = open("C:/Python/새파일.txt", 'r')
while True:
    d = a.readline()
    if not d: break
    print(d)
a.close()


def square(a, b):
    return (a+b)*2, a*b
def curcle(a):
    return a * 6.28, a*a*3.14


while True:
    a = input("1:사각형, 2:원 , 3:종료>>")
    if a == '1':
        b,c =square(int(input("첫번째 수를 입력하세요:")),int(input("두번째 수를 입력하세요:")))
        print(f"사각형의 둘래는{b}, 넒이는{c} 입니다")
    elif a == '2':
        b,c = curcle(int(input("첫번째 수를 입력하세요:")))
        print(f"사각형의 둘래는{b}, 넒이는{c} 입니다")
    elif a == '3':
        break
    else:
        print("잘못 입력하였습니다.")
