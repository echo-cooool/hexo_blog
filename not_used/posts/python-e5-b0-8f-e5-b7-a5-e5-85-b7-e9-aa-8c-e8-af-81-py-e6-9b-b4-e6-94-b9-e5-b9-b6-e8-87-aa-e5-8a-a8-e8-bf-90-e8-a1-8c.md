---
title: python小工具——验证*.py更改并自动运行
tags:
  - python
url: 14343.html
id: 14343
categories:
  - Python
date: 2018-05-28 12:22:18
---

这个程序的作用主要是方便开发，要不然平时在vim里写完python的程序需要调试，来回来去的退出，或者切换到另一个终端来运行这个程序比较耗费时间。 所以写了这个小程序 首先读取文件MD5 ，并将其保存。 我们知道，只要文件被修改，那么MD5一定会改变，所以再每间隔一秒钟验证一次新的MD5，如果不一致，那么就执行这个文件。之后更新MD_old

import os
import hashlib
import time
file_name = "1.py"
file\_name = raw\_input("Please input the filename(*.py) :")
os.popen('touch '+file_name)
md5\_old = md5\_before = hashlib.md5(open(file_name).read()).hexdigest()
def checkmd5():
        md5\_now = hashlib.md5(open(file\_name).read()).hexdigest()
        global md5_old
        if md5\_now != md5\_old :
            md5\_old  = md5\_now
            return 1
        return 0
print "Success ! "
while 1:
    time.sleep(1)
    x = checkmd5()
    if x == 1:
        os.system("python "+ file_name)
    if x == 0:
        pass

![](http://blog.echo.cool/wp-content/uploads/2018/05/Capture-15.jpg) 判断文件修改参考如下：

作者：无关风月
链接：https://www.zhihu.com/question/54356152/answer/141533816
来源：知乎
In \[65\]: import hashlib
In \[66\]: md5_before = hashlib.md5(open('a.txt').read()).hexdigest()
In \[67\]: import os
In \[68\]: mtime\_before = os.stat('a.txt').st\_mtime
In \[70\]: !touch a.txt    # touch 会改变mtime，但不会改变内容
In \[71\]: os.stat('a.txt').st\_mtime == mtime\_before
Out\[71\]: False
In \[72\]: hashlib.md5(open('a.txt').read()).hexdigest() == md5_before
Out\[72\]: True
In \[73\]: !echo a >> a.txt  # 改变内容
In \[74\]: os.stat('a.txt').st\_mtime == mtime\_before
Out\[74\]: False
In \[75\]: hashlib.md5(open('a.txt').read()).hexdigest() == md5_before
Out\[75\]: False

改进版：

import os
import hashlib
import time
def checkmd5(file_name):  #检查文件md5
        md5\_now = hashlib.md5(open(file\_name).read()).hexdigest() #获取现在的md5
        global md5_old
        if md5\_now != md5\_old :
            md5\_old  = md5\_now
            return 1
        return 0
def touch_file():
    file_name = ""
    try: #防止键入异常
        while file_name == "" :
            file\_name = raw\_input("Please input the filename(*.py) :").replace('r', '') #读取文件名字符串，并且使用replace替换换行符
    except:
        print ("Please input the right name!")
    if os.path.isfile(file_name) == False:
        fp = open(file_name,'w')
        fp.write("import os nimport math nimport time n ndef main():n    print("Hello World")") #写入部分代码
        fp.write("nnnnif \_\_name\_\_ == "\_\_main\_\_":n    main()")
        print("Succeed make the file !")
    else:    
        print ("The file already exist !")
    global md5_old #全局变量
    md5\_old = hashlib.md5(open(file\_name).read()).hexdigest()
    return file_name
def start\_watch(file\_name):
    print "Success ! "
    while 1:
        time.sleep(2)
        x = checkmd5(file_name) #获取md5是否改变
        if x == 1:
            print("Dected file change ! n")
            print ("Programme start !")
            os.system("python "+ file_name)
            print("program End !")
        if x == 0:
            pass
def main(): #主函数
    start\_watch(touch\_file())
if \_\_name\_\_ == "\_\_main\_\_":
    main()

![](http://blog.echo.cool/wp-content/uploads/2018/05/Screenshot-6.png) ![](http://blog.echo.cool/wp-content/uploads/2018/05/Screenshot-7.png)