---
title: 会考成绩查询程序Python
url: 15067.html
id: 15067
categories:
  - Computer
  - Python
date: 2019-02-02 19:57:45
tags:
---

因为想查一查年级的会考成绩 ，所以就写了这个程序 之前一直比较头疼的验证码，这次用了一个若快的平台解决了。 现在主要看一看代码，平台就不介绍了。 首先，通过获取到目标页的cookie来进行下一步操作，这个主要是因为bjeea是通过cookie来表示用户的访问的，这样我们在后期维持这个cookie就可以验证我们的验证码是否正确

    def get_cookie():
        res = requests.get(url = http://query.bjeea.cn/queryService/rest/score/131)
        cookies = res.cookies
        print(cookies)
        return cookies

之后 用这个cookie去获取一个验证码，这里同时进行了识别操作rc.rk_create(im, 1040)\[\\'Result\\'\]直接取回了字符类型的验证码识别结果。

    def get_captha(cookies):
        rc = RClient('w1109790800', 'Lkq2mapp',)
        res = requests.get(url = http://query.bjeea.cn/captcha.jpg,cookies = cookies,headers = header)
        image = Image.open(BytesIO(res.content))
        img = image
        img.save(upload.jpg)
        im = open('upload.jpg', 'rb').read()
        captha = rc.rk_create(im, 1040)['Result']
        print(captha)
        return captha

接下来就可以构造请求 查询这一个人的分数了，同时写入一个文件。

    def get_score(id_s,name):
        name = str(name.encode('utf-8')).replace(\\x,%).replace("\'",).replace("\'",)
        print(name)
        cookies = get_cookie()
        captha = get_captha(cookies)
        data = modeId=101&examId=5170&reportNo=+str(id_s)+&name=+name+&captcha=+str(captha)
        res=requests.post(url = http://query.bjeea.cn/queryService/rest/score/101 ,cookies = cookies,data = data,headers = header)
        if res.text != {\error\:\您输入的验证码错误,请刷新后重新输入.\}:
            process(res.text) 
    def process(res):
        res = json.loads(res)
        name = res['name']
        print(name)
        for i in range(0,3):
            score = res[huiKaoList][i][kmcj]
            score_name = res[huiKaoList][i][kmmc]
            with open(1.csv, 'a', newline='') as file:
                 csv_file = csv.writer(file)
                 csv_file.writerow([name,score_name,score])
            print(name,score_name,score)

在主函数这里，为了减少识别错误，我们对于失败的识别再试一次：

    def main():
        with open(3.csv) as f:
            reader = csv.reader(f)
            for row in reader:
                try:
                    get_score(row[0],row[1])
                except:
                    pass

这样，我们就得到了成绩的文件。 ![](http://blog.echo.cool/wp-content/uploads/2019/02/Capture-1024x605.jpg)

再附带一个完整程序：

    # -*- coding: UTF-8 -*-
    import requests
    import json
    from PIL import Image
    import sys, os, random, urllib
    import urllib.request
    from hashlib import md5
    from datetime import *
    from io import BytesIO
    import csv
    header={
            User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36,
            Content-Type: application/x-www-form-urlencoded; charset=UTF-8,
            Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7
        }
    
    class RClient(object):
    
        def __init__(self, username, password):
            self.username = username
            try:
                self.password = md5(password).hexdigest()
            except TypeError:
                self.password = md5(password.encode('utf-8')).hexdigest()
            self.soft_id = '121813'
            self.soft_key = 'd80c84e377d5435484ffa00d376d23bb'
            self.base_params = {
                'username': self.username,
                'password': self.password,
                'softid': self.soft_id,
                'softkey': self.soft_key,
            }
            self.headers = {
                'Connection': 'Keep-Alive',
                'Expect': '100-continue',
                'User-Agent': 'ben',
            }
    
        def rk_create(self, im, im_type, timeout=60):
            im: 图片字节
            im_type: 题目类型
            params = {
                'typeid': im_type,
                'timeout': timeout,
            }
            params.update(self.base_params)
            files = {'image': ('a.jpg', im)}
            r = requests.post('http://api.ruokuai.com/create.json', data=params, files=files, headers=self.headers)
            print(r)
            return r.json()
    
        def rk_report_error(self, im_id):
            im_id:报错题目的ID
            params = {
                'id': im_id,
            }
            params.update(self.base_params)
            r = requests.post('http://api.ruokuai.com/reporterror.json', data=params, headers=self.headers)
            return r.json()
    
    def get_captha(cookies):
        rc = RClient('w1109790800', 'Lkq2mapp',)
        res = requests.get(url = http://query.bjeea.cn/captcha.jpg,cookies = cookies,headers = header)
        image = Image.open(BytesIO(res.content))
        img = image
        img.save(upload.jpg)
        im = open('upload.jpg', 'rb').read()
        captha = rc.rk_create(im, 1040)['Result']
        print(captha)
        return captha
    def get_cookie():
        res = requests.get(url = http://query.bjeea.cn/queryService/rest/score/131)
        cookies = res.cookies
        print(cookies)
        return cookies
    def get_score(id_s,name):
        name = str(name.encode('utf-8')).replace(\\x,%).replace("\'",).replace("\'",)
        print(name)
        cookies = get_cookie()
        captha = get_captha(cookies)
        data = modeId=101&examId=5170&reportNo=+str(id_s)+&name=+name+&captcha=+str(captha)
        res=requests.post(url = http://query.bjeea.cn/queryService/rest/score/101 ,cookies = cookies,data = data,headers = header)
        if res.text != {\error\:\您输入的验证码错误,请刷新后重新输入.\}:
            process(res.text) 
    def process(res):
        res = json.loads(res)
        name = res['name']
        print(name)
        for i in range(0,3):
            score = res[huiKaoList][i][kmcj]
            score_name = res[huiKaoList][i][kmmc]
            with open(1.csv, 'a', newline='') as file:
                 csv_file = csv.writer(file)
                 csv_file.writerow([name,score_name,score])
            print(name,score_name,score)
    def main():
        with open(3.csv) as f:
            reader = csv.reader(f)
            for row in reader:
                try:
                    get_score(row[0],row[1])
                except:
                    pass
    main()