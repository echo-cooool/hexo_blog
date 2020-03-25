---
title: Python str类型转为float类型
tags:
  - python
url: 86.html
id: 86
categories:
  - Python
date: 2018-04-13 22:55:17
---

在写坐标转换问题的时候遇到的问题 有一个函数很好 贴出来： 利用map和reduce编写一个str2float函数，把字符串'123.456'转换成浮点数123.456

    from functools import reduce
    
    def str2float(s):
      return reduce(lambda x,y:x+int2dec(y),map(str2int,s.split('.')))
    def char2num(s):
      return {'0':0,'1':1,'2':2,'3':3,'4':4,'5':5,'6':6,'7':7,'8':8,'9':9}[s]
    def str2int(s):
      return reduce(lambda x,y:x*10+y,map(char2num,s))
    def intLen(i):
      return len('%d'%i)
    def int2dec(i):
      return i/(10**intLen(i))
    
    print(str2float('123.456'))

 

    from functools import reduce
    
    def str2float(s):
      return reduce(lambda x,y:x+int2dec(y),map(str2int,s.split('.')))
    def char2num(s):
      return {'0':0,'1':1,'2':2,'3':3,'4':4,'5':5,'6':6,'7':7,'8':8,'9':9}[s]
    def str2int(s):
      return reduce(lambda x,y:x*10+y,map(char2num,s))
    def intLen(i):
      return len('%d'%i)
    def int2dec(i):
      return i/(10**intLen(i))
    
    print(str2float('123.456'))
    

39.9074569444,116.2948912521 39.9076709213,116.2949073453 39.9076748804,116.2951563318 and((abs(r1 - a1) < 0.003)or(abs(r2 - a2) < 0.003))