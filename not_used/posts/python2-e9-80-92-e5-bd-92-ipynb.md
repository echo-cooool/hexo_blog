---
title: python2 递归.ipynb
tags:
  - python
url: 14339.html
id: 14339
categories:
  - Python
date: 2018-05-25 23:14:53
---

递归阶乘

In \[4\]:

x = input("X = ")
def fact(x):
    if x == 1 :
        return 1
    return fact(x-1) * x
print fact(x)

X = 5
120

递归求和

In \[6\]:

x = input("x = ")
def xigema(x):
    if x == 1 :
        return 1
    return xigema(x - 1) + x
print xigema(x)

x = 3
6

递归求和改进版

In \[18\]:

start = input("Start = ")
end = input("End = ")
def xigema(start):
    if start == end :
        return end
    #print start
    return xigema(start + 1) + start
try :
    a =  xigema(start)
    print a
except: 
    print "ERROR"

Start = 4
End = 6
15

递归生成斐波那契数列

In \[23\]:

num = input("num = ")

def fb(n):
    if n == 0 :   
        return 0  
    elif n == 1 :  
        return 1  
    else :  
        return fb( n - 1 ) + fb( n - 2 ) 
try :
    for i in range ( 0 , num  ) :  
        print fb(i)  
except: 
    print "ERROR"

num = 7
0
1
1
2
3
5
8