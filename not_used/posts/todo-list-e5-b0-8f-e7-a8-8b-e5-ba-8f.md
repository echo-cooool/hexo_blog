---
title: Todo-List小程序
url: 14704.html
id: 14704
categories:
  - Computer
date: 2018-06-17 23:12:02
tags:
---

![](http://blog.echo.cool/wp-content/uploads/2018/06/Screenshot-47-600x338.png)![](http://blog.echo.cool/wp-content/uploads/2018/06/mmexport1529077936045-600x183.png) ![](http://blog.echo.cool/wp-content/uploads/2018/06/Screenshot_20180617-195236-300x600.png)![](http://blog.echo.cool/wp-content/uploads/2018/06/Screenshot_20180617-194511-300x600.png) 2018.7.7 现在的小程序已经完善了许多新功能，其实很多都是借用了百度人工智能的API。 不得不说，模块化开发已经很容易就可以实现 这次是用Flask写的后端。

\# coding: utf-8

import os
from io import BytesIO
import os,base64

from flask import Flask
from flask import redirect
from flask import url_for
from flask import g
from flask import request
from flask import send\_from\_directory
from flask import flash,make_response,Response  
from flask import Markup
from flask import render_template
from werkzeug import Request
import leancloud
import requests
import json  
from views.todos import todos_view
from views.users import users_view
from aip import AipImageClassify
from aip import AipFace
""" 你的 APPID AK SK """
APP_ID = '11470546'
API_KEY = 'hBYWy8rqaABMrkKCdFpNqOaj'
SECRET_KEY = 'Eox3cFvvj2oV0I6OHqufUt4b7yfdYfyK '

client = AipImageClassify(APP\_ID, API\_KEY, SECRET_KEY)
client\_face = AipFace(APP\_ID, API\_KEY, SECRET\_KEY)

app = Flask(\_\_name\_\_)
app.config.update(dict(PREFERRED\_URL\_SCHEME='https'))
try:
    app.secret\_key = bytes(os.environ.get('SECRET\_KEY'), 'utf-8')
except TypeError:
    import sys
    sys.exit('未检测到密钥。请在 LeanCloud 控制台 > 云引擎 > 设置中新增一个名为 SECRET_KEY 的环境变量，再重试部署。')
global cookie_data
cookie\_data = "mmsess=s%3A70opOTJ-kIHh0aI\_RT3RJEOgM5xBwSZr.r2sEk%2BF%2FWID8qnVZomBfKI7U2pmmhHRYgBnzZeAaeR0"
class HTTPMethodOverrideMiddleware(object):
    """
    使用中间件以接受标准 HTTP 方法
    详见：https://gist.github.com/nervouna/47cf9b694842134c41f59d72bd18bd6c
    """

    allowed_methods = frozenset(\['GET', 'HEAD', 'POST', 'PUT', 'DELETE', 'OPTIONS'\])
    bodyless_methods = frozenset(\['GET', 'HEAD', 'DELETE', 'OPTIONS'\])

    def \_\_init\_\_(self, app):
        self.app = app

    def \_\_call\_\_(self, environ, start_response):
        request = Request(environ)
        method = request.args.get('METHOD', '').upper()
        if method in self.allowed_methods:
            method = method.encode('ascii', 'replace')
            environ\['REQUEST_METHOD'\] = method
        if method in self.bodyless_methods:
            environ\['CONTENT_LENGTH'\] = 0
        return self.app(environ, start_response)

\# 注册中间件
app.wsgi\_app = HTTPMethodOverrideMiddleware(app.wsgi\_app)
app.wsgi\_app = leancloud.HttpsRedirectMiddleware(app.wsgi\_app)
app.wsgi\_app = leancloud.engine.CookieSessionMiddleware(app.wsgi\_app, app.secret_key)

\# 动态路由
app.register\_blueprint(todos\_view, url_prefix='/todos')
app.register\_blueprint(users\_view, url_prefix='/users')


@app.before_request
def before_request():
    g.user = leancloud.User.get_current()


@app.route('/')
def index():
    return redirect(url_for('todos.show'))

def Response_headers(content):  
    resp = Response(content)  
    resp.headers\['Access-Control-Allow-Origin'\] = '*'  
    return resp 
@app.route('/help')
def help():
    return render_template('help.html')

@app.route('/cookie',methods=\['GET','POST'\])
def cookie(): 
        global cookie_data
        print(request.form)
        print(request.form.to_dict())
        cookie\_data = request.form.to\_dict()\['cookie'\]
        print (cookie_data) 
        return "New cookie :" + cookie_data

@app.route('/face',methods=\['GET','POST'\])
def face():
    print(request.form)
    url = request.form.to_dict()\['url'\]
    print(url)

    # 将这个图片从内存中打开，然后就可以用Image的方法进行操作了
    """ 如果有可选参数 """
    options = {}
    options\["face_field"\] = "age,beauty,expression,faceshape,gender,glasses,landmark,race,quality,facetype"
    options\["max\_face\_num"\] = 2
    options\["face_type"\] = "LIVE"
    """ 带参数调用人脸检测 """
    imageType = "URL"
    result =client_face.detect(url,imageType,options)
    print("Result:  "+ str(result))
    return str(result).replace("\\'","\\"")

@app.route('/recog_car',methods=\['GET','POST'\])
def recog_car():
    print(request.form)
    url = request.form.to_dict()\['url'\]
    print(url)
    response = requests.get(url) # 将这个图片保存在内存
    # 将这个图片从内存中打开，然后就可以用Image的方法进行操作了
    """ 如果有可选参数 """
    options = {}
    options\["top_num"\] = 7
    """ 带参数调用车辆识别 """
    result =client.carDetect(BytesIO(response.content).read(), options)
    print(result)
    return str(result).replace("\\'","\\"")

@app.route('/app2',methods=\['GET','POST'\])
def app2():
    print(request.form)
    if request.method == 'POST':  
        # POST:
        # request.form获得所有post参数放在一个类似dict类中,to_dict()是字典化
        # 单个参数可以通过request.form.to_dict().get("xxx","")获得
        # ----------------------------------------------------
        # GET:
        # request.args获得所有get参数放在一个类似dict类中,to_dict()是字典化
        # 单个参数可以通过request.args.to_dict().get('xxx',"")获得
        global cookie_data
        headers={
        'Connection': 'keep-alive',
        'Content-Type':'application/json',
        'Cookie': cookie_data,
        }
        print("Headers"+str(headers))
        print(request.form.to_dict())
        data= str(request.form.to_dict()).replace("\\'","\\"")
        data2={"url":"http://www.baihecard.com:8860/?code=Ziv36RTE7ebWBRs159CDt6QgtfcxXjALdpiPV68eCfo#/","usercode":"Ziv36RTE7ebWBRs159CDt6QgtfcxXjALdpiPV68eCfo","agentId":"1000003"}
        print (data)
        data2 = str(data2).replace("\\'","\\"")
        print("Data2 :"+data2)
        auth = requests.post(url = 'http://www.baihecard.com:8870/wxApi/user/check',data=data2,headers= headers)
        d = requests.post(url = 'http://www.baihecard.com:8870/wxPay/reqCardNo',data=data,headers= headers)
        if d.text == "PARAM ERROR":
            d = requests.post(url = 'http://www.baihecard.com:8870/wxApi/wxPay/tradeTest',data=data,headers= headers)
        print(auth.text)
        print(d.text)
        datax = request.form
        content = str(d.text) 
        resp = Response_headers(content)  
        return resp  
    else:  
        content = json.dumps({"error_code":"1001"})  
        resp = Response_headers(content)  
        return resp 
@app.route('/robots.txt')
@app.route('/favicon.svg')
@app.route('/favicon.ico')
def static\_from\_root():
    return send\_from\_directory(app.static_folder, request.path\[1:\])
def get\_file\_content(filePath):
    with open(filePath, 'rb') as fp:
        return fp.read()

网上也都在说，falsk比较适合写API，事实的确如此。 ![](http://blog.echo.cool/wp-content/uploads/2018/06/Screenshot-49.png) ![](http://blog.echo.cool/wp-content/uploads/2018/06/Screenshot-50.png)   2018.7.8 加入了一点Face++的识别功能。 将来可以考虑做一个自动美颜的APP P![](http://blog.echo.cool/wp-content/uploads/2018/06/1.jpg) ![](http://blog.echo.cool/wp-content/uploads/2018/06/2-337x600.jpg) ![](http://blog.echo.cool/wp-content/uploads/2018/06/3-600x324.jpg)

wx.request({
            url: 'https://api-cn.faceplusplus.com/facepp/beta/beautify',
            method: 'POST',
            data: { 
              "api_key": "J8KVbu9ZTqysCqYfyoHkY4xhCN0bXek0",
              "api\_secret": "hjhnnnLWcqGyE9UjJQs\_iAE0lOjcCYd-",
              "image_url": file.url() 
              },
            header: {
              'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8',
            },
            success: function (res) {
              console.log(res.data)
              _this.setData({ listData: res.data });
              var array = wx.base64ToArrayBuffer(res.data.result);
              var base64 = wx.arrayBufferToBase64(array);
              _this.setData({ imageData: 'data:image/jpeg;base64,' + base64 });
              wx.hideLoading();
              
              



            }
          })