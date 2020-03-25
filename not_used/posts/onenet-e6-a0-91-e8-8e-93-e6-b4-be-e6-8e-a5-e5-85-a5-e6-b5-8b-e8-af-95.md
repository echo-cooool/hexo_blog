---
title: OneNet树莓派接入测试
tags:
  - onenet
  - 树莓派
url: 14049.html
id: 14049
categories:
  - 树莓派&amp;Arduino
date: 2018-05-19 14:57:36
---

今天试了一下中国移动的IOT平台，把树莓派的CPU温度和到自己网站的ping值同步了上去： ![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-32.jpg) 接入流程： \[caption id="attachment_14438" align="alignnone" width="661"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-33.jpg)\[/caption\] 我们使用了HTTP协议

> 1 回话方式：HTTP/1.0。HTTP/1.1HTTP-NG。这里只用到了HTTP/1.0和HTTP/1.1。另外一种不清楚。HTTP/1.0
> HTTP/1.0
> 1.1 建立连接-&amp;gt;请求-&amp;gt;响应-&amp;gt;断开连接每次连接只处理一次请求和相应，对资源的每一次访问都要建立一个单独的连接。浏览器到服务器的每次通讯都是完全分开的。没有Host域，所以不可以创建基于主机头的虚拟主机
> HTTP/1.1
> 1.2 在一个TCP连接中可以传送多个HTTP请求和响应不需要等待上次HTTP响应完毕，可以多个HTTP请求同时进行。服务器会根据浏览器发送的请求顺序来按顺序进行响应，这被称作管线。有Host域，可以建立虚拟主机。
> 2\. 请求消息
> 结构：
> 请求行
> 若干消息头(可选)
> 实体内容(可选)
> GET无实体内容
> 3请求方式：
> GET：请求获取Request-URI所标识的资源
> POST：在Request-URI所标识的的资源后附加新的数据
> HEAD：请求获取Request-URI所标识的资源的响应消息报头
> PUT：请求服务器存储一个资源，并用Request-URI作为资源标识
> DELETE：请求服务器删除Request-URI所标识的资源
> TRACE：请求服务器回送收到的请求信息，主要用于测试和诊断
> CONNECT：保留将来使用
> OPTIONS：请求查询服务器的性能，或者查询与资源相关的选项和需求
> ps:一般物联网平台用的比较多的是post和get方法，其他方法很少见。
> 4\. 状态行
> 结构：HTTP版本号_状态码_状态描述(CRLF)如：HTTP/1.1 200 OK
> 5\. 使用GET和POST传递参数
> GET使用URL传递参数
> 如：
> GET /List.aspx?Catagoryid=5&amp;amp;Cityid=23 HTTP/1.1
> POST使用实体内容传递参数
> 如：
> POST /List.aspx HTTP/1.1
> Content-Type:application/x-www-form-urlencoded
> Content-Length:22
> Catagoryid=5&amp;amp;Cityid=23
> 在POST消息头中要设置Content-Type的值为application/x-www-form-urlencoded，以及使用Content-Length 以标识实体内容的长度。
> 当Content-Length长度比实体内容长度短时，则会忽略多出部分的实体内容。当Content-Length少于实体长度时，则会继续等待。
> 6 响应状态码
> 状态代码由三位数字组成，第一位定义了响应的类别：
> 1xx:指示信息&amp;mdash;&amp;mdash;表示请求已接收，继续处理。
> 2xx:成功&amp;mdash;&amp;mdash;表示请求已被成功接收、理解、接受。
> 3xx:重定向&amp;mdash;&amp;mdash;要完成请求必须进行更进一步的操作。
> 4xx:客户端错误&amp;mdash;&amp;mdash;请求有语法错误或请求无法实现。
> 5xx:服务器端错误&amp;mdash;&amp;mdash;服务器未能实现合法的请求。
> 200 OK 客户端请求成功
> 206 客户端发送了带有Range头的GET请求，服务器正确的返回了该范围的数据
> 302/307 指出被请求的文档已经临时移动到别处，此文档的新的URL在Location响应头中给出
> 304 客户机缓存的版本是最新的，客户机应该继续使用它
> 400 Bad Request 客户端请求有语法错误，不能被服务器理解
> 401 Unauthorized 表示客户机访问的是一个受口令和密码保护的页面，并且在WWW-Authenticate响应头提示客户机应重新发出一个带有Authorization头的请求信息。
> 403 Forbidden服务器收到请求，但是拒绝提供服务
> 404 Not Found 请求的资源不存在
> 500 Internal Server Error服务器端的CGI、ASP、JSP发生错误
> 503 Server Unavaliable服务器当前不能处理客户端的请求，一段时间后可能恢复正常
> ps:转载自：http://www.cnblogs.com/YinWangLive/archive/2009/04/10/1433330.html
> 看到这些基本了解到用串口助手发送数据回来400/404/500 等错误信息的基本含义了。但协议本身有有些迷糊，错误信息怎么找到了，最重要的方法还是看文档，然后依据文档的方法调试。以下是我调试好的数据包，大家可以看下。
> 1 数据流
> 1.1数据流上传
> POST /devices/680869/datapoints HTTP/1.1
> api-key: bryNFvy6sbj9Isu5mHXp3fwIvtc=
> Host:api.heclouds.com
> Connection:close
> Content-Length:59
> {"datastreams":\[{"id":"temp","datapoints":\[{"value":50}\]}\]}
> ps:这是默认的数据流上传方式。如果想要长连接Connection:close 这句要删除，HTTP/1.1这里要写。如果写HTTP/1.0就是发送一次数据然后网站就断开连接了。
> 如果想要简化数据包，需要在头文件修改数据包传输协议。我这里选择方式3 。POST /devices/680869/datapoints?type=3 HTTP/1.1
> 1.2发送一个设备上的N个数据流
> POST /devices/680869/datapoints?type=3 HTTP/1.1
> api-key: bryNFvy6sbj9Isu5mHXp3fwIvtc=
> Host:api.heclouds.com
> Connection:close
> Content-Length:23
> {"shidu":22,"wendu":22}
> ps: Content-Length:23 后的换行符号一定要。{"shidu":22,"wendu":22} 后的换行符可以不要，但尽量使用换行符，这是个习惯问题。23是指数据包{"shidu":22,"wendu":22}的字符数字，汉字也遵循相似的规则，字符的长度不包括前后的换行符，数字的大小谨慎使用。比如改为22会出现如下效果
> 12:32:52 收到数据：HTTP/1.1 200 OK
> Date: Wed, 04 May 2016 04:32:34 GMT
> Content-Type: application/json
> Content-Length: 34
> Connection: close
> Server: Apache-Coyote/1.1
> Pragma: no-cache
> {"errno":4,"error":"invalid JSON"}
> 数据长度改为24,25没有问题，但改为26，服务器就没有反应了。个人猜测网站设计时，一段HTTP协议发送完成后允许换行和不换行共存，23-25长度下数据均可正常上传，这是网站设计时考虑的一些使用者习惯问题。
> 1.3发送一个设备上的N个数据流例2
> 当然一次上传可以上传某项目中的一个设备的N个数据流。跨项目这是不行的，因为APIKEY不一致。跨设备好像不行，没有仔细研究。下面介绍我的上传开关信息http协议
> POST /devices/680872/datapoints?type=3 HTTP/1.1 api-key: vUAoLurFOH=xkqr9s7w4dXuXBGY=
> Host:api.heclouds.com
> Connection:close
> Content-Length:42
> {"taideng":0,"diandengl":0,"diandeng2":1}
> 返回的数据如下：
> 12:45:46 收到数据：HTTP/1.1 200 OK
> Date: Wed, 04 May 2016 04:45:28 GMTContent-Type: application/json
> Content-Length: 26
> Connection: close
> Server: Apache-Coyote/1.1
> Pragma: no-cache
> {"errno":0,"error":"succ"}
> 2 除了上传数据之外，还需要获取数据，比如改变了开关值，设备需要主动获取开关值，设备才可以达到远程控制的目的。
> 2.1获取设备多个数据流
> GET /devices/680872/datastreams HTTP/1.1
> api-key: vUAoLurFOH=xkqr9s7w4dXuXBGY=
> Host:api.heclouds.com
> Connection:close
> 返回的数据如下：
> {"errno":0,"data":\[{"create\_time":"2016-01-14 09:34:17","update\_at":"2016-05-04 12:45:28","id":"taideng","uuid":"f498ffdb-b639-5596-9081-90072c4396d3","current\_value":0},{"create\_time":"2016-01-13 20:01:27","update\_at":"2016-05-02 22:40:09","id":"diandeng1","uuid":"0486063b-0e01-5e1b-a21d-bd9a90347d43","current\_value":0},{"create\_time":"2016-01-14 09:34:24","update\_at":"2016-05-04 12:45:28","id":"diandeng2","uuid":"a551ca79-4fb4-542c-84a0-3537ecf84875","current\_value":1},{"create\_time":"2016-05-04 10:09:22","update\_at":"2016-05-04 12:45:28","id":"diandengl","uuid":"5e0ba4db-e85e-4d8e-b706-4e04e88bf8bb","current\_value":0}\],"error":"succ"}
> ps:Connection:close 后面要加两个换行符，否则服务器没有响应的。
> 2.2 读取设备单个数据流
> GET /devices/680872/datastreams/taideng HTTP/1.1
> api-key: vUAoLurFOH=xkqr9s7w4dXuXBGY=
> Host:api.heclouds.com
> Connection:close
> 返回数据
> Date: Wed, 04 May 2016 04:54:26 GMT
> Content-Type: application/json
> Content-Length: 138
> Connection: close
> Server: Apache-Coyote/1.1
> Pragma: no-cache
> {"errno":0,"data":{"create\_time":"2016-01-14 09:34:17","update\_at":"2016-05-04 12:45:28","id":"taideng","current_value":0},"error":"succ"}
> 3 设备
> 这里我觉得设备和数据流没有什么区别，只是方便app,微信开发的，省去网站注册麻烦。这里就略过。但还是要写下我的笔记。
> 3.1读取多个设备
> GET /devices HTTP/1.1
> api-key: vUAoLurFOH=xkqr9s7w4dXuXBGY=
> Host:api.heclouds.com
> Connection:close
> 返回数据：
> {"errno":0,"data":{"per\_page":30,"devices":\[{"private":false,"protocol":"HTTP","create\_time":"2016-01-15 08:20:35","location":{"lon":114.39322112330001,"lat":30.508559475486003},"id":"680997","auth\_info":{"SYS":"WYfjhCGqU2ks4ltBQe02kkWTYxE="},"title":"鐢电伅鎺у埗2","desc":"瀹ゅ鐢电伅鎺у埗","tags":\["瀹ゅ鐢电伅鎺у埗"\]},{"private":false,"protocol":"HTTP","create\_time":"2016-01-13 19:59:02","location":{"lon":114.45659857426999,"lat":30.470787904259},"auth\_info":{"SYS":"Sonv4XxoF68E82739gfef1NTu3g="},"id":"680872","title":"鐢电伅","desc":"鐢电伅","tags":\["鐢电伅鐘舵&amp;euro;?\]}\],"total\_count":2,"page":1},"error":"succ"}
> 3.2读取单个设备具体信息
> Date: Wed, 04 May 2016 05:01:05 GMT
> Content-Type: application/json
> Content-Length: 140
> Connection: close
> Server: Apache-Coyote/1.1
> Pragma: no-cache
> {"errno":0,"data":\[{"create\_time":"2016-01-14 09:34:17","update\_at":"2016-05-04 12:45:28","id":"taideng","current_value":0}\],"error":"succ"}
> 3.3读取触发器 温度高触发器
> GET /triggers/11608 HTTP/1.1
> api-key: bryNFvy6sbj9Isu5mHXp3fwIvtc=
> Host:api.heclouds.com
> Connection:close
> 返回数据：
> Date: Wed, 04 May 2016 05:02:41 GMT
> Content-Type: application/json
> Content-Length: 191
> Connection: close
> Server: Apache-Coyote/1.1
> Pragma: no-cache
> {"errno":0,"data":{"invalid":true,"dev\_ids":\["680869"\],"threshold":20,"id":11608,"title":"hightemp","type":"&amp;gt;=","ds\_id":"wendu","url":"http://api.heclouds.com/devices/680869"},"error":"succ"}
> 3.4读触发器。电灯1触发器
> GET /triggers/11610 HTTP/1.1
> api-key: vUAoLurFOH=xkqr9s7w4dXuXBGY=
> Host:api.heclouds.com
> Connection:close
> 返回数据：
> Date: Wed, 04 May 2016 05:04:17 GMT
> Content-Type: application/json
> Content-Length: 171
> Connection: close
> Server: Apache-Coyote/1.1
> Pragma: no-cache
> {"errno":0,"data":{"dev\_ids":\["680872"\],"id":11610,"title":"寮&amp;euro;鐢电伅1","type":"change","ds\_id":"diandeng1","url":"http://api.heclouds.com/devices/680872"},"error":"succ"}
> 3.5获取数据点
> GET /devices/680869/datapoints HTTP/1.1
> api-key: bryNFvy6sbj9Isu5mHXp3fwIvtc=
> Host:api.heclouds.com
> Connection:close
> 返回数据
> Date: Wed, 04 May 2016 05:04:17 GMT
> Content-Type: application/json
> Content-Length: 209
> Connection: close
> Server: Apache-Coyote/1.1
> Pragma: no-cache
> {"errno":0,"data":{"count":2,"datastreams":\[{"datapoints":\[{"at":"2016-05-04 13:05:05.701","value":19}\],"id":"shidu"},{"datapoints":\[{"at":"2016-05-04 13:05:05.704","value":30}\],"id":"wendu"}\]},"error":"succ"}
> 4二进制
> 4.1上传二进制
> POST /bindata?device\_id=1078739&amp;amp;datastream\_id=ir HTTP/1.1
> api-key: bryNFvy6sbj9Isu5mHXp3fwIvtc=
> Host:api.heclouds.com
> Content-Length:1
> 0
> 13:08:05 收到数据：HTTP/1.1 200 OK
> Date: Wed, 04 May 2016 05:07:47 GMT
> Content-Type: application/json
> Content-Length: 70
> Connection: keep-alive
> Server: Apache-Coyote/1.1
> Pragma: no-cache
> {"errno":0,"data":{"index":"1078739\_1462338467786\_ir"},"error":"succ"}
> ps:收到的数据中我可能忘了把一些附加信息粘贴上去，但这不影响效果。
> 5历史数据
> 读取历史数据：
> GET /datapoints?start=2015-12-02T14:01:46&amp;amp;device_id=978118&amp;amp;limit=6000 HTTP/1.1
> api-key: bryNFvy6sbj9Isu5mHXp3fwIvtc=
> Host:api.heclouds.com
> Connection:close
> 返回数据：
> {"errno":0,"data":{"datapoints":\[{"at":"2016-03-28 09:41:52.278","ds\_id":"temp2","value":22,"dev\_id":"978118"},{"at":"2016-04-19 19:58:56.147","ds\_id":"temp2","value":22,"dev\_id":"978118"},{"at":"2016-05-04 10:40:42.551","ds\_id":"temp2","value":22,"dev\_id":"978118"},{"at":"2016-03-28 09:41:52.281","ds\_id":"temp1","value":22,"dev\_id":"978118"},{"at":"2016-04-19 19:58:56.150","ds\_id":"temp1","value":22,"dev\_id":"978118"},{"at":"2016-05-04 10:40:42.558","ds\_id":"temp1","value":22,"dev\_id":"978118"}\],"count":6},"error":"succ"}

\# -*- coding:utf-8 -*-
\# File: cputemp.py
#向平台已经创建的数据流发送数据点
import urllib2
import json
import time
import datetime
import os
APIKEY = 'JoMs4Homyc0tyOyGTLLsms1Ypfs='  #改成你的APIKEY

def get_ping():
        a = os.popen("ping ssr.gsssr.space -c 1").readlines()

        print a\[1\].split()\[7\].split("=")\[1\]
        return a\[1\].split()\[7\].split("=")\[1\]
def get_temp():
        # 打开文件
        file = open("/sys/class/thermal/thermal_zone0/temp")
        # 读取结果，并转换为浮点数
        temp = float(file.read()) / 1000
        # 关闭文件
        file.close()
        # 向控制台打印结果
        print "CPU的温度值为: %.3f" %temp
        # 返回温度值
        return temp


def http_put(id,num):
    CurTime = datetime.datetime.now()
    url='http://api.heclouds.com/devices/31322507/datapoints'
    values={'datastreams':\[{"id":id,"datapoints":\[{"at":CurTime.isoformat(),"value":num}\]}\]}

    print "当前的ISO时间为： %s" %CurTime.isoformat()
    print "上传的数据值为: " + str(num)

    jdata = json.dumps(values)                  # 对数据进行JSON格式化编码
    #打印json内容
    print jdata
    request = urllib2.Request(url, jdata)
    request.add_header('api-key', APIKEY)
    request.get_method = lambda:'POST'          # 设置HTTP的访问方式
    request = urllib2.urlopen(request)
    return request.read()

while True:
 try:
        temperature = get_temp()
        resp = http_put("temp",temperature)
        print "TEMP OneNET请求结果:\\n %s" %resp
        time.sleep(5)
        ping = get_ping()
        resp = http_put("ping",ping)
        print "TEMP OneNET请求结果:\\n %s" %resp
 except:
        print "ERROR"